---
title: "SQL 資料倉儲的 aaaOptimizing 交易 |Microsoft 文件"
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
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="d053a-103">最佳化 SQL 資料倉儲的交易</span><span class="sxs-lookup"><span data-stu-id="d053a-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="d053a-104">本文說明如何 toooptimize hello 的交易式的程式碼的效能，同時長回復的風險降到最低。</span><span class="sxs-lookup"><span data-stu-id="d053a-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="d053a-105">交易和記錄</span><span class="sxs-lookup"><span data-stu-id="d053a-105">Transactions and logging</span></span>
<span data-ttu-id="d053a-106">交易是關聯式資料庫引擎的重要元件。</span><span class="sxs-lookup"><span data-stu-id="d053a-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="d053a-107">SQL 資料倉儲會在資料修改期間使用交易。</span><span class="sxs-lookup"><span data-stu-id="d053a-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="d053a-108">這些交易可以是明確或隱含的。</span><span class="sxs-lookup"><span data-stu-id="d053a-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="d053a-109">單一 `INSERT`、`UPDATE` 和 `DELETE` 陳述式都是隱含交易的範例。</span><span class="sxs-lookup"><span data-stu-id="d053a-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="d053a-110">外顯交易由開發人員使用明確撰寫`BEGIN TRAN`，`COMMIT TRAN`或`ROLLBACK TRAN`和通常用在多個修改陳述式需要 toobe 中單一不可部分完成單位連結在一起。</span><span class="sxs-lookup"><span data-stu-id="d053a-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="d053a-111">Azure SQL 資料倉儲認可使用交易記錄的變更 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d053a-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="d053a-112">每個散發套件都有自己的交易記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d053a-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="d053a-113">交易記錄檔寫入是自動的。</span><span class="sxs-lookup"><span data-stu-id="d053a-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="d053a-114">不需要任何組態。</span><span class="sxs-lookup"><span data-stu-id="d053a-114">There is no configuration required.</span></span> <span data-ttu-id="d053a-115">不過，儘管這個程序可確保 hello 寫入它會導致額外負荷 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="d053a-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="d053a-116">您可以藉由撰寫交易式的有效程式碼，將影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="d053a-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="d053a-117">交易式的有效程式碼大致分為兩個類別。</span><span class="sxs-lookup"><span data-stu-id="d053a-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="d053a-118">盡可能使用最低限度的記錄建構</span><span class="sxs-lookup"><span data-stu-id="d053a-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="d053a-119">使用已設定領域的批次 tooavoid 單數長時間執行交易處理資料</span><span class="sxs-lookup"><span data-stu-id="d053a-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="d053a-120">採用的資料分割切換的大型修改 tooa 給定資料分割模式</span><span class="sxs-lookup"><span data-stu-id="d053a-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="d053a-121">最低限度 vs. 完整記錄</span><span class="sxs-lookup"><span data-stu-id="d053a-121">Minimal vs. full logging</span></span>
<span data-ttu-id="d053a-122">與完整記錄作業，使用 hello 交易記錄檔 tookeep 追蹤的每個資料列變更，不同的是最低限度記錄的作業追蹤的範圍配置與僅限中繼資料變更。</span><span class="sxs-lookup"><span data-stu-id="d053a-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="d053a-123">因此，最低限度記錄包含僅記錄 hello 資訊是 hello 事件中發生失敗或明確要求的必要的 toorollback hello 交易 (`ROLLBACK TRAN`)。</span><span class="sxs-lookup"><span data-stu-id="d053a-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="d053a-124">因為較 hello 交易記錄中追蹤資訊，最低限度記錄的作業執行效能高於大小類似的完整記錄作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="d053a-125">此外，因為較少寫入 hello 交易記錄檔，就會產生較少的記錄資料，因此多個 I/O 有效率。</span><span class="sxs-lookup"><span data-stu-id="d053a-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="d053a-126">hello 交易安全限制僅適用於 toofully 記錄作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="d053a-127">最低限度記錄作業可以加入明確交易。</span><span class="sxs-lookup"><span data-stu-id="d053a-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="d053a-128">追蹤配置結構中的所有變更，則它是可能 tooroll 後使用最低限度記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="d053a-129">很重要的 hello 變更 「 最低限度"toounderstand 記錄它不是未記錄。</span><span class="sxs-lookup"><span data-stu-id="d053a-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="d053a-130">最低限度記錄作業</span><span class="sxs-lookup"><span data-stu-id="d053a-130">Minimally logged operations</span></span>
<span data-ttu-id="d053a-131">hello 下列作業都能使用最低限度記錄：</span><span class="sxs-lookup"><span data-stu-id="d053a-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="d053a-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="d053a-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="d053a-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="d053a-133">INSERT..SELECT</span></span>
* <span data-ttu-id="d053a-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="d053a-134">CREATE INDEX</span></span>
* <span data-ttu-id="d053a-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="d053a-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="d053a-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="d053a-136">DROP INDEX</span></span>
* <span data-ttu-id="d053a-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="d053a-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="d053a-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="d053a-138">DROP TABLE</span></span>
* <span data-ttu-id="d053a-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="d053a-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="d053a-140">內部資料移動作業 (例如`BROADCAST`和`SHUFFLE`) 不會受到 hello 交易安全性限制。</span><span class="sxs-lookup"><span data-stu-id="d053a-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="d053a-141">大量載入的最低限度記錄</span><span class="sxs-lookup"><span data-stu-id="d053a-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="d053a-142">`CTAS` 和 `INSERT...SELECT` 都是大量載入作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="d053a-143">不過，會同時受到 hello 目標資料表定義與 hello 負載案例而定。</span><span class="sxs-lookup"><span data-stu-id="d053a-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="d053a-144">以下是說明大量作業是否為完全或最低限度記錄的資料表︰</span><span class="sxs-lookup"><span data-stu-id="d053a-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="d053a-145">主要索引</span><span class="sxs-lookup"><span data-stu-id="d053a-145">Primary Index</span></span> | <span data-ttu-id="d053a-146">載入案例</span><span class="sxs-lookup"><span data-stu-id="d053a-146">Load Scenario</span></span> | <span data-ttu-id="d053a-147">記錄模式</span><span class="sxs-lookup"><span data-stu-id="d053a-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d053a-148">堆積</span><span class="sxs-lookup"><span data-stu-id="d053a-148">Heap</span></span> |<span data-ttu-id="d053a-149">任意</span><span class="sxs-lookup"><span data-stu-id="d053a-149">Any</span></span> |<span data-ttu-id="d053a-150">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="d053a-150">**Minimal**</span></span> |
| <span data-ttu-id="d053a-151">叢集索引</span><span class="sxs-lookup"><span data-stu-id="d053a-151">Clustered Index</span></span> |<span data-ttu-id="d053a-152">空的目標資料表</span><span class="sxs-lookup"><span data-stu-id="d053a-152">Empty target table</span></span> |<span data-ttu-id="d053a-153">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="d053a-153">**Minimal**</span></span> |
| <span data-ttu-id="d053a-154">叢集索引</span><span class="sxs-lookup"><span data-stu-id="d053a-154">Clustered Index</span></span> |<span data-ttu-id="d053a-155">載入的資料列不會與目標中的現有頁面重疊</span><span class="sxs-lookup"><span data-stu-id="d053a-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="d053a-156">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="d053a-156">**Minimal**</span></span> |
| <span data-ttu-id="d053a-157">叢集索引</span><span class="sxs-lookup"><span data-stu-id="d053a-157">Clustered Index</span></span> |<span data-ttu-id="d053a-158">載入的資料列會與目標中的現有頁面重疊</span><span class="sxs-lookup"><span data-stu-id="d053a-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="d053a-159">完整</span><span class="sxs-lookup"><span data-stu-id="d053a-159">Full</span></span> |
| <span data-ttu-id="d053a-160">叢集資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="d053a-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="d053a-161">每個與分割對齊的散發套件之批次大小 >= 102,400</span><span class="sxs-lookup"><span data-stu-id="d053a-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="d053a-162">**最低限度**</span><span class="sxs-lookup"><span data-stu-id="d053a-162">**Minimal**</span></span> |
| <span data-ttu-id="d053a-163">叢集資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="d053a-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="d053a-164">批次大小 < 每個與分割對齊的散發套件 102,400</span><span class="sxs-lookup"><span data-stu-id="d053a-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="d053a-165">完整</span><span class="sxs-lookup"><span data-stu-id="d053a-165">Full</span></span> |

