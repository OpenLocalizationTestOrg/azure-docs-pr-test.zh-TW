---
title: "SQL 資料倉儲中的 aaaIndexing 資料表 |Microsoft Azure"
description: "開始在 Azure SQL 資料倉儲中編製資料表的索引"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>在 SQL 資料倉儲中編製資料表的索引
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

SQL 資料倉儲提供數個索引選項，包括[叢集資料行存放區索引][clustered columnstore indexes]、[叢集索引和非叢集索引][clustered indexes and nonclustered indexes]。  此外，它也提供一個索引選項，也稱為[堆積][heap]。  本文涵蓋的每個索引類型的 hello 優點，以及您的索引超出最高效能的秘訣 toogetting hello。 請參閱[建立資料表語法][ create table syntax]如需詳細資訊，如何 toocreate SQL 資料倉儲中的資料表。

## <a name="clustered-columnstore-indexes"></a>叢集資料行存放區索引
根據預設，若未在資料表上指定任何索引選項，則 SQL 資料倉儲會建立叢集資料行存放區索引。 叢集資料行存放區資料表，提供兩個 hello 最高等級的資料壓縮為 hello 最佳的整體查詢效能。  叢集資料行存放區資料表通常會優於叢集的索引或堆積資料表，和通常是 hello 最好的選擇對於大型資料表。  基於這些理由，叢集資料行存放區時，最佳的地方 toostart hello 您不確定如何 tooindex 您的資料表。  

toocreate 叢集資料行存放區資料表，只要在 hello WITH 子句中指定的叢集資料行存放區索引，或保持關閉狀態 hello WITH 子句：

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

在有些情況下，叢集資料行存放區可能不是很好的選擇︰

* 資料行存放區資料表不支援 varchar(max)、nvarchar(max) 和 varbinary(max)。  請改為考慮堆積或叢集索引。
* 資料行存放區資料表可能比暫時性資料沒有效率。  請考慮堆積，甚至是暫時性資料表。
* 具有少於 1 億個資料列的小型資料表。  請考慮堆積資料表。

## <a name="heap-tables"></a>堆積資料表
當您暫時包括登陸 SQL 資料倉儲上的資料時，您可能會發現使用堆積的資料表會進行更快 hello 整體程序。  這是因為載入 tooheaps 會比 tooindex 資料表更快，且在某些情況下 hello 後續讀取進行從快取。  如果您載入它之前執行多個轉換、 載入 hello tooheap 資料表將會比載入 hello 資料 tooa 快很多的資料只有 toostage 叢集資料行存放區資料表。 此外，載入資料 tooa[暫存資料表][ Temporary]也將載入速度比將載入資料表 toopermanent 儲存體。  

若為小於 1 億個資料列的小型查閱資料表，堆積資料表通常比較適合。  超過 100 百萬個資料列之後，叢集資料行存放區資料表會立即 tooachieve 最佳的壓縮。

toocreate 堆積資料表，只要指定堆積 hello WITH 子句中：

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>叢集與非叢集索引
叢集的索引的單一資料列需要 toobe 快速擷取時，可能會優於叢集資料行存放區資料表。  查詢是單一或很少的資料列查閱的叢集索引或非叢集的次要索引，請考慮需要的 tooperformance 極端的速度。  hello 缺點 toousing 叢集索引是無益 hello 叢集的索引資料行上使用選擇性很高的篩選條件的查詢。  非叢集索引可以是其他資料行上的 tooimprove 篩選器加入 tooother 資料行。  不過，它會加入 tooa 資料表每個索引會增加空間和處理時間 tooloads。

toocreate 叢集的索引的資料表，只需指定 hello WITH 子句中的叢集索引：

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd 非叢集索引在資料表中，只要使用 hello，請使用下列語法：

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>最佳化叢集資料行存放區索引
叢集資料行存放區資料表會將資料組織成不同區段。  擁有高品質的高區段是資料行存放區資料表上的重要 tooachieving 達到最佳查詢效能。  依資料列壓縮的資料列群組中的 hello 數目，您可以測量區段品質。  區段品質最好是在最有至少 100 K 每個壓縮的資料列的資料列群組，並取得效能，因為 hello 每一列數目資料列群組方法 1,048,576 個資料列，也就是 hello 大部分的資料列群組可以包含的資料列。

