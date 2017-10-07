---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 （概觀） |Microsoft 文件"
description: "Azure SQL 資料倉儲中的效能相應放大功能。 向外延展藉由調整 Dwu 或暫停和繼續計算資源 toosave 成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="71a47-104">管理 Azure SQL 資料倉儲中的計算能力 (概觀)</span><span class="sxs-lookup"><span data-stu-id="71a47-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71a47-105">概觀</span><span class="sxs-lookup"><span data-stu-id="71a47-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="71a47-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="71a47-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="71a47-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71a47-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="71a47-108">REST</span><span class="sxs-lookup"><span data-stu-id="71a47-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="71a47-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="71a47-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="71a47-110">儲存體和計算，分別讓每個 tooscale，區隔 hello 架構的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="71a47-110">hello architecture of SQL Data Warehouse separates storage and compute, allowing each tooscale independently.</span></span> <span data-ttu-id="71a47-111">如此一來，計算可以是獨立的資料量 hello 縮放的 toomeet 效能需求。</span><span class="sxs-lookup"><span data-stu-id="71a47-111">As a result, compute can be scaled toomeet performance demands independent of hello amount of data.</span></span> <span data-ttu-id="71a47-112">這個架構的自然結果為計算[計費][billed]和儲存體無關。</span><span class="sxs-lookup"><span data-stu-id="71a47-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="71a47-113">本概觀說明如何擴充適用於 SQL 資料倉儲，且 tooutilize hello 暫停、 繼續和 SQL 資料倉儲的延展功能的方式。</span><span class="sxs-lookup"><span data-stu-id="71a47-113">This overview describes how scale out works with SQL Data Warehouse and how tooutilize hello pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="71a47-114">請參閱 hello[資料倉儲單位 (Dwu)] [ data warehouse units (DWUs)]頁面 toolearn 相關性 Dwu 和效能。</span><span class="sxs-lookup"><span data-stu-id="71a47-114">Consult hello [data warehouse units (DWUs)][data warehouse units (DWUs)] page toolearn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="71a47-115">計算管理作業如何在 SQL 資料倉儲中運作</span><span class="sxs-lookup"><span data-stu-id="71a47-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="71a47-116">SQL 資料倉儲的 hello 架構是由控制節點所組成，計算節點及分散到 60 分佈 hello 儲存層。</span><span class="sxs-lookup"><span data-stu-id="71a47-116">hello architecture for SQL Data Warehouse consists of a control node, compute nodes, and hello storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="71a47-117">在正常作用中工作階段期間在 SQL 資料倉儲中，系統的前端節點會管理 hello 中繼資料，並包含 hello 分散式查詢最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="71a47-117">During a normal active session in SQL Data Warehouse, your system's head node manages hello metadata and contains hello distributed query optimizer.</span></span> <span data-ttu-id="71a47-118">此前端節點以下為計算節點和儲存層。</span><span class="sxs-lookup"><span data-stu-id="71a47-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="71a47-119">DWU 400，系統會有一個前端節點、 四個計算節點，與 hello 儲存層，60 分佈所組成。</span><span class="sxs-lookup"><span data-stu-id="71a47-119">For a DWU 400, your system has one head node, four compute nodes, and hello storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="71a47-120">當您使用小數位數或暫停作業時，hello 系統首先會清除所有傳入的查詢，然後回復交易 tooensure 一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="71a47-120">When you undergo a scale or pause operation, hello system first kills all incoming queries and then rolls back transactions tooensure a consistent state.</span></span> <span data-ttu-id="71a47-121">針對調整作業，僅在這個交易回復完成後調整才會發生。</span><span class="sxs-lookup"><span data-stu-id="71a47-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="71a47-122">向上延展作業，請 hello 系統佈建 hello 額外需要的運算節點數，然後重新附加 hello 計算節點 toohello 儲存層。</span><span class="sxs-lookup"><span data-stu-id="71a47-122">For a scale-up operation, hello system provisions hello extra desired number of compute nodes, and then begins reattaching hello compute nodes toohello storage layer.</span></span> <span data-ttu-id="71a47-123">向下調整作業，請 hello 不需要的節點會釋放，hello 其餘運算節點重新附加本身 toohello 適當數量的分佈。</span><span class="sxs-lookup"><span data-stu-id="71a47-123">For a scale-down operation, hello unneeded nodes are released and hello remaining compute nodes reattach themselves toohello appropriate number of distributions.</span></span> <span data-ttu-id="71a47-124">暫停作業中，所有計算節點並釋出與您的系統將會進行各種不同的中繼資料作業 tooleave 最終穩定的狀態系統。</span><span class="sxs-lookup"><span data-stu-id="71a47-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations tooleave your final system in a stable state.</span></span>

