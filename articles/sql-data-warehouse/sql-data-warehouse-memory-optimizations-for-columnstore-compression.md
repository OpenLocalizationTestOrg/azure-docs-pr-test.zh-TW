---
title: "改善 Azure SQL 中的資料行存放區索引效能 | Microsoft Docs"
description: "減少記憶體需求或增加可用的記憶體，以最大化壓縮到每個資料列群組之資料行存放區索引的資料列數目。"
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
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="3fa02-103">最大化資料行存放區的資料列群組品質</span><span class="sxs-lookup"><span data-stu-id="3fa02-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="3fa02-104">資料列群組品質取決於資料列群組中的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="3fa02-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="3fa02-105">減少記憶體需求或增加可用的記憶體，以最大化壓縮到每個資料列群組之資料行存放區索引的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="3fa02-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="3fa02-106">使用這些方法來改善壓縮率和查詢資料行存放區索引的效能。</span><span class="sxs-lookup"><span data-stu-id="3fa02-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="3fa02-107">為什麼資料列群組很重要</span><span class="sxs-lookup"><span data-stu-id="3fa02-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="3fa02-108">因為資料行存放區索引會藉由掃描個別資料列群組的資料行區段來掃描資料表，最大化每個資料列群組的資料列數目可以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="3fa02-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="3fa02-109">當資料列群組會有大量的資料列時，可改善資料壓縮，這表示從磁碟讀取的資料比較少。</span><span class="sxs-lookup"><span data-stu-id="3fa02-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="3fa02-110">如需關於資料列群組的詳細資訊，請參閱[資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="3fa02-111">資料列群組的目標大小</span><span class="sxs-lookup"><span data-stu-id="3fa02-111">Target size for rowgroups</span></span>
<span data-ttu-id="3fa02-112">為了達到最佳查詢效能，目標是最大化存放區索引中每個資料行的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="3fa02-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="3fa02-113">一個資料列群組最多可有 1,048,576 個資料列。</span><span class="sxs-lookup"><span data-stu-id="3fa02-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="3fa02-114">每個資料列群組沒有資料列數目上限也沒關係。</span><span class="sxs-lookup"><span data-stu-id="3fa02-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="3fa02-115">當資料列群組擁有至少 100,000 個資料列時，資料行存放區索引會獲得良好效能。</span><span class="sxs-lookup"><span data-stu-id="3fa02-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="3fa02-116">資料列群組可以在壓縮期間進行修剪</span><span class="sxs-lookup"><span data-stu-id="3fa02-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="3fa02-117">在大量載入或資料行存放區索引重建期間，有時可用的記憶體不足，無法壓縮指定給每個資料列群組的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="3fa02-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="3fa02-118">當有記憶體不足的壓力時，資料行存放區索引會修剪資料列群組大小，因此會成功壓縮到資料行存放區內。</span><span class="sxs-lookup"><span data-stu-id="3fa02-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="3fa02-119">當記憶體不足，無法將至少 10,000 個資料列壓縮到每個資料列群組時，SQL 資料倉儲會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3fa02-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="3fa02-120">如需有關大量載入的詳細資訊，請參閱[大量載入叢集資料行存放區索引](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="3fa02-121">如何監視資料列群組品質</span><span class="sxs-lookup"><span data-stu-id="3fa02-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="3fa02-122">有一個 DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) 會公開一些實用資訊，例如資料列群組中的資料列數目，以及如果發生修剪，則修剪原因為何。</span><span class="sxs-lookup"><span data-stu-id="3fa02-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="3fa02-123">您可以建立下列檢視，並將其作為查詢這個 DMV 以取得有關資料列群組修剪資訊的便利方法。</span><span class="sxs-lookup"><span data-stu-id="3fa02-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

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

