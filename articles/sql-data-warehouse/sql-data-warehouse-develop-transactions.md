---
title: "SQL 資料倉儲中的 aaaTransactions |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中實作交易以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="5939d-103">SQL 資料倉儲中的交易</span><span class="sxs-lookup"><span data-stu-id="5939d-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="5939d-104">如您所預期，SQL 資料倉儲 hello 資料倉儲工作負載的部分支援的交易。</span><span class="sxs-lookup"><span data-stu-id="5939d-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="5939d-105">不過，SQL 資料倉儲的 tooensure hello 效能所維護的某些功能會受到限制時的小數位數比較的 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5939d-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="5939d-106">本文章重點說明 hello 差異，並列出 hello 其他人。</span><span class="sxs-lookup"><span data-stu-id="5939d-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="5939d-107">交易隔離層級</span><span class="sxs-lookup"><span data-stu-id="5939d-107">Transaction isolation levels</span></span>
<span data-ttu-id="5939d-108">SQL 資料倉儲實作 ACID 交易。</span><span class="sxs-lookup"><span data-stu-id="5939d-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="5939d-109">不過，hello hello 交易支援的隔離是限制太`READ UNCOMMITTED`，就無法變更。</span><span class="sxs-lookup"><span data-stu-id="5939d-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="5939d-110">您可以實作的一些程式碼撰寫 tooprevent dirty 讀取的資料，如果這是您的問題的方法。</span><span class="sxs-lookup"><span data-stu-id="5939d-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="5939d-111">hello 最受歡迎的方法會利用 CTAS 和資料表資料分割切換 （通常稱為 hello 滑動視窗模式） tooprevent 使用者查詢仍在準備資料。</span><span class="sxs-lookup"><span data-stu-id="5939d-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="5939d-112">檢視預先篩選 hello 資料也是常用的方法。</span><span class="sxs-lookup"><span data-stu-id="5939d-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="5939d-113">交易大小</span><span class="sxs-lookup"><span data-stu-id="5939d-113">Transaction size</span></span>
<span data-ttu-id="5939d-114">單一資料修改交易的大小是有限制的。</span><span class="sxs-lookup"><span data-stu-id="5939d-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="5939d-115">hello 現在會套用限制 「 每一通訊群組 」。</span><span class="sxs-lookup"><span data-stu-id="5939d-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="5939d-116">因此，hello 總計配置可以計算 hello 限制乘以 hello 發佈計數。</span><span class="sxs-lookup"><span data-stu-id="5939d-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="5939d-117">hello 交易中的資料列 tooapproximate hello 最大數目除以 hello 的每個資料列大小總計的 hello 發佈端點。</span><span class="sxs-lookup"><span data-stu-id="5939d-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="5939d-118">可變長度資料行，請考慮花費的平均資料行長度，而不是使用 hello 大小上限。</span><span class="sxs-lookup"><span data-stu-id="5939d-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="5939d-119">Hello hello 表有進行下列假設：</span><span class="sxs-lookup"><span data-stu-id="5939d-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="5939d-120">已發生的資料平均散發</span><span class="sxs-lookup"><span data-stu-id="5939d-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="5939d-121">hello 平均資料列長度是 250 個位元組</span><span class="sxs-lookup"><span data-stu-id="5939d-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="5939d-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="5939d-122">[DWU][DWU]</span></span> | <span data-ttu-id="5939d-123">每個散發的容量 (GiB)</span><span class="sxs-lookup"><span data-stu-id="5939d-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="5939d-124">散發的數目</span><span class="sxs-lookup"><span data-stu-id="5939d-124">Number of Distributions</span></span> | <span data-ttu-id="5939d-125">交易大小上限 (GiB)</span><span class="sxs-lookup"><span data-stu-id="5939d-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="5939d-126"># 每發佈的資料列</span><span class="sxs-lookup"><span data-stu-id="5939d-126"># Rows per distribution</span></span> | <span data-ttu-id="5939d-127">每個交易的資料列數上限</span><span class="sxs-lookup"><span data-stu-id="5939d-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5939d-128">DW100</span><span class="sxs-lookup"><span data-stu-id="5939d-128">DW100</span></span> |<span data-ttu-id="5939d-129">1</span><span class="sxs-lookup"><span data-stu-id="5939d-129">1</span></span> |<span data-ttu-id="5939d-130">60</span><span class="sxs-lookup"><span data-stu-id="5939d-130">60</span></span> |<span data-ttu-id="5939d-131">60</span><span class="sxs-lookup"><span data-stu-id="5939d-131">60</span></span> |<span data-ttu-id="5939d-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-132">4,000,000</span></span> |<span data-ttu-id="5939d-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-133">240,000,000</span></span> |
| <span data-ttu-id="5939d-134">DW200</span><span class="sxs-lookup"><span data-stu-id="5939d-134">DW200</span></span> |<span data-ttu-id="5939d-135">1.5</span><span class="sxs-lookup"><span data-stu-id="5939d-135">1.5</span></span> |<span data-ttu-id="5939d-136">60</span><span class="sxs-lookup"><span data-stu-id="5939d-136">60</span></span> |<span data-ttu-id="5939d-137">90</span><span class="sxs-lookup"><span data-stu-id="5939d-137">90</span></span> |<span data-ttu-id="5939d-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-138">6,000,000</span></span> |<span data-ttu-id="5939d-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-139">360,000,000</span></span> |
| <span data-ttu-id="5939d-140">DW300</span><span class="sxs-lookup"><span data-stu-id="5939d-140">DW300</span></span> |<span data-ttu-id="5939d-141">2.25</span><span class="sxs-lookup"><span data-stu-id="5939d-141">2.25</span></span> |<span data-ttu-id="5939d-142">60</span><span class="sxs-lookup"><span data-stu-id="5939d-142">60</span></span> |<span data-ttu-id="5939d-143">135</span><span class="sxs-lookup"><span data-stu-id="5939d-143">135</span></span> |<span data-ttu-id="5939d-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-144">9,000,000</span></span> |<span data-ttu-id="5939d-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-145">540,000,000</span></span> |
| <span data-ttu-id="5939d-146">DW400</span><span class="sxs-lookup"><span data-stu-id="5939d-146">DW400</span></span> |<span data-ttu-id="5939d-147">3</span><span class="sxs-lookup"><span data-stu-id="5939d-147">3</span></span> |<span data-ttu-id="5939d-148">60</span><span class="sxs-lookup"><span data-stu-id="5939d-148">60</span></span> |<span data-ttu-id="5939d-149">180</span><span class="sxs-lookup"><span data-stu-id="5939d-149">180</span></span> |<span data-ttu-id="5939d-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-150">12,000,000</span></span> |<span data-ttu-id="5939d-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-151">720,000,000</span></span> |
| <span data-ttu-id="5939d-152">DW500</span><span class="sxs-lookup"><span data-stu-id="5939d-152">DW500</span></span> |<span data-ttu-id="5939d-153">3.75</span><span class="sxs-lookup"><span data-stu-id="5939d-153">3.75</span></span> |<span data-ttu-id="5939d-154">60</span><span class="sxs-lookup"><span data-stu-id="5939d-154">60</span></span> |<span data-ttu-id="5939d-155">225</span><span class="sxs-lookup"><span data-stu-id="5939d-155">225</span></span> |<span data-ttu-id="5939d-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-156">15,000,000</span></span> |<span data-ttu-id="5939d-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-157">900,000,000</span></span> |
| <span data-ttu-id="5939d-158">DW600</span><span class="sxs-lookup"><span data-stu-id="5939d-158">DW600</span></span> |<span data-ttu-id="5939d-159">4.5</span><span class="sxs-lookup"><span data-stu-id="5939d-159">4.5</span></span> |<span data-ttu-id="5939d-160">60</span><span class="sxs-lookup"><span data-stu-id="5939d-160">60</span></span> |<span data-ttu-id="5939d-161">270</span><span class="sxs-lookup"><span data-stu-id="5939d-161">270</span></span> |<span data-ttu-id="5939d-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-162">18,000,000</span></span> |<span data-ttu-id="5939d-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-163">1,080,000,000</span></span> |
| <span data-ttu-id="5939d-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="5939d-164">DW1000</span></span> |<span data-ttu-id="5939d-165">7.5</span><span class="sxs-lookup"><span data-stu-id="5939d-165">7.5</span></span> |<span data-ttu-id="5939d-166">60</span><span class="sxs-lookup"><span data-stu-id="5939d-166">60</span></span> |<span data-ttu-id="5939d-167">450</span><span class="sxs-lookup"><span data-stu-id="5939d-167">450</span></span> |<span data-ttu-id="5939d-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-168">30,000,000</span></span> |<span data-ttu-id="5939d-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-169">1,800,000,000</span></span> |
| <span data-ttu-id="5939d-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="5939d-170">DW1200</span></span> |<span data-ttu-id="5939d-171">9</span><span class="sxs-lookup"><span data-stu-id="5939d-171">9</span></span> |<span data-ttu-id="5939d-172">60</span><span class="sxs-lookup"><span data-stu-id="5939d-172">60</span></span> |<span data-ttu-id="5939d-173">540</span><span class="sxs-lookup"><span data-stu-id="5939d-173">540</span></span> |<span data-ttu-id="5939d-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-174">36,000,000</span></span> |<span data-ttu-id="5939d-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-175">2,160,000,000</span></span> |
| <span data-ttu-id="5939d-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="5939d-176">DW1500</span></span> |<span data-ttu-id="5939d-177">11.25</span><span class="sxs-lookup"><span data-stu-id="5939d-177">11.25</span></span> |<span data-ttu-id="5939d-178">60</span><span class="sxs-lookup"><span data-stu-id="5939d-178">60</span></span> |<span data-ttu-id="5939d-179">675</span><span class="sxs-lookup"><span data-stu-id="5939d-179">675</span></span> |<span data-ttu-id="5939d-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-180">45,000,000</span></span> |<span data-ttu-id="5939d-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-181">2,700,000,000</span></span> |
| <span data-ttu-id="5939d-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="5939d-182">DW2000</span></span> |<span data-ttu-id="5939d-183">15</span><span class="sxs-lookup"><span data-stu-id="5939d-183">15</span></span> |<span data-ttu-id="5939d-184">60</span><span class="sxs-lookup"><span data-stu-id="5939d-184">60</span></span> |<span data-ttu-id="5939d-185">900</span><span class="sxs-lookup"><span data-stu-id="5939d-185">900</span></span> |<span data-ttu-id="5939d-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-186">60,000,000</span></span> |<span data-ttu-id="5939d-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-187">3,600,000,000</span></span> |
| <span data-ttu-id="5939d-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="5939d-188">DW3000</span></span> |<span data-ttu-id="5939d-189">22.5</span><span class="sxs-lookup"><span data-stu-id="5939d-189">22.5</span></span> |<span data-ttu-id="5939d-190">60</span><span class="sxs-lookup"><span data-stu-id="5939d-190">60</span></span> |<span data-ttu-id="5939d-191">1,350</span><span class="sxs-lookup"><span data-stu-id="5939d-191">1,350</span></span> |<span data-ttu-id="5939d-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-192">90,000,000</span></span> |<span data-ttu-id="5939d-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-193">5,400,000,000</span></span> |
| <span data-ttu-id="5939d-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="5939d-194">DW6000</span></span> |<span data-ttu-id="5939d-195">45</span><span class="sxs-lookup"><span data-stu-id="5939d-195">45</span></span> |<span data-ttu-id="5939d-196">60</span><span class="sxs-lookup"><span data-stu-id="5939d-196">60</span></span> |<span data-ttu-id="5939d-197">2,700</span><span class="sxs-lookup"><span data-stu-id="5939d-197">2,700</span></span> |<span data-ttu-id="5939d-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-198">180,000,000</span></span> |<span data-ttu-id="5939d-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="5939d-199">10,800,000,000</span></span> |