| <span data-ttu-id="71a47-125">DWU</span><span class="sxs-lookup"><span data-stu-id="71a47-125">DWU</span></span>  | <span data-ttu-id="71a47-126">\# 個計算節點</span><span class="sxs-lookup"><span data-stu-id="71a47-126">\#of compute nodes</span></span> | <span data-ttu-id="71a47-127">每節點 \# 個散發</span><span class="sxs-lookup"><span data-stu-id="71a47-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="71a47-128">100</span><span class="sxs-lookup"><span data-stu-id="71a47-128">100</span></span>  | <span data-ttu-id="71a47-129">1</span><span class="sxs-lookup"><span data-stu-id="71a47-129">1</span></span>                  | <span data-ttu-id="71a47-130">60</span><span class="sxs-lookup"><span data-stu-id="71a47-130">60</span></span>                           |
| <span data-ttu-id="71a47-131">200</span><span class="sxs-lookup"><span data-stu-id="71a47-131">200</span></span>  | <span data-ttu-id="71a47-132">2</span><span class="sxs-lookup"><span data-stu-id="71a47-132">2</span></span>                  | <span data-ttu-id="71a47-133">30</span><span class="sxs-lookup"><span data-stu-id="71a47-133">30</span></span>                           |
| <span data-ttu-id="71a47-134">300</span><span class="sxs-lookup"><span data-stu-id="71a47-134">300</span></span>  | <span data-ttu-id="71a47-135">3</span><span class="sxs-lookup"><span data-stu-id="71a47-135">3</span></span>                  | <span data-ttu-id="71a47-136">20</span><span class="sxs-lookup"><span data-stu-id="71a47-136">20</span></span>                           |
| <span data-ttu-id="71a47-137">400</span><span class="sxs-lookup"><span data-stu-id="71a47-137">400</span></span>  | <span data-ttu-id="71a47-138">4</span><span class="sxs-lookup"><span data-stu-id="71a47-138">4</span></span>                  | <span data-ttu-id="71a47-139">15</span><span class="sxs-lookup"><span data-stu-id="71a47-139">15</span></span>                           |
| <span data-ttu-id="71a47-140">500</span><span class="sxs-lookup"><span data-stu-id="71a47-140">500</span></span>  | <span data-ttu-id="71a47-141">5</span><span class="sxs-lookup"><span data-stu-id="71a47-141">5</span></span>                  | <span data-ttu-id="71a47-142">12</span><span class="sxs-lookup"><span data-stu-id="71a47-142">12</span></span>                           |
| <span data-ttu-id="71a47-143">600</span><span class="sxs-lookup"><span data-stu-id="71a47-143">600</span></span>  | <span data-ttu-id="71a47-144">6</span><span class="sxs-lookup"><span data-stu-id="71a47-144">6</span></span>                  | <span data-ttu-id="71a47-145">10</span><span class="sxs-lookup"><span data-stu-id="71a47-145">10</span></span>                           |
| <span data-ttu-id="71a47-146">1000</span><span class="sxs-lookup"><span data-stu-id="71a47-146">1000</span></span> | <span data-ttu-id="71a47-147">10</span><span class="sxs-lookup"><span data-stu-id="71a47-147">10</span></span>                 | <span data-ttu-id="71a47-148">6</span><span class="sxs-lookup"><span data-stu-id="71a47-148">6</span></span>                            |
| <span data-ttu-id="71a47-149">1200</span><span class="sxs-lookup"><span data-stu-id="71a47-149">1200</span></span> | <span data-ttu-id="71a47-150">12</span><span class="sxs-lookup"><span data-stu-id="71a47-150">12</span></span>                 | <span data-ttu-id="71a47-151">5</span><span class="sxs-lookup"><span data-stu-id="71a47-151">5</span></span>                            |
| <span data-ttu-id="71a47-152">1500</span><span class="sxs-lookup"><span data-stu-id="71a47-152">1500</span></span> | <span data-ttu-id="71a47-153">15</span><span class="sxs-lookup"><span data-stu-id="71a47-153">15</span></span>                 | <span data-ttu-id="71a47-154">4</span><span class="sxs-lookup"><span data-stu-id="71a47-154">4</span></span>                            |
| <span data-ttu-id="71a47-155">2000</span><span class="sxs-lookup"><span data-stu-id="71a47-155">2000</span></span> | <span data-ttu-id="71a47-156">20</span><span class="sxs-lookup"><span data-stu-id="71a47-156">20</span></span>                 | <span data-ttu-id="71a47-157">3</span><span class="sxs-lookup"><span data-stu-id="71a47-157">3</span></span>                            |
| <span data-ttu-id="71a47-158">3000</span><span class="sxs-lookup"><span data-stu-id="71a47-158">3000</span></span> | <span data-ttu-id="71a47-159">30</span><span class="sxs-lookup"><span data-stu-id="71a47-159">30</span></span>                 | <span data-ttu-id="71a47-160">2</span><span class="sxs-lookup"><span data-stu-id="71a47-160">2</span></span>                            |
| <span data-ttu-id="71a47-161">6000</span><span class="sxs-lookup"><span data-stu-id="71a47-161">6000</span></span> | <span data-ttu-id="71a47-162">60</span><span class="sxs-lookup"><span data-stu-id="71a47-162">60</span></span>                 | <span data-ttu-id="71a47-163">1</span><span class="sxs-lookup"><span data-stu-id="71a47-163">1</span></span>                            |

