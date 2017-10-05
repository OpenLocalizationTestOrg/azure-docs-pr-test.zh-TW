---
title: "複寫資料表設計指引 - Azure SQL 資料倉儲 | Microsoft Docs"
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
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="d88e4-103">在 Azure SQL 資料倉儲中使用複寫資料表的設計指引</span><span class="sxs-lookup"><span data-stu-id="d88e4-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d88e4-104">本文針對在「SQL 資料倉儲」結構描述中設計複寫資料表提供建議。</span><span class="sxs-lookup"><span data-stu-id="d88e4-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="d88e4-105">您可以使用這些建議來降低資料移動和查詢的複雜性，以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="d88e4-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="d88e4-106">複寫資料表功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="d88e4-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="d88e4-107">有些行為可能會變更。</span><span class="sxs-lookup"><span data-stu-id="d88e4-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="d88e4-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d88e4-108">Prerequisites</span></span>
<span data-ttu-id="d88e4-109">本文假設您已熟悉「SQL 資料倉儲」中的資料散發和資料移動概念。</span><span class="sxs-lookup"><span data-stu-id="d88e4-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="d88e4-110">如需詳細資訊，請參閱[分散式資料](sql-data-warehouse-distributed-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d88e4-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="d88e4-111">在資料表設計過程中，請儘可能了解您的資料及查詢資料的方式。</span><span class="sxs-lookup"><span data-stu-id="d88e4-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="d88e4-112">例如，請思考一下下列問題：</span><span class="sxs-lookup"><span data-stu-id="d88e4-112">For example, consider these questions:</span></span>

