---
title: "SQL 資料倉儲中的 aaaDistributing 資料表 |Microsoft 文件"
description: "開始在 Azure SQL 資料倉儲中散發資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>在 SQL 資料倉儲中散發資料表
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [資料類型][Data Types]
> * [散發][Distribute]
> * [索引][Index]
> * [資料分割][Partition]
> * [統計資料][Statistics]
> * [暫存][Temporary]
>
>

SQL 資料倉儲是大量平行處理 (MPP) 分散式資料庫系統。  將資料和處理能力分割於多個節點之間，SQL 資料倉儲就能夠提供極大的延展性 - 遠超過任何單一系統。  決定如何 toodistribute 您的 SQL 資料倉儲中的資料最重要的 hello 的其中一個因素 tooachieving 達到最佳效能。   hello 金鑰 toooptimal 效能最小化資料移動，然後依次 hello 金鑰 toominimizing 資料移動選取 hello 右散發策略。

## <a name="understanding-data-movement"></a>了解資料移動
MPP 系統、 在每個資料表中的 hello 資料分割到數個基礎資料庫。  hello 最最佳化查詢 MPP 系統上的可以只傳遞 tooexecute hello 上個別的分散式的資料庫，而不需要互動之間 hello 其他資料庫。  例如，假設您的銷售資料的資料庫有「銷售」和「客戶」兩個資料表。  如果您有需要 toojoin sales 資料表 tooyour 客戶資料表的查詢，並除以銷售和客戶資料表總客戶編號置於個別的資料庫中的每一位客戶，任何加入銷售和客戶的查詢就可以解決在每個不知道資料庫 hello 其他資料庫。  相反地，如果銷售資料除以訂單號碼，而您的客戶資料，客戶數目時，然後任何指定的資料庫不會有 hello 相對應的資料每個客戶，因此如果您想 toojoin 銷售資料 tooyour 客戶資料，您需要tooget hello 資料每個客戶的 hello 其他資料庫。  在第二個範例中，移動資料將需要 toooccur toomove hello 客戶資料 toohello 銷售資料，因此 hello 兩個資料表可以聯結。  

資料移動不一定是一件壞事，有時候很有必要 toosolve 查詢。  但當您可以避免這個額外的步驟，自然地查詢的執行速度會更快。  資料移動最常發生於聯結資料表或執行彙總時。  通常您需要 toodo 兩者，您可能無法 toooptimize 一種情況，例如聯結，您仍然必須解決的資料移動 toohelp hello 其他案例中的，例如彙總。  hello 訣竅找出這是較少工作。  在大部分情況下，散發大型事實資料表經常聯結的資料行上是 hello 最有效方法以降低 hello 大部分的資料移動。  散發資料聯結資料行上的進行更多的常見方法 tooreduce 資料移動比散發到彙總中的資料行的資料。

## <a name="select-distribution-method"></a>選擇散發方法
Hello 幕後 SQL 資料倉儲會將您的資料分割成 60 的資料庫。  每個個別的資料庫是參照的 tooas**發佈**。  當資料載入至每個資料表時，SQL 資料倉儲會如何具有 tooknow toodivide 跨這些 60 發佈資料。  

hello 發佈方法定義在 hello 資料表層級和目前有兩個選擇：

1. **循環配置資源** 會平均但隨機散發資料。
2. **雜湊散發** 會根據單一資料行的雜湊值散發資料

根據預設，當您未定義的資料散發方式，您的資料表將發佈使用 hello**循環配置資源**發佈方法。  不過，因為您變得較複雜實作中，您會想使用 tooconsider**雜湊散發**資料表 toominimize 資料移動，這會依次最佳化查詢效能。

### <a name="round-robin-tables"></a>循環配置資源資料表
使用 hello 散發資料的循環配置資源方法，是非常如何聽起來。  載入資料時，每個資料列會直接傳送 toohello 下一個發佈。  散發 hello 資料的這個方法會一律隨機將 hello 資料非常平均分散到所有 hello 分佈。  也就是說，沒有任何排序完成期間 hello 循環配置資源的程序而放置您的資料。  基於這個理由，循環配置資源散發有時稱為隨機雜湊。  循環配置資源的分散式資料表沒有任何需要 toounderstand hello 資料。  基於這個理由，循環配置資源資料表通常具有良好的載入目標。

根據預設，如果選擇沒有散發方法，則 hello 循環配置資源發佈方法將用於。  不過，雖然循環配置資源表格是簡單的 toouse，因為資料會隨機分佈在 hello 系統表示 hello 系統無法保證的散發每個資料列是上。  在結果中，有時候 hello 系統需求 tooinvoke 資料移動作業 toobetter 組織資料之前它可以解析查詢。  此額外步驟會使您的查詢變慢。

請考慮使用循環配置資源發佈 hello 下列案例中針對資料表：