<span data-ttu-id="3fa02-124">trim_reason_desc 會告知是否已修剪資料列群組 (trim_reason_desc = NO_TRIM 表示沒有修剪，且資料列群組屬於最佳品質)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="3fa02-125">下列修剪原因表示過早修剪了資料列群組：</span><span class="sxs-lookup"><span data-stu-id="3fa02-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="3fa02-126">BULKLOAD：當傳入的負載資料列批次具有少於 1 百萬個的資料列時，會使用這個修剪原因。</span><span class="sxs-lookup"><span data-stu-id="3fa02-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="3fa02-127">如果插入了多於 100,000 個資料列 (而不是插入到差異存放區)，則引擎會建立壓縮的資料列群組，但是會將修剪原因設定為大量載入。</span><span class="sxs-lookup"><span data-stu-id="3fa02-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="3fa02-128">在此情況下，請考慮增加您的批次載入空檔以累積更多資料列。</span><span class="sxs-lookup"><span data-stu-id="3fa02-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="3fa02-129">此外，重新評估您的資料分割配置，確保它不會太過細微，因為資料列群組不能跨越資料分割界限。</span><span class="sxs-lookup"><span data-stu-id="3fa02-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="3fa02-130">MEMORY_LIMITATION：若要建立包含 1 百萬個資料列的資料列群組，引擎會需要特定數量的工作記憶體。</span><span class="sxs-lookup"><span data-stu-id="3fa02-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="3fa02-131">當載入工作階段的可用記憶體小於所需的工作記憶體時，會提前修剪資料列群組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="3fa02-132">下列各節說明如何評估所需記憶體及配置更多記憶體。</span><span class="sxs-lookup"><span data-stu-id="3fa02-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="3fa02-133">DICTIONARY_SIZE：這個修剪原因表示因為至少有一個字串資料行具有寬/或高基數字串而發生資料列群組修剪。</span><span class="sxs-lookup"><span data-stu-id="3fa02-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="3fa02-134">記憶體中的字典大小限制為 16 MB，且一旦達到此限制，便會壓縮資料列群組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="3fa02-135">如果您遇到這種情況，請考慮將問題資料行隔離到單獨的資料表中。</span><span class="sxs-lookup"><span data-stu-id="3fa02-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="3fa02-136">如何估計記憶體需求</span><span class="sxs-lookup"><span data-stu-id="3fa02-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="3fa02-137">要壓縮一個資料列群組所需的最大記憶體大約是</span><span class="sxs-lookup"><span data-stu-id="3fa02-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="3fa02-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="3fa02-138">72 MB +</span></span>
- <span data-ttu-id="3fa02-139">\#資料列 \* \#資料行 \* 8 個位元組 +</span><span class="sxs-lookup"><span data-stu-id="3fa02-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="3fa02-140">\#資料列 \* \#短字串資料行 \* 32 個位元組 +</span><span class="sxs-lookup"><span data-stu-id="3fa02-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="3fa02-141">\#長字串資料行 \* 壓縮字典 16 MB</span><span class="sxs-lookup"><span data-stu-id="3fa02-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="3fa02-142">短字串資料行使用 < = 32 個位元組的字串資料類型和長字串資料行使用 > 32 個位元組的字串資料類型。</span><span class="sxs-lookup"><span data-stu-id="3fa02-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="3fa02-143">會使用專為壓縮文字的壓縮方法來壓縮長字串。</span><span class="sxs-lookup"><span data-stu-id="3fa02-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="3fa02-144">這個壓縮方法會使用字典來儲存文字模式。</span><span class="sxs-lookup"><span data-stu-id="3fa02-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="3fa02-145">字典的大小上限為 16 MB。</span><span class="sxs-lookup"><span data-stu-id="3fa02-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="3fa02-146">資料列群組中的每一個長字串資料行只有一個字典。</span><span class="sxs-lookup"><span data-stu-id="3fa02-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="3fa02-147">如需資料行存放區記憶體需求的深入討論，請參閱影片 [Azure SQL 資料倉儲調整︰組態和指引](https://myignite.microsoft.com/videos/14822)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="3fa02-148">減少記憶體需求的方式</span><span class="sxs-lookup"><span data-stu-id="3fa02-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="3fa02-149">使用下列技巧來減少記憶體需求，以將資料列群組壓縮到資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="3fa02-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="3fa02-150">使用較少的資料行</span><span class="sxs-lookup"><span data-stu-id="3fa02-150">Use fewer columns</span></span>
<span data-ttu-id="3fa02-151">可能的話，設計較少資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="3fa02-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="3fa02-152">當資料列群組壓縮至資料行存放區內時，資料行存放區索引會個別壓縮每個資料行區段。</span><span class="sxs-lookup"><span data-stu-id="3fa02-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="3fa02-153">因此，要壓縮資料列群組的記憶體需求會隨資料行數的增加而增加。</span><span class="sxs-lookup"><span data-stu-id="3fa02-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="3fa02-154">使用較少的字串資料行</span><span class="sxs-lookup"><span data-stu-id="3fa02-154">Use fewer string columns</span></span>
<span data-ttu-id="3fa02-155">字串資料類型的資料行比數字和日期資料類型需要更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="3fa02-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="3fa02-156">若要減少記憶體需求，請考慮從事實資料表中移除字串資料行，並將其放在較小的維度資料表中。</span><span class="sxs-lookup"><span data-stu-id="3fa02-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="3fa02-157">字串壓縮的其他記憶體需求︰</span><span class="sxs-lookup"><span data-stu-id="3fa02-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="3fa02-158">最多 32 個字元的字串資料類型可能每個值需要 32 個額外的位元組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="3fa02-159">使用超過 32 個字元的字串資料類型會使用字典方法進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="3fa02-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="3fa02-160">資料列群組中的每個資料行可能需要建置額外的 16 MB 建置字典。</span><span class="sxs-lookup"><span data-stu-id="3fa02-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="3fa02-161">避免過度分割</span><span class="sxs-lookup"><span data-stu-id="3fa02-161">Avoid over-partitioning</span></span>

