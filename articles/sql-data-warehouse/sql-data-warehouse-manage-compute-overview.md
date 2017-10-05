---
title: "管理 Azure SQL 資料倉儲中的計算能力 (概觀) | Microsoft Docs"
description: "Azure SQL 資料倉儲中的效能相應放大功能。 藉由調整 DWU 以相應放大或暫停和繼續計算資源來節省成本。"
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
ms.openlocfilehash: abe22f542a79714f6e894870872ee6b76ffe7633
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a><span data-ttu-id="dffae-104">管理 Azure SQL 資料倉儲中的計算能力 (概觀)</span><span class="sxs-lookup"><span data-stu-id="dffae-104">Manage compute power in Azure SQL Data Warehouse (Overview)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dffae-105">概觀</span><span class="sxs-lookup"><span data-stu-id="dffae-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="dffae-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="dffae-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="dffae-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dffae-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="dffae-108">REST</span><span class="sxs-lookup"><span data-stu-id="dffae-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="dffae-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="dffae-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<span data-ttu-id="dffae-110">SQL 資料倉儲的架構分隔儲存體和計算功能，可單獨進行調整。</span><span class="sxs-lookup"><span data-stu-id="dffae-110">The architecture of SQL Data Warehouse separates storage and compute, allowing each to scale independently.</span></span> <span data-ttu-id="dffae-111">如此一來，可以調整計算以符合與資料量無關的效能需求。</span><span class="sxs-lookup"><span data-stu-id="dffae-111">As a result, compute can be scaled to meet performance demands independent of the amount of data.</span></span> <span data-ttu-id="dffae-112">這個架構的自然結果為計算[計費][billed]和儲存體無關。</span><span class="sxs-lookup"><span data-stu-id="dffae-112">A natural consequence of this architecture is that [billing][billed] for compute and storage is separate.</span></span> 

<span data-ttu-id="dffae-113">本概觀說明擴充如何與 SQL 資料倉儲搭配使用，以及如何運用暫停、繼續和調整 SQL 資料倉儲的功能。</span><span class="sxs-lookup"><span data-stu-id="dffae-113">This overview describes how scale out works with SQL Data Warehouse and how to utilize the pause, resume, and scale capabilities of SQL Data Warehouse.</span></span> <span data-ttu-id="dffae-114">請參閱[資料倉儲單位 (DWU)][data warehouse units (DWUs)] 頁面以了解 DWU 和效能有何相關。</span><span class="sxs-lookup"><span data-stu-id="dffae-114">Consult the [data warehouse units (DWUs)][data warehouse units (DWUs)] page to learn how DWUs and performance are related.</span></span> 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a><span data-ttu-id="dffae-115">計算管理作業如何在 SQL 資料倉儲中運作</span><span class="sxs-lookup"><span data-stu-id="dffae-115">How compute management operations work in SQL Data Warehouse</span></span>
<span data-ttu-id="dffae-116">SQL 資料倉儲架構是由控制節點、計算節點及分散到 60 個散發套件的儲存層所組成。</span><span class="sxs-lookup"><span data-stu-id="dffae-116">The architecture for SQL Data Warehouse consists of a control node, compute nodes, and the storage layer spread across 60 distributions.</span></span> 

<span data-ttu-id="dffae-117">在 SQL 資料倉儲中的正常作用中工作階段期間，您系統的前端節點會管理中繼資料並包含分散式查詢最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="dffae-117">During a normal active session in SQL Data Warehouse, your system's head node manages the metadata and contains the distributed query optimizer.</span></span> <span data-ttu-id="dffae-118">此前端節點以下為計算節點和儲存層。</span><span class="sxs-lookup"><span data-stu-id="dffae-118">Beneath this head node are your compute nodes and your storage layer.</span></span> <span data-ttu-id="dffae-119">針對 DWU 400，您的系統有一個前端節點、四個計算節點和儲存層，其中包含 60 個散發套件。</span><span class="sxs-lookup"><span data-stu-id="dffae-119">For a DWU 400, your system has one head node, four compute nodes, and the storage layer, consisting of 60 distributions.</span></span> 

