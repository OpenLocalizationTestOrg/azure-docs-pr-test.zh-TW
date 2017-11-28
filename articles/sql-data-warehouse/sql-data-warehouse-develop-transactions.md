---
title: "SQL 資料倉儲中的交易 | Microsoft Docs"
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
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="98961-103">SQL 資料倉儲中的交易</span><span class="sxs-lookup"><span data-stu-id="98961-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="98961-104">如您所預期，SQL 資料倉儲支援交易做為資料倉儲工作負載的一部分。</span><span class="sxs-lookup"><span data-stu-id="98961-104">As you would expect, SQL Data Warehouse supports transactions as part of the data warehouse workload.</span></span> <span data-ttu-id="98961-105">不過，為了確保 SQL 資料倉儲的效能維持在一定的程度，某些功能會受到限制 (相較於 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="98961-105">However, to ensure the performance of SQL Data Warehouse is maintained at scale some features are limited when compared to SQL Server.</span></span> <span data-ttu-id="98961-106">本文特別強調差異，並列出其他交易。</span><span class="sxs-lookup"><span data-stu-id="98961-106">This article highlights the differences and lists the others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="98961-107">交易隔離層級</span><span class="sxs-lookup"><span data-stu-id="98961-107">Transaction isolation levels</span></span>
<span data-ttu-id="98961-108">SQL 資料倉儲實作 ACID 交易。</span><span class="sxs-lookup"><span data-stu-id="98961-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="98961-109">不過，交易支援的隔離僅限於 `READ UNCOMMITTED` ，這無法變更。</span><span class="sxs-lookup"><span data-stu-id="98961-109">However, the Isolation of the transactional support is limited to `READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="98961-110">您可以實作許多編碼方法，以避免中途讀取 (dirty read) 資料 (如果您對此有所考量的話)。</span><span class="sxs-lookup"><span data-stu-id="98961-110">You can implement a number of coding methods to prevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="98961-111">大多數受歡迎的方法會運用 CTAS 和資料表分割切換 (通常也稱為滑動視窗模式)，以防止使用者查詢仍正準備中的資料。</span><span class="sxs-lookup"><span data-stu-id="98961-111">The most popular methods leverage both CTAS and table partition switching (often known as the sliding window pattern) to prevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="98961-112">預先篩選資料的檢視也是常用的方法。</span><span class="sxs-lookup"><span data-stu-id="98961-112">Views that pre-filter the data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="98961-113">交易大小</span><span class="sxs-lookup"><span data-stu-id="98961-113">Transaction size</span></span>
<span data-ttu-id="98961-114">單一資料修改交易的大小是有限制的。</span><span class="sxs-lookup"><span data-stu-id="98961-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="98961-115">「每個散發」都會套用目前的限制。</span><span class="sxs-lookup"><span data-stu-id="98961-115">The limit today is applied "per distribution".</span></span> <span data-ttu-id="98961-116">因此，將限制乘以散發計數可算出總配置。</span><span class="sxs-lookup"><span data-stu-id="98961-116">Therefore, the total allocation can be calculated by multiplying the limit by the distribution count.</span></span> <span data-ttu-id="98961-117">若要大致估計交易中的資料列總數，請將散發容量除以每個資料列的大小總計。</span><span class="sxs-lookup"><span data-stu-id="98961-117">To approximate the maximum number of rows in the transaction divide the distribution cap by the total size of each row.</span></span> <span data-ttu-id="98961-118">針對可變動的長度資料行，請考慮取得平均資料行長度，而不是使用大小上限。</span><span class="sxs-lookup"><span data-stu-id="98961-118">For variable length columns consider taking an average column length rather than using the maximum size.</span></span>

<span data-ttu-id="98961-119">在下表中，已進行下列假設：</span><span class="sxs-lookup"><span data-stu-id="98961-119">In the table below the following assumptions have been made:</span></span>

* <span data-ttu-id="98961-120">已發生的資料平均散發</span><span class="sxs-lookup"><span data-stu-id="98961-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="98961-121">平均資料列長度是 250 個位元組</span><span class="sxs-lookup"><span data-stu-id="98961-121">The average row length is 250 bytes</span></span>