<span data-ttu-id="d053a-166">值得注意的是任何寫入 tooupdate 次要或非叢集索引一律會完整記錄作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d053a-167">SQL 資料倉儲有 60 個散發套件。</span><span class="sxs-lookup"><span data-stu-id="d053a-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="d053a-168">因此，假設所有資料列平均分配，登陸在單一磁碟分割，您的批次必須 toocontain 6,144,000 資料列或更大的 toobe 最低限度記錄的寫入 tooa 叢集資料行存放區索引時。</span><span class="sxs-lookup"><span data-stu-id="d053a-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="d053a-169">Hello 資料表已分割，而且正在插入資料列的 hello 跨越資料分割界限，如果您將需要每個資料分割界限假設平均資料散發 6,144,000 資料列。</span><span class="sxs-lookup"><span data-stu-id="d053a-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="d053a-170">每個發佈中的每個資料分割必須獨立超過 hello 102,400 資料列臨界值 hello 插入 toobe hello 發佈到使用最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="d053a-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="d053a-171">利用叢集索引將資料載入非空白資料表中，通常會混合包含完整記錄和最低限度記錄資料列。</span><span class="sxs-lookup"><span data-stu-id="d053a-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="d053a-172">叢集索引是頁面的平衡樹狀結構 (b 型樹狀目錄)。</span><span class="sxs-lookup"><span data-stu-id="d053a-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="d053a-173">如果 hello 頁面寫入 tooalready 包含另一個交易的資料列，然後這些寫入將會完整記錄。</span><span class="sxs-lookup"><span data-stu-id="d053a-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="d053a-174">不過，如果是空的 hello 頁面然後 hello 寫入 toothat 頁面將會進行最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="d053a-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="d053a-175">最佳化刪除</span><span class="sxs-lookup"><span data-stu-id="d053a-175">Optimizing deletes</span></span>
<span data-ttu-id="d053a-176">`DELETE` 是完整記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="d053a-177">如果您需要 toodelete 大量資料表或資料分割中的資料時，通常會比較合理太`SELECT`hello 資料想 tookeep，可以執行以最低限度記錄作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="d053a-178">tooaccomplish，建立新的資料表與[CTAS][CTAS]。</span><span class="sxs-lookup"><span data-stu-id="d053a-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="d053a-179">建立之後，使用[重新命名][ RENAME] tooswap 移出您舊的資料表與 hello 新建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="d053a-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
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

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="d053a-180">最佳化更新</span><span class="sxs-lookup"><span data-stu-id="d053a-180">Optimizing updates</span></span>
<span data-ttu-id="d053a-181">`UPDATE` 是完整記錄的作業。</span><span class="sxs-lookup"><span data-stu-id="d053a-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="d053a-182">如果您需要 tooupdate 大量的資料表中的資料列或資料分割通常很效率 toouse 最低限度記錄的作業，例如[CTAS] [ CTAS] toodo 如此。</span><span class="sxs-lookup"><span data-stu-id="d053a-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="d053a-183">在 hello 下例完整資料表更新已經過轉換的 tooa `CTAS` ，方便您最低限度記錄。</span><span class="sxs-lookup"><span data-stu-id="d053a-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="d053a-184">在此情況下我們 retrospectively 新增折扣量 toohello 銷售 hello 資料表中：</span><span class="sxs-lookup"><span data-stu-id="d053a-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
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

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="d053a-185">使用 SQL 資料倉儲工作負載管理功能有助於重新建立大型資料表。</span><span class="sxs-lookup"><span data-stu-id="d053a-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="d053a-186">如需詳細資訊，請參閱 toohello 工作負載管理 > 一節中 hello[並行][ concurrency]發行項。</span><span class="sxs-lookup"><span data-stu-id="d053a-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="d053a-187">利用分割切換進行最佳化</span><span class="sxs-lookup"><span data-stu-id="d053a-187">Optimizing with partition switching</span></span>
<span data-ttu-id="d053a-188">面臨[資料表分割][table partition]內部的大規模修改時，分割切換模式相當實用。</span><span class="sxs-lookup"><span data-stu-id="d053a-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="d053a-189">如果 hello 資料修改會很可觀，而且跨越多個資料分割，然後只需反覆 hello 分割區會達到 hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="d053a-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="d053a-190">hello 步驟 tooperform 分割區切換如下所示：</span><span class="sxs-lookup"><span data-stu-id="d053a-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="d053a-191">建立空白分割</span><span class="sxs-lookup"><span data-stu-id="d053a-191">Create an empty out partition</span></span>
2. <span data-ttu-id="d053a-192">執行 CTAS hello 'update'</span><span class="sxs-lookup"><span data-stu-id="d053a-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="d053a-193">切換移出 hello 現有資料 toohello 移出資料表</span><span class="sxs-lookup"><span data-stu-id="d053a-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="d053a-194">切換移入 hello 新的資料</span><span class="sxs-lookup"><span data-stu-id="d053a-194">Switch in hello new data</span></span>
5. <span data-ttu-id="d053a-195">Hello 資料進行清除</span><span class="sxs-lookup"><span data-stu-id="d053a-195">Clean up hello data</span></span>