* 以簡單的起點開始使用時
* 如果沒有明顯的聯結索引鍵
* 如果不是散發 hello 資料表的雜湊的候選資料行
* 如果 hello 資料表不會共用共同的聯結索引鍵與其他資料表
* 如果比其他 hello 查詢中聯結的那麼顯著 hello 聯結
* 當 hello 資料表是暫時的臨時資料表

兩個範例都會建立循環配置資源資料表︰

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> 循環配置資源時所明確 DDL 中的 hello 預設資料表類型是最佳做法，讓資料表配置的 hello 意圖清除 tooothers。
>
>

### <a name="hash-distributed-tables"></a>雜湊散發資料表
使用**雜湊散發**演算法 toodistribute 資料表可以提升效能許多案例中，藉由在查詢時減少資料移動。  分散式的資料表是屬 hello 資料表的雜湊散發資料庫時您所選取的單一資料行上使用雜湊演算法。  hello 散發資料行是決定 hello 資料分成分散式資料庫的方式。  hello 雜湊函式會使用 hello 散發資料行 tooassign 列 toodistributions。  hello 雜湊演算法，並產生分佈是具決定性。  也就是 hello hello 相同的資料類型會一律使用相同的值有 toohello 相同的散發。    

這個範例會建立依照識別碼散發的資料表︰

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>選擇散發資料行
當您選擇太**雜湊散發**資料表時，您將需要 tooselect 單一散發資料行。  當選取散發資料行，有三個主要的因素 tooconsider。  

選取具有下列特性的單一資料行︰

1. 不會更新
2. 平均散發資料，以避免資料扭曲
3. 最小化資料移動

### <a name="select-distribution-column-which-will-not-be-updated"></a>選取不會更新的散發資料行
散發資料行不可更新，因此，選取具靜態值的資料行。  如果資料行，將需要更新 toobe，通常是不好發佈候選。  如果沒有，您必須更新散發資料行的情況下，作法是先刪除 hello 資料列，然後插入新資料列。

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>選取將平均散發資料的散發資料行
分散式的系統執行只盡其最慢的發佈時，會很重要的 toodivide hello 工作平均跨順序 tooachieve 平衡執行中的 hello 分佈 hello 系統。  hello hello 工作就會劃分分散式系統的方式根據每個散發 hello 資料所在。  這使得散發 hello 資料，讓每個分佈有相等的工作，並將採用 hello 相同時間 toocomplete hello 工作及其部分的非常重要的 tooselect hello 右散發資料行。  當工作也分成 hello 系統時，hello 資料被平衡 hello 分佈。  當資料不平衡時，我們將此稱為 **資料扭曲**。  

toodivide 資料平均，避免資料扭曲，請選取您的散發資料行時，請考慮下列 hello:

1. 選取包含大量相異值的資料行。
2. 避免將資料散發於含有少許相異值的資料行。
3. 避免將資料散發於 null 頻繁出現的資料行。
4. 避免在日期資料行上散發資料。

由於每個值是 60 分佈的雜湊的 too1，tooachieve 平均散發您會想 tooselect 的高唯一且包含超過 60 的唯一值的資料行。  tooillustrate，試想一個情況，資料行僅具有 40 的唯一值。  如果此資料行已選定為 hello 散發索引鍵，hello 資料為該資料表會登陸 40 分佈最多，僅保留任何資料，然後沒有處理 toodo 20 分佈。  相反地，hello 其他 40 分佈會有多個工作 toodo 如果 hello 資料的平均散佈超過 60 份的分佈。  這個案例就是資料扭曲的範例。

MPP 系統中每個查詢步驟會等到所有分佈 toocomplete 之 hello 工作。  如果一個散發是執行作業超過 hello 其他項目，則 hello 資源的 hello 其他分佈基本上會浪費只等待 hello 忙碌中發佈。  當所有散發的工作分配不均時，我們將此稱為 **處理誤差**。  處理誤差會導致查詢 toorun 低於如果 hello 工作負載平均分散到 hello 分佈。  資料扭曲，都會導致 tooprocessing 誤差。

避免依 hello null 值將所有登陸在 hello 相同分配高度可為 null 的資料行上發佈。 散發之日期資料行也可能造成處理誤差的特定日期的所有資料將都登陸在 hello 相同，因為通訊群組。 如果數個使用者會在查詢執行所有篩選 hello 相同的日期，則只有 1 個的 hello 60 分佈會進行所有 hello 工作的特定的日期都只會在一個發佈。 在此案例中，hello 查詢可能都會執行 60 時間低於如果 hello 資料已平均分散到所有 hello 分佈。

