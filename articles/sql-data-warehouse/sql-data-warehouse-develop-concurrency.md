---
title: "SQL 資料倉儲中的並行存取和工作負載管理 | Microsoft Docs"
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
ms.openlocfilehash: eaf2d43286dbaa52ada1430fbb7ce1e37f41c0d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="c5f52-103">SQL 資料倉儲中的並行存取和工作負載管理</span><span class="sxs-lookup"><span data-stu-id="c5f52-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="c5f52-104">為了大規模傳遞可預測的效能，Microsoft Azure SQL 資料倉儲可協助您控制並行存取層級和資源配置，例如記憶體和 CPU 優先順序。</span><span class="sxs-lookup"><span data-stu-id="c5f52-104">To deliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="c5f52-105">本文介紹並行存取和工作負載管理的概念；說明如何實作這兩種功能，以及如何在資料倉儲中控制它們。</span><span class="sxs-lookup"><span data-stu-id="c5f52-105">This article introduces you to the concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="c5f52-106">SQL 資料倉儲工作負載管理的目的，是要幫助您支援多使用者環境。</span><span class="sxs-lookup"><span data-stu-id="c5f52-106">SQL Data Warehouse workload management is intended to help you support multi-user environments.</span></span> <span data-ttu-id="c5f52-107">它並不適用於多租用戶工作負載。</span><span class="sxs-lookup"><span data-stu-id="c5f52-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="c5f52-108">並行存取限制</span><span class="sxs-lookup"><span data-stu-id="c5f52-108">Concurrency limits</span></span>
<span data-ttu-id="c5f52-109">SQL 資料倉儲最多允許 1,024 個並行存取連線。</span><span class="sxs-lookup"><span data-stu-id="c5f52-109">SQL Data Warehouse allows up to 1,024 concurrent connections.</span></span> <span data-ttu-id="c5f52-110">這 1,024 個連線全都可以並行提交查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="c5f52-111">不過，為達到最佳輸送量，SQL 資料倉儲可能會將某些查詢排入佇列，以確保每個查詢能夠獲得最少的記憶體授與。</span><span class="sxs-lookup"><span data-stu-id="c5f52-111">However, to optimize throughput, SQL Data Warehouse may queue some queries to ensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="c5f52-112">佇列會在查詢執行時發生。</span><span class="sxs-lookup"><span data-stu-id="c5f52-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="c5f52-113">藉由在到達並行存取限制時將查詢排入佇列，SQL 資料倉儲就可透過確保作用中查詢能夠取得急需的記憶體資源存取權，來增加總輸送量。</span><span class="sxs-lookup"><span data-stu-id="c5f52-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access to critically needed memory resources.</span></span>  

<span data-ttu-id="c5f52-114">並行存取限制受到兩個概念所控制：「並行查詢」和「並行存取插槽」。</span><span class="sxs-lookup"><span data-stu-id="c5f52-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="c5f52-115">若要執行查詢，它必須在查詢並行限制和並行存取插槽配置內執行。</span><span class="sxs-lookup"><span data-stu-id="c5f52-115">For a query to execute, it must execute within both the query concurrency limit and the concurrency slot allocation.</span></span>

