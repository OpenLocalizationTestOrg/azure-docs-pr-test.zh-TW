---
title: "SQL 資料倉儲中的 aaaPartitioning 資料表 |Microsoft 文件"
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
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
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

所有 SQL 資料倉儲資料表類型都支援資料分割；包括叢集資料行存放區、叢集索引和堆積。  所有散發類型也也支援資料分割，包括散發的雜湊或循環配置資源。  資料分割可讓您 toodivide 您較小的群組的資料，以及在大部分情況下，資料分割的資料便已完成的日期資料行。

## <a name="benefits-of-partitioning"></a>資料分割的優點
資料分割可以提升資料維護和查詢效能。  其優點兩個或其中一個是取決於如何載入資料，以及是否 hello 相同的資料行可以使用這兩種用途，因為資料分割只能在一個資料行上。

### <a name="benefits-tooloads"></a>優點 tooloads
hello SQL 資料倉儲中資料分割的主要優點是改善 hello 效率與效能載入使用的分割區刪除的資料、 切換和合併。  在大部分情況下，資料分割的日期資料行緊密繫結 toohello 順序 hello 資料是載入的 toohello 資料庫。  其中一個 hello 使用它 hello 避免交易記錄的資料分割 toomaintain 資料的最大的優勢。  雖然只要插入、 更新或刪除資料可以 hello 最直接的方法，以極小的思考和投入時間，而使用您在載入程序分割可以大幅改善效能。

切換資料分割可以使用的 tooquickly 移除或取代資料表區段。  例如，銷售事實資料表可能過去 36 個月包含 hello 是只有資料。  在每個月的 hello 結尾，hello 早月份的銷售資料的資料表中刪除了 hello。  無法刪除此資料，會使用 delete 陳述式 toodelete hello 資料 hello 最舊的月份。  不過，刪除大量的資料列逐列與 delete 陳述式可以花很長的時間，以及建立大型交易發生錯誤時，可能需要很長的時間 toorollback hello 風險。  更接近最佳的方法是 toosimply 卸除 hello 最舊的磁碟分割的資料。  刪除 hello 個別資料列，需要數小時，刪除整個磁碟分割可能需要為秒鐘。

### <a name="benefits-tooqueries"></a>優點 tooqueries
資料分割也可以使用的 tooimprove 查詢效能。  如果查詢的資料分割的資料行上套用篩選器，這可能會限制 hello 掃描 tooonly hello 限定可能遠 hello 資料子集，避免完整資料表掃描的資料分割。  與 hello 的叢集資料行存放區索引的簡介，hello 述詞刪除效能優勢會較不會很有用，但在某些情況下可能會有好處 tooqueries。  比方說，hello 銷售事實資料表為資料分割到 36 個月使用 hello 銷售日期欄位，然後在 hello 銷售日期篩選的查詢可以略過不符合 hello 篩選條件的資料分割中的搜尋。

## <a name="partition-sizing-guidance"></a>磁碟分割大小調整指引
資料分割時可以使用的 tooimprove 效能某些案例中，建立具有資料表**太多**資料分割會降低效能，在某些情況下。  叢集資料行存放區資料表尤其堪慮。  針對資料分割 toobe 很有幫助，很重要的 toounderstand 時的資料分割 toocreate toouse 分割與 hello 數目。  那里已為 toohow 沒有硬式快速規則多個資料分割太多，這取決於您的資料而多少資料分割會載入 toosimultaneously。  但是為一般的經驗法則，將加入 10s too100s 的資料分割，而不是 1000年。

建立資料分割上時**叢集資料行存放區**很重要 tooconsider 多少資料列會讓每個分割區資料表。  為了讓叢集資料行存放區資料表達到最佳壓縮和效能，每個散發與分割區都需要至少 100 萬個資料列。  建立分割區之前，SQL 資料倉儲已將每個資料表分割成 60 個分散式資料庫。  任何資料分割加入的 tooa 資料表是另外建立 hello 幕後 toohello 分佈。  如果 hello 銷售事實資料表包含 36 的每月資料分割，而且假設 SQL 資料倉儲具有 60 分佈，然後 hello 銷售事實資料表應該包含每個月，60 萬個資料列或 2.1 10 億個資料列，當所有月份已都擴展時，請使用此範例中。  如果資料表包含比 hello 建議的每個資料分割的資料列的最小數目，大幅減少資料列時，請考慮使用較少的資料分割中的每個資料分割的資料列順序 toomake 增加 hello 數目。  另請參閱 hello[索引][ Index]發行項，其中包含您可以執行的叢集資料行存放區索引的 SQL 資料倉儲 tooassess hello 品質的查詢。

## <a name="syntax-difference-from-sql-server"></a>與 SQL Server 的語法差異
SQL 資料倉儲引進與 SQL Server 稍有不同的簡化分割定義。  資料分割函式和配置不會如同在 SQL Server 中一樣，使用於 SQL 資料倉儲。  相反地，您只需要 toodo 是識別資料分割的資料行和 hello 邊界點。  雖然資料分割的 hello 語法稍有不同 SQL Server，hello 基本概念是 hello 相同。  SQL Server 和 SQL 資料倉儲支援每個資料表一個分割資料行，它可以是遠距資料分割。  toolearn 進一步了解資料分割，請參閱[Partitioned Tables and Indexes][Partitioned Tables and Indexes]。

