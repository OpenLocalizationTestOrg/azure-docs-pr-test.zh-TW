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
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="7b735-103">最大化資料行存放區的資料列群組品質</span><span class="sxs-lookup"><span data-stu-id="7b735-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="7b735-104">資料列群組品質取決於 hello 資料列群組中的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="7b735-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="7b735-105">降低記憶體需求或 hello 可用記憶體 toomaximize hello 數目增加到每個資料列群組壓縮的資料行存放區索引的資料列。</span><span class="sxs-lookup"><span data-stu-id="7b735-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="7b735-106">使用這些方法 tooimprove 壓縮率和查詢效能的資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7b735-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="7b735-107">為什麼 hello 資料列群組大小問題</span><span class="sxs-lookup"><span data-stu-id="7b735-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="7b735-108">因為資料行存放區索引掃描的個別資料列群組的資料行區段掃描的資料表，最大化的每個資料列群組中的資料列的 hello 數目可以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="7b735-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="7b735-109">當資料列群組有大量的資料列時，可改善資料壓縮，表示從磁碟較少資料 tooread。</span><span class="sxs-lookup"><span data-stu-id="7b735-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="7b735-110">如需關於資料列群組的詳細資訊，請參閱[資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7b735-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="7b735-111">資料列群組的目標大小</span><span class="sxs-lookup"><span data-stu-id="7b735-111">Target size for rowgroups</span></span>
<span data-ttu-id="7b735-112">為了達到最佳查詢效能，hello 目標是每個資料列群組資料行存放區索引中的資料列的 toomaximize hello 數目。</span><span class="sxs-lookup"><span data-stu-id="7b735-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="7b735-113">一個資料列群組最多可有 1,048,576 個資料列。</span><span class="sxs-lookup"><span data-stu-id="7b735-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="7b735-114">它的關係 toonot 有 hello 的每個資料列群組資料列數目上限。</span><span class="sxs-lookup"><span data-stu-id="7b735-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="7b735-115">當資料列群組擁有至少 100,000 個資料列時，資料行存放區索引會獲得良好效能。</span><span class="sxs-lookup"><span data-stu-id="7b735-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="7b735-116">資料列群組可以在壓縮期間進行修剪</span><span class="sxs-lookup"><span data-stu-id="7b735-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="7b735-117">大量載入或資料行存放區索引重建時，有時也沒有足夠記憶體可用 toocompress 所有 hello 指定每個資料列群組的資料列。</span><span class="sxs-lookup"><span data-stu-id="7b735-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="7b735-118">記憶體不足的壓力時，資料行存放區索引會修剪 hello 資料列群組大小，因此壓縮成 hello 資料行存放區可以成功。</span><span class="sxs-lookup"><span data-stu-id="7b735-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="7b735-119">記憶體不足，無法 toocompress 至少 10,000 資料列插入每個資料列群組時，SQL 資料倉儲會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b735-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="7b735-120">如需有關大量載入的詳細資訊，請參閱[大量載入叢集資料行存放區索引](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)。</span><span class="sxs-lookup"><span data-stu-id="7b735-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="7b735-121">如何 toomonitor rowgroup 品質</span><span class="sxs-lookup"><span data-stu-id="7b735-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="7b735-122">沒有公開實用資訊，例如資料列群組和 hello 修剪原因中資料列數目，如果有已修剪的 DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats)。</span><span class="sxs-lookup"><span data-stu-id="7b735-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="7b735-123">您可以調整資料列群組上建立 hello 下列便利的方式 tooquery 以檢視此 DMV tooget 資訊。</span><span class="sxs-lookup"><span data-stu-id="7b735-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="7b735-124">hello trim_reason_desc 告訴 hello 資料列群組是否已修剪 (trim_reason_desc = NO_TRIM 意味著時發生無修剪，且最佳品質的資料列群組)。</span><span class="sxs-lookup"><span data-stu-id="7b735-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="7b735-125">hello 修剪原因表示過早修剪的 hello 資料列群組：</span><span class="sxs-lookup"><span data-stu-id="7b735-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="7b735-126">大量載入： Hello 傳入 hello 負載的資料列批次在小於 1 百萬個資料列，會使用這個修剪原因。</span><span class="sxs-lookup"><span data-stu-id="7b735-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="7b735-127">如果有超過 100,000 （做為 hello 差異存放區相對於 tooinserting) 正在插入的資料列但集 hello 修剪原因 tooBULKLOAD hello 引擎會建立壓縮的資料列群組。</span><span class="sxs-lookup"><span data-stu-id="7b735-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="7b735-128">在此案例中，請考慮增加您的批次載入視窗 tooaccumulate 多個資料列。</span><span class="sxs-lookup"><span data-stu-id="7b735-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="7b735-129">此外，重新評估您為資料列群組不能跨越資料分割界限並不太精細的資料分割配置 tooensure。</span><span class="sxs-lookup"><span data-stu-id="7b735-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="7b735-130">MEMORY_LIMITATION: hello 引擎需要 toocreate 1 百萬個資料列，工作記憶體數量的資料列群組。</span><span class="sxs-lookup"><span data-stu-id="7b735-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="7b735-131">當載入工作階段的 hello 的可用記憶體少於 hello 所需工作記憶體，取得提前修剪資料列群組。</span><span class="sxs-lookup"><span data-stu-id="7b735-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="7b735-132">hello 下列各節說明方式 tooestimate 記憶體需要配置更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="7b735-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="7b735-133">DICTIONARY_SIZE：這個修剪原因表示因為至少有一個字串資料行具有寬/或高基數字串而發生資料列群組修剪。</span><span class="sxs-lookup"><span data-stu-id="7b735-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="7b735-134">hello 字典大小為有限的 too16 MB 記憶體中，而且一旦 hello 資料列群組達到這個限制壓縮檔。</span><span class="sxs-lookup"><span data-stu-id="7b735-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="7b735-135">如果您執行到這種情況下，請考慮 hello 有問題的資料行隔離到個別的資料表。</span><span class="sxs-lookup"><span data-stu-id="7b735-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="7b735-136">如何 tooestimate 記憶體需求</span><span class="sxs-lookup"><span data-stu-id="7b735-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="7b735-137">大約是 hello 所需的最大記憶體 toocompress 一個資料列群組</span><span class="sxs-lookup"><span data-stu-id="7b735-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="7b735-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="7b735-138">72 MB +</span></span>
- <span data-ttu-id="7b735-139">\#資料列 \* \#資料行 \* 8 個位元組 +</span><span class="sxs-lookup"><span data-stu-id="7b735-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="7b735-140">\#資料列 \* \#短字串資料行 \* 32 個位元組 +</span><span class="sxs-lookup"><span data-stu-id="7b735-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="7b735-141">\#長字串資料行 \* 壓縮字典 16 MB</span><span class="sxs-lookup"><span data-stu-id="7b735-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="7b735-142">短字串資料行使用 < = 32 個位元組的字串資料類型和長字串資料行使用 > 32 個位元組的字串資料類型。</span><span class="sxs-lookup"><span data-stu-id="7b735-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="7b735-143">會使用專為壓縮文字的壓縮方法來壓縮長字串。</span><span class="sxs-lookup"><span data-stu-id="7b735-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="7b735-144">這個壓縮方法會使用*字典*toostore 文字模式。</span><span class="sxs-lookup"><span data-stu-id="7b735-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="7b735-145">hello 字典的大小上限是 16 MB。</span><span class="sxs-lookup"><span data-stu-id="7b735-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="7b735-146">沒有 hello 資料列群組中每一個長字串資料行只有一個字典。</span><span class="sxs-lookup"><span data-stu-id="7b735-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="7b735-147">如需資料行存放區記憶體需求的深入討論，請參閱影片 [Azure SQL 資料倉儲調整︰組態和指引](https://myignite.microsoft.com/videos/14822)。</span><span class="sxs-lookup"><span data-stu-id="7b735-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="7b735-148">方式 tooreduce 記憶體需求</span><span class="sxs-lookup"><span data-stu-id="7b735-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="7b735-149">使用下列技巧 tooreduce hello 資料列群組壓縮至資料行存放區索引的記憶體需求的 hello。</span><span class="sxs-lookup"><span data-stu-id="7b735-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="7b735-150">使用較少的資料行</span><span class="sxs-lookup"><span data-stu-id="7b735-150">Use fewer columns</span></span>
<span data-ttu-id="7b735-151">可能的話，請設計 hello 具有較少的資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="7b735-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="7b735-152">當資料列群組壓縮成 hello 資料行存放區時，hello 資料行存放區索引會個別壓縮每個資料行區段。</span><span class="sxs-lookup"><span data-stu-id="7b735-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="7b735-153">因此 hello toocompress 資料列群組會增加為 hello 數目的資料行增加記憶體需求。</span><span class="sxs-lookup"><span data-stu-id="7b735-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="7b735-154">使用較少的字串資料行</span><span class="sxs-lookup"><span data-stu-id="7b735-154">Use fewer string columns</span></span>
<span data-ttu-id="7b735-155">字串資料類型的資料行比數字和日期資料類型需要更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7b735-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="7b735-156">tooreduce 記憶體需求，請考慮移除事實資料表中的字串資料行，並放在較小的維度資料表中。</span><span class="sxs-lookup"><span data-stu-id="7b735-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="7b735-157">字串壓縮的其他記憶體需求︰</span><span class="sxs-lookup"><span data-stu-id="7b735-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="7b735-158">向上 too32 字元字串資料類型可能需要每個值 32 額外的位元組。</span><span class="sxs-lookup"><span data-stu-id="7b735-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="7b735-159">使用超過 32 個字元的字串資料類型會使用字典方法進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="7b735-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="7b735-160">Hello 資料列群組中的每個資料行可能需要向上 tooan 其他 16 MB toobuild hello 字典。</span><span class="sxs-lookup"><span data-stu-id="7b735-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="7b735-161">避免過度分割</span><span class="sxs-lookup"><span data-stu-id="7b735-161">Avoid over-partitioning</span></span>

