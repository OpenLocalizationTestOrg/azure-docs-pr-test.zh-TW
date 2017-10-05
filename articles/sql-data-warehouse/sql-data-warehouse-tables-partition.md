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
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="42cf5-103">在 SQL 資料倉儲中分割資料表</span><span class="sxs-lookup"><span data-stu-id="42cf5-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="42cf5-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="42cf5-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="42cf5-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="42cf5-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="42cf5-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="42cf5-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="42cf5-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="42cf5-107">[Index][Index]</span></span>
> * <span data-ttu-id="42cf5-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="42cf5-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="42cf5-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="42cf5-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="42cf5-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="42cf5-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="42cf5-111">所有 SQL 資料倉儲資料表類型都支援資料分割；包括叢集資料行存放區、叢集索引和堆積。</span><span class="sxs-lookup"><span data-stu-id="42cf5-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="42cf5-112">所有散發類型也也支援資料分割，包括散發的雜湊或循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="42cf5-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="42cf5-113">資料分割可讓您將資料分成較小的資料群組，而在大部分情況下，會在日期資料行上進行資料分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-113">Partitioning enables you to divide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="42cf5-114">資料分割的優點</span><span class="sxs-lookup"><span data-stu-id="42cf5-114">Benefits of partitioning</span></span>
<span data-ttu-id="42cf5-115">資料分割可以提升資料維護和查詢效能。</span><span class="sxs-lookup"><span data-stu-id="42cf5-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="42cf5-116">其具備上述兩個優點，還是只有一個優點，取決於資料的載入方式，以及相同的資料行是否可用於這兩個目的，因為資料分割只能在一個資料行上進行。</span><span class="sxs-lookup"><span data-stu-id="42cf5-116">Whether it benefits both or just one is dependent on how data is loaded and whether the same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-to-loads"></a><span data-ttu-id="42cf5-117">載入的優點</span><span class="sxs-lookup"><span data-stu-id="42cf5-117">Benefits to loads</span></span>
<span data-ttu-id="42cf5-118">SQL 資料倉儲中資料分割的主要優點是藉由使用分割區刪除、切換和合併，來改善資料載入的效率與效能。</span><span class="sxs-lookup"><span data-stu-id="42cf5-118">The primary benefit of partitioning in SQL Data Warehouse is improve the efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="42cf5-119">在大部分情況下，會依照與資料載入到資料庫的順序密切相關的日期資料行分割資料。</span><span class="sxs-lookup"><span data-stu-id="42cf5-119">In most cases data is partitioned on a date column that is closely tied to the sequence which the data is loaded to the database.</span></span>  <span data-ttu-id="42cf5-120">使用資料分割來維護資料的最大優點之一是避免記錄交易。</span><span class="sxs-lookup"><span data-stu-id="42cf5-120">One of the greatest benefits of using partitions to maintain data it the avoidance of transaction logging.</span></span>  <span data-ttu-id="42cf5-121">雖然插入、更新或刪除資料可能是最直接的方法，但只要付出一些關心和努力，在載入處理期間使用資料分割可以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="42cf5-121">While simply inserting, updating or deleting data can be the most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="42cf5-122">切換分割區可用於快速移除或取得資料表的某個區段。</span><span class="sxs-lookup"><span data-stu-id="42cf5-122">Partition switching can be used to quickly remove or replace a section of a table.</span></span>  <span data-ttu-id="42cf5-123">例如，銷售事實資料表可能僅包含過去 36 個月的資料。</span><span class="sxs-lookup"><span data-stu-id="42cf5-123">For example, a sales fact table might contain just data for the past 36 months.</span></span>  <span data-ttu-id="42cf5-124">在每個月月底，便會從資料表刪除最舊月份的銷售資料。</span><span class="sxs-lookup"><span data-stu-id="42cf5-124">At the end of every month, the oldest month of sales data is deleted from the table.</span></span>  <span data-ttu-id="42cf5-125">使用 delete 陳述式來刪除最舊月份的資料，即可刪除此資料。</span><span class="sxs-lookup"><span data-stu-id="42cf5-125">This data could be deleted by using a delete statement to delete the data for the oldest month.</span></span>  <span data-ttu-id="42cf5-126">不過，使用 delete 陳述式逐列刪除大量資料可能需要很長的時間，而且會產生大型交易的風險，如果發生錯誤，則可能需要很長的時間來復原。</span><span class="sxs-lookup"><span data-stu-id="42cf5-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create the risk of large transactions which could take a long time to rollback if something goes wrong.</span></span>  <span data-ttu-id="42cf5-127">比較理想的方法是直接卸除最舊的資料磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-127">A more optimal approach is to simply drop the oldest partition of data.</span></span>  <span data-ttu-id="42cf5-128">刪除個別的資料列需要數小時的時間，而刪除整個磁碟分割可能只要數秒。</span><span class="sxs-lookup"><span data-stu-id="42cf5-128">Where deleting the individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-to-queries"></a><span data-ttu-id="42cf5-129">查詢的優點</span><span class="sxs-lookup"><span data-stu-id="42cf5-129">Benefits to queries</span></span>
<span data-ttu-id="42cf5-130">資料分割也可用來改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="42cf5-130">Partitioning can also be used to improve query performance.</span></span>  <span data-ttu-id="42cf5-131">如果查詢在資料分割資料行上套用篩選，這可能會讓掃描僅限於合格的資料分割 (這可能是較小部分的資料)，進而避免掃描整個資料表。</span><span class="sxs-lookup"><span data-stu-id="42cf5-131">If a query applies a filter on a partitioned column, this can limit the scan to only the qualifying partitions which may be a much smaller subset of the data, avoiding a full table scan.</span></span>  <span data-ttu-id="42cf5-132">引進叢集資料行存放區索引後，述詞消除效能優勢比較沒有幫助，但在某些情況下，對查詢有所益處。</span><span class="sxs-lookup"><span data-stu-id="42cf5-132">With the introduction of clustered columnstore indexes, the predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit to queries.</span></span>  <span data-ttu-id="42cf5-133">例如，如果使用銷售日期欄位將銷售事實資料表分割成 36 個月，以銷售日期進行篩選的查詢便可略過不符合篩選條件的分割區。</span><span class="sxs-lookup"><span data-stu-id="42cf5-133">For example, if the sales fact table is partitioned into 36 months using the sales date field, then queries that filter on the sale date can skip searching in partitions that don’t match the filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="42cf5-134">磁碟分割大小調整指引</span><span class="sxs-lookup"><span data-stu-id="42cf5-134">Partition sizing guidance</span></span>
<span data-ttu-id="42cf5-135">雖然資料分割可用來改善某些案例的效能，但是在某些情況下，建立具有 **太多** 資料分割的資料表可能會降低效能。</span><span class="sxs-lookup"><span data-stu-id="42cf5-135">While partitioning can be used to improve performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="42cf5-136">叢集資料行存放區資料表尤其堪慮。</span><span class="sxs-lookup"><span data-stu-id="42cf5-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="42cf5-137">若要讓資料分割有所助益，務必要了解使用資料分割的時機，以及要建立的分割區數目。</span><span class="sxs-lookup"><span data-stu-id="42cf5-137">For partitioning to be helpful, it is important to understand when to use partitioning and the number of partitions to create.</span></span>  <span data-ttu-id="42cf5-138">多少資料分割才算太多並無硬性規定，這取決於您的資料以及您同時載入多少資料分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-138">There is no hard fast rule as to how many partitions are too many, it depends on your data and how many partitions you are loading to simultaneously.</span></span>  <span data-ttu-id="42cf5-139">但依照一般經驗法則，考慮加入 10 到 100 個分割區，而不是 1000 個。</span><span class="sxs-lookup"><span data-stu-id="42cf5-139">But as a general rule of thumb, think of adding 10s to 100s of partitions, not 1000s.</span></span>

