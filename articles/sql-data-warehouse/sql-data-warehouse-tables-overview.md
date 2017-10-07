---
title: "SQL 資料倉儲中的資料表 aaaOverview |Microsoft 文件"
description: "開始使用 Azure SQL 資料倉儲資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>SQL 資料倉儲中的資料表概觀
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

開始在 SQL 資料倉儲中建立資料表很簡單。  基本的 hello [CREATE TABLE] [ CREATE TABLE]語法遵循 hello 最常見的一般語法已經熟悉的其他資料庫工作。  toocreate 資料表，您只需要 tooname 資料表時，命名您的資料行，並定義每個資料行的資料類型。  如果您已在其他資料庫中建立資料表，這應該看起來非常熟悉 tooyou。

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

hello，上述範例會建立具有兩個資料行，FirstName 和 LastName 名為 Customers 的資料表。  每個資料行定義資料類型為 VARCHAR(25)，這會限制 hello 資料 too25 字元。  是大部分 hello 與其他資料庫相同的資料表，以及其他項目，這些基本屬性。  資料型別會定義每個資料行，並確定 hello 資料的完整性。  索引可以藉由減少 I/O tooimprove 效能加入。  資料分割可以加入 tooimprove 效能時，如果需要 toomodify 資料。

[重新命名][RENAME] SQL 資料倉儲資料表的方式如下：

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>分散式資料表
分散式系統，例如 SQL 資料倉儲為 hello 所導入新的基本屬性**散發資料行**。  hello 散發資料行是非常什麼聽起來。  決定的 hello 資料行，所以如何 toodistribute，或您 hello 幕後的資料分割。  當您建立未指定 hello 散發資料行的資料表時，hello 資料表會自動發佈使用**循環配置資源**。  雖然在某些情況下，循環配置資源資料表可能已足夠，但定義散發資料行可大幅減少期間查詢的資料移動，因而讓效能達到最佳化。  中的情況下的少量資料表中的資料，請選擇 toocreate hello 資料表以 hello**複寫**分佈類型複製資料 tooeach 計算節點，並將儲存在查詢執行時間的資料移動。 請參閱[散發資料表][ Distribute] toolearn 深入了解如何 tooselect 散發資料行。

## <a name="indexing-and-partitioning-tables"></a>編製資料表的索引和分割資料表
當您變得更進階的中使用 SQL 資料倉儲，並想 toooptimize 效能，您會想 toolearn 深入了解資料表設計。  toolearn 詳細資訊，請參閱 hello 文件上[資料表資料類型][Data Types]，[散發資料表][Distribute]， [的資料表建立索引][ Index]和[分割資料表][Partition]。

## <a name="table-statistics"></a>資料表統計資料
統計資料是您的 SQL 資料倉儲非常重要的 toogetting hello 最佳效能。  由於 SQL 資料倉儲沒有目前尚不會自動建立，而且，更新統計資料，像是可能來自 tooexpect Azure SQL Database 中的，閱讀我們的文章[統計資料][ Statistics]可能是其中一種 hello最重要的文件閱讀 tooensure，您會得到 hello 最佳效能從您的查詢。

## <a name="temporary-tables"></a>暫存資料表
暫存資料表是只針對 hello 期間您的登入存在，並且無法看到其他使用者的資料表。  暫存資料表可以其他人看到的暫存結果是適合 tooprevent 和也會減少 hello 需要清理。  由於暫存資料表也會使用本機儲存體，所以可為某些作業提供更快的效能。  請參閱 hello[暫存資料表][ Temporary]如需有關暫存資料表的發行項。

## <a name="external-tables"></a>外部資料表
外部資料表，也稱為 Polybase 資料表，是可從 SQL 資料倉儲，但點 toodata 外部從 SQL 資料倉儲查詢的資料表。  例如，您可以建立外部資料表的點 toofiles Azure Blob 儲存體上。  如需有關如何 toocreate 及查詢外部資料表，請參閱[載入資料，使用 Polybase][Load data with Polybase]。  

## <a name="unsupported-table-features"></a>不支援的資料表功能
雖然 SQL 資料倉儲包含許多 hello 其他資料庫所提供的相同功能的資料表，有一些功能並不支援。  以下是一些 hello 一份資料表尚未支援的功能。

| 不支援的功能 |
| --- |
| 主索引鍵、外部索引鍵、唯一和檢查[資料表條件約束][Table Constraints] |
| [唯一索引][Unique Indexes] |
| [計算資料行][Computed Columns] |
| [疏鬆資料行][Sparse Columns] |
| [使用者定義的類型][User-Defined Types] |
| [順序][Sequence] |
| [觸發程序][Triggers] |
| [索引檢視表][Indexed Views] |
| [同義字][Synonyms] |

## <a name="table-size-queries"></a>資料表大小查詢
一個簡單的方式 tooidentify 空間和中的 hello 60 發佈的每個資料表所耗用的資料列是 toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED]。

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

不過，使用 DBCC 命令相當受限。  動態管理檢視 (Dmv) 可讓您 toosee 更詳細說明，以及可讓您更大的掌控 hello 查詢結果。  從許多我們的範例建立此檢視中，將會參考的 tooby，在此範例與其他文件開始。

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>資料表空間摘要
此查詢會傳回依資料表 hello 資料列和空間。  它是很好的查詢 toosee 哪一個資料表是最大的資料表，以及他們是否已循環配置資源，複製或散佈的雜湊。  分散式的雜湊表也會顯示 hello 散發資料行。  在大部分情況下，最大的資料表應該是具有叢集資料行存放區索引的雜湊散發資料表。

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>依散發類型的資料表空間
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>依索引類型的資料表空間
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>散發空間摘要
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，請參閱 hello 文件上[資料表資料類型][Data Types]，[散發資料表][Distribute]， [的資料表建立索引][ Index]，[分割資料表][Partition]，[維護資料表統計資料][ Statistics]和[暫存資料表][Temporary]。  若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。

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
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
