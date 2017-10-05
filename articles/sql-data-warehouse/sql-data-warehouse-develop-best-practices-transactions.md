---
title: "最佳化 SQL 資料倉儲的交易 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中撰寫有效率交易更新的最佳作法指引"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="78db9-103">最佳化 SQL 資料倉儲的交易</span><span class="sxs-lookup"><span data-stu-id="78db9-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="78db9-104">本文說明如何將您的交易程式碼效能最佳化，同時將長時間回復的風險降至最低。</span><span class="sxs-lookup"><span data-stu-id="78db9-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="78db9-105">交易和記錄</span><span class="sxs-lookup"><span data-stu-id="78db9-105">Transactions and logging</span></span>
<span data-ttu-id="78db9-106">交易是關聯式資料庫引擎的重要元件。</span><span class="sxs-lookup"><span data-stu-id="78db9-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="78db9-107">SQL 資料倉儲會在資料修改期間使用交易。</span><span class="sxs-lookup"><span data-stu-id="78db9-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="78db9-108">這些交易可以是明確或隱含的。</span><span class="sxs-lookup"><span data-stu-id="78db9-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="78db9-109">單一 `INSERT`、`UPDATE` 和 `DELETE` 陳述式都是隱含交易的範例。</span><span class="sxs-lookup"><span data-stu-id="78db9-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="78db9-110">明確交易由使用 `BEGIN TRAN`、`COMMIT TRAN` 或 `ROLLBACK TRAN` 的開發人員明確撰寫，且通常用於多個修改陳述式必須一起連結為單一不可部分完成單位的時候。</span><span class="sxs-lookup"><span data-stu-id="78db9-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="78db9-111">Azure SQL 資料倉儲認可使用交易記錄檔之資料庫的變更。</span><span class="sxs-lookup"><span data-stu-id="78db9-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="78db9-112">每個散發套件都有自己的交易記錄檔。</span><span class="sxs-lookup"><span data-stu-id="78db9-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="78db9-113">交易記錄檔寫入是自動的。</span><span class="sxs-lookup"><span data-stu-id="78db9-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="78db9-114">不需要任何組態。</span><span class="sxs-lookup"><span data-stu-id="78db9-114">There is no configuration required.</span></span> <span data-ttu-id="78db9-115">不過，儘管這個程序可保證寫入，但是它會在系統中引進額外負荷。</span><span class="sxs-lookup"><span data-stu-id="78db9-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="78db9-116">您可以藉由撰寫交易式的有效程式碼，將影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="78db9-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="78db9-117">交易式的有效程式碼大致分為兩個類別。</span><span class="sxs-lookup"><span data-stu-id="78db9-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="78db9-118">盡可能使用最低限度的記錄建構</span><span class="sxs-lookup"><span data-stu-id="78db9-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="78db9-119">使用已設定範圍的批次處理資料，以避免單數的長時間執行交易</span><span class="sxs-lookup"><span data-stu-id="78db9-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="78db9-120">採用分割切換模式進行指定分割的大規模修改</span><span class="sxs-lookup"><span data-stu-id="78db9-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="78db9-121">最低限度 vs. 完整記錄</span><span class="sxs-lookup"><span data-stu-id="78db9-121">Minimal vs. full logging</span></span>
<span data-ttu-id="78db9-122">完整記錄作業使用交易記錄檔追蹤每個資料列的變更，最低限度記錄作業不一樣，它只會追蹤程度配置與中繼資料變更。</span><span class="sxs-lookup"><span data-stu-id="78db9-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="78db9-123">因此，最低限度記錄只會記錄在失敗事件或明確要求 (`ROLLBACK TRAN`) 中回復交易所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="78db9-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="78db9-124">因為在交易記錄檔中追蹤較少的資訊，最低限度記錄作業的執行效果優於大小類似的完整記錄作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="78db9-125">此外，因為交易記錄檔中較少寫入，所以產生更少量的記錄檔資料，因此有更多有效的 I/O。</span><span class="sxs-lookup"><span data-stu-id="78db9-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="78db9-126">交易安全限制僅適用於完整記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="78db9-127">最低限度記錄作業可以加入明確交易。</span><span class="sxs-lookup"><span data-stu-id="78db9-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="78db9-128">配置結構中的所有變更都會受到追蹤，就可以回復最低限度記錄作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="78db9-129">請務必了解變更為「最低限度」記錄，而不是未記錄。</span><span class="sxs-lookup"><span data-stu-id="78db9-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="78db9-130">最低限度記錄作業</span><span class="sxs-lookup"><span data-stu-id="78db9-130">Minimally logged operations</span></span>
<span data-ttu-id="78db9-131">下列作業也能以最低限度記錄︰</span><span class="sxs-lookup"><span data-stu-id="78db9-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="78db9-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="78db9-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="78db9-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="78db9-133">INSERT..SELECT</span></span>
* <span data-ttu-id="78db9-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="78db9-134">CREATE INDEX</span></span>
* <span data-ttu-id="78db9-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="78db9-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="78db9-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="78db9-136">DROP INDEX</span></span>
* <span data-ttu-id="78db9-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="78db9-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="78db9-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="78db9-138">DROP TABLE</span></span>
* <span data-ttu-id="78db9-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="78db9-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="78db9-140">內部資料移動作業 (例如 `BROADCAST` 和 `SHUFFLE`) 不受交易安全限制影響。</span><span class="sxs-lookup"><span data-stu-id="78db9-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="78db9-141">大量載入的最低限度記錄</span><span class="sxs-lookup"><span data-stu-id="78db9-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="78db9-142">`CTAS` 和 `INSERT...SELECT` 都是大量載入作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="78db9-143">不過，兩者都會受到目標資料表定義的影響，取決於載入案例。</span><span class="sxs-lookup"><span data-stu-id="78db9-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="78db9-144">以下是說明大量作業是否為完全或最低限度記錄的資料表︰</span><span class="sxs-lookup"><span data-stu-id="78db9-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="78db9-145">主要索引</span><span class="sxs-lookup"><span data-stu-id="78db9-145">Primary Index</span></span> | <span data-ttu-id="78db9-146">載入案例</span><span class="sxs-lookup"><span data-stu-id="78db9-146">Load Scenario</span></span> | <span data-ttu-id="78db9-147">記錄模式</span><span class="sxs-lookup"><span data-stu-id="78db9-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78db9-148">堆積</span><span class="sxs-lookup"><span data-stu-id="78db9-148">Heap</span></span> |<span data-ttu-id="78db9-149">任意</span><span class="sxs-lookup"><span data-stu-id="78db9-149">Any</span></span> |<span data-ttu-id="78db9-150">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="78db9-150">**Minimal**</span></span> |
| <span data-ttu-id="78db9-151">叢集索引</span><span class="sxs-lookup"><span data-stu-id="78db9-151">Clustered Index</span></span> |<span data-ttu-id="78db9-152">空的目標資料表</span><span class="sxs-lookup"><span data-stu-id="78db9-152">Empty target table</span></span> |<span data-ttu-id="78db9-153">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="78db9-153">**Minimal**</span></span> |
| <span data-ttu-id="78db9-154">叢集索引</span><span class="sxs-lookup"><span data-stu-id="78db9-154">Clustered Index</span></span> |<span data-ttu-id="78db9-155">載入的資料列不會與目標中的現有頁面重疊</span><span class="sxs-lookup"><span data-stu-id="78db9-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="78db9-156">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="78db9-156">**Minimal**</span></span> |
| <span data-ttu-id="78db9-157">叢集索引</span><span class="sxs-lookup"><span data-stu-id="78db9-157">Clustered Index</span></span> |<span data-ttu-id="78db9-158">載入的資料列會與目標中的現有頁面重疊</span><span class="sxs-lookup"><span data-stu-id="78db9-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="78db9-159">完整</span><span class="sxs-lookup"><span data-stu-id="78db9-159">Full</span></span> |
| <span data-ttu-id="78db9-160">叢集資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="78db9-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="78db9-161">每個與分割對齊的散發套件之批次大小 >= 102,400</span><span class="sxs-lookup"><span data-stu-id="78db9-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="78db9-162">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="78db9-162">**Minimal**</span></span> |
| <span data-ttu-id="78db9-163">叢集資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="78db9-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="78db9-164">批次大小 < 每個與分割對齊的散發套件 102,400</span><span class="sxs-lookup"><span data-stu-id="78db9-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="78db9-165">完整</span><span class="sxs-lookup"><span data-stu-id="78db9-165">Full</span></span> |