檢視下方的 hello 可建立及使用您的系統 toocompute hello 上每個資料列的平均資料列群組，並識別任何的次佳的叢集資料行存放區索引。  您的索引時，將會當做 SQL 陳述式可以是使用的 toorebuild 產生 hello 此檢視表的最後一個資料行。

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

既然您已經建立 hello 檢視，執行此查詢 tooidentify 資料表具有小於 100 萬個資料列的資料列群組。  當然，您可能想 100k tooincrease hello 臨界值，如果您要尋找更多區段最佳品質。 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

一旦執行 hello 查詢您可以開始在 hello 資料 toolook 及分析您的結果。 下表說明哪些 toolook 為您的資料列群組分析。

| 資料欄 | 如何 toouse 這項資料 |
| --- | --- |
| [table_partition_count] |如果 hello 資料表已分割，則您可能預期 toosee 較高的開啟資料列群組計數。 Hello 發佈中的每個資料分割理論上可以有與其相關聯的開啟的資料列群組。 將這個因素納入您的分析。 小型資料表已分割，無法藉由移除資料分割完全，因為這樣做會改善壓縮 hello 最佳化。 |
| [row_count_total] |Hello 資料表的總計資料列計數。 例如，您可以使用此值 toocalculate 百分比的資料列在 hello 壓縮狀態。 |
| [row_count_per_distribution_MAX] |如果所有資料列平均分散於這個值會是每個發佈的資料列的 hello 目標數目。 比較此值與 hello compressed_rowgroup_count。 |
| [COMPRESSED_rowgroup_rows] |Hello 資料表的資料行存放區格式中的資料列總數。 |
| [COMPRESSED_rowgroup_rows_AVG] |如果 hello 平均資料列數目會大幅小於 hello 最大資料列群組的資料列數目，請考慮使用 CTAS 或 ALTER INDEX REBUILD toorecompress hello 資料 |
| [COMPRESSED_rowgroup_count] |資料行存放區格式中的資料列群組數目。 如果這個數字已經很高的關聯 toohello 資料表中則 hello 資料行存放區密度是低的指標。 |
| [COMPRESSED_rowgroup_rows_DELETED] |資料行存放區格式中的資料列會以邏輯方式刪除。 如果 hello 數字很高的相對 tootable 大小，請考慮重新建立 hello 磁碟分割或重建 hello 索引，因為它實際上會加以移除。 |
| [COMPRESSED_rowgroup_rows_MIN] |將此選項搭配 hello 平均和最大資料行 toounderstand hello 範圍的值用於 hello 在您的資料行存放區中的資料列群組。 低的數字，透過 hello 載入閾值 (每個分割區對齊發佈 102400) 建議最佳化位於 hello 資料載入 |
| [COMPRESSED_rowgroup_rows_MAX] |同上。 |
| [OPEN_rowgroup_count] |開放資料列群組都正常。 每個資料表散發都應該有一個開放資料列群組 (60)。 過多的數目表示資料跨分割載入。 資料分割策略 toomake 確定它是音效檢查 hello |
| [OPEN_rowgroup_rows] |每個資料列群組可以有最多 1,048,576 個資料列。 使用此值 toosee 滿 hello 開啟的資料列群組目前是 |
| [OPEN_rowgroup_rows_MIN] |開啟 [群組]，表示資料是 trickle 載入 hello 資料表或是的 hello 上次載入溢出到此資料列群組的其餘資料列。 使用 hello MIN、 MAX、 AVG 資料行 toosee 多少資料坐在開啟的資料列群組中。 用於小型資料表，它可能是 100%的 hello 的所有資料 ！ 在此情況下 ALTER INDEX REBUILD tooforce hello 資料 toocolumnstore。 |
| [OPEN_rowgroup_rows_MAX] |同上。 |
| [OPEN_rowgroup_rows_AVG] |同上。 |
| [CLOSED_rowgroup_rows] |查看 hello 關閉資料列群組資料列是例行性檢查。 |
| [CLOSED_rowgroup_count] |hello 已關閉的資料列群組的數目應該很小，如果任何完全看到的。 已關閉的資料列群組可以是轉換的 toocompressed rowg roups 使用 hello ALTER INDEX...REORGANISE 命令。 不過，通常並不需要。 已關閉的群組會自動轉換的 toocolumnstore hello 背景"tuple mover"處理序的資料列群組。 |
| [CLOSED_rowgroup_rows_MIN] |關閉資料列群組應該具有極高的填滿率。 如果已關閉的資料列群組的 hello 填滿速率過低時，進一步的分析 hello 資料行存放區則需要。 |
| [CLOSED_rowgroup_rows_MAX] |同上。 |
| [CLOSED_rowgroup_rows_AVG] |同上。 |
| [Rebuild_Index_SQL] |為資料表的 SQL toorebuild 資料行存放區索引 |