<span data-ttu-id="71a47-164">hello 三個主要的功能來管理計算為：</span><span class="sxs-lookup"><span data-stu-id="71a47-164">hello three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="71a47-165">暫停</span><span class="sxs-lookup"><span data-stu-id="71a47-165">Pause</span></span>
2. <span data-ttu-id="71a47-166">繼續</span><span class="sxs-lookup"><span data-stu-id="71a47-166">Resume</span></span>
3. <span data-ttu-id="71a47-167">調整</span><span class="sxs-lookup"><span data-stu-id="71a47-167">Scale</span></span>

<span data-ttu-id="71a47-168">每項作業可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="71a47-168">Each of these operations may take several minutes toocomplete.</span></span> <span data-ttu-id="71a47-169">如果您是調整/暫停/繼續自動，您可能想 tooimplement 邏輯 tooensure 某些作業完成之前繼續執行其他動作。</span><span class="sxs-lookup"><span data-stu-id="71a47-169">If you are scaling/pausing/resuming automatically, you may want tooimplement logic tooensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="71a47-170">核取 hello 資料庫狀態，透過不同的端點，可讓這類作業的 toocorrectly 實作自動化。</span><span class="sxs-lookup"><span data-stu-id="71a47-170">Checking hello database state through various endpoints will allow you toocorrectly implement automation of such operations.</span></span> <span data-ttu-id="71a47-171">hello 入口網站會提供完成的作業與 hello 資料庫目前狀態的通知，但不允許以程式設計方式檢查有無狀態。</span><span class="sxs-lookup"><span data-stu-id="71a47-171">hello portal will provide notification upon completion of an operation and hello databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="71a47-172">計算管理功能並未跨所有端點存在。</span><span class="sxs-lookup"><span data-stu-id="71a47-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="71a47-173">暫停/繼續</span><span class="sxs-lookup"><span data-stu-id="71a47-173">Pause/Resume</span></span> | <span data-ttu-id="71a47-174">調整</span><span class="sxs-lookup"><span data-stu-id="71a47-174">Scale</span></span> | <span data-ttu-id="71a47-175">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="71a47-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="71a47-176">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="71a47-176">Azure portal</span></span> | <span data-ttu-id="71a47-177">是</span><span class="sxs-lookup"><span data-stu-id="71a47-177">Yes</span></span>          | <span data-ttu-id="71a47-178">是</span><span class="sxs-lookup"><span data-stu-id="71a47-178">Yes</span></span>   | <span data-ttu-id="71a47-179">**否**</span><span class="sxs-lookup"><span data-stu-id="71a47-179">**No**</span></span>               |
| <span data-ttu-id="71a47-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71a47-180">PowerShell</span></span>   | <span data-ttu-id="71a47-181">是</span><span class="sxs-lookup"><span data-stu-id="71a47-181">Yes</span></span>          | <span data-ttu-id="71a47-182">是</span><span class="sxs-lookup"><span data-stu-id="71a47-182">Yes</span></span>   | <span data-ttu-id="71a47-183">是</span><span class="sxs-lookup"><span data-stu-id="71a47-183">Yes</span></span>                  |
| <span data-ttu-id="71a47-184">REST API</span><span class="sxs-lookup"><span data-stu-id="71a47-184">REST API</span></span>     | <span data-ttu-id="71a47-185">是</span><span class="sxs-lookup"><span data-stu-id="71a47-185">Yes</span></span>          | <span data-ttu-id="71a47-186">是</span><span class="sxs-lookup"><span data-stu-id="71a47-186">Yes</span></span>   | <span data-ttu-id="71a47-187">是</span><span class="sxs-lookup"><span data-stu-id="71a47-187">Yes</span></span>                  |
| <span data-ttu-id="71a47-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="71a47-188">T-SQL</span></span>        | <span data-ttu-id="71a47-189">**否**</span><span class="sxs-lookup"><span data-stu-id="71a47-189">**No**</span></span>       | <span data-ttu-id="71a47-190">是</span><span class="sxs-lookup"><span data-stu-id="71a47-190">Yes</span></span>   | <span data-ttu-id="71a47-191">是</span><span class="sxs-lookup"><span data-stu-id="71a47-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="71a47-192">調整計算</span><span class="sxs-lookup"><span data-stu-id="71a47-192">Scale compute</span></span>