<span data-ttu-id="7b735-162">資料行存放區索引針對每個資料分割會建立一個或多個資料列群組。</span><span class="sxs-lookup"><span data-stu-id="7b735-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="7b735-163">在 SQL 資料倉儲中，快速的資料分割的 hello 數目成長因為 hello 資料分佈，而分割每個發佈。</span><span class="sxs-lookup"><span data-stu-id="7b735-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="7b735-164">Hello 資料表有太多資料分割，如果可能不會有足夠的資料列 toofill hello 資料列群組。</span><span class="sxs-lookup"><span data-stu-id="7b735-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="7b735-165">hello 缺少的資料列不會建立在壓縮期間，記憶體不足的壓力，但它會導致無法達到 hello 最佳資料行存放區查詢效能的 toorowgroups。</span><span class="sxs-lookup"><span data-stu-id="7b735-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="7b735-166">另一個原因 tooavoid 過度分割是記憶體額外負荷資料列載入分割區資料表上的資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7b735-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="7b735-167">在載入期間，許多資料分割可能會收到 hello 內送資料列，這會保留在記憶體中，直到每個分割區有足夠的資料列 toobe 壓縮。</span><span class="sxs-lookup"><span data-stu-id="7b735-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="7b735-168">具有太多資料分割會建立額外的記憶體不足壓力。</span><span class="sxs-lookup"><span data-stu-id="7b735-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="7b735-169">簡化查詢 hello 載入</span><span class="sxs-lookup"><span data-stu-id="7b735-169">Simplify hello load query</span></span>