## <a name="causes-of-poor-columnstore-index-quality"></a>資料行存放區索引品質不佳的原因
如果您已識別的資料表具有品質不佳的區段，您會想 tooidentify hello 根本原因。  以下是區段品質不佳的一些其他常見原因︰

1. 建立索引時的記憶體壓力
2. 大量的 DML 作業
3. 小型或緩慢移動的載入作業
4. 太多資料分割

這些因素可能會導致資料行存放區索引 toohave 大幅少於 hello 最佳 1 百萬個資料列，每個資料列群組。  它們也可能導致資料列 toogo toohello 差異資料列群組而不是壓縮的資料列群組。 

### <a name="memory-pressure-when-index-was-built"></a>建立索引時的記憶體壓力
hello 每個壓縮的資料列群組的資料列數目會直接相關的 toohello hello 資料列的寬度和 hello 可用 tooprocess hello 資料列群組的記憶體數量。  當資料列寫 toocolumnstore 資料表，記憶體不足的壓力時，資料行存放區區段品質可能會降低。  因此，hello 最佳作法是只寫入 tooyour 資料行存放區索引的資料表存取 tooas 太多記憶體中的盡可能 toogive hello 工作階段。  因為沒有記憶體和並行存取之間的取捨，hello 指引 hello 右記憶體配置取決於 hello 每一個資料列的資料表時，hello 數量 DWU 您所配置的 tooyour 系統和並行的 hello 數量位置，您可以提供 toohello這撰寫 tooyour 資料表的工作階段。  最佳做法，建議您啟動 xlargerc，如果您使用 DW300 或更少，largerc，如果您使用 DW400 tooDW600 和 mediumrc 如果您使用 DW1000 和更新版本。

### <a name="high-volume-of-dml-operations"></a>大量的 DML 作業
大量更新及刪除資料列的 DML 作業可能效率不彰引入 hello 資料行存放區。 當您修改 hello 多數 hello 中的資料列的資料列群組時，這是特別有用。

* 為已刪除，只以邏輯方式刪除資料列從壓縮的資料列群組標示 hello 資料列。 重建 hello 分割區或資料表之前，hello 資料列會保留在 hello 壓縮的資料列群組。
* 插入資料列加入稱為差異資料列群組的 hello 列 tootooan 內部資料列存放區資料表。 hello 插入資料列才轉換的 toocolumnstore hello 差異資料列群組已滿，而且會標記為關閉。 一旦到達 hello 1,048,576 個資料列最大容量，會關閉資料列群組。 
* 更新資料行存放區格式的資料列會做為邏輯刪除和插入來處理。 hello 插入資料列可能會儲存在 hello 差異存放區中。

批次更新和插入超過 hello 大量臨界值的每個資料分割對齊的發佈將會直接 toohello 資料行存放區格式寫入 102,400 個資料列的作業。 不過，假設平均分佈，您必須修改此 toooccur 的單一作業中的多個 6.144 百萬個資料列的 toobe。 如果給定資料分割的資料列的 hello 數對齊發佈是小於 102400 hello 資料列將會移 toohello 差異存放區，而會留在那裡直到足夠的資料列已插入或修改的 tooclose hello 資料列群組或 hello 索引後，已重建。

### <a name="small-or-trickle-load-operations"></a>小型或緩慢移動的載入作業
流入 SQL 資料倉儲的小型負載，有時也稱為緩慢移動的負載。 它們通常代表 hello 系統的 內嵌在資料附近常數資料流。 不過，因為這個資料流是附近連續 hello 磁碟區的資料列不是特別大。 通常 hello 資料低於大幅 hello 閾值所需的直接載入 toocolumnstore 格式。

在這些情況下，它通常是更好的 tooland hello 資料第一次在 Azure blob 儲存體，並讓它累積先前 tooloading。 這項技術通常稱為 *微批次處理*。

