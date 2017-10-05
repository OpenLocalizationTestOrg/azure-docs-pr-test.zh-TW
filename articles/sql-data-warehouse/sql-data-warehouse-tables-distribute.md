---
title: "在 SQL 資料倉儲中散發資料表 | Microsoft Docs"
description: "開始在 Azure SQL 資料倉儲中散發資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="e9dcf-103">在 SQL 資料倉儲中散發資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e9dcf-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e9dcf-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="e9dcf-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="e9dcf-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-107">[Index][Index]</span></span>
> * <span data-ttu-id="e9dcf-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="e9dcf-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="e9dcf-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="e9dcf-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="e9dcf-111">SQL 資料倉儲是大量平行處理 (MPP) 分散式資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="e9dcf-112">將資料和處理能力分割於多個節點之間，SQL 資料倉儲就能夠提供極大的延展性 - 遠超過任何單一系統。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="e9dcf-113">決定如何在 SQL 資料倉儲內散發資料是達到最佳效能的最重要因素之一。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="e9dcf-114">要達到最佳效能的關鍵是將資料移動降至最低，而將資料移動降至最低的關鍵是選取正確的散發策略。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="e9dcf-115">了解資料移動</span><span class="sxs-lookup"><span data-stu-id="e9dcf-115">Understanding data movement</span></span>
<span data-ttu-id="e9dcf-116">在 MPP 系統中，每個資料表中的資料會被分到數個基礎資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="e9dcf-117">MPP 系統上最佳化的查詢可以只傳遞到個別分散式資料庫上執行，與其他資料庫之間不需要互動。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="e9dcf-118">例如，假設您的銷售資料的資料庫有「銷售」和「客戶」兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="e9dcf-119">如果您的查詢需要將銷售資料表和客戶資料表聯結，而您將銷售和客戶資料表都依客戶編號分開，將每個客戶放在不同的資料庫，則任何聯結銷售和客戶的查詢皆可以在各個資料庫中解決，不需要知道其他資料庫的存在。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="e9dcf-120">相較之下，如果您將銷售資料依訂單編號分開，將客戶資料依客戶編號分開，則任何一個資料庫皆不會有每位客戶的相對應資料，因此，如果您想要將銷售資料聯結至客戶資料，便需要從其他資料庫取得每位客戶的資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="e9dcf-121">在這第二個範例中，需要移動資料，將客戶資料移至銷售資料，如此才可以聯結兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="e9dcf-122">資料移動不一定是一件壞事，有時候是要解決查詢的必要手段。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="e9dcf-123">但當您可以避免這個額外的步驟，自然地查詢的執行速度會更快。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="e9dcf-124">資料移動最常發生於聯結資料表或執行彙總時。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="e9dcf-125">通常您兩種都需要做，因此即使您可以最佳化其中一種情況，例如聯結，您仍需要資料移動來幫您解決其他案例，例如彙總。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="e9dcf-126">訣竅是找出哪一個較少工作。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="e9dcf-127">大多數情況下，在通常聯結的資料行上散發大型事實資料表，是將資料移動降至最低的最有效方法。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="e9dcf-128">相較於散發彙總牽涉到的資料行資料，散發聯結資料行上的資料，是減少資料移動更為普遍的方法。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="e9dcf-129">選擇散發方法</span><span class="sxs-lookup"><span data-stu-id="e9dcf-129">Select distribution method</span></span>
<span data-ttu-id="e9dcf-130">SQL 資料倉儲會在幕後將您的資料分成 60 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="e9dcf-131">每個個別的資料庫都稱為 **散發**。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="e9dcf-132">當資料載入每個資料表時，SQL 資料倉儲必須知道如何將資料分成這 60 個散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="e9dcf-133">散發方法會定義於資料表層級，目前有兩個選擇︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="e9dcf-134">**循環配置資源** 會平均但隨機散發資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="e9dcf-135">**雜湊散發** 會根據單一資料行的雜湊值散發資料</span><span class="sxs-lookup"><span data-stu-id="e9dcf-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="e9dcf-136">根據預設，如果未定義資料散發方式，您的資料表會使用 **循環配置資源** 散發方法進行散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="e9dcf-137">不過，當您日益熟練實作，您會考慮使用 **雜湊散發** 資料表將資料移動降至最低，進而使查詢效能達到最佳化。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="e9dcf-138">循環配置資源資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-138">Round Robin Tables</span></span>
<span data-ttu-id="e9dcf-139">使用循環配置資源方法來散發資料名符其實。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="e9dcf-140">載入資料後，每個資料列只會傳送到下一個散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="e9dcf-141">此種資料散發方法一律會將資料非常平均地隨機散發到所有的散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="e9dcf-142">也就是說，在放置資料的循環配置資源處理期間，不會進行任何排序。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="e9dcf-143">基於這個理由，循環配置資源散發有時稱為隨機雜湊。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="e9dcf-144">使用循環配置資源分散式資料表，不需要了解資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="e9dcf-145">基於這個理由，循環配置資源資料表通常具有良好的載入目標。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="e9dcf-146">根據預設，如果未選擇散發方法，則會使用循環配置資源散發方法。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="e9dcf-147">不過，雖然循環配置資源資料表很容易使用，但因為資料會隨機分散於系統，這表示系統無法保證每個資料列位於哪個發散。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="e9dcf-148">因此，系統有時候需要叫用資料移動作業，才能在解析查詢前，更加妥善地組織您的資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="e9dcf-149">此額外步驟會使您的查詢變慢。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="e9dcf-150">在下列情況下，請考慮對資料表使用循環配置資源散發：</span><span class="sxs-lookup"><span data-stu-id="e9dcf-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="e9dcf-151">以簡單的起點開始使用時</span><span class="sxs-lookup"><span data-stu-id="e9dcf-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="e9dcf-152">如果沒有明顯的聯結索引鍵</span><span class="sxs-lookup"><span data-stu-id="e9dcf-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="e9dcf-153">如果沒有合適的候選資料行可供雜湊散發資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="e9dcf-154">如果資料表並未與其他資料表共用常見的聯結索引鍵</span><span class="sxs-lookup"><span data-stu-id="e9dcf-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="e9dcf-155">如果此聯結比查詢中的其他聯結較不重要</span><span class="sxs-lookup"><span data-stu-id="e9dcf-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="e9dcf-156">當資料表是暫存預備資料表時</span><span class="sxs-lookup"><span data-stu-id="e9dcf-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="e9dcf-157">兩個範例都會建立循環配置資源資料表︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="e9dcf-158">雖然循環配置資源是預設資料表類型，但以您的 DDL 明確表示被視為最佳做法，讓其他人能夠清楚了解您的資料表配置的意圖。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="e9dcf-159">雜湊散發資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-159">Hash Distributed Tables</span></span>
<span data-ttu-id="e9dcf-160">使用 **雜湊散發** 演算法來散發您的資料表，可減少查詢時的資料移動，進而改善許多案例的效能。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="e9dcf-161">雜湊散發資料表是在您選取的單一資料行上使用雜湊演算法，分配於分散式資料庫間的資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="e9dcf-162">散發資料行可決定如何將資料分配於您的分散式資料庫。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="e9dcf-163">雜湊函式會使用散發資料行將資料列指派給散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="e9dcf-164">雜湊演算法與所產生的散發具決定性。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="e9dcf-165">也就是，相同資料類型的相同值永遠都使用相同的散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="e9dcf-166">這個範例會建立依照識別碼散發的資料表︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="e9dcf-167">選擇散發資料行</span><span class="sxs-lookup"><span data-stu-id="e9dcf-167">Select distribution column</span></span>
<span data-ttu-id="e9dcf-168">當您選擇 **雜湊散發** 資料表時，您必須選取單一散發資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="e9dcf-169">選取散發資料行時，需要考量三個主要因素。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="e9dcf-170">選取具有下列特性的單一資料行︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-170">Select a single column which will:</span></span>