<span data-ttu-id="5939d-200">hello 交易大小限制會套用每個交易或作業。</span><span class="sxs-lookup"><span data-stu-id="5939d-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="5939d-201">它不會套用到所有並行交易。</span><span class="sxs-lookup"><span data-stu-id="5939d-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="5939d-202">因此每個交易並允許 toowrite 資料 toohello 記錄此數量。</span><span class="sxs-lookup"><span data-stu-id="5939d-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="5939d-203">toooptimize hello toohello 記錄檔中寫入的資料量降到最低，請參閱 toohello[交易的最佳作法][ Transactions best practices]發行項。</span><span class="sxs-lookup"><span data-stu-id="5939d-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="5939d-204">hello 交易大小僅可達成雜湊或 ROUND_ROBIN 分散式的資料表 hello 位置分散的 hello 資料最大值為偶數。</span><span class="sxs-lookup"><span data-stu-id="5939d-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="5939d-205">如果 hello 交易正在寫入的資料扭曲方式 toohello 分佈 hello 限制則可能 toobe 達到先前 toohello 最大交易大小。</span><span class="sxs-lookup"><span data-stu-id="5939d-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="5939d-206">交易狀態</span><span class="sxs-lookup"><span data-stu-id="5939d-206">Transaction state</span></span>
<span data-ttu-id="5939d-207">SQL 資料倉儲會使用 hello XACT_STATE 函數 tooreport 失敗的交易使用 hello 值-2。</span><span class="sxs-lookup"><span data-stu-id="5939d-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="5939d-208">這表示 hello 交易失敗，且標示為進行僅復原</span><span class="sxs-lookup"><span data-stu-id="5939d-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="5939d-209">hello-2 的 hello XACT_STATE 函數 toodenote 失敗的交易代表不同的行為 tooSQL 伺服器使用。</span><span class="sxs-lookup"><span data-stu-id="5939d-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="5939d-210">SQL Server 使用 hello 值-1 toorepresent 認可的交易。</span><span class="sxs-lookup"><span data-stu-id="5939d-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="5939d-211">SQL Server 可以容忍某些錯誤，在交易內，而不需要 toobe 標示為認可。</span><span class="sxs-lookup"><span data-stu-id="5939d-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="5939d-212">例如， `SELECT 1/0` 會導致錯誤，但不會強制交易進入無法認可的狀態。</span><span class="sxs-lookup"><span data-stu-id="5939d-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="5939d-213">SQL Server 也允許 hello 認可的交易讀取。</span><span class="sxs-lookup"><span data-stu-id="5939d-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="5939d-214">不過，SQL 資料倉儲不會讓您這樣做作。</span><span class="sxs-lookup"><span data-stu-id="5939d-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="5939d-215">如果 SQL 資料倉儲交易內會發生錯誤，它會自動進入 hello-2 狀態，而且您不會無法 toomake 任何進一步 select 陳述式直到 hello 陳述式已回復。</span><span class="sxs-lookup"><span data-stu-id="5939d-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="5939d-216">因此，這是您的應用程式程式碼 toosee 如果它是使用 XACT_STATE 您可能需要修改 toomake 程式碼的重要 toocheck。</span><span class="sxs-lookup"><span data-stu-id="5939d-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="5939d-217">比方說，在 SQL Server 中，您可能會看到類似這樣的交易：</span><span class="sxs-lookup"><span data-stu-id="5939d-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5939d-218">如果您離開您的程式碼，因為其值高於您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="5939d-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="5939d-219">Msg 111233，層級 16，狀態 1，行 1 111233; 目前交易已中止，而且任何暫止變更已復原的 hello。</span><span class="sxs-lookup"><span data-stu-id="5939d-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="5939d-220">原因︰處於僅限復原狀態中的交易，未在使用 DDL、DML 或 SELECT 陳述式之前明確復原。</span><span class="sxs-lookup"><span data-stu-id="5939d-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="5939d-221">您也不會收到 hello hello 錯誤 * 函式的輸出。</span><span class="sxs-lookup"><span data-stu-id="5939d-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="5939d-222">SQL 資料倉儲中 hello 的程式碼需要 toobe 稍有變更：</span><span class="sxs-lookup"><span data-stu-id="5939d-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="5939d-223">hello 預期的行為現在觀察到。</span><span class="sxs-lookup"><span data-stu-id="5939d-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="5939d-224">hello 交易中的 hello 錯誤並如預期般，hello 錯誤 * 函式提供的值。</span><span class="sxs-lookup"><span data-stu-id="5939d-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="5939d-225">所有已變更為該 hello `ROLLBACK` hello 的交易之前 toohappen hello 讀取 hello 錯誤的資訊在 hello`CATCH`區塊。</span><span class="sxs-lookup"><span data-stu-id="5939d-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="5939d-226">Error_Line() 函式</span><span class="sxs-lookup"><span data-stu-id="5939d-226">Error_Line() function</span></span>
<span data-ttu-id="5939d-227">它也值得注意的是，SQL 資料倉儲不會實作或支援 hello error_line （） 函式。</span><span class="sxs-lookup"><span data-stu-id="5939d-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="5939d-228">如果此程式碼中有您需要 tooremove 它 toobe 符合 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5939d-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="5939d-229">請改用您的程式碼中的查詢標籤 tooimplement 對等的功能。</span><span class="sxs-lookup"><span data-stu-id="5939d-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="5939d-230">請參閱 toohello[標籤][ LABEL]文件以取得更多詳細資料，這項功能。</span><span class="sxs-lookup"><span data-stu-id="5939d-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="5939d-231">使用 THROW 和 RAISERROR</span><span class="sxs-lookup"><span data-stu-id="5939d-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="5939d-232">THROW 是 hello 更現代實作引發 SQL 資料倉儲中的例外狀況，但也支援 RAISERROR。</span><span class="sxs-lookup"><span data-stu-id="5939d-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="5939d-233">有一些值得支付注意 toohowever 的一些差異。</span><span class="sxs-lookup"><span data-stu-id="5939d-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="5939d-234">使用者定義的數字不能在 hello 100000 150,000 範圍擲回的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="5939d-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="5939d-235">RAISERROR 錯誤訊息固定為 50,000</span><span class="sxs-lookup"><span data-stu-id="5939d-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="5939d-236">不支援使用 sys.messages</span><span class="sxs-lookup"><span data-stu-id="5939d-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="5939d-237">限制</span><span class="sxs-lookup"><span data-stu-id="5939d-237">Limitiations</span></span>
<span data-ttu-id="5939d-238">SQL 資料倉儲確實有一些與 tootransactions 其他限制。</span><span class="sxs-lookup"><span data-stu-id="5939d-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="5939d-239">如下所示：</span><span class="sxs-lookup"><span data-stu-id="5939d-239">They are as follows:</span></span>