### <a name="too-many-partitions"></a>太多資料分割
另一件事 tooconsider 是 hello 影響您的叢集資料行存放區資料表上的分割區。  資料分割之前，SQL 資料倉儲已將您的資料分成 60 個資料庫。  進一步分割會分割您的資料。  如果分割資料，則您會想 tooconsider，**每個**磁碟分割將需要 toohave 至少 1 百萬個資料列 toobenefit 從叢集資料行存放區索引。  如果您您資料表分割成多 100 個資料分割，則您的資料表必須從叢集資料行存放區索引的 toohave 至少 6 10 億個資料列 toobenefit (60 分佈 * 100 個資料分割 * 1 百萬個資料列)。 如果 100 的資料分割資料表並沒有 6 10 億個資料列，減少 hello 資料分割數目，或請考慮改用堆積資料表。

一旦使用某些資料已載入您的資料表，請遵循以下步驟 tooidentify hello，並重建具有次佳的叢集資料行存放區索引的資料表。

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>重建索引 tooimprove 區段品質
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>步驟 1： 識別或建立使用者使用 hello 右資源類別
Tooimmediately 改善區段品質的一個快速方法是 toorebuild hello 索引。  hello hello 檢視上方所傳回的 SQL 會傳回您的索引可以是使用的 toorebuild 的 ALTER INDEX REBUILD 陳述式。  請確定您配置足夠記憶體 toohello 工作階段，這將會重建索引時重建您的索引。  toodo，增加 hello 資源的類別權限 toorebuild hello 索引對此資料表 toohello 建議最小值的使用者。  無法變更 hello 資料庫擁有者使用者 hello 資源類別，因此如果您沒有 hello 系統上建立使用者，您必須 toodo 因此第一次。  我們建議的 hello 至少是 xlargerc 如果您使用 DW300 或較少 largerc 如果您使用 DW400 tooDW600 和 mediumrc 如果您使用 DW1000 和更新版本。

以下是如何的範例 tooallocate 更多記憶體 tooa 使用者藉由增加其資源類別。  如需有關資源類別，以及如何 toocreate 新的使用者可以在 hello[並行存取，以及工作負載管理][ Concurrency]發行項。

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>步驟 2︰使用較高的資源類別使用者重建叢集資料行存放區索引
Hello 使用者步驟 1 中 (例如 LoadUser) 現在使用較高的資源類別，並執行 hello ALTER INDEX 陳述式，以登入。  請確定此使用者擁有 ALTER 權限 toohello 表正在重建 hello 索引時。  下列範例將示範如何 toorebuild hello 整個資料行存放區索引，或如何 toorebuild 單一磁碟分割。 在大型資料表時，這會是一次的單一資料分割的實際 toorebuild 索引。

或者，而不會重建 hello 索引，您無法複製 hello 資料表 tooa 新資料表使用[CTAS][CTAS]。  哪一種方式最好？ 針對大量的資料，[CTAS][CTAS] 的速度通常比 [ALTER INDEX][ALTER INDEX] 來得快。 對於較小的磁碟區的資料， [ALTER INDEX] [ ALTER INDEX]是更容易 toouse，不需要您 tooswap 移出 hello 資料表。  請參閱**CTAS 和資料分割切換以重建索引**下方如需有關 toorebuild CTAS 搭配的索引。

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

在 SQL 資料倉儲中重建索引是一項離線作業。  如需重建索引的詳細資訊，請參閱 ALTER INDEX REBUILD 一節中的 hello[資料行存放區索引重組][ Columnstore Indexes Defragmentation]與 hello 語法主題[ALTER INDEX][ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>步驟 3︰確認已改善叢集資料行存放區區段品質
請重新執行 hello 查詢不良以識別資料表區段品質，並確認區段品質已改善。  如果區段品質無法改善，可能是資料表中的 hello 資料列會額外寬。  請考慮在重建索引時使用較高的資源類別或 DWU。

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>使用 CTAS 和分割切換重建索引
這個範例會使用[CTAS] [ CTAS]和資料分割切換 toorebuild 的資料表資料分割。 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
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
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
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
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

如需詳細資訊重新建立資料分割使用`CTAS`，請參閱 hello[分割][ Partition]發行項。

## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[分割資料表][Partition]，[維護資料表統計資料][ Statistics]和[暫存資料表][Temporary]。  toolearn 深入了解最佳做法，請參閱[SQL 資料倉儲的最佳作法][SQL Data Warehouse Best Practices]。

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