<span data-ttu-id="7b735-170">hello 資料庫共用 hello hello 查詢中的所有 hello 運算子之間的查詢記憶體授權。</span><span class="sxs-lookup"><span data-stu-id="7b735-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="7b735-171">當查詢載入具有複雜的排序和聯結時，會減少 hello 適用於壓縮的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7b735-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="7b735-172">設計 hello 負載查詢 toofocus 只能在載入 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="7b735-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="7b735-173">如果您需要 toorun 轉換 hello 資料上的，執行這些分開 hello 負載查詢。</span><span class="sxs-lookup"><span data-stu-id="7b735-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="7b735-174">例如，階段 hello 在堆積的資料表中，執行資料 hello 轉換，並且再載入 hello 暫存 hello 資料行存放區索引的資料表。</span><span class="sxs-lookup"><span data-stu-id="7b735-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="7b735-175">您可以也 hello 資料載入第一次，然後使用 hello MPP 系統 tootransform hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7b735-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="7b735-176">調整 MAXDOP</span><span class="sxs-lookup"><span data-stu-id="7b735-176">Adjust MAXDOP</span></span>

<span data-ttu-id="7b735-177">每個發佈到平行的 hello 資料行存放區壓縮資料列群組時可用的每個發佈一個以上的 CPU 核心。</span><span class="sxs-lookup"><span data-stu-id="7b735-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="7b735-178">hello 平行處理原則需要額外的記憶體資源，可能會導致 toomemory 不足的壓力和資料列群組的修剪。</span><span class="sxs-lookup"><span data-stu-id="7b735-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="7b735-179">tooreduce 記憶體不足的壓力，您可以使用 hello MAXDOP 查詢提示 tooforce hello 負載作業 toorun 在序列中每個發佈的模式。</span><span class="sxs-lookup"><span data-stu-id="7b735-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="7b735-180">方式 tooallocate 更多記憶體</span><span class="sxs-lookup"><span data-stu-id="7b735-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="7b735-181">DWU 大小和 hello 使用者資源類別一起判斷多少記憶體可供使用者查詢。</span><span class="sxs-lookup"><span data-stu-id="7b735-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="7b735-182">tooincrease hello 記憶體授與負載查詢，您可以增加 hello Dwu 數目，或增加 hello 資源類別。</span><span class="sxs-lookup"><span data-stu-id="7b735-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="7b735-183">tooincrease hello dwu 調整，請參閱[如何調整效能？](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="7b735-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="7b735-184">toochange hello 資源類別可用於查詢時，請參閱[變更使用者資源類別範例](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="7b735-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="7b735-185">例如，在 DWU 100 hello smallrc 資源類別中的使用者可以使用 100 MB 的記憶體的每個散發。</span><span class="sxs-lookup"><span data-stu-id="7b735-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="7b735-186">Hello 的詳細資訊，請參閱[SQL 資料倉儲中的並行存取](sql-data-warehouse-develop-concurrency.md)。</span><span class="sxs-lookup"><span data-stu-id="7b735-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="7b735-187">假設您決定您需要 700 MB 的記憶體 tooget 高品質的資料列群組大小。</span><span class="sxs-lookup"><span data-stu-id="7b735-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="7b735-188">這些範例說明如何執行查詢 hello 載入具有足夠的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7b735-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="7b735-189">使用 DWU 1000 和 mediumrc，記憶體授權為 800 MB</span><span class="sxs-lookup"><span data-stu-id="7b735-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="7b735-190">使用 DWU 600 和 largerc，記憶體授權為 800 MB。</span><span class="sxs-lookup"><span data-stu-id="7b735-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b735-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b735-191">Next steps</span></span>

<span data-ttu-id="7b735-192">toofind 更方式 tooimprove 高效能在 SQL 資料倉儲中，請參閱 hello[效能概觀](sql-data-warehouse-overview-manage-user-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="7b735-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