下列範例中的資料分割的 SQL 資料倉儲的 hello [CREATE TABLE] [ CREATE TABLE]陳述式中，資料分割 hello OrderDateKey 資料行上的 hello FactInternetSales 資料表：

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
SQL Server toomigrate 只分割定義 tooSQL 資料倉儲：

* 消除 hello SQL Server[分割區配置][partition scheme]。
* 新增 hello[資料分割函數][ partition function]定義 tooyour 建立資料表。

如果您從 SQL Server 執行個體 hello 以下 SQL 移轉資料分割的資料表可協助您在每個資料分割中的資料列的 toointerrogate hello 數目。  請注意，如果 hello 相同資料分割的資料粒度上使用 SQL 資料倉儲，每個資料分割的資料列的 hello 數目將會降低，因數為 60。  

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
是一個 toohello 資料表資料分割決策的最後一段考量 toofactor[工作負載管理][workload management]。  主要 hello 管理的記憶體和並行存取 SQL 資料倉儲中的工作負載管理。  在 SQL 資料倉儲 hello 配置 tooeach 發佈在查詢執行期間的最大記憶體是管的資源類別。  在理想情況下您的資料分割將調整大小 in consideration of hello 記憶體需求，建立叢集資料行存放區索引的其他因素。  配置更多記憶體給叢集資料行存放區索引時，即可獲得極大的好處。  因此，您將會重建分割區索引的 tooensure 尚未用完的記憶體。 增加 hello 數量記憶體可用 tooyour 查詢可藉由切換從 hello 預設角色、 smallrc、 tooone 的 hello 其他角色，例如 largerc。

Hello 配置的記憶體，每個發佈的詳細資訊，請查詢 hello 資源管理員動態管理檢視。 事實上，記憶體授權會早於下列 hello 圖形。 不過，這會提供指導方針，以便在針對資料管理作業調整分割大小時使用。  請嘗試 tooavoid 調整大小超出 hello hello 超大型資源類別所提供的記憶體授與資料分割。 如果分割區超出本圖風險 hello 反過來 tooless 最佳壓縮的記憶體不足壓力。

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
SQL 資料倉儲支援資料分割、合併和切換。 這些函式的每一個都是使用 hello excuted [ALTER TABLE] [ ALTER TABLE]陳述式。

您必須確定 hello 資料分割將對齊其各自的界限上，且符合 hello 資料表定義的兩個資料表之間的 tooswitch 分割區。 Check 條件約束沒有 tooenforce hello 資料表 hello 來源資料表中的值範圍必須包含 hello 相同為 hello 目標資料表資料分割界限。 如果這不是 hello 案例，則會失敗 hello 資料分割切換，將不會同步 hello 分割區中繼資料。

### <a name="how-toosplit-a-partition-that-contains-data"></a>如何 toosplit 包含資料的磁碟分割
hello 最有效率的方法 toosplit 已經包含資料的資料分割是 toouse`CTAS`陳述式。 如果 hello 資料分割的資料表的叢集資料行存放區則 hello 資料表資料分割必須是空白之前可以分割。

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
> 建立 hello 統計資料物件，我們確定該資料表的中繼資料更精確。 如果我們省略了建立統計資料，SQL 資料倉儲將會使用預設值。 如需統計資料的詳細資訊，請檢閱[統計資料][statistics]。
> 
> 

我們可以在使用 hello hello 資料列計數查詢`sys.partitions`目錄檢視：

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

如果我們嘗試 toosplit 此資料表，我們會收到錯誤：

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346，層級 15，狀態 1，行 44 分割子句的 ALTER PARTITION 陳述式失敗，因為不是空的 hello 磁碟分割。  Hello 資料表上存在的資料行存放區索引時，可以在分割只有空的資料分割。 請考慮停用後再發出 hello ALTER PARTITION 陳述式，再重建 hello 資料行存放區索引，ALTER PARTITION 完成後的 hello 資料行存放區索引。

不過，我們可以使用`CTAS`toocreate 新的資料表 toohold 我們的資料。

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

允許參數為 hello 資料分割界限對齊。 這會導致 hello 來源資料表具有空的分割區，我們接下來可以分割。

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

剩下 toodo 是我們資料 toohello 新資料分割界限使用的 tooalign `CTAS` toohello 主資料表中切換資料

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

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

當您完成 hello hello 資料移動是個不錯的主意 toorefresh hello 統計資料在 hello 目標資料表 tooensure 它們正確地反映 hello hello 中的資料及其個別資料分割的新發佈：

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>資料表分割原始檔控制
tooavoid 從您的資料表定義**rusting**在您的原始檔控制系統中，您可能想 tooconsider hello 遵循方法：

1. 建立 hello 資料表為資料分割資料表，但不會有資料分割值

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

1. `SPLIT`hello 資料表 hello 部署程序的一部分：

```sql
-- Create a table containing hello partition boundaries

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

-- Iterate over hello partition boundaries and split hello table

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

這個方法 hello 與原始檔控制中的程式碼保持不變，而 hello 資料分割的界限值允許 toobe 動態;經過一段時間發展與 hello 倉儲。

## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[維護資料表統計資料][ Statistics]和[暫存資料表][Temporary]。  若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。

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