<span data-ttu-id="42cf5-140">在 **叢集資料行存放區** 資料表上建立資料分割時，請務必考慮每個資料分割中將放入多少資料列。</span><span class="sxs-lookup"><span data-stu-id="42cf5-140">When creating partitioning on **clustered columnstore** tables, it is important to consider how many rows will land in each partition.</span></span>  <span data-ttu-id="42cf5-141">為了讓叢集資料行存放區資料表達到最佳壓縮和效能，每個散發與分割區都需要至少 100 萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="42cf5-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="42cf5-142">建立分割區之前，SQL 資料倉儲已將每個資料表分割成 60 個分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="42cf5-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="42cf5-143">除了散發以外，任何加入至資料表的資料分割都是在幕後建立。</span><span class="sxs-lookup"><span data-stu-id="42cf5-143">Any partitioning added to a table is in addition to the distributions created behind the scenes.</span></span>  <span data-ttu-id="42cf5-144">依據此範例，如果銷售事實資料表包含 36 個月的分割區，並假設 SQL 資料倉儲有 60 個散發，則銷售事實資料表每個月應包含 6 千萬個資料列，或是在填入所有月份時包含 21 億個資料列。</span><span class="sxs-lookup"><span data-stu-id="42cf5-144">Using this example, if the sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then the sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="42cf5-145">如果資料表包含的資料列遠少於每個分割區建議的最小資料列數，請考慮使用較少的分割區，以增加每個分割區的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="42cf5-145">If a table contains significantly less rows than the recommended minimum number of rows per partition, consider using fewer partitions in order to make increase the number of rows per partition.</span></span>  <span data-ttu-id="42cf5-146">另請參閱[索引][Index]一文，其中包含可在 SQL 資料倉儲執行的查詢，以評估叢集資料行存放區索引的品質。</span><span class="sxs-lookup"><span data-stu-id="42cf5-146">Also see the [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse to assess the quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="42cf5-147">與 SQL Server 的語法差異</span><span class="sxs-lookup"><span data-stu-id="42cf5-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="42cf5-148">SQL 資料倉儲引進與 SQL Server 稍有不同的簡化分割定義。</span><span class="sxs-lookup"><span data-stu-id="42cf5-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="42cf5-149">資料分割函式和配置不會如同在 SQL Server 中一樣，使用於 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="42cf5-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="42cf5-150">相反地，您只需要識別已分割的資料行和邊界點。</span><span class="sxs-lookup"><span data-stu-id="42cf5-150">Instead, all you need to do is identify partitioned column and the boundary points.</span></span>  <span data-ttu-id="42cf5-151">雖然資料分割的語法與 SQL Server 稍有不同，但基本概念是一樣的。</span><span class="sxs-lookup"><span data-stu-id="42cf5-151">While the syntax of partitioning may be slightly different from SQL Server, the basic concepts are the same.</span></span>  <span data-ttu-id="42cf5-152">SQL Server 和 SQL 資料倉儲支援每個資料表一個分割資料行，它可以是遠距資料分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="42cf5-153">若要深入了解資料分割，請參閱[分割資料表和索引][Partitioned Tables and Indexes]。</span><span class="sxs-lookup"><span data-stu-id="42cf5-153">To learn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="42cf5-154">SQL 資料倉儲分割 [CREATE TABLE][CREATE TABLE] 陳述式的以下範例，會依據 OrderDateKey 資料行分割 FactInternetSales 資料表︰</span><span class="sxs-lookup"><span data-stu-id="42cf5-154">The below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions the FactInternetSales table on the OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="42cf5-155">從 SQL Server 移轉資料分割</span><span class="sxs-lookup"><span data-stu-id="42cf5-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="42cf5-156">若要將 SQL Server 分割定義移轉至 SQL 資料倉儲，只需：</span><span class="sxs-lookup"><span data-stu-id="42cf5-156">To migrate SQL Server partition definitions to SQL Data Warehouse simply:</span></span>

* <span data-ttu-id="42cf5-157">刪除 SQL Server [資料分割配置][partition scheme]。</span><span class="sxs-lookup"><span data-stu-id="42cf5-157">Eliminate the SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="42cf5-158">將[資料分割函式][partition function]定義新增至您的 CREATE TABLE。</span><span class="sxs-lookup"><span data-stu-id="42cf5-158">Add the [partition function][partition function] definition to your CREATE TABLE.</span></span>

<span data-ttu-id="42cf5-159">如果您從 SQL Server 執行個體移轉分割資料表，下面的 SQL 可協助您詢問每個分割區中的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="42cf5-159">If you are migrating a partitioned table from a SQL Server instance the below SQL can help you to interrogate the number of rows that are in each partition.</span></span>  <span data-ttu-id="42cf5-160">請記住，如果 SQL 資料倉儲上使用相同的資料分割資料細微性，則每個分割區的資料列數目會依 60 的倍數減少。</span><span class="sxs-lookup"><span data-stu-id="42cf5-160">Keep in mind that if the same partitioning granularity is used on SQL Data Warehouse, the number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="42cf5-161">工作負載管理</span><span class="sxs-lookup"><span data-stu-id="42cf5-161">Workload management</span></span>
<span data-ttu-id="42cf5-162">要納入資料表分割決策的最後一項資訊是[工作負載管理][workload management]。</span><span class="sxs-lookup"><span data-stu-id="42cf5-162">One final piece consideration to factor in to the table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="42cf5-163">SQL 資料倉儲中的工作負載管理主要是記憶體和並行存取管理。</span><span class="sxs-lookup"><span data-stu-id="42cf5-163">Workload management in SQL Data Warehouse is primarily the management of memory and concurrency.</span></span>  <span data-ttu-id="42cf5-164">在 SQL 資料倉儲中，資源類別會控管在查詢執行期間配置給每個散發的最大記憶體。</span><span class="sxs-lookup"><span data-stu-id="42cf5-164">In SQL Data Warehouse the maximum memory allocated to each distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="42cf5-165">在理想的情況下，會考量建置叢集資料行存放區索引的記憶體需求等其他因素，以調整您的分割大小。</span><span class="sxs-lookup"><span data-stu-id="42cf5-165">Ideally your partitions will be sized in consideration of other factors like the memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="42cf5-166">配置更多記憶體給叢集資料行存放區索引時，即可獲得極大的好處。</span><span class="sxs-lookup"><span data-stu-id="42cf5-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="42cf5-167">因此，您會想要確定重建分割索引不會耗盡記憶體。</span><span class="sxs-lookup"><span data-stu-id="42cf5-167">Therefore, you will want to ensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="42cf5-168">從預設角色 smallrc 切換到其他角色 (例如 largerc)，即可增加您的查詢可用的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="42cf5-168">Increasing the amount of memory available to your query can be achieved by switching from the default role, smallrc, to one of the other roles such as largerc.</span></span>

<span data-ttu-id="42cf5-169">查詢資源管理員動態管理檢視，即可取得每個散發的記憶體配置資訊。</span><span class="sxs-lookup"><span data-stu-id="42cf5-169">Information on the allocation of memory per distribution is available by querying the resource governor dynamic management views.</span></span> <span data-ttu-id="42cf5-170">事實上，記憶體授與會小於下列數據。</span><span class="sxs-lookup"><span data-stu-id="42cf5-170">In reality your memory grant will be less than the figures below.</span></span> <span data-ttu-id="42cf5-171">不過，這會提供指導方針，以便在針對資料管理作業調整分割大小時使用。</span><span class="sxs-lookup"><span data-stu-id="42cf5-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="42cf5-172">盡量避免將分割大小調整超過超大型資源類別所提供的記憶體授與。</span><span class="sxs-lookup"><span data-stu-id="42cf5-172">Try to avoid sizing your partitions beyond the memory grant provided by the extra large resource class.</span></span> <span data-ttu-id="42cf5-173">如果分割成長超過此數據，您就會冒著記憶體壓力的風險，進而導致比較不理想的壓縮。</span><span class="sxs-lookup"><span data-stu-id="42cf5-173">If your partitions grow beyond this figure you run the risk of memory pressure which in turn leads to less optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="42cf5-174">分割切換</span><span class="sxs-lookup"><span data-stu-id="42cf5-174">Partition switching</span></span>
<span data-ttu-id="42cf5-175">SQL 資料倉儲支援資料分割、合併和切換。</span><span class="sxs-lookup"><span data-stu-id="42cf5-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="42cf5-176">這些功能是使用 [ALTER TABLE][ALTER TABLE] 陳述式執行。</span><span class="sxs-lookup"><span data-stu-id="42cf5-176">Each of these functions is excuted using the [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="42cf5-177">若要切換兩個資料表間的分割，您必須確定分割對齊其各自的界限，而且資料表定義相符。</span><span class="sxs-lookup"><span data-stu-id="42cf5-177">To switch partitions between two tables you must ensure that the partitions align on their respective boundaries and that the table definitions match.</span></span> <span data-ttu-id="42cf5-178">檢查條件約束不適用於強制資料表中的值範圍，來源資料表必須包含與目標資料表相同的分割界限。</span><span class="sxs-lookup"><span data-stu-id="42cf5-178">As check constraints are not available to enforce the range of values in a table the source table must contain the same partition boundaries as the target table.</span></span> <span data-ttu-id="42cf5-179">如果情況不是如此，則分割切換將會失敗，因為分割中繼資料不會同步處理。</span><span class="sxs-lookup"><span data-stu-id="42cf5-179">If this is not the case, then the partition switch will fail as the partition metadata will not be synchronized.</span></span>

### <a name="how-to-split-a-partition-that-contains-data"></a><span data-ttu-id="42cf5-180">如何分割包含資料的分割</span><span class="sxs-lookup"><span data-stu-id="42cf5-180">How to split a partition that contains data</span></span>
<span data-ttu-id="42cf5-181">使用 `CTAS` 陳述式是分割已含資料之分割的最有效方法。</span><span class="sxs-lookup"><span data-stu-id="42cf5-181">The most efficient method to split a partition that already contains data is to use a `CTAS` statement.</span></span> <span data-ttu-id="42cf5-182">如果分割資料表是叢集式資料行存放區，則資料表分割必須空的，才可加以分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-182">If the partitioned table is a clustered columnstore then the table partition must be empty before it can be split.</span></span>

<span data-ttu-id="42cf5-183">下列範例顯示每個分割包含一個資料列的分割資料行存放區資料表：</span><span class="sxs-lookup"><span data-stu-id="42cf5-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="42cf5-184">藉由建立統計資料物件，我們確定資料表中繼資料更加精確。</span><span class="sxs-lookup"><span data-stu-id="42cf5-184">By Creating the statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="42cf5-185">如果我們省略了建立統計資料，SQL 資料倉儲將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="42cf5-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="42cf5-186">如需統計資料的詳細資訊，請檢閱[統計資料][statistics]。</span><span class="sxs-lookup"><span data-stu-id="42cf5-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="42cf5-187">我們可以接著使用 `sys.partitions` 目錄檢視，查詢資料列計數：</span><span class="sxs-lookup"><span data-stu-id="42cf5-187">We can then query for the row count using the `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="42cf5-188">如果我們嘗試分割此資料表，我們會收到錯誤：</span><span class="sxs-lookup"><span data-stu-id="42cf5-188">If we try to split this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="42cf5-189">訊息 35346、層級 15、狀態 1、行 44：ALTER PARTITION 陳述式的 SPLIT 子句失敗，因為分割不是空的。</span><span class="sxs-lookup"><span data-stu-id="42cf5-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because the partition is not empty.</span></span>  <span data-ttu-id="42cf5-190">只有在資料表上存在資料行存放區索引時，才可以分割空的分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-190">Only empty partitions can be split in when a columnstore index exists on the table.</span></span> <span data-ttu-id="42cf5-191">請考慮在發出 ALTER PARTITION 陳述式前停用資料行存放區索引，然後在 ALTER PARTITION 完成後重建資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="42cf5-191">Consider disabling the columnstore index before issuing the ALTER PARTITION statement, then rebuilding the columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="42cf5-192">不過，我們可以使用 `CTAS` 建立新資料表以保存資料。</span><span class="sxs-lookup"><span data-stu-id="42cf5-192">However, we can use `CTAS` to create a new table to hold our data.</span></span>

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

<span data-ttu-id="42cf5-193">分割界限已對齊，所以允許切換。</span><span class="sxs-lookup"><span data-stu-id="42cf5-193">As the partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="42cf5-194">這會讓來源資料表有空白分割可供我們接著分割。</span><span class="sxs-lookup"><span data-stu-id="42cf5-194">This will leave the source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="42cf5-195">接下來只需使用 `CTAS` 將我們的資料對齊新的分割界限，並將我們的資料切換回到主資料表</span><span class="sxs-lookup"><span data-stu-id="42cf5-195">All that is left to do is to align our data to the new partition boundaries using `CTAS` and switch our data back in to the main table</span></span>

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

<span data-ttu-id="42cf5-196">完成資料移動後，最好能重新整理目標資料表上的統計資料，確保統計資料可在其各自的分割中精確地反映出資料的新散發：</span><span class="sxs-lookup"><span data-stu-id="42cf5-196">Once you have completed the movement of the data it is a good idea to refresh the statistics on the target table to ensure they accurately reflect the new distribution of the data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="42cf5-197">資料表分割原始檔控制</span><span class="sxs-lookup"><span data-stu-id="42cf5-197">Table partitioning source control</span></span>
<span data-ttu-id="42cf5-198">若要避免您的資料表定義在您的原始檔控制系統中 **失效** ，您可以考慮下列方法：</span><span class="sxs-lookup"><span data-stu-id="42cf5-198">To avoid your table definition from **rusting** in your source control system you may want to consider the following approach:</span></span>

1. <span data-ttu-id="42cf5-199">將資料表建立為分割資料表，但沒有分割值</span><span class="sxs-lookup"><span data-stu-id="42cf5-199">Create the table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="42cf5-200">`SPLIT` 資料表：</span><span class="sxs-lookup"><span data-stu-id="42cf5-200">`SPLIT` the table as part of the deployment process:</span></span>

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

<span data-ttu-id="42cf5-201">利用這種方法，原始檔控制中的程式碼會保持靜態，並允許動態的分割界限值；隨著時間與倉儲一起發展。</span><span class="sxs-lookup"><span data-stu-id="42cf5-201">With this approach the code in source control remains static and the partitioning boundary values are allowed to be dynamic; evolving with the warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42cf5-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42cf5-202">Next steps</span></span>
<span data-ttu-id="42cf5-203">若要深入了解，請參閱[資料表概觀][Overview]、[資料表資料類型][Data Types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[維護資料表統計資料][Statistics]和[暫存資料表][Temporary]等文章。</span><span class="sxs-lookup"><span data-stu-id="42cf5-203">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="42cf5-204">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="42cf5-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
