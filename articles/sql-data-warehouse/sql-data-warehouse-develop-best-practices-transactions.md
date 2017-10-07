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
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>最佳化 SQL 資料倉儲的交易
本文說明如何 toooptimize hello 的交易式的程式碼的效能，同時長回復的風險降到最低。

## <a name="transactions-and-logging"></a>交易和記錄
交易是關聯式資料庫引擎的重要元件。 SQL 資料倉儲會在資料修改期間使用交易。 這些交易可以是明確或隱含的。 單一 `INSERT`、`UPDATE` 和 `DELETE` 陳述式都是隱含交易的範例。 外顯交易由開發人員使用明確撰寫`BEGIN TRAN`，`COMMIT TRAN`或`ROLLBACK TRAN`和通常用在多個修改陳述式需要 toobe 中單一不可部分完成單位連結在一起。 

Azure SQL 資料倉儲認可使用交易記錄的變更 toohello 資料庫。 每個散發套件都有自己的交易記錄檔。 交易記錄檔寫入是自動的。 不需要任何組態。 不過，儘管這個程序可確保 hello 寫入它會導致額外負荷 hello 系統中。 您可以藉由撰寫交易式的有效程式碼，將影響降到最低。 交易式的有效程式碼大致分為兩個類別。

* 盡可能使用最低限度的記錄建構
* 使用已設定領域的批次 tooavoid 單數長時間執行交易處理資料
* 採用的資料分割切換的大型修改 tooa 給定資料分割模式

## <a name="minimal-vs-full-logging"></a>最低限度 vs. 完整記錄
與完整記錄作業，使用 hello 交易記錄檔 tookeep 追蹤的每個資料列變更，不同的是最低限度記錄的作業追蹤的範圍配置與僅限中繼資料變更。 因此，最低限度記錄包含僅記錄 hello 資訊是 hello 事件中發生失敗或明確要求的必要的 toorollback hello 交易 (`ROLLBACK TRAN`)。 因為較 hello 交易記錄中追蹤資訊，最低限度記錄的作業執行效能高於大小類似的完整記錄作業。 此外，因為較少寫入 hello 交易記錄檔，就會產生較少的記錄資料，因此多個 I/O 有效率。

hello 交易安全限制僅適用於 toofully 記錄作業。

> [!NOTE]
> 最低限度記錄作業可以加入明確交易。 追蹤配置結構中的所有變更，則它是可能 tooroll 後使用最低限度記錄的作業。 很重要的 hello 變更 「 最低限度"toounderstand 記錄它不是未記錄。
> 
> 

## <a name="minimally-logged-operations"></a>最低限度記錄作業
hello 下列作業都能使用最低限度記錄：

* CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> 內部資料移動作業 (例如`BROADCAST`和`SHUFFLE`) 不會受到 hello 交易安全性限制。
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>大量載入的最低限度記錄
`CTAS` 和 `INSERT...SELECT` 都是大量載入作業。 不過，會同時受到 hello 目標資料表定義與 hello 負載案例而定。 以下是說明大量作業是否為完全或最低限度記錄的資料表︰  

| 主要索引 | 載入案例 | 記錄模式 |
| --- | --- | --- |
| 堆積 |任意 |**最低限度** |
| 叢集索引 |空的目標資料表 |**最低限度** |
| 叢集索引 |載入的資料列不會與目標中的現有頁面重疊 |**最低限度** |
| 叢集索引 |載入的資料列會與目標中的現有頁面重疊 |完整 |
| 叢集資料行存放區索引 |每個與分割對齊的散發套件之批次大小 >= 102,400 |**最低限度** |
| 叢集資料行存放區索引 |批次大小 < 每個與分割對齊的散發套件 102,400 |完整 |

值得注意的是任何寫入 tooupdate 次要或非叢集索引一律會完整記錄作業。

> [!IMPORTANT]
> SQL 資料倉儲有 60 個散發套件。 因此，假設所有資料列平均分配，登陸在單一磁碟分割，您的批次必須 toocontain 6,144,000 資料列或更大的 toobe 最低限度記錄的寫入 tooa 叢集資料行存放區索引時。 Hello 資料表已分割，而且正在插入資料列的 hello 跨越資料分割界限，如果您將需要每個資料分割界限假設平均資料散發 6,144,000 資料列。 每個發佈中的每個資料分割必須獨立超過 hello 102,400 資料列臨界值 hello 插入 toobe hello 發佈到使用最低限度記錄。
> 
> 