<span data-ttu-id="dffae-120">在進行調整或暫停作業時，系統會先刪除所有傳入的查詢，並會復原交易，以確保一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="dffae-120">When you undergo a scale or pause operation, the system first kills all incoming queries and then rolls back transactions to ensure a consistent state.</span></span> <span data-ttu-id="dffae-121">針對調整作業，僅在這個交易回復完成後調整才會發生。</span><span class="sxs-lookup"><span data-stu-id="dffae-121">For scale operations, scaling will only occur once this transactional rollback has completed.</span></span> <span data-ttu-id="dffae-122">相應增加作業中，系統會佈建計算節點的額外所需數目，然後開始將計算節點重新附加至儲存層。</span><span class="sxs-lookup"><span data-stu-id="dffae-122">For a scale-up operation, the system provisions the extra desired number of compute nodes, and then begins reattaching the compute nodes to the storage layer.</span></span> <span data-ttu-id="dffae-123">相應減少作業中，會釋放不需要的節點，其餘的計算節點會將其本身重新附加至適當數目的散發套件。</span><span class="sxs-lookup"><span data-stu-id="dffae-123">For a scale-down operation, the unneeded nodes are released and the remaining compute nodes reattach themselves to the appropriate number of distributions.</span></span> <span data-ttu-id="dffae-124">暫停作業中，會釋放所有的計算節點，而且您的系統會經歷各種中繼資料作業以將最後系統保持在穩定的狀態。</span><span class="sxs-lookup"><span data-stu-id="dffae-124">For a pause operation, all compute nodes are released and your system will undergo a variety of metadata operations to leave your final system in a stable state.</span></span>

| <span data-ttu-id="dffae-125">DWU</span><span class="sxs-lookup"><span data-stu-id="dffae-125">DWU</span></span>  | <span data-ttu-id="dffae-126">\# 個計算節點</span><span class="sxs-lookup"><span data-stu-id="dffae-126">\#of compute nodes</span></span> | <span data-ttu-id="dffae-127">每節點 \# 個散發</span><span class="sxs-lookup"><span data-stu-id="dffae-127">\# of distributions per node</span></span> |
| ---- | ------------------ | ---------------------------- |
| <span data-ttu-id="dffae-128">100</span><span class="sxs-lookup"><span data-stu-id="dffae-128">100</span></span>  | <span data-ttu-id="dffae-129">1</span><span class="sxs-lookup"><span data-stu-id="dffae-129">1</span></span>                  | <span data-ttu-id="dffae-130">60</span><span class="sxs-lookup"><span data-stu-id="dffae-130">60</span></span>                           |
| <span data-ttu-id="dffae-131">200</span><span class="sxs-lookup"><span data-stu-id="dffae-131">200</span></span>  | <span data-ttu-id="dffae-132">2</span><span class="sxs-lookup"><span data-stu-id="dffae-132">2</span></span>                  | <span data-ttu-id="dffae-133">30</span><span class="sxs-lookup"><span data-stu-id="dffae-133">30</span></span>                           |
| <span data-ttu-id="dffae-134">300</span><span class="sxs-lookup"><span data-stu-id="dffae-134">300</span></span>  | <span data-ttu-id="dffae-135">3</span><span class="sxs-lookup"><span data-stu-id="dffae-135">3</span></span>                  | <span data-ttu-id="dffae-136">20</span><span class="sxs-lookup"><span data-stu-id="dffae-136">20</span></span>                           |
| <span data-ttu-id="dffae-137">400</span><span class="sxs-lookup"><span data-stu-id="dffae-137">400</span></span>  | <span data-ttu-id="dffae-138">4</span><span class="sxs-lookup"><span data-stu-id="dffae-138">4</span></span>                  | <span data-ttu-id="dffae-139">15</span><span class="sxs-lookup"><span data-stu-id="dffae-139">15</span></span>                           |
| <span data-ttu-id="dffae-140">500</span><span class="sxs-lookup"><span data-stu-id="dffae-140">500</span></span>  | <span data-ttu-id="dffae-141">5</span><span class="sxs-lookup"><span data-stu-id="dffae-141">5</span></span>                  | <span data-ttu-id="dffae-142">12</span><span class="sxs-lookup"><span data-stu-id="dffae-142">12</span></span>                           |
| <span data-ttu-id="dffae-143">600</span><span class="sxs-lookup"><span data-stu-id="dffae-143">600</span></span>  | <span data-ttu-id="dffae-144">6</span><span class="sxs-lookup"><span data-stu-id="dffae-144">6</span></span>                  | <span data-ttu-id="dffae-145">10</span><span class="sxs-lookup"><span data-stu-id="dffae-145">10</span></span>                           |
| <span data-ttu-id="dffae-146">1000</span><span class="sxs-lookup"><span data-stu-id="dffae-146">1000</span></span> | <span data-ttu-id="dffae-147">10</span><span class="sxs-lookup"><span data-stu-id="dffae-147">10</span></span>                 | <span data-ttu-id="dffae-148">6</span><span class="sxs-lookup"><span data-stu-id="dffae-148">6</span></span>                            |
| <span data-ttu-id="dffae-149">1200</span><span class="sxs-lookup"><span data-stu-id="dffae-149">1200</span></span> | <span data-ttu-id="dffae-150">12</span><span class="sxs-lookup"><span data-stu-id="dffae-150">12</span></span>                 | <span data-ttu-id="dffae-151">5</span><span class="sxs-lookup"><span data-stu-id="dffae-151">5</span></span>                            |
| <span data-ttu-id="dffae-152">1500</span><span class="sxs-lookup"><span data-stu-id="dffae-152">1500</span></span> | <span data-ttu-id="dffae-153">15</span><span class="sxs-lookup"><span data-stu-id="dffae-153">15</span></span>                 | <span data-ttu-id="dffae-154">4</span><span class="sxs-lookup"><span data-stu-id="dffae-154">4</span></span>                            |
| <span data-ttu-id="dffae-155">2000</span><span class="sxs-lookup"><span data-stu-id="dffae-155">2000</span></span> | <span data-ttu-id="dffae-156">20</span><span class="sxs-lookup"><span data-stu-id="dffae-156">20</span></span>                 | <span data-ttu-id="dffae-157">3</span><span class="sxs-lookup"><span data-stu-id="dffae-157">3</span></span>                            |
| <span data-ttu-id="dffae-158">3000</span><span class="sxs-lookup"><span data-stu-id="dffae-158">3000</span></span> | <span data-ttu-id="dffae-159">30</span><span class="sxs-lookup"><span data-stu-id="dffae-159">30</span></span>                 | <span data-ttu-id="dffae-160">2</span><span class="sxs-lookup"><span data-stu-id="dffae-160">2</span></span>                            |
| <span data-ttu-id="dffae-161">6000</span><span class="sxs-lookup"><span data-stu-id="dffae-161">6000</span></span> | <span data-ttu-id="dffae-162">60</span><span class="sxs-lookup"><span data-stu-id="dffae-162">60</span></span>                 | <span data-ttu-id="dffae-163">1</span><span class="sxs-lookup"><span data-stu-id="dffae-163">1</span></span>                            |

