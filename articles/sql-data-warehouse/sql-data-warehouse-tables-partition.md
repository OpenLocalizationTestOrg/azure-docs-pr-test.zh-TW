---
title: "在 SQL 資料倉儲中分割資料表 | Microsoft Docs"
description: "開始在 Azure SQL 資料倉儲中分割資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 3edfd34d368228be32afef48688739639a3b03ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>在 SQL 資料倉儲中分割資料表
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

所有 SQL 資料倉儲資料表類型都支援資料分割；包括叢集資料行存放區、叢集索引和堆積。  所有散發類型也也支援資料分割，包括散發的雜湊或循環配置資源。  資料分割可讓您將資料分成較小的資料群組，而在大部分情況下，會在日期資料行上進行資料分割。

## <a name="benefits-of-partitioning"></a>資料分割的優點
資料分割可以提升資料維護和查詢效能。  其具備上述兩個優點，還是只有一個優點，取決於資料的載入方式，以及相同的資料行是否可用於這兩個目的，因為資料分割只能在一個資料行上進行。

### <a name="benefits-to-loads"></a>載入的優點
SQL 資料倉儲中資料分割的主要優點是藉由使用分割區刪除、切換和合併，來改善資料載入的效率與效能。  在大部分情況下，會依照與資料載入到資料庫的順序密切相關的日期資料行分割資料。  使用資料分割來維護資料的最大優點之一是避免記錄交易。  雖然插入、更新或刪除資料可能是最直接的方法，但只要付出一些關心和努力，在載入處理期間使用資料分割可以大幅改善效能。

切換分割區可用於快速移除或取得資料表的某個區段。  例如，銷售事實資料表可能僅包含過去 36 個月的資料。  在每個月月底，便會從資料表刪除最舊月份的銷售資料。  使用 delete 陳述式來刪除最舊月份的資料，即可刪除此資料。  不過，使用 delete 陳述式逐列刪除大量資料可能需要很長的時間，而且會產生大型交易的風險，如果發生錯誤，則可能需要很長的時間來復原。  比較理想的方法是直接卸除最舊的資料磁碟分割。  刪除個別的資料列需要數小時的時間，而刪除整個磁碟分割可能只要數秒。

### <a name="benefits-to-queries"></a>查詢的優點
資料分割也可用來改善查詢效能。  如果查詢在資料分割資料行上套用篩選，這可能會讓掃描僅限於合格的資料分割 (這可能是較小部分的資料)，進而避免掃描整個資料表。  引進叢集資料行存放區索引後，述詞消除效能優勢比較沒有幫助，但在某些情況下，對查詢有所益處。  例如，如果使用銷售日期欄位將銷售事實資料表分割成 36 個月，以銷售日期進行篩選的查詢便可略過不符合篩選條件的分割區。

## <a name="partition-sizing-guidance"></a>磁碟分割大小調整指引
雖然資料分割可用來改善某些案例的效能，但是在某些情況下，建立具有 **太多** 資料分割的資料表可能會降低效能。  叢集資料行存放區資料表尤其堪慮。  若要讓資料分割有所助益，務必要了解使用資料分割的時機，以及要建立的分割區數目。  多少資料分割才算太多並無硬性規定，這取決於您的資料以及您同時載入多少資料分割。  但依照一般經驗法則，考慮加入 10 到 100 個分割區，而不是 1000 個。

在 **叢集資料行存放區** 資料表上建立資料分割時，請務必考慮每個資料分割中將放入多少資料列。  為了讓叢集資料行存放區資料表達到最佳壓縮和效能，每個散發與分割區都需要至少 100 萬個資料列。  建立分割區之前，SQL 資料倉儲已將每個資料表分割成 60 個分散式資料庫。  除了散發以外，任何加入至資料表的資料分割都是在幕後建立。  依據此範例，如果銷售事實資料表包含 36 個月的分割區，並假設 SQL 資料倉儲有 60 個散發，則銷售事實資料表每個月應包含 6 千萬個資料列，或是在填入所有月份時包含 21 億個資料列。  如果資料表包含的資料列遠少於每個分割區建議的最小資料列數，請考慮使用較少的分割區，以增加每個分割區的資料列數目。  另請參閱[索引][Index]一文，其中包含可在 SQL 資料倉儲執行的查詢，以評估叢集資料行存放區索引的品質。

## <a name="syntax-difference-from-sql-server"></a>與 SQL Server 的語法差異
SQL 資料倉儲引進與 SQL Server 稍有不同的簡化分割定義。  資料分割函式和配置不會如同在 SQL Server 中一樣，使用於 SQL 資料倉儲。  相反地，您只需要識別已分割的資料行和邊界點。  雖然資料分割的語法與 SQL Server 稍有不同，但基本概念是一樣的。  SQL Server 和 SQL 資料倉儲支援每個資料表一個分割資料行，它可以是遠距資料分割。  若要深入了解資料分割，請參閱[分割資料表和索引][Partitioned Tables and Indexes]。

