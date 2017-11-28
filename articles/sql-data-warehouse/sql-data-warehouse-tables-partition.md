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
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="8c647-103">在 SQL 資料倉儲中分割資料表</span><span class="sxs-lookup"><span data-stu-id="8c647-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8c647-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="8c647-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="8c647-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="8c647-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="8c647-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8c647-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="8c647-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="8c647-107">[Index][Index]</span></span>
> * <span data-ttu-id="8c647-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="8c647-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="8c647-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8c647-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="8c647-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8c647-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="8c647-111">所有 SQL 資料倉儲資料表類型都支援資料分割；包括叢集資料行存放區、叢集索引和堆積。</span><span class="sxs-lookup"><span data-stu-id="8c647-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="8c647-112">所有散發類型也也支援資料分割，包括散發的雜湊或循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="8c647-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="8c647-113">資料分割可讓您 toodivide 您較小的群組的資料，以及在大部分情況下，資料分割的資料便已完成的日期資料行。</span><span class="sxs-lookup"><span data-stu-id="8c647-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="8c647-114">資料分割的優點</span><span class="sxs-lookup"><span data-stu-id="8c647-114">Benefits of partitioning</span></span>
<span data-ttu-id="8c647-115">資料分割可以提升資料維護和查詢效能。</span><span class="sxs-lookup"><span data-stu-id="8c647-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="8c647-116">其優點兩個或其中一個是取決於如何載入資料，以及是否 hello 相同的資料行可以使用這兩種用途，因為資料分割只能在一個資料行上。</span><span class="sxs-lookup"><span data-stu-id="8c647-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="8c647-117">優點 tooloads</span><span class="sxs-lookup"><span data-stu-id="8c647-117">Benefits tooloads</span></span>
<span data-ttu-id="8c647-118">hello SQL 資料倉儲中資料分割的主要優點是改善 hello 效率與效能載入使用的分割區刪除的資料、 切換和合併。</span><span class="sxs-lookup"><span data-stu-id="8c647-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="8c647-119">在大部分情況下，資料分割的日期資料行緊密繫結 toohello 順序 hello 資料是載入的 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c647-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="8c647-120">其中一個 hello 使用它 hello 避免交易記錄的資料分割 toomaintain 資料的最大的優勢。</span><span class="sxs-lookup"><span data-stu-id="8c647-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="8c647-121">雖然只要插入、 更新或刪除資料可以 hello 最直接的方法，以極小的思考和投入時間，而使用您在載入程序分割可以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="8c647-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="8c647-122">切換資料分割可以使用的 tooquickly 移除或取代資料表區段。</span><span class="sxs-lookup"><span data-stu-id="8c647-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="8c647-123">例如，銷售事實資料表可能過去 36 個月包含 hello 是只有資料。</span><span class="sxs-lookup"><span data-stu-id="8c647-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="8c647-124">在每個月的 hello 結尾，hello 早月份的銷售資料的資料表中刪除了 hello。</span><span class="sxs-lookup"><span data-stu-id="8c647-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="8c647-125">無法刪除此資料，會使用 delete 陳述式 toodelete hello 資料 hello 最舊的月份。</span><span class="sxs-lookup"><span data-stu-id="8c647-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="8c647-126">不過，刪除大量的資料列逐列與 delete 陳述式可以花很長的時間，以及建立大型交易發生錯誤時，可能需要很長的時間 toorollback hello 風險。</span><span class="sxs-lookup"><span data-stu-id="8c647-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="8c647-127">更接近最佳的方法是 toosimply 卸除 hello 最舊的磁碟分割的資料。</span><span class="sxs-lookup"><span data-stu-id="8c647-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="8c647-128">刪除 hello 個別資料列，需要數小時，刪除整個磁碟分割可能需要為秒鐘。</span><span class="sxs-lookup"><span data-stu-id="8c647-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="8c647-129">優點 tooqueries</span><span class="sxs-lookup"><span data-stu-id="8c647-129">Benefits tooqueries</span></span>
<span data-ttu-id="8c647-130">資料分割也可以使用的 tooimprove 查詢效能。</span><span class="sxs-lookup"><span data-stu-id="8c647-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="8c647-131">如果查詢的資料分割的資料行上套用篩選器，這可能會限制 hello 掃描 tooonly hello 限定可能遠 hello 資料子集，避免完整資料表掃描的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="8c647-132">與 hello 的叢集資料行存放區索引的簡介，hello 述詞刪除效能優勢會較不會很有用，但在某些情況下可能會有好處 tooqueries。</span><span class="sxs-lookup"><span data-stu-id="8c647-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="8c647-133">比方說，hello 銷售事實資料表為資料分割到 36 個月使用 hello 銷售日期欄位，然後在 hello 銷售日期篩選的查詢可以略過不符合 hello 篩選條件的資料分割中的搜尋。</span><span class="sxs-lookup"><span data-stu-id="8c647-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="8c647-134">磁碟分割大小調整指引</span><span class="sxs-lookup"><span data-stu-id="8c647-134">Partition sizing guidance</span></span>
<span data-ttu-id="8c647-135">資料分割時可以使用的 tooimprove 效能某些案例中，建立具有資料表**太多**資料分割會降低效能，在某些情況下。</span><span class="sxs-lookup"><span data-stu-id="8c647-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="8c647-136">叢集資料行存放區資料表尤其堪慮。</span><span class="sxs-lookup"><span data-stu-id="8c647-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="8c647-137">針對資料分割 toobe 很有幫助，很重要的 toounderstand 時的資料分割 toocreate toouse 分割與 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8c647-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="8c647-138">那里已為 toohow 沒有硬式快速規則多個資料分割太多，這取決於您的資料而多少資料分割會載入 toosimultaneously。</span><span class="sxs-lookup"><span data-stu-id="8c647-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="8c647-139">但是為一般的經驗法則，將加入 10s too100s 的資料分割，而不是 1000年。</span><span class="sxs-lookup"><span data-stu-id="8c647-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="8c647-140">建立資料分割上時**叢集資料行存放區**很重要 tooconsider 多少資料列會讓每個分割區資料表。</span><span class="sxs-lookup"><span data-stu-id="8c647-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="8c647-141">為了讓叢集資料行存放區資料表達到最佳壓縮和效能，每個散發與分割區都需要至少 100 萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="8c647-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="8c647-142">建立分割區之前，SQL 資料倉儲已將每個資料表分割成 60 個分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c647-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="8c647-143">任何資料分割加入的 tooa 資料表是另外建立 hello 幕後 toohello 分佈。</span><span class="sxs-lookup"><span data-stu-id="8c647-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="8c647-144">如果 hello 銷售事實資料表包含 36 的每月資料分割，而且假設 SQL 資料倉儲具有 60 分佈，然後 hello 銷售事實資料表應該包含每個月，60 萬個資料列或 2.1 10 億個資料列，當所有月份已都擴展時，請使用此範例中。</span><span class="sxs-lookup"><span data-stu-id="8c647-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="8c647-145">如果資料表包含比 hello 建議的每個資料分割的資料列的最小數目，大幅減少資料列時，請考慮使用較少的資料分割中的每個資料分割的資料列順序 toomake 增加 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8c647-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="8c647-146">另請參閱 hello[索引][ Index]發行項，其中包含您可以執行的叢集資料行存放區索引的 SQL 資料倉儲 tooassess hello 品質的查詢。</span><span class="sxs-lookup"><span data-stu-id="8c647-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="8c647-147">與 SQL Server 的語法差異</span><span class="sxs-lookup"><span data-stu-id="8c647-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="8c647-148">SQL 資料倉儲引進與 SQL Server 稍有不同的簡化分割定義。</span><span class="sxs-lookup"><span data-stu-id="8c647-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="8c647-149">資料分割函式和配置不會如同在 SQL Server 中一樣，使用於 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="8c647-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="8c647-150">相反地，您只需要 toodo 是識別資料分割的資料行和 hello 邊界點。</span><span class="sxs-lookup"><span data-stu-id="8c647-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="8c647-151">雖然資料分割的 hello 語法稍有不同 SQL Server，hello 基本概念是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="8c647-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="8c647-152">SQL Server 和 SQL 資料倉儲支援每個資料表一個分割資料行，它可以是遠距資料分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="8c647-153">toolearn 進一步了解資料分割，請參閱[Partitioned Tables and Indexes][Partitioned Tables and Indexes]。</span><span class="sxs-lookup"><span data-stu-id="8c647-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="8c647-154">下列範例中的資料分割的 SQL 資料倉儲的 hello [CREATE TABLE] [ CREATE TABLE]陳述式中，資料分割 hello OrderDateKey 資料行上的 hello FactInternetSales 資料表：</span><span class="sxs-lookup"><span data-stu-id="8c647-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="8c647-155">從 SQL Server 移轉資料分割</span><span class="sxs-lookup"><span data-stu-id="8c647-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="8c647-156">SQL Server toomigrate 只分割定義 tooSQL 資料倉儲：</span><span class="sxs-lookup"><span data-stu-id="8c647-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="8c647-157">消除 hello SQL Server[分割區配置][partition scheme]。</span><span class="sxs-lookup"><span data-stu-id="8c647-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="8c647-158">新增 hello[資料分割函數][ partition function]定義 tooyour 建立資料表。</span><span class="sxs-lookup"><span data-stu-id="8c647-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="8c647-159">如果您從 SQL Server 執行個體 hello 以下 SQL 移轉資料分割的資料表可協助您在每個資料分割中的資料列的 toointerrogate hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8c647-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="8c647-160">請注意，如果 hello 相同資料分割的資料粒度上使用 SQL 資料倉儲，每個資料分割的資料列的 hello 數目將會降低，因數為 60。</span><span class="sxs-lookup"><span data-stu-id="8c647-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="8c647-161">工作負載管理</span><span class="sxs-lookup"><span data-stu-id="8c647-161">Workload management</span></span>
<span data-ttu-id="8c647-162">是一個 toohello 資料表資料分割決策的最後一段考量 toofactor[工作負載管理][workload management]。</span><span class="sxs-lookup"><span data-stu-id="8c647-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="8c647-163">主要 hello 管理的記憶體和並行存取 SQL 資料倉儲中的工作負載管理。</span><span class="sxs-lookup"><span data-stu-id="8c647-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="8c647-164">在 SQL 資料倉儲 hello 配置 tooeach 發佈在查詢執行期間的最大記憶體是管的資源類別。</span><span class="sxs-lookup"><span data-stu-id="8c647-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="8c647-165">在理想情況下您的資料分割將調整大小 in consideration of hello 記憶體需求，建立叢集資料行存放區索引的其他因素。</span><span class="sxs-lookup"><span data-stu-id="8c647-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="8c647-166">配置更多記憶體給叢集資料行存放區索引時，即可獲得極大的好處。</span><span class="sxs-lookup"><span data-stu-id="8c647-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="8c647-167">因此，您將會重建分割區索引的 tooensure 尚未用完的記憶體。</span><span class="sxs-lookup"><span data-stu-id="8c647-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="8c647-168">增加 hello 數量記憶體可用 tooyour 查詢可藉由切換從 hello 預設角色、 smallrc、 tooone 的 hello 其他角色，例如 largerc。</span><span class="sxs-lookup"><span data-stu-id="8c647-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="8c647-169">Hello 配置的記憶體，每個發佈的詳細資訊，請查詢 hello 資源管理員動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="8c647-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="8c647-170">事實上，記憶體授權會早於下列 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="8c647-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="8c647-171">不過，這會提供指導方針，以便在針對資料管理作業調整分割大小時使用。</span><span class="sxs-lookup"><span data-stu-id="8c647-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="8c647-172">請嘗試 tooavoid 調整大小超出 hello hello 超大型資源類別所提供的記憶體授與資料分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="8c647-173">如果分割區超出本圖風險 hello 反過來 tooless 最佳壓縮的記憶體不足壓力。</span><span class="sxs-lookup"><span data-stu-id="8c647-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="8c647-174">分割切換</span><span class="sxs-lookup"><span data-stu-id="8c647-174">Partition switching</span></span>
<span data-ttu-id="8c647-175">SQL 資料倉儲支援資料分割、合併和切換。</span><span class="sxs-lookup"><span data-stu-id="8c647-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="8c647-176">這些函式的每一個都是使用 hello excuted [ALTER TABLE] [ ALTER TABLE]陳述式。</span><span class="sxs-lookup"><span data-stu-id="8c647-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="8c647-177">您必須確定 hello 資料分割將對齊其各自的界限上，且符合 hello 資料表定義的兩個資料表之間的 tooswitch 分割區。</span><span class="sxs-lookup"><span data-stu-id="8c647-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="8c647-178">Check 條件約束沒有 tooenforce hello 資料表 hello 來源資料表中的值範圍必須包含 hello 相同為 hello 目標資料表資料分割界限。</span><span class="sxs-lookup"><span data-stu-id="8c647-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="8c647-179">如果這不是 hello 案例，則會失敗 hello 資料分割切換，將不會同步 hello 分割區中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8c647-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="8c647-180">如何 toosplit 包含資料的磁碟分割</span><span class="sxs-lookup"><span data-stu-id="8c647-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="8c647-181">hello 最有效率的方法 toosplit 已經包含資料的資料分割是 toouse`CTAS`陳述式。</span><span class="sxs-lookup"><span data-stu-id="8c647-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="8c647-182">如果 hello 資料分割的資料表的叢集資料行存放區則 hello 資料表資料分割必須是空白之前可以分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="8c647-183">下列範例顯示每個分割包含一個資料列的分割資料行存放區資料表：</span><span class="sxs-lookup"><span data-stu-id="8c647-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="8c647-184">建立 hello 統計資料物件，我們確定該資料表的中繼資料更精確。</span><span class="sxs-lookup"><span data-stu-id="8c647-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="8c647-185">如果我們省略了建立統計資料，SQL 資料倉儲將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="8c647-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="8c647-186">如需統計資料的詳細資訊，請檢閱[統計資料][statistics]。</span><span class="sxs-lookup"><span data-stu-id="8c647-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="8c647-187">我們可以在使用 hello hello 資料列計數查詢`sys.partitions`目錄檢視：</span><span class="sxs-lookup"><span data-stu-id="8c647-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="8c647-188">如果我們嘗試 toosplit 此資料表，我們會收到錯誤：</span><span class="sxs-lookup"><span data-stu-id="8c647-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8c647-189">Msg 35346，層級 15，狀態 1，行 44 分割子句的 ALTER PARTITION 陳述式失敗，因為不是空的 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="8c647-190">Hello 資料表上存在的資料行存放區索引時，可以在分割只有空的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="8c647-191">請考慮停用後再發出 hello ALTER PARTITION 陳述式，再重建 hello 資料行存放區索引，ALTER PARTITION 完成後的 hello 資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="8c647-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="8c647-192">不過，我們可以使用`CTAS`toocreate 新的資料表 toohold 我們的資料。</span><span class="sxs-lookup"><span data-stu-id="8c647-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="8c647-193">允許參數為 hello 資料分割界限對齊。</span><span class="sxs-lookup"><span data-stu-id="8c647-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="8c647-194">這會導致 hello 來源資料表具有空的分割區，我們接下來可以分割。</span><span class="sxs-lookup"><span data-stu-id="8c647-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8c647-195">剩下 toodo 是我們資料 toohello 新資料分割界限使用的 tooalign `CTAS` toohello 主資料表中切換資料</span><span class="sxs-lookup"><span data-stu-id="8c647-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