<span data-ttu-id="dffae-164">管理計算所需的三個主要功能如下︰</span><span class="sxs-lookup"><span data-stu-id="dffae-164">The three primary functions for managing compute are:</span></span>

1. <span data-ttu-id="dffae-165">暫停</span><span class="sxs-lookup"><span data-stu-id="dffae-165">Pause</span></span>
2. <span data-ttu-id="dffae-166">繼續</span><span class="sxs-lookup"><span data-stu-id="dffae-166">Resume</span></span>
3. <span data-ttu-id="dffae-167">調整</span><span class="sxs-lookup"><span data-stu-id="dffae-167">Scale</span></span>

<span data-ttu-id="dffae-168">每個這些作業可能需要幾分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="dffae-168">Each of these operations may take several minutes to complete.</span></span> <span data-ttu-id="dffae-169">如果您是自動調整/暫停/繼續，可能想要實作邏輯以確保在進行其他動作之前，先確認特定作業已完成。</span><span class="sxs-lookup"><span data-stu-id="dffae-169">If you are scaling/pausing/resuming automatically, you may want to implement logic to ensure that certain operations have been completed before proceeding with another action.</span></span> 

<span data-ttu-id="dffae-170">透過各種端點檢查資料庫狀態可讓您正確地實作這類作業的自動化。</span><span class="sxs-lookup"><span data-stu-id="dffae-170">Checking the database state through various endpoints will allow you to correctly implement automation of such operations.</span></span> <span data-ttu-id="dffae-171">入口網站會在作業完成時提供通知和資料庫的目前狀態，但不允許以程式設計方式檢查狀態。</span><span class="sxs-lookup"><span data-stu-id="dffae-171">The portal will provide notification upon completion of an operation and the databases current state but does not allow for programmatic checking of state.</span></span> 