* <span data-ttu-id="5939d-240">沒有分散式交易</span><span class="sxs-lookup"><span data-stu-id="5939d-240">No distributed transactions</span></span>
* <span data-ttu-id="5939d-241">不允許巢狀交易</span><span class="sxs-lookup"><span data-stu-id="5939d-241">No nested transactions permitted</span></span>
* <span data-ttu-id="5939d-242">不允許儲存點</span><span class="sxs-lookup"><span data-stu-id="5939d-242">No save points allowed</span></span>
* <span data-ttu-id="5939d-243">沒有具名的交易</span><span class="sxs-lookup"><span data-stu-id="5939d-243">No named transactions</span></span>
* <span data-ttu-id="5939d-244">沒有標示的交易</span><span class="sxs-lookup"><span data-stu-id="5939d-244">No marked transactions</span></span>
* <span data-ttu-id="5939d-245">使用者定義的交易內部不支援 DDL，例如 `CREATE TABLE`</span><span class="sxs-lookup"><span data-stu-id="5939d-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="5939d-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5939d-246">Next steps</span></span>
<span data-ttu-id="5939d-247">toolearn 進一步了解最佳化交易，請參閱[交易的最佳作法][Transactions best practices]。</span><span class="sxs-lookup"><span data-stu-id="5939d-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="5939d-248">toolearn 有關其他 SQL 資料倉儲的最佳作法，請參閱[SQL 資料倉儲的最佳作法][SQL Data Warehouse best practices]。</span><span class="sxs-lookup"><span data-stu-id="5939d-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