<span data-ttu-id="3fa02-162">資料行存放區索引針對每個資料分割會建立一個或多個資料列群組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="3fa02-163">在 SQL 資料倉儲中，資料分割數會快速成長，因為資料散發且會分割每個散發。</span><span class="sxs-lookup"><span data-stu-id="3fa02-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="3fa02-164">如果資料表有太多資料分割，則可能沒有足夠的資料列可填滿資料列群組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="3fa02-165">缺少的資料列在壓縮期間不會建立記憶體不足的壓力，但這會造成無法達到最佳資料行存放區的資料列群組查詢效能。</span><span class="sxs-lookup"><span data-stu-id="3fa02-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="3fa02-166">要避免過度磁碟分割的另一個原因，是有額外負荷的記憶體將資料列載入分割資料表上的資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="3fa02-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="3fa02-167">在載入期間，許多資料分割可能會收到內送資料列並保留在記憶體中，直到每個分割區有足夠的資料列可壓縮為止。</span><span class="sxs-lookup"><span data-stu-id="3fa02-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="3fa02-168">具有太多資料分割會建立額外的記憶體不足壓力。</span><span class="sxs-lookup"><span data-stu-id="3fa02-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="3fa02-169">簡化載入查詢</span><span class="sxs-lookup"><span data-stu-id="3fa02-169">Simplify the load query</span></span>

<span data-ttu-id="3fa02-170">資料庫會共用在查詢中所有運算子之間的查詢記憶體授權。</span><span class="sxs-lookup"><span data-stu-id="3fa02-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="3fa02-171">當載入查詢具有複雜的排序和聯結時，可供壓縮的記憶體便會減少。</span><span class="sxs-lookup"><span data-stu-id="3fa02-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="3fa02-172">設計負載查詢以僅著重於載入查詢。</span><span class="sxs-lookup"><span data-stu-id="3fa02-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="3fa02-173">如果您需要在資料上執行轉換，從載入查詢個別執行它們。</span><span class="sxs-lookup"><span data-stu-id="3fa02-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="3fa02-174">例如，接移堆積資料表中的資料、執行轉換，然後將暫存資料表載入資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="3fa02-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="3fa02-175">您可以也先載入資料，然後使用 MPP 系統來轉換資料。</span><span class="sxs-lookup"><span data-stu-id="3fa02-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="3fa02-176">調整 MAXDOP</span><span class="sxs-lookup"><span data-stu-id="3fa02-176">Adjust MAXDOP</span></span>

<span data-ttu-id="3fa02-177">當有多個 CPU 核心可供每個散發使用時，每個散發會將資料列群組平行壓縮到資料行存放區。</span><span class="sxs-lookup"><span data-stu-id="3fa02-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="3fa02-178">平行處理原則需要額外的記憶體資源，可能會導致記憶體不足的壓力和調整資料列群組。</span><span class="sxs-lookup"><span data-stu-id="3fa02-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="3fa02-179">若要減少記憶體不足的壓力，您可以使用 MAXDOP 查詢提示來強制載入作業，以便在每個散發內的序列模式中執行。</span><span class="sxs-lookup"><span data-stu-id="3fa02-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="3fa02-180">配置更多記憶體的方式</span><span class="sxs-lookup"><span data-stu-id="3fa02-180">Ways to allocate more memory</span></span>

<span data-ttu-id="3fa02-181">DWU 大小和使用者資源類別會共同判斷有多少記憶體可供使用者查詢。</span><span class="sxs-lookup"><span data-stu-id="3fa02-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="3fa02-182">若要增加負載查詢的記憶體授權，您可以增加 DWU 數目或增加資源類別。</span><span class="sxs-lookup"><span data-stu-id="3fa02-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="3fa02-183">若要增加 DWU，請參閱[如何調整效能？](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="3fa02-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="3fa02-184">若要變更查詢的資源類別，請參閱[變更使用者資源類別的範例](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="3fa02-185">例如，在 DWU 100 上，smallrc 資源類別中的使用者每個散發可以使用 100 MB 的記憶體。</span><span class="sxs-lookup"><span data-stu-id="3fa02-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="3fa02-186">如需詳細資訊，請參閱 [SQL 資料倉儲中的並行存取](sql-data-warehouse-develop-concurrency.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="3fa02-187">假設您決定您需要 700 MB 的記憶體，以取得高品質的資料列群組大小。</span><span class="sxs-lookup"><span data-stu-id="3fa02-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="3fa02-188">下列範例會示範如何使用足夠的記憶體執行載入查詢。</span><span class="sxs-lookup"><span data-stu-id="3fa02-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="3fa02-189">使用 DWU 1000 和 mediumrc，記憶體授權為 800 MB</span><span class="sxs-lookup"><span data-stu-id="3fa02-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="3fa02-190">使用 DWU 600 和 largerc，記憶體授權為 800 MB。</span><span class="sxs-lookup"><span data-stu-id="3fa02-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3fa02-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fa02-191">Next steps</span></span>

<span data-ttu-id="3fa02-192">若要尋找更多在 SQL 資料倉儲中改善效能的方法，請參閱[效能概觀](sql-data-warehouse-overview-manage-user-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="3fa02-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