<span data-ttu-id="78db9-166">值得注意的是任何更新次要或非叢集索引的寫入一定是完整記錄作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78db9-167">SQL 資料倉儲有 60 個散發套件。</span><span class="sxs-lookup"><span data-stu-id="78db9-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="78db9-168">因此，假設所有資料列平均散發，並位於單一分割中，您的批次必須包含 6,144,000 個資料列或更大刑，才能在寫入叢集資料行存放區索引時進行最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="78db9-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="78db9-169">如果資料表已分割，且插入的資料列跨越分割界限，每個假設平均資料散發的分割界限將需要 6,144,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="78db9-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="78db9-170">每個散發套件中的每個分割必須獨立超過 102,400 的資料列臨界值，才能讓插入以最低限度記錄在散發套件中。</span><span class="sxs-lookup"><span data-stu-id="78db9-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="78db9-171">利用叢集索引將資料載入非空白資料表中，通常會混合包含完整記錄和最低限度記錄資料列。</span><span class="sxs-lookup"><span data-stu-id="78db9-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="78db9-172">叢集索引是頁面的平衡樹狀結構 (b 型樹狀目錄)。</span><span class="sxs-lookup"><span data-stu-id="78db9-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="78db9-173">如果寫入的頁面中已包含另一個交易的資料列，則這些寫入將會完整記錄。</span><span class="sxs-lookup"><span data-stu-id="78db9-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="78db9-174">不過，如果頁面是空的，則該頁面的寫入將會以最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="78db9-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="78db9-175">最佳化刪除</span><span class="sxs-lookup"><span data-stu-id="78db9-175">Optimizing deletes</span></span>
<span data-ttu-id="78db9-176">`DELETE` 是完整記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="78db9-177">如果您需要刪除資料表或分割中的大量資料，比較理想的做法通常是 `SELECT` 您想要保留的資料，這可以最低限度記錄作業來執行。</span><span class="sxs-lookup"><span data-stu-id="78db9-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="78db9-178">若要達成此目的，請使用 [CTAS][CTAS] 建立新的資料表。</span><span class="sxs-lookup"><span data-stu-id="78db9-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="78db9-179">建立之後，請使用 [RENAME][RENAME] 來交換您的舊資料表與新建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="78db9-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="78db9-180">最佳化更新</span><span class="sxs-lookup"><span data-stu-id="78db9-180">Optimizing updates</span></span>
<span data-ttu-id="78db9-181">`UPDATE` 是完整記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="78db9-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="78db9-182">如果您需要更新資料表或分割中的大量資料列，通常更有效率的方法是使用最低限度記錄作業 (例如 [CTAS][CTAS]) 來達成此目的。</span><span class="sxs-lookup"><span data-stu-id="78db9-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="78db9-183">在下列範例中，完整的資料表更新已轉換成 `CTAS` ，以便進行最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="78db9-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="78db9-184">在此情況下，我們反而要將折扣金額新增到資料表中的銷售額︰</span><span class="sxs-lookup"><span data-stu-id="78db9-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="78db9-185">使用 SQL 資料倉儲工作負載管理功能有助於重新建立大型資料表。</span><span class="sxs-lookup"><span data-stu-id="78db9-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="78db9-186">如需詳細資料，請參閱[並行][concurrency]一文中的工作負載管理一節。</span><span class="sxs-lookup"><span data-stu-id="78db9-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="78db9-187">利用分割切換進行最佳化</span><span class="sxs-lookup"><span data-stu-id="78db9-187">Optimizing with partition switching</span></span>
<span data-ttu-id="78db9-188">面臨[資料表分割][table partition]內部的大規模修改時，分割切換模式相當實用。</span><span class="sxs-lookup"><span data-stu-id="78db9-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="78db9-189">如果大量修改資料而且跨越多個分割，則只逐一查看分割也可達到相同的結果。</span><span class="sxs-lookup"><span data-stu-id="78db9-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="78db9-190">執行分割切換的步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="78db9-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="78db9-191">建立空白分割</span><span class="sxs-lookup"><span data-stu-id="78db9-191">Create an empty out partition</span></span>
2. <span data-ttu-id="78db9-192">執行「更新」做為 CTAS</span><span class="sxs-lookup"><span data-stu-id="78db9-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="78db9-193">將現有資料切換出至外資料表</span><span class="sxs-lookup"><span data-stu-id="78db9-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="78db9-194">切換入新資料</span><span class="sxs-lookup"><span data-stu-id="78db9-194">Switch in the new data</span></span>
5. <span data-ttu-id="78db9-195">清除資料</span><span class="sxs-lookup"><span data-stu-id="78db9-195">Clean up the data</span></span>