1. <span data-ttu-id="e9dcf-171">不會更新</span><span class="sxs-lookup"><span data-stu-id="e9dcf-171">Not be updated</span></span>
2. <span data-ttu-id="e9dcf-172">平均散發資料，以避免資料扭曲</span><span class="sxs-lookup"><span data-stu-id="e9dcf-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="e9dcf-173">最小化資料移動</span><span class="sxs-lookup"><span data-stu-id="e9dcf-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="e9dcf-174">選取不會更新的散發資料行</span><span class="sxs-lookup"><span data-stu-id="e9dcf-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="e9dcf-175">散發資料行不可更新，因此，選取具靜態值的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="e9dcf-176">如果資料行需要更新，該資料行通常不是理想的散發候選項目。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="e9dcf-177">如果您必須更新散發資料行，做法是先刪除資料列，然後插入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="e9dcf-178">選取將平均散發資料的散發資料行</span><span class="sxs-lookup"><span data-stu-id="e9dcf-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="e9dcf-179">分散式系統的執行速度只與其最慢的散發一樣快，所以務必將工作平均分配於各散發，以便讓系統達到平衡的執行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="e9dcf-180">工作會根據每個散發的資料所在位置，分配於分散式系統。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="e9dcf-181">這對於選取正確的散發資料行來散發資料非常重要，如此一來，每個散發都有相等的工作，而且完成其工作部分所需的時間相同。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="e9dcf-182">當工作在系統中分配良好時，資料的散發就會平衡。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="e9dcf-183">當資料不平衡時，我們將此稱為 **資料扭曲**。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="e9dcf-184">若要平均分配資料以避免資料扭曲，請在選取散發資料行時考量下列各項︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="e9dcf-185">選取包含大量相異值的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="e9dcf-186">避免將資料散發於含有少許相異值的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="e9dcf-187">避免將資料散發於 null 頻繁出現的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="e9dcf-188">避免在日期資料行上散發資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="e9dcf-189">因為每個值會雜湊至 60 個散發之一，若要達到平均散發，您要選取極為獨特並包含超過 60 個唯一值的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="e9dcf-190">為了方便解說，請考慮資料行只有 40 個唯一值的案例。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="e9dcf-191">如果選取此資料行做為散發索引鍵，則該資料表的資料最多會落在 40 個散發，以致 20 個散發不含任何資料，而且沒有要進行的處理。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="e9dcf-192">相反地，如果資料平均分散於 60 個散發，則其他 40 個散發有更多工作需要進行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="e9dcf-193">這個案例就是資料扭曲的範例。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="e9dcf-194">在 MPP 系統中，每個查詢步驟會等待所有散發完成它們的工作部分。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="e9dcf-195">若某個散發進行的工作較其他散發多，則其他散發的資源會因為等待該忙碌的散發而浪費。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="e9dcf-196">當所有散發的工作分配不均時，我們將此稱為 **處理誤差**。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="e9dcf-197">處理誤差將造成查詢的執行速度比工作負載平均分配於散發時更慢。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="e9dcf-198">資料扭曲將導致處理誤差。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="e9dcf-199">避免散發於高度可為 null 的資料行，因為 null 值將全部落在相同的散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="e9dcf-200">散發於日期資料行也可能造成處理誤差，因為指定日期的所有資料將落在相同的散發。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="e9dcf-201">如果數個使用者正在執行的查詢均篩選相同日期，則 60 個散發中只有 1 個會執行所有工作，因為一個指定日期只會在一個散發中。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="e9dcf-202">在此案例中，查詢的執行速度可能比資料平均分配於所有散發時慢 60 倍。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="e9dcf-203">若沒有理想的候選資料行存在，則考慮使用循環配置資源做為散發方法。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="e9dcf-204">選取會將資料移動降至最低的散發資料行</span><span class="sxs-lookup"><span data-stu-id="e9dcf-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="e9dcf-205">藉由選取適當散發資料行來將資料移動降至最低，是讓 SQL 資料倉儲的效能達到最佳化的最重要策略之一。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="e9dcf-206">資料移動最常發生於聯結資料表或執行彙總時。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="e9dcf-207">用於 `JOIN`、`GROUP BY`、`DISTINCT`、`OVER`、`HAVING` 子句的資料行全都是**理想**的雜湊散發候選項目。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="e9dcf-208">另一方面，用於 `WHERE` 子句的資料行 **不是** 理想的雜湊資料行候選項目，因為它們會限制哪些散發參與查詢，因而導致處理誤差。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="e9dcf-209">可能適合用於散發但通常會造成此處理誤差的資料行範例，就是日期資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="e9dcf-210">一般而言，如果您有兩個經常涉入聯結的大型事實資料表，將兩個資料表散發在其中一個聯結資料行上可得到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="e9dcf-211">如果您有永遠不會聯結到另一個大型事實資料表的資料表，則尋找經常出現在 `GROUP BY` 子句中的資料行。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="e9dcf-212">有幾個關鍵條件必須符合，以避免聯結期間的資料移動︰</span><span class="sxs-lookup"><span data-stu-id="e9dcf-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="e9dcf-213">參與聯結之資料行的相關資料表必須雜湊散發於其中 **一個** 聯結資料行上。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="e9dcf-214">兩個資料表間聯結資料行的資料類型必須相符。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="e9dcf-215">資料行必須以 equals 運算子聯結。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="e9dcf-216">聯結類型可能不是 `CROSS JOIN`。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="e9dcf-217">資料扭曲疑難排解</span><span class="sxs-lookup"><span data-stu-id="e9dcf-217">Troubleshooting data skew</span></span>
<span data-ttu-id="e9dcf-218">資料表的資料是使用雜湊散發方法來散發時，有些散發可能會扭曲，會比其他資料表具有更多資料。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="e9dcf-219">過多資料扭曲可能會影響查詢效能，因為散發查詢的最終結果必須等待執行時間最長的散發完成。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="e9dcf-220">視資料扭曲的程度而定，您可能需要處理它。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="e9dcf-221">識別扭曲</span><span class="sxs-lookup"><span data-stu-id="e9dcf-221">Identifying skew</span></span>
<span data-ttu-id="e9dcf-222">識別資料表扭曲的簡單方法是使用 `DBCC PDW_SHOWSPACEUSED`。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="e9dcf-223">這個非常快速且簡單的方式，用來查看儲存在您資料庫中每 60 個散發內的資料表資料列數目。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="e9dcf-224">請記住，為了達到最平衡的效能，分散式資料表中的資料列應該平均分散到所有散發中。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="e9dcf-225">不過，如果您查詢 Azure SQL 資料倉儲動態管理檢視 (DMV)，則可以執行更詳細的分析。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="e9dcf-226">若要開始，請使用[資料表概觀][Overview]一文中的 SQL 建立 [dbo.vTableSizes][dbo.vTableSizes] 檢視。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="e9dcf-227">建立檢視後，請執行此查詢來識別哪些資料表有 10% 以上的資料扭曲。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="e9dcf-228">解決資料扭曲</span><span class="sxs-lookup"><span data-stu-id="e9dcf-228">Resolving data skew</span></span>
<span data-ttu-id="e9dcf-229">並非所有的扭曲都足以批准修正。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="e9dcf-230">在某些情況下，某些查詢中的資料表效能可以超越資料扭曲的傷害。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="e9dcf-231">若要決定是否應該解決資料表中的資料扭曲，您應該盡可能了解工作負載中的資料磁區和查詢。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="e9dcf-232">查看扭曲影響的方法之一是使用[查詢監視][Query Monitoring]一文中的步驟，監視扭曲對於查詢效能的影響，尤其是對在個別散發上完成查詢所需時間的影響。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="e9dcf-233">散發資料就是找出將資料扭曲降至最低與將資料移動降至最低兩者之間的正確平衡點。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="e9dcf-234">這些可能是相反的目標，有時候您會想要保留資料扭曲，以減少資料移動。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="e9dcf-235">比方說，當散發資料行經常是聯結和彙總中的共用資料行時，您便會將資料移動降至最低。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="e9dcf-236">擁有最少的資料移動，所帶來的好處可能勝過具有資料扭曲的影響。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="e9dcf-237">解決資料扭曲的一般方式，是重新建立具有不同散發資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="e9dcf-238">沒有任何方法可變更現有資料表上的散發資料行，所以變更資料表散發的方法是使用 [CTAS][] 重建資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="e9dcf-239">以下是解決資料扭曲的兩個範例：</span><span class="sxs-lookup"><span data-stu-id="e9dcf-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="e9dcf-240">範例 1︰重建具有新散發資料行的資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="e9dcf-241">此範例會使用 [CTAS][] 來重建具有不同雜湊資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="e9dcf-242">範例 2︰使用循環配置資源散發重建資料表</span><span class="sxs-lookup"><span data-stu-id="e9dcf-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="e9dcf-243">此範例會使用 [CTAS][] 來重建具有循環配置資源 (而非雜湊散發) 的資料表。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="e9dcf-244">這項變更將會產生平均的資料散發，但代價是資料移動增加。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="e9dcf-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9dcf-245">Next steps</span></span>
<span data-ttu-id="e9dcf-246">若要深入了解資料表設計，請參閱[散發][Distribute]、[索引][Index]、[資料分割][Partition]、[資料類型][Data Types]、[統計資料][Statistics] 和 [暫存資料表][Temporary]等文章。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="e9dcf-247">如需最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="e9dcf-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