利用叢集索引將資料載入非空白資料表中，通常會混合包含完整記錄和最低限度記錄資料列。 叢集索引是頁面的平衡樹狀結構 (b 型樹狀目錄)。 如果 hello 頁面寫入 tooalready 包含另一個交易的資料列，然後這些寫入將會完整記錄。 不過，如果是空的 hello 頁面然後 hello 寫入 toothat 頁面將會進行最低限度記錄。

## <a name="optimizing-deletes"></a>最佳化刪除
`DELETE` 是完整記錄的作業。  如果您需要 toodelete 大量資料表或資料分割中的資料時，通常會比較合理太`SELECT`hello 資料想 tookeep，可以執行以最低限度記錄作業。  tooaccomplish，建立新的資料表與[CTAS][CTAS]。  建立之後，使用[重新命名][ RENAME] tooswap 移出您舊的資料表與 hello 新建立的資料表。

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

## <a name="optimizing-updates"></a>最佳化更新
`UPDATE` 是完整記錄的作業。  如果您需要 tooupdate 大量的資料表中的資料列或資料分割通常很效率 toouse 最低限度記錄的作業，例如[CTAS] [ CTAS] toodo 如此。

在 hello 下例完整資料表更新已經過轉換的 tooa `CTAS` ，方便您最低限度記錄。

在此情況下我們 retrospectively 新增折扣量 toohello 銷售 hello 資料表中：

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
> 使用 SQL 資料倉儲工作負載管理功能有助於重新建立大型資料表。 如需詳細資訊，請參閱 toohello 工作負載管理 > 一節中 hello[並行][ concurrency]發行項。
> 
> 

## <a name="optimizing-with-partition-switching"></a>利用分割切換進行最佳化
面臨[資料表分割][table partition]內部的大規模修改時，分割切換模式相當實用。 如果 hello 資料修改會很可觀，而且跨越多個資料分割，然後只需反覆 hello 分割區會達到 hello 相同的結果。

hello 步驟 tooperform 分割區切換如下所示：

1. 建立空白分割
2. 執行 CTAS hello 'update'
3. 切換移出 hello 現有資料 toohello 移出資料表
4. 切換移入 hello 新的資料
5. Hello 資料進行清除

不過，toohelp 識別 hello 分割 tooswitch 我們首先需要 toobuild 的協助程式程序，例如其中一個 hello 下方。 

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

此程序最大化程式碼重複使用，並保留 hello 資料分割切換更精簡的範例。

hello 的下列程式碼會示範 hello 五個步驟上述 tooachieve 完整的資料分割切換的常式。

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

## <a name="minimize-logging-with-small-batches"></a>小型批次的最低限度記錄
對於大型資料修改作業，可能更有意義 toodivide hello 作業成區塊或批次 tooscope hello 單位的工作。

以下提供實用的範例。 已設定 tooa 一般數字 toohighlight hello 技術 hello 批次大小。 事實上 hello 批次大小會變得很大。 

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

## <a name="pause-and-scaling-guidance"></a>暫停和調整指引
Azure SQL 資料倉儲可讓您暫停、繼續及調整需要的資料倉儲。 您暫停或調整您的 SQL 資料倉儲時，任何進行中的交易都會立即; 終止的重要 toounderstand造成任何開啟的交易 toobe 回復。 如果您的工作負載已發行的長時間執行和不完整的資料修改先前 toohello 暫停或調整規模作業，則這項工作需要 toobe 復原。 這可能會影響 hello toopause 所花費的時間，或調整 Azure SQL 資料倉儲資料庫。 

> [!IMPORTANT]
> `UPDATE` 和 `DELETE` 都是完整記錄作業，因此這些復原/重做作業花費的時間可能會比對等的最低限度記錄作業長很多。 
> 
> 

hello 最佳的案例是 toolet 飛行資料修改交易完成之前 toopausing 或調整 SQL 資料倉儲中。 但是，這不一定都可行。 toomitigate hello 風險長復原，請考慮下列選項的 hello 的其中一個：

* 使用 [CTAS][CTAS] 重新撰寫長時間執行的作業
* Hello 作業細分成多個區塊。在 hello 資料列的子集上操作

## <a name="next-steps"></a>後續步驟
請參閱[SQL 資料倉儲中的交易][ Transactions in SQL Data Warehouse] toolearn 更多關於隔離等級和交易式的限制。  如需其他最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。

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

