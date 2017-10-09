---
title: "SQL 資料倉儲中的 aaaConcurrency 和工作負載管理 |Microsoft 文件"
description: "了解 Azure SQL 資料倉儲中的並行存取和工作負載管理以開發解決方案。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="055fd-103">SQL 資料倉儲中的並行存取和工作負載管理</span><span class="sxs-lookup"><span data-stu-id="055fd-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="055fd-104">Microsoft Azure SQL 資料倉儲大規模 toodeliver 可預測的效能可協助您控制並行層級和資源配置，例如記憶體和 CPU 優先順序。</span><span class="sxs-lookup"><span data-stu-id="055fd-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="055fd-105">本文介紹 toohello 概念的並行存取，以及工作負載的管理，說明已實作這兩種功能，以及如何控制這些資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="055fd-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="055fd-106">支援多使用者環境的預定的 toohelp SQL 資料倉儲工作負載管理。</span><span class="sxs-lookup"><span data-stu-id="055fd-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="055fd-107">它並不適用於多租用戶工作負載。</span><span class="sxs-lookup"><span data-stu-id="055fd-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="055fd-108">並行存取限制</span><span class="sxs-lookup"><span data-stu-id="055fd-108">Concurrency limits</span></span>
<span data-ttu-id="055fd-109">SQL 資料倉儲可讓向上 too1，024 並行連線。</span><span class="sxs-lookup"><span data-stu-id="055fd-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="055fd-110">這 1,024 個連線全都可以並行提交查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="055fd-111">不過，SQL 資料倉儲 toooptimize 輸送量可能排入佇列，每個查詢所接收的最小記憶體授與某些查詢 tooensure。</span><span class="sxs-lookup"><span data-stu-id="055fd-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="055fd-112">佇列會在查詢執行時發生。</span><span class="sxs-lookup"><span data-stu-id="055fd-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="055fd-113">佇列的查詢時可以提高的並行到達限制，SQL 資料倉儲總輸送量，方法是確保作用中的查詢取得存取 toocritically 所需的記憶體資源。</span><span class="sxs-lookup"><span data-stu-id="055fd-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="055fd-114">並行存取限制受到兩個概念所控制：「並行查詢」和「並行存取插槽」。</span><span class="sxs-lookup"><span data-stu-id="055fd-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="055fd-115">針對查詢 tooexecute，它必須在 hello 查詢並行限制和 hello 並行位置配置內執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="055fd-116">並行的查詢是執行在 hello 相同的 hello 查詢時間。</span><span class="sxs-lookup"><span data-stu-id="055fd-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="055fd-117">SQL 資料倉儲支援 too32 hello 較大的 DWU 大小上的並行查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="055fd-118">並行存取插槽是根據 DWU 所配置。</span><span class="sxs-lookup"><span data-stu-id="055fd-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="055fd-119">每 100 個 DWU 提供 4 個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="055fd-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="055fd-120">例如，DW100 會配置 4 個並行存取插槽，而 DW1000 會配置 40 個。</span><span class="sxs-lookup"><span data-stu-id="055fd-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="055fd-121">每個查詢取用一或多個並行 [插槽]，相依於 hello[資源類別](#resource-classes)的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="055fd-122">Hello smallrc 資源類別中執行的查詢取用一個並行存取的位置。</span><span class="sxs-lookup"><span data-stu-id="055fd-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="055fd-123">較高資源類別中執行的查詢會使用更多的並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="055fd-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="055fd-124">hello 以下表格說明 hello 限制的並行查詢和在 hello 並行插槽各種 DWU 大小。</span><span class="sxs-lookup"><span data-stu-id="055fd-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="055fd-125">並行存取限制</span><span class="sxs-lookup"><span data-stu-id="055fd-125">Concurrency limits</span></span>
| <span data-ttu-id="055fd-126">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-126">DWU</span></span> | <span data-ttu-id="055fd-127">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="055fd-127">Max concurrent queries</span></span> | <span data-ttu-id="055fd-128">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="055fd-129">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-129">DW100</span></span> |<span data-ttu-id="055fd-130">4</span><span class="sxs-lookup"><span data-stu-id="055fd-130">4</span></span> |<span data-ttu-id="055fd-131">4</span><span class="sxs-lookup"><span data-stu-id="055fd-131">4</span></span> |
| <span data-ttu-id="055fd-132">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-132">DW200</span></span> |<span data-ttu-id="055fd-133">8</span><span class="sxs-lookup"><span data-stu-id="055fd-133">8</span></span> |<span data-ttu-id="055fd-134">8</span><span class="sxs-lookup"><span data-stu-id="055fd-134">8</span></span> |
| <span data-ttu-id="055fd-135">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-135">DW300</span></span> |<span data-ttu-id="055fd-136">12</span><span class="sxs-lookup"><span data-stu-id="055fd-136">12</span></span> |<span data-ttu-id="055fd-137">12</span><span class="sxs-lookup"><span data-stu-id="055fd-137">12</span></span> |
| <span data-ttu-id="055fd-138">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-138">DW400</span></span> |<span data-ttu-id="055fd-139">16</span><span class="sxs-lookup"><span data-stu-id="055fd-139">16</span></span> |<span data-ttu-id="055fd-140">16</span><span class="sxs-lookup"><span data-stu-id="055fd-140">16</span></span> |
| <span data-ttu-id="055fd-141">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-141">DW500</span></span> |<span data-ttu-id="055fd-142">20</span><span class="sxs-lookup"><span data-stu-id="055fd-142">20</span></span> |<span data-ttu-id="055fd-143">20</span><span class="sxs-lookup"><span data-stu-id="055fd-143">20</span></span> |
| <span data-ttu-id="055fd-144">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-144">DW600</span></span> |<span data-ttu-id="055fd-145">24</span><span class="sxs-lookup"><span data-stu-id="055fd-145">24</span></span> |<span data-ttu-id="055fd-146">24</span><span class="sxs-lookup"><span data-stu-id="055fd-146">24</span></span> |
| <span data-ttu-id="055fd-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-147">DW1000</span></span> |<span data-ttu-id="055fd-148">32</span><span class="sxs-lookup"><span data-stu-id="055fd-148">32</span></span> |<span data-ttu-id="055fd-149">40</span><span class="sxs-lookup"><span data-stu-id="055fd-149">40</span></span> |
| <span data-ttu-id="055fd-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-150">DW1200</span></span> |<span data-ttu-id="055fd-151">32</span><span class="sxs-lookup"><span data-stu-id="055fd-151">32</span></span> |<span data-ttu-id="055fd-152">48</span><span class="sxs-lookup"><span data-stu-id="055fd-152">48</span></span> |
| <span data-ttu-id="055fd-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-153">DW1500</span></span> |<span data-ttu-id="055fd-154">32</span><span class="sxs-lookup"><span data-stu-id="055fd-154">32</span></span> |<span data-ttu-id="055fd-155">60</span><span class="sxs-lookup"><span data-stu-id="055fd-155">60</span></span> |
| <span data-ttu-id="055fd-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-156">DW2000</span></span> |<span data-ttu-id="055fd-157">32</span><span class="sxs-lookup"><span data-stu-id="055fd-157">32</span></span> |<span data-ttu-id="055fd-158">80</span><span class="sxs-lookup"><span data-stu-id="055fd-158">80</span></span> |
| <span data-ttu-id="055fd-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-159">DW3000</span></span> |<span data-ttu-id="055fd-160">32</span><span class="sxs-lookup"><span data-stu-id="055fd-160">32</span></span> |<span data-ttu-id="055fd-161">120</span><span class="sxs-lookup"><span data-stu-id="055fd-161">120</span></span> |
| <span data-ttu-id="055fd-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-162">DW6000</span></span> |<span data-ttu-id="055fd-163">32</span><span class="sxs-lookup"><span data-stu-id="055fd-163">32</span></span> |<span data-ttu-id="055fd-164">240</span><span class="sxs-lookup"><span data-stu-id="055fd-164">240</span></span> |