<span data-ttu-id="71a47-193">SQL 資料倉儲中的效能測量單位為[資料倉儲單位 (DWU)][data warehouse units (DWUs)]，這是計算資源的抽象量值，例如 CPU、記憶體和 I/O 頻寬。</span><span class="sxs-lookup"><span data-stu-id="71a47-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="71a47-194">希望 tooscale 他們的系統效能的使用者可以在透過各種方式，例如透過 hello 入口網站，T-SQL、 REST Api。</span><span class="sxs-lookup"><span data-stu-id="71a47-194">A user who wishes tooscale their system's performance can do so through various means, such as through hello portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="71a47-195">如何調整計算？</span><span class="sxs-lookup"><span data-stu-id="71a47-195">How do I scale compute?</span></span>
<span data-ttu-id="71a47-196">運算能力您管理的 SQL 資料倉儲藉由變更 hello 的 DWU 設定。</span><span class="sxs-lookup"><span data-stu-id="71a47-196">Compute power is managed for you SQL Data Warehouse by changing hello DWU setting.</span></span> <span data-ttu-id="71a47-197">隨著您針對特定作業新增更多的 DWU，效能會[以線性方式][linearly]提升。</span><span class="sxs-lookup"><span data-stu-id="71a47-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="71a47-198">當您將系統相應增加或減少時，我們提供的 DWU 供應項目可確保您的效能會明顯變更。</span><span class="sxs-lookup"><span data-stu-id="71a47-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="71a47-199">tooadjust Dwu，您可以使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="71a47-199">tooadjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="71a47-200">[使用 Azure 入口網站調整計算能力][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="71a47-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="71a47-201">[使用 PowerShell 調整計算能力][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="71a47-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="71a47-202">[使用 REST API 調整計算能力][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="71a47-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="71a47-203">[使用 TSQL 調整計算能力][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="71a47-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="71a47-204">應該使用多少 DWU 呢？</span><span class="sxs-lookup"><span data-stu-id="71a47-204">How many DWUs should I use?</span></span>

<span data-ttu-id="71a47-205">toounderstand 您理想 DWU 值為何，請嘗試向上和向下調整並執行幾個查詢載入資料之後。</span><span class="sxs-lookup"><span data-stu-id="71a47-205">toounderstand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="71a47-206">由於調整很快速，您可以在一小時內嘗各種效能層級。</span><span class="sxs-lookup"><span data-stu-id="71a47-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="71a47-207">SQL 資料倉儲是設計的 tooprocess 大量的資料。</span><span class="sxs-lookup"><span data-stu-id="71a47-207">SQL Data Warehouse is designed tooprocess large amounts of data.</span></span> <span data-ttu-id="71a47-208">toosee 想 toouse 大型資料集接近或超過 1 TB 的縮放比例，尤其是在較大的 dwu 調整其 true 功能。</span><span class="sxs-lookup"><span data-stu-id="71a47-208">toosee its true capabilities for scaling, especially at larger DWUs, you want toouse a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="71a47-209">尋找建議 hello 最佳的 DWU，您的工作負載：</span><span class="sxs-lookup"><span data-stu-id="71a47-209">Recommendations for finding hello best DWU for your workload:</span></span>

1. <span data-ttu-id="71a47-210">若是開發過程中的資料倉儲，可選取較少的 DWU 效能等級。</span><span class="sxs-lookup"><span data-stu-id="71a47-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="71a47-211">DW400 或 DW200 是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="71a47-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="71a47-212">監視您的應用程式效能，觀察選取的 Dwu 的 hello 數目比較 toohello 您觀察到的效能。</span><span class="sxs-lookup"><span data-stu-id="71a47-212">Monitor your application performance, observing hello number of DWUs selected compared toohello performance you observe.</span></span>
3. <span data-ttu-id="71a47-213">判斷多少快或慢的效能應該是您 tooreach hello 最佳的效能層級為您的需求，假設線性標尺。</span><span class="sxs-lookup"><span data-stu-id="71a47-213">Determine how much faster or slower performance should be for you tooreach hello optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="71a47-214">增加或減少 hello 數目要 dwu 調整比例 toohow 更快或慢中的工作負載 tooperform。</span><span class="sxs-lookup"><span data-stu-id="71a47-214">Increase or decrease hello number of DWUs in proportion toohow much faster or slower you want your workload tooperform.</span></span> 
5. <span data-ttu-id="71a47-215">繼續進行調整，直到達到您業務需求的最佳效能為止。</span><span class="sxs-lookup"><span data-stu-id="71a47-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="71a47-216">如果 hello 工作可以分割為計算節點，則查詢效能就只會增加與多個平行化作業。</span><span class="sxs-lookup"><span data-stu-id="71a47-216">Query performance only increases with more parallelization if hello work can be split between compute nodes.</span></span> <span data-ttu-id="71a47-217">如果您發現縮放比例不會變更您的效能，請查看我們的效能微調文章 toocheck 是否平均地分散您的資料，或引進大量的資料移動。</span><span class="sxs-lookup"><span data-stu-id="71a47-217">If you find that scaling is not changing your performance, please check out our performance tuning articles toocheck whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="71a47-218">何時調整 DWU？</span><span class="sxs-lookup"><span data-stu-id="71a47-218">When should I scale DWUs?</span></span>
<span data-ttu-id="71a47-219">調整 Dwu 改變 hello 下列重要案例：</span><span class="sxs-lookup"><span data-stu-id="71a47-219">Scaling DWUs alters hello following important scenarios:</span></span>

1. <span data-ttu-id="71a47-220">以線性方式變更的掃描、 彙總和 CTAS 陳述式的 hello 系統的效能</span><span class="sxs-lookup"><span data-stu-id="71a47-220">Linearly changing performance of hello system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="71a47-221">Hello 日益增加的讀取器和寫入器時載入使用 PolyBase</span><span class="sxs-lookup"><span data-stu-id="71a47-221">Increasing hello number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="71a47-222">並行查詢和並行存取插槽數目上限</span><span class="sxs-lookup"><span data-stu-id="71a47-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="71a47-223">建議當 tooscale dwu 調整：</span><span class="sxs-lookup"><span data-stu-id="71a47-223">Recommendations for when tooscale DWUs:</span></span>

1. <span data-ttu-id="71a47-224">執行大量資料載入或轉換作業之前，相應增加 DWU 以使您的資料更快速可供使用。</span><span class="sxs-lookup"><span data-stu-id="71a47-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="71a47-225">尖峰營業時間，調整 tooaccommodate 大量的並行查詢。</span><span class="sxs-lookup"><span data-stu-id="71a47-225">During peak business hours, scale tooaccommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="71a47-226">暫停計算</span><span class="sxs-lookup"><span data-stu-id="71a47-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="71a47-227">toopause 資料庫，可使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="71a47-227">toopause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="71a47-228">[使用 Azure 入口網站暫停計算][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="71a47-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="71a47-229">[使用 PowerShell 暫停計算][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="71a47-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="71a47-230">[使用 REST API 暫停計算][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="71a47-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="71a47-231">繼續計算</span><span class="sxs-lookup"><span data-stu-id="71a47-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="71a47-232">tooresume 資料庫，可使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="71a47-232">tooresume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="71a47-233">[使用 Azure 入口網站繼續計算][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="71a47-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="71a47-234">[使用 PowerShell 繼續計算][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="71a47-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="71a47-235">[使用 REST API 繼續計算][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="71a47-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="71a47-236">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="71a47-236">Check database state</span></span> 

<span data-ttu-id="71a47-237">tooresume 資料庫，可使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="71a47-237">tooresume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="71a47-238">[使用 T-SQL 檢查資料庫狀態][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="71a47-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="71a47-239">[使用 PowerShell 檢查資料庫狀態][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="71a47-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="71a47-240">[使用 REST API 檢查資料庫狀態][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="71a47-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="71a47-241">權限</span><span class="sxs-lookup"><span data-stu-id="71a47-241">Permissions</span></span>

<span data-ttu-id="71a47-242">縮放比例的 hello 資料庫需要 hello 中所述的權限[ALTER DATABASE][ALTER DATABASE]。</span><span class="sxs-lookup"><span data-stu-id="71a47-242">Scaling hello database requires hello permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="71a47-243">暫停及繼續需要 hello [SQL DB 參與者][ SQL DB Contributor]權限，特別是 Microsoft.Sql/servers/databases/action。</span><span class="sxs-lookup"><span data-stu-id="71a47-243">Pause and Resume require hello [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="71a47-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71a47-244">Next steps</span></span>
<span data-ttu-id="71a47-245">請參閱下列文章 toohelp 您了解一些額外的關鍵效能概念 toohello:</span><span class="sxs-lookup"><span data-stu-id="71a47-245">Refer toohello following articles toohelp you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="71a47-246">[工作負載和並行管理][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="71a47-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="71a47-247">[資料表設計概觀][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="71a47-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="71a47-248">[資料表散發][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="71a47-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="71a47-249">[索引資料表的編製][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="71a47-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="71a47-250">[資料表分割][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="71a47-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="71a47-251">[資料表統計資料][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="71a47-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="71a47-252">[最佳作法][Best practices]</span><span class="sxs-lookup"><span data-stu-id="71a47-252">[Best practices][Best practices]</span></span>

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
