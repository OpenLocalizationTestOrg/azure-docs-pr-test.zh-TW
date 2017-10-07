---
title: "aaaDesign 指導複寫的資料表-Azure SQL 資料倉儲 |Microsoft 文件"
description: "針對在「Azure SQL 資料倉儲」結構描述中設計複寫資料表提供建議。"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="47a08-103">在 Azure SQL 資料倉儲中使用複寫資料表的設計指引</span><span class="sxs-lookup"><span data-stu-id="47a08-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="47a08-104">本文針對在「SQL 資料倉儲」結構描述中設計複寫資料表提供建議。</span><span class="sxs-lookup"><span data-stu-id="47a08-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="47a08-105">使用這些建議 tooimprove 查詢效能降低資料移動和查詢的複雜性。</span><span class="sxs-lookup"><span data-stu-id="47a08-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="47a08-106">hello 複寫的資料表功能目前處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="47a08-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="47a08-107">某些行為是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="47a08-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="47a08-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="47a08-108">Prerequisites</span></span>
<span data-ttu-id="47a08-109">本文假設您已熟悉「SQL 資料倉儲」中的資料散發和資料移動概念。</span><span class="sxs-lookup"><span data-stu-id="47a08-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="47a08-110">如需詳細資訊，請參閱[分散式資料](sql-data-warehouse-distributed-data.md)。</span><span class="sxs-lookup"><span data-stu-id="47a08-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="47a08-111">資料表設計的一部分，了解最大的資料，及其如何 hello 查詢資料。</span><span class="sxs-lookup"><span data-stu-id="47a08-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="47a08-112">例如，請思考一下下列問題：</span><span class="sxs-lookup"><span data-stu-id="47a08-112">For example, consider these questions:</span></span>

- <span data-ttu-id="47a08-113">大小是 hello 資料表？</span><span class="sxs-lookup"><span data-stu-id="47a08-113">How large is hello table?</span></span>   
- <span data-ttu-id="47a08-114">Hello 資料表重新整理的頻率？</span><span class="sxs-lookup"><span data-stu-id="47a08-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="47a08-115">我是否在資料倉儲中有事實資料表和維度資料表？</span><span class="sxs-lookup"><span data-stu-id="47a08-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="47a08-116">什麼是複寫資料表？</span><span class="sxs-lookup"><span data-stu-id="47a08-116">What is a replicated table?</span></span>
<span data-ttu-id="47a08-117">複寫的資料表有 hello 資料表可存取的完整複本，每個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="47a08-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="47a08-118">複寫資料表中移除計算節點，然後再聯結或彙總之間的 hello 需要 tootransfer 資料。</span><span class="sxs-lookup"><span data-stu-id="47a08-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="47a08-119">Hello 資料表有多個複本，因為複寫的資料表時效果最佳 hello 資料表大小會小於 2 GB 壓縮。</span><span class="sxs-lookup"><span data-stu-id="47a08-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="47a08-120">hello 圖顯示可供存取每個計算節點上的複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="47a08-121">在 SQL 資料倉儲、 hello 複寫的資料表會是每個計算節點上的完整複製的 tooa 散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="47a08-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="47a08-122">![複寫的資料表](media/guidance-for-using-replicated-tables/replicated-table.png "複寫的資料表")</span><span class="sxs-lookup"><span data-stu-id="47a08-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="47a08-123">複寫資料表適用於星型結構描述中的小型維度資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="47a08-124">維度資料表通常都使得 toostore 可行的大小，並維護多個複本。</span><span class="sxs-lookup"><span data-stu-id="47a08-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="47a08-125">維度會儲存變更緩慢的描述性資料，例如客戶名稱和地址，以及產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47a08-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="47a08-126">hello 緩時變 hello 資料的本質會導致 toofewer 重建的 hello 複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="47a08-127">在下列情況下，請考慮使用複寫資料表：</span><span class="sxs-lookup"><span data-stu-id="47a08-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="47a08-128">在磁碟上的 hello 資料表大小為小於 2 GB，不論 hello 的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="47a08-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="47a08-129">toofind hello 的資料表大小，您可以使用 hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql)命令： `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`。</span><span class="sxs-lookup"><span data-stu-id="47a08-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="47a08-130">hello 資料表用於聯結需要移動資料。</span><span class="sxs-lookup"><span data-stu-id="47a08-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="47a08-131">例如上分散雜湊資料表, 的聯結時 hello 聯結的資料行不是 hello 相同的散發資料行需要資料移動。</span><span class="sxs-lookup"><span data-stu-id="47a08-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="47a08-132">如果其中一個 hello 雜湊散發資料表很小，請考慮複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="47a08-133">循環配置資源資料表上的聯結需要進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="47a08-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="47a08-134">建議您在大多數情況下都使用複寫資料表，而不要使用循環配置資源資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="47a08-135">請考慮將轉換的現有分散式資料表 tooa 複寫的資料表：</span><span class="sxs-lookup"><span data-stu-id="47a08-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="47a08-136">查詢計劃使用廣播 hello 資料 tooall hello 計算節點的資料移動作業。</span><span class="sxs-lookup"><span data-stu-id="47a08-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="47a08-137">hello BroadcastMoveOperation 昂貴，而且會降低查詢效能。</span><span class="sxs-lookup"><span data-stu-id="47a08-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="47a08-138">tooview 資料移動作業，在查詢計畫中，使用[sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="47a08-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="47a08-139">複寫的資料表可能不會產生最佳查詢效能 hello 時：</span><span class="sxs-lookup"><span data-stu-id="47a08-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="47a08-140">hello 資料表有頻繁的插入、 更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="47a08-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="47a08-141">這些資料操作語言 (DML) 作業需要重建 hello 複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="47a08-142">經常重建會導致效能變差。</span><span class="sxs-lookup"><span data-stu-id="47a08-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="47a08-143">hello 資料倉儲會經常調整。</span><span class="sxs-lookup"><span data-stu-id="47a08-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="47a08-144">調整資料倉儲變更 hello 運算節點數目，而造成重建。</span><span class="sxs-lookup"><span data-stu-id="47a08-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="47a08-145">hello 資料表有大量的資料行，但資料作業通常存取只有少數資料行。</span><span class="sxs-lookup"><span data-stu-id="47a08-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="47a08-146">在此案例中，而不是複寫 hello 整份資料表，它可能會更有效率的 toohash 散發 hello 資料表，然後 hello 經常存取的資料行上建立索引。</span><span class="sxs-lookup"><span data-stu-id="47a08-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="47a08-147">當查詢需要的資料移動，SQL 資料倉儲，只在 hello 移動資料要求資料行。</span><span class="sxs-lookup"><span data-stu-id="47a08-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="47a08-148">使用複寫資料表搭配簡單查詢述詞</span><span class="sxs-lookup"><span data-stu-id="47a08-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="47a08-149">您選擇 toodistribute 或複寫資料表之前，請考慮 hello 您計劃 toorun hello 資料表的查詢類型。</span><span class="sxs-lookup"><span data-stu-id="47a08-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="47a08-150">請儘可能</span><span class="sxs-lookup"><span data-stu-id="47a08-150">Whenever possible,</span></span>