<span data-ttu-id="d053a-196">不過，toohelp 識別 hello 分割 tooswitch 我們首先需要 toobuild 的協助程式程序，例如其中一個 hello 下方。</span><span class="sxs-lookup"><span data-stu-id="d053a-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="d053a-197">此程序最大化程式碼重複使用，並保留 hello 資料分割切換更精簡的範例。</span><span class="sxs-lookup"><span data-stu-id="d053a-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="d053a-198">hello 的下列程式碼會示範 hello 五個步驟上述 tooachieve 完整的資料分割切換的常式。</span><span class="sxs-lookup"><span data-stu-id="d053a-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
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

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
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

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="d053a-199">小型批次的最低限度記錄</span><span class="sxs-lookup"><span data-stu-id="d053a-199">Minimize logging with small batches</span></span>
<span data-ttu-id="d053a-200">對於大型資料修改作業，可能更有意義 toodivide hello 作業成區塊或批次 tooscope hello 單位的工作。</span><span class="sxs-lookup"><span data-stu-id="d053a-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="d053a-201">以下提供實用的範例。</span><span class="sxs-lookup"><span data-stu-id="d053a-201">A working example is provided below.</span></span> <span data-ttu-id="d053a-202">已設定 tooa 一般數字 toohighlight hello 技術 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="d053a-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="d053a-203">事實上 hello 批次大小會變得很大。</span><span class="sxs-lookup"><span data-stu-id="d053a-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="d053a-204">暫停和調整指引</span><span class="sxs-lookup"><span data-stu-id="d053a-204">Pause and scaling guidance</span></span>
<span data-ttu-id="d053a-205">Azure SQL 資料倉儲可讓您暫停、繼續及調整需要的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="d053a-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="d053a-206">您暫停或調整您的 SQL 資料倉儲時，任何進行中的交易都會立即; 終止的重要 toounderstand造成任何開啟的交易 toobe 回復。</span><span class="sxs-lookup"><span data-stu-id="d053a-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="d053a-207">如果您的工作負載已發行的長時間執行和不完整的資料修改先前 toohello 暫停或調整規模作業，則這項工作需要 toobe 復原。</span><span class="sxs-lookup"><span data-stu-id="d053a-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="d053a-208">這可能會影響 hello toopause 所花費的時間，或調整 Azure SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="d053a-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d053a-209">`UPDATE` 和 `DELETE` 都是完整記錄作業，因此這些復原/重做作業花費的時間可能會比對等的最低限度記錄作業長很多。</span><span class="sxs-lookup"><span data-stu-id="d053a-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="d053a-210">hello 最佳的案例是 toolet 飛行資料修改交易完成之前 toopausing 或調整 SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="d053a-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="d053a-211">但是，這不一定都可行。</span><span class="sxs-lookup"><span data-stu-id="d053a-211">However, this may not always be practical.</span></span> <span data-ttu-id="d053a-212">toomitigate hello 風險長復原，請考慮下列選項的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="d053a-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="d053a-213">使用 [CTAS][CTAS] 重新撰寫長時間執行的作業</span><span class="sxs-lookup"><span data-stu-id="d053a-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="d053a-214">Hello 作業細分成多個區塊。在 hello 資料列的子集上操作</span><span class="sxs-lookup"><span data-stu-id="d053a-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="d053a-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d053a-215">Next steps</span></span>
<span data-ttu-id="d053a-216">請參閱[SQL 資料倉儲中的交易][ Transactions in SQL Data Warehouse] toolearn 更多關於隔離等級和交易式的限制。</span><span class="sxs-lookup"><span data-stu-id="d053a-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="d053a-217">如需其他最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="d053a-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