| <span data-ttu-id="98961-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="98961-122">[DWU][DWU]</span></span> | <span data-ttu-id="98961-123">每個散發的容量 (GiB)</span><span class="sxs-lookup"><span data-stu-id="98961-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="98961-124">散發的數目</span><span class="sxs-lookup"><span data-stu-id="98961-124">Number of Distributions</span></span> | <span data-ttu-id="98961-125">交易大小上限 (GiB)</span><span class="sxs-lookup"><span data-stu-id="98961-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="98961-126"># 每發佈的資料列</span><span class="sxs-lookup"><span data-stu-id="98961-126"># Rows per distribution</span></span> | <span data-ttu-id="98961-127">每個交易的資料列數上限</span><span class="sxs-lookup"><span data-stu-id="98961-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="98961-128">DW100</span><span class="sxs-lookup"><span data-stu-id="98961-128">DW100</span></span> |<span data-ttu-id="98961-129">1</span><span class="sxs-lookup"><span data-stu-id="98961-129">1</span></span> |<span data-ttu-id="98961-130">60</span><span class="sxs-lookup"><span data-stu-id="98961-130">60</span></span> |<span data-ttu-id="98961-131">60</span><span class="sxs-lookup"><span data-stu-id="98961-131">60</span></span> |<span data-ttu-id="98961-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-132">4,000,000</span></span> |<span data-ttu-id="98961-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-133">240,000,000</span></span> |
| <span data-ttu-id="98961-134">DW200</span><span class="sxs-lookup"><span data-stu-id="98961-134">DW200</span></span> |<span data-ttu-id="98961-135">1.5</span><span class="sxs-lookup"><span data-stu-id="98961-135">1.5</span></span> |<span data-ttu-id="98961-136">60</span><span class="sxs-lookup"><span data-stu-id="98961-136">60</span></span> |<span data-ttu-id="98961-137">90</span><span class="sxs-lookup"><span data-stu-id="98961-137">90</span></span> |<span data-ttu-id="98961-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-138">6,000,000</span></span> |<span data-ttu-id="98961-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-139">360,000,000</span></span> |
| <span data-ttu-id="98961-140">DW300</span><span class="sxs-lookup"><span data-stu-id="98961-140">DW300</span></span> |<span data-ttu-id="98961-141">2.25</span><span class="sxs-lookup"><span data-stu-id="98961-141">2.25</span></span> |<span data-ttu-id="98961-142">60</span><span class="sxs-lookup"><span data-stu-id="98961-142">60</span></span> |<span data-ttu-id="98961-143">135</span><span class="sxs-lookup"><span data-stu-id="98961-143">135</span></span> |<span data-ttu-id="98961-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-144">9,000,000</span></span> |<span data-ttu-id="98961-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-145">540,000,000</span></span> |
| <span data-ttu-id="98961-146">DW400</span><span class="sxs-lookup"><span data-stu-id="98961-146">DW400</span></span> |<span data-ttu-id="98961-147">3</span><span class="sxs-lookup"><span data-stu-id="98961-147">3</span></span> |<span data-ttu-id="98961-148">60</span><span class="sxs-lookup"><span data-stu-id="98961-148">60</span></span> |<span data-ttu-id="98961-149">180</span><span class="sxs-lookup"><span data-stu-id="98961-149">180</span></span> |<span data-ttu-id="98961-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-150">12,000,000</span></span> |<span data-ttu-id="98961-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-151">720,000,000</span></span> |
| <span data-ttu-id="98961-152">DW500</span><span class="sxs-lookup"><span data-stu-id="98961-152">DW500</span></span> |<span data-ttu-id="98961-153">3.75</span><span class="sxs-lookup"><span data-stu-id="98961-153">3.75</span></span> |<span data-ttu-id="98961-154">60</span><span class="sxs-lookup"><span data-stu-id="98961-154">60</span></span> |<span data-ttu-id="98961-155">225</span><span class="sxs-lookup"><span data-stu-id="98961-155">225</span></span> |<span data-ttu-id="98961-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-156">15,000,000</span></span> |<span data-ttu-id="98961-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-157">900,000,000</span></span> |
| <span data-ttu-id="98961-158">DW600</span><span class="sxs-lookup"><span data-stu-id="98961-158">DW600</span></span> |<span data-ttu-id="98961-159">4.5</span><span class="sxs-lookup"><span data-stu-id="98961-159">4.5</span></span> |<span data-ttu-id="98961-160">60</span><span class="sxs-lookup"><span data-stu-id="98961-160">60</span></span> |<span data-ttu-id="98961-161">270</span><span class="sxs-lookup"><span data-stu-id="98961-161">270</span></span> |<span data-ttu-id="98961-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-162">18,000,000</span></span> |<span data-ttu-id="98961-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-163">1,080,000,000</span></span> |
| <span data-ttu-id="98961-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="98961-164">DW1000</span></span> |<span data-ttu-id="98961-165">7.5</span><span class="sxs-lookup"><span data-stu-id="98961-165">7.5</span></span> |<span data-ttu-id="98961-166">60</span><span class="sxs-lookup"><span data-stu-id="98961-166">60</span></span> |<span data-ttu-id="98961-167">450</span><span class="sxs-lookup"><span data-stu-id="98961-167">450</span></span> |<span data-ttu-id="98961-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-168">30,000,000</span></span> |<span data-ttu-id="98961-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-169">1,800,000,000</span></span> |
| <span data-ttu-id="98961-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="98961-170">DW1200</span></span> |<span data-ttu-id="98961-171">9</span><span class="sxs-lookup"><span data-stu-id="98961-171">9</span></span> |<span data-ttu-id="98961-172">60</span><span class="sxs-lookup"><span data-stu-id="98961-172">60</span></span> |<span data-ttu-id="98961-173">540</span><span class="sxs-lookup"><span data-stu-id="98961-173">540</span></span> |<span data-ttu-id="98961-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-174">36,000,000</span></span> |<span data-ttu-id="98961-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-175">2,160,000,000</span></span> |
| <span data-ttu-id="98961-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="98961-176">DW1500</span></span> |<span data-ttu-id="98961-177">11.25</span><span class="sxs-lookup"><span data-stu-id="98961-177">11.25</span></span> |<span data-ttu-id="98961-178">60</span><span class="sxs-lookup"><span data-stu-id="98961-178">60</span></span> |<span data-ttu-id="98961-179">675</span><span class="sxs-lookup"><span data-stu-id="98961-179">675</span></span> |<span data-ttu-id="98961-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-180">45,000,000</span></span> |<span data-ttu-id="98961-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-181">2,700,000,000</span></span> |
| <span data-ttu-id="98961-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="98961-182">DW2000</span></span> |<span data-ttu-id="98961-183">15</span><span class="sxs-lookup"><span data-stu-id="98961-183">15</span></span> |<span data-ttu-id="98961-184">60</span><span class="sxs-lookup"><span data-stu-id="98961-184">60</span></span> |<span data-ttu-id="98961-185">900</span><span class="sxs-lookup"><span data-stu-id="98961-185">900</span></span> |<span data-ttu-id="98961-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-186">60,000,000</span></span> |<span data-ttu-id="98961-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-187">3,600,000,000</span></span> |
| <span data-ttu-id="98961-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="98961-188">DW3000</span></span> |<span data-ttu-id="98961-189">22.5</span><span class="sxs-lookup"><span data-stu-id="98961-189">22.5</span></span> |<span data-ttu-id="98961-190">60</span><span class="sxs-lookup"><span data-stu-id="98961-190">60</span></span> |<span data-ttu-id="98961-191">1,350</span><span class="sxs-lookup"><span data-stu-id="98961-191">1,350</span></span> |<span data-ttu-id="98961-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-192">90,000,000</span></span> |<span data-ttu-id="98961-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-193">5,400,000,000</span></span> |
| <span data-ttu-id="98961-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="98961-194">DW6000</span></span> |<span data-ttu-id="98961-195">45</span><span class="sxs-lookup"><span data-stu-id="98961-195">45</span></span> |<span data-ttu-id="98961-196">60</span><span class="sxs-lookup"><span data-stu-id="98961-196">60</span></span> |<span data-ttu-id="98961-197">2,700</span><span class="sxs-lookup"><span data-stu-id="98961-197">2,700</span></span> |<span data-ttu-id="98961-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-198">180,000,000</span></span> |<span data-ttu-id="98961-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="98961-199">10,800,000,000</span></span> |