<span data-ttu-id="78db9-196">不過，若要協助識別要切換的分割，我們必須先建置如下的協助程式程序。</span><span class="sxs-lookup"><span data-stu-id="78db9-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="78db9-197">此程序會將程式碼的重複使用最大化，並讓分割切換範例更加精簡。</span><span class="sxs-lookup"><span data-stu-id="78db9-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="78db9-198">下列程式碼示範上述達到完整分割切換例行工作的五個步驟。</span><span class="sxs-lookup"><span data-stu-id="78db9-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update the data in the select portion of the CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="78db9-199">小型批次的最低限度記錄</span><span class="sxs-lookup"><span data-stu-id="78db9-199">Minimize logging with small batches</span></span>
<span data-ttu-id="78db9-200">針對大型資料修改作業，適合將作業分成區塊或批次來指定工作單位的範圍。</span><span class="sxs-lookup"><span data-stu-id="78db9-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="78db9-201">以下提供實用的範例。</span><span class="sxs-lookup"><span data-stu-id="78db9-201">A working example is provided below.</span></span> <span data-ttu-id="78db9-202">批次大小設為簡單數字來醒目提示此技術。</span><span class="sxs-lookup"><span data-stu-id="78db9-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="78db9-203">事實上，批次大小明顯大很多。</span><span class="sxs-lookup"><span data-stu-id="78db9-203">In reality the batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="78db9-204">暫停和調整指引</span><span class="sxs-lookup"><span data-stu-id="78db9-204">Pause and scaling guidance</span></span>
<span data-ttu-id="78db9-205">Azure SQL 資料倉儲可讓您暫停、繼續及調整需要的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="78db9-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="78db9-206">當您暫停或調整您的 SQL 資料倉儲，請務必了解任何進行中的交易都會立即終止；導致所有開放的交易都會回復。</span><span class="sxs-lookup"><span data-stu-id="78db9-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="78db9-207">如果您的工作負載在暫停或調整作業之前發出長時間執行且不完整的資料修改，則這項工作必須復原。</span><span class="sxs-lookup"><span data-stu-id="78db9-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="78db9-208">這可能會影響暫停或調整 Azure SQL 資料倉儲資料庫的時間。</span><span class="sxs-lookup"><span data-stu-id="78db9-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="78db9-209">`UPDATE` 和 `DELETE` 都是完整記錄作業，因此這些復原/重做作業花費的時間可能會比對等的最低限度記錄作業長很多。</span><span class="sxs-lookup"><span data-stu-id="78db9-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="78db9-210">最佳案例是在暫停或調整 SQL 資料倉儲之前，讓進行中的資料修改交易完成。</span><span class="sxs-lookup"><span data-stu-id="78db9-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="78db9-211">但是，這不一定都可行。</span><span class="sxs-lookup"><span data-stu-id="78db9-211">However, this may not always be practical.</span></span> <span data-ttu-id="78db9-212">若要降低長時間回復的風險，請考慮下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="78db9-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="78db9-213">使用 [CTAS][CTAS] 重新撰寫長時間執行的作業</span><span class="sxs-lookup"><span data-stu-id="78db9-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="78db9-214">將作業分成多個區塊；在資料列子集上運作</span><span class="sxs-lookup"><span data-stu-id="78db9-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="78db9-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78db9-215">Next steps</span></span>
<span data-ttu-id="78db9-216">若要進一步了解隔離等級和交易限制，請參閱 [SQL 資料倉儲中的交易][Transactions in SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="78db9-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="78db9-217">如需其他最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="78db9-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