>  [!NOTE]
>
>  <span data-ttu-id="dffae-172">計算管理功能並未跨所有端點存在。</span><span class="sxs-lookup"><span data-stu-id="dffae-172">Compute management functionality does not exist across all endpoints.</span></span>
>
>  

|              | <span data-ttu-id="dffae-173">暫停/繼續</span><span class="sxs-lookup"><span data-stu-id="dffae-173">Pause/Resume</span></span> | <span data-ttu-id="dffae-174">調整</span><span class="sxs-lookup"><span data-stu-id="dffae-174">Scale</span></span> | <span data-ttu-id="dffae-175">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="dffae-175">Check database state</span></span> |
| ------------ | ------------ | ----- | -------------------- |
| <span data-ttu-id="dffae-176">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dffae-176">Azure portal</span></span> | <span data-ttu-id="dffae-177">是</span><span class="sxs-lookup"><span data-stu-id="dffae-177">Yes</span></span>          | <span data-ttu-id="dffae-178">是</span><span class="sxs-lookup"><span data-stu-id="dffae-178">Yes</span></span>   | <span data-ttu-id="dffae-179">**否**</span><span class="sxs-lookup"><span data-stu-id="dffae-179">**No**</span></span>               |
| <span data-ttu-id="dffae-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dffae-180">PowerShell</span></span>   | <span data-ttu-id="dffae-181">是</span><span class="sxs-lookup"><span data-stu-id="dffae-181">Yes</span></span>          | <span data-ttu-id="dffae-182">是</span><span class="sxs-lookup"><span data-stu-id="dffae-182">Yes</span></span>   | <span data-ttu-id="dffae-183">是</span><span class="sxs-lookup"><span data-stu-id="dffae-183">Yes</span></span>                  |
| <span data-ttu-id="dffae-184">REST API</span><span class="sxs-lookup"><span data-stu-id="dffae-184">REST API</span></span>     | <span data-ttu-id="dffae-185">是</span><span class="sxs-lookup"><span data-stu-id="dffae-185">Yes</span></span>          | <span data-ttu-id="dffae-186">是</span><span class="sxs-lookup"><span data-stu-id="dffae-186">Yes</span></span>   | <span data-ttu-id="dffae-187">是</span><span class="sxs-lookup"><span data-stu-id="dffae-187">Yes</span></span>                  |
| <span data-ttu-id="dffae-188">T-SQL</span><span class="sxs-lookup"><span data-stu-id="dffae-188">T-SQL</span></span>        | <span data-ttu-id="dffae-189">**否**</span><span class="sxs-lookup"><span data-stu-id="dffae-189">**No**</span></span>       | <span data-ttu-id="dffae-190">是</span><span class="sxs-lookup"><span data-stu-id="dffae-190">Yes</span></span>   | <span data-ttu-id="dffae-191">是</span><span class="sxs-lookup"><span data-stu-id="dffae-191">Yes</span></span>                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="dffae-192">調整計算</span><span class="sxs-lookup"><span data-stu-id="dffae-192">Scale compute</span></span>

<span data-ttu-id="dffae-193">SQL 資料倉儲中的效能測量單位為[資料倉儲單位 (DWU)][data warehouse units (DWUs)]，這是計算資源的抽象量值，例如 CPU、記憶體和 I/O 頻寬。</span><span class="sxs-lookup"><span data-stu-id="dffae-193">Performance in SQL Data Warehouse is measured in [data warehouse units (DWUs)][data warehouse units (DWUs)] which is an abstracted measure of compute resources such as CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="dffae-194">想要調整其系統效能的使用者可透過各種方式來完成，例如透過入口網站、T-SQL 和 REST API。</span><span class="sxs-lookup"><span data-stu-id="dffae-194">A user who wishes to scale their system's performance can do so through various means, such as through the portal, T-SQL, and REST APIs.</span></span> 