- <span data-ttu-id="47a08-151">針對含有簡單查詢述詞 (例如相等比較或不等比較) 的查詢使用複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="47a08-152">針對含有複雜查詢述詞 (例如相似或不相似) 的查詢使用分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="47a08-153">Hello 工作會分散到所有的 hello 運算節點時，則需要大量 CPU 的查詢會具有最佳。</span><span class="sxs-lookup"><span data-stu-id="47a08-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="47a08-154">例如，以在資料表的每個資料列上執行計算的查詢來說，在複寫資料表上執行會比在分散式資料表上執行效能更佳。</span><span class="sxs-lookup"><span data-stu-id="47a08-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="47a08-155">儲存複寫的資料表中每個計算節點上的完整，因此需要大量 CPU 的查詢，針對複寫的資料表會針對 hello 整份資料表上執行的每個計算節點。</span><span class="sxs-lookup"><span data-stu-id="47a08-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="47a08-156">hello 額外的計算會降低查詢效能。</span><span class="sxs-lookup"><span data-stu-id="47a08-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="47a08-157">例如，此查詢含有複雜的述詞。</span><span class="sxs-lookup"><span data-stu-id="47a08-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="47a08-158">當供應者是分散式資料表而不是複寫資料表時，它的執行速度較快。</span><span class="sxs-lookup"><span data-stu-id="47a08-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="47a08-159">在此範例中，供應者可以是雜湊分散式或循環配置資源分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="47a08-160">轉換現有的循環配置資源資料表 tooreplicated 資料表</span><span class="sxs-lookup"><span data-stu-id="47a08-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="47a08-161">如果您已經有循環配置資源的資料表，我們建議將它們轉換 tooreplicated 資料表符合本文所述的準則。</span><span class="sxs-lookup"><span data-stu-id="47a08-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="47a08-162">複寫的資料表循環配置資源資料表改善效能，因為它們不需要進行資料移動的 hello 需要。</span><span class="sxs-lookup"><span data-stu-id="47a08-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="47a08-163">循環配置資源資料表針對聯結一律需要進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="47a08-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="47a08-164">這個範例會使用[CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory 資料表 tooa 複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="47a08-165">不論 DimSalesTerritory 是雜湊分散式還是循環配置資源資料表，此範例都有效。</span><span class="sxs-lookup"><span data-stu-id="47a08-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="47a08-166">循環配置資源與複寫之查詢效能比較範例</span><span class="sxs-lookup"><span data-stu-id="47a08-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="47a08-167">複寫的資料表不為聯結需要移動任何資料，因為 hello 整份資料表已經存在每個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="47a08-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="47a08-168">如果 hello 維度資料表是分散式循環配置資源，聯結會在完整 tooeach 計算節點複製 hello 維度資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="47a08-169">toomove hello 資料，hello 查詢計劃包含呼叫 BroadcastMoveOperation 作業。</span><span class="sxs-lookup"><span data-stu-id="47a08-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="47a08-170">這類資料移動作業會降低查詢效能，而使用複寫資料表則可免除這類作業。</span><span class="sxs-lookup"><span data-stu-id="47a08-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="47a08-171">tooview 查詢計畫的步驟，使用 hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)系統目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="47a08-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="47a08-172">例如，下列查詢針對 hello AdventureWorks 結構描述中，在 hello` FactInternetSales`資料表是雜湊散發。</span><span class="sxs-lookup"><span data-stu-id="47a08-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="47a08-173">hello`DimDate`和`DimSalesTerritory`資料表為較小的維度資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="47a08-174">此查詢會傳回 2004年會計年度北美地區的 hello 總銷售額：</span><span class="sxs-lookup"><span data-stu-id="47a08-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="47a08-175">我們已將 `DimDate` 和 `DimSalesTerritory` 重新建立成循環配置資源資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="47a08-176">如此一來，hello 查詢示範了下列查詢計劃，具有多個廣播移動作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="47a08-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![循環配置資源的查詢計劃](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="47a08-178">重新建立`DimDate`和`DimSalesTerritory`做為複寫資料表，並再次執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="47a08-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="47a08-179">hello 產生查詢計劃是較短，而且未有任何廣播移動。</span><span class="sxs-lookup"><span data-stu-id="47a08-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![複寫的查詢計劃](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="47a08-181">修改複寫資料表時的效能考量</span><span class="sxs-lookup"><span data-stu-id="47a08-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="47a08-182">SQL 資料倉儲實作複寫的資料表，藉由維護 hello 資料表的主要版本。</span><span class="sxs-lookup"><span data-stu-id="47a08-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="47a08-183">它會複製 hello 主要版本 tooone 每個計算節點上的散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="47a08-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="47a08-184">變更時，SQL 資料倉儲會先更新 hello 主要資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="47a08-185">然後，它會需要重建 hello 資料表每個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="47a08-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="47a08-186">複寫資料表的重建包含複製 hello 資料表 tooeach 計算節點，然後再重建 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="47a08-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="47a08-187">在執行下列動作之後，必須進行重建：</span><span class="sxs-lookup"><span data-stu-id="47a08-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="47a08-188">載入或修改資料</span><span class="sxs-lookup"><span data-stu-id="47a08-188">Data is loaded or modified</span></span>
- <span data-ttu-id="47a08-189">hello 資料倉儲是縮放的 tooa 不同的 DWU 設定</span><span class="sxs-lookup"><span data-stu-id="47a08-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="47a08-190">更新資料表定義</span><span class="sxs-lookup"><span data-stu-id="47a08-190">Table definition is updated</span></span>

<span data-ttu-id="47a08-191">在執行下列動作之後，不須進行重建：</span><span class="sxs-lookup"><span data-stu-id="47a08-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="47a08-192">暫停作業</span><span class="sxs-lookup"><span data-stu-id="47a08-192">Pause operation</span></span>
- <span data-ttu-id="47a08-193">繼續作業</span><span class="sxs-lookup"><span data-stu-id="47a08-193">Resume operation</span></span>

<span data-ttu-id="47a08-194">在修改資料之後，立即 hello 重建不會發生。</span><span class="sxs-lookup"><span data-stu-id="47a08-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="47a08-195">相反地，就會觸發 hello 重建 hello 從 hello 資料表選取查詢的第一次。</span><span class="sxs-lookup"><span data-stu-id="47a08-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="47a08-196">Hello 初始 select 陳述式中從 hello 資料表是步驟 toorebuild hello 複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="47a08-197">Hello 重建 hello 查詢中進行設定，因為 hello 影響 toohello 初始 select 陳述式可能是重大 hello hello 資料表大小而定。</span><span class="sxs-lookup"><span data-stu-id="47a08-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="47a08-198">如果需要重建涉及多個複寫的資料表時，每個複本就會以序列方式重建 hello 陳述式中的步驟。</span><span class="sxs-lookup"><span data-stu-id="47a08-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="47a08-199">toomaintain 資料一致性的 hello hello 重建時複寫的資料表的獨佔鎖定在 hello 資料表取得。</span><span class="sxs-lookup"><span data-stu-id="47a08-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="47a08-200">hello 鎖定會防止所有存取 toohello 表 hello 重建 hello 持續期間。</span><span class="sxs-lookup"><span data-stu-id="47a08-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="47a08-201">謹慎地使用索引</span><span class="sxs-lookup"><span data-stu-id="47a08-201">Use indexes conservatively</span></span>
<span data-ttu-id="47a08-202">標準索引作法適用於 tooreplicated 資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="47a08-203">SQL 資料倉儲重建 hello 重建一部分的每個複寫的資料表索引。</span><span class="sxs-lookup"><span data-stu-id="47a08-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="47a08-204">Hello 效能改善超過 hello 成本重建 hello 索引時，只使用索引。</span><span class="sxs-lookup"><span data-stu-id="47a08-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="47a08-205">批次資料載入</span><span class="sxs-lookup"><span data-stu-id="47a08-205">Batch data loads</span></span>
<span data-ttu-id="47a08-206">當資料載入複寫資料表中，以重試 toominimize 重建一起批次處理載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="47a08-207">執行 select 陳述式之前執行所有批次的 hello 負載。</span><span class="sxs-lookup"><span data-stu-id="47a08-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="47a08-208">例如，以下載入模式會從四個來源載入資料，然後叫用四次重建。</span><span class="sxs-lookup"><span data-stu-id="47a08-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="47a08-209">從來源 1 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-209">Load from source 1.</span></span>
- <span data-ttu-id="47a08-210">Select 陳述式觸發重建 1。</span><span class="sxs-lookup"><span data-stu-id="47a08-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="47a08-211">從來源 2 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-211">Load from source 2.</span></span>
- <span data-ttu-id="47a08-212">Select 陳述式觸發重建 2。</span><span class="sxs-lookup"><span data-stu-id="47a08-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="47a08-213">從來源 3 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-213">Load from source 3.</span></span>
- <span data-ttu-id="47a08-214">Select 陳述式觸發重建 3。</span><span class="sxs-lookup"><span data-stu-id="47a08-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="47a08-215">從來源 4 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-215">Load from source 4.</span></span>
- <span data-ttu-id="47a08-216">Select 陳述式觸發重建 4。</span><span class="sxs-lookup"><span data-stu-id="47a08-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="47a08-217">例如，以下載入模式會從四個來源載入資料，但只會叫用一次重建。</span><span class="sxs-lookup"><span data-stu-id="47a08-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="47a08-218">從來源 1 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-218">Load from source 1.</span></span>
- <span data-ttu-id="47a08-219">從來源 2 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-219">Load from source 2.</span></span>
- <span data-ttu-id="47a08-220">從來源 3 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-220">Load from source 3.</span></span>
- <span data-ttu-id="47a08-221">從來源 4 載入。</span><span class="sxs-lookup"><span data-stu-id="47a08-221">Load from source 4.</span></span>
- <span data-ttu-id="47a08-222">Select 陳述式觸發重建。</span><span class="sxs-lookup"><span data-stu-id="47a08-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="47a08-223">在批次載入後重建複寫資料表</span><span class="sxs-lookup"><span data-stu-id="47a08-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="47a08-224">tooensure 一致的查詢執行時間，建議使用強制重新整理 hello 複寫資料表的批次載入之後。</span><span class="sxs-lookup"><span data-stu-id="47a08-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="47a08-225">否則，hello 第一個查詢必須等候 hello 資料表 toorefresh 包含重建 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="47a08-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="47a08-226">根據 hello 大小和受影響的複寫資料表的數目，hello 效能的影響可能十分顯著。</span><span class="sxs-lookup"><span data-stu-id="47a08-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="47a08-227">此查詢會使用 hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello 複寫已修改，但不重新建立資料表。</span><span class="sxs-lookup"><span data-stu-id="47a08-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="47a08-228">執行陳述式之後 hello 上述輸出中的每個資料表上的 hello tooforce 重建。</span><span class="sxs-lookup"><span data-stu-id="47a08-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="47a08-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47a08-229">Next steps</span></span> 
<span data-ttu-id="47a08-230">toocreate 複寫的資料表，請使用其中一個陳述式：</span><span class="sxs-lookup"><span data-stu-id="47a08-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="47a08-231">CREATE TABLE (Azure SQL 資料倉儲)</span><span class="sxs-lookup"><span data-stu-id="47a08-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="47a08-232">CREATE TABLE AS SELECT (Azure SQL 資料倉儲)</span><span class="sxs-lookup"><span data-stu-id="47a08-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="47a08-233">如需分散式資料表的概觀，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。</span><span class="sxs-lookup"><span data-stu-id="47a08-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