<span data-ttu-id="98961-200">系統會針對每個交易或作業套用交易大小限制。</span><span class="sxs-lookup"><span data-stu-id="98961-200">The transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="98961-201">它不會套用到所有並行交易。</span><span class="sxs-lookup"><span data-stu-id="98961-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="98961-202">因此允許每一個交易在記錄檔中寫入這個資料量。</span><span class="sxs-lookup"><span data-stu-id="98961-202">Therefore each transaction is permitted to write this amount of data to the log.</span></span> 

<span data-ttu-id="98961-203">若要最佳化寫入記錄的資料量並降到最低，請參閱[交易的最佳做法][Transactions best practices]一文。</span><span class="sxs-lookup"><span data-stu-id="98961-203">To optimize and minimize the amount of data written to the log please refer to the [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="98961-204">交易大小上限僅可針對 HASH 或 ROUND_ROBIN 散發資料表 (資料會平均分佈) 來達成。</span><span class="sxs-lookup"><span data-stu-id="98961-204">The maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where the spread of the data is even.</span></span> <span data-ttu-id="98961-205">如果交易是以扭曲方式將資料寫入散發，則可能會在到達交易大小上限之前就先達到限制。</span><span class="sxs-lookup"><span data-stu-id="98961-205">If the transaction is writing data in a skewed fashion to the distributions then the limit is likely to be reached prior to the maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="98961-206">交易狀態</span><span class="sxs-lookup"><span data-stu-id="98961-206">Transaction state</span></span>
<span data-ttu-id="98961-207">SQL 資料倉儲會使用 XACT_STATE() 函式 (採用值 -2) 來報告失敗的交易。</span><span class="sxs-lookup"><span data-stu-id="98961-207">SQL Data Warehouse uses the XACT_STATE() function to report a failed transaction using the value -2.</span></span> <span data-ttu-id="98961-208">這表示交易已失敗並標示為僅可復原</span><span class="sxs-lookup"><span data-stu-id="98961-208">This means that the transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="98961-209">XACT_STATE 函式使用 -2 表示失敗的交易，以代表 SQL Server 中不同的行為。</span><span class="sxs-lookup"><span data-stu-id="98961-209">The use of -2 by the XACT_STATE function to denote a failed transaction represents different behavior to SQL Server.</span></span> <span data-ttu-id="98961-210">SQL Server 使用值 -1 來代表無法認可的交易。</span><span class="sxs-lookup"><span data-stu-id="98961-210">SQL Server uses the value -1 to represent an un-committable transaction.</span></span> <span data-ttu-id="98961-211">SQL Server 可以容忍交易內的某些錯誤，而不需將其標示為無法認可。</span><span class="sxs-lookup"><span data-stu-id="98961-211">SQL Server can tolerate some errors inside a transaction without it having to be marked as un-committable.</span></span> <span data-ttu-id="98961-212">例如， `SELECT 1/0` 會導致錯誤，但不會強制交易進入無法認可的狀態。</span><span class="sxs-lookup"><span data-stu-id="98961-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="98961-213">SQL Server 也允許讀取無法認可的交易。</span><span class="sxs-lookup"><span data-stu-id="98961-213">SQL Server also permits reads in the un-committable transaction.</span></span> <span data-ttu-id="98961-214">不過，SQL 資料倉儲不會讓您這樣做作。</span><span class="sxs-lookup"><span data-stu-id="98961-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="98961-215">如果 SQL 資料倉儲交易內部發生錯誤，就會自動進入 -2 狀態，而且您不能進行任何進一步的 Select 陳述式，直到陳述式回復為止。</span><span class="sxs-lookup"><span data-stu-id="98961-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter the -2 state and you will not be able to make any further select statements until the statement has been rolled back.</span></span> <span data-ttu-id="98961-216">因此，檢查您的應用程式程式碼是否使用 XACT_STATE() 就相當重要，因為您可能需要修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="98961-216">It is therefore important to check that your application code to see if it uses  XACT_STATE() as you may need to make code modifications.</span></span>
> 
> 

<span data-ttu-id="98961-217">比方說，在 SQL Server 中，您可能會看到類似這樣的交易：</span><span class="sxs-lookup"><span data-stu-id="98961-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

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

<span data-ttu-id="98961-218">如果您將您的程式碼保持原狀 (如上方所示)，您將會收到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="98961-218">If you leave your code as it is above then you will get the following error message:</span></span>

<span data-ttu-id="98961-219">Msg 111233, Level 16, State 1, Line 1 111233;目前的交易已經中止，並已回復任何暫止的變更。</span><span class="sxs-lookup"><span data-stu-id="98961-219">Msg 111233, Level 16, State 1, Line 1 111233;The current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="98961-220">原因︰處於僅限復原狀態中的交易，未在使用 DDL、DML 或 SELECT 陳述式之前明確復原。</span><span class="sxs-lookup"><span data-stu-id="98961-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="98961-221">您也不會收到 ERROR_* 函式的輸出。</span><span class="sxs-lookup"><span data-stu-id="98961-221">You will also not get the output of the ERROR_* functions.</span></span>

<span data-ttu-id="98961-222">SQL 資料倉儲中的程式碼需要稍微變更：</span><span class="sxs-lookup"><span data-stu-id="98961-222">In SQL Data Warehouse the code needs to be slightly altered:</span></span>

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

<span data-ttu-id="98961-223">目前已觀察到預期的行為。</span><span class="sxs-lookup"><span data-stu-id="98961-223">The expected behavior is now observed.</span></span> <span data-ttu-id="98961-224">已管理交易中的錯誤，且 ERROR_* 函式提供了預期的值。</span><span class="sxs-lookup"><span data-stu-id="98961-224">The error in the transaction is managed and the ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="98961-225">唯一的變更就是交易的 `ROLLBACK` 必須在讀取 `CATCH` 區塊中的錯誤資訊之前發生。</span><span class="sxs-lookup"><span data-stu-id="98961-225">All that has changed is that the `ROLLBACK` of the transaction had to happen before the read of the error information in the `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="98961-226">Error_Line() 函式</span><span class="sxs-lookup"><span data-stu-id="98961-226">Error_Line() function</span></span>
<span data-ttu-id="98961-227">另外值得注意的是，SQL 資料倉儲不會實作或支援 ERROR_LINE() 函式。</span><span class="sxs-lookup"><span data-stu-id="98961-227">It is also worth noting that SQL Data Warehouse does not implement or support the ERROR_LINE() function.</span></span> <span data-ttu-id="98961-228">如果您的程式碼中有此函式，您必須將它移除才能符合 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="98961-228">If you have this in your code you will need to remove it to be compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="98961-229">在程式碼中使用查詢標籤，而不需實作對等的功能。</span><span class="sxs-lookup"><span data-stu-id="98961-229">Use query labels in your code instead to implement equivalent functionality.</span></span> <span data-ttu-id="98961-230">如需這項功能的詳細資料，請參閱 [LABEL][LABEL] 一文。</span><span class="sxs-lookup"><span data-stu-id="98961-230">Please refer to the [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="98961-231">使用 THROW 和 RAISERROR</span><span class="sxs-lookup"><span data-stu-id="98961-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="98961-232">THROW 是在 SQL 資料倉儲中引發例外狀況的新式作法，但也支援 RAISERROR。</span><span class="sxs-lookup"><span data-stu-id="98961-232">THROW is the more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="98961-233">不過，有一些值得注意的差異。</span><span class="sxs-lookup"><span data-stu-id="98961-233">There are a few differences that are worth paying attention to however.</span></span>

* <span data-ttu-id="98961-234">對於 THROW，使用者定義的錯誤訊息數目不能在 100,000 - 150,000 範圍內</span><span class="sxs-lookup"><span data-stu-id="98961-234">User defined error messages numbers cannot be in the 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="98961-235">RAISERROR 錯誤訊息固定為 50,000</span><span class="sxs-lookup"><span data-stu-id="98961-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="98961-236">不支援使用 sys.messages</span><span class="sxs-lookup"><span data-stu-id="98961-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="98961-237">限制</span><span class="sxs-lookup"><span data-stu-id="98961-237">Limitiations</span></span>
<span data-ttu-id="98961-238">SQL 資料倉儲有一些與交易相關的其他限制。</span><span class="sxs-lookup"><span data-stu-id="98961-238">SQL Data Warehouse does have a few other restrictions that relate to transactions.</span></span>

<span data-ttu-id="98961-239">如下所示：</span><span class="sxs-lookup"><span data-stu-id="98961-239">They are as follows:</span></span>

* <span data-ttu-id="98961-240">沒有分散式交易</span><span class="sxs-lookup"><span data-stu-id="98961-240">No distributed transactions</span></span>
* <span data-ttu-id="98961-241">不允許巢狀交易</span><span class="sxs-lookup"><span data-stu-id="98961-241">No nested transactions permitted</span></span>
* <span data-ttu-id="98961-242">不允許儲存點</span><span class="sxs-lookup"><span data-stu-id="98961-242">No save points allowed</span></span>
* <span data-ttu-id="98961-243">沒有具名的交易</span><span class="sxs-lookup"><span data-stu-id="98961-243">No named transactions</span></span>
* <span data-ttu-id="98961-244">沒有標示的交易</span><span class="sxs-lookup"><span data-stu-id="98961-244">No marked transactions</span></span>
* <span data-ttu-id="98961-245">使用者定義的交易內部不支援 DDL，例如 `CREATE TABLE`</span><span class="sxs-lookup"><span data-stu-id="98961-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="98961-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98961-246">Next steps</span></span>
<span data-ttu-id="98961-247">若要深入了解最佳化交易，請參閱[交易的最佳做法][Transactions best practices]。</span><span class="sxs-lookup"><span data-stu-id="98961-247">To learn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="98961-248">若要深入了解其他 SQL 資料倉儲最佳作法，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse best practices]。</span><span class="sxs-lookup"><span data-stu-id="98961-248">To learn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
