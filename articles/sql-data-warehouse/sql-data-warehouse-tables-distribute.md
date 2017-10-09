---
title: "SQL 資料倉儲中的 aaaDistributing 資料表 |Microsoft 文件"
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="78b76-103">在 SQL 資料倉儲中散發資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="78b76-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="78b76-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="78b76-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="78b76-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="78b76-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="78b76-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="78b76-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="78b76-107">[Index][Index]</span></span>
> * <span data-ttu-id="78b76-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="78b76-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="78b76-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="78b76-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="78b76-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="78b76-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="78b76-111">SQL 資料倉儲是大量平行處理 (MPP) 分散式資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="78b76-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="78b76-112">將資料和處理能力分割於多個節點之間，SQL 資料倉儲就能夠提供極大的延展性 - 遠超過任何單一系統。</span><span class="sxs-lookup"><span data-stu-id="78b76-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="78b76-113">決定如何 toodistribute 您的 SQL 資料倉儲中的資料最重要的 hello 的其中一個因素 tooachieving 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="78b76-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="78b76-114">hello 金鑰 toooptimal 效能最小化資料移動，然後依次 hello 金鑰 toominimizing 資料移動選取 hello 右散發策略。</span><span class="sxs-lookup"><span data-stu-id="78b76-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="78b76-115">了解資料移動</span><span class="sxs-lookup"><span data-stu-id="78b76-115">Understanding data movement</span></span>
<span data-ttu-id="78b76-116">MPP 系統、 在每個資料表中的 hello 資料分割到數個基礎資料庫。</span><span class="sxs-lookup"><span data-stu-id="78b76-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="78b76-117">hello 最最佳化查詢 MPP 系統上的可以只傳遞 tooexecute hello 上個別的分散式的資料庫，而不需要互動之間 hello 其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="78b76-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="78b76-118">例如，假設您的銷售資料的資料庫有「銷售」和「客戶」兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="78b76-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="78b76-119">如果您有需要 toojoin sales 資料表 tooyour 客戶資料表的查詢，並除以銷售和客戶資料表總客戶編號置於個別的資料庫中的每一位客戶，任何加入銷售和客戶的查詢就可以解決在每個不知道資料庫 hello 其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="78b76-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="78b76-120">相反地，如果銷售資料除以訂單號碼，而您的客戶資料，客戶數目時，然後任何指定的資料庫不會有 hello 相對應的資料每個客戶，因此如果您想 toojoin 銷售資料 tooyour 客戶資料，您需要tooget hello 資料每個客戶的 hello 其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="78b76-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="78b76-121">在第二個範例中，移動資料將需要 toooccur toomove hello 客戶資料 toohello 銷售資料，因此 hello 兩個資料表可以聯結。</span><span class="sxs-lookup"><span data-stu-id="78b76-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="78b76-122">資料移動不一定是一件壞事，有時候很有必要 toosolve 查詢。</span><span class="sxs-lookup"><span data-stu-id="78b76-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="78b76-123">但當您可以避免這個額外的步驟，自然地查詢的執行速度會更快。</span><span class="sxs-lookup"><span data-stu-id="78b76-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="78b76-124">資料移動最常發生於聯結資料表或執行彙總時。</span><span class="sxs-lookup"><span data-stu-id="78b76-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="78b76-125">通常您需要 toodo 兩者，您可能無法 toooptimize 一種情況，例如聯結，您仍然必須解決的資料移動 toohelp hello 其他案例中的，例如彙總。</span><span class="sxs-lookup"><span data-stu-id="78b76-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="78b76-126">hello 訣竅找出這是較少工作。</span><span class="sxs-lookup"><span data-stu-id="78b76-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="78b76-127">在大部分情況下，散發大型事實資料表經常聯結的資料行上是 hello 最有效方法以降低 hello 大部分的資料移動。</span><span class="sxs-lookup"><span data-stu-id="78b76-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="78b76-128">散發資料聯結資料行上的進行更多的常見方法 tooreduce 資料移動比散發到彙總中的資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="78b76-129">選擇散發方法</span><span class="sxs-lookup"><span data-stu-id="78b76-129">Select distribution method</span></span>
<span data-ttu-id="78b76-130">Hello 幕後 SQL 資料倉儲會將您的資料分割成 60 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="78b76-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="78b76-131">每個個別的資料庫是參照的 tooas**發佈**。</span><span class="sxs-lookup"><span data-stu-id="78b76-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="78b76-132">當資料載入至每個資料表時，SQL 資料倉儲會如何具有 tooknow toodivide 跨這些 60 發佈資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="78b76-133">hello 發佈方法定義在 hello 資料表層級和目前有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="78b76-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="78b76-134">**循環配置資源** 會平均但隨機散發資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="78b76-135">**雜湊散發** 會根據單一資料行的雜湊值散發資料</span><span class="sxs-lookup"><span data-stu-id="78b76-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="78b76-136">根據預設，當您未定義的資料散發方式，您的資料表將發佈使用 hello**循環配置資源**發佈方法。</span><span class="sxs-lookup"><span data-stu-id="78b76-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="78b76-137">不過，因為您變得較複雜實作中，您會想使用 tooconsider**雜湊散發**資料表 toominimize 資料移動，這會依次最佳化查詢效能。</span><span class="sxs-lookup"><span data-stu-id="78b76-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="78b76-138">循環配置資源資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-138">Round Robin Tables</span></span>
<span data-ttu-id="78b76-139">使用 hello 散發資料的循環配置資源方法，是非常如何聽起來。</span><span class="sxs-lookup"><span data-stu-id="78b76-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="78b76-140">載入資料時，每個資料列會直接傳送 toohello 下一個發佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="78b76-141">散發 hello 資料的這個方法會一律隨機將 hello 資料非常平均分散到所有 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="78b76-142">也就是說，沒有任何排序完成期間 hello 循環配置資源的程序而放置您的資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="78b76-143">基於這個理由，循環配置資源散發有時稱為隨機雜湊。</span><span class="sxs-lookup"><span data-stu-id="78b76-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="78b76-144">循環配置資源的分散式資料表沒有任何需要 toounderstand hello 資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="78b76-145">基於這個理由，循環配置資源資料表通常具有良好的載入目標。</span><span class="sxs-lookup"><span data-stu-id="78b76-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="78b76-146">根據預設，如果選擇沒有散發方法，則 hello 循環配置資源發佈方法將用於。</span><span class="sxs-lookup"><span data-stu-id="78b76-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="78b76-147">不過，雖然循環配置資源表格是簡單的 toouse，因為資料會隨機分佈在 hello 系統表示 hello 系統無法保證的散發每個資料列是上。</span><span class="sxs-lookup"><span data-stu-id="78b76-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="78b76-148">在結果中，有時候 hello 系統需求 tooinvoke 資料移動作業 toobetter 組織資料之前它可以解析查詢。</span><span class="sxs-lookup"><span data-stu-id="78b76-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="78b76-149">此額外步驟會使您的查詢變慢。</span><span class="sxs-lookup"><span data-stu-id="78b76-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="78b76-150">請考慮使用循環配置資源發佈 hello 下列案例中針對資料表：</span><span class="sxs-lookup"><span data-stu-id="78b76-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="78b76-151">以簡單的起點開始使用時</span><span class="sxs-lookup"><span data-stu-id="78b76-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="78b76-152">如果沒有明顯的聯結索引鍵</span><span class="sxs-lookup"><span data-stu-id="78b76-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="78b76-153">如果不是散發 hello 資料表的雜湊的候選資料行</span><span class="sxs-lookup"><span data-stu-id="78b76-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="78b76-154">如果 hello 資料表不會共用共同的聯結索引鍵與其他資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="78b76-155">如果比其他 hello 查詢中聯結的那麼顯著 hello 聯結</span><span class="sxs-lookup"><span data-stu-id="78b76-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="78b76-156">當 hello 資料表是暫時的臨時資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="78b76-157">兩個範例都會建立循環配置資源資料表︰</span><span class="sxs-lookup"><span data-stu-id="78b76-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="78b76-158">循環配置資源時所明確 DDL 中的 hello 預設資料表類型是最佳做法，讓資料表配置的 hello 意圖清除 tooothers。</span><span class="sxs-lookup"><span data-stu-id="78b76-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="78b76-159">雜湊散發資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-159">Hash Distributed Tables</span></span>
<span data-ttu-id="78b76-160">使用**雜湊散發**演算法 toodistribute 資料表可以提升效能許多案例中，藉由在查詢時減少資料移動。</span><span class="sxs-lookup"><span data-stu-id="78b76-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="78b76-161">分散式的資料表是屬 hello 資料表的雜湊散發資料庫時您所選取的單一資料行上使用雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="78b76-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="78b76-162">hello 散發資料行是決定 hello 資料分成分散式資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="78b76-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="78b76-163">hello 雜湊函式會使用 hello 散發資料行 tooassign 列 toodistributions。</span><span class="sxs-lookup"><span data-stu-id="78b76-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="78b76-164">hello 雜湊演算法，並產生分佈是具決定性。</span><span class="sxs-lookup"><span data-stu-id="78b76-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="78b76-165">也就是 hello hello 相同的資料類型會一律使用相同的值有 toohello 相同的散發。</span><span class="sxs-lookup"><span data-stu-id="78b76-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="78b76-166">這個範例會建立依照識別碼散發的資料表︰</span><span class="sxs-lookup"><span data-stu-id="78b76-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="78b76-167">選擇散發資料行</span><span class="sxs-lookup"><span data-stu-id="78b76-167">Select distribution column</span></span>
<span data-ttu-id="78b76-168">當您選擇太**雜湊散發**資料表時，您將需要 tooselect 單一散發資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="78b76-169">當選取散發資料行，有三個主要的因素 tooconsider。</span><span class="sxs-lookup"><span data-stu-id="78b76-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="78b76-170">選取具有下列特性的單一資料行︰</span><span class="sxs-lookup"><span data-stu-id="78b76-170">Select a single column which will:</span></span>

