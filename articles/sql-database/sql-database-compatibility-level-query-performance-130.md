---
title: "資料庫相容性層級 130 - Azure SQL Database | Microsoft Docs"
description: "在本文中，我們會探索以相容性層級 130 執行 Azure SQL Databse 的優點，並善用新查詢最佳化工具和查詢處理器功能的優點。 我們也會解決對現有 SQL 應用程式的查詢效能可能造成的副作用。"
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="ff380-104">改善 Azure SQL Database 中相容性層級 130 的查詢效能</span><span class="sxs-lookup"><span data-stu-id="ff380-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="ff380-105">Azure SQL Database 會在許多不同的相容性層級上以透明方式執行數十萬個資料庫，對其所有客戶保留並保證對應 Microsoft SQL Server 版本的回溯相容性！</span><span class="sxs-lookup"><span data-stu-id="ff380-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="ff380-106">在本文中，我們會探索以相容性層級 130 執行 Azure SQL Databse 的優點，並善用新查詢最佳化工具和查詢處理器功能的優點。</span><span class="sxs-lookup"><span data-stu-id="ff380-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="ff380-107">我們也會解決對現有 SQL 應用程式的查詢效能可能造成的副作用。</span><span class="sxs-lookup"><span data-stu-id="ff380-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="ff380-108">當作歷程記錄的提醒，預設相容性層級的 SQL 版本比對如下︰</span><span class="sxs-lookup"><span data-stu-id="ff380-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="ff380-109">100：在 SQL Server 2008 和 Azure SQL Database V11 中。</span><span class="sxs-lookup"><span data-stu-id="ff380-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="ff380-110">110：在 SQL Server 2012 和 Azure SQL Database V11 中。</span><span class="sxs-lookup"><span data-stu-id="ff380-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="ff380-111">120：在 SQL Server 2014 和 Azure SQL Database V12 中。</span><span class="sxs-lookup"><span data-stu-id="ff380-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="ff380-112">130：在 SQL Server 2016 和 Azure SQL Database V12 中。</span><span class="sxs-lookup"><span data-stu-id="ff380-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff380-113">從 **2016 年 6 月中旬**開始，在 Azure SQL Database 中，**新建**資料庫的預設相容性層級會是 130 (而不是 120)。</span><span class="sxs-lookup"><span data-stu-id="ff380-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="ff380-114">在 2016 年 6 月中旬前建立的資料庫將「不」  受影響，而且會維持其目前的相容性層級 (100、110 或 120)。</span><span class="sxs-lookup"><span data-stu-id="ff380-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="ff380-115">從 Azure SQL Database V11 版移轉到 V12 版的資料庫，其相容性層級會是 100 或 110。</span><span class="sxs-lookup"><span data-stu-id="ff380-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="ff380-116">關於相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="ff380-116">About compatibility level 130</span></span>
<span data-ttu-id="ff380-117">首先，如果想要知道資料庫目前的相容性層級，請執行下列 Transact-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff380-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="ff380-118">在 **新建** 資料庫變更為層級 130 之前，讓我們透過一些非常基本的查詢範例來檢閱這項變更的相關資訊，並了解相關人員如何從中受益。</span><span class="sxs-lookup"><span data-stu-id="ff380-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="ff380-119">關聯式資料庫中的查詢處理可能非常複雜，以致大量的電算機科學和數學人員得以了解固有的設計選擇和行為。</span><span class="sxs-lookup"><span data-stu-id="ff380-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="ff380-120">本文件的內容已刻意簡化，以確保具有一些最基本技術背景的人員可以了解相容性層級變更的影響，並判斷其對於應用程式有何好處。</span><span class="sxs-lookup"><span data-stu-id="ff380-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="ff380-121">我們快速看一下相容性層級 130 對資料表有何好處。</span><span class="sxs-lookup"><span data-stu-id="ff380-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="ff380-122">您可以在 [ALTER DATABASE 相容性層級 (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)找到更多詳細資料，但簡短摘要如下︰</span><span class="sxs-lookup"><span data-stu-id="ff380-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="ff380-123">Insert-select 陳述式的 Insert 作業可以是多執行緒作業或可以有平行計劃，而這項作業之前是單一執行緒作業。</span><span class="sxs-lookup"><span data-stu-id="ff380-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="ff380-124">記憶體最佳化資料表和資料表變數查詢現在可以有平行計劃，而這項作業之前也是單一執行緒作業。</span><span class="sxs-lookup"><span data-stu-id="ff380-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="ff380-125">記憶體最佳化資料表的統計資料現在可以取樣並會自動更新。</span><span class="sxs-lookup"><span data-stu-id="ff380-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="ff380-126">如需詳細資訊，請參閱 [Database Engine 新功能：In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) 。</span><span class="sxs-lookup"><span data-stu-id="ff380-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="ff380-127">資料行存放區索引的批次模式和資料列模式變更</span><span class="sxs-lookup"><span data-stu-id="ff380-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="ff380-128">具有資料行存放區索引的資料表現在會以批次模式排序。</span><span class="sxs-lookup"><span data-stu-id="ff380-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="ff380-129">時間範圍彙總現在以批次模式運作，例如 TSQL LAG/LEAD 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff380-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="ff380-130">具有多個不同子句的資料行存放區資料表會以批次模式進行查詢。</span><span class="sxs-lookup"><span data-stu-id="ff380-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="ff380-131">在 DOP = 1 之下執行或具有序列計劃的查詢也會以批次模式執行。</span><span class="sxs-lookup"><span data-stu-id="ff380-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="ff380-132">最後，基數估計改進實際上隨著相容性層級 120 出現，但如何您是在較低的相容性層級 (也就是 100 或 110) 執行，移到相容性層級 130 也會帶來這些改進，而這些改進也有益於您應用程式的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="ff380-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="ff380-133">演練相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="ff380-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="ff380-134">首先，我們要建立一些資料表、索引和隨機資料，以演練某些新功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="ff380-135">TSQL 指令碼範例可以在 SQL Server 2016 底下或在 Azure SQL Database 底下執行。</span><span class="sxs-lookup"><span data-stu-id="ff380-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="ff380-136">不過，在建立 Azure SQL Database 時，務必至少選擇 P2 資料庫，因為您至少需要幾個核心才能允許多執行緒處理，並因而受益於這些功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="ff380-137">我們現在來看一下相容性層級 130 隨附的一些查詢處理功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="ff380-138">平行 INSERT</span><span class="sxs-lookup"><span data-stu-id="ff380-138">Parallel INSERT</span></span>
<span data-ttu-id="ff380-139">執行下面的 TSQL 陳述式時會在相容性層級 120 和 130 之下執行 INSERT 作業，其分別在單一執行緒模型 (120) 和多執行緒模型 (130) 中執行 INSERT 作業。</span><span class="sxs-lookup"><span data-stu-id="ff380-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-140">藉由要求實際查詢計劃、查看其圖形表示法或其 XML 內容，您即可判斷正在執行哪個基數估計函式。</span><span class="sxs-lookup"><span data-stu-id="ff380-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="ff380-141">查看圖 1 的並排計劃，我們可以清楚地看到資料行存放區 INSERT 作業從 120 中的序列執行變成 130 中的平行執行。</span><span class="sxs-lookup"><span data-stu-id="ff380-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="ff380-142">此外，請注意 130 計劃中的迭代器圖示變更顯示兩個平行箭號，這說明了迭代器現在的確是平行執行的這項事實。</span><span class="sxs-lookup"><span data-stu-id="ff380-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="ff380-143">如果您有大量 INSERT 作業要完成，平行執行 (已連結至您可對資料庫支配的核心數目) 的效果會更佳；視您的情況而言，速度最高可快 100 倍！</span><span class="sxs-lookup"><span data-stu-id="ff380-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="ff380-144">*圖 1︰INSERT 作業從序列執行變成在相容性層級 130 的平行執行。*</span><span class="sxs-lookup"><span data-stu-id="ff380-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![圖 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="ff380-146">序列批次模式</span><span class="sxs-lookup"><span data-stu-id="ff380-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="ff380-147">同樣地，在處理資料列時移到相容性層級 130 即可進行批次模式處理。</span><span class="sxs-lookup"><span data-stu-id="ff380-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="ff380-148">第一，批次模式作業僅適用於您已備妥資料行存放區索引時。</span><span class="sxs-lookup"><span data-stu-id="ff380-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="ff380-149">第二，一個批次通常代表 ~900 個資料列，並使用針對多核心 CPU、較高記憶體輸送量最佳化的程式碼邏輯，而且盡可能直接運用資料行存放區的壓縮資料。</span><span class="sxs-lookup"><span data-stu-id="ff380-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="ff380-150">在這些條件之下，SQL Server 2016 一次可以處理 ~900 個資料列，而不是一次處理 1 個資料列，因此作業的整體額外成本現在是由整個批次分擔，進而降低各資料列的整體成本。</span><span class="sxs-lookup"><span data-stu-id="ff380-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="ff380-151">與資料行存放區壓縮結合的這個共用作業數量基本上可減少 SELECT 批次模式作業中的延遲。</span><span class="sxs-lookup"><span data-stu-id="ff380-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="ff380-152">您可以在 [資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)找到有關資料行存放區和批次模式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ff380-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-153">如下所見，觀察圖 2 的並排查詢計劃，我們可以看到處理模式已隨個相容性層級變更，因此，同時在兩個相容性層級執行查詢時，我們可以看到大部分的處理時間花費在資料列模式 (86%) (相較於已處理 2 個批次的批次模式 (14%))。</span><span class="sxs-lookup"><span data-stu-id="ff380-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="ff380-154">增加資料集，優點也會增加。</span><span class="sxs-lookup"><span data-stu-id="ff380-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="ff380-155">*圖 2︰SELECT 作業從序列變成在相容性層級 130 的批次模式。*</span><span class="sxs-lookup"><span data-stu-id="ff380-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![圖 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="ff380-157">排序執行的批次模式</span><span class="sxs-lookup"><span data-stu-id="ff380-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="ff380-158">類似上述情況，但套用至排序作業後，從資料列模式 (相容性層級 120) 轉換為批次模式 (相容性層級 130) 可提升 SORT 作業的效能，其理由相同。</span><span class="sxs-lookup"><span data-stu-id="ff380-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-159">如圖 3 並排顯示，我們可以看到資料列模式的排序作業代表 81%的成本，而批次模式只代表 19% 的成本 (排序本身分別佔 81% 和 56%)。</span><span class="sxs-lookup"><span data-stu-id="ff380-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="ff380-160">*圖 3︰SORT 作業從資料列模式變成在相容性層級 130 的批次模式。*</span><span class="sxs-lookup"><span data-stu-id="ff380-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![圖 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="ff380-162">很明顯地，這些範例只包含成千上萬個資料列，而在查看近來大部分 SQL Server 中可用的資料時，這算不了什麼。</span><span class="sxs-lookup"><span data-stu-id="ff380-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="ff380-163">只要針對數百萬個資料列進行預估，即可在執行的數分鐘內轉譯，而免除每天擱置您的工作負載本質。</span><span class="sxs-lookup"><span data-stu-id="ff380-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="ff380-164">基數估計 (CE) 改進</span><span class="sxs-lookup"><span data-stu-id="ff380-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="ff380-165">任何執行相容性層級 120 或更高層級的資料庫，將使用隨著 SQL Server 2014 引進的新基數估計功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="ff380-166">基本上，基數估計用於根據估計的成本來判斷 SQL Server 將如何執行查詢的邏輯。</span><span class="sxs-lookup"><span data-stu-id="ff380-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="ff380-167">這項估計是使用來自與該查詢所牽涉物件相關聯的統計資料的輸入來計算。</span><span class="sxs-lookup"><span data-stu-id="ff380-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="ff380-168">實際上，概括來說，基數估計函式是資料列計數估計值，以及下列各項的相關資訊：值分佈、相異值計數，以及查詢中參考的資料表和物件內含的重複計數。</span><span class="sxs-lookup"><span data-stu-id="ff380-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="ff380-169">如果這些估計值錯誤，可能會因為授與的記憶體不足 (也就是 TempDB 溢出)、選取序列計劃執行 (而非平行計劃執行) 等等，而導致不必要的磁碟 I/O。</span><span class="sxs-lookup"><span data-stu-id="ff380-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="ff380-170">總而言之，不正確的估計值可能會導致查詢執行的整體效能降低。</span><span class="sxs-lookup"><span data-stu-id="ff380-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="ff380-171">另一方面，更完善的估計值、更精確的估計值會導致更好的查詢執行！</span><span class="sxs-lookup"><span data-stu-id="ff380-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="ff380-172">如之前所述，查詢最佳化和評估值是複雜的事物，但如果您想要深入了解查詢計劃和基數估算器，您可以參考 [使用 SQL Server 2014 基數估計器來最佳化查詢計劃](https://msdn.microsoft.com/library/dn673537.aspx) 文件，以獲得深入說明。</span><span class="sxs-lookup"><span data-stu-id="ff380-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="ff380-173">您目前使用哪個基數估計？</span><span class="sxs-lookup"><span data-stu-id="ff380-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="ff380-174">若要判斷您查詢是在哪個基數估計之下執行，只要使用以下的查詢範例即可。</span><span class="sxs-lookup"><span data-stu-id="ff380-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="ff380-175">請注意，第一個範例會在相容性層級 110 之下執行，暗示使用舊的基數估計函式。</span><span class="sxs-lookup"><span data-stu-id="ff380-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-176">執行完成後，按一下 XML 連結，並查看第一個迭代器的屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ff380-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="ff380-177">請注意，名為 CardinalityEstimationModelVersion 的屬性名稱目前設定為 70。</span><span class="sxs-lookup"><span data-stu-id="ff380-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="ff380-178">這並不表示資料庫相容性層級設定為 SQL Server 7.0 版 (如上面的 TSQL 陳述式所示，其設定於 110)，但值 70 只代表自 SQL Server 7.0 起可用的舊版基數估計功能，而直到 SQL Server 2014 (隨附相容性層級 120) 以後才有主要版本。</span><span class="sxs-lookup"><span data-stu-id="ff380-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="ff380-179">*圖 4：使用相容性層級 110 或更低層級時，CardinalityEstimationModelVersion 會設定為 70。*</span><span class="sxs-lookup"><span data-stu-id="ff380-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![圖 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="ff380-181">或者，您可以將相容性層級變更為 130，並使用設定為 NO 的 LEGACY_CARDINALITY_ESTIMATION 搭配 [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx) 來停止使用新的基數估計函式。</span><span class="sxs-lookup"><span data-stu-id="ff380-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="ff380-182">從基數估計函式的觀點來看，這與使用 110 完全相同，同時使用最新的查詢處理相容性層級。</span><span class="sxs-lookup"><span data-stu-id="ff380-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="ff380-183">這麼做，您就可以受益於最新相容性層級隨附的新查詢處理功能 (也就是批次模式，但必要時仍會依賴舊的基數估計功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-184">只要移到相容性層級 120 或 130，即可啟用新的基數估計功能。</span><span class="sxs-lookup"><span data-stu-id="ff380-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="ff380-185">在這種情況下，預設 CardinalityEstimationModelVersion 便會跟著設定為 120 或 130，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ff380-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-186">*圖 5：使用相容性層級 130 時，CardinalityEstimationModelVersion 會設定為 130。*</span><span class="sxs-lookup"><span data-stu-id="ff380-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![圖 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="ff380-188">見證基數估計差異</span><span class="sxs-lookup"><span data-stu-id="ff380-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="ff380-189">現在，讓我們執行稍微複雜的查詢 (牽涉到包含一個 WHERE 子句及一些述詞的 INNER JOIN)，而且先查看舊基數估計函式的資料列計數估計值。</span><span class="sxs-lookup"><span data-stu-id="ff380-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-190">有效地執行這項查詢會傳回 200,704 個資料列，而透過舊基數估計功能的資料列預估值宣告 194,284 個資料列。</span><span class="sxs-lookup"><span data-stu-id="ff380-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="ff380-191">很明顯地，如之前所述，這些資料列計數結果還是會視您執行先前範例的頻率而定，在每次執行時一再填入範例資料表。</span><span class="sxs-lookup"><span data-stu-id="ff380-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="ff380-192">顯然，除了資料表圖形、資料內容，以及此資料實際上彼此相互關聯的方式，查詢中的述詞也會影響的實際估計。</span><span class="sxs-lookup"><span data-stu-id="ff380-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="ff380-193">*圖 6︰資料列計數估計值為 194,284 或與預期的 200,704 個資料列相差 6,000 個資料列。*</span><span class="sxs-lookup"><span data-stu-id="ff380-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![圖 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="ff380-195">同樣地，我們現在使用新的基數估計功能執行相同的查詢。</span><span class="sxs-lookup"><span data-stu-id="ff380-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="ff380-196">看看下面，我們現在看到資料列估計值為 202,877，或更加接近且高於舊的基數估計。</span><span class="sxs-lookup"><span data-stu-id="ff380-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="ff380-197">*圖 7︰資料列計數估計現在是 202,877，而不是 194,284。*</span><span class="sxs-lookup"><span data-stu-id="ff380-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![圖 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="ff380-199">事實上，結果集為 200,704 個資料列 (但全都取決於您執行先前範例查詢的頻率，而更重要的是，因為 TSQL 使用 RAND() 陳述式，所以每次執行傳回的實際值會有所不同)。</span><span class="sxs-lookup"><span data-stu-id="ff380-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="ff380-200">因此，在此特殊範例中，新的基數估計在估計資料列數時的效果更好，因為 202,877 比 194,284 更接近 200,704！</span><span class="sxs-lookup"><span data-stu-id="ff380-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="ff380-201">最後，如果您將 WHERE 子句變更為等號 (舉例來說，而非 “>”)，這可能會使新舊基數函式之間的估計值更加不同 (視您可以取得多少相符項目而定)。</span><span class="sxs-lookup"><span data-stu-id="ff380-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="ff380-202">很明顯地，在此情況下，與實際計數相差 ~6000 個資料列，在某些情況下並不代表大量資料。</span><span class="sxs-lookup"><span data-stu-id="ff380-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="ff380-203">現在，將此變換成跨數個資料表的數百萬個資料列和更複雜的查詢，而有時候估計值可能會相差數百萬個資料列，因此，挑選錯誤執行計畫，或要求授與的記憶體不足 (導致 TempDB 溢出和更多的 I/O) 的風險會高出許多。</span><span class="sxs-lookup"><span data-stu-id="ff380-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="ff380-204">如果您有機會，請使用最典型的查詢和資料集來練習這項比較，並親自查看一些舊的和新的估計值受到多少影響，然而有些估計值可能只是變得與事實相差更遠，其他一些估計值可能只是更接近結果集中實際傳回的實際資料列計數。</span><span class="sxs-lookup"><span data-stu-id="ff380-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="ff380-205">這全都取決於您的查詢圖形、Azure SQL Database 特性、資料集的本質和大小，以及其相關的可用統計資料。</span><span class="sxs-lookup"><span data-stu-id="ff380-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="ff380-206">如果您剛建立 Azure SQL Database 執行個體，查詢最佳化工具必須從頭建立其知識，而不是重複使用先前查詢執行所構成的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ff380-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="ff380-207">因此，估計值非常情境式，而且幾乎是每個伺服器和應用程式情況所特有。</span><span class="sxs-lookup"><span data-stu-id="ff380-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="ff380-208">這是要牢記在心的重要層面！</span><span class="sxs-lookup"><span data-stu-id="ff380-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="ff380-209">需要考量的一些注意事項</span><span class="sxs-lookup"><span data-stu-id="ff380-209">Some considerations to take into account</span></span>
<span data-ttu-id="ff380-210">雖然大部分的工作負載受益於相容性層級 130，但是在您對生產環境採用此相容性層級之前，基本上有 3 個選項︰</span><span class="sxs-lookup"><span data-stu-id="ff380-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="ff380-211">請移到相容性層級 130，並查看如何執行動作。</span><span class="sxs-lookup"><span data-stu-id="ff380-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="ff380-212">如果您發現一些效能衰退，只要將相容性層級設回其原始層級，或保留 130，而且只讓基數估計回復到舊版模式 (如前文所述，這可獨力處理此問題)。</span><span class="sxs-lookup"><span data-stu-id="ff380-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="ff380-213">您可在類似的生產負載之下徹底測試現有的應用程式、進行微調，以及在正式推出前驗證效能。</span><span class="sxs-lookup"><span data-stu-id="ff380-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="ff380-214">若有任何問題，同上所述，您可以隨時回到原始的相容性層級，或只讓基數估計回復到舊版模式。</span><span class="sxs-lookup"><span data-stu-id="ff380-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="ff380-215">做為處理這些問題的最後一個選項，最新的方法是使用查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="ff380-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="ff380-216">這是現今的建議選項！</span><span class="sxs-lookup"><span data-stu-id="ff380-216">That’s today’s recommended option!</span></span> <span data-ttu-id="ff380-217">為了協助分析在相容性層級 120 或更低層級與相容性層級 130 之下的查詢，我們完全鼓勵您使用查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="ff380-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="ff380-218">查詢存放區適用於最新版的 Azure SQL Database V12，而且其設計用來協助您進行查詢效能疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ff380-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="ff380-219">將查詢存放區視為您的資料庫的飛行資料記錄器，其可收集和呈現關於所有查詢的詳細歷程記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="ff380-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="ff380-220">這可減少診斷和解決問題所需的時間，進而大幅簡化效能鑑識。</span><span class="sxs-lookup"><span data-stu-id="ff380-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="ff380-221">如需詳細資訊，請參閱 [查詢存放區︰您的資料庫的飛行資料記錄器](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。</span><span class="sxs-lookup"><span data-stu-id="ff380-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="ff380-222">概括而言，如果您已經有一組在相容性層級 120 或更低層級執行的資料庫，並規劃將其中一些資料庫移到 130，或因為您的工作負載自動佈建一些很快就會預設為 130 的新資料庫，請考慮下列各項︰</span><span class="sxs-lookup"><span data-stu-id="ff380-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="ff380-223">在變更為生產環境中的新相容性層級之前，啟用查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="ff380-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="ff380-224">如需詳細資訊，您可以參考 [變更資料庫相容性模式和使用查詢存放區](https://msdn.microsoft.com/library/bb895281.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ff380-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="ff380-225">接下來，使用具代表性的資料和類似生產環境的查詢來測試所有重要工作負載，並且比較所經歷的效能與存放區所報告的效能。</span><span class="sxs-lookup"><span data-stu-id="ff380-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="ff380-226">如果您遇到一些效能衰退，您可以找出衰退的查詢存放區查詢，並使用查詢存放區提供的計畫強制選項 (也稱為計畫關聯)。</span><span class="sxs-lookup"><span data-stu-id="ff380-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="ff380-227">在這種情況下，您肯定會保持相容性層級 130，並使用查詢存放區的建議的先前查詢計畫。</span><span class="sxs-lookup"><span data-stu-id="ff380-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="ff380-228">如果您想要運用 Azure SQL Database (執行 SQL Server 2016) 的新特性與功能，但很容易相容性層級 130 所帶來的變更所影響，則最後的手段是使用 ALTER DATABASE 陳述式，考慮讓相容性層級強制回到符合您的工作負載的層級。</span><span class="sxs-lookup"><span data-stu-id="ff380-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="ff380-229">但首先，請注意查詢存放區計畫關聯選項是最佳的選擇，因為不使用 130 基本上會保持在舊版 SQL Server 的功能層級。</span><span class="sxs-lookup"><span data-stu-id="ff380-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="ff380-230">如果您有橫跨多個資料庫的多租用戶應用程式，則可能必須更新您的資料庫的佈建邏輯，以確保所有資料庫 (舊的和新佈建的) 的相容性層級都一致。</span><span class="sxs-lookup"><span data-stu-id="ff380-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="ff380-231">應用程式工作負載效能可能很容易受某些資料庫在不同相容性層級執行的這個事實所影響，因此，所有資料庫的相容性層級都必須一致，以便為所有的客戶提供相同的經驗。</span><span class="sxs-lookup"><span data-stu-id="ff380-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="ff380-232">請注意，這並非必要，實際上取決於您的應用程式受相容性層級影響的程度。</span><span class="sxs-lookup"><span data-stu-id="ff380-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="ff380-233">最後，至於基數估計，就像變更相容性層級一樣，在投入生產之前，建議在新的條件之下測試您的生產工作負載，以判斷您的應用程式是否受益於基數估計的改進。</span><span class="sxs-lookup"><span data-stu-id="ff380-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ff380-234">結論</span><span class="sxs-lookup"><span data-stu-id="ff380-234">Conclusion</span></span>
<span data-ttu-id="ff380-235">使用 Azure SQL Database 以受益於所有的 SQL Server 2016 增強功能，可以明顯地改善查詢執行。</span><span class="sxs-lookup"><span data-stu-id="ff380-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="ff380-236">現狀正是如此！</span><span class="sxs-lookup"><span data-stu-id="ff380-236">Just as-is!</span></span> <span data-ttu-id="ff380-237">當然，如同任何新功能，必須執行適當的評估，才能判斷您的資料庫工作負載運作最佳的確切條件。</span><span class="sxs-lookup"><span data-stu-id="ff380-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="ff380-238">經驗顯示，大部分的工作負載至少應該在相容性層級 130 之下以透明的方式執行，同時利用新的查詢處理函式和新的基數估計。</span><span class="sxs-lookup"><span data-stu-id="ff380-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="ff380-239">實際上，總有一些例外狀況，而進行適當的審慎調查是很重要的評估，用來判斷您可以從這些增強功能獲益多少。</span><span class="sxs-lookup"><span data-stu-id="ff380-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="ff380-240">同樣地，查詢存放區對於執行這項工作很有幫助！</span><span class="sxs-lookup"><span data-stu-id="ff380-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="ff380-241">隨著 SQL Azure 發展，您可以預見未來會有相容性層級 140。</span><span class="sxs-lookup"><span data-stu-id="ff380-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="ff380-242">在適當時機，我們會開始談論未來相容性層級 140 的願景，就像我們在此簡短討論相容性層級 130 的願景一樣。</span><span class="sxs-lookup"><span data-stu-id="ff380-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="ff380-243">我們現在別忘了，從 2016 年 6 月開始，Azure SQL Database 會將新建資料庫的預設相容性層級從 120 變更為 130。</span><span class="sxs-lookup"><span data-stu-id="ff380-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="ff380-244">請留意！</span><span class="sxs-lookup"><span data-stu-id="ff380-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="ff380-245">參考</span><span class="sxs-lookup"><span data-stu-id="ff380-245">References</span></span>
* [<span data-ttu-id="ff380-246">Database Engine 新功能</span><span class="sxs-lookup"><span data-stu-id="ff380-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="ff380-247">部落格︰查詢存放區︰您的資料庫的飛行資料記錄器 (Borko Novakovic，2016 年 6 月 8 日)</span><span class="sxs-lookup"><span data-stu-id="ff380-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="ff380-248">ALTER DATABASE 相容性層級 (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ff380-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="ff380-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="ff380-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="ff380-250">Azure SQL Database V12 的相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="ff380-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="ff380-251">使用 SQL Server 2014 基數估計器 (CE) 來最佳化查詢計劃</span><span class="sxs-lookup"><span data-stu-id="ff380-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="ff380-252">資料行存放區索引指南</span><span class="sxs-lookup"><span data-stu-id="ff380-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="ff380-253">落格︰改善 Azure SQL Database 中相容性層級 130 的查詢效能 (Alain Lissoir，2016 年 5 月 6 日)</span><span class="sxs-lookup"><span data-stu-id="ff380-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
