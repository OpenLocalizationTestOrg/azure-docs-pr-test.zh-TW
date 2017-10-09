---
title: "在 Azure SQL aaaImprove 資料行存放區索引效能 |Microsoft 文件"
description: "降低記憶體需求或 hello 可用記憶體 toomaximize hello 數目增加到每個資料列群組壓縮的資料行存放區索引的資料列。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>最大化資料行存放區的資料列群組品質

資料列群組品質取決於 hello 資料列群組中的資料列數目。 降低記憶體需求或 hello 可用記憶體 toomaximize hello 數目增加到每個資料列群組壓縮的資料行存放區索引的資料列。  使用這些方法 tooimprove 壓縮率和查詢效能的資料行存放區索引。

## <a name="why-hello-rowgroup-size-matters"></a>為什麼 hello 資料列群組大小問題
因為資料行存放區索引掃描的個別資料列群組的資料行區段掃描的資料表，最大化的每個資料列群組中的資料列的 hello 數目可以提升查詢效能。 當資料列群組有大量的資料列時，可改善資料壓縮，表示從磁碟較少資料 tooread。

如需關於資料列群組的詳細資訊，請參閱[資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)。

## <a name="target-size-for-rowgroups"></a>資料列群組的目標大小
為了達到最佳查詢效能，hello 目標是每個資料列群組資料行存放區索引中的資料列的 toomaximize hello 數目。 一個資料列群組最多可有 1,048,576 個資料列。 它的關係 toonot 有 hello 的每個資料列群組資料列數目上限。 當資料列群組擁有至少 100,000 個資料列時，資料行存放區索引會獲得良好效能。

## <a name="rowgroups-can-get-trimmed-during-compression"></a>資料列群組可以在壓縮期間進行修剪

大量載入或資料行存放區索引重建時，有時也沒有足夠記憶體可用 toocompress 所有 hello 指定每個資料列群組的資料列。 記憶體不足的壓力時，資料行存放區索引會修剪 hello 資料列群組大小，因此壓縮成 hello 資料行存放區可以成功。 

記憶體不足，無法 toocompress 至少 10,000 資料列插入每個資料列群組時，SQL 資料倉儲會產生錯誤。

如需有關大量載入的詳細資訊，請參閱[大量載入叢集資料行存放區索引](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)。

## <a name="how-toomonitor-rowgroup-quality"></a>如何 toomonitor rowgroup 品質

沒有公開實用資訊，例如資料列群組和 hello 修剪原因中資料列數目，如果有已修剪的 DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats)。 您可以調整資料列群組上建立 hello 下列便利的方式 tooquery 以檢視此 DMV tooget 資訊。

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

hello trim_reason_desc 告訴 hello 資料列群組是否已修剪 (trim_reason_desc = NO_TRIM 意味著時發生無修剪，且最佳品質的資料列群組)。 hello 修剪原因表示過早修剪的 hello 資料列群組：
- 大量載入： Hello 傳入 hello 負載的資料列批次在小於 1 百萬個資料列，會使用這個修剪原因。 如果有超過 100,000 （做為 hello 差異存放區相對於 tooinserting) 正在插入的資料列但集 hello 修剪原因 tooBULKLOAD hello 引擎會建立壓縮的資料列群組。 在此案例中，請考慮增加您的批次載入視窗 tooaccumulate 多個資料列。 此外，重新評估您為資料列群組不能跨越資料分割界限並不太精細的資料分割配置 tooensure。
- MEMORY_LIMITATION: hello 引擎需要 toocreate 1 百萬個資料列，工作記憶體數量的資料列群組。 當載入工作階段的 hello 的可用記憶體少於 hello 所需工作記憶體，取得提前修剪資料列群組。 hello 下列各節說明方式 tooestimate 記憶體需要配置更多記憶體。
- DICTIONARY_SIZE：這個修剪原因表示因為至少有一個字串資料行具有寬/或高基數字串而發生資料列群組修剪。 hello 字典大小為有限的 too16 MB 記憶體中，而且一旦 hello 資料列群組達到這個限制壓縮檔。 如果您執行到這種情況下，請考慮 hello 有問題的資料行隔離到個別的資料表。

## <a name="how-tooestimate-memory-requirements"></a>如何 tooestimate 記憶體需求

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

大約是 hello 所需的最大記憶體 toocompress 一個資料列群組

- 72 MB +
- \#資料列 \* \#資料行 \* 8 個位元組 +
- \#資料列 \* \#短字串資料行 \* 32 個位元組 +
- \#長字串資料行 \* 壓縮字典 16 MB

短字串資料行使用 < = 32 個位元組的字串資料類型和長字串資料行使用 > 32 個位元組的字串資料類型。

會使用專為壓縮文字的壓縮方法來壓縮長字串。 這個壓縮方法會使用*字典*toostore 文字模式。 hello 字典的大小上限是 16 MB。 沒有 hello 資料列群組中每一個長字串資料行只有一個字典。