<span data-ttu-id="055fd-165">當符合以上其中一個臨界值時，新的查詢將以先進先出順序排入佇列和執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="055fd-166">完成查詢與 hello 查詢和插槽數目低於 hello 限制時，會發行排入佇列的查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="055fd-167">*選取*以獨佔方式在執行的查詢動態管理檢視 (Dmv)，或目錄檢視都未受到任何 hello 並行存取限制。</span><span class="sxs-lookup"><span data-stu-id="055fd-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="055fd-168">您可以監視 hello 系統，無論 hello 在其上執行的查詢數目。</span><span class="sxs-lookup"><span data-stu-id="055fd-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="055fd-169">資源類別</span><span class="sxs-lookup"><span data-stu-id="055fd-169">Resource classes</span></span>
<span data-ttu-id="055fd-170">資源類別可協助您控制記憶體配置和給定 tooa 查詢的 CPU 循環。</span><span class="sxs-lookup"><span data-stu-id="055fd-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="055fd-171">您可以指派兩種類型的資料庫角色的 hello 表單中的資源類別 tooa 使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="055fd-172">兩種類型的資源類別，如下所示為 hello:</span><span class="sxs-lookup"><span data-stu-id="055fd-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="055fd-173">動態資源類別 (**smallrc，mediumrc，largerc，xlargerc**) 配置的記憶體，根據 hello 以變數目前的 DWU。</span><span class="sxs-lookup"><span data-stu-id="055fd-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="055fd-174">這表示當您向上擴充 tooa 較大的 DWU，查詢會自動取得更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="055fd-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="055fd-175">靜態資源類別 (**staticrc10，staticrc20，staticrc30，staticrc40，staticrc50，staticrc60，staticrc70，staticrc80**) 配置 hello 相同數量的記憶體，不論 hello 目前的 DWU (前提是 hello DWU 本身有足夠的記憶體）。</span><span class="sxs-lookup"><span data-stu-id="055fd-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="055fd-176">這表示在較大的 DWU 中，您將可以在每個資源類別中同時執行更多查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="055fd-177">採用 **smallrc** 和 **staticrc10** 的使用者會獲得較小量的記憶體，且可利用較高的並行存取能力。</span><span class="sxs-lookup"><span data-stu-id="055fd-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="055fd-178">相反地，使用者指派太**xlargerc**或**staticrc80**有大量的記憶體，並因此更少的查詢可以同時執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="055fd-179">根據預設，每個使用者都 hello 小型資源類別的成員**smallrc**。</span><span class="sxs-lookup"><span data-stu-id="055fd-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="055fd-180">hello 程序`sp_addrolemember`是使用 tooincrease hello 資源類別，和`sp_droprolemember`是使用 toodecrease hello 資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="055fd-181">例如，此命令將會增加 hello 資源類別的 loaduser 太**largerc**:</span><span class="sxs-lookup"><span data-stu-id="055fd-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="055fd-182">不採用資源類別的查詢</span><span class="sxs-lookup"><span data-stu-id="055fd-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="055fd-183">有幾種查詢類別不會因較大的記憶體配置而受益。</span><span class="sxs-lookup"><span data-stu-id="055fd-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="055fd-184">hello 系統會忽略其資源類別配置，並一律改為在 hello 小型資源類別中執行這些查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="055fd-185">如果在 hello 小型資源類別中永遠執行這些查詢，可以執行並行位置有不足的壓力，而且它們不會使用比所需的多個位置。</span><span class="sxs-lookup"><span data-stu-id="055fd-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="055fd-186">如需詳細資訊，請參閱 [資源類別例外狀況](#query-exceptions-to-concurrency-limits) 。</span><span class="sxs-lookup"><span data-stu-id="055fd-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="055fd-187">資源類別指派的詳細資料</span><span class="sxs-lookup"><span data-stu-id="055fd-187">Details on resource class assignment</span></span>


<span data-ttu-id="055fd-188">資源類別的其他詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="055fd-188">A few more details on resource class:</span></span>

* <span data-ttu-id="055fd-189">*更改角色*需要的權限的使用者 toochange hello 資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="055fd-190">雖然您可以新增使用者 tooone 或多個 hello 較高的資源類別，動態資源類別的優先順序高於靜態資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="055fd-191">也就是說，如果使用者被指派 tooboth **mediumrc**（動態） 和**staticrc80**（靜態） **mediumrc**是 hello 資源類別，才會被接受。</span><span class="sxs-lookup"><span data-stu-id="055fd-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="055fd-192">當使用者獲指派 toomore 比特定的資源類別類型 （多個動態資源類別或多個靜態資源類別） 中的一項資源類別時，被採用 hello 最高的資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="055fd-193">也就是如果 tooboth mediumrc 與 largerc，則指派給使用者，被適用於高資源類別 hello (largerc)。</span><span class="sxs-lookup"><span data-stu-id="055fd-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="055fd-194">如果使用者獲指派 tooboth **staticrc20**和**statirc80**， **staticrc80**會接受。</span><span class="sxs-lookup"><span data-stu-id="055fd-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="055fd-195">無法變更 hello 系統管理使用者的 hello 資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="055fd-196">如需詳細範例，請參閱 [變更使用者資源類別的範例](#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="055fd-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="055fd-197">記憶體配置</span><span class="sxs-lookup"><span data-stu-id="055fd-197">Memory allocation</span></span>
<span data-ttu-id="055fd-198">有優缺點 tooincreasing 使用者的資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="055fd-199">增加使用者的資源類別，提供其查詢存取 toomore 記憶體，這可能表示查詢執行的速度。</span><span class="sxs-lookup"><span data-stu-id="055fd-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="055fd-200">不過，較高的資源類別也會減少 hello 可以執行的並行查詢數目。</span><span class="sxs-lookup"><span data-stu-id="055fd-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="055fd-201">這是 hello 配置大量記憶體 tooa 單一查詢，或允許其他查詢，也需要記憶體配置，同時 toorun 之間的取捨。</span><span class="sxs-lookup"><span data-stu-id="055fd-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="055fd-202">一位使用者指定高配置記憶體的查詢，如果其他使用者將不會存取 toothat 相同記憶體 toorun 查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="055fd-203">下表中的 hello 對應 hello 記憶體配置 tooeach 發佈 DWU 和資源的類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="055fd-204">每個散發套件的動態資源類別 (MB) 記憶體配置</span><span class="sxs-lookup"><span data-stu-id="055fd-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="055fd-205">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-205">DWU</span></span> | <span data-ttu-id="055fd-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="055fd-206">smallrc</span></span> | <span data-ttu-id="055fd-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="055fd-207">mediumrc</span></span> | <span data-ttu-id="055fd-208">largerc</span><span class="sxs-lookup"><span data-stu-id="055fd-208">largerc</span></span> | <span data-ttu-id="055fd-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="055fd-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="055fd-210">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-210">DW100</span></span> |<span data-ttu-id="055fd-211">100</span><span class="sxs-lookup"><span data-stu-id="055fd-211">100</span></span> |<span data-ttu-id="055fd-212">100</span><span class="sxs-lookup"><span data-stu-id="055fd-212">100</span></span> |<span data-ttu-id="055fd-213">200</span><span class="sxs-lookup"><span data-stu-id="055fd-213">200</span></span> |<span data-ttu-id="055fd-214">400</span><span class="sxs-lookup"><span data-stu-id="055fd-214">400</span></span> |
| <span data-ttu-id="055fd-215">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-215">DW200</span></span> |<span data-ttu-id="055fd-216">100</span><span class="sxs-lookup"><span data-stu-id="055fd-216">100</span></span> |<span data-ttu-id="055fd-217">200</span><span class="sxs-lookup"><span data-stu-id="055fd-217">200</span></span> |<span data-ttu-id="055fd-218">400</span><span class="sxs-lookup"><span data-stu-id="055fd-218">400</span></span> |<span data-ttu-id="055fd-219">800</span><span class="sxs-lookup"><span data-stu-id="055fd-219">800</span></span> |
| <span data-ttu-id="055fd-220">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-220">DW300</span></span> |<span data-ttu-id="055fd-221">100</span><span class="sxs-lookup"><span data-stu-id="055fd-221">100</span></span> |<span data-ttu-id="055fd-222">200</span><span class="sxs-lookup"><span data-stu-id="055fd-222">200</span></span> |<span data-ttu-id="055fd-223">400</span><span class="sxs-lookup"><span data-stu-id="055fd-223">400</span></span> |<span data-ttu-id="055fd-224">800</span><span class="sxs-lookup"><span data-stu-id="055fd-224">800</span></span> |
| <span data-ttu-id="055fd-225">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-225">DW400</span></span> |<span data-ttu-id="055fd-226">100</span><span class="sxs-lookup"><span data-stu-id="055fd-226">100</span></span> |<span data-ttu-id="055fd-227">400</span><span class="sxs-lookup"><span data-stu-id="055fd-227">400</span></span> |<span data-ttu-id="055fd-228">800</span><span class="sxs-lookup"><span data-stu-id="055fd-228">800</span></span> |<span data-ttu-id="055fd-229">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-229">1,600</span></span> |
| <span data-ttu-id="055fd-230">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-230">DW500</span></span> |<span data-ttu-id="055fd-231">100</span><span class="sxs-lookup"><span data-stu-id="055fd-231">100</span></span> |<span data-ttu-id="055fd-232">400</span><span class="sxs-lookup"><span data-stu-id="055fd-232">400</span></span> |<span data-ttu-id="055fd-233">800</span><span class="sxs-lookup"><span data-stu-id="055fd-233">800</span></span> |<span data-ttu-id="055fd-234">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-234">1,600</span></span> |
| <span data-ttu-id="055fd-235">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-235">DW600</span></span> |<span data-ttu-id="055fd-236">100</span><span class="sxs-lookup"><span data-stu-id="055fd-236">100</span></span> |<span data-ttu-id="055fd-237">400</span><span class="sxs-lookup"><span data-stu-id="055fd-237">400</span></span> |<span data-ttu-id="055fd-238">800</span><span class="sxs-lookup"><span data-stu-id="055fd-238">800</span></span> |<span data-ttu-id="055fd-239">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-239">1,600</span></span> |
| <span data-ttu-id="055fd-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-240">DW1000</span></span> |<span data-ttu-id="055fd-241">100</span><span class="sxs-lookup"><span data-stu-id="055fd-241">100</span></span> |<span data-ttu-id="055fd-242">800</span><span class="sxs-lookup"><span data-stu-id="055fd-242">800</span></span> |<span data-ttu-id="055fd-243">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-243">1,600</span></span> |<span data-ttu-id="055fd-244">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-244">3,200</span></span> |
| <span data-ttu-id="055fd-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-245">DW1200</span></span> |<span data-ttu-id="055fd-246">100</span><span class="sxs-lookup"><span data-stu-id="055fd-246">100</span></span> |<span data-ttu-id="055fd-247">800</span><span class="sxs-lookup"><span data-stu-id="055fd-247">800</span></span> |<span data-ttu-id="055fd-248">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-248">1,600</span></span> |<span data-ttu-id="055fd-249">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-249">3,200</span></span> |
| <span data-ttu-id="055fd-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-250">DW1500</span></span> |<span data-ttu-id="055fd-251">100</span><span class="sxs-lookup"><span data-stu-id="055fd-251">100</span></span> |<span data-ttu-id="055fd-252">800</span><span class="sxs-lookup"><span data-stu-id="055fd-252">800</span></span> |<span data-ttu-id="055fd-253">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-253">1,600</span></span> |<span data-ttu-id="055fd-254">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-254">3,200</span></span> |
| <span data-ttu-id="055fd-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-255">DW2000</span></span> |<span data-ttu-id="055fd-256">100</span><span class="sxs-lookup"><span data-stu-id="055fd-256">100</span></span> |<span data-ttu-id="055fd-257">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-257">1,600</span></span> |<span data-ttu-id="055fd-258">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-258">3,200</span></span> |<span data-ttu-id="055fd-259">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-259">6,400</span></span> |
| <span data-ttu-id="055fd-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-260">DW3000</span></span> |<span data-ttu-id="055fd-261">100</span><span class="sxs-lookup"><span data-stu-id="055fd-261">100</span></span> |<span data-ttu-id="055fd-262">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-262">1,600</span></span> |<span data-ttu-id="055fd-263">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-263">3,200</span></span> |<span data-ttu-id="055fd-264">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-264">6,400</span></span> |
| <span data-ttu-id="055fd-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-265">DW6000</span></span> |<span data-ttu-id="055fd-266">100</span><span class="sxs-lookup"><span data-stu-id="055fd-266">100</span></span> |<span data-ttu-id="055fd-267">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-267">3,200</span></span> |<span data-ttu-id="055fd-268">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-268">6,400</span></span> |<span data-ttu-id="055fd-269">12,800</span><span class="sxs-lookup"><span data-stu-id="055fd-269">12,800</span></span> |

<span data-ttu-id="055fd-270">下表中的 hello 對應 hello 記憶體配置 tooeach 發佈 DWU 和靜態資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="055fd-271">請注意 hello 較高的資源類別具有其記憶體減少 toohonor hello 全域 DWU 限制。</span><span class="sxs-lookup"><span data-stu-id="055fd-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="055fd-272">每個散發套件的靜態資源類別 (MB) 記憶體配置</span><span class="sxs-lookup"><span data-stu-id="055fd-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="055fd-273">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-273">DWU</span></span> | <span data-ttu-id="055fd-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="055fd-274">staticrc10</span></span> | <span data-ttu-id="055fd-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="055fd-275">staticrc20</span></span> | <span data-ttu-id="055fd-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="055fd-276">staticrc30</span></span> | <span data-ttu-id="055fd-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="055fd-277">staticrc40</span></span> | <span data-ttu-id="055fd-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="055fd-278">staticrc50</span></span> | <span data-ttu-id="055fd-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="055fd-279">staticrc60</span></span> | <span data-ttu-id="055fd-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="055fd-280">staticrc70</span></span> | <span data-ttu-id="055fd-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="055fd-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="055fd-282">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-282">DW100</span></span> |<span data-ttu-id="055fd-283">100</span><span class="sxs-lookup"><span data-stu-id="055fd-283">100</span></span> |<span data-ttu-id="055fd-284">200</span><span class="sxs-lookup"><span data-stu-id="055fd-284">200</span></span> |<span data-ttu-id="055fd-285">400</span><span class="sxs-lookup"><span data-stu-id="055fd-285">400</span></span> |<span data-ttu-id="055fd-286">400</span><span class="sxs-lookup"><span data-stu-id="055fd-286">400</span></span> |<span data-ttu-id="055fd-287">400</span><span class="sxs-lookup"><span data-stu-id="055fd-287">400</span></span> |<span data-ttu-id="055fd-288">400</span><span class="sxs-lookup"><span data-stu-id="055fd-288">400</span></span> |<span data-ttu-id="055fd-289">400</span><span class="sxs-lookup"><span data-stu-id="055fd-289">400</span></span> |<span data-ttu-id="055fd-290">400</span><span class="sxs-lookup"><span data-stu-id="055fd-290">400</span></span> |
| <span data-ttu-id="055fd-291">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-291">DW200</span></span> |<span data-ttu-id="055fd-292">100</span><span class="sxs-lookup"><span data-stu-id="055fd-292">100</span></span> |<span data-ttu-id="055fd-293">200</span><span class="sxs-lookup"><span data-stu-id="055fd-293">200</span></span> |<span data-ttu-id="055fd-294">400</span><span class="sxs-lookup"><span data-stu-id="055fd-294">400</span></span> |<span data-ttu-id="055fd-295">800</span><span class="sxs-lookup"><span data-stu-id="055fd-295">800</span></span> |<span data-ttu-id="055fd-296">800</span><span class="sxs-lookup"><span data-stu-id="055fd-296">800</span></span> |<span data-ttu-id="055fd-297">800</span><span class="sxs-lookup"><span data-stu-id="055fd-297">800</span></span> |<span data-ttu-id="055fd-298">800</span><span class="sxs-lookup"><span data-stu-id="055fd-298">800</span></span> |<span data-ttu-id="055fd-299">800</span><span class="sxs-lookup"><span data-stu-id="055fd-299">800</span></span> |
| <span data-ttu-id="055fd-300">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-300">DW300</span></span> |<span data-ttu-id="055fd-301">100</span><span class="sxs-lookup"><span data-stu-id="055fd-301">100</span></span> |<span data-ttu-id="055fd-302">200</span><span class="sxs-lookup"><span data-stu-id="055fd-302">200</span></span> |<span data-ttu-id="055fd-303">400</span><span class="sxs-lookup"><span data-stu-id="055fd-303">400</span></span> |<span data-ttu-id="055fd-304">800</span><span class="sxs-lookup"><span data-stu-id="055fd-304">800</span></span> |<span data-ttu-id="055fd-305">800</span><span class="sxs-lookup"><span data-stu-id="055fd-305">800</span></span> |<span data-ttu-id="055fd-306">800</span><span class="sxs-lookup"><span data-stu-id="055fd-306">800</span></span> |<span data-ttu-id="055fd-307">800</span><span class="sxs-lookup"><span data-stu-id="055fd-307">800</span></span> |<span data-ttu-id="055fd-308">800</span><span class="sxs-lookup"><span data-stu-id="055fd-308">800</span></span> |
| <span data-ttu-id="055fd-309">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-309">DW400</span></span> |<span data-ttu-id="055fd-310">100</span><span class="sxs-lookup"><span data-stu-id="055fd-310">100</span></span> |<span data-ttu-id="055fd-311">200</span><span class="sxs-lookup"><span data-stu-id="055fd-311">200</span></span> |<span data-ttu-id="055fd-312">400</span><span class="sxs-lookup"><span data-stu-id="055fd-312">400</span></span> |<span data-ttu-id="055fd-313">800</span><span class="sxs-lookup"><span data-stu-id="055fd-313">800</span></span> |<span data-ttu-id="055fd-314">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-314">1,600</span></span> |<span data-ttu-id="055fd-315">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-315">1,600</span></span> |<span data-ttu-id="055fd-316">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-316">1,600</span></span> |<span data-ttu-id="055fd-317">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-317">1,600</span></span> |
| <span data-ttu-id="055fd-318">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-318">DW500</span></span> |<span data-ttu-id="055fd-319">100</span><span class="sxs-lookup"><span data-stu-id="055fd-319">100</span></span> |<span data-ttu-id="055fd-320">200</span><span class="sxs-lookup"><span data-stu-id="055fd-320">200</span></span> |<span data-ttu-id="055fd-321">400</span><span class="sxs-lookup"><span data-stu-id="055fd-321">400</span></span> |<span data-ttu-id="055fd-322">800</span><span class="sxs-lookup"><span data-stu-id="055fd-322">800</span></span> |<span data-ttu-id="055fd-323">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-323">1,600</span></span> |<span data-ttu-id="055fd-324">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-324">1,600</span></span> |<span data-ttu-id="055fd-325">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-325">1,600</span></span> |<span data-ttu-id="055fd-326">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-326">1,600</span></span> |
| <span data-ttu-id="055fd-327">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-327">DW600</span></span> |<span data-ttu-id="055fd-328">100</span><span class="sxs-lookup"><span data-stu-id="055fd-328">100</span></span> |<span data-ttu-id="055fd-329">200</span><span class="sxs-lookup"><span data-stu-id="055fd-329">200</span></span> |<span data-ttu-id="055fd-330">400</span><span class="sxs-lookup"><span data-stu-id="055fd-330">400</span></span> |<span data-ttu-id="055fd-331">800</span><span class="sxs-lookup"><span data-stu-id="055fd-331">800</span></span> |<span data-ttu-id="055fd-332">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-332">1,600</span></span> |<span data-ttu-id="055fd-333">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-333">1,600</span></span> |<span data-ttu-id="055fd-334">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-334">1,600</span></span> |<span data-ttu-id="055fd-335">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-335">1,600</span></span> |
| <span data-ttu-id="055fd-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-336">DW1000</span></span> |<span data-ttu-id="055fd-337">100</span><span class="sxs-lookup"><span data-stu-id="055fd-337">100</span></span> |<span data-ttu-id="055fd-338">200</span><span class="sxs-lookup"><span data-stu-id="055fd-338">200</span></span> |<span data-ttu-id="055fd-339">400</span><span class="sxs-lookup"><span data-stu-id="055fd-339">400</span></span> |<span data-ttu-id="055fd-340">800</span><span class="sxs-lookup"><span data-stu-id="055fd-340">800</span></span> |<span data-ttu-id="055fd-341">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-341">1,600</span></span> |<span data-ttu-id="055fd-342">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-342">3,200</span></span> |<span data-ttu-id="055fd-343">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-343">3,200</span></span> |<span data-ttu-id="055fd-344">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-344">3,200</span></span> |
| <span data-ttu-id="055fd-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-345">DW1200</span></span> |<span data-ttu-id="055fd-346">100</span><span class="sxs-lookup"><span data-stu-id="055fd-346">100</span></span> |<span data-ttu-id="055fd-347">200</span><span class="sxs-lookup"><span data-stu-id="055fd-347">200</span></span> |<span data-ttu-id="055fd-348">400</span><span class="sxs-lookup"><span data-stu-id="055fd-348">400</span></span> |<span data-ttu-id="055fd-349">800</span><span class="sxs-lookup"><span data-stu-id="055fd-349">800</span></span> |<span data-ttu-id="055fd-350">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-350">1,600</span></span> |<span data-ttu-id="055fd-351">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-351">3,200</span></span> |<span data-ttu-id="055fd-352">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-352">3,200</span></span> |<span data-ttu-id="055fd-353">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-353">3,200</span></span> |
| <span data-ttu-id="055fd-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-354">DW1500</span></span> |<span data-ttu-id="055fd-355">100</span><span class="sxs-lookup"><span data-stu-id="055fd-355">100</span></span> |<span data-ttu-id="055fd-356">200</span><span class="sxs-lookup"><span data-stu-id="055fd-356">200</span></span> |<span data-ttu-id="055fd-357">400</span><span class="sxs-lookup"><span data-stu-id="055fd-357">400</span></span> |<span data-ttu-id="055fd-358">800</span><span class="sxs-lookup"><span data-stu-id="055fd-358">800</span></span> |<span data-ttu-id="055fd-359">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-359">1,600</span></span> |<span data-ttu-id="055fd-360">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-360">3,200</span></span> |<span data-ttu-id="055fd-361">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-361">3,200</span></span> |<span data-ttu-id="055fd-362">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-362">3,200</span></span> |
| <span data-ttu-id="055fd-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-363">DW2000</span></span> |<span data-ttu-id="055fd-364">100</span><span class="sxs-lookup"><span data-stu-id="055fd-364">100</span></span> |<span data-ttu-id="055fd-365">200</span><span class="sxs-lookup"><span data-stu-id="055fd-365">200</span></span> |<span data-ttu-id="055fd-366">400</span><span class="sxs-lookup"><span data-stu-id="055fd-366">400</span></span> |<span data-ttu-id="055fd-367">800</span><span class="sxs-lookup"><span data-stu-id="055fd-367">800</span></span> |<span data-ttu-id="055fd-368">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-368">1,600</span></span> |<span data-ttu-id="055fd-369">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-369">3,200</span></span> |<span data-ttu-id="055fd-370">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-370">6,400</span></span> |<span data-ttu-id="055fd-371">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-371">6,400</span></span> |
| <span data-ttu-id="055fd-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-372">DW3000</span></span> |<span data-ttu-id="055fd-373">100</span><span class="sxs-lookup"><span data-stu-id="055fd-373">100</span></span> |<span data-ttu-id="055fd-374">200</span><span class="sxs-lookup"><span data-stu-id="055fd-374">200</span></span> |<span data-ttu-id="055fd-375">400</span><span class="sxs-lookup"><span data-stu-id="055fd-375">400</span></span> |<span data-ttu-id="055fd-376">800</span><span class="sxs-lookup"><span data-stu-id="055fd-376">800</span></span> |<span data-ttu-id="055fd-377">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-377">1,600</span></span> |<span data-ttu-id="055fd-378">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-378">3,200</span></span> |<span data-ttu-id="055fd-379">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-379">6,400</span></span> |<span data-ttu-id="055fd-380">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-380">6,400</span></span> |
| <span data-ttu-id="055fd-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-381">DW6000</span></span> |<span data-ttu-id="055fd-382">100</span><span class="sxs-lookup"><span data-stu-id="055fd-382">100</span></span> |<span data-ttu-id="055fd-383">200</span><span class="sxs-lookup"><span data-stu-id="055fd-383">200</span></span> |<span data-ttu-id="055fd-384">400</span><span class="sxs-lookup"><span data-stu-id="055fd-384">400</span></span> |<span data-ttu-id="055fd-385">800</span><span class="sxs-lookup"><span data-stu-id="055fd-385">800</span></span> |<span data-ttu-id="055fd-386">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-386">1,600</span></span> |<span data-ttu-id="055fd-387">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-387">3,200</span></span> |<span data-ttu-id="055fd-388">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-388">6,400</span></span> |<span data-ttu-id="055fd-389">12,800</span><span class="sxs-lookup"><span data-stu-id="055fd-389">12,800</span></span> |

<span data-ttu-id="055fd-390">從上述資料表的 hello，您可以看到在 hello DW2000 上執行的查詢**xlargerc**資源類別必須存取 too6，400 MB 的記憶體內的每個 hello 60 分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="055fd-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="055fd-391">SQL 資料倉儲中有 60 個散發套件。</span><span class="sxs-lookup"><span data-stu-id="055fd-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="055fd-392">因此，toocalculate hello 總記憶體配置指定的資源類別中的查詢時，值以上的 hello 應該乘以 60。</span><span class="sxs-lookup"><span data-stu-id="055fd-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="055fd-393">全系統記憶體配置 (GB)</span><span class="sxs-lookup"><span data-stu-id="055fd-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="055fd-394">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-394">DWU</span></span> | <span data-ttu-id="055fd-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="055fd-395">smallrc</span></span> | <span data-ttu-id="055fd-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="055fd-396">mediumrc</span></span> | <span data-ttu-id="055fd-397">largerc</span><span class="sxs-lookup"><span data-stu-id="055fd-397">largerc</span></span> | <span data-ttu-id="055fd-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="055fd-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="055fd-399">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-399">DW100</span></span> |<span data-ttu-id="055fd-400">6</span><span class="sxs-lookup"><span data-stu-id="055fd-400">6</span></span> |<span data-ttu-id="055fd-401">6</span><span class="sxs-lookup"><span data-stu-id="055fd-401">6</span></span> |<span data-ttu-id="055fd-402">12</span><span class="sxs-lookup"><span data-stu-id="055fd-402">12</span></span> |<span data-ttu-id="055fd-403">23</span><span class="sxs-lookup"><span data-stu-id="055fd-403">23</span></span> |
| <span data-ttu-id="055fd-404">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-404">DW200</span></span> |<span data-ttu-id="055fd-405">6</span><span class="sxs-lookup"><span data-stu-id="055fd-405">6</span></span> |<span data-ttu-id="055fd-406">12</span><span class="sxs-lookup"><span data-stu-id="055fd-406">12</span></span> |<span data-ttu-id="055fd-407">23</span><span class="sxs-lookup"><span data-stu-id="055fd-407">23</span></span> |<span data-ttu-id="055fd-408">47</span><span class="sxs-lookup"><span data-stu-id="055fd-408">47</span></span> |
| <span data-ttu-id="055fd-409">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-409">DW300</span></span> |<span data-ttu-id="055fd-410">6</span><span class="sxs-lookup"><span data-stu-id="055fd-410">6</span></span> |<span data-ttu-id="055fd-411">12</span><span class="sxs-lookup"><span data-stu-id="055fd-411">12</span></span> |<span data-ttu-id="055fd-412">23</span><span class="sxs-lookup"><span data-stu-id="055fd-412">23</span></span> |<span data-ttu-id="055fd-413">47</span><span class="sxs-lookup"><span data-stu-id="055fd-413">47</span></span> |
| <span data-ttu-id="055fd-414">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-414">DW400</span></span> |<span data-ttu-id="055fd-415">6</span><span class="sxs-lookup"><span data-stu-id="055fd-415">6</span></span> |<span data-ttu-id="055fd-416">23</span><span class="sxs-lookup"><span data-stu-id="055fd-416">23</span></span> |<span data-ttu-id="055fd-417">47</span><span class="sxs-lookup"><span data-stu-id="055fd-417">47</span></span> |<span data-ttu-id="055fd-418">94</span><span class="sxs-lookup"><span data-stu-id="055fd-418">94</span></span> |
| <span data-ttu-id="055fd-419">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-419">DW500</span></span> |<span data-ttu-id="055fd-420">6</span><span class="sxs-lookup"><span data-stu-id="055fd-420">6</span></span> |<span data-ttu-id="055fd-421">23</span><span class="sxs-lookup"><span data-stu-id="055fd-421">23</span></span> |<span data-ttu-id="055fd-422">47</span><span class="sxs-lookup"><span data-stu-id="055fd-422">47</span></span> |<span data-ttu-id="055fd-423">94</span><span class="sxs-lookup"><span data-stu-id="055fd-423">94</span></span> |
| <span data-ttu-id="055fd-424">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-424">DW600</span></span> |<span data-ttu-id="055fd-425">6</span><span class="sxs-lookup"><span data-stu-id="055fd-425">6</span></span> |<span data-ttu-id="055fd-426">23</span><span class="sxs-lookup"><span data-stu-id="055fd-426">23</span></span> |<span data-ttu-id="055fd-427">47</span><span class="sxs-lookup"><span data-stu-id="055fd-427">47</span></span> |<span data-ttu-id="055fd-428">94</span><span class="sxs-lookup"><span data-stu-id="055fd-428">94</span></span> |
| <span data-ttu-id="055fd-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-429">DW1000</span></span> |<span data-ttu-id="055fd-430">6</span><span class="sxs-lookup"><span data-stu-id="055fd-430">6</span></span> |<span data-ttu-id="055fd-431">47</span><span class="sxs-lookup"><span data-stu-id="055fd-431">47</span></span> |<span data-ttu-id="055fd-432">94</span><span class="sxs-lookup"><span data-stu-id="055fd-432">94</span></span> |<span data-ttu-id="055fd-433">188</span><span class="sxs-lookup"><span data-stu-id="055fd-433">188</span></span> |
| <span data-ttu-id="055fd-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-434">DW1200</span></span> |<span data-ttu-id="055fd-435">6</span><span class="sxs-lookup"><span data-stu-id="055fd-435">6</span></span> |<span data-ttu-id="055fd-436">47</span><span class="sxs-lookup"><span data-stu-id="055fd-436">47</span></span> |<span data-ttu-id="055fd-437">94</span><span class="sxs-lookup"><span data-stu-id="055fd-437">94</span></span> |<span data-ttu-id="055fd-438">188</span><span class="sxs-lookup"><span data-stu-id="055fd-438">188</span></span> |
| <span data-ttu-id="055fd-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-439">DW1500</span></span> |<span data-ttu-id="055fd-440">6</span><span class="sxs-lookup"><span data-stu-id="055fd-440">6</span></span> |<span data-ttu-id="055fd-441">47</span><span class="sxs-lookup"><span data-stu-id="055fd-441">47</span></span> |<span data-ttu-id="055fd-442">94</span><span class="sxs-lookup"><span data-stu-id="055fd-442">94</span></span> |<span data-ttu-id="055fd-443">188</span><span class="sxs-lookup"><span data-stu-id="055fd-443">188</span></span> |
| <span data-ttu-id="055fd-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-444">DW2000</span></span> |<span data-ttu-id="055fd-445">6</span><span class="sxs-lookup"><span data-stu-id="055fd-445">6</span></span> |<span data-ttu-id="055fd-446">94</span><span class="sxs-lookup"><span data-stu-id="055fd-446">94</span></span> |<span data-ttu-id="055fd-447">188</span><span class="sxs-lookup"><span data-stu-id="055fd-447">188</span></span> |<span data-ttu-id="055fd-448">375</span><span class="sxs-lookup"><span data-stu-id="055fd-448">375</span></span> |
| <span data-ttu-id="055fd-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-449">DW3000</span></span> |<span data-ttu-id="055fd-450">6</span><span class="sxs-lookup"><span data-stu-id="055fd-450">6</span></span> |<span data-ttu-id="055fd-451">94</span><span class="sxs-lookup"><span data-stu-id="055fd-451">94</span></span> |<span data-ttu-id="055fd-452">188</span><span class="sxs-lookup"><span data-stu-id="055fd-452">188</span></span> |<span data-ttu-id="055fd-453">375</span><span class="sxs-lookup"><span data-stu-id="055fd-453">375</span></span> |
| <span data-ttu-id="055fd-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-454">DW6000</span></span> |<span data-ttu-id="055fd-455">6</span><span class="sxs-lookup"><span data-stu-id="055fd-455">6</span></span> |<span data-ttu-id="055fd-456">188</span><span class="sxs-lookup"><span data-stu-id="055fd-456">188</span></span> |<span data-ttu-id="055fd-457">375</span><span class="sxs-lookup"><span data-stu-id="055fd-457">375</span></span> |<span data-ttu-id="055fd-458">750</span><span class="sxs-lookup"><span data-stu-id="055fd-458">750</span></span> |

<span data-ttu-id="055fd-459">從這個資料表的全系統記憶體配置中，您可以看到上 DW2000 hello xlargerc 資源類別中執行查詢配置 375 gb 的記憶體總計 (6,400 MB * 60 分佈 / 1024 tooconvert tooGB) 上的 SQL 資料倉儲的 hello 全部內容。</span><span class="sxs-lookup"><span data-stu-id="055fd-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="055fd-460">hello 相同計算套用 toostatic 資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="055fd-461">並行存取插槽耗用量</span><span class="sxs-lookup"><span data-stu-id="055fd-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="055fd-462">SQL 資料倉儲會授與更多的記憶體 tooqueries 較高的資源類別中執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="055fd-463">記憶體是固定的資源。</span><span class="sxs-lookup"><span data-stu-id="055fd-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="055fd-464">因此，hello 更多的記憶體配置每個查詢，可以在執行較少的並行查詢的 hello。</span><span class="sxs-lookup"><span data-stu-id="055fd-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="055fd-465">hello 表 reiterates 所有 hello hello 並行的 DWU 可用的插槽與每個資源類別所耗用的 hello 插槽數目會顯示在單一檢視中的上一個概念。</span><span class="sxs-lookup"><span data-stu-id="055fd-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="055fd-466">動態資源類別並行存取插槽的配置和耗用量</span><span class="sxs-lookup"><span data-stu-id="055fd-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="055fd-467">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-467">DWU</span></span> | <span data-ttu-id="055fd-468">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="055fd-468">Maximum concurrent queries</span></span> | <span data-ttu-id="055fd-469">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-469">Concurrency slots allocated</span></span> | <span data-ttu-id="055fd-470">Smallrc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-470">Slots used by smallrc</span></span> | <span data-ttu-id="055fd-471">Mediumrc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-471">Slots used by mediumrc</span></span> | <span data-ttu-id="055fd-472">Largerc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-472">Slots used by largerc</span></span> | <span data-ttu-id="055fd-473">Xlargerc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="055fd-474">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-474">DW100</span></span> |<span data-ttu-id="055fd-475">4</span><span class="sxs-lookup"><span data-stu-id="055fd-475">4</span></span> |<span data-ttu-id="055fd-476">4</span><span class="sxs-lookup"><span data-stu-id="055fd-476">4</span></span> |<span data-ttu-id="055fd-477">1</span><span class="sxs-lookup"><span data-stu-id="055fd-477">1</span></span> |<span data-ttu-id="055fd-478">1</span><span class="sxs-lookup"><span data-stu-id="055fd-478">1</span></span> |<span data-ttu-id="055fd-479">2</span><span class="sxs-lookup"><span data-stu-id="055fd-479">2</span></span> |<span data-ttu-id="055fd-480">4</span><span class="sxs-lookup"><span data-stu-id="055fd-480">4</span></span> |
| <span data-ttu-id="055fd-481">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-481">DW200</span></span> |<span data-ttu-id="055fd-482">8</span><span class="sxs-lookup"><span data-stu-id="055fd-482">8</span></span> |<span data-ttu-id="055fd-483">8</span><span class="sxs-lookup"><span data-stu-id="055fd-483">8</span></span> |<span data-ttu-id="055fd-484">1</span><span class="sxs-lookup"><span data-stu-id="055fd-484">1</span></span> |<span data-ttu-id="055fd-485">2</span><span class="sxs-lookup"><span data-stu-id="055fd-485">2</span></span> |<span data-ttu-id="055fd-486">4</span><span class="sxs-lookup"><span data-stu-id="055fd-486">4</span></span> |<span data-ttu-id="055fd-487">8</span><span class="sxs-lookup"><span data-stu-id="055fd-487">8</span></span> |
| <span data-ttu-id="055fd-488">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-488">DW300</span></span> |<span data-ttu-id="055fd-489">12</span><span class="sxs-lookup"><span data-stu-id="055fd-489">12</span></span> |<span data-ttu-id="055fd-490">12</span><span class="sxs-lookup"><span data-stu-id="055fd-490">12</span></span> |<span data-ttu-id="055fd-491">1</span><span class="sxs-lookup"><span data-stu-id="055fd-491">1</span></span> |<span data-ttu-id="055fd-492">2</span><span class="sxs-lookup"><span data-stu-id="055fd-492">2</span></span> |<span data-ttu-id="055fd-493">4</span><span class="sxs-lookup"><span data-stu-id="055fd-493">4</span></span> |<span data-ttu-id="055fd-494">8</span><span class="sxs-lookup"><span data-stu-id="055fd-494">8</span></span> |
| <span data-ttu-id="055fd-495">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-495">DW400</span></span> |<span data-ttu-id="055fd-496">16</span><span class="sxs-lookup"><span data-stu-id="055fd-496">16</span></span> |<span data-ttu-id="055fd-497">16</span><span class="sxs-lookup"><span data-stu-id="055fd-497">16</span></span> |<span data-ttu-id="055fd-498">1</span><span class="sxs-lookup"><span data-stu-id="055fd-498">1</span></span> |<span data-ttu-id="055fd-499">4</span><span class="sxs-lookup"><span data-stu-id="055fd-499">4</span></span> |<span data-ttu-id="055fd-500">8</span><span class="sxs-lookup"><span data-stu-id="055fd-500">8</span></span> |<span data-ttu-id="055fd-501">16</span><span class="sxs-lookup"><span data-stu-id="055fd-501">16</span></span> |
| <span data-ttu-id="055fd-502">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-502">DW500</span></span> |<span data-ttu-id="055fd-503">20</span><span class="sxs-lookup"><span data-stu-id="055fd-503">20</span></span> |<span data-ttu-id="055fd-504">20</span><span class="sxs-lookup"><span data-stu-id="055fd-504">20</span></span> |<span data-ttu-id="055fd-505">1</span><span class="sxs-lookup"><span data-stu-id="055fd-505">1</span></span> |<span data-ttu-id="055fd-506">4</span><span class="sxs-lookup"><span data-stu-id="055fd-506">4</span></span> |<span data-ttu-id="055fd-507">8</span><span class="sxs-lookup"><span data-stu-id="055fd-507">8</span></span> |<span data-ttu-id="055fd-508">16</span><span class="sxs-lookup"><span data-stu-id="055fd-508">16</span></span> |
| <span data-ttu-id="055fd-509">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-509">DW600</span></span> |<span data-ttu-id="055fd-510">24</span><span class="sxs-lookup"><span data-stu-id="055fd-510">24</span></span> |<span data-ttu-id="055fd-511">24</span><span class="sxs-lookup"><span data-stu-id="055fd-511">24</span></span> |<span data-ttu-id="055fd-512">1</span><span class="sxs-lookup"><span data-stu-id="055fd-512">1</span></span> |<span data-ttu-id="055fd-513">4</span><span class="sxs-lookup"><span data-stu-id="055fd-513">4</span></span> |<span data-ttu-id="055fd-514">8</span><span class="sxs-lookup"><span data-stu-id="055fd-514">8</span></span> |<span data-ttu-id="055fd-515">16</span><span class="sxs-lookup"><span data-stu-id="055fd-515">16</span></span> |
| <span data-ttu-id="055fd-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-516">DW1000</span></span> |<span data-ttu-id="055fd-517">32</span><span class="sxs-lookup"><span data-stu-id="055fd-517">32</span></span> |<span data-ttu-id="055fd-518">40</span><span class="sxs-lookup"><span data-stu-id="055fd-518">40</span></span> |<span data-ttu-id="055fd-519">1</span><span class="sxs-lookup"><span data-stu-id="055fd-519">1</span></span> |<span data-ttu-id="055fd-520">8</span><span class="sxs-lookup"><span data-stu-id="055fd-520">8</span></span> |<span data-ttu-id="055fd-521">16</span><span class="sxs-lookup"><span data-stu-id="055fd-521">16</span></span> |<span data-ttu-id="055fd-522">32</span><span class="sxs-lookup"><span data-stu-id="055fd-522">32</span></span> |
| <span data-ttu-id="055fd-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-523">DW1200</span></span> |<span data-ttu-id="055fd-524">32</span><span class="sxs-lookup"><span data-stu-id="055fd-524">32</span></span> |<span data-ttu-id="055fd-525">48</span><span class="sxs-lookup"><span data-stu-id="055fd-525">48</span></span> |<span data-ttu-id="055fd-526">1</span><span class="sxs-lookup"><span data-stu-id="055fd-526">1</span></span> |<span data-ttu-id="055fd-527">8</span><span class="sxs-lookup"><span data-stu-id="055fd-527">8</span></span> |<span data-ttu-id="055fd-528">16</span><span class="sxs-lookup"><span data-stu-id="055fd-528">16</span></span> |<span data-ttu-id="055fd-529">32</span><span class="sxs-lookup"><span data-stu-id="055fd-529">32</span></span> |
| <span data-ttu-id="055fd-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-530">DW1500</span></span> |<span data-ttu-id="055fd-531">32</span><span class="sxs-lookup"><span data-stu-id="055fd-531">32</span></span> |<span data-ttu-id="055fd-532">60</span><span class="sxs-lookup"><span data-stu-id="055fd-532">60</span></span> |<span data-ttu-id="055fd-533">1</span><span class="sxs-lookup"><span data-stu-id="055fd-533">1</span></span> |<span data-ttu-id="055fd-534">8</span><span class="sxs-lookup"><span data-stu-id="055fd-534">8</span></span> |<span data-ttu-id="055fd-535">16</span><span class="sxs-lookup"><span data-stu-id="055fd-535">16</span></span> |<span data-ttu-id="055fd-536">32</span><span class="sxs-lookup"><span data-stu-id="055fd-536">32</span></span> |
| <span data-ttu-id="055fd-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-537">DW2000</span></span> |<span data-ttu-id="055fd-538">32</span><span class="sxs-lookup"><span data-stu-id="055fd-538">32</span></span> |<span data-ttu-id="055fd-539">80</span><span class="sxs-lookup"><span data-stu-id="055fd-539">80</span></span> |<span data-ttu-id="055fd-540">1</span><span class="sxs-lookup"><span data-stu-id="055fd-540">1</span></span> |<span data-ttu-id="055fd-541">16</span><span class="sxs-lookup"><span data-stu-id="055fd-541">16</span></span> |<span data-ttu-id="055fd-542">32</span><span class="sxs-lookup"><span data-stu-id="055fd-542">32</span></span> |<span data-ttu-id="055fd-543">64</span><span class="sxs-lookup"><span data-stu-id="055fd-543">64</span></span> |
| <span data-ttu-id="055fd-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-544">DW3000</span></span> |<span data-ttu-id="055fd-545">32</span><span class="sxs-lookup"><span data-stu-id="055fd-545">32</span></span> |<span data-ttu-id="055fd-546">120</span><span class="sxs-lookup"><span data-stu-id="055fd-546">120</span></span> |<span data-ttu-id="055fd-547">1</span><span class="sxs-lookup"><span data-stu-id="055fd-547">1</span></span> |<span data-ttu-id="055fd-548">16</span><span class="sxs-lookup"><span data-stu-id="055fd-548">16</span></span> |<span data-ttu-id="055fd-549">32</span><span class="sxs-lookup"><span data-stu-id="055fd-549">32</span></span> |<span data-ttu-id="055fd-550">64</span><span class="sxs-lookup"><span data-stu-id="055fd-550">64</span></span> |
| <span data-ttu-id="055fd-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-551">DW6000</span></span> |<span data-ttu-id="055fd-552">32</span><span class="sxs-lookup"><span data-stu-id="055fd-552">32</span></span> |<span data-ttu-id="055fd-553">240</span><span class="sxs-lookup"><span data-stu-id="055fd-553">240</span></span> |<span data-ttu-id="055fd-554">1</span><span class="sxs-lookup"><span data-stu-id="055fd-554">1</span></span> |<span data-ttu-id="055fd-555">32</span><span class="sxs-lookup"><span data-stu-id="055fd-555">32</span></span> |<span data-ttu-id="055fd-556">64</span><span class="sxs-lookup"><span data-stu-id="055fd-556">64</span></span> |<span data-ttu-id="055fd-557">128</span><span class="sxs-lookup"><span data-stu-id="055fd-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="055fd-558">靜態資源類別並行存取插槽的配置和耗用量</span><span class="sxs-lookup"><span data-stu-id="055fd-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="055fd-559">DWU</span><span class="sxs-lookup"><span data-stu-id="055fd-559">DWU</span></span> | <span data-ttu-id="055fd-560">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="055fd-560">Maximum concurrent queries</span></span> | <span data-ttu-id="055fd-561">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-561">Concurrency slots allocated</span></span> |<span data-ttu-id="055fd-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="055fd-562">staticrc10</span></span> | <span data-ttu-id="055fd-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="055fd-563">staticrc20</span></span> | <span data-ttu-id="055fd-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="055fd-564">staticrc30</span></span> | <span data-ttu-id="055fd-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="055fd-565">staticrc40</span></span> | <span data-ttu-id="055fd-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="055fd-566">staticrc50</span></span> | <span data-ttu-id="055fd-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="055fd-567">staticrc60</span></span> | <span data-ttu-id="055fd-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="055fd-568">staticrc70</span></span> | <span data-ttu-id="055fd-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="055fd-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="055fd-570">DW100</span><span class="sxs-lookup"><span data-stu-id="055fd-570">DW100</span></span> |<span data-ttu-id="055fd-571">4</span><span class="sxs-lookup"><span data-stu-id="055fd-571">4</span></span> |<span data-ttu-id="055fd-572">4</span><span class="sxs-lookup"><span data-stu-id="055fd-572">4</span></span> |<span data-ttu-id="055fd-573">1</span><span class="sxs-lookup"><span data-stu-id="055fd-573">1</span></span> |<span data-ttu-id="055fd-574">2</span><span class="sxs-lookup"><span data-stu-id="055fd-574">2</span></span> |<span data-ttu-id="055fd-575">4</span><span class="sxs-lookup"><span data-stu-id="055fd-575">4</span></span> |<span data-ttu-id="055fd-576">4</span><span class="sxs-lookup"><span data-stu-id="055fd-576">4</span></span> |<span data-ttu-id="055fd-577">4</span><span class="sxs-lookup"><span data-stu-id="055fd-577">4</span></span> |<span data-ttu-id="055fd-578">4</span><span class="sxs-lookup"><span data-stu-id="055fd-578">4</span></span> |<span data-ttu-id="055fd-579">4</span><span class="sxs-lookup"><span data-stu-id="055fd-579">4</span></span> |<span data-ttu-id="055fd-580">4</span><span class="sxs-lookup"><span data-stu-id="055fd-580">4</span></span> |
| <span data-ttu-id="055fd-581">DW200</span><span class="sxs-lookup"><span data-stu-id="055fd-581">DW200</span></span> |<span data-ttu-id="055fd-582">8</span><span class="sxs-lookup"><span data-stu-id="055fd-582">8</span></span> |<span data-ttu-id="055fd-583">8</span><span class="sxs-lookup"><span data-stu-id="055fd-583">8</span></span> |<span data-ttu-id="055fd-584">1</span><span class="sxs-lookup"><span data-stu-id="055fd-584">1</span></span> |<span data-ttu-id="055fd-585">2</span><span class="sxs-lookup"><span data-stu-id="055fd-585">2</span></span> |<span data-ttu-id="055fd-586">4</span><span class="sxs-lookup"><span data-stu-id="055fd-586">4</span></span> |<span data-ttu-id="055fd-587">8</span><span class="sxs-lookup"><span data-stu-id="055fd-587">8</span></span> |<span data-ttu-id="055fd-588">8</span><span class="sxs-lookup"><span data-stu-id="055fd-588">8</span></span> |<span data-ttu-id="055fd-589">8</span><span class="sxs-lookup"><span data-stu-id="055fd-589">8</span></span> |<span data-ttu-id="055fd-590">8</span><span class="sxs-lookup"><span data-stu-id="055fd-590">8</span></span> |<span data-ttu-id="055fd-591">8</span><span class="sxs-lookup"><span data-stu-id="055fd-591">8</span></span> |
| <span data-ttu-id="055fd-592">DW300</span><span class="sxs-lookup"><span data-stu-id="055fd-592">DW300</span></span> |<span data-ttu-id="055fd-593">12</span><span class="sxs-lookup"><span data-stu-id="055fd-593">12</span></span> |<span data-ttu-id="055fd-594">12</span><span class="sxs-lookup"><span data-stu-id="055fd-594">12</span></span> |<span data-ttu-id="055fd-595">1</span><span class="sxs-lookup"><span data-stu-id="055fd-595">1</span></span> |<span data-ttu-id="055fd-596">2</span><span class="sxs-lookup"><span data-stu-id="055fd-596">2</span></span> |<span data-ttu-id="055fd-597">4</span><span class="sxs-lookup"><span data-stu-id="055fd-597">4</span></span> |<span data-ttu-id="055fd-598">8</span><span class="sxs-lookup"><span data-stu-id="055fd-598">8</span></span> |<span data-ttu-id="055fd-599">8</span><span class="sxs-lookup"><span data-stu-id="055fd-599">8</span></span> |<span data-ttu-id="055fd-600">8</span><span class="sxs-lookup"><span data-stu-id="055fd-600">8</span></span> |<span data-ttu-id="055fd-601">8</span><span class="sxs-lookup"><span data-stu-id="055fd-601">8</span></span> |<span data-ttu-id="055fd-602">8</span><span class="sxs-lookup"><span data-stu-id="055fd-602">8</span></span> |
| <span data-ttu-id="055fd-603">DW400</span><span class="sxs-lookup"><span data-stu-id="055fd-603">DW400</span></span> |<span data-ttu-id="055fd-604">16</span><span class="sxs-lookup"><span data-stu-id="055fd-604">16</span></span> |<span data-ttu-id="055fd-605">16</span><span class="sxs-lookup"><span data-stu-id="055fd-605">16</span></span> |<span data-ttu-id="055fd-606">1</span><span class="sxs-lookup"><span data-stu-id="055fd-606">1</span></span> |<span data-ttu-id="055fd-607">2</span><span class="sxs-lookup"><span data-stu-id="055fd-607">2</span></span> |<span data-ttu-id="055fd-608">4</span><span class="sxs-lookup"><span data-stu-id="055fd-608">4</span></span> |<span data-ttu-id="055fd-609">8</span><span class="sxs-lookup"><span data-stu-id="055fd-609">8</span></span> |<span data-ttu-id="055fd-610">16</span><span class="sxs-lookup"><span data-stu-id="055fd-610">16</span></span> |<span data-ttu-id="055fd-611">16</span><span class="sxs-lookup"><span data-stu-id="055fd-611">16</span></span> |<span data-ttu-id="055fd-612">16</span><span class="sxs-lookup"><span data-stu-id="055fd-612">16</span></span> |<span data-ttu-id="055fd-613">16</span><span class="sxs-lookup"><span data-stu-id="055fd-613">16</span></span> |
| <span data-ttu-id="055fd-614">DW500</span><span class="sxs-lookup"><span data-stu-id="055fd-614">DW500</span></span> | <span data-ttu-id="055fd-615">20</span><span class="sxs-lookup"><span data-stu-id="055fd-615">20</span></span>| <span data-ttu-id="055fd-616">20</span><span class="sxs-lookup"><span data-stu-id="055fd-616">20</span></span>| <span data-ttu-id="055fd-617">1</span><span class="sxs-lookup"><span data-stu-id="055fd-617">1</span></span>| <span data-ttu-id="055fd-618">2</span><span class="sxs-lookup"><span data-stu-id="055fd-618">2</span></span>| <span data-ttu-id="055fd-619">4</span><span class="sxs-lookup"><span data-stu-id="055fd-619">4</span></span>| <span data-ttu-id="055fd-620">8</span><span class="sxs-lookup"><span data-stu-id="055fd-620">8</span></span>| <span data-ttu-id="055fd-621">16</span><span class="sxs-lookup"><span data-stu-id="055fd-621">16</span></span>| <span data-ttu-id="055fd-622">16</span><span class="sxs-lookup"><span data-stu-id="055fd-622">16</span></span>| <span data-ttu-id="055fd-623">16</span><span class="sxs-lookup"><span data-stu-id="055fd-623">16</span></span>| <span data-ttu-id="055fd-624">16</span><span class="sxs-lookup"><span data-stu-id="055fd-624">16</span></span>|
| <span data-ttu-id="055fd-625">DW600</span><span class="sxs-lookup"><span data-stu-id="055fd-625">DW600</span></span> | <span data-ttu-id="055fd-626">24</span><span class="sxs-lookup"><span data-stu-id="055fd-626">24</span></span>| <span data-ttu-id="055fd-627">24</span><span class="sxs-lookup"><span data-stu-id="055fd-627">24</span></span>| <span data-ttu-id="055fd-628">1</span><span class="sxs-lookup"><span data-stu-id="055fd-628">1</span></span>| <span data-ttu-id="055fd-629">2</span><span class="sxs-lookup"><span data-stu-id="055fd-629">2</span></span>| <span data-ttu-id="055fd-630">4</span><span class="sxs-lookup"><span data-stu-id="055fd-630">4</span></span>| <span data-ttu-id="055fd-631">8</span><span class="sxs-lookup"><span data-stu-id="055fd-631">8</span></span>| <span data-ttu-id="055fd-632">16</span><span class="sxs-lookup"><span data-stu-id="055fd-632">16</span></span>| <span data-ttu-id="055fd-633">16</span><span class="sxs-lookup"><span data-stu-id="055fd-633">16</span></span>| <span data-ttu-id="055fd-634">16</span><span class="sxs-lookup"><span data-stu-id="055fd-634">16</span></span>| <span data-ttu-id="055fd-635">16</span><span class="sxs-lookup"><span data-stu-id="055fd-635">16</span></span>|
| <span data-ttu-id="055fd-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="055fd-636">DW1000</span></span> | <span data-ttu-id="055fd-637">32</span><span class="sxs-lookup"><span data-stu-id="055fd-637">32</span></span>| <span data-ttu-id="055fd-638">40</span><span class="sxs-lookup"><span data-stu-id="055fd-638">40</span></span>| <span data-ttu-id="055fd-639">1</span><span class="sxs-lookup"><span data-stu-id="055fd-639">1</span></span>| <span data-ttu-id="055fd-640">2</span><span class="sxs-lookup"><span data-stu-id="055fd-640">2</span></span>| <span data-ttu-id="055fd-641">4</span><span class="sxs-lookup"><span data-stu-id="055fd-641">4</span></span>| <span data-ttu-id="055fd-642">8</span><span class="sxs-lookup"><span data-stu-id="055fd-642">8</span></span>| <span data-ttu-id="055fd-643">16</span><span class="sxs-lookup"><span data-stu-id="055fd-643">16</span></span>| <span data-ttu-id="055fd-644">32</span><span class="sxs-lookup"><span data-stu-id="055fd-644">32</span></span>| <span data-ttu-id="055fd-645">32</span><span class="sxs-lookup"><span data-stu-id="055fd-645">32</span></span>| <span data-ttu-id="055fd-646">32</span><span class="sxs-lookup"><span data-stu-id="055fd-646">32</span></span>|
| <span data-ttu-id="055fd-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="055fd-647">DW1200</span></span> | <span data-ttu-id="055fd-648">32</span><span class="sxs-lookup"><span data-stu-id="055fd-648">32</span></span>| <span data-ttu-id="055fd-649">48</span><span class="sxs-lookup"><span data-stu-id="055fd-649">48</span></span>| <span data-ttu-id="055fd-650">1</span><span class="sxs-lookup"><span data-stu-id="055fd-650">1</span></span>| <span data-ttu-id="055fd-651">2</span><span class="sxs-lookup"><span data-stu-id="055fd-651">2</span></span>| <span data-ttu-id="055fd-652">4</span><span class="sxs-lookup"><span data-stu-id="055fd-652">4</span></span>| <span data-ttu-id="055fd-653">8</span><span class="sxs-lookup"><span data-stu-id="055fd-653">8</span></span>| <span data-ttu-id="055fd-654">16</span><span class="sxs-lookup"><span data-stu-id="055fd-654">16</span></span>| <span data-ttu-id="055fd-655">32</span><span class="sxs-lookup"><span data-stu-id="055fd-655">32</span></span>| <span data-ttu-id="055fd-656">32</span><span class="sxs-lookup"><span data-stu-id="055fd-656">32</span></span>| <span data-ttu-id="055fd-657">32</span><span class="sxs-lookup"><span data-stu-id="055fd-657">32</span></span>|
| <span data-ttu-id="055fd-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="055fd-658">DW1500</span></span> | <span data-ttu-id="055fd-659">32</span><span class="sxs-lookup"><span data-stu-id="055fd-659">32</span></span>| <span data-ttu-id="055fd-660">60</span><span class="sxs-lookup"><span data-stu-id="055fd-660">60</span></span>| <span data-ttu-id="055fd-661">1</span><span class="sxs-lookup"><span data-stu-id="055fd-661">1</span></span>| <span data-ttu-id="055fd-662">2</span><span class="sxs-lookup"><span data-stu-id="055fd-662">2</span></span>| <span data-ttu-id="055fd-663">4</span><span class="sxs-lookup"><span data-stu-id="055fd-663">4</span></span>| <span data-ttu-id="055fd-664">8</span><span class="sxs-lookup"><span data-stu-id="055fd-664">8</span></span>| <span data-ttu-id="055fd-665">16</span><span class="sxs-lookup"><span data-stu-id="055fd-665">16</span></span>| <span data-ttu-id="055fd-666">32</span><span class="sxs-lookup"><span data-stu-id="055fd-666">32</span></span>| <span data-ttu-id="055fd-667">32</span><span class="sxs-lookup"><span data-stu-id="055fd-667">32</span></span>| <span data-ttu-id="055fd-668">32</span><span class="sxs-lookup"><span data-stu-id="055fd-668">32</span></span>|
| <span data-ttu-id="055fd-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="055fd-669">DW2000</span></span> | <span data-ttu-id="055fd-670">32</span><span class="sxs-lookup"><span data-stu-id="055fd-670">32</span></span>| <span data-ttu-id="055fd-671">80</span><span class="sxs-lookup"><span data-stu-id="055fd-671">80</span></span>| <span data-ttu-id="055fd-672">1</span><span class="sxs-lookup"><span data-stu-id="055fd-672">1</span></span>| <span data-ttu-id="055fd-673">2</span><span class="sxs-lookup"><span data-stu-id="055fd-673">2</span></span>| <span data-ttu-id="055fd-674">4</span><span class="sxs-lookup"><span data-stu-id="055fd-674">4</span></span>| <span data-ttu-id="055fd-675">8</span><span class="sxs-lookup"><span data-stu-id="055fd-675">8</span></span>| <span data-ttu-id="055fd-676">16</span><span class="sxs-lookup"><span data-stu-id="055fd-676">16</span></span>| <span data-ttu-id="055fd-677">32</span><span class="sxs-lookup"><span data-stu-id="055fd-677">32</span></span>| <span data-ttu-id="055fd-678">64</span><span class="sxs-lookup"><span data-stu-id="055fd-678">64</span></span>| <span data-ttu-id="055fd-679">64</span><span class="sxs-lookup"><span data-stu-id="055fd-679">64</span></span>|
| <span data-ttu-id="055fd-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="055fd-680">DW3000</span></span> | <span data-ttu-id="055fd-681">32</span><span class="sxs-lookup"><span data-stu-id="055fd-681">32</span></span>| <span data-ttu-id="055fd-682">120</span><span class="sxs-lookup"><span data-stu-id="055fd-682">120</span></span>| <span data-ttu-id="055fd-683">1</span><span class="sxs-lookup"><span data-stu-id="055fd-683">1</span></span>| <span data-ttu-id="055fd-684">2</span><span class="sxs-lookup"><span data-stu-id="055fd-684">2</span></span>| <span data-ttu-id="055fd-685">4</span><span class="sxs-lookup"><span data-stu-id="055fd-685">4</span></span>| <span data-ttu-id="055fd-686">8</span><span class="sxs-lookup"><span data-stu-id="055fd-686">8</span></span>| <span data-ttu-id="055fd-687">16</span><span class="sxs-lookup"><span data-stu-id="055fd-687">16</span></span>| <span data-ttu-id="055fd-688">32</span><span class="sxs-lookup"><span data-stu-id="055fd-688">32</span></span>| <span data-ttu-id="055fd-689">64</span><span class="sxs-lookup"><span data-stu-id="055fd-689">64</span></span>| <span data-ttu-id="055fd-690">64</span><span class="sxs-lookup"><span data-stu-id="055fd-690">64</span></span>|
| <span data-ttu-id="055fd-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="055fd-691">DW6000</span></span> | <span data-ttu-id="055fd-692">32</span><span class="sxs-lookup"><span data-stu-id="055fd-692">32</span></span>| <span data-ttu-id="055fd-693">240</span><span class="sxs-lookup"><span data-stu-id="055fd-693">240</span></span>| <span data-ttu-id="055fd-694">1</span><span class="sxs-lookup"><span data-stu-id="055fd-694">1</span></span>| <span data-ttu-id="055fd-695">2</span><span class="sxs-lookup"><span data-stu-id="055fd-695">2</span></span>| <span data-ttu-id="055fd-696">4</span><span class="sxs-lookup"><span data-stu-id="055fd-696">4</span></span>| <span data-ttu-id="055fd-697">8</span><span class="sxs-lookup"><span data-stu-id="055fd-697">8</span></span>| <span data-ttu-id="055fd-698">16</span><span class="sxs-lookup"><span data-stu-id="055fd-698">16</span></span>| <span data-ttu-id="055fd-699">32</span><span class="sxs-lookup"><span data-stu-id="055fd-699">32</span></span>| <span data-ttu-id="055fd-700">64</span><span class="sxs-lookup"><span data-stu-id="055fd-700">64</span></span>| <span data-ttu-id="055fd-701">128</span><span class="sxs-lookup"><span data-stu-id="055fd-701">128</span></span>|

<span data-ttu-id="055fd-702">從上述表格中，您會看到以 DW1000 身分執行的 SQL 資料倉儲，配置最多 32 個並行查詢，以及總數 40 個的並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="055fd-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="055fd-703">如果所有的使用者都以 smallrc 執行，將允許 32 個並行查詢，因為每個查詢會取用 1 個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="055fd-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="055fd-704">如果執行 mediumrc DW1000 上的所有使用者、 每個查詢則會配置 800 MB 散發 47 GB 的記憶體總計配置每個查詢，每並行就是限制的 too5 使用者 (40 並行插槽 / 每位使用者 mediumrc 插槽 8)。</span><span class="sxs-lookup"><span data-stu-id="055fd-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="055fd-705">選取適當的資源類別</span><span class="sxs-lookup"><span data-stu-id="055fd-705">Selecting proper resource class</span></span>  
<span data-ttu-id="055fd-706">最好的作法是 toopermanently 指派使用者 tooa 資源類別，而不是變更其資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="055fd-707">例如，載入 tooclustered 資料行存放區資料表建立高品質索引配置更多的記憶體時。</span><span class="sxs-lookup"><span data-stu-id="055fd-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="055fd-708">tooensure 負載存取 toohigher 記憶體、 建立使用者，特別是用於載入資料和永久指派此使用者 tooa 高資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="055fd-709">有幾個最佳作法 toofollow 這裡。</span><span class="sxs-lookup"><span data-stu-id="055fd-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="055fd-710">如上所述，SQL DW 支援兩種資源類別類型：靜態資源類別和動態資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="055fd-711">載入的最佳做法</span><span class="sxs-lookup"><span data-stu-id="055fd-711">Loading best practices</span></span>
1.  <span data-ttu-id="055fd-712">如果 hello 期望載入一般資料量，靜態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="055fd-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="055fd-713">更新版本中，當向上 tooget 更多計算能力、 hello 資料倉儲將無法 toorun 更多的並行查詢-現成的因為 hello 負載使用者不會耗用更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="055fd-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="055fd-714">如果 hello 期望在某些情況下更大的負載，動態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="055fd-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="055fd-715">更新版本中，當向上 tooget 更多計算能力，hello 負載使用者會收到更多的記憶體--現成的因此允許 hello 負載 tooperform 更快。</span><span class="sxs-lookup"><span data-stu-id="055fd-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="055fd-716">hello 所需的記憶體 tooprocess 載入有效率地取決於 hello 性質 hello 資料表載入和處理資料的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="055fd-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="055fd-717">比方說，CCI 資料表將資料載入要求一些記憶體 toolet CCI 資料列群組達到牽動。</span><span class="sxs-lookup"><span data-stu-id="055fd-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="055fd-718">如需詳細資訊，請參閱 hello 資料行存放區索引資料載入指引。</span><span class="sxs-lookup"><span data-stu-id="055fd-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="055fd-719">最佳做法，我們建議您 toouse 至少 200 MB 的記憶體載入。</span><span class="sxs-lookup"><span data-stu-id="055fd-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="055fd-720">查詢的最佳做法</span><span class="sxs-lookup"><span data-stu-id="055fd-720">Querying best practices</span></span>
<span data-ttu-id="055fd-721">查詢會因其複雜性而有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="055fd-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="055fd-722">增加每個查詢的記憶體，或增加 hello 並行是這兩個有效的方式 tooaugment 根據 hello 查詢需求的整體輸送量。</span><span class="sxs-lookup"><span data-stu-id="055fd-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="055fd-723">如果 hello 期望規則、 複雜的查詢 (例如，toogenerate 每日及每週的報表)，但是不需要 tootake 並行優點，動態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="055fd-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="055fd-724">如果 hello 系統有多個資料 tooprocess，向上擴充 hello 資料倉儲將會因此自動提供更多記憶體 toohello 使用者執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="055fd-725">如果 hello 期望變數或 diurnal 並行模式 (例如透過 web UI 廣泛存取如果會查詢 hello 資料庫)，靜態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="055fd-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="055fd-726">稍後，當 toodata 倉儲向上擴充，hello hello 靜態資源類別相關聯的使用者會自動是無法 toorun 更多的並行查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="055fd-727">它相依於許多因素，例如 hello 少量資料的查詢，hello hello 資料表結構描述，以及各種聯結、 選取項目，與群組述詞的性質為非簡單式，根據您的查詢 hello 需求選取適當的記憶體授與。</span><span class="sxs-lookup"><span data-stu-id="055fd-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="055fd-728">一般的觀點而言，配置更多記憶體可讓查詢 toocomplete 較快，但是會減少 hello 整體的並行存取。</span><span class="sxs-lookup"><span data-stu-id="055fd-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="055fd-729">如果您不在意並行存取能力，則可以放心地超額配置記憶體。</span><span class="sxs-lookup"><span data-stu-id="055fd-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="055fd-730">您可能需要 toofine 微調輸送量，嘗試的資源類別的各種類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="055fd-731">您可以使用 hello 下列預存程序 toofigure 出並行存取，以及記憶體授與每個資源類別，為給定 SLO 和 hello 最接近最佳資源類別的記憶體密集 CCI 非資料分割 CCI 資料表作業在指定的資源類別：</span><span class="sxs-lookup"><span data-stu-id="055fd-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="055fd-732">Description:</span><span class="sxs-lookup"><span data-stu-id="055fd-732">Description:</span></span>  
<span data-ttu-id="055fd-733">以下是 hello 用途，此預存程序：</span><span class="sxs-lookup"><span data-stu-id="055fd-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="055fd-734">toohelp 出每個資源類別，在給定的 SLO 的並行存取，以及記憶體授與使用者數。</span><span class="sxs-lookup"><span data-stu-id="055fd-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="055fd-735">使用者需要 tooprovide NULL 的結構描述和 tablename 這個 hello 下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="055fd-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="055fd-736">toohelp 使用者找出 hello 最接近最佳資源類別 hello 記憶體 intensed CCI 作業 （負載，複製資料表時，會重建索引等） 指定的資源類別的非資料分割 CCI 資料表上。</span><span class="sxs-lookup"><span data-stu-id="055fd-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="055fd-737">hello 預存程序會使用這個資料表的結構描述 toofind 出 hello 所需的記憶體授與。</span><span class="sxs-lookup"><span data-stu-id="055fd-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="055fd-738">相依性及限制：</span><span class="sxs-lookup"><span data-stu-id="055fd-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="055fd-739">這個預存程序不是設計的 toocalculate cci 分割資料表的記憶體需求。</span><span class="sxs-lookup"><span data-stu-id="055fd-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="055fd-740">這個預存程序不接受的 CTAS/INSERT SELECT hello SELECT 部分的記憶體需求納入考量，並假設它 toobe 簡單的選取。</span><span class="sxs-lookup"><span data-stu-id="055fd-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="055fd-741">這個預存程序會使用暫存資料表，因此這可用 hello 工作階段中建立此預存程序所在。</span><span class="sxs-lookup"><span data-stu-id="055fd-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="055fd-742">這個預存程序取決於 hello 目前供應項目 （例如硬體組態、 DMS 組態），如果變更了，然後此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="055fd-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="055fd-743">此預存程序仰賴目前提供的並行存取限制，如果限制有任何變更，此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="055fd-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="055fd-744">此預存程序仰賴現有的資源類別供應項目，如果其中有任何變更，此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="055fd-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="055fd-745">如果您在使用所提供的參數來執行預存程序後沒有取得輸出，則可能有兩種情況。</span><span class="sxs-lookup"><span data-stu-id="055fd-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="055fd-746">1.DW 參數包含無效的 SLO 值</span><span class="sxs-lookup"><span data-stu-id="055fd-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="055fd-747">2.沒有符合 CCI 作業的資源類別 (若已提供資料表名稱)。</span><span class="sxs-lookup"><span data-stu-id="055fd-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="055fd-748">例如，在 DW100，最高可用的記憶體授與為 400 MB 和寬型資料表結構描述是否足以 toocross hello 需求為 400 MB。</span><span class="sxs-lookup"><span data-stu-id="055fd-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="055fd-749">使用範例：</span><span class="sxs-lookup"><span data-stu-id="055fd-749">Usage example:</span></span>
<span data-ttu-id="055fd-750">語法：</span><span class="sxs-lookup"><span data-stu-id="055fd-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="055fd-751">@DWU:請提供 NULL 參數 tooextract hello hello 資料倉儲資料庫從目前的 DWU，或提供任何支援的 DWU hello 'DW100' 形式</span><span class="sxs-lookup"><span data-stu-id="055fd-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="055fd-752">@SCHEMA_NAME:提供 hello 資料表的結構描述名稱</span><span class="sxs-lookup"><span data-stu-id="055fd-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="055fd-753">@TABLE_NAME:提供 hello 感興趣的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="055fd-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="055fd-754">執行此預存程序的範例：</span><span class="sxs-lookup"><span data-stu-id="055fd-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="055fd-755">無法建立 Table1 hello 上述範例中使用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="055fd-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="055fd-756">以下是 hello 預存程序定義：</span><span class="sxs-lookup"><span data-stu-id="055fd-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="055fd-757">查詢的重要性</span><span class="sxs-lookup"><span data-stu-id="055fd-757">Query importance</span></span>
<span data-ttu-id="055fd-758">SQL 資料倉儲使用工作負載群組來實作資源類別。</span><span class="sxs-lookup"><span data-stu-id="055fd-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="055fd-759">有八個 hello 跨各種 DWU 大小控制 hello 行為 hello 資源類別的工作負載群組的總計。</span><span class="sxs-lookup"><span data-stu-id="055fd-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="055fd-760">對於任何 DWU，SQL 資料倉儲會使用僅有四個 hello 八個工作負載群組。</span><span class="sxs-lookup"><span data-stu-id="055fd-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="055fd-761">這使得意義，因為每個工作負載群組指派的四個資源類別 tooone: smallrc mediumrc，largerc，或 xlargerc。</span><span class="sxs-lookup"><span data-stu-id="055fd-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="055fd-762">hello 的了解 hello 工作負載群組重要性是其中部分工作負載群組會設定 toohigher*重要性*。</span><span class="sxs-lookup"><span data-stu-id="055fd-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="055fd-763">重要性可用於 CPU 排程。</span><span class="sxs-lookup"><span data-stu-id="055fd-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="055fd-764">以高重要性執行的查詢會取得比中度重要性的查詢高三倍的 CPU 週期。</span><span class="sxs-lookup"><span data-stu-id="055fd-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="055fd-765">因此，並行存取插槽對應也會判斷 CPU 優先順序。</span><span class="sxs-lookup"><span data-stu-id="055fd-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="055fd-766">當查詢取用 16 個以上的插槽時，就會以高重要性執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="055fd-767">hello 下表顯示每個工作負載群組的 hello 重要性對應。</span><span class="sxs-lookup"><span data-stu-id="055fd-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="055fd-768">工作負載群組對應 tooconcurrency 位置和重要性</span><span class="sxs-lookup"><span data-stu-id="055fd-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="055fd-769">工作負載群組</span><span class="sxs-lookup"><span data-stu-id="055fd-769">Workload groups</span></span> | <span data-ttu-id="055fd-770">並行存取插槽對應</span><span class="sxs-lookup"><span data-stu-id="055fd-770">Concurrency slot mapping</span></span> | <span data-ttu-id="055fd-771">MB / 散發套件</span><span class="sxs-lookup"><span data-stu-id="055fd-771">MB / Distribution</span></span> | <span data-ttu-id="055fd-772">重要性對應</span><span class="sxs-lookup"><span data-stu-id="055fd-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="055fd-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="055fd-773">SloDWGroupC00</span></span> |<span data-ttu-id="055fd-774">1</span><span class="sxs-lookup"><span data-stu-id="055fd-774">1</span></span> |<span data-ttu-id="055fd-775">100</span><span class="sxs-lookup"><span data-stu-id="055fd-775">100</span></span> |<span data-ttu-id="055fd-776">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-776">Medium</span></span> |
| <span data-ttu-id="055fd-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="055fd-777">SloDWGroupC01</span></span> |<span data-ttu-id="055fd-778">2</span><span class="sxs-lookup"><span data-stu-id="055fd-778">2</span></span> |<span data-ttu-id="055fd-779">200</span><span class="sxs-lookup"><span data-stu-id="055fd-779">200</span></span> |<span data-ttu-id="055fd-780">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-780">Medium</span></span> |
| <span data-ttu-id="055fd-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="055fd-781">SloDWGroupC02</span></span> |<span data-ttu-id="055fd-782">4</span><span class="sxs-lookup"><span data-stu-id="055fd-782">4</span></span> |<span data-ttu-id="055fd-783">400</span><span class="sxs-lookup"><span data-stu-id="055fd-783">400</span></span> |<span data-ttu-id="055fd-784">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-784">Medium</span></span> |
| <span data-ttu-id="055fd-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-785">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-786">8</span><span class="sxs-lookup"><span data-stu-id="055fd-786">8</span></span> |<span data-ttu-id="055fd-787">800</span><span class="sxs-lookup"><span data-stu-id="055fd-787">800</span></span> |<span data-ttu-id="055fd-788">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-788">Medium</span></span> |
| <span data-ttu-id="055fd-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="055fd-789">SloDWGroupC04</span></span> |<span data-ttu-id="055fd-790">16</span><span class="sxs-lookup"><span data-stu-id="055fd-790">16</span></span> |<span data-ttu-id="055fd-791">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-791">1,600</span></span> |<span data-ttu-id="055fd-792">高</span><span class="sxs-lookup"><span data-stu-id="055fd-792">High</span></span> |
| <span data-ttu-id="055fd-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="055fd-793">SloDWGroupC05</span></span> |<span data-ttu-id="055fd-794">32</span><span class="sxs-lookup"><span data-stu-id="055fd-794">32</span></span> |<span data-ttu-id="055fd-795">3,200</span><span class="sxs-lookup"><span data-stu-id="055fd-795">3,200</span></span> |<span data-ttu-id="055fd-796">高</span><span class="sxs-lookup"><span data-stu-id="055fd-796">High</span></span> |
| <span data-ttu-id="055fd-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="055fd-797">SloDWGroupC06</span></span> |<span data-ttu-id="055fd-798">64</span><span class="sxs-lookup"><span data-stu-id="055fd-798">64</span></span> |<span data-ttu-id="055fd-799">6,400</span><span class="sxs-lookup"><span data-stu-id="055fd-799">6,400</span></span> |<span data-ttu-id="055fd-800">高</span><span class="sxs-lookup"><span data-stu-id="055fd-800">High</span></span> |
| <span data-ttu-id="055fd-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="055fd-801">SloDWGroupC07</span></span> |<span data-ttu-id="055fd-802">128</span><span class="sxs-lookup"><span data-stu-id="055fd-802">128</span></span> |<span data-ttu-id="055fd-803">12,800</span><span class="sxs-lookup"><span data-stu-id="055fd-803">12,800</span></span> |<span data-ttu-id="055fd-804">高</span><span class="sxs-lookup"><span data-stu-id="055fd-804">High</span></span> |

<span data-ttu-id="055fd-805">從 hello**配置和耗用量的並行插槽**圖表中，您可以看到，DW500 1、 4、 8 或 16 的並行存取位置 smallrc、 mediumrc、 largerc，和 xlargerc，分別使用。</span><span class="sxs-lookup"><span data-stu-id="055fd-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="055fd-806">您可以在 hello 上述圖表 toofind hello 重要性，針對每個資源類別中查詢這些值。</span><span class="sxs-lookup"><span data-stu-id="055fd-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="055fd-807">資源類別 tooimportance 的 DW500 對應</span><span class="sxs-lookup"><span data-stu-id="055fd-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="055fd-808">資源類別</span><span class="sxs-lookup"><span data-stu-id="055fd-808">Resource class</span></span> | <span data-ttu-id="055fd-809">工作負載群組</span><span class="sxs-lookup"><span data-stu-id="055fd-809">Workload group</span></span> | <span data-ttu-id="055fd-810">已使用的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="055fd-810">Concurrency slots used</span></span> | <span data-ttu-id="055fd-811">MB / 散發套件</span><span class="sxs-lookup"><span data-stu-id="055fd-811">MB / Distribution</span></span> | <span data-ttu-id="055fd-812">重要性</span><span class="sxs-lookup"><span data-stu-id="055fd-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="055fd-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="055fd-813">smallrc</span></span> |<span data-ttu-id="055fd-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="055fd-814">SloDWGroupC00</span></span> |<span data-ttu-id="055fd-815">1</span><span class="sxs-lookup"><span data-stu-id="055fd-815">1</span></span> |<span data-ttu-id="055fd-816">100</span><span class="sxs-lookup"><span data-stu-id="055fd-816">100</span></span> |<span data-ttu-id="055fd-817">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-817">Medium</span></span> |
| <span data-ttu-id="055fd-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="055fd-818">mediumrc</span></span> |<span data-ttu-id="055fd-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="055fd-819">SloDWGroupC02</span></span> |<span data-ttu-id="055fd-820">4</span><span class="sxs-lookup"><span data-stu-id="055fd-820">4</span></span> |<span data-ttu-id="055fd-821">400</span><span class="sxs-lookup"><span data-stu-id="055fd-821">400</span></span> |<span data-ttu-id="055fd-822">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-822">Medium</span></span> |
| <span data-ttu-id="055fd-823">largerc</span><span class="sxs-lookup"><span data-stu-id="055fd-823">largerc</span></span> |<span data-ttu-id="055fd-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-824">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-825">8</span><span class="sxs-lookup"><span data-stu-id="055fd-825">8</span></span> |<span data-ttu-id="055fd-826">800</span><span class="sxs-lookup"><span data-stu-id="055fd-826">800</span></span> |<span data-ttu-id="055fd-827">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-827">Medium</span></span> |
| <span data-ttu-id="055fd-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="055fd-828">xlargerc</span></span> |<span data-ttu-id="055fd-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="055fd-829">SloDWGroupC04</span></span> |<span data-ttu-id="055fd-830">16</span><span class="sxs-lookup"><span data-stu-id="055fd-830">16</span></span> |<span data-ttu-id="055fd-831">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-831">1,600</span></span> |<span data-ttu-id="055fd-832">高</span><span class="sxs-lookup"><span data-stu-id="055fd-832">High</span></span> |
| <span data-ttu-id="055fd-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="055fd-833">staticrc10</span></span> |<span data-ttu-id="055fd-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="055fd-834">SloDWGroupC00</span></span> |<span data-ttu-id="055fd-835">1</span><span class="sxs-lookup"><span data-stu-id="055fd-835">1</span></span> |<span data-ttu-id="055fd-836">100</span><span class="sxs-lookup"><span data-stu-id="055fd-836">100</span></span> |<span data-ttu-id="055fd-837">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-837">Medium</span></span> |
| <span data-ttu-id="055fd-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="055fd-838">staticrc20</span></span> |<span data-ttu-id="055fd-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="055fd-839">SloDWGroupC01</span></span> |<span data-ttu-id="055fd-840">2</span><span class="sxs-lookup"><span data-stu-id="055fd-840">2</span></span> |<span data-ttu-id="055fd-841">200</span><span class="sxs-lookup"><span data-stu-id="055fd-841">200</span></span> |<span data-ttu-id="055fd-842">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-842">Medium</span></span> |
| <span data-ttu-id="055fd-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="055fd-843">staticrc30</span></span> |<span data-ttu-id="055fd-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="055fd-844">SloDWGroupC02</span></span> |<span data-ttu-id="055fd-845">4</span><span class="sxs-lookup"><span data-stu-id="055fd-845">4</span></span> |<span data-ttu-id="055fd-846">400</span><span class="sxs-lookup"><span data-stu-id="055fd-846">400</span></span> |<span data-ttu-id="055fd-847">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-847">Medium</span></span> |
| <span data-ttu-id="055fd-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="055fd-848">staticrc40</span></span> |<span data-ttu-id="055fd-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-849">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-850">8</span><span class="sxs-lookup"><span data-stu-id="055fd-850">8</span></span> |<span data-ttu-id="055fd-851">800</span><span class="sxs-lookup"><span data-stu-id="055fd-851">800</span></span> |<span data-ttu-id="055fd-852">中型</span><span class="sxs-lookup"><span data-stu-id="055fd-852">Medium</span></span> |
| <span data-ttu-id="055fd-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="055fd-853">staticrc50</span></span> |<span data-ttu-id="055fd-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-854">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-855">16</span><span class="sxs-lookup"><span data-stu-id="055fd-855">16</span></span> |<span data-ttu-id="055fd-856">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-856">1,600</span></span> |<span data-ttu-id="055fd-857">高</span><span class="sxs-lookup"><span data-stu-id="055fd-857">High</span></span> |
| <span data-ttu-id="055fd-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="055fd-858">staticrc60</span></span> |<span data-ttu-id="055fd-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-859">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-860">16</span><span class="sxs-lookup"><span data-stu-id="055fd-860">16</span></span> |<span data-ttu-id="055fd-861">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-861">1,600</span></span> |<span data-ttu-id="055fd-862">高</span><span class="sxs-lookup"><span data-stu-id="055fd-862">High</span></span> |
| <span data-ttu-id="055fd-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="055fd-863">staticrc70</span></span> |<span data-ttu-id="055fd-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-864">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-865">16</span><span class="sxs-lookup"><span data-stu-id="055fd-865">16</span></span> |<span data-ttu-id="055fd-866">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-866">1,600</span></span> |<span data-ttu-id="055fd-867">高</span><span class="sxs-lookup"><span data-stu-id="055fd-867">High</span></span> |
| <span data-ttu-id="055fd-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="055fd-868">staticrc80</span></span> |<span data-ttu-id="055fd-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="055fd-869">SloDWGroupC03</span></span> |<span data-ttu-id="055fd-870">16</span><span class="sxs-lookup"><span data-stu-id="055fd-870">16</span></span> |<span data-ttu-id="055fd-871">1,600</span><span class="sxs-lookup"><span data-stu-id="055fd-871">1,600</span></span> |<span data-ttu-id="055fd-872">高</span><span class="sxs-lookup"><span data-stu-id="055fd-872">High</span></span> |

<span data-ttu-id="055fd-873">您可以使用 hello 疑難排解時，下列 DMV 查詢 toolook 在 hello 檢視方塊的 hello 資源管理員，或 tooanalyze hello 工作負載群組的作用中和歷史使用量詳細的記憶體資源配置中的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="055fd-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="055fd-874">採用並行存取限制的查詢</span><span class="sxs-lookup"><span data-stu-id="055fd-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="055fd-875">大多數查詢都受到資源類別控管。</span><span class="sxs-lookup"><span data-stu-id="055fd-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="055fd-876">這些查詢都必須容納在 hello 並行查詢和並行位置臨界值內。</span><span class="sxs-lookup"><span data-stu-id="055fd-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="055fd-877">使用者無法選擇 tooexclude 查詢從 hello 並行存取模型中的插槽。</span><span class="sxs-lookup"><span data-stu-id="055fd-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="055fd-878">tooreiterate，hello 下列陳述式，採用資源類別：</span><span class="sxs-lookup"><span data-stu-id="055fd-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="055fd-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="055fd-879">INSERT-SELECT</span></span>
* <span data-ttu-id="055fd-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="055fd-880">UPDATE</span></span>
* <span data-ttu-id="055fd-881">刪除</span><span class="sxs-lookup"><span data-stu-id="055fd-881">DELETE</span></span>
* <span data-ttu-id="055fd-882">SELECT (當查詢使用者資料表時)</span><span class="sxs-lookup"><span data-stu-id="055fd-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="055fd-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="055fd-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="055fd-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="055fd-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="055fd-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="055fd-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="055fd-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="055fd-886">CREATE INDEX</span></span>
* <span data-ttu-id="055fd-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="055fd-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="055fd-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="055fd-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="055fd-889">載入資料</span><span class="sxs-lookup"><span data-stu-id="055fd-889">Data loading</span></span>
* <span data-ttu-id="055fd-890">Hello 資料移動服務 (DMS) 所進行的資料移動作業</span><span class="sxs-lookup"><span data-stu-id="055fd-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="055fd-891">查詢例外狀況 tooconcurrency 限制</span><span class="sxs-lookup"><span data-stu-id="055fd-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="055fd-892">某些查詢不接受 hello 資源指派給類別 toowhich hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="055fd-893">當 hello 特定命令所需的記憶體資源不足，通常是因為 hello 命令是中繼資料的作業時，對這些例外狀況 toohello 並行存取限制。</span><span class="sxs-lookup"><span data-stu-id="055fd-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="055fd-894">這些例外狀況 hello 目標是 tooavoid 較大的記憶體配置將永遠不需要的查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="055fd-895">在這些情況下，不論 hello 實際資源類別一律會使用小型資源類別 (smallrc) hello 預設指派 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="055fd-896">例如， `CREATE LOGIN` 一律會在 smallrc 中執行。</span><span class="sxs-lookup"><span data-stu-id="055fd-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="055fd-897">hello 所需資源 toofulfill 這項作業都是很低，因此不會有意義 tooinclude hello 查詢 hello 並行存取模型中的插槽中。</span><span class="sxs-lookup"><span data-stu-id="055fd-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="055fd-898">這些查詢也不會受到 hello 32 使用者並行存取限制，無限的數量的這些查詢可以執行 toohello 工作階段限制為 1,024 工作階段設定。</span><span class="sxs-lookup"><span data-stu-id="055fd-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="055fd-899">hello 下列陳述式不接受資源類別：</span><span class="sxs-lookup"><span data-stu-id="055fd-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="055fd-900">CREATE 或 DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="055fd-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="055fd-901">ALTER TABLE ...SWITCH、SPLIT 或 MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="055fd-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="055fd-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="055fd-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="055fd-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="055fd-903">DROP INDEX</span></span>
* <span data-ttu-id="055fd-904">CREATE、UPDATE 或 DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="055fd-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="055fd-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="055fd-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="055fd-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="055fd-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="055fd-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="055fd-907">CREATE LOGIN</span></span>
* <span data-ttu-id="055fd-908">CREATE、ALTER 或 DROP USER</span><span class="sxs-lookup"><span data-stu-id="055fd-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="055fd-909">CREATE、ALTER 或 DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="055fd-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="055fd-910">CREATE 或 DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="055fd-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="055fd-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="055fd-911">INSERT VALUES</span></span>
* <span data-ttu-id="055fd-912">從系統檢視和 DMV 來 SELECT</span><span class="sxs-lookup"><span data-stu-id="055fd-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="055fd-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="055fd-913">EXPLAIN</span></span>
* <span data-ttu-id="055fd-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="055fd-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="055fd-915"><a name="changing-user-resource-class-example"></a> 變更使用者資源類別的範例</span><span class="sxs-lookup"><span data-stu-id="055fd-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="055fd-916">**建立登入：**開啟連接 tooyour**主要**上 hello 裝載您的 SQL 資料倉儲資料庫的 SQL server 資料庫並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="055fd-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="055fd-917">Azure SQL 資料倉儲使用者 hello master 資料庫中是個不錯的主意 toocreate 使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="055fd-918">在 master 中建立使用者，可讓使用者 toologin 使用 SSMS 等工具，而不指定資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="055fd-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="055fd-919">它也可讓它們 toouse hello 物件總管 中 tooview SQL server 的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="055fd-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="055fd-920">如需有關建立和管理使用者的詳細資料，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="055fd-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="055fd-921">**建立 SQL 資料倉儲的使用者：**開啟連接 toohello **SQL 資料倉儲**資料庫並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="055fd-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="055fd-922">**授與權限：**下列範例授與 hello`CONTROL`上 hello **SQL 資料倉儲**資料庫。</span><span class="sxs-lookup"><span data-stu-id="055fd-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="055fd-923">`CONTROL`在 hello 資料庫層級是 hello db_owner SQL Server 中的對等。</span><span class="sxs-lookup"><span data-stu-id="055fd-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="055fd-924">**增加資源類別：**使用 hello 下列查詢會 tooadd 使用者 tooa 較高的工作負載管理角色。</span><span class="sxs-lookup"><span data-stu-id="055fd-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="055fd-925">**減少資源類別：**使用 hello 下列查詢會 tooremove 工作負載管理角色的使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="055fd-926">不可能 tooremove smallrc 的使用者。</span><span class="sxs-lookup"><span data-stu-id="055fd-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="055fd-927">已排入佇列的查詢偵測和其他 DMV</span><span class="sxs-lookup"><span data-stu-id="055fd-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="055fd-928">您可以使用 hello`sys.dm_pdw_exec_requests`並行佇列中等待的 DMV tooidentify 查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="055fd-929">正在等待並行存取插槽的查詢狀態為 **暫停**。</span><span class="sxs-lookup"><span data-stu-id="055fd-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="055fd-930">工作負載管理角色可以使用 `sys.database_principals`來檢視。</span><span class="sxs-lookup"><span data-stu-id="055fd-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="055fd-931">hello，下列查詢會顯示每個使用者指派給角色。</span><span class="sxs-lookup"><span data-stu-id="055fd-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="055fd-932">SQL 資料倉儲具有 hello 下列等候類型：</span><span class="sxs-lookup"><span data-stu-id="055fd-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="055fd-933">**LocalQueriesConcurrencyResourceType**： 坐 hello 並行插槽 framework 外部的查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="055fd-934">DMV 查詢及 `SELECT @@VERSION` 這類的系統函數是本機查詢的範例。</span><span class="sxs-lookup"><span data-stu-id="055fd-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="055fd-935">**UserConcurrencyResourceType**： 坐在 hello 並行處理插槽架構內的查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="055fd-936">針對使用者資料表的查詢代表會使用此資源類型的範例。</span><span class="sxs-lookup"><span data-stu-id="055fd-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="055fd-937">**DmsConcurrencyResourceType**：資料移動作業所產生的等候。</span><span class="sxs-lookup"><span data-stu-id="055fd-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="055fd-938">**BackupConcurrencyResourceType**：此等候指出正在備份資料庫。</span><span class="sxs-lookup"><span data-stu-id="055fd-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="055fd-939">hello 這個資源類型的最大值為 1。</span><span class="sxs-lookup"><span data-stu-id="055fd-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="055fd-940">如果已經在 hello 要求多個備份相同的時間，其他人會排入佇列的 hello。</span><span class="sxs-lookup"><span data-stu-id="055fd-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="055fd-941">hello `sys.dm_pdw_waits` DMV 可以是使用的 toosee 要求正在等候的資源。</span><span class="sxs-lookup"><span data-stu-id="055fd-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="055fd-942">hello `sys.dm_pdw_resource_waits` DMV 顯示只有 hello 資源等候由給定的查詢。</span><span class="sxs-lookup"><span data-stu-id="055fd-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="055fd-943">資源等候時間僅會測量等候所提供的資源 toobe hello 時間，因為相對於的 toosignal 等候時間，這就是 hello 時間花費 hello 基礎 SQL 伺服器 tooschedule hello 查詢到 hello CPU。</span><span class="sxs-lookup"><span data-stu-id="055fd-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="055fd-944">hello `sys.dm_pdw_wait_stats` DMV 可用來等候的歷史趨勢分析。</span><span class="sxs-lookup"><span data-stu-id="055fd-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="055fd-945">後續步驟</span><span class="sxs-lookup"><span data-stu-id="055fd-945">Next steps</span></span>
<span data-ttu-id="055fd-946">如需管理資料庫使用者和安全性的詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="055fd-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="055fd-947">如何在較大的資源類別的詳細資訊，可改進叢集資料行存放區索引的品質，請參閱[重建索引 tooimprove 區段品質]。</span><span class="sxs-lookup"><span data-stu-id="055fd-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[重建索引 tooimprove 區段品質]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