SQL 資料倉儲分割 [CREATE TABLE][CREATE TABLE] 陳述式的以下範例，會依據 OrderDateKey 資料行分割 FactInternetSales 資料表︰

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>從 SQL Server 移轉資料分割
若要將 SQL Server 分割定義移轉至 SQL 資料倉儲，只需：

* 刪除 SQL Server [資料分割配置][partition scheme]。
* 將[資料分割函式][partition function]定義新增至您的 CREATE TABLE。

如果您從 SQL Server 執行個體移轉分割資料表，下面的 SQL 可協助您詢問每個分割區中的資料列數目。  請記住，如果 SQL 資料倉儲上使用相同的資料分割資料細微性，則每個分割區的資料列數目會依 60 的倍數減少。  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>工作負載管理
要納入資料表分割決策的最後一項資訊是[工作負載管理][workload management]。  SQL 資料倉儲中的工作負載管理主要是記憶體和並行存取管理。  在 SQL 資料倉儲中，資源類別會控管在查詢執行期間配置給每個散發的最大記憶體。  在理想的情況下，會考量建置叢集資料行存放區索引的記憶體需求等其他因素，以調整您的分割大小。  配置更多記憶體給叢集資料行存放區索引時，即可獲得極大的好處。  因此，您會想要確定重建分割索引不會耗盡記憶體。 從預設角色 smallrc 切換到其他角色 (例如 largerc)，即可增加您的查詢可用的記憶體數量。

查詢資源管理員動態管理檢視，即可取得每個散發的記憶體配置資訊。 事實上，記憶體授與會小於下列數據。 不過，這會提供指導方針，以便在針對資料管理作業調整分割大小時使用。  盡量避免將分割大小調整超過超大型資源類別所提供的記憶體授與。 如果分割成長超過此數據，您就會冒著記憶體壓力的風險，進而導致比較不理想的壓縮。

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>分割切換
SQL 資料倉儲支援資料分割、合併和切換。 這些功能是使用 [ALTER TABLE][ALTER TABLE] 陳述式執行。

若要切換兩個資料表間的分割，您必須確定分割對齊其各自的界限，而且資料表定義相符。 檢查條件約束不適用於強制資料表中的值範圍，來源資料表必須包含與目標資料表相同的分割界限。 如果情況不是如此，則分割切換將會失敗，因為分割中繼資料不會同步處理。

### <a name="how-to-split-a-partition-that-contains-data"></a>如何分割包含資料的分割
使用 `CTAS` 陳述式是分割已含資料之分割的最有效方法。 如果分割資料表是叢集式資料行存放區，則資料表分割必須空的，才可加以分割。

下列範例顯示每個分割包含一個資料列的分割資料行存放區資料表：

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> 藉由建立統計資料物件，我們確定資料表中繼資料更加精確。 如果我們省略了建立統計資料，SQL 資料倉儲將會使用預設值。 如需統計資料的詳細資訊，請檢閱[統計資料][statistics]。
> 
> 

我們可以接著使用 `sys.partitions` 目錄檢視，查詢資料列計數：

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

如果我們嘗試分割此資料表，我們會收到錯誤：

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

訊息 35346、層級 15、狀態 1、行 44：ALTER PARTITION 陳述式的 SPLIT 子句失敗，因為分割不是空的。  只有在資料表上存在資料行存放區索引時，才可以分割空的分割。 請考慮在發出 ALTER PARTITION 陳述式前停用資料行存放區索引，然後在 ALTER PARTITION 完成後重建資料行存放區索引。

不過，我們可以使用 `CTAS` 建立新資料表以保存資料。

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

分割界限已對齊，所以允許切換。 這會讓來源資料表有空白分割可供我們接著分割。

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

接下來只需使用 `CTAS` 將我們的資料對齊新的分割界限，並將我們的資料切換回到主資料表

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 TO dbo.FactInternetSales PARTITION 2;
```

完成資料移動後，最好能重新整理目標資料表上的統計資料，確保統計資料可在其各自的分割中精確地反映出資料的新散發：

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>資料表分割原始檔控制
若要避免您的資料表定義在您的原始檔控制系統中 **失效** ，您可以考慮下列方法：

1. 將資料表建立為分割資料表，但沒有分割值

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT` 資料表：

```sql
-- Create a table containing the partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over the partition boundaries and split the table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

利用這種方法，原始檔控制中的程式碼會保持靜態，並允許動態的分割界限值；隨著時間與倉儲一起發展。

## <a name="next-steps"></a>後續步驟
若要深入了解，請參閱[資料表概觀][Overview]、[資料表資料類型][Data Types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[維護資料表統計資料][Statistics]和[暫存資料表][Temporary]等文章。  若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