1. <span data-ttu-id="78b76-171">不會更新</span><span class="sxs-lookup"><span data-stu-id="78b76-171">Not be updated</span></span>
2. <span data-ttu-id="78b76-172">平均散發資料，以避免資料扭曲</span><span class="sxs-lookup"><span data-stu-id="78b76-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="78b76-173">最小化資料移動</span><span class="sxs-lookup"><span data-stu-id="78b76-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="78b76-174">選取不會更新的散發資料行</span><span class="sxs-lookup"><span data-stu-id="78b76-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="78b76-175">散發資料行不可更新，因此，選取具靜態值的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="78b76-176">如果資料行，將需要更新 toobe，通常是不好發佈候選。</span><span class="sxs-lookup"><span data-stu-id="78b76-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="78b76-177">如果沒有，您必須更新散發資料行的情況下，作法是先刪除 hello 資料列，然後插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="78b76-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="78b76-178">選取將平均散發資料的散發資料行</span><span class="sxs-lookup"><span data-stu-id="78b76-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="78b76-179">分散式的系統執行只盡其最慢的發佈時，會很重要的 toodivide hello 工作平均跨順序 tooachieve 平衡執行中的 hello 分佈 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="78b76-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="78b76-180">hello hello 工作就會劃分分散式系統的方式根據每個散發 hello 資料所在。</span><span class="sxs-lookup"><span data-stu-id="78b76-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="78b76-181">這使得散發 hello 資料，讓每個分佈有相等的工作，並將採用 hello 相同時間 toocomplete hello 工作及其部分的非常重要的 tooselect hello 右散發資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="78b76-182">當工作也分成 hello 系統時，hello 資料被平衡 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="78b76-183">當資料不平衡時，我們將此稱為 **資料扭曲**。</span><span class="sxs-lookup"><span data-stu-id="78b76-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="78b76-184">toodivide 資料平均，避免資料扭曲，請選取您的散發資料行時，請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="78b76-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="78b76-185">選取包含大量相異值的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="78b76-186">避免將資料散發於含有少許相異值的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="78b76-187">避免將資料散發於 null 頻繁出現的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="78b76-188">避免在日期資料行上散發資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="78b76-189">由於每個值是 60 分佈的雜湊的 too1，tooachieve 平均散發您會想 tooselect 的高唯一且包含超過 60 的唯一值的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="78b76-190">tooillustrate，試想一個情況，資料行僅具有 40 的唯一值。</span><span class="sxs-lookup"><span data-stu-id="78b76-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="78b76-191">如果此資料行已選定為 hello 散發索引鍵，hello 資料為該資料表會登陸 40 分佈最多，僅保留任何資料，然後沒有處理 toodo 20 分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="78b76-192">相反地，hello 其他 40 分佈會有多個工作 toodo 如果 hello 資料的平均散佈超過 60 份的分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="78b76-193">這個案例就是資料扭曲的範例。</span><span class="sxs-lookup"><span data-stu-id="78b76-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="78b76-194">MPP 系統中每個查詢步驟會等到所有分佈 toocomplete 之 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="78b76-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="78b76-195">如果一個散發是執行作業超過 hello 其他項目，則 hello 資源的 hello 其他分佈基本上會浪費只等待 hello 忙碌中發佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="78b76-196">當所有散發的工作分配不均時，我們將此稱為 **處理誤差**。</span><span class="sxs-lookup"><span data-stu-id="78b76-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="78b76-197">處理誤差會導致查詢 toorun 低於如果 hello 工作負載平均分散到 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="78b76-198">資料扭曲，都會導致 tooprocessing 誤差。</span><span class="sxs-lookup"><span data-stu-id="78b76-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="78b76-199">避免依 hello null 值將所有登陸在 hello 相同分配高度可為 null 的資料行上發佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="78b76-200">散發之日期資料行也可能造成處理誤差的特定日期的所有資料將都登陸在 hello 相同，因為通訊群組。</span><span class="sxs-lookup"><span data-stu-id="78b76-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="78b76-201">如果數個使用者會在查詢執行所有篩選 hello 相同的日期，則只有 1 個的 hello 60 分佈會進行所有 hello 工作的特定的日期都只會在一個發佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="78b76-202">在此案例中，hello 查詢可能都會執行 60 時間低於如果 hello 資料已平均分散到所有 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="78b76-203">當沒有候選資料行存在，請考慮使用循環配置資源做為 hello 發佈方法。</span><span class="sxs-lookup"><span data-stu-id="78b76-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="78b76-204">選取會將資料移動降至最低的散發資料行</span><span class="sxs-lookup"><span data-stu-id="78b76-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="78b76-205">選取 hello 右散發資料行降到最低的資料移動是其中一種 hello 最佳化您的 SQL 資料倉儲的效能最重要的策略。</span><span class="sxs-lookup"><span data-stu-id="78b76-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="78b76-206">資料移動最常發生於聯結資料表或執行彙總時。</span><span class="sxs-lookup"><span data-stu-id="78b76-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="78b76-207">用於 `JOIN`、`GROUP BY`、`DISTINCT`、`OVER`、`HAVING` 子句的資料行全都是**理想**的雜湊散發候選項目。</span><span class="sxs-lookup"><span data-stu-id="78b76-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="78b76-208">在 hello 相反地，資料行中 hello`WHERE`子句執行**不**讓良好的雜湊資料行的候選項目的限制哪一個分佈參與 hello 查詢，導致處理因為誤差。</span><span class="sxs-lookup"><span data-stu-id="78b76-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="78b76-209">這可能會吸引人 toodistribute，但通常可能會造成這項處理誤差的資料行的理想範例為日期資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="78b76-210">一般而言，如果您有兩個大型事實資料表經常涉及的聯結中，您會取得 hello 最高效能散發 hello 聯結資料行其中兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="78b76-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="78b76-211">如果您有絕不會是聯結的 tooanother 大型事實資料表的資料表，然後尋找經常處於 hello toocolumns`GROUP BY`子句。</span><span class="sxs-lookup"><span data-stu-id="78b76-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="78b76-212">有幾個索引鍵的條件加入期間必須符合的 tooavoid 資料移動：</span><span class="sxs-lookup"><span data-stu-id="78b76-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="78b76-213">hello hello 聯結中涉及的資料表必須是分佈在雜湊**一個**hello hello 聯結中參與的資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="78b76-214">hello hello 聯結資料行資料類型必須符合這兩個資料表之間。</span><span class="sxs-lookup"><span data-stu-id="78b76-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="78b76-215">必須以等號運算子加入 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="78b76-216">hello 聯結類型可能無法`CROSS JOIN`。</span><span class="sxs-lookup"><span data-stu-id="78b76-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="78b76-217">資料扭曲疑難排解</span><span class="sxs-lookup"><span data-stu-id="78b76-217">Troubleshooting data skew</span></span>
<span data-ttu-id="78b76-218">當資料表資料發佈使用 hello 雜湊散發方法有某些機率準 toohave 比其他不當比例的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="78b76-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="78b76-219">因為 hello 最終結果的分散式查詢必須等候 hello 最長執行發佈 toofinish 誤差過多資料可能會影響查詢效能。</span><span class="sxs-lookup"><span data-stu-id="78b76-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="78b76-220">視 hello 程度 hello 資料扭曲您可能需要 tooaddress 它。</span><span class="sxs-lookup"><span data-stu-id="78b76-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="78b76-221">識別扭曲</span><span class="sxs-lookup"><span data-stu-id="78b76-221">Identifying skew</span></span>
<span data-ttu-id="78b76-222">簡單的方式 tooidentify 資料表為準是 toouse `DBCC PDW_SHOWSPACEUSED`。</span><span class="sxs-lookup"><span data-stu-id="78b76-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="78b76-223">這是非常快速且簡單的方式 toosee hello 的資料表會儲存在每個資料庫的 hello 60 分佈的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="78b76-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="78b76-224">請記住，為了 hello 最平衡效能，hello 分散式資料表中的資料列應該分成平均 hello 的所有分佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="78b76-225">不過，如果您查詢 hello Azure SQL 資料倉儲動態管理檢視 (DMV)，您可以執行更詳細的分析。</span><span class="sxs-lookup"><span data-stu-id="78b76-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="78b76-226">toostart，建立 hello 檢視[dbo.vTableSizes] [ dbo.vTableSizes]使用檢視 hello SQL 從[資料表概觀][ Overview]發行項。</span><span class="sxs-lookup"><span data-stu-id="78b76-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="78b76-227">一旦建立 hello 檢視時，執行此查詢 tooidentify，哪些資料表有個以上的資料 10%誤差。</span><span class="sxs-lookup"><span data-stu-id="78b76-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="78b76-228">解決資料扭曲</span><span class="sxs-lookup"><span data-stu-id="78b76-228">Resolving data skew</span></span>
<span data-ttu-id="78b76-229">不是所有誤差是足夠 toowarrant 修正程式。</span><span class="sxs-lookup"><span data-stu-id="78b76-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="78b76-230">在某些情況下，某些查詢中資料表的 hello 效能可能會超過資料扭曲 hello 的傷害。</span><span class="sxs-lookup"><span data-stu-id="78b76-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="78b76-231">toodecide，如果您也應該解決資料扭曲在資料表中，您應該了解有關 hello 資料磁碟區和查詢最大的在您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="78b76-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="78b76-232">其中一種方式在 hello 誤差影響 toolook 是 hello toouse hello 步驟[查詢監視][ Query Monitoring]文章 toomonitor hello 影響的查詢效能傾斜和特別 hello 影響 toohow 長時間查詢需要 toocomplete hello 個別發佈。</span><span class="sxs-lookup"><span data-stu-id="78b76-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="78b76-233">將資料散發是要尋找 hello 資料誤差降至最低，並盡量減少資料移動之間的正確平衡。</span><span class="sxs-lookup"><span data-stu-id="78b76-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="78b76-234">這些可以團體的目標，有時候您會想 tookeep 資料偏斜順序 tooreduce 資料移動。</span><span class="sxs-lookup"><span data-stu-id="78b76-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="78b76-235">比方說，當 hello 散發資料行經常 hello 聯結和彙總中的共用的資料，您將會最小化資料移動。</span><span class="sxs-lookup"><span data-stu-id="78b76-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="78b76-236">hello 擁有 hello 最少的資料移動可能會遠大於 hello 影響的資料扭曲。</span><span class="sxs-lookup"><span data-stu-id="78b76-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="78b76-237">hello 的典型方式 tooresolve 資料誤差是 toore-建立 hello 資料表具有不同的散發資料行。</span><span class="sxs-lookup"><span data-stu-id="78b76-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="78b76-238">因為沒有任何方法 toochange hello 散發資料行上的現有資料表，資料表的 hello 方式 toochange hello 發佈它 toorecreate 它有 [CTAS] []。</span><span class="sxs-lookup"><span data-stu-id="78b76-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="78b76-239">以下是解決資料扭曲的兩個範例：</span><span class="sxs-lookup"><span data-stu-id="78b76-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="78b76-240">範例 1： 重新建立 hello 與新的散發資料行的資料表</span><span class="sxs-lookup"><span data-stu-id="78b76-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="78b76-241">這個範例會使用 [CTAS] [] toore-建立具有不同的雜湊散發資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="78b76-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="78b76-242">範例 2： 重新建立 hello 資料表使用循環配置資源發佈</span><span class="sxs-lookup"><span data-stu-id="78b76-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="78b76-243">這個範例會使用 [CTAS] [] toore-建立具有循環配置資源，而不是雜湊散發的資料表。</span><span class="sxs-lookup"><span data-stu-id="78b76-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="78b76-244">這項變更將會產生即使資料分佈 hello 成本增加的資料移動。</span><span class="sxs-lookup"><span data-stu-id="78b76-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="78b76-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78b76-245">Next steps</span></span>
<span data-ttu-id="78b76-246">toolearn 有關資料表設計的詳細資訊，請參閱 「 hello[散發][Distribute]，[索引][Index]，[分割][Partition]，[資料型別][Data Types]，[統計資料][ Statistics]和[暫存資料表] [ Temporary]文件。</span><span class="sxs-lookup"><span data-stu-id="78b76-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="78b76-247">如需最佳做法的概觀，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="78b76-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