- <span data-ttu-id="d88e4-113">資料表的大小為何？</span><span class="sxs-lookup"><span data-stu-id="d88e4-113">How large is the table?</span></span>   
- <span data-ttu-id="d88e4-114">資料表的重新整理頻率為何？</span><span class="sxs-lookup"><span data-stu-id="d88e4-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="d88e4-115">我是否在資料倉儲中有事實資料表和維度資料表？</span><span class="sxs-lookup"><span data-stu-id="d88e4-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="d88e4-116">什麼是複寫資料表？</span><span class="sxs-lookup"><span data-stu-id="d88e4-116">What is a replicated table?</span></span>
<span data-ttu-id="d88e4-117">複寫資料表在每個計算節點上都有一份可存取的完整資料表複本。</span><span class="sxs-lookup"><span data-stu-id="d88e4-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="d88e4-118">複寫資料表可使在進行聯結或彙總之前，不需要在計算節點之間傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="d88e4-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="d88e4-119">由於資料表有多個複本，因此當資料表大小在壓縮後小於 2 GB 時，複寫資料表的運作效能最佳。</span><span class="sxs-lookup"><span data-stu-id="d88e4-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="d88e4-120">下圖顯示每個計算節點上可存取的複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="d88e4-121">在「SQL 資料倉儲」中，會將複寫資料表完整複製到每個計算節點上的散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="d88e4-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="d88e4-122">![複寫的資料表](media/guidance-for-using-replicated-tables/replicated-table.png "複寫的資料表")</span><span class="sxs-lookup"><span data-stu-id="d88e4-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="d88e4-123">複寫資料表適用於星型結構描述中的小型維度資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="d88e4-124">維度資料表的大小通常是適合儲存及維護多個複本的大小。</span><span class="sxs-lookup"><span data-stu-id="d88e4-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="d88e4-125">維度會儲存變更緩慢的描述性資料，例如客戶名稱和地址，以及產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d88e4-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="d88e4-126">資料的變更緩慢特性導致較少發生重建複寫資料表的情況。</span><span class="sxs-lookup"><span data-stu-id="d88e4-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="d88e4-127">在下列情況下，請考慮使用複寫資料表：</span><span class="sxs-lookup"><span data-stu-id="d88e4-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="d88e4-128">磁碟上的資料表大小小於 2 GB，不論它有幾個資料列。</span><span class="sxs-lookup"><span data-stu-id="d88e4-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="d88e4-129">若要了解資料表的大小，您可以使用 [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) 命令：`DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`。</span><span class="sxs-lookup"><span data-stu-id="d88e4-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="d88e4-130">資料表用於需要進行資料移動的聯結中。</span><span class="sxs-lookup"><span data-stu-id="d88e4-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="d88e4-131">例如，當聯結資料行不是相同的散發資料行時，雜湊分散式資料表上的聯結就需要進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="d88e4-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="d88e4-132">如果其中一個雜湊分散式資料表是小型資料表，請考慮使用複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="d88e4-133">循環配置資源資料表上的聯結需要進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="d88e4-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="d88e4-134">建議您在大多數情況下都使用複寫資料表，而不要使用循環配置資源資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="d88e4-135">在下列情況下，請考慮將現有的分散式資料表轉換成複寫資料表：</span><span class="sxs-lookup"><span data-stu-id="d88e4-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="d88e4-136">查詢計劃使用會將資料廣播到所有計算節點的資料移動作業。</span><span class="sxs-lookup"><span data-stu-id="d88e4-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="d88e4-137">BroadcastMoveOperation 相當耗費資源，並且會降低查詢效能。</span><span class="sxs-lookup"><span data-stu-id="d88e4-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="d88e4-138">若要檢視查詢計劃中的資料移動作業，請使用 [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="d88e4-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="d88e4-139">在下列情況下，複寫資料表可能無法產生最佳查詢效能：</span><span class="sxs-lookup"><span data-stu-id="d88e4-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="d88e4-140">資料表有頻繁的插入、更新及刪除作業。</span><span class="sxs-lookup"><span data-stu-id="d88e4-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="d88e4-141">這些資料操作語言 (DML) 作業需要重建複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="d88e4-142">經常重建會導致效能變差。</span><span class="sxs-lookup"><span data-stu-id="d88e4-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="d88e4-143">經常調整資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="d88e4-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="d88e4-144">調整資料倉儲會變更計算節點數目，進而導致重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="d88e4-145">資料表有大量資料行，但資料作業通常只存取少數資料行。</span><span class="sxs-lookup"><span data-stu-id="d88e4-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="d88e4-146">在此情況下，以雜湊方式散發資料表，然後針對經常存取的資料行建立索引，可能會比複寫整個資料表還要有效。</span><span class="sxs-lookup"><span data-stu-id="d88e4-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="d88e4-147">當查詢需要進行資料移動時，「SQL 資料倉儲」只會移動所要求資料行中的資料。</span><span class="sxs-lookup"><span data-stu-id="d88e4-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="d88e4-148">使用複寫資料表搭配簡單查詢述詞</span><span class="sxs-lookup"><span data-stu-id="d88e4-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="d88e4-149">在您選擇是要散發還是複寫資料表之前，請先思考您打算對資料表執行的查詢類型。</span><span class="sxs-lookup"><span data-stu-id="d88e4-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="d88e4-150">請儘可能</span><span class="sxs-lookup"><span data-stu-id="d88e4-150">Whenever possible,</span></span>

- <span data-ttu-id="d88e4-151">針對含有簡單查詢述詞 (例如相等比較或不等比較) 的查詢使用複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="d88e4-152">針對含有複雜查詢述詞 (例如相似或不相似) 的查詢使用分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="d88e4-153">需要大量 CPU 的查詢在工作分散於所有計算節點時效能最佳。</span><span class="sxs-lookup"><span data-stu-id="d88e4-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="d88e4-154">例如，以在資料表的每個資料列上執行計算的查詢來說，在複寫資料表上執行會比在分散式資料表上執行效能更佳。</span><span class="sxs-lookup"><span data-stu-id="d88e4-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="d88e4-155">由於複寫資料表是完整儲存在每個計算節點上，因此對複寫資料表執行需要大量 CPU 的查詢時，執行對象會是每個計算節點上的整個資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="d88e4-156">額外的計算會降低查詢效能。</span><span class="sxs-lookup"><span data-stu-id="d88e4-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="d88e4-157">例如，此查詢含有複雜的述詞。</span><span class="sxs-lookup"><span data-stu-id="d88e4-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="d88e4-158">當供應者是分散式資料表而不是複寫資料表時，它的執行速度較快。</span><span class="sxs-lookup"><span data-stu-id="d88e4-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="d88e4-159">在此範例中，供應者可以是雜湊分散式或循環配置資源分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="d88e4-160">將現有的循環配置資源資料表轉換成分散式資料表</span><span class="sxs-lookup"><span data-stu-id="d88e4-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="d88e4-161">如果您已經有循環配置資源資料表，而且它們符合本文中所述的準則，建議您將它們轉換成複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="d88e4-162">複寫資料表可提升循環配置資源資料表的效能，因為它們不需進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="d88e4-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="d88e4-163">循環配置資源資料表針對聯結一律需要進行資料移動。</span><span class="sxs-lookup"><span data-stu-id="d88e4-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="d88e4-164">此範例使用 [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) 將 DimSalesTerritory 資料表變更為複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="d88e4-165">不論 DimSalesTerritory 是雜湊分散式還是循環配置資源資料表，此範例都有效。</span><span class="sxs-lookup"><span data-stu-id="d88e4-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="d88e4-166">循環配置資源與複寫之查詢效能比較範例</span><span class="sxs-lookup"><span data-stu-id="d88e4-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="d88e4-167">複寫資料表針對聯結不需要進行任何資料移動，因為整個資料表已經存在於每個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="d88e4-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="d88e4-168">如果維度資料表是循環配置資源分散式資料表，聯結就會將整個維度資料表複製到每個計算節點。</span><span class="sxs-lookup"><span data-stu-id="d88e4-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="d88e4-169">為了移動資料，查詢計劃會包含一個名為 BroadcastMoveOperation 的作業。</span><span class="sxs-lookup"><span data-stu-id="d88e4-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="d88e4-170">這類資料移動作業會降低查詢效能，而使用複寫資料表則可免除這類作業。</span><span class="sxs-lookup"><span data-stu-id="d88e4-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="d88e4-171">若要檢視查詢計劃步驟，請使用 [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) 系統目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="d88e4-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="d88e4-172">例如，在以下針對 AdventureWorks 結構描述執行的查詢中，` FactInternetSales` 資料表是雜湊分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="d88e4-173">`DimDate` 和 `DimSalesTerritory` 資料表是較小型的維度資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="d88e4-174">此查詢會傳回 2004 會計年度北美的總銷售額：</span><span class="sxs-lookup"><span data-stu-id="d88e4-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="d88e4-175">我們已將 `DimDate` 和 `DimSalesTerritory` 重新建立成循環配置資源資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="d88e4-176">因此，此查詢顯示了以下查詢計劃，其中包含多個廣播移動作業：</span><span class="sxs-lookup"><span data-stu-id="d88e4-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![循環配置資源的查詢計劃](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="d88e4-178">我們已將 `DimDate` 和 `DimSalesTerritory` 重新建立成複寫資料表，並已重新執行查詢。</span><span class="sxs-lookup"><span data-stu-id="d88e4-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="d88e4-179">產生的查詢計劃長度變短許多，且沒有任何廣播移動。</span><span class="sxs-lookup"><span data-stu-id="d88e4-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![複寫的查詢計劃](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="d88e4-181">修改複寫資料表時的效能考量</span><span class="sxs-lookup"><span data-stu-id="d88e4-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="d88e4-182">「SQL 資料倉儲」是透過維護資料表的主要版本來實作複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="d88e4-183">它會將主要版本複製到每個計算節點上的一個散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="d88e4-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="d88e4-184">當發生變更時，「SQL 資料倉儲」會先更新主資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="d88e4-185">接著，它會要求重建每個計算節點上的資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="d88e4-186">重建複寫資料表包括將資料表複製到每個計算節點，然後重建索引。</span><span class="sxs-lookup"><span data-stu-id="d88e4-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="d88e4-187">在執行下列動作之後，必須進行重建：</span><span class="sxs-lookup"><span data-stu-id="d88e4-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="d88e4-188">載入或修改資料</span><span class="sxs-lookup"><span data-stu-id="d88e4-188">Data is loaded or modified</span></span>
- <span data-ttu-id="d88e4-189">將資料倉儲調整成不同的 DWU 設定</span><span class="sxs-lookup"><span data-stu-id="d88e4-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="d88e4-190">更新資料表定義</span><span class="sxs-lookup"><span data-stu-id="d88e4-190">Table definition is updated</span></span>

<span data-ttu-id="d88e4-191">在執行下列動作之後，不須進行重建：</span><span class="sxs-lookup"><span data-stu-id="d88e4-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="d88e4-192">暫停作業</span><span class="sxs-lookup"><span data-stu-id="d88e4-192">Pause operation</span></span>
- <span data-ttu-id="d88e4-193">繼續作業</span><span class="sxs-lookup"><span data-stu-id="d88e4-193">Resume operation</span></span>

<span data-ttu-id="d88e4-194">在修改資料之後，不會立即進行重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="d88e4-195">取而代之的是，會在查詢從資料表選取資料時觸發重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="d88e4-196">在從資料表進行選取的初始 select 陳述式內，包含重建複寫資料表的步驟。</span><span class="sxs-lookup"><span data-stu-id="d88e4-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="d88e4-197">由於重建是在查詢內進行的，因此視資料表的大小而定，可能會對初始 select 陳述式造成明顯的影響。</span><span class="sxs-lookup"><span data-stu-id="d88e4-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="d88e4-198">如果牽涉到多個需要重建的複寫資料表，將會如陳述式內的步驟一般，循序重建每個複本。</span><span class="sxs-lookup"><span data-stu-id="d88e4-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="d88e4-199">為了在重建複寫資料表時維持資料一致性，會在資料表上進行獨佔鎖定。</span><span class="sxs-lookup"><span data-stu-id="d88e4-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="d88e4-200">此鎖定會在重建持續時間，防止所有對資料表進行的存取。</span><span class="sxs-lookup"><span data-stu-id="d88e4-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="d88e4-201">謹慎地使用索引</span><span class="sxs-lookup"><span data-stu-id="d88e4-201">Use indexes conservatively</span></span>
<span data-ttu-id="d88e4-202">標準索引編製做法適用於複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="d88e4-203">「SQL 資料倉儲」會在重建時，一併重建每個複寫資料表索引。</span><span class="sxs-lookup"><span data-stu-id="d88e4-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="d88e4-204">請只有在效能的提升超過重建索引的代價時，才使用索引。</span><span class="sxs-lookup"><span data-stu-id="d88e4-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="d88e4-205">批次資料載入</span><span class="sxs-lookup"><span data-stu-id="d88e4-205">Batch data loads</span></span>
<span data-ttu-id="d88e4-206">將資料載入複寫資料表時，請嘗試一起批次載入，以將重建次數降到最低。</span><span class="sxs-lookup"><span data-stu-id="d88e4-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="d88e4-207">請在執行 select 陳述式之前，先執行所有批次處理的載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="d88e4-208">例如，以下載入模式會從四個來源載入資料，然後叫用四次重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="d88e4-209">從來源 1 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-209">Load from source 1.</span></span>
- <span data-ttu-id="d88e4-210">Select 陳述式觸發重建 1。</span><span class="sxs-lookup"><span data-stu-id="d88e4-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="d88e4-211">從來源 2 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-211">Load from source 2.</span></span>
- <span data-ttu-id="d88e4-212">Select 陳述式觸發重建 2。</span><span class="sxs-lookup"><span data-stu-id="d88e4-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="d88e4-213">從來源 3 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-213">Load from source 3.</span></span>
- <span data-ttu-id="d88e4-214">Select 陳述式觸發重建 3。</span><span class="sxs-lookup"><span data-stu-id="d88e4-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="d88e4-215">從來源 4 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-215">Load from source 4.</span></span>
- <span data-ttu-id="d88e4-216">Select 陳述式觸發重建 4。</span><span class="sxs-lookup"><span data-stu-id="d88e4-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="d88e4-217">例如，以下載入模式會從四個來源載入資料，但只會叫用一次重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="d88e4-218">從來源 1 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-218">Load from source 1.</span></span>
- <span data-ttu-id="d88e4-219">從來源 2 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-219">Load from source 2.</span></span>
- <span data-ttu-id="d88e4-220">從來源 3 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-220">Load from source 3.</span></span>
- <span data-ttu-id="d88e4-221">從來源 4 載入。</span><span class="sxs-lookup"><span data-stu-id="d88e4-221">Load from source 4.</span></span>
- <span data-ttu-id="d88e4-222">Select 陳述式觸發重建。</span><span class="sxs-lookup"><span data-stu-id="d88e4-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="d88e4-223">在批次載入後重建複寫資料表</span><span class="sxs-lookup"><span data-stu-id="d88e4-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="d88e4-224">為了確保查詢執行時間一致，建議您在批次載入後，強制重新整理複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="d88e4-225">否則，第一個查詢將必須等候資料表重新整理，其中包括重建索引。</span><span class="sxs-lookup"><span data-stu-id="d88e4-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="d88e4-226">視受影響的複寫資料表大小和數目而定，可能會有明顯的效能影響。</span><span class="sxs-lookup"><span data-stu-id="d88e4-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="d88e4-227">此查詢使用 [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV 來列出已修改但未重建的複寫資料表。</span><span class="sxs-lookup"><span data-stu-id="d88e4-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="d88e4-228">若要強制重建，請針對上面輸出中的每個資料表執行下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="d88e4-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="d88e4-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d88e4-229">Next steps</span></span> 
<span data-ttu-id="d88e4-230">若要建立複寫資料表，請使用下列其中一個陳述式：</span><span class="sxs-lookup"><span data-stu-id="d88e4-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="d88e4-231">CREATE TABLE (Azure SQL 資料倉儲)</span><span class="sxs-lookup"><span data-stu-id="d88e4-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="d88e4-232">CREATE TABLE AS SELECT (Azure SQL 資料倉儲)</span><span class="sxs-lookup"><span data-stu-id="d88e4-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="d88e4-233">如需分散式資料表的概觀，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。</span><span class="sxs-lookup"><span data-stu-id="d88e4-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