### <a name="how-do-i-scale-compute"></a><span data-ttu-id="dffae-195">如何調整計算？</span><span class="sxs-lookup"><span data-stu-id="dffae-195">How do I scale compute?</span></span>
<span data-ttu-id="dffae-196">計算電源會藉由變更 DWU 設定來管理您的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="dffae-196">Compute power is managed for you SQL Data Warehouse by changing the DWU setting.</span></span> <span data-ttu-id="dffae-197">隨著您針對特定作業新增更多的 DWU，效能會[以線性方式][linearly]提升。</span><span class="sxs-lookup"><span data-stu-id="dffae-197">Performance increases [linearly][linearly] as you add more DWU for certain operations.</span></span>  <span data-ttu-id="dffae-198">當您將系統相應增加或減少時，我們提供的 DWU 供應項目可確保您的效能會明顯變更。</span><span class="sxs-lookup"><span data-stu-id="dffae-198">We offer DWU offerings that ensure that your performance will change noticeably when you scale your system up or down.</span></span> 

<span data-ttu-id="dffae-199">若要調整 DWU，您可以使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="dffae-199">To adjust DWUs, you can use any of these individual methods.</span></span>

* <span data-ttu-id="dffae-200">[使用 Azure 入口網站調整計算能力][Scale compute power with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="dffae-200">[Scale compute power with Azure portal][Scale compute power with Azure portal]</span></span>
* <span data-ttu-id="dffae-201">[使用 PowerShell 調整計算能力][Scale compute power with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dffae-201">[Scale compute power with PowerShell][Scale compute power with PowerShell]</span></span>
* <span data-ttu-id="dffae-202">[使用 REST API 調整計算能力][Scale compute power with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="dffae-202">[Scale compute power with REST APIs][Scale compute power with REST APIs]</span></span>
* <span data-ttu-id="dffae-203">[使用 TSQL 調整計算能力][Scale compute power with TSQL]</span><span class="sxs-lookup"><span data-stu-id="dffae-203">[Scale compute power with TSQL][Scale compute power with TSQL]</span></span>

### <a name="how-many-dwus-should-i-use"></a><span data-ttu-id="dffae-204">應該使用多少 DWU 呢？</span><span class="sxs-lookup"><span data-stu-id="dffae-204">How many DWUs should I use?</span></span>

<span data-ttu-id="dffae-205">為了要了解您理想的 DWU 值，嘗試在載入您的資料之後相應增加和相應減少並執行幾個查詢。</span><span class="sxs-lookup"><span data-stu-id="dffae-205">To understand what your ideal DWU value is, try scaling up and down, and running a few queries after loading your data.</span></span> <span data-ttu-id="dffae-206">由於調整很快速，您可以在一小時內嘗各種效能層級。</span><span class="sxs-lookup"><span data-stu-id="dffae-206">Since scaling is quick, you can try various performance levels in an hour or less.</span></span> 

> [!Note] 
> <span data-ttu-id="dffae-207">SQL 資料倉儲是專為處理大量資料所設計。</span><span class="sxs-lookup"><span data-stu-id="dffae-207">SQL Data Warehouse is designed to process large amounts of data.</span></span> <span data-ttu-id="dffae-208">若要查看其進行調整的實際能力，尤其是在較大的 DWU，您想要使用接近或超過 1 TB 的大型資料集。</span><span class="sxs-lookup"><span data-stu-id="dffae-208">To see its true capabilities for scaling, especially at larger DWUs, you want to use a large data set which approaches or exceeds 1 TB.</span></span>

<span data-ttu-id="dffae-209">尋找您的工作負載的最佳 DWU 的建議事項︰</span><span class="sxs-lookup"><span data-stu-id="dffae-209">Recommendations for finding the best DWU for your workload:</span></span>

1. <span data-ttu-id="dffae-210">若是開發過程中的資料倉儲，可選取較少的 DWU 效能等級。</span><span class="sxs-lookup"><span data-stu-id="dffae-210">For a data warehouse in development, begin by selecting a smaller DWU performance level.</span></span>  <span data-ttu-id="dffae-211">DW400 或 DW200 是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="dffae-211">A good starting point is DW400 or DW200.</span></span>
2. <span data-ttu-id="dffae-212">監視應用程式效能，觀察比較所選 DWU 數目與您觀察到的效能。</span><span class="sxs-lookup"><span data-stu-id="dffae-212">Monitor your application performance, observing the number of DWUs selected compared to the performance you observe.</span></span>
3. <span data-ttu-id="dffae-213">透過假設線性標尺，判斷需要將效能加快或減慢多少才能達到您需求的最佳效能等級。</span><span class="sxs-lookup"><span data-stu-id="dffae-213">Determine how much faster or slower performance should be for you to reach the optimum performance level for your requirements by assuming linear scale.</span></span>
4. <span data-ttu-id="dffae-214">增加或減少 DWU 數目與您想要讓您的工作負載更快或更慢執行成正比。</span><span class="sxs-lookup"><span data-stu-id="dffae-214">Increase or decrease the number of DWUs in proportion to how much faster or slower you want your workload to perform.</span></span> 
5. <span data-ttu-id="dffae-215">繼續進行調整，直到達到您業務需求的最佳效能為止。</span><span class="sxs-lookup"><span data-stu-id="dffae-215">Continue making adjustments until you reach an optimum performance level for your business requirements.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dffae-216">如果工作可以在計算節點之間分割，則查詢效能只會隨更多的平行處理增加。</span><span class="sxs-lookup"><span data-stu-id="dffae-216">Query performance only increases with more parallelization if the work can be split between compute nodes.</span></span> <span data-ttu-id="dffae-217">如果您發現縮放比例不會變更您的效能，請造訪我們的效能微調文章，以檢查您的資料是否平均地分散，或是您是否進行大量的資料移動。</span><span class="sxs-lookup"><span data-stu-id="dffae-217">If you find that scaling is not changing your performance, please check out our performance tuning articles to check whether your data is unevenly distributed or if you are introducing a large amount of data movement.</span></span> 

### <a name="when-should-i-scale-dwus"></a><span data-ttu-id="dffae-218">何時調整 DWU？</span><span class="sxs-lookup"><span data-stu-id="dffae-218">When should I scale DWUs?</span></span>
<span data-ttu-id="dffae-219">調整 DWU 會改變下列重要案例︰</span><span class="sxs-lookup"><span data-stu-id="dffae-219">Scaling DWUs alters the following important scenarios:</span></span>

1. <span data-ttu-id="dffae-220">以線性方式變更掃描、彙總和 CTAS 陳述式的系統效能</span><span class="sxs-lookup"><span data-stu-id="dffae-220">Linearly changing performance of the system for scans, aggregations, and CTAS statements</span></span>
2. <span data-ttu-id="dffae-221">使用 PolyBase 載入時，增加讀取器和寫入的數目</span><span class="sxs-lookup"><span data-stu-id="dffae-221">Increasing the number of readers and writers when loading with PolyBase</span></span>
3. <span data-ttu-id="dffae-222">並行查詢和並行存取插槽數目上限</span><span class="sxs-lookup"><span data-stu-id="dffae-222">Maximum number of concurrent queries and concurrency slots</span></span>

<span data-ttu-id="dffae-223">DWU 調整時機的建議︰</span><span class="sxs-lookup"><span data-stu-id="dffae-223">Recommendations for when to scale DWUs:</span></span>

1. <span data-ttu-id="dffae-224">執行大量資料載入或轉換作業之前，相應增加 DWU 以使您的資料更快速可供使用。</span><span class="sxs-lookup"><span data-stu-id="dffae-224">Before you perform a heavy data loading or transformation operation, scale up DWUs so that your data is available more quickly.</span></span>
2. <span data-ttu-id="dffae-225">在尖峰營業時間內，調整以適應大量的並行查詢。</span><span class="sxs-lookup"><span data-stu-id="dffae-225">During peak business hours, scale to accommodate larger numbers of concurrent queries.</span></span> 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="dffae-226">暫停計算</span><span class="sxs-lookup"><span data-stu-id="dffae-226">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="dffae-227">若要暫停資料庫，您可以使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="dffae-227">To pause a database, use any of these individual methods.</span></span>

* <span data-ttu-id="dffae-228">[使用 Azure 入口網站暫停計算][Pause compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="dffae-228">[Pause compute with Azure portal][Pause compute with Azure portal]</span></span>
* <span data-ttu-id="dffae-229">[使用 PowerShell 暫停計算][Pause compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dffae-229">[Pause compute with PowerShell][Pause compute with PowerShell]</span></span>
* <span data-ttu-id="dffae-230">[使用 REST API 暫停計算][Pause compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="dffae-230">[Pause compute with REST APIs][Pause compute with REST APIs]</span></span>

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="dffae-231">繼續計算</span><span class="sxs-lookup"><span data-stu-id="dffae-231">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="dffae-232">若要繼續資料庫，您可以使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="dffae-232">To resume a database, use any of these individual methods.</span></span>

* <span data-ttu-id="dffae-233">[使用 Azure 入口網站繼續計算][Resume compute with Azure portal]</span><span class="sxs-lookup"><span data-stu-id="dffae-233">[Resume compute with Azure portal][Resume compute with Azure portal]</span></span>
* <span data-ttu-id="dffae-234">[使用 PowerShell 繼續計算][Resume compute with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dffae-234">[Resume compute with PowerShell][Resume compute with PowerShell]</span></span>
* <span data-ttu-id="dffae-235">[使用 REST API 繼續計算][Resume compute with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="dffae-235">[Resume compute with REST APIs][Resume compute with REST APIs]</span></span>

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="dffae-236">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="dffae-236">Check database state</span></span> 

<span data-ttu-id="dffae-237">若要繼續資料庫，您可以使用任何一種個別的方法。</span><span class="sxs-lookup"><span data-stu-id="dffae-237">To resume a database, use any of these individual methods.</span></span>

- <span data-ttu-id="dffae-238">[使用 T-SQL 檢查資料庫狀態][Check database state with T-SQL]</span><span class="sxs-lookup"><span data-stu-id="dffae-238">[Check database state with T-SQL][Check database state with T-SQL]</span></span>
- <span data-ttu-id="dffae-239">[使用 PowerShell 檢查資料庫狀態][Check database state with PowerShell]</span><span class="sxs-lookup"><span data-stu-id="dffae-239">[Check database state with PowerShell][Check database state with PowerShell]</span></span>
- <span data-ttu-id="dffae-240">[使用 REST API 檢查資料庫狀態][Check database state with REST APIs]</span><span class="sxs-lookup"><span data-stu-id="dffae-240">[Check database state with REST APIs][Check database state with REST APIs]</span></span>

## <a name="permissions"></a><span data-ttu-id="dffae-241">權限</span><span class="sxs-lookup"><span data-stu-id="dffae-241">Permissions</span></span>

<span data-ttu-id="dffae-242">調整資料庫需要 [ALTER DATABASE][ALTER DATABASE] 中所述的權限。</span><span class="sxs-lookup"><span data-stu-id="dffae-242">Scaling the database requires the permissions described in [ALTER DATABASE][ALTER DATABASE].</span></span>  <span data-ttu-id="dffae-243">暫停和繼續需要 [SQL DB 參與者][SQL DB Contributor]權限，特別是 Microsoft.Sql/servers/databases/action。</span><span class="sxs-lookup"><span data-stu-id="dffae-243">Pause and Resume require the [SQL DB Contributor][SQL DB Contributor] permission, specifically Microsoft.Sql/servers/databases/action.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="dffae-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dffae-244">Next steps</span></span>
<span data-ttu-id="dffae-245">請參閱下列文章，以瞭解其他一些關鍵效能概念：</span><span class="sxs-lookup"><span data-stu-id="dffae-245">Refer to the following articles to help you understand some additional key performance concepts:</span></span>

* <span data-ttu-id="dffae-246">[工作負載和並行管理][Workload and concurrency management]</span><span class="sxs-lookup"><span data-stu-id="dffae-246">[Workload and concurrency management][Workload and concurrency management]</span></span>
* <span data-ttu-id="dffae-247">[資料表設計概觀][Table design overview]</span><span class="sxs-lookup"><span data-stu-id="dffae-247">[Table design overview][Table design overview]</span></span>
* <span data-ttu-id="dffae-248">[資料表散發][Table distribution]</span><span class="sxs-lookup"><span data-stu-id="dffae-248">[Table distribution][Table distribution]</span></span>
* <span data-ttu-id="dffae-249">[索引資料表的編製][Table indexing]</span><span class="sxs-lookup"><span data-stu-id="dffae-249">[Table indexing][Table indexing]</span></span>
* <span data-ttu-id="dffae-250">[資料表分割][Table partitioning]</span><span class="sxs-lookup"><span data-stu-id="dffae-250">[Table partitioning][Table partitioning]</span></span>
* <span data-ttu-id="dffae-251">[資料表統計資料][Table statistics]</span><span class="sxs-lookup"><span data-stu-id="dffae-251">[Table statistics][Table statistics]</span></span>
* <span data-ttu-id="dffae-252">[最佳作法][Best practices]</span><span class="sxs-lookup"><span data-stu-id="dffae-252">[Best practices][Best practices]</span></span>

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