* <span data-ttu-id="c5f52-116">並行查詢是在同一時間執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-116">Concurrent queries are the queries executing at the same time.</span></span> <span data-ttu-id="c5f52-117">「SQL 資料倉儲」在較大的 DWU 大小上最多可支援 32 個並行查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-117">SQL Data Warehouse supports up to 32 concurrent queries on the larger DWU sizes.</span></span>
* <span data-ttu-id="c5f52-118">並行存取插槽是根據 DWU 所配置。</span><span class="sxs-lookup"><span data-stu-id="c5f52-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="c5f52-119">每 100 個 DWU 提供 4 個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="c5f52-120">例如，DW100 會配置 4 個並行存取插槽，而 DW1000 會配置 40 個。</span><span class="sxs-lookup"><span data-stu-id="c5f52-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="c5f52-121">根據查詢的 [資源類別](#resource-classes) 而定，每個查詢會使用一或多個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-121">Each query consumes one or more concurrency slots, dependent on the [resource class](#resource-classes) of the query.</span></span> <span data-ttu-id="c5f52-122">smallrc 資源類別中執行的查詢會使用一個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-122">Queries running in the smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="c5f52-123">較高資源類別中執行的查詢會使用更多的並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="c5f52-124">下表說明在不同的 DWU 大小，並行查詢和並行存取插槽的限制。</span><span class="sxs-lookup"><span data-stu-id="c5f52-124">The following table describes the limits for both concurrent queries and concurrency slots at the various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="c5f52-125">並行存取限制</span><span class="sxs-lookup"><span data-stu-id="c5f52-125">Concurrency limits</span></span>
| <span data-ttu-id="c5f52-126">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-126">DWU</span></span> | <span data-ttu-id="c5f52-127">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="c5f52-127">Max concurrent queries</span></span> | <span data-ttu-id="c5f52-128">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="c5f52-129">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-129">DW100</span></span> |<span data-ttu-id="c5f52-130">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-130">4</span></span> |<span data-ttu-id="c5f52-131">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-131">4</span></span> |
| <span data-ttu-id="c5f52-132">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-132">DW200</span></span> |<span data-ttu-id="c5f52-133">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-133">8</span></span> |<span data-ttu-id="c5f52-134">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-134">8</span></span> |
| <span data-ttu-id="c5f52-135">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-135">DW300</span></span> |<span data-ttu-id="c5f52-136">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-136">12</span></span> |<span data-ttu-id="c5f52-137">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-137">12</span></span> |
| <span data-ttu-id="c5f52-138">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-138">DW400</span></span> |<span data-ttu-id="c5f52-139">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-139">16</span></span> |<span data-ttu-id="c5f52-140">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-140">16</span></span> |
| <span data-ttu-id="c5f52-141">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-141">DW500</span></span> |<span data-ttu-id="c5f52-142">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-142">20</span></span> |<span data-ttu-id="c5f52-143">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-143">20</span></span> |
| <span data-ttu-id="c5f52-144">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-144">DW600</span></span> |<span data-ttu-id="c5f52-145">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-145">24</span></span> |<span data-ttu-id="c5f52-146">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-146">24</span></span> |
| <span data-ttu-id="c5f52-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-147">DW1000</span></span> |<span data-ttu-id="c5f52-148">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-148">32</span></span> |<span data-ttu-id="c5f52-149">40</span><span class="sxs-lookup"><span data-stu-id="c5f52-149">40</span></span> |
| <span data-ttu-id="c5f52-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-150">DW1200</span></span> |<span data-ttu-id="c5f52-151">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-151">32</span></span> |<span data-ttu-id="c5f52-152">48</span><span class="sxs-lookup"><span data-stu-id="c5f52-152">48</span></span> |
| <span data-ttu-id="c5f52-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-153">DW1500</span></span> |<span data-ttu-id="c5f52-154">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-154">32</span></span> |<span data-ttu-id="c5f52-155">60</span><span class="sxs-lookup"><span data-stu-id="c5f52-155">60</span></span> |
| <span data-ttu-id="c5f52-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-156">DW2000</span></span> |<span data-ttu-id="c5f52-157">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-157">32</span></span> |<span data-ttu-id="c5f52-158">80</span><span class="sxs-lookup"><span data-stu-id="c5f52-158">80</span></span> |
| <span data-ttu-id="c5f52-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-159">DW3000</span></span> |<span data-ttu-id="c5f52-160">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-160">32</span></span> |<span data-ttu-id="c5f52-161">120</span><span class="sxs-lookup"><span data-stu-id="c5f52-161">120</span></span> |
| <span data-ttu-id="c5f52-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-162">DW6000</span></span> |<span data-ttu-id="c5f52-163">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-163">32</span></span> |<span data-ttu-id="c5f52-164">240</span><span class="sxs-lookup"><span data-stu-id="c5f52-164">240</span></span> |

<span data-ttu-id="c5f52-165">當符合以上其中一個臨界值時，新的查詢將以先進先出順序排入佇列和執行。</span><span class="sxs-lookup"><span data-stu-id="c5f52-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="c5f52-166">當一個查詢完成，而查詢與插槽數目低於限制時，就會釋放已排入佇列的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-166">As a queries finishes and the number of queries and slots falls below the limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="c5f52-167">只針對動態管理檢視 (DMV) 或目錄檢視執行的 SELECT 查詢不受任何並行存取限制所控管。</span><span class="sxs-lookup"><span data-stu-id="c5f52-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of the concurrency limits.</span></span> <span data-ttu-id="c5f52-168">不論在系統上執行的查詢數目多寡，您都可監視該系統。</span><span class="sxs-lookup"><span data-stu-id="c5f52-168">You can monitor the system regardless of the number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="c5f52-169">資源類別</span><span class="sxs-lookup"><span data-stu-id="c5f52-169">Resource classes</span></span>
<span data-ttu-id="c5f52-170">資源類別可協助您控制指定給查詢的記憶體配置以及 CPU 週期。</span><span class="sxs-lookup"><span data-stu-id="c5f52-170">Resource classes help you control memory allocation and CPU cycles given to a query.</span></span> <span data-ttu-id="c5f52-171">您可以利用資料庫角色的形式對使用者指派兩種資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-171">You can assign two types of resource classes to a user in the form of database roles.</span></span> <span data-ttu-id="c5f52-172">這兩種資源類別如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5f52-172">The two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="c5f52-173">動態資源類別 (**smallrc、mediumrc、largerc、xlargerc**) 會根據目前的 DWU 來配置數量不一的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on the current DWU.</span></span> <span data-ttu-id="c5f52-174">這表示當您相應增加為較大的 DWU 時，您的查詢會自動獲得更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-174">This means that when you scale up to a larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="c5f52-175">靜態資源類別 (**staticrc10、staticrc20、staticrc30、staticrc40、staticrc50、staticrc60、staticrc70、staticrc80**) 則一律會配置相同數量的記憶體，不論目前的 DWU 有多大 (前提是 DWU 本身有足夠的記憶體)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate the same amount of memory regardless of the current DWU (provided that the DWU itself has enough memory).</span></span> <span data-ttu-id="c5f52-176">這表示在較大的 DWU 中，您將可以在每個資源類別中同時執行更多查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="c5f52-177">採用 **smallrc** 和 **staticrc10** 的使用者會獲得較小量的記憶體，且可利用較高的並行存取能力。</span><span class="sxs-lookup"><span data-stu-id="c5f52-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="c5f52-178">相反地，指派給 **xlargerc** 或 **staticrc80** 的使用者會獲得大量的記憶體，因此可並行執行的查詢較少。</span><span class="sxs-lookup"><span data-stu-id="c5f52-178">In contrast, users assigned to **xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="c5f52-179">根據預設，每位使用者都是小型資源類別 **smallrc** 的成員。</span><span class="sxs-lookup"><span data-stu-id="c5f52-179">By default, each user is a member of the small resource class, **smallrc**.</span></span> <span data-ttu-id="c5f52-180">`sp_addrolemember` 程序可用來增加資源類別，`sp_droprolemember` 則可用來減少資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-180">The procedure `sp_addrolemember` is used to increase the resource class, and `sp_droprolemember` is used to decrease the resource class.</span></span> <span data-ttu-id="c5f52-181">例如，此命令會將 loaduser 的資源類別增加為 **largerc**︰</span><span class="sxs-lookup"><span data-stu-id="c5f52-181">For example, this command would increase the resource class of loaduser to **largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="c5f52-182">不採用資源類別的查詢</span><span class="sxs-lookup"><span data-stu-id="c5f52-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="c5f52-183">有幾種查詢類別不會因較大的記憶體配置而受益。</span><span class="sxs-lookup"><span data-stu-id="c5f52-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="c5f52-184">系統會忽略它們的資源類別配置，並一律改為在小型資源類別中執行這些查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-184">The system ignores their resource class allocation and always run these queries in the small resource class instead.</span></span> <span data-ttu-id="c5f52-185">如果這些查詢一律會在小型資源類別中執行，它們就能在並行存取插槽有壓力時執行，而且只會取用所需的插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-185">If these queries always run in the small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="c5f52-186">如需詳細資訊，請參閱 [資源類別例外狀況](#query-exceptions-to-concurrency-limits) 。</span><span class="sxs-lookup"><span data-stu-id="c5f52-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="c5f52-187">資源類別指派的詳細資料</span><span class="sxs-lookup"><span data-stu-id="c5f52-187">Details on resource class assignment</span></span>


<span data-ttu-id="c5f52-188">資源類別的其他詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="c5f52-188">A few more details on resource class:</span></span>

* <span data-ttu-id="c5f52-189"> 權限，才能變更使用者的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-189">*Alter role* permission is required to change the resource class of a user.</span></span>
* <span data-ttu-id="c5f52-190">雖然您可以將使用者新增至一或多個較高的資源類別，但動態資源類別的優先順序高於靜態資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-190">Although you can add a user to one or more of the higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="c5f52-191">也就是說，如果您將使用者同時指派給 **mediumrc** (動態) 和 **staticrc80** (靜態)，則系統會採用 **mediumrc** 資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-191">That is, if a user is assigned to both **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is the resource class that is honored.</span></span>
 * <span data-ttu-id="c5f52-192">當您將使用者指派給特定資源類別類型中的多個資源類別 (多個動態資源類別或多個靜態資源類別) 時，系統會採用最高的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-192">When a user is assigned to more than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), the highest resource class is honored.</span></span> <span data-ttu-id="c5f52-193">也就是說，如果您將使用者同時指派給 mediumrc 和 largerc，則系統會採用較高的資源類別 (largerc)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-193">That is, if a user is assigned to both mediumrc and largerc, the higher resource class (largerc) is honored.</span></span> <span data-ttu-id="c5f52-194">而且，如果您將使用者指派給 **staticrc20** 和 **statirc80**，系統會採用 **staticrc80**。</span><span class="sxs-lookup"><span data-stu-id="c5f52-194">And if a user is assigned to both **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="c5f52-195">無法變更系統管理使用者的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-195">The resource class of the system administrative user cannot be changed.</span></span>

<span data-ttu-id="c5f52-196">如需詳細範例，請參閱 [變更使用者資源類別的範例](#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="c5f52-197">記憶體配置</span><span class="sxs-lookup"><span data-stu-id="c5f52-197">Memory allocation</span></span>
<span data-ttu-id="c5f52-198">提升使用者的資源類別有利有弊。</span><span class="sxs-lookup"><span data-stu-id="c5f52-198">There are pros and cons to increasing a user's resource class.</span></span> <span data-ttu-id="c5f52-199">提升使用者的資源類別可讓查詢存取更多記憶體，這表示查詢可能執行得更快。</span><span class="sxs-lookup"><span data-stu-id="c5f52-199">Increasing a resource class for a user, gives their queries access to more memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="c5f52-200">不過，較高的資源類別也會減少可以執行的並行查詢數目。</span><span class="sxs-lookup"><span data-stu-id="c5f52-200">However, higher resource classes also reduce the number of concurrent queries that can run.</span></span> <span data-ttu-id="c5f52-201">應該將大量記憶體配置給單一查詢，還是允許其他也需要配置記憶體的查詢並行執行，需要在這兩者之間進行取捨。</span><span class="sxs-lookup"><span data-stu-id="c5f52-201">This is the trade-off between allocating large amounts of memory to a single query or allowing other queries, which also need memory allocations, to run concurrently.</span></span> <span data-ttu-id="c5f52-202">如果為某一位使用者提供高記憶體配置進行查詢，則其他使用者將無法存取該相同記憶體來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-202">If one user is given high allocations of memory for a query, other users will not have access to that same memory to run a query.</span></span>

<span data-ttu-id="c5f52-203">下表依 DWU 和資源類別來對應所配置的記憶體與每個散發套件。</span><span class="sxs-lookup"><span data-stu-id="c5f52-203">The following table maps the memory allocated to each distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="c5f52-204">每個散發套件的動態資源類別 (MB) 記憶體配置</span><span class="sxs-lookup"><span data-stu-id="c5f52-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="c5f52-205">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-205">DWU</span></span> | <span data-ttu-id="c5f52-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-206">smallrc</span></span> | <span data-ttu-id="c5f52-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-207">mediumrc</span></span> | <span data-ttu-id="c5f52-208">largerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-208">largerc</span></span> | <span data-ttu-id="c5f52-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="c5f52-210">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-210">DW100</span></span> |<span data-ttu-id="c5f52-211">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-211">100</span></span> |<span data-ttu-id="c5f52-212">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-212">100</span></span> |<span data-ttu-id="c5f52-213">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-213">200</span></span> |<span data-ttu-id="c5f52-214">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-214">400</span></span> |
| <span data-ttu-id="c5f52-215">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-215">DW200</span></span> |<span data-ttu-id="c5f52-216">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-216">100</span></span> |<span data-ttu-id="c5f52-217">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-217">200</span></span> |<span data-ttu-id="c5f52-218">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-218">400</span></span> |<span data-ttu-id="c5f52-219">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-219">800</span></span> |
| <span data-ttu-id="c5f52-220">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-220">DW300</span></span> |<span data-ttu-id="c5f52-221">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-221">100</span></span> |<span data-ttu-id="c5f52-222">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-222">200</span></span> |<span data-ttu-id="c5f52-223">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-223">400</span></span> |<span data-ttu-id="c5f52-224">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-224">800</span></span> |
| <span data-ttu-id="c5f52-225">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-225">DW400</span></span> |<span data-ttu-id="c5f52-226">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-226">100</span></span> |<span data-ttu-id="c5f52-227">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-227">400</span></span> |<span data-ttu-id="c5f52-228">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-228">800</span></span> |<span data-ttu-id="c5f52-229">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-229">1,600</span></span> |
| <span data-ttu-id="c5f52-230">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-230">DW500</span></span> |<span data-ttu-id="c5f52-231">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-231">100</span></span> |<span data-ttu-id="c5f52-232">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-232">400</span></span> |<span data-ttu-id="c5f52-233">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-233">800</span></span> |<span data-ttu-id="c5f52-234">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-234">1,600</span></span> |
| <span data-ttu-id="c5f52-235">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-235">DW600</span></span> |<span data-ttu-id="c5f52-236">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-236">100</span></span> |<span data-ttu-id="c5f52-237">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-237">400</span></span> |<span data-ttu-id="c5f52-238">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-238">800</span></span> |<span data-ttu-id="c5f52-239">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-239">1,600</span></span> |
| <span data-ttu-id="c5f52-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-240">DW1000</span></span> |<span data-ttu-id="c5f52-241">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-241">100</span></span> |<span data-ttu-id="c5f52-242">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-242">800</span></span> |<span data-ttu-id="c5f52-243">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-243">1,600</span></span> |<span data-ttu-id="c5f52-244">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-244">3,200</span></span> |
| <span data-ttu-id="c5f52-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-245">DW1200</span></span> |<span data-ttu-id="c5f52-246">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-246">100</span></span> |<span data-ttu-id="c5f52-247">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-247">800</span></span> |<span data-ttu-id="c5f52-248">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-248">1,600</span></span> |<span data-ttu-id="c5f52-249">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-249">3,200</span></span> |
| <span data-ttu-id="c5f52-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-250">DW1500</span></span> |<span data-ttu-id="c5f52-251">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-251">100</span></span> |<span data-ttu-id="c5f52-252">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-252">800</span></span> |<span data-ttu-id="c5f52-253">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-253">1,600</span></span> |<span data-ttu-id="c5f52-254">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-254">3,200</span></span> |
| <span data-ttu-id="c5f52-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-255">DW2000</span></span> |<span data-ttu-id="c5f52-256">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-256">100</span></span> |<span data-ttu-id="c5f52-257">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-257">1,600</span></span> |<span data-ttu-id="c5f52-258">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-258">3,200</span></span> |<span data-ttu-id="c5f52-259">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-259">6,400</span></span> |
| <span data-ttu-id="c5f52-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-260">DW3000</span></span> |<span data-ttu-id="c5f52-261">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-261">100</span></span> |<span data-ttu-id="c5f52-262">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-262">1,600</span></span> |<span data-ttu-id="c5f52-263">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-263">3,200</span></span> |<span data-ttu-id="c5f52-264">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-264">6,400</span></span> |
| <span data-ttu-id="c5f52-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-265">DW6000</span></span> |<span data-ttu-id="c5f52-266">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-266">100</span></span> |<span data-ttu-id="c5f52-267">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-267">3,200</span></span> |<span data-ttu-id="c5f52-268">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-268">6,400</span></span> |<span data-ttu-id="c5f52-269">12,800</span><span class="sxs-lookup"><span data-stu-id="c5f52-269">12,800</span></span> |

<span data-ttu-id="c5f52-270">下表依 DWU 和靜態資源類別來對應所配置的記憶體與每個散發套件。</span><span class="sxs-lookup"><span data-stu-id="c5f52-270">The following table maps the memory allocated to each distribution by DWU and static resource class.</span></span> <span data-ttu-id="c5f52-271">請注意，較高的資源類別會縮減其記憶體，以採用全域的 DWU 限制。</span><span class="sxs-lookup"><span data-stu-id="c5f52-271">Note that the higher resource classes have their memory reduced to honor the global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="c5f52-272">每個散發套件的靜態資源類別 (MB) 記憶體配置</span><span class="sxs-lookup"><span data-stu-id="c5f52-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="c5f52-273">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-273">DWU</span></span> | <span data-ttu-id="c5f52-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="c5f52-274">staticrc10</span></span> | <span data-ttu-id="c5f52-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="c5f52-275">staticrc20</span></span> | <span data-ttu-id="c5f52-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="c5f52-276">staticrc30</span></span> | <span data-ttu-id="c5f52-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="c5f52-277">staticrc40</span></span> | <span data-ttu-id="c5f52-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="c5f52-278">staticrc50</span></span> | <span data-ttu-id="c5f52-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="c5f52-279">staticrc60</span></span> | <span data-ttu-id="c5f52-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="c5f52-280">staticrc70</span></span> | <span data-ttu-id="c5f52-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="c5f52-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="c5f52-282">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-282">DW100</span></span> |<span data-ttu-id="c5f52-283">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-283">100</span></span> |<span data-ttu-id="c5f52-284">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-284">200</span></span> |<span data-ttu-id="c5f52-285">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-285">400</span></span> |<span data-ttu-id="c5f52-286">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-286">400</span></span> |<span data-ttu-id="c5f52-287">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-287">400</span></span> |<span data-ttu-id="c5f52-288">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-288">400</span></span> |<span data-ttu-id="c5f52-289">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-289">400</span></span> |<span data-ttu-id="c5f52-290">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-290">400</span></span> |
| <span data-ttu-id="c5f52-291">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-291">DW200</span></span> |<span data-ttu-id="c5f52-292">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-292">100</span></span> |<span data-ttu-id="c5f52-293">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-293">200</span></span> |<span data-ttu-id="c5f52-294">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-294">400</span></span> |<span data-ttu-id="c5f52-295">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-295">800</span></span> |<span data-ttu-id="c5f52-296">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-296">800</span></span> |<span data-ttu-id="c5f52-297">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-297">800</span></span> |<span data-ttu-id="c5f52-298">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-298">800</span></span> |<span data-ttu-id="c5f52-299">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-299">800</span></span> |
| <span data-ttu-id="c5f52-300">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-300">DW300</span></span> |<span data-ttu-id="c5f52-301">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-301">100</span></span> |<span data-ttu-id="c5f52-302">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-302">200</span></span> |<span data-ttu-id="c5f52-303">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-303">400</span></span> |<span data-ttu-id="c5f52-304">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-304">800</span></span> |<span data-ttu-id="c5f52-305">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-305">800</span></span> |<span data-ttu-id="c5f52-306">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-306">800</span></span> |<span data-ttu-id="c5f52-307">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-307">800</span></span> |<span data-ttu-id="c5f52-308">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-308">800</span></span> |
| <span data-ttu-id="c5f52-309">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-309">DW400</span></span> |<span data-ttu-id="c5f52-310">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-310">100</span></span> |<span data-ttu-id="c5f52-311">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-311">200</span></span> |<span data-ttu-id="c5f52-312">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-312">400</span></span> |<span data-ttu-id="c5f52-313">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-313">800</span></span> |<span data-ttu-id="c5f52-314">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-314">1,600</span></span> |<span data-ttu-id="c5f52-315">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-315">1,600</span></span> |<span data-ttu-id="c5f52-316">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-316">1,600</span></span> |<span data-ttu-id="c5f52-317">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-317">1,600</span></span> |
| <span data-ttu-id="c5f52-318">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-318">DW500</span></span> |<span data-ttu-id="c5f52-319">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-319">100</span></span> |<span data-ttu-id="c5f52-320">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-320">200</span></span> |<span data-ttu-id="c5f52-321">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-321">400</span></span> |<span data-ttu-id="c5f52-322">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-322">800</span></span> |<span data-ttu-id="c5f52-323">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-323">1,600</span></span> |<span data-ttu-id="c5f52-324">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-324">1,600</span></span> |<span data-ttu-id="c5f52-325">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-325">1,600</span></span> |<span data-ttu-id="c5f52-326">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-326">1,600</span></span> |
| <span data-ttu-id="c5f52-327">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-327">DW600</span></span> |<span data-ttu-id="c5f52-328">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-328">100</span></span> |<span data-ttu-id="c5f52-329">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-329">200</span></span> |<span data-ttu-id="c5f52-330">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-330">400</span></span> |<span data-ttu-id="c5f52-331">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-331">800</span></span> |<span data-ttu-id="c5f52-332">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-332">1,600</span></span> |<span data-ttu-id="c5f52-333">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-333">1,600</span></span> |<span data-ttu-id="c5f52-334">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-334">1,600</span></span> |<span data-ttu-id="c5f52-335">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-335">1,600</span></span> |
| <span data-ttu-id="c5f52-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-336">DW1000</span></span> |<span data-ttu-id="c5f52-337">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-337">100</span></span> |<span data-ttu-id="c5f52-338">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-338">200</span></span> |<span data-ttu-id="c5f52-339">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-339">400</span></span> |<span data-ttu-id="c5f52-340">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-340">800</span></span> |<span data-ttu-id="c5f52-341">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-341">1,600</span></span> |<span data-ttu-id="c5f52-342">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-342">3,200</span></span> |<span data-ttu-id="c5f52-343">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-343">3,200</span></span> |<span data-ttu-id="c5f52-344">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-344">3,200</span></span> |
| <span data-ttu-id="c5f52-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-345">DW1200</span></span> |<span data-ttu-id="c5f52-346">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-346">100</span></span> |<span data-ttu-id="c5f52-347">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-347">200</span></span> |<span data-ttu-id="c5f52-348">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-348">400</span></span> |<span data-ttu-id="c5f52-349">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-349">800</span></span> |<span data-ttu-id="c5f52-350">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-350">1,600</span></span> |<span data-ttu-id="c5f52-351">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-351">3,200</span></span> |<span data-ttu-id="c5f52-352">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-352">3,200</span></span> |<span data-ttu-id="c5f52-353">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-353">3,200</span></span> |
| <span data-ttu-id="c5f52-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-354">DW1500</span></span> |<span data-ttu-id="c5f52-355">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-355">100</span></span> |<span data-ttu-id="c5f52-356">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-356">200</span></span> |<span data-ttu-id="c5f52-357">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-357">400</span></span> |<span data-ttu-id="c5f52-358">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-358">800</span></span> |<span data-ttu-id="c5f52-359">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-359">1,600</span></span> |<span data-ttu-id="c5f52-360">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-360">3,200</span></span> |<span data-ttu-id="c5f52-361">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-361">3,200</span></span> |<span data-ttu-id="c5f52-362">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-362">3,200</span></span> |
| <span data-ttu-id="c5f52-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-363">DW2000</span></span> |<span data-ttu-id="c5f52-364">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-364">100</span></span> |<span data-ttu-id="c5f52-365">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-365">200</span></span> |<span data-ttu-id="c5f52-366">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-366">400</span></span> |<span data-ttu-id="c5f52-367">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-367">800</span></span> |<span data-ttu-id="c5f52-368">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-368">1,600</span></span> |<span data-ttu-id="c5f52-369">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-369">3,200</span></span> |<span data-ttu-id="c5f52-370">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-370">6,400</span></span> |<span data-ttu-id="c5f52-371">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-371">6,400</span></span> |
| <span data-ttu-id="c5f52-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-372">DW3000</span></span> |<span data-ttu-id="c5f52-373">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-373">100</span></span> |<span data-ttu-id="c5f52-374">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-374">200</span></span> |<span data-ttu-id="c5f52-375">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-375">400</span></span> |<span data-ttu-id="c5f52-376">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-376">800</span></span> |<span data-ttu-id="c5f52-377">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-377">1,600</span></span> |<span data-ttu-id="c5f52-378">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-378">3,200</span></span> |<span data-ttu-id="c5f52-379">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-379">6,400</span></span> |<span data-ttu-id="c5f52-380">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-380">6,400</span></span> |
| <span data-ttu-id="c5f52-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-381">DW6000</span></span> |<span data-ttu-id="c5f52-382">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-382">100</span></span> |<span data-ttu-id="c5f52-383">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-383">200</span></span> |<span data-ttu-id="c5f52-384">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-384">400</span></span> |<span data-ttu-id="c5f52-385">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-385">800</span></span> |<span data-ttu-id="c5f52-386">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-386">1,600</span></span> |<span data-ttu-id="c5f52-387">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-387">3,200</span></span> |<span data-ttu-id="c5f52-388">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-388">6,400</span></span> |<span data-ttu-id="c5f52-389">12,800</span><span class="sxs-lookup"><span data-stu-id="c5f52-389">12,800</span></span> |

<span data-ttu-id="c5f52-390">從上表中，可知在 DW2000 上以 **xlargerc** 資源類別執行的查詢，可在 60 個分散式資料庫內各取得 6,400 MB 的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-390">From the preceding table, you can see that a query running on a DW2000 in the **xlargerc** resource class would have access to 6,400 MB of memory within each of the 60 distributed databases.</span></span>  <span data-ttu-id="c5f52-391">SQL 資料倉儲中有 60 個散發套件。</span><span class="sxs-lookup"><span data-stu-id="c5f52-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="c5f52-392">因此，若要計算給定資源類別中某個查詢的總記憶體配置，上述的值應該乘以 60。</span><span class="sxs-lookup"><span data-stu-id="c5f52-392">Therefore, to calculate the total memory allocation for a query in a given resource class, the above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="c5f52-393">全系統記憶體配置 (GB)</span><span class="sxs-lookup"><span data-stu-id="c5f52-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="c5f52-394">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-394">DWU</span></span> | <span data-ttu-id="c5f52-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-395">smallrc</span></span> | <span data-ttu-id="c5f52-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-396">mediumrc</span></span> | <span data-ttu-id="c5f52-397">largerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-397">largerc</span></span> | <span data-ttu-id="c5f52-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="c5f52-399">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-399">DW100</span></span> |<span data-ttu-id="c5f52-400">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-400">6</span></span> |<span data-ttu-id="c5f52-401">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-401">6</span></span> |<span data-ttu-id="c5f52-402">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-402">12</span></span> |<span data-ttu-id="c5f52-403">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-403">23</span></span> |
| <span data-ttu-id="c5f52-404">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-404">DW200</span></span> |<span data-ttu-id="c5f52-405">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-405">6</span></span> |<span data-ttu-id="c5f52-406">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-406">12</span></span> |<span data-ttu-id="c5f52-407">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-407">23</span></span> |<span data-ttu-id="c5f52-408">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-408">47</span></span> |
| <span data-ttu-id="c5f52-409">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-409">DW300</span></span> |<span data-ttu-id="c5f52-410">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-410">6</span></span> |<span data-ttu-id="c5f52-411">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-411">12</span></span> |<span data-ttu-id="c5f52-412">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-412">23</span></span> |<span data-ttu-id="c5f52-413">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-413">47</span></span> |
| <span data-ttu-id="c5f52-414">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-414">DW400</span></span> |<span data-ttu-id="c5f52-415">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-415">6</span></span> |<span data-ttu-id="c5f52-416">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-416">23</span></span> |<span data-ttu-id="c5f52-417">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-417">47</span></span> |<span data-ttu-id="c5f52-418">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-418">94</span></span> |
| <span data-ttu-id="c5f52-419">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-419">DW500</span></span> |<span data-ttu-id="c5f52-420">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-420">6</span></span> |<span data-ttu-id="c5f52-421">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-421">23</span></span> |<span data-ttu-id="c5f52-422">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-422">47</span></span> |<span data-ttu-id="c5f52-423">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-423">94</span></span> |
| <span data-ttu-id="c5f52-424">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-424">DW600</span></span> |<span data-ttu-id="c5f52-425">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-425">6</span></span> |<span data-ttu-id="c5f52-426">23</span><span class="sxs-lookup"><span data-stu-id="c5f52-426">23</span></span> |<span data-ttu-id="c5f52-427">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-427">47</span></span> |<span data-ttu-id="c5f52-428">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-428">94</span></span> |
| <span data-ttu-id="c5f52-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-429">DW1000</span></span> |<span data-ttu-id="c5f52-430">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-430">6</span></span> |<span data-ttu-id="c5f52-431">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-431">47</span></span> |<span data-ttu-id="c5f52-432">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-432">94</span></span> |<span data-ttu-id="c5f52-433">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-433">188</span></span> |
| <span data-ttu-id="c5f52-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-434">DW1200</span></span> |<span data-ttu-id="c5f52-435">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-435">6</span></span> |<span data-ttu-id="c5f52-436">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-436">47</span></span> |<span data-ttu-id="c5f52-437">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-437">94</span></span> |<span data-ttu-id="c5f52-438">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-438">188</span></span> |
| <span data-ttu-id="c5f52-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-439">DW1500</span></span> |<span data-ttu-id="c5f52-440">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-440">6</span></span> |<span data-ttu-id="c5f52-441">47</span><span class="sxs-lookup"><span data-stu-id="c5f52-441">47</span></span> |<span data-ttu-id="c5f52-442">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-442">94</span></span> |<span data-ttu-id="c5f52-443">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-443">188</span></span> |
| <span data-ttu-id="c5f52-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-444">DW2000</span></span> |<span data-ttu-id="c5f52-445">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-445">6</span></span> |<span data-ttu-id="c5f52-446">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-446">94</span></span> |<span data-ttu-id="c5f52-447">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-447">188</span></span> |<span data-ttu-id="c5f52-448">375</span><span class="sxs-lookup"><span data-stu-id="c5f52-448">375</span></span> |
| <span data-ttu-id="c5f52-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-449">DW3000</span></span> |<span data-ttu-id="c5f52-450">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-450">6</span></span> |<span data-ttu-id="c5f52-451">94</span><span class="sxs-lookup"><span data-stu-id="c5f52-451">94</span></span> |<span data-ttu-id="c5f52-452">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-452">188</span></span> |<span data-ttu-id="c5f52-453">375</span><span class="sxs-lookup"><span data-stu-id="c5f52-453">375</span></span> |
| <span data-ttu-id="c5f52-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-454">DW6000</span></span> |<span data-ttu-id="c5f52-455">6</span><span class="sxs-lookup"><span data-stu-id="c5f52-455">6</span></span> |<span data-ttu-id="c5f52-456">188</span><span class="sxs-lookup"><span data-stu-id="c5f52-456">188</span></span> |<span data-ttu-id="c5f52-457">375</span><span class="sxs-lookup"><span data-stu-id="c5f52-457">375</span></span> |<span data-ttu-id="c5f52-458">750</span><span class="sxs-lookup"><span data-stu-id="c5f52-458">750</span></span> |

<span data-ttu-id="c5f52-459">從以上的系統整體記憶體配置表格中，可知以 xlargerc 資源類別於 DW2000 上執行的查詢，會在整個 SQL 資料倉儲配置總共 375 GB 的記憶體 (6,400 MB * 60 個散發套件 / 1,024 以轉換為 GB)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in the xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 to convert to GB) over the entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="c5f52-460">靜態資源類別的計算方式也是這樣。</span><span class="sxs-lookup"><span data-stu-id="c5f52-460">The same calculation applies to static resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="c5f52-461">並行存取插槽耗用量</span><span class="sxs-lookup"><span data-stu-id="c5f52-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="c5f52-462">針對在更高資源類別中執行的查詢，SQL 資料倉儲會授與更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-462">SQL Data Warehouse grants more memory to queries running in higher resource classes.</span></span> <span data-ttu-id="c5f52-463">記憶體是固定的資源。</span><span class="sxs-lookup"><span data-stu-id="c5f52-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="c5f52-464">因此，配置給每個查詢的記憶體越多，可執行的並行查詢就越少。</span><span class="sxs-lookup"><span data-stu-id="c5f52-464">Therefore, the more memory allocated per query, the fewer concurrent queries can execute.</span></span> <span data-ttu-id="c5f52-465">下表會以單一檢視重述上述所有概念，其中顯示 DWU 可用的並行存取插槽數目和每個資源類別所取用的插槽數目。</span><span class="sxs-lookup"><span data-stu-id="c5f52-465">The following table reiterates all of the previous concepts in a single view that shows the number of concurrency slots available by DWU and the slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="c5f52-466">動態資源類別並行存取插槽的配置和耗用量</span><span class="sxs-lookup"><span data-stu-id="c5f52-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="c5f52-467">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-467">DWU</span></span> | <span data-ttu-id="c5f52-468">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="c5f52-468">Maximum concurrent queries</span></span> | <span data-ttu-id="c5f52-469">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-469">Concurrency slots allocated</span></span> | <span data-ttu-id="c5f52-470">Smallrc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-470">Slots used by smallrc</span></span> | <span data-ttu-id="c5f52-471">Mediumrc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-471">Slots used by mediumrc</span></span> | <span data-ttu-id="c5f52-472">Largerc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-472">Slots used by largerc</span></span> | <span data-ttu-id="c5f52-473">Xlargerc 所使用的插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="c5f52-474">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-474">DW100</span></span> |<span data-ttu-id="c5f52-475">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-475">4</span></span> |<span data-ttu-id="c5f52-476">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-476">4</span></span> |<span data-ttu-id="c5f52-477">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-477">1</span></span> |<span data-ttu-id="c5f52-478">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-478">1</span></span> |<span data-ttu-id="c5f52-479">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-479">2</span></span> |<span data-ttu-id="c5f52-480">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-480">4</span></span> |
| <span data-ttu-id="c5f52-481">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-481">DW200</span></span> |<span data-ttu-id="c5f52-482">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-482">8</span></span> |<span data-ttu-id="c5f52-483">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-483">8</span></span> |<span data-ttu-id="c5f52-484">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-484">1</span></span> |<span data-ttu-id="c5f52-485">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-485">2</span></span> |<span data-ttu-id="c5f52-486">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-486">4</span></span> |<span data-ttu-id="c5f52-487">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-487">8</span></span> |
| <span data-ttu-id="c5f52-488">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-488">DW300</span></span> |<span data-ttu-id="c5f52-489">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-489">12</span></span> |<span data-ttu-id="c5f52-490">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-490">12</span></span> |<span data-ttu-id="c5f52-491">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-491">1</span></span> |<span data-ttu-id="c5f52-492">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-492">2</span></span> |<span data-ttu-id="c5f52-493">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-493">4</span></span> |<span data-ttu-id="c5f52-494">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-494">8</span></span> |
| <span data-ttu-id="c5f52-495">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-495">DW400</span></span> |<span data-ttu-id="c5f52-496">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-496">16</span></span> |<span data-ttu-id="c5f52-497">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-497">16</span></span> |<span data-ttu-id="c5f52-498">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-498">1</span></span> |<span data-ttu-id="c5f52-499">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-499">4</span></span> |<span data-ttu-id="c5f52-500">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-500">8</span></span> |<span data-ttu-id="c5f52-501">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-501">16</span></span> |
| <span data-ttu-id="c5f52-502">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-502">DW500</span></span> |<span data-ttu-id="c5f52-503">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-503">20</span></span> |<span data-ttu-id="c5f52-504">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-504">20</span></span> |<span data-ttu-id="c5f52-505">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-505">1</span></span> |<span data-ttu-id="c5f52-506">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-506">4</span></span> |<span data-ttu-id="c5f52-507">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-507">8</span></span> |<span data-ttu-id="c5f52-508">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-508">16</span></span> |
| <span data-ttu-id="c5f52-509">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-509">DW600</span></span> |<span data-ttu-id="c5f52-510">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-510">24</span></span> |<span data-ttu-id="c5f52-511">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-511">24</span></span> |<span data-ttu-id="c5f52-512">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-512">1</span></span> |<span data-ttu-id="c5f52-513">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-513">4</span></span> |<span data-ttu-id="c5f52-514">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-514">8</span></span> |<span data-ttu-id="c5f52-515">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-515">16</span></span> |
| <span data-ttu-id="c5f52-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-516">DW1000</span></span> |<span data-ttu-id="c5f52-517">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-517">32</span></span> |<span data-ttu-id="c5f52-518">40</span><span class="sxs-lookup"><span data-stu-id="c5f52-518">40</span></span> |<span data-ttu-id="c5f52-519">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-519">1</span></span> |<span data-ttu-id="c5f52-520">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-520">8</span></span> |<span data-ttu-id="c5f52-521">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-521">16</span></span> |<span data-ttu-id="c5f52-522">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-522">32</span></span> |
| <span data-ttu-id="c5f52-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-523">DW1200</span></span> |<span data-ttu-id="c5f52-524">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-524">32</span></span> |<span data-ttu-id="c5f52-525">48</span><span class="sxs-lookup"><span data-stu-id="c5f52-525">48</span></span> |<span data-ttu-id="c5f52-526">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-526">1</span></span> |<span data-ttu-id="c5f52-527">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-527">8</span></span> |<span data-ttu-id="c5f52-528">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-528">16</span></span> |<span data-ttu-id="c5f52-529">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-529">32</span></span> |
| <span data-ttu-id="c5f52-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-530">DW1500</span></span> |<span data-ttu-id="c5f52-531">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-531">32</span></span> |<span data-ttu-id="c5f52-532">60</span><span class="sxs-lookup"><span data-stu-id="c5f52-532">60</span></span> |<span data-ttu-id="c5f52-533">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-533">1</span></span> |<span data-ttu-id="c5f52-534">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-534">8</span></span> |<span data-ttu-id="c5f52-535">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-535">16</span></span> |<span data-ttu-id="c5f52-536">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-536">32</span></span> |
| <span data-ttu-id="c5f52-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-537">DW2000</span></span> |<span data-ttu-id="c5f52-538">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-538">32</span></span> |<span data-ttu-id="c5f52-539">80</span><span class="sxs-lookup"><span data-stu-id="c5f52-539">80</span></span> |<span data-ttu-id="c5f52-540">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-540">1</span></span> |<span data-ttu-id="c5f52-541">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-541">16</span></span> |<span data-ttu-id="c5f52-542">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-542">32</span></span> |<span data-ttu-id="c5f52-543">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-543">64</span></span> |
| <span data-ttu-id="c5f52-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-544">DW3000</span></span> |<span data-ttu-id="c5f52-545">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-545">32</span></span> |<span data-ttu-id="c5f52-546">120</span><span class="sxs-lookup"><span data-stu-id="c5f52-546">120</span></span> |<span data-ttu-id="c5f52-547">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-547">1</span></span> |<span data-ttu-id="c5f52-548">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-548">16</span></span> |<span data-ttu-id="c5f52-549">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-549">32</span></span> |<span data-ttu-id="c5f52-550">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-550">64</span></span> |
| <span data-ttu-id="c5f52-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-551">DW6000</span></span> |<span data-ttu-id="c5f52-552">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-552">32</span></span> |<span data-ttu-id="c5f52-553">240</span><span class="sxs-lookup"><span data-stu-id="c5f52-553">240</span></span> |<span data-ttu-id="c5f52-554">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-554">1</span></span> |<span data-ttu-id="c5f52-555">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-555">32</span></span> |<span data-ttu-id="c5f52-556">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-556">64</span></span> |<span data-ttu-id="c5f52-557">128</span><span class="sxs-lookup"><span data-stu-id="c5f52-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="c5f52-558">靜態資源類別並行存取插槽的配置和耗用量</span><span class="sxs-lookup"><span data-stu-id="c5f52-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="c5f52-559">DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-559">DWU</span></span> | <span data-ttu-id="c5f52-560">並行查詢上限</span><span class="sxs-lookup"><span data-stu-id="c5f52-560">Maximum concurrent queries</span></span> | <span data-ttu-id="c5f52-561">配置的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-561">Concurrency slots allocated</span></span> |<span data-ttu-id="c5f52-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="c5f52-562">staticrc10</span></span> | <span data-ttu-id="c5f52-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="c5f52-563">staticrc20</span></span> | <span data-ttu-id="c5f52-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="c5f52-564">staticrc30</span></span> | <span data-ttu-id="c5f52-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="c5f52-565">staticrc40</span></span> | <span data-ttu-id="c5f52-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="c5f52-566">staticrc50</span></span> | <span data-ttu-id="c5f52-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="c5f52-567">staticrc60</span></span> | <span data-ttu-id="c5f52-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="c5f52-568">staticrc70</span></span> | <span data-ttu-id="c5f52-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="c5f52-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="c5f52-570">DW100</span><span class="sxs-lookup"><span data-stu-id="c5f52-570">DW100</span></span> |<span data-ttu-id="c5f52-571">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-571">4</span></span> |<span data-ttu-id="c5f52-572">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-572">4</span></span> |<span data-ttu-id="c5f52-573">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-573">1</span></span> |<span data-ttu-id="c5f52-574">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-574">2</span></span> |<span data-ttu-id="c5f52-575">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-575">4</span></span> |<span data-ttu-id="c5f52-576">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-576">4</span></span> |<span data-ttu-id="c5f52-577">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-577">4</span></span> |<span data-ttu-id="c5f52-578">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-578">4</span></span> |<span data-ttu-id="c5f52-579">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-579">4</span></span> |<span data-ttu-id="c5f52-580">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-580">4</span></span> |
| <span data-ttu-id="c5f52-581">DW200</span><span class="sxs-lookup"><span data-stu-id="c5f52-581">DW200</span></span> |<span data-ttu-id="c5f52-582">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-582">8</span></span> |<span data-ttu-id="c5f52-583">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-583">8</span></span> |<span data-ttu-id="c5f52-584">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-584">1</span></span> |<span data-ttu-id="c5f52-585">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-585">2</span></span> |<span data-ttu-id="c5f52-586">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-586">4</span></span> |<span data-ttu-id="c5f52-587">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-587">8</span></span> |<span data-ttu-id="c5f52-588">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-588">8</span></span> |<span data-ttu-id="c5f52-589">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-589">8</span></span> |<span data-ttu-id="c5f52-590">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-590">8</span></span> |<span data-ttu-id="c5f52-591">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-591">8</span></span> |
| <span data-ttu-id="c5f52-592">DW300</span><span class="sxs-lookup"><span data-stu-id="c5f52-592">DW300</span></span> |<span data-ttu-id="c5f52-593">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-593">12</span></span> |<span data-ttu-id="c5f52-594">12</span><span class="sxs-lookup"><span data-stu-id="c5f52-594">12</span></span> |<span data-ttu-id="c5f52-595">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-595">1</span></span> |<span data-ttu-id="c5f52-596">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-596">2</span></span> |<span data-ttu-id="c5f52-597">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-597">4</span></span> |<span data-ttu-id="c5f52-598">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-598">8</span></span> |<span data-ttu-id="c5f52-599">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-599">8</span></span> |<span data-ttu-id="c5f52-600">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-600">8</span></span> |<span data-ttu-id="c5f52-601">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-601">8</span></span> |<span data-ttu-id="c5f52-602">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-602">8</span></span> |
| <span data-ttu-id="c5f52-603">DW400</span><span class="sxs-lookup"><span data-stu-id="c5f52-603">DW400</span></span> |<span data-ttu-id="c5f52-604">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-604">16</span></span> |<span data-ttu-id="c5f52-605">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-605">16</span></span> |<span data-ttu-id="c5f52-606">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-606">1</span></span> |<span data-ttu-id="c5f52-607">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-607">2</span></span> |<span data-ttu-id="c5f52-608">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-608">4</span></span> |<span data-ttu-id="c5f52-609">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-609">8</span></span> |<span data-ttu-id="c5f52-610">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-610">16</span></span> |<span data-ttu-id="c5f52-611">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-611">16</span></span> |<span data-ttu-id="c5f52-612">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-612">16</span></span> |<span data-ttu-id="c5f52-613">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-613">16</span></span> |
| <span data-ttu-id="c5f52-614">DW500</span><span class="sxs-lookup"><span data-stu-id="c5f52-614">DW500</span></span> | <span data-ttu-id="c5f52-615">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-615">20</span></span>| <span data-ttu-id="c5f52-616">20</span><span class="sxs-lookup"><span data-stu-id="c5f52-616">20</span></span>| <span data-ttu-id="c5f52-617">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-617">1</span></span>| <span data-ttu-id="c5f52-618">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-618">2</span></span>| <span data-ttu-id="c5f52-619">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-619">4</span></span>| <span data-ttu-id="c5f52-620">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-620">8</span></span>| <span data-ttu-id="c5f52-621">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-621">16</span></span>| <span data-ttu-id="c5f52-622">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-622">16</span></span>| <span data-ttu-id="c5f52-623">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-623">16</span></span>| <span data-ttu-id="c5f52-624">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-624">16</span></span>|
| <span data-ttu-id="c5f52-625">DW600</span><span class="sxs-lookup"><span data-stu-id="c5f52-625">DW600</span></span> | <span data-ttu-id="c5f52-626">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-626">24</span></span>| <span data-ttu-id="c5f52-627">24</span><span class="sxs-lookup"><span data-stu-id="c5f52-627">24</span></span>| <span data-ttu-id="c5f52-628">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-628">1</span></span>| <span data-ttu-id="c5f52-629">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-629">2</span></span>| <span data-ttu-id="c5f52-630">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-630">4</span></span>| <span data-ttu-id="c5f52-631">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-631">8</span></span>| <span data-ttu-id="c5f52-632">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-632">16</span></span>| <span data-ttu-id="c5f52-633">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-633">16</span></span>| <span data-ttu-id="c5f52-634">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-634">16</span></span>| <span data-ttu-id="c5f52-635">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-635">16</span></span>|
| <span data-ttu-id="c5f52-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="c5f52-636">DW1000</span></span> | <span data-ttu-id="c5f52-637">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-637">32</span></span>| <span data-ttu-id="c5f52-638">40</span><span class="sxs-lookup"><span data-stu-id="c5f52-638">40</span></span>| <span data-ttu-id="c5f52-639">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-639">1</span></span>| <span data-ttu-id="c5f52-640">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-640">2</span></span>| <span data-ttu-id="c5f52-641">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-641">4</span></span>| <span data-ttu-id="c5f52-642">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-642">8</span></span>| <span data-ttu-id="c5f52-643">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-643">16</span></span>| <span data-ttu-id="c5f52-644">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-644">32</span></span>| <span data-ttu-id="c5f52-645">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-645">32</span></span>| <span data-ttu-id="c5f52-646">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-646">32</span></span>|
| <span data-ttu-id="c5f52-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="c5f52-647">DW1200</span></span> | <span data-ttu-id="c5f52-648">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-648">32</span></span>| <span data-ttu-id="c5f52-649">48</span><span class="sxs-lookup"><span data-stu-id="c5f52-649">48</span></span>| <span data-ttu-id="c5f52-650">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-650">1</span></span>| <span data-ttu-id="c5f52-651">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-651">2</span></span>| <span data-ttu-id="c5f52-652">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-652">4</span></span>| <span data-ttu-id="c5f52-653">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-653">8</span></span>| <span data-ttu-id="c5f52-654">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-654">16</span></span>| <span data-ttu-id="c5f52-655">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-655">32</span></span>| <span data-ttu-id="c5f52-656">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-656">32</span></span>| <span data-ttu-id="c5f52-657">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-657">32</span></span>|
| <span data-ttu-id="c5f52-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="c5f52-658">DW1500</span></span> | <span data-ttu-id="c5f52-659">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-659">32</span></span>| <span data-ttu-id="c5f52-660">60</span><span class="sxs-lookup"><span data-stu-id="c5f52-660">60</span></span>| <span data-ttu-id="c5f52-661">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-661">1</span></span>| <span data-ttu-id="c5f52-662">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-662">2</span></span>| <span data-ttu-id="c5f52-663">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-663">4</span></span>| <span data-ttu-id="c5f52-664">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-664">8</span></span>| <span data-ttu-id="c5f52-665">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-665">16</span></span>| <span data-ttu-id="c5f52-666">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-666">32</span></span>| <span data-ttu-id="c5f52-667">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-667">32</span></span>| <span data-ttu-id="c5f52-668">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-668">32</span></span>|
| <span data-ttu-id="c5f52-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="c5f52-669">DW2000</span></span> | <span data-ttu-id="c5f52-670">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-670">32</span></span>| <span data-ttu-id="c5f52-671">80</span><span class="sxs-lookup"><span data-stu-id="c5f52-671">80</span></span>| <span data-ttu-id="c5f52-672">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-672">1</span></span>| <span data-ttu-id="c5f52-673">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-673">2</span></span>| <span data-ttu-id="c5f52-674">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-674">4</span></span>| <span data-ttu-id="c5f52-675">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-675">8</span></span>| <span data-ttu-id="c5f52-676">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-676">16</span></span>| <span data-ttu-id="c5f52-677">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-677">32</span></span>| <span data-ttu-id="c5f52-678">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-678">64</span></span>| <span data-ttu-id="c5f52-679">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-679">64</span></span>|
| <span data-ttu-id="c5f52-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="c5f52-680">DW3000</span></span> | <span data-ttu-id="c5f52-681">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-681">32</span></span>| <span data-ttu-id="c5f52-682">120</span><span class="sxs-lookup"><span data-stu-id="c5f52-682">120</span></span>| <span data-ttu-id="c5f52-683">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-683">1</span></span>| <span data-ttu-id="c5f52-684">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-684">2</span></span>| <span data-ttu-id="c5f52-685">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-685">4</span></span>| <span data-ttu-id="c5f52-686">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-686">8</span></span>| <span data-ttu-id="c5f52-687">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-687">16</span></span>| <span data-ttu-id="c5f52-688">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-688">32</span></span>| <span data-ttu-id="c5f52-689">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-689">64</span></span>| <span data-ttu-id="c5f52-690">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-690">64</span></span>|
| <span data-ttu-id="c5f52-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="c5f52-691">DW6000</span></span> | <span data-ttu-id="c5f52-692">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-692">32</span></span>| <span data-ttu-id="c5f52-693">240</span><span class="sxs-lookup"><span data-stu-id="c5f52-693">240</span></span>| <span data-ttu-id="c5f52-694">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-694">1</span></span>| <span data-ttu-id="c5f52-695">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-695">2</span></span>| <span data-ttu-id="c5f52-696">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-696">4</span></span>| <span data-ttu-id="c5f52-697">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-697">8</span></span>| <span data-ttu-id="c5f52-698">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-698">16</span></span>| <span data-ttu-id="c5f52-699">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-699">32</span></span>| <span data-ttu-id="c5f52-700">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-700">64</span></span>| <span data-ttu-id="c5f52-701">128</span><span class="sxs-lookup"><span data-stu-id="c5f52-701">128</span></span>|

<span data-ttu-id="c5f52-702">從上述表格中，您會看到以 DW1000 身分執行的 SQL 資料倉儲，配置最多 32 個並行查詢，以及總數 40 個的並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="c5f52-703">如果所有的使用者都以 smallrc 執行，將允許 32 個並行查詢，因為每個查詢會取用 1 個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="c5f52-704">如果 DW1000 上的所有使用者都是在 mediumrc 中執行，則會針對每個散發套件為各個查詢各配置 800 MB，每個查詢的總記憶體配置為 47 GB，且將並行存取限制為 5 位使用者 (40 個並行存取插槽 / 每位 mediumrc 使用者 8 個插槽)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited to 5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="c5f52-705">選取適當的資源類別</span><span class="sxs-lookup"><span data-stu-id="c5f52-705">Selecting proper resource class</span></span>  
<span data-ttu-id="c5f52-706">理想的作法是將使用者永久指派給資源類別，而不是變更他們的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-706">A good practice is to permanently assign users to a resource class rather than changing their resource classes.</span></span> <span data-ttu-id="c5f52-707">例如，在配置了更多記憶體時，叢集資料行存放區資料表的載入會建立更高品質的索引。</span><span class="sxs-lookup"><span data-stu-id="c5f52-707">For example, loads to clustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="c5f52-708">若要確保載入可以取得更高的記憶體，請建立特別用來載入資料的使用者，並將使用者永久指派給較高的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-708">To ensure that loads have access to higher memory, create a user specifically for loading data and permanently assign this user to a higher resource class.</span></span>
<span data-ttu-id="c5f52-709">以下是幾種可供採用的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="c5f52-709">There are a couple of best practices to follow here.</span></span> <span data-ttu-id="c5f52-710">如上所述，SQL DW 支援兩種資源類別類型：靜態資源類別和動態資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="c5f52-711">載入的最佳做法</span><span class="sxs-lookup"><span data-stu-id="c5f52-711">Loading best practices</span></span>
1.  <span data-ttu-id="c5f52-712">如果預期的載入具有一般數量的資料，則靜態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="c5f52-712">If the expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="c5f52-713">之後當您相應增加系統以獲得更多運算能力時，資料倉儲將能夠立即執行更多的並行查詢，因為載入使用者不會耗用更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-713">Later, when scaling up to get more computational power, the data warehouse will be able to run more concurrent queries out-of-the-box, as the load user does not consume more memory.</span></span>
2.  <span data-ttu-id="c5f52-714">如果在某些情況下預期會有更大的載入，則動態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="c5f52-714">If the expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="c5f52-715">之後當您相應增加系統以獲得更多運算能力時，載入使用者會獲得更多立即可用的記憶體，因此可讓載入提高執行速度。</span><span class="sxs-lookup"><span data-stu-id="c5f52-715">Later, when scaling up to get more computational power, the load user will get more memory out-of-the-box, hence allowing the load to perform faster.</span></span>

<span data-ttu-id="c5f52-716">若要有效率地處理載入，所需的記憶體取決於所載入之資料表的性質和所處理的資料量。</span><span class="sxs-lookup"><span data-stu-id="c5f52-716">The memory needed to process loads efficiently depends on the nature of the table loaded and the amount of data processed.</span></span> <span data-ttu-id="c5f52-717">例如，將資料載入到 CCI 資料表需要使用一些記憶體，來讓 CCI 資料列群組達到最適化。</span><span class="sxs-lookup"><span data-stu-id="c5f52-717">For instance, loading data into CCI tables requires some memory to let CCI rowgroups reach optimality.</span></span> <span data-ttu-id="c5f52-718">如需詳細資訊，請參閱「資料行存放區索引 - 資料載入」指引。</span><span class="sxs-lookup"><span data-stu-id="c5f52-718">For more details, see the Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="c5f52-719">我們會建議您採用的最佳做法是，至少提供 200 MB 的記憶體供載入使用。</span><span class="sxs-lookup"><span data-stu-id="c5f52-719">As a best practice, we advise you to use at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="c5f52-720">查詢的最佳做法</span><span class="sxs-lookup"><span data-stu-id="c5f52-720">Querying best practices</span></span>
<span data-ttu-id="c5f52-721">查詢會因其複雜性而有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="c5f52-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="c5f52-722">視查詢需求而定，增加每個查詢的記憶體或增加並行存取能力都能有效地增加整體的輸送量。</span><span class="sxs-lookup"><span data-stu-id="c5f52-722">Increasing memory per query or increasing the concurrency are both valid ways to augment overall throughput depending on the query needs.</span></span>
1.  <span data-ttu-id="c5f52-723">如果預期進行的是定期的複雜查詢 (例如，要產生每日及每週報告)，而且不需要利用並行存取能力，則動態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="c5f52-723">If the expectations are regular, complex queries (for instance, to generate daily and weekly reports) and do not need to take advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="c5f52-724">如果系統要處理的資料變多，相應增加資料倉儲會因此自動提供更多的記憶體供執行查詢的使用者使用。</span><span class="sxs-lookup"><span data-stu-id="c5f52-724">If the system has more data to process, scaling up the data warehouse will therefore automatically provide more memory to the user running the query.</span></span>
2.  <span data-ttu-id="c5f52-725">如果預期進行的是變動或日常的並行存取模式 (例如，如果透過可供廣泛存取的 Web UI 來查詢資料庫)，則靜態資源類別是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="c5f52-725">If the expectations are variable or diurnal concurrency patterns (for instance if the database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="c5f52-726">之後當您相應增加資料倉儲時，與靜態資源類別相關聯的使用者就能夠自動執行更多的並行查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-726">Later, when scaling up to data warehouse, the user associated with the static resource class will automatically be able to run more concurrent queries.</span></span>

<span data-ttu-id="c5f52-727">根據查詢需求來選取要授與的適當記憶體並不容易，因為這取決於許多因素，例如所查詢的資料量、資料表結構描述的性質，以及各種聯結、選取和群組述詞。</span><span class="sxs-lookup"><span data-stu-id="c5f52-727">Selecting proper memory grant depending on the need of your query is non-trivial, as it depends on many factors, such as the amount of data queried, the nature of the table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="c5f52-728">一般來說，配置更多的記憶體會讓查詢更快完成，但會減少整體的並行存取能力。</span><span class="sxs-lookup"><span data-stu-id="c5f52-728">From a general standpoint, allocating more memory will allow queries to complete faster, but would reduce the overall concurrency.</span></span> <span data-ttu-id="c5f52-729">如果您不在意並行存取能力，則可以放心地超額配置記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="c5f52-730">若要微調輸送量，您可能需要嘗試不同的資源類別組合。</span><span class="sxs-lookup"><span data-stu-id="c5f52-730">To fine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="c5f52-731">您可以使用下列預存程序，找出在給定 SLO 時要對每個資源類別授與的並行存取能力和記憶體，以及在給定資源類別時最適合非分割 CCI 資料表上的記憶體密集 CCI 作業使用的最接近資源類別：</span><span class="sxs-lookup"><span data-stu-id="c5f52-731">You can use the following stored procedure to figure out concurrency and memory grant per resource class at a given SLO and the closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="c5f52-732">Description:</span><span class="sxs-lookup"><span data-stu-id="c5f52-732">Description:</span></span>  
<span data-ttu-id="c5f52-733">以下是此預存程序的用途：</span><span class="sxs-lookup"><span data-stu-id="c5f52-733">Here's the purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="c5f52-734">協助使用者找出在給定 SLO 時，要對每個資源類別授與的並行存取能力和記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-734">To help user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="c5f52-735">為此，使用者必須同時為結構描述和 tablename 提供 NULL，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c5f52-735">User needs to provide NULL for both schema and tablename for this as shown in the example below.</span></span>  
2. <span data-ttu-id="c5f52-736">協助使用者找出在給定資源類別時，最適合非分割 CCI 資料表上的記憶體密集 CCI 作業 (載入、複製資料表、重建索引等) 使用的最接近資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-736">To help user figure out the closest best resource class for the memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="c5f52-737">此預存程序會使用資料表結構描述來找出為此所需授與的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5f52-737">The stored proc uses table schema to find out the required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="c5f52-738">相依性及限制：</span><span class="sxs-lookup"><span data-stu-id="c5f52-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="c5f52-739">此預存程序並非設計來計算分割 CCI 資料表的記憶體需求。</span><span class="sxs-lookup"><span data-stu-id="c5f52-739">This stored proc is not designed to calculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="c5f52-740">此預存程序不會針對 CTAS/INSERT-SELECT 的 SELECT 部分考慮記憶體需求，而是會假設它是簡單的 SELECT。</span><span class="sxs-lookup"><span data-stu-id="c5f52-740">This stored proc doesn't take memory requirement into account for the SELECT part of CTAS/INSERT-SELECT and assumes it to be a simple SELECT.</span></span>
- <span data-ttu-id="c5f52-741">此預存程序會使用暫存資料表，因此可用於此預存程序建立所在的工作階段。</span><span class="sxs-lookup"><span data-stu-id="c5f52-741">This stored proc uses a temp table so this can be used in the session where this stored proc was created.</span></span>    
- <span data-ttu-id="c5f52-742">此預存程序仰賴目前的供應項目 (例如，硬體組態、DMS 組態)，如果其中有任何變更，此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="c5f52-742">This stored proc depends on the current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="c5f52-743">此預存程序仰賴目前提供的並行存取限制，如果限制有任何變更，此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="c5f52-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="c5f52-744">此預存程序仰賴現有的資源類別供應項目，如果其中有任何變更，此預存程序就無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="c5f52-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="c5f52-745">如果您在使用所提供的參數來執行預存程序後沒有取得輸出，則可能有兩種情況。</span><span class="sxs-lookup"><span data-stu-id="c5f52-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="c5f52-746">1.DW 參數包含無效的 SLO 值</span><span class="sxs-lookup"><span data-stu-id="c5f52-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="c5f52-747">2.沒有符合 CCI 作業的資源類別 (若已提供資料表名稱)。</span><span class="sxs-lookup"><span data-stu-id="c5f52-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="c5f52-748">例如，在 DW100 時，可供授與的最高記憶體為 400 MB，但資料表結構描述的寬度卻足以跨過 400 MB 的需求。</span><span class="sxs-lookup"><span data-stu-id="c5f52-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough to cross the requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="c5f52-749">使用範例：</span><span class="sxs-lookup"><span data-stu-id="c5f52-749">Usage example:</span></span>
<span data-ttu-id="c5f52-750">語法：</span><span class="sxs-lookup"><span data-stu-id="c5f52-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="c5f52-751">@DWU: 提供 NULL 參數以從資料倉儲資料庫擷取目前的 DWU，或是以 'DW100' 的形式提供任何受支援的 DWU</span><span class="sxs-lookup"><span data-stu-id="c5f52-751">@DWU: Either provide a NULL parameter to extract the current DWU from the DW DB or provide any supported DWU in the form of 'DW100'</span></span>
2. <span data-ttu-id="c5f52-752">@SCHEMA_NAME: 提供資料表的結構描述名稱</span><span class="sxs-lookup"><span data-stu-id="c5f52-752">@SCHEMA_NAME: Provide a schema name of the table</span></span>
3. <span data-ttu-id="c5f52-753">@TABLE_NAME: 提供相關的資料表名稱</span><span class="sxs-lookup"><span data-stu-id="c5f52-753">@TABLE_NAME: Provide a table name of the interest</span></span>

<span data-ttu-id="c5f52-754">執行此預存程序的範例：</span><span class="sxs-lookup"><span data-stu-id="c5f52-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="c5f52-755">上述範例中使用的 Table1 會以如下方式建立：</span><span class="sxs-lookup"><span data-stu-id="c5f52-755">Table1 used in the above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-the-stored-procedure-definition"></a><span data-ttu-id="c5f52-756">以下是預存程序定義：</span><span class="sxs-lookup"><span data-stu-id="c5f52-756">Here's the stored procedure definition:</span></span>
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
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) to hold mapping info.
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
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
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

## <a name="query-importance"></a><span data-ttu-id="c5f52-757">查詢的重要性</span><span class="sxs-lookup"><span data-stu-id="c5f52-757">Query importance</span></span>
<span data-ttu-id="c5f52-758">SQL 資料倉儲使用工作負載群組來實作資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="c5f52-759">共有八個工作負載群組，它們可跨各種 DWU 大小控制資源類別的行為。</span><span class="sxs-lookup"><span data-stu-id="c5f52-759">There are a total of eight workload groups that control the behavior of the resource classes across the various DWU sizes.</span></span> <span data-ttu-id="c5f52-760">對於任何 DWU，SQL 資料倉儲只會使用這八個工作負載群組的其中四個。</span><span class="sxs-lookup"><span data-stu-id="c5f52-760">For any DWU, SQL Data Warehouse uses only four of the eight workload groups.</span></span> <span data-ttu-id="c5f52-761">這很合理，因為每個工作負載群組都會指派給四個資源類別之一：smallrc、mediumrc、largerc 或 xlargerc。</span><span class="sxs-lookup"><span data-stu-id="c5f52-761">This makes sense because each workload group is assigned to one of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="c5f52-762">了解這些工作負載群組的重要性在於其中某些工作負載群組會設定為較高的「重要性」 。</span><span class="sxs-lookup"><span data-stu-id="c5f52-762">The importance of understanding the workload groups is that some of these workload groups are set to higher *importance*.</span></span> <span data-ttu-id="c5f52-763">重要性可用於 CPU 排程。</span><span class="sxs-lookup"><span data-stu-id="c5f52-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="c5f52-764">以高重要性執行的查詢會取得比中度重要性的查詢高三倍的 CPU 週期。</span><span class="sxs-lookup"><span data-stu-id="c5f52-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="c5f52-765">因此，並行存取插槽對應也會判斷 CPU 優先順序。</span><span class="sxs-lookup"><span data-stu-id="c5f52-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="c5f52-766">當查詢取用 16 個以上的插槽時，就會以高重要性執行。</span><span class="sxs-lookup"><span data-stu-id="c5f52-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="c5f52-767">下表是每個工作負載群組的重要性對應。</span><span class="sxs-lookup"><span data-stu-id="c5f52-767">The following table shows the importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-to-concurrency-slots-and-importance"></a><span data-ttu-id="c5f52-768">工作負載群組與並行存取插槽數目和重要性的對應</span><span class="sxs-lookup"><span data-stu-id="c5f52-768">Workload group mappings to concurrency slots and importance</span></span>
| <span data-ttu-id="c5f52-769">工作負載群組</span><span class="sxs-lookup"><span data-stu-id="c5f52-769">Workload groups</span></span> | <span data-ttu-id="c5f52-770">並行存取插槽對應</span><span class="sxs-lookup"><span data-stu-id="c5f52-770">Concurrency slot mapping</span></span> | <span data-ttu-id="c5f52-771">MB / 散發套件</span><span class="sxs-lookup"><span data-stu-id="c5f52-771">MB / Distribution</span></span> | <span data-ttu-id="c5f52-772">重要性對應</span><span class="sxs-lookup"><span data-stu-id="c5f52-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="c5f52-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="c5f52-773">SloDWGroupC00</span></span> |<span data-ttu-id="c5f52-774">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-774">1</span></span> |<span data-ttu-id="c5f52-775">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-775">100</span></span> |<span data-ttu-id="c5f52-776">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-776">Medium</span></span> |
| <span data-ttu-id="c5f52-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="c5f52-777">SloDWGroupC01</span></span> |<span data-ttu-id="c5f52-778">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-778">2</span></span> |<span data-ttu-id="c5f52-779">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-779">200</span></span> |<span data-ttu-id="c5f52-780">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-780">Medium</span></span> |
| <span data-ttu-id="c5f52-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="c5f52-781">SloDWGroupC02</span></span> |<span data-ttu-id="c5f52-782">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-782">4</span></span> |<span data-ttu-id="c5f52-783">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-783">400</span></span> |<span data-ttu-id="c5f52-784">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-784">Medium</span></span> |
| <span data-ttu-id="c5f52-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-785">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-786">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-786">8</span></span> |<span data-ttu-id="c5f52-787">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-787">800</span></span> |<span data-ttu-id="c5f52-788">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-788">Medium</span></span> |
| <span data-ttu-id="c5f52-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="c5f52-789">SloDWGroupC04</span></span> |<span data-ttu-id="c5f52-790">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-790">16</span></span> |<span data-ttu-id="c5f52-791">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-791">1,600</span></span> |<span data-ttu-id="c5f52-792">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-792">High</span></span> |
| <span data-ttu-id="c5f52-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="c5f52-793">SloDWGroupC05</span></span> |<span data-ttu-id="c5f52-794">32</span><span class="sxs-lookup"><span data-stu-id="c5f52-794">32</span></span> |<span data-ttu-id="c5f52-795">3,200</span><span class="sxs-lookup"><span data-stu-id="c5f52-795">3,200</span></span> |<span data-ttu-id="c5f52-796">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-796">High</span></span> |
| <span data-ttu-id="c5f52-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="c5f52-797">SloDWGroupC06</span></span> |<span data-ttu-id="c5f52-798">64</span><span class="sxs-lookup"><span data-stu-id="c5f52-798">64</span></span> |<span data-ttu-id="c5f52-799">6,400</span><span class="sxs-lookup"><span data-stu-id="c5f52-799">6,400</span></span> |<span data-ttu-id="c5f52-800">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-800">High</span></span> |
| <span data-ttu-id="c5f52-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="c5f52-801">SloDWGroupC07</span></span> |<span data-ttu-id="c5f52-802">128</span><span class="sxs-lookup"><span data-stu-id="c5f52-802">128</span></span> |<span data-ttu-id="c5f52-803">12,800</span><span class="sxs-lookup"><span data-stu-id="c5f52-803">12,800</span></span> |<span data-ttu-id="c5f52-804">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-804">High</span></span> |

<span data-ttu-id="c5f52-805">從 **並行存取插槽的配置和耗用量** 圖表中，您可以看到 DW500 針對 smallrc、mediumrc、largerc 和 xlargerc，分別使用了 1、4、8 或 16 個並行存取插槽。</span><span class="sxs-lookup"><span data-stu-id="c5f52-805">From the **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="c5f52-806">您可以在上述圖表中查看這些值，以了解每個資源類別的重要性。</span><span class="sxs-lookup"><span data-stu-id="c5f52-806">You can look those values up in the preceding chart to find the importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-to-importance"></a><span data-ttu-id="c5f52-807">重要性與資源類別的 DW500 對應</span><span class="sxs-lookup"><span data-stu-id="c5f52-807">DW500 mapping of resource classes to importance</span></span>
| <span data-ttu-id="c5f52-808">資源類別</span><span class="sxs-lookup"><span data-stu-id="c5f52-808">Resource class</span></span> | <span data-ttu-id="c5f52-809">工作負載群組</span><span class="sxs-lookup"><span data-stu-id="c5f52-809">Workload group</span></span> | <span data-ttu-id="c5f52-810">已使用的並行存取插槽</span><span class="sxs-lookup"><span data-stu-id="c5f52-810">Concurrency slots used</span></span> | <span data-ttu-id="c5f52-811">MB / 散發套件</span><span class="sxs-lookup"><span data-stu-id="c5f52-811">MB / Distribution</span></span> | <span data-ttu-id="c5f52-812">重要性</span><span class="sxs-lookup"><span data-stu-id="c5f52-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="c5f52-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-813">smallrc</span></span> |<span data-ttu-id="c5f52-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="c5f52-814">SloDWGroupC00</span></span> |<span data-ttu-id="c5f52-815">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-815">1</span></span> |<span data-ttu-id="c5f52-816">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-816">100</span></span> |<span data-ttu-id="c5f52-817">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-817">Medium</span></span> |
| <span data-ttu-id="c5f52-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="c5f52-818">mediumrc</span></span> |<span data-ttu-id="c5f52-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="c5f52-819">SloDWGroupC02</span></span> |<span data-ttu-id="c5f52-820">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-820">4</span></span> |<span data-ttu-id="c5f52-821">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-821">400</span></span> |<span data-ttu-id="c5f52-822">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-822">Medium</span></span> |
| <span data-ttu-id="c5f52-823">largerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-823">largerc</span></span> |<span data-ttu-id="c5f52-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-824">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-825">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-825">8</span></span> |<span data-ttu-id="c5f52-826">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-826">800</span></span> |<span data-ttu-id="c5f52-827">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-827">Medium</span></span> |
| <span data-ttu-id="c5f52-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="c5f52-828">xlargerc</span></span> |<span data-ttu-id="c5f52-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="c5f52-829">SloDWGroupC04</span></span> |<span data-ttu-id="c5f52-830">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-830">16</span></span> |<span data-ttu-id="c5f52-831">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-831">1,600</span></span> |<span data-ttu-id="c5f52-832">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-832">High</span></span> |
| <span data-ttu-id="c5f52-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="c5f52-833">staticrc10</span></span> |<span data-ttu-id="c5f52-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="c5f52-834">SloDWGroupC00</span></span> |<span data-ttu-id="c5f52-835">1</span><span class="sxs-lookup"><span data-stu-id="c5f52-835">1</span></span> |<span data-ttu-id="c5f52-836">100</span><span class="sxs-lookup"><span data-stu-id="c5f52-836">100</span></span> |<span data-ttu-id="c5f52-837">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-837">Medium</span></span> |
| <span data-ttu-id="c5f52-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="c5f52-838">staticrc20</span></span> |<span data-ttu-id="c5f52-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="c5f52-839">SloDWGroupC01</span></span> |<span data-ttu-id="c5f52-840">2</span><span class="sxs-lookup"><span data-stu-id="c5f52-840">2</span></span> |<span data-ttu-id="c5f52-841">200</span><span class="sxs-lookup"><span data-stu-id="c5f52-841">200</span></span> |<span data-ttu-id="c5f52-842">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-842">Medium</span></span> |
| <span data-ttu-id="c5f52-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="c5f52-843">staticrc30</span></span> |<span data-ttu-id="c5f52-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="c5f52-844">SloDWGroupC02</span></span> |<span data-ttu-id="c5f52-845">4</span><span class="sxs-lookup"><span data-stu-id="c5f52-845">4</span></span> |<span data-ttu-id="c5f52-846">400</span><span class="sxs-lookup"><span data-stu-id="c5f52-846">400</span></span> |<span data-ttu-id="c5f52-847">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-847">Medium</span></span> |
| <span data-ttu-id="c5f52-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="c5f52-848">staticrc40</span></span> |<span data-ttu-id="c5f52-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-849">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-850">8</span><span class="sxs-lookup"><span data-stu-id="c5f52-850">8</span></span> |<span data-ttu-id="c5f52-851">800</span><span class="sxs-lookup"><span data-stu-id="c5f52-851">800</span></span> |<span data-ttu-id="c5f52-852">中型</span><span class="sxs-lookup"><span data-stu-id="c5f52-852">Medium</span></span> |
| <span data-ttu-id="c5f52-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="c5f52-853">staticrc50</span></span> |<span data-ttu-id="c5f52-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-854">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-855">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-855">16</span></span> |<span data-ttu-id="c5f52-856">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-856">1,600</span></span> |<span data-ttu-id="c5f52-857">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-857">High</span></span> |
| <span data-ttu-id="c5f52-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="c5f52-858">staticrc60</span></span> |<span data-ttu-id="c5f52-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-859">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-860">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-860">16</span></span> |<span data-ttu-id="c5f52-861">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-861">1,600</span></span> |<span data-ttu-id="c5f52-862">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-862">High</span></span> |
| <span data-ttu-id="c5f52-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="c5f52-863">staticrc70</span></span> |<span data-ttu-id="c5f52-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-864">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-865">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-865">16</span></span> |<span data-ttu-id="c5f52-866">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-866">1,600</span></span> |<span data-ttu-id="c5f52-867">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-867">High</span></span> |
| <span data-ttu-id="c5f52-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="c5f52-868">staticrc80</span></span> |<span data-ttu-id="c5f52-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="c5f52-869">SloDWGroupC03</span></span> |<span data-ttu-id="c5f52-870">16</span><span class="sxs-lookup"><span data-stu-id="c5f52-870">16</span></span> |<span data-ttu-id="c5f52-871">1,600</span><span class="sxs-lookup"><span data-stu-id="c5f52-871">1,600</span></span> |<span data-ttu-id="c5f52-872">高</span><span class="sxs-lookup"><span data-stu-id="c5f52-872">High</span></span> |

<span data-ttu-id="c5f52-873">您可以使用下列 DMV 查詢，從資源管理員的觀點詳細查看記憶體資源配置的差異，或在進行疑難排解時，分析工作負載群組的作用中和歷史使用量。</span><span class="sxs-lookup"><span data-stu-id="c5f52-873">You can use the following DMV query to look at the differences in memory resource allocation in detail from the perspective of the resource governor, or to analyze active and historic usage of the workload groups when troubleshooting.</span></span>

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

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="c5f52-874">採用並行存取限制的查詢</span><span class="sxs-lookup"><span data-stu-id="c5f52-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="c5f52-875">大多數查詢都受到資源類別控管。</span><span class="sxs-lookup"><span data-stu-id="c5f52-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="c5f52-876">這些查詢必須同時符合並行查詢和並行存取插槽臨界值。</span><span class="sxs-lookup"><span data-stu-id="c5f52-876">These queries must fit inside both the concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="c5f52-877">使用者無法選擇從並行存取插槽模型中排除查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-877">A user cannot choose to exclude a query from the concurrency slot model.</span></span>

<span data-ttu-id="c5f52-878">再次提醒您，下列陳述式會採用資源類別：</span><span class="sxs-lookup"><span data-stu-id="c5f52-878">To reiterate, the following statements honor resource classes:</span></span>

* <span data-ttu-id="c5f52-879">INSERT-SELECT</span><span class="sxs-lookup"><span data-stu-id="c5f52-879">INSERT-SELECT</span></span>
* <span data-ttu-id="c5f52-880">UPDATE</span><span class="sxs-lookup"><span data-stu-id="c5f52-880">UPDATE</span></span>
* <span data-ttu-id="c5f52-881">刪除</span><span class="sxs-lookup"><span data-stu-id="c5f52-881">DELETE</span></span>
* <span data-ttu-id="c5f52-882">SELECT (當查詢使用者資料表時)</span><span class="sxs-lookup"><span data-stu-id="c5f52-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="c5f52-883">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="c5f52-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="c5f52-884">ALTER INDEX REORGANIZE</span><span class="sxs-lookup"><span data-stu-id="c5f52-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="c5f52-885">ALTER TABLE REBUILD</span><span class="sxs-lookup"><span data-stu-id="c5f52-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="c5f52-886">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="c5f52-886">CREATE INDEX</span></span>
* <span data-ttu-id="c5f52-887">CREATE CLUSTERED COLUMNSTORE INDEX</span><span class="sxs-lookup"><span data-stu-id="c5f52-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="c5f52-888">CREATE TABLE AS SELECT (CTAS)</span><span class="sxs-lookup"><span data-stu-id="c5f52-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="c5f52-889">載入資料</span><span class="sxs-lookup"><span data-stu-id="c5f52-889">Data loading</span></span>
* <span data-ttu-id="c5f52-890">資料移動服務 (DMS) 進行的資料移動作業</span><span class="sxs-lookup"><span data-stu-id="c5f52-890">Data movement operations conducted by the Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-to-concurrency-limits"></a><span data-ttu-id="c5f52-891">並行存取限制查詢例外狀況</span><span class="sxs-lookup"><span data-stu-id="c5f52-891">Query exceptions to concurrency limits</span></span>
<span data-ttu-id="c5f52-892">部分查詢不支援使用者受指派的資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-892">Some queries do not honor the resource class to which the user is assigned.</span></span> <span data-ttu-id="c5f52-893">這些並行存取限制例外狀況是在某特定命令所需的記憶體資源過低時才會發生，通常是因為該命令為中繼資料作業。</span><span class="sxs-lookup"><span data-stu-id="c5f52-893">These exceptions to the concurrency limits are made when the memory resources needed for a particular command are low, often because the command is a metadata operation.</span></span> <span data-ttu-id="c5f52-894">這些例外狀況的目標是，避免將較大的記憶體配置給永遠不需要那麼多記憶體的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-894">The goal of these exceptions is to avoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="c5f52-895">在這些情況下，一律會使用預設小型資源類別 (smallrc)，而不考慮指派給使用者的實際資源類別。</span><span class="sxs-lookup"><span data-stu-id="c5f52-895">In these cases, the default small resource class (smallrc) is always used regardless of the actual resource class assigned to the user.</span></span> <span data-ttu-id="c5f52-896">例如， `CREATE LOGIN` 一律會在 smallrc 中執行。</span><span class="sxs-lookup"><span data-stu-id="c5f52-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="c5f52-897">完成此作業所需的資源非常少，因此沒必要將查詢納入並行存取插槽模型中。</span><span class="sxs-lookup"><span data-stu-id="c5f52-897">The resources required to fulfill this operation are very low, so it does not make sense to include the query in the concurrency slot model.</span></span>  <span data-ttu-id="c5f52-898">這些查詢也不會受到 32 個使用者並行存取限制，不限數目的這些查詢可以執行的工作階段上限為 1,024 個工作階段。</span><span class="sxs-lookup"><span data-stu-id="c5f52-898">These queries are also not limited by the 32 user concurrency limit, an unlimited number of these queries can run up to the session limit of 1,024 sessions.</span></span>

<span data-ttu-id="c5f52-899">下列陳述式未採用資源類別：</span><span class="sxs-lookup"><span data-stu-id="c5f52-899">The following statements do not honor resource classes:</span></span>

* <span data-ttu-id="c5f52-900">CREATE 或 DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="c5f52-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="c5f52-901">ALTER TABLE ...SWITCH、SPLIT 或 MERGE PARTITION</span><span class="sxs-lookup"><span data-stu-id="c5f52-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="c5f52-902">ALTER INDEX DISABLE</span><span class="sxs-lookup"><span data-stu-id="c5f52-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="c5f52-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="c5f52-903">DROP INDEX</span></span>
* <span data-ttu-id="c5f52-904">CREATE、UPDATE 或 DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="c5f52-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="c5f52-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="c5f52-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="c5f52-906">ALTER AUTHORIZATION</span><span class="sxs-lookup"><span data-stu-id="c5f52-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="c5f52-907">CREATE LOGIN</span><span class="sxs-lookup"><span data-stu-id="c5f52-907">CREATE LOGIN</span></span>
* <span data-ttu-id="c5f52-908">CREATE、ALTER 或 DROP USER</span><span class="sxs-lookup"><span data-stu-id="c5f52-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="c5f52-909">CREATE、ALTER 或 DROP PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="c5f52-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="c5f52-910">CREATE 或 DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="c5f52-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="c5f52-911">INSERT VALUES</span><span class="sxs-lookup"><span data-stu-id="c5f52-911">INSERT VALUES</span></span>
* <span data-ttu-id="c5f52-912">從系統檢視和 DMV 來 SELECT</span><span class="sxs-lookup"><span data-stu-id="c5f52-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="c5f52-913">EXPLAIN</span><span class="sxs-lookup"><span data-stu-id="c5f52-913">EXPLAIN</span></span>
* <span data-ttu-id="c5f52-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="c5f52-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="c5f52-915"><a name="changing-user-resource-class-example"></a> 變更使用者資源類別的範例</span><span class="sxs-lookup"><span data-stu-id="c5f52-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="c5f52-916">**建立登入：**開啟 SQL Server 上裝載 SQL 資料倉儲資料庫的**主要**資料庫的連接，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="c5f52-916">**Create login:** Open a connection to your **master** database on the SQL server hosting your SQL Data Warehouse database and execute the following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c5f52-917">在主要資料庫中建立一個使用者做為 Azure SQL 資料倉儲使用者是不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="c5f52-917">It is a good idea to create a user in the master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="c5f52-918">在主要資料庫中建立使用者，使用者就能使用類似 SSMS 的工具登入而不用指定資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c5f52-918">Creating a user in master allows a user to login using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="c5f52-919">它也可讓使用者使用物件總管來檢視 SQL Server 上的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="c5f52-919">It also allows them to use the object explorer to view all databases on a SQL server.</span></span>  <span data-ttu-id="c5f52-920">如需有關建立和管理使用者的詳細資料，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="c5f52-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="c5f52-921">**建立 SQL 資料倉儲使用者︰**開啟 **SQL 資料倉儲**資料庫的連接，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="c5f52-921">**Create SQL Data Warehouse user:** Open a connection to the **SQL Data Warehouse** database and execute the following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="c5f52-922">**授與權限︰**下列範例會授與 **SQL 資料倉儲** 資料庫上的 `CONTROL`。</span><span class="sxs-lookup"><span data-stu-id="c5f52-922">**Grant permissions:** The following example grants `CONTROL` on the **SQL Data Warehouse** database.</span></span> <span data-ttu-id="c5f52-923">資料庫層級的 `CONTROL`相當於 SQL Server 中的 db_owner。</span><span class="sxs-lookup"><span data-stu-id="c5f52-923">`CONTROL` at the database level is the equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW to newperson;
    ```
4. <span data-ttu-id="c5f52-924">**增加資源類別︰** 使用下列查詢，將使用者加入至更高的工作負載管理角色。</span><span class="sxs-lookup"><span data-stu-id="c5f52-924">**Increase resource class:** Use the following query to add a user to a higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="c5f52-925">**減少資源類別︰** 使用下列查詢，從工作負載管理角色移除使用者。</span><span class="sxs-lookup"><span data-stu-id="c5f52-925">**Decrease resource class:** Use the following query to remove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c5f52-926">您無法從 smallrc 移除使用者。</span><span class="sxs-lookup"><span data-stu-id="c5f52-926">It is not possible to remove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="c5f52-927">已排入佇列的查詢偵測和其他 DMV</span><span class="sxs-lookup"><span data-stu-id="c5f52-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="c5f52-928">您可以使用 `sys.dm_pdw_exec_requests` DMV，來識別正在並行存取佇列中等候的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-928">You can use the `sys.dm_pdw_exec_requests` DMV to identify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="c5f52-929">正在等待並行存取插槽的查詢狀態為 **暫停**。</span><span class="sxs-lookup"><span data-stu-id="c5f52-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="c5f52-930">工作負載管理角色可以使用 `sys.database_principals`來檢視。</span><span class="sxs-lookup"><span data-stu-id="c5f52-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="c5f52-931">下列查詢會顯示每位使用者指派給哪些角色。</span><span class="sxs-lookup"><span data-stu-id="c5f52-931">The following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="c5f52-932">SQL 資料倉儲具有下列等候類型：</span><span class="sxs-lookup"><span data-stu-id="c5f52-932">SQL Data Warehouse has the following wait types:</span></span>

* <span data-ttu-id="c5f52-933">**LocalQueriesConcurrencyResourceType**：位於並行存取插槽架構外部的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of the concurrency slot framework.</span></span> <span data-ttu-id="c5f52-934">DMV 查詢及 `SELECT @@VERSION` 這類的系統函數是本機查詢的範例。</span><span class="sxs-lookup"><span data-stu-id="c5f52-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="c5f52-935">**UserConcurrencyResourceType**：位於並行存取插槽架構內部的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f52-935">**UserConcurrencyResourceType**: Queries that sit inside the concurrency slot framework.</span></span> <span data-ttu-id="c5f52-936">針對使用者資料表的查詢代表會使用此資源類型的範例。</span><span class="sxs-lookup"><span data-stu-id="c5f52-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="c5f52-937">**DmsConcurrencyResourceType**：資料移動作業所產生的等候。</span><span class="sxs-lookup"><span data-stu-id="c5f52-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="c5f52-938">**BackupConcurrencyResourceType**：此等候指出正在備份資料庫。</span><span class="sxs-lookup"><span data-stu-id="c5f52-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="c5f52-939">此資源類型的最大值為 1。</span><span class="sxs-lookup"><span data-stu-id="c5f52-939">The maximum value for this resource type is 1.</span></span> <span data-ttu-id="c5f52-940">如果在同一時間要求多個備份，其他備份將會排入佇列。</span><span class="sxs-lookup"><span data-stu-id="c5f52-940">If multiple backups have been requested at the same time, the others will queue.</span></span>

<span data-ttu-id="c5f52-941">`sys.dm_pdw_waits` DMV 可用來查看要求正在等待哪些資源。</span><span class="sxs-lookup"><span data-stu-id="c5f52-941">The `sys.dm_pdw_waits` DMV can be used to see which resources a request is waiting for.</span></span>

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

<span data-ttu-id="c5f52-942">`sys.dm_pdw_resource_waits` DMV 只會顯示等待指定查詢取用的資源。</span><span class="sxs-lookup"><span data-stu-id="c5f52-942">The `sys.dm_pdw_resource_waits` DMV shows only the resource waits consumed by a given query.</span></span> <span data-ttu-id="c5f52-943">資源等候時間只會測量等候提供資源的時間，與訊號等候時間相反，後者是基礎 SQL Server 將查詢排程到 CPU 所需的時間。</span><span class="sxs-lookup"><span data-stu-id="c5f52-943">Resource wait time only measures the time waiting for resources to be provided, as opposed to signal wait time, which is the time it takes for the underlying SQL servers to schedule the query onto the CPU.</span></span>

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

<span data-ttu-id="c5f52-944">`sys.dm_pdw_wait_stats` DMV 可用於針對等候項目進行歷史趨勢分析。</span><span class="sxs-lookup"><span data-stu-id="c5f52-944">The `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c5f52-945">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5f52-945">Next steps</span></span>
<span data-ttu-id="c5f52-946">如需管理資料庫使用者和安全性的詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="c5f52-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="c5f52-947">如需較大資源類別如何改善叢集資料行存放區索引品質的詳細資訊，請參閱 [重建索引以提升區段品質]。</span><span class="sxs-lookup"><span data-stu-id="c5f52-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes to improve segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[重建索引以提升區段品質]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