如需資料行存放區記憶體需求的深入討論，請參閱影片 [Azure SQL 資料倉儲調整︰組態和指引](https://myignite.microsoft.com/videos/14822)。

## <a name="ways-tooreduce-memory-requirements"></a>方式 tooreduce 記憶體需求

使用下列技巧 tooreduce hello 資料列群組壓縮至資料行存放區索引的記憶體需求的 hello。

### <a name="use-fewer-columns"></a>使用較少的資料行
可能的話，請設計 hello 具有較少的資料行的資料表。 當資料列群組壓縮成 hello 資料行存放區時，hello 資料行存放區索引會個別壓縮每個資料行區段。 因此 hello toocompress 資料列群組會增加為 hello 數目的資料行增加記憶體需求。


### <a name="use-fewer-string-columns"></a>使用較少的字串資料行
字串資料類型的資料行比數字和日期資料類型需要更多的記憶體。 tooreduce 記憶體需求，請考慮移除事實資料表中的字串資料行，並放在較小的維度資料表中。

字串壓縮的其他記憶體需求︰

- 向上 too32 字元字串資料類型可能需要每個值 32 額外的位元組。
- 使用超過 32 個字元的字串資料類型會使用字典方法進行壓縮。  Hello 資料列群組中的每個資料行可能需要向上 tooan 其他 16 MB toobuild hello 字典。

### <a name="avoid-over-partitioning"></a>避免過度分割

資料行存放區索引針對每個資料分割會建立一個或多個資料列群組。 在 SQL 資料倉儲中，快速的資料分割的 hello 數目成長因為 hello 資料分佈，而分割每個發佈。 Hello 資料表有太多資料分割，如果可能不會有足夠的資料列 toofill hello 資料列群組。 hello 缺少的資料列不會建立在壓縮期間，記憶體不足的壓力，但它會導致無法達到 hello 最佳資料行存放區查詢效能的 toorowgroups。

另一個原因 tooavoid 過度分割是記憶體額外負荷資料列載入分割區資料表上的資料行存放區索引。 在載入期間，許多資料分割可能會收到 hello 內送資料列，這會保留在記憶體中，直到每個分割區有足夠的資料列 toobe 壓縮。 具有太多資料分割會建立額外的記憶體不足壓力。

### <a name="simplify-hello-load-query"></a>簡化查詢 hello 載入

hello 資料庫共用 hello hello 查詢中的所有 hello 運算子之間的查詢記憶體授權。 當查詢載入具有複雜的排序和聯結時，會減少 hello 適用於壓縮的記憶體。

設計 hello 負載查詢 toofocus 只能在載入 hello 查詢。 如果您需要 toorun 轉換 hello 資料上的，執行這些分開 hello 負載查詢。 例如，階段 hello 在堆積的資料表中，執行資料 hello 轉換，並且再載入 hello 暫存 hello 資料行存放區索引的資料表。 您可以也 hello 資料載入第一次，然後使用 hello MPP 系統 tootransform hello 資料。

### <a name="adjust-maxdop"></a>調整 MAXDOP

每個發佈到平行的 hello 資料行存放區壓縮資料列群組時可用的每個發佈一個以上的 CPU 核心。 hello 平行處理原則需要額外的記憶體資源，可能會導致 toomemory 不足的壓力和資料列群組的修剪。

tooreduce 記憶體不足的壓力，您可以使用 hello MAXDOP 查詢提示 tooforce hello 負載作業 toorun 在序列中每個發佈的模式。

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>方式 tooallocate 更多記憶體

DWU 大小和 hello 使用者資源類別一起判斷多少記憶體可供使用者查詢。 tooincrease hello 記憶體授與負載查詢，您可以增加 hello Dwu 數目，或增加 hello 資源類別。

- tooincrease hello dwu 調整，請參閱[如何調整效能？](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- toochange hello 資源類別可用於查詢時，請參閱[變更使用者資源類別範例](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。

例如，在 DWU 100 hello smallrc 資源類別中的使用者可以使用 100 MB 的記憶體的每個散發。 Hello 的詳細資訊，請參閱[SQL 資料倉儲中的並行存取](sql-data-warehouse-develop-concurrency.md)。

假設您決定您需要 700 MB 的記憶體 tooget 高品質的資料列群組大小。 這些範例說明如何執行查詢 hello 載入具有足夠的記憶體。

- 使用 DWU 1000 和 mediumrc，記憶體授權為 800 MB
- 使用 DWU 600 和 largerc，記憶體授權為 800 MB。


## <a name="next-steps"></a>後續步驟

toofind 更方式 tooimprove 高效能在 SQL 資料倉儲中，請參閱 hello[效能概觀](sql-data-warehouse-overview-manage-user-queries.md)。

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