<span data-ttu-id="8c647-196">當您完成 hello hello 資料移動是個不錯的主意 toorefresh hello 統計資料在 hello 目標資料表 tooensure 它們正確地反映 hello hello 中的資料及其個別資料分割的新發佈：</span><span class="sxs-lookup"><span data-stu-id="8c647-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="8c647-197">資料表分割原始檔控制</span><span class="sxs-lookup"><span data-stu-id="8c647-197">Table partitioning source control</span></span>
<span data-ttu-id="8c647-198">tooavoid 從您的資料表定義**rusting**在您的原始檔控制系統中，您可能想 tooconsider hello 遵循方法：</span><span class="sxs-lookup"><span data-stu-id="8c647-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="8c647-199">建立 hello 資料表為資料分割資料表，但不會有資料分割值</span><span class="sxs-lookup"><span data-stu-id="8c647-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="8c647-200">`SPLIT`hello 資料表 hello 部署程序的一部分：</span><span class="sxs-lookup"><span data-stu-id="8c647-200">`SPLIT` hello table as part of hello deployment process:</span></span>

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

<span data-ttu-id="8c647-201">這個方法 hello 與原始檔控制中的程式碼保持不變，而 hello 資料分割的界限值允許 toobe 動態;經過一段時間發展與 hello 倉儲。</span><span class="sxs-lookup"><span data-stu-id="8c647-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c647-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c647-202">Next steps</span></span>
<span data-ttu-id="8c647-203">toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[維護資料表統計資料][ Statistics]和[暫存資料表][Temporary]。</span><span class="sxs-lookup"><span data-stu-id="8c647-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="8c647-204">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="8c647-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