當沒有候選資料行存在，請考慮使用循環配置資源做為 hello 發佈方法。

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>選取會將資料移動降至最低的散發資料行
選取 hello 右散發資料行降到最低的資料移動是其中一種 hello 最佳化您的 SQL 資料倉儲的效能最重要的策略。  資料移動最常發生於聯結資料表或執行彙總時。  用於 `JOIN`、`GROUP BY`、`DISTINCT`、`OVER`、`HAVING` 子句的資料行全都是**理想**的雜湊散發候選項目。

在 hello 相反地，資料行中 hello`WHERE`子句執行**不**讓良好的雜湊資料行的候選項目的限制哪一個分佈參與 hello 查詢，導致處理因為誤差。  這可能會吸引人 toodistribute，但通常可能會造成這項處理誤差的資料行的理想範例為日期資料行。

一般而言，如果您有兩個大型事實資料表經常涉及的聯結中，您會取得 hello 最高效能散發 hello 聯結資料行其中兩個資料表。  如果您有絕不會是聯結的 tooanother 大型事實資料表的資料表，然後尋找經常處於 hello toocolumns`GROUP BY`子句。

有幾個索引鍵的條件加入期間必須符合的 tooavoid 資料移動：

1. hello hello 聯結中涉及的資料表必須是分佈在雜湊**一個**hello hello 聯結中參與的資料行。
2. hello hello 聯結資料行資料類型必須符合這兩個資料表之間。
3. 必須以等號運算子加入 hello 資料行。
4. hello 聯結類型可能無法`CROSS JOIN`。

## <a name="troubleshooting-data-skew"></a>資料扭曲疑難排解
當資料表資料發佈使用 hello 雜湊散發方法有某些機率準 toohave 比其他不當比例的詳細資料。 因為 hello 最終結果的分散式查詢必須等候 hello 最長執行發佈 toofinish 誤差過多資料可能會影響查詢效能。 視 hello 程度 hello 資料扭曲您可能需要 tooaddress 它。

### <a name="identifying-skew"></a>識別扭曲
簡單的方式 tooidentify 資料表為準是 toouse `DBCC PDW_SHOWSPACEUSED`。  這是非常快速且簡單的方式 toosee hello 的資料表會儲存在每個資料庫的 hello 60 分佈的資料列數目。  請記住，為了 hello 最平衡效能，hello 分散式資料表中的資料列應該分成平均 hello 的所有分佈。

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

不過，如果您查詢 hello Azure SQL 資料倉儲動態管理檢視 (DMV)，您可以執行更詳細的分析。  toostart，建立 hello 檢視[dbo.vTableSizes] [ dbo.vTableSizes]使用檢視 hello SQL 從[資料表概觀][ Overview]發行項。  一旦建立 hello 檢視時，執行此查詢 tooidentify，哪些資料表有個以上的資料 10%誤差。

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>解決資料扭曲
不是所有誤差是足夠 toowarrant 修正程式。  在某些情況下，某些查詢中資料表的 hello 效能可能會超過資料扭曲 hello 的傷害。  toodecide，如果您也應該解決資料扭曲在資料表中，您應該了解有關 hello 資料磁碟區和查詢最大的在您的工作負載。   其中一種方式在 hello 誤差影響 toolook 是 hello toouse hello 步驟[查詢監視][ Query Monitoring]文章 toomonitor hello 影響的查詢效能傾斜和特別 hello 影響 toohow 長時間查詢需要 toocomplete hello 個別發佈。

將資料散發是要尋找 hello 資料誤差降至最低，並盡量減少資料移動之間的正確平衡。 這些可以團體的目標，有時候您會想 tookeep 資料偏斜順序 tooreduce 資料移動。 比方說，當 hello 散發資料行經常 hello 聯結和彙總中的共用的資料，您將會最小化資料移動。 hello 擁有 hello 最少的資料移動可能會遠大於 hello 影響的資料扭曲。

hello 的典型方式 tooresolve 資料誤差是 toore-建立 hello 資料表具有不同的散發資料行。 因為沒有任何方法 toochange hello 散發資料行上的現有資料表，資料表的 hello 方式 toochange hello 發佈它 toorecreate 它有 [CTAS] []。  以下是解決資料扭曲的兩個範例：

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>範例 1： 重新建立 hello 與新的散發資料行的資料表
這個範例會使用 [CTAS] [] toore-建立具有不同的雜湊散發資料行的資料表。

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>範例 2： 重新建立 hello 資料表使用循環配置資源發佈
這個範例會使用 [CTAS] [] toore-建立具有循環配置資源，而不是雜湊散發的資料表。 這項變更將會產生即使資料分佈 hello 成本增加的資料移動。

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>後續步驟
toolearn 有關資料表設計的詳細資訊，請參閱 「 hello[散發][Distribute]，[索引][Index]，[分割][Partition]，[資料型別][Data Types]，[統計資料][ Statistics]和[暫存資料表] [ Temporary]文件。

如需最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
