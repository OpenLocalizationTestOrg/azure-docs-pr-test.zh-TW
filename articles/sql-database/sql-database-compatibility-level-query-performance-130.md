---
title: "aaaDatabase 相容性等級 130 的 Azure SQL Database |Microsoft 文件"
description: "在本文中，我們將探索 hello 優勢的相容性層級 130，執行您的 Azure SQL Database 以及運用 hello 優點 hello 新查詢最佳化工具，查詢處理器功能。 我們也會解決 hello 可能副作用 hello hello 現有 SQL 應用程式的查詢效能。"
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="99776-104">改善 Azure SQL Database 中相容性層級 130 的查詢效能</span><span class="sxs-lookup"><span data-stu-id="99776-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="99776-105">Azure SQL Database 執行無障礙地數百個資料庫在許多不同的相容性層級，保留，並為所有客戶，以及確保 hello 回溯相容性 toohello 對應版本的 Microsoft SQL Server ！</span><span class="sxs-lookup"><span data-stu-id="99776-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="99776-106">在本文中，我們將探索 hello 優勢的相容性層級 130，執行您的 Azure SQL Database 以及運用 hello 優點 hello 新查詢最佳化工具，查詢處理器功能。</span><span class="sxs-lookup"><span data-stu-id="99776-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="99776-107">我們也會解決 hello 可能副作用 hello hello 現有 SQL 應用程式的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="99776-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="99776-108">歷程記錄的提醒的 SQL 版本 toodefault 相容性層級的 hello 對齊方式如下：</span><span class="sxs-lookup"><span data-stu-id="99776-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="99776-109">100：在 SQL Server 2008 和 Azure SQL Database V11 中。</span><span class="sxs-lookup"><span data-stu-id="99776-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="99776-110">110：在 SQL Server 2012 和 Azure SQL Database V11 中。</span><span class="sxs-lookup"><span data-stu-id="99776-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="99776-111">120：在 SQL Server 2014 和 Azure SQL Database V12 中。</span><span class="sxs-lookup"><span data-stu-id="99776-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="99776-112">130：在 SQL Server 2016 和 Azure SQL Database V12 中。</span><span class="sxs-lookup"><span data-stu-id="99776-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99776-113">從開始**2016 年 6 月 mid**，在 Azure SQL Database，hello 預設相容性層級會 130 而不是 120 個**新建**資料庫。</span><span class="sxs-lookup"><span data-stu-id="99776-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="99776-114">在 2016 年 6 月中旬前建立的資料庫將「不」  受影響，而且會維持其目前的相容性層級 (100、110 或 120)。</span><span class="sxs-lookup"><span data-stu-id="99776-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="99776-115">從 Azure SQL Database 版本 V11 tooV12 移轉的資料庫都會有 100 或 110 的相容性層級。</span><span class="sxs-lookup"><span data-stu-id="99776-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="99776-116">關於相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="99776-116">About compatibility level 130</span></span>
<span data-ttu-id="99776-117">首先，如果您想 tooknow hello 目前相容性層級的資料庫，執行下列 TRANSACT-SQL 陳述式的 hello。</span><span class="sxs-lookup"><span data-stu-id="99776-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="99776-118">在此變更之前就進行 toolevel 130**新**建立資料庫，讓我們檢閱這項變更是所有相關資訊，透過某些非常基本的查詢範例，並請參閱如何的任何人都可以從中受益。</span><span class="sxs-lookup"><span data-stu-id="99776-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="99776-119">關聯式資料庫中的查詢處理可能會很複雜，而且可能會 toolots 電腦科學和數學 toounderstand hello 固有的設計選項和行為。</span><span class="sxs-lookup"><span data-stu-id="99776-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="99776-120">本文件中，在 hello 內容已經過刻意簡化的 tooensure 某些最小的技術背景的任何人都可以用來了解 hello 影響 hello 相容性層級變更，並判斷它的優點的應用程式。</span><span class="sxs-lookup"><span data-stu-id="99776-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="99776-121">讓我們先快速查看哪些 hello 相容性層級 130 會在 [hello] 資料表。</span><span class="sxs-lookup"><span data-stu-id="99776-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="99776-122">您可以在 [ALTER DATABASE 相容性層級 (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)找到更多詳細資料，但簡短摘要如下︰</span><span class="sxs-lookup"><span data-stu-id="99776-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="99776-123">hello Insert select 陳述式的 Insert 作業可以是多執行緒或可以有平行計畫，而這項作業為單一執行緒之前。</span><span class="sxs-lookup"><span data-stu-id="99776-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="99776-124">記憶體最佳化資料表和資料表變數查詢現在可以有平行計劃，而這項作業之前也是單一執行緒作業。</span><span class="sxs-lookup"><span data-stu-id="99776-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="99776-125">記憶體最佳化資料表的統計資料現在可以取樣並會自動更新。</span><span class="sxs-lookup"><span data-stu-id="99776-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="99776-126">如需詳細資訊，請參閱 [Database Engine 新功能：In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) 。</span><span class="sxs-lookup"><span data-stu-id="99776-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="99776-127">資料行存放區索引的批次模式和資料列模式變更</span><span class="sxs-lookup"><span data-stu-id="99776-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="99776-128">具有資料行存放區索引的資料表現在會以批次模式排序。</span><span class="sxs-lookup"><span data-stu-id="99776-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="99776-129">時間範圍彙總現在以批次模式運作，例如 TSQL LAG/LEAD 陳述式。</span><span class="sxs-lookup"><span data-stu-id="99776-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="99776-130">具有多個不同子句的資料行存放區資料表會以批次模式進行查詢。</span><span class="sxs-lookup"><span data-stu-id="99776-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="99776-131">在 DOP = 1 之下執行或具有序列計劃的查詢也會以批次模式執行。</span><span class="sxs-lookup"><span data-stu-id="99776-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="99776-132">最後，基數估計的改進實際上相容性層級 120，但如果您執行較低的相容性層級 （也就是 100 或 110）、 hello 移動 toocompatibility 層級 130 也將這些增強功能，以及有這些也可以獲得更佳應用程式的 hello 查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="99776-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="99776-133">演練相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="99776-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="99776-134">第一個我們得到一些資料表、 索引和建立隨機資料 toopractice 某些這些新功能。</span><span class="sxs-lookup"><span data-stu-id="99776-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="99776-135">SQL Server 2016 中，或 Azure SQL Database 下，可以執行 hello TSQL 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="99776-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="99776-136">不過，在建立 Azure SQL database 時，請確定您選擇在 hello 最小 P2 資料庫，因為您必須至少有幾個核心 tooallow 多執行緒處理，並因此受益於這些功能。</span><span class="sxs-lookup"><span data-stu-id="99776-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="99776-137">現在，讓我們先尋找 toosome 即將相容性層級 130 的 hello 查詢處理功能。</span><span class="sxs-lookup"><span data-stu-id="99776-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="99776-138">平行 INSERT</span><span class="sxs-lookup"><span data-stu-id="99776-138">Parallel INSERT</span></span>
<span data-ttu-id="99776-139">執行下列的 hello TSQL 陳述式執行 hello 相容性層級 120 和 130，它會在單一執行緒模型 (120)，並在多執行緒模型 (130) 中分別執行 hello 插入作業的插入作業。</span><span class="sxs-lookup"><span data-stu-id="99776-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="99776-140">藉由要求 hello hello 實際查詢計劃，查看其圖形表示法或其 XML 內容，您可以判斷哪一個函式會在播放的基數估計。</span><span class="sxs-lookup"><span data-stu-id="99776-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="99776-141">查看圖 1 中的 hello 計劃-並存，我們可以清楚地看到該 hello 插入的資料行存放區執行會進入從序列中 120 tooparallel 130。</span><span class="sxs-lookup"><span data-stu-id="99776-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="99776-142">另外請注意顯示兩個平行的箭號，說明現在 hello 迭代器執行的 hello 事實確實平行 hello 130 計劃中的 hello 變更的 hello 迭代器圖示。</span><span class="sxs-lookup"><span data-stu-id="99776-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="99776-143">如果您有大型的 INSERT 作業 toocomplete，hello 平行執行，連結的 toohello 您有在 hello 資料庫，供您使用的核心數目執行效能。向上 tooa 100 倍視情況 ！</span><span class="sxs-lookup"><span data-stu-id="99776-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="99776-144">*圖 1： 從相容性層級 130 的序列 tooparallel 插入作業變更。*</span><span class="sxs-lookup"><span data-stu-id="99776-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![圖 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="99776-146">序列批次模式</span><span class="sxs-lookup"><span data-stu-id="99776-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="99776-147">同樣地，當處理資料列的資料移動 toocompatibility 層級 130 啟用批次模式處理。</span><span class="sxs-lookup"><span data-stu-id="99776-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="99776-148">第一，批次模式作業僅適用於您已備妥資料行存放區索引時。</span><span class="sxs-lookup"><span data-stu-id="99776-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="99776-149">第二，批次通常代表 ~ 900 個資料列，會使用針對多核心 CPU、 記憶體較高的輸送量最佳化的程式碼邏輯和直接利用 hello hello 盡可能的資料行存放區的壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="99776-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="99776-150">在這些情況中下, SQL Server 2016 可以同時發生，處理 ~ 900 的資料列，而不是在 hello 階段 1 個資料列，因此，hello hello 作業的整體額外負荷成本都現在共用 hello 整個批次，減少 hello 整體成本資料列。</span><span class="sxs-lookup"><span data-stu-id="99776-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="99776-151">此共用的作業基本上與 hello 資料行存放區壓縮結合量可減少選取的批次模式作業中的 hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="99776-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="99776-152">關於 hello 資料行存放區尋找更多詳細資料和批次模式在[資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99776-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="99776-153">為顯示下方，觀察 hello 查詢計劃-並存上圖 2 中，我們可以看到到 hello 處理模式已變更 hello 相容性層級，且其結果是，當執行 hello 查詢這兩個相容性層級中，我們可以看到大部分的 hello 處理時間花在資料列模式 （86%) 相較 toohello 批次模式 （14%)、 2 批次已處理的所在。</span><span class="sxs-lookup"><span data-stu-id="99776-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="99776-154">增加 hello 資料集，hello 權益會逐漸增加。</span><span class="sxs-lookup"><span data-stu-id="99776-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="99776-155">*圖 2： 從相容性層級 130 的序列 toobatch 模式選取作業的變更。*</span><span class="sxs-lookup"><span data-stu-id="99776-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![圖 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="99776-157">排序執行的批次模式</span><span class="sxs-lookup"><span data-stu-id="99776-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="99776-158">從資料列模式 （相容性層級 120） toobatch 模式 （相容性層級 130） 的類似 toohello 上述項目，但套用的 tooa 排序作業，hello 轉換，改善 hello 效能 hello hello 的排序作業相同的原因。</span><span class="sxs-lookup"><span data-stu-id="99776-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="99776-159">顯示由並行上圖 3，我們可以看到 hello 排序作業，資料列模式代表 81 hello 成本，而 hello 批次模式只代表 19 %hello 成本 （分別 81%和 56 %hello 排序本身上） 的百分比。</span><span class="sxs-lookup"><span data-stu-id="99776-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="99776-160">*圖 3： 從資料列 toobatch 模式相容性層級 130 排序作業變更。*</span><span class="sxs-lookup"><span data-stu-id="99776-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![圖 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="99776-162">很明顯地，這些範例只包含數以萬計的資料列，這會是 nothing 近來查看大多數的 SQL Server 中可用的 hello 資料時。</span><span class="sxs-lookup"><span data-stu-id="99776-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="99776-163">相反地，只要專案數百萬列的這些，而且這可以轉譯在幾分鐘的時間可以節省運算暫止的工作負載的 hello 本質每天執行。</span><span class="sxs-lookup"><span data-stu-id="99776-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="99776-164">基數估計 (CE) 改進</span><span class="sxs-lookup"><span data-stu-id="99776-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="99776-165">使用 SQL Server 2014 引進，可讓任何資料庫相容性層級 120 或更新版本執行 hello 新的基數估計功能使用。</span><span class="sxs-lookup"><span data-stu-id="99776-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="99776-166">基本上，基數估計是使用 SQL server 將如何執行查詢，根據其估計的成本 toodetermine hello 邏輯。</span><span class="sxs-lookup"><span data-stu-id="99776-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="99776-167">使用來自該查詢中所涉及的物件相關聯的統計資料的輸入來計算 hello 估計。</span><span class="sxs-lookup"><span data-stu-id="99776-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="99776-168">實際上，在高層次，基數估計函數以及 hello 值分佈的 hello，相異值計數的相關資訊的資料列計數估計以及重複計數會包含在 hello 資料表和 hello 查詢中參考的物件。</span><span class="sxs-lookup"><span data-stu-id="99776-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="99776-169">Tooa 選取項目，透過平行序列計畫執行的計劃執行，tooname 一些或取得這些估計不正確，可能會導致 toounnecessary 磁碟 I/O，因為 tooinsufficient 記憶體授權 （也就是 TempDB 溢出）。</span><span class="sxs-lookup"><span data-stu-id="99776-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="99776-170">結束時，不正確的估計值可能會導致 tooan hello 執行查詢的整體效能降低。</span><span class="sxs-lookup"><span data-stu-id="99776-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="99776-171">在 hello 其他側邊、 更佳的估計值、 估計較為精確，潛在客戶 toobetter 查詢執行 ！</span><span class="sxs-lookup"><span data-stu-id="99776-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="99776-172">如前所述，查詢最佳化和評估複雜的主題、 但如果您想 toolearn 更多關於查詢計劃和基數估計工具，您可以參考 toohello 文件[最佳化您的查詢計劃 hello SQL Server 2014基數估計工具](https://msdn.microsoft.com/library/dn673537.aspx)的深入剖析。</span><span class="sxs-lookup"><span data-stu-id="99776-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="99776-173">您目前使用哪個基數估計？</span><span class="sxs-lookup"><span data-stu-id="99776-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="99776-174">toodetermine 下執行查詢的基數估計，我們只使用 hello 查詢範例如下。</span><span class="sxs-lookup"><span data-stu-id="99776-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="99776-175">請注意，第一個範例會執行在相容性層級 110，意味著 hello 使用 hello 舊的基數估計函式。</span><span class="sxs-lookup"><span data-stu-id="99776-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="99776-176">完成執行之後，請按一下 hello XML 連結，並查看 hello hello 第一個迭代器的屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="99776-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="99776-177">請注意呼叫目前設於 70 CardinalityEstimationModelVersion hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="99776-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="99776-178">並不表示 hello 資料庫相容性層級設定 （它設定為在上述的 hello TSQL 陳述式中可見的 110 上），toohello SQL Server 7.0 版，但 hello 值 70 只代表 hello 舊版基數估計功能自 SQL 起可用伺服器 7.0、 SQL Server 2014 （隨附於相容性層級為 120） 之前有沒有主要修訂。</span><span class="sxs-lookup"><span data-stu-id="99776-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="99776-179">*圖 4: hello CardinalityEstimationModelVersion too70 時設定使用相容性層級為 110 或下方。*</span><span class="sxs-lookup"><span data-stu-id="99776-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![圖 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="99776-181">或者，您可以變更相容性層級 too130 hello，並使用 LEGACY_CARDINALITY_ESTIMATION 設定 tooON 與 hello 停用 hello 使用新的基數估計函式，hello [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="99776-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="99776-182">這會是完全 hello 與使用基數估計函式觀點來看，從 110 時使用 hello 最新查詢處理相容性層級相同。</span><span class="sxs-lookup"><span data-stu-id="99776-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="99776-183">這樣做，您就可以受益於 hello 新查詢處理來自 hello 最新相容性層級 （也就是批次模式） 的功能，但仍依賴 hello 舊的基數估計功能，如有必要。</span><span class="sxs-lookup"><span data-stu-id="99776-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="99776-184">只移動 toohello 相容性等級 120 或 130 啟用 hello 新的基數估計功能。</span><span class="sxs-lookup"><span data-stu-id="99776-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="99776-185">在這種情況下，too120 或下方的 做為可見 130，則會據以設定 hello 預設 CardinalityEstimationModelVersion。</span><span class="sxs-lookup"><span data-stu-id="99776-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="99776-186">*圖 5: hello CardinalityEstimationModelVersion too130 時設定使用 130 的相容性層級。*</span><span class="sxs-lookup"><span data-stu-id="99776-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![圖 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="99776-188">Witnessing hello 基數估計差異</span><span class="sxs-lookup"><span data-stu-id="99776-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="99776-189">現在，我們先執行稍微複雜查詢涉及 INNER JOIN 使用 WHERE 子句的部分述詞，並讓我們看看 hello 資料列計數估計 hello 舊的基數估計函數從第一次。</span><span class="sxs-lookup"><span data-stu-id="99776-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="99776-190">有效地執行這項查詢會傳回 200,704 資料列，而 hello 與 hello 舊的基數估計功能的資料列估計宣告 194,284 資料列。</span><span class="sxs-lookup"><span data-stu-id="99776-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="99776-191">很明顯地，如上述，這些資料列計數結果也取決於頻率執行 hello 先前的範例，其中會填入 hello 不斷地在每次執行的範例資料表。</span><span class="sxs-lookup"><span data-stu-id="99776-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="99776-192">很明顯地，在查詢中的 hello 述詞也會有影響 hello 實際估計除了 hello 資料表形狀、 資料內容，和如何這項資料實際上相互關聯與彼此。</span><span class="sxs-lookup"><span data-stu-id="99776-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="99776-193">*圖 6: hello 資料列計數估計超出 194,284 或 6000 的資料列從預期的 hello 200,704 資料列。*</span><span class="sxs-lookup"><span data-stu-id="99776-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![圖 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="99776-195">在 hello 同樣地，我們現在執行相同查詢搭配新的基數估計功能 hello hello。</span><span class="sxs-lookup"><span data-stu-id="99776-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="99776-196">查看 hello 以下，我們現在看到該 hello 資料列估計為 202,877，或更為接近而且多於 hello 舊的基數估計。</span><span class="sxs-lookup"><span data-stu-id="99776-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="99776-197">*圖 7: hello 資料列計數估計現在是 202,877，而不是 194,284。*</span><span class="sxs-lookup"><span data-stu-id="99776-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![圖 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="99776-199">事實上，hello 結果集是 200,704 的資料列 （但都取決於您未執行頻率的 hello hello 查詢先前的範例，但更重要的是，hello TSQL 使用 hello rand （） 陳述式，因為 hello 傳回的實際值可能與一個執行 toohello 旁邊）。</span><span class="sxs-lookup"><span data-stu-id="99776-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="99776-200">因此，在此特定範例中，hello 新的基數估計會執行在估計 hello 的資料列數目，因為 202,877 更接近 too200，704，比 194,284 更好 ！</span><span class="sxs-lookup"><span data-stu-id="99776-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="99776-201">最後，如果您變更 WHERE 子句述詞 tooequality hello (而非">"執行個體)，這可能會使 hello 評估 hello 舊與新的基數函式之間更不同，視多少相符記錄而定，您可以取得。</span><span class="sxs-lookup"><span data-stu-id="99776-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="99776-202">很明顯地，在此情況下，與實際計數相差 ~6000 個資料列，在某些情況下並不代表大量資料。</span><span class="sxs-lookup"><span data-stu-id="99776-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="99776-203">現在，跨數個資料表和更複雜的查詢，轉置的資料列的這個 toomillions 有時候 hello 估計還可以和關閉數百萬個資料列，因此，hello 挑選向上 hello 錯誤執行計畫，或要求記憶體不足，無法授與前置的風險tooTempDB 轉散，並因此多個 I/O，會高出許多。</span><span class="sxs-lookup"><span data-stu-id="99776-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="99776-204">如果您有機會 hello，練習這項比較最常見的查詢與資料集，並且親自體驗了多少有些 hello 舊和新估計受到影響，而某些可能就會變得關閉 hello 現實情況下，從更多或某些其他人只較接近 toohello 實際資料列計算實際 hello 結果集中傳回。</span><span class="sxs-lookup"><span data-stu-id="99776-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="99776-205">取決於它的所有查詢、 hello Azure SQL 資料庫特性、 hello 本質和 hello 大小的資料集和 hello 提供其相關的統計資料的 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="99776-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="99776-206">如果您剛剛建立您的 Azure SQL Database 執行個體、 hello 查詢最佳化工具會有 toobuild 了解，而不是重複使用的統計資料的 hello 先前查詢所做的重新執行。</span><span class="sxs-lookup"><span data-stu-id="99776-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="99776-207">因此，hello 估計是非常內容和幾乎特定 tooevery 伺服器和應用程式的情況。</span><span class="sxs-lookup"><span data-stu-id="99776-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="99776-208">它是在心的重要層面 tookeep ！</span><span class="sxs-lookup"><span data-stu-id="99776-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="99776-209">納入考量的一些考量 tootake</span><span class="sxs-lookup"><span data-stu-id="99776-209">Some considerations tootake into account</span></span>
<span data-ttu-id="99776-210">雖然大部分的工作負載而獲益 hello 相容性層級 130 採用您的生產環境的 hello 相容性層級之前，您基本上會有 3 個選項：</span><span class="sxs-lookup"><span data-stu-id="99776-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="99776-211">您將 toocompatibility 層級 130，並查看項目執行的方式。</span><span class="sxs-lookup"><span data-stu-id="99776-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="99776-212">如果您注意到某些迴歸，您只設定 hello 相容性層級回復 tooits 原始的層級，或保留 130 和只反向 hello 基數估計回復 toohello 舊版模式 （以上所述，這單獨無法解決 hello 問題）。</span><span class="sxs-lookup"><span data-stu-id="99776-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="99776-213">您藉此徹底測試您現有的應用程式，類似的生產負載、 微調，以及驗證之前進行 tooproduction hello 效能。</span><span class="sxs-lookup"><span data-stu-id="99776-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="99776-214">若有任何問題，與上述相同可以永遠返回 toohello 原始相容性層級，或直接反向操作 hello 基數估計回復 toohello 傳統模式。</span><span class="sxs-lookup"><span data-stu-id="99776-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="99776-215">做為最後一個選項，以及 hello 最新的方式 tooaddress 這些問題，是 tooleverage hello 查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="99776-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="99776-216">這是現今的建議選項！</span><span class="sxs-lookup"><span data-stu-id="99776-216">That’s today’s recommended option!</span></span> <span data-ttu-id="99776-217">tooassist hello 分析您的查詢，在相容性層級 120 或下方與 130，不建議您足夠 toouse 查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="99776-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="99776-218">查詢存放區與 hello 最新版本的 Azure SQL Database V12，而且其設計目的是 toohelp 您的查詢效能的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="99776-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="99776-219">將為您收集及呈現有關所有查詢的詳細歷程記錄資訊的資料庫的飛行資料記錄器視為 hello 查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="99776-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="99776-220">這可大幅減少 hello 時間 toodiagnose 簡化效能鑑識調查並解決問題。</span><span class="sxs-lookup"><span data-stu-id="99776-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="99776-221">如需詳細資訊，請參閱 [查詢存放區︰您的資料庫的飛行資料記錄器](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。</span><span class="sxs-lookup"><span data-stu-id="99776-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="99776-222">在高層級，如果您已經有一組資料庫執行相容性層級 120 或以下，且計劃 toomove hello 其中部分 too130，或因為您的工作負載自動佈建的新資料庫將會很快就會由預設 too130 設定，請考慮hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="99776-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="99776-223">在變更之前 toohello 新相容性層級在生產環境中的，啟用查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="99776-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="99776-224">您可以使用參照太[變更 hello 資料庫相容性模式並使用 hello 查詢存放區](https://msdn.microsoft.com/library/bb895281.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99776-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="99776-225">接著，測試所有重要的工作負載使用具代表性的資料和類似實際執行環境和發生的比較 hello 效能及與查詢存放區所報告的查詢。</span><span class="sxs-lookup"><span data-stu-id="99776-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="99776-226">如果您遇到某些迴歸，您可以識別 hello 迴歸的查詢以 hello 查詢存放區，並使用 hello 計畫強制執行查詢存放區中的選項 （也稱為計畫釘選）。</span><span class="sxs-lookup"><span data-stu-id="99776-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="99776-227">在這種情況下，您針對保持 hello 相容性層級 130 並且 hello 先前的查詢計劃為 hello 查詢存放區的建議。</span><span class="sxs-lookup"><span data-stu-id="99776-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="99776-228">如果您想 tooleverage 新特色與功能的 Azure SQL Database （這執行 SQL Server 2016），但是機密 toochanges 由 hello 相容性層級 130 的最後手段，您可以考慮強制 hello 相容性層級備份使用 ALTER DATABASE 陳述式來符合您的工作負載的 toohello 層級。</span><span class="sxs-lookup"><span data-stu-id="99776-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="99776-229">但首先，注意 hello 查詢存放區方案釘選 選項處於最佳選項，因為未使用 130 基本上保持在 hello 功能層級的較舊的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="99776-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="99776-230">如果您有跨越多個資料庫的多租用戶應用程式時，可能需要 tooupdate hello 佈建您的資料庫 tooensure 一致的相容性層級的邏輯，所有的資料庫;舊的和新佈建項目。</span><span class="sxs-lookup"><span data-stu-id="99776-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="99776-231">應用程式工作負載效能可能是有些資料庫執行不同的相容性層級的機密 toohello 事實，因此，可能需要的任何資料庫的相容性層級一致性 tooprovide hello 相同的順序所有跨 hello 面板中遇到 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="99776-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="99776-232">請注意，它不是託管，它其實取決於您的應用程式如何受到 hello 相容性層級。</span><span class="sxs-lookup"><span data-stu-id="99776-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="99776-233">最後，有關 hello 基數估計一樣 hello 相容性層級，再繼續在生產環境中，變更它，如果您的應用程式受惠建議 tootest hello 新條件 toodetermine 下的您生產工作負載hello 基數估計的改進。</span><span class="sxs-lookup"><span data-stu-id="99776-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="99776-234">結論</span><span class="sxs-lookup"><span data-stu-id="99776-234">Conclusion</span></span>
<span data-ttu-id="99776-235">使用 Azure SQL Database 所有 SQL Server 2016 增強 toobenefit 清楚可以改善查詢執行。</span><span class="sxs-lookup"><span data-stu-id="99776-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="99776-236">現狀正是如此！</span><span class="sxs-lookup"><span data-stu-id="99776-236">Just as-is!</span></span> <span data-ttu-id="99776-237">當然，任何新功能，像是正確評估必須完成的資料庫工作負載運作 hello 最佳 toodetermine hello 確切條件。</span><span class="sxs-lookup"><span data-stu-id="99776-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="99776-238">經驗顯示，大部分的工作負載所預期的 tooat 至少執行無障礙地相容性等級 130，同時利用新的查詢處理函式和新的基數估計。</span><span class="sxs-lookup"><span data-stu-id="99776-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="99776-239">所雖如此，實際上，總是會有一些例外狀況，以及執行適當的到期勤加注意的重要評估 toodetermine 多少您可以從這些增強功能獲益。</span><span class="sxs-lookup"><span data-stu-id="99776-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="99776-240">同樣地，hello 查詢存放區可以是大的幫助，在此情況下這項工作 ！</span><span class="sxs-lookup"><span data-stu-id="99776-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="99776-241">隨著 SQL Azure 的發展，您可以預期未來 hello 相容性層級 140。</span><span class="sxs-lookup"><span data-stu-id="99776-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="99776-242">在適當時機，我們會開始談論未來相容性層級 140 的願景，就像我們在此簡短討論相容性層級 130 的願景一樣。</span><span class="sxs-lookup"><span data-stu-id="99776-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="99776-243">現在，我們不忘記，從 2016 年 6 月開始，Azure SQL Database，將變更 hello 預設相容性層級 120 too130 新建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="99776-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="99776-244">請留意！</span><span class="sxs-lookup"><span data-stu-id="99776-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="99776-245">參考</span><span class="sxs-lookup"><span data-stu-id="99776-245">References</span></span>
* [<span data-ttu-id="99776-246">Database Engine 新功能</span><span class="sxs-lookup"><span data-stu-id="99776-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="99776-247">部落格︰查詢存放區︰您的資料庫的飛行資料記錄器 (Borko Novakovic，2016 年 6 月 8 日)</span><span class="sxs-lookup"><span data-stu-id="99776-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="99776-248">ALTER DATABASE 相容性層級 (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="99776-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="99776-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="99776-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="99776-250">Azure SQL Database V12 的相容性層級 130</span><span class="sxs-lookup"><span data-stu-id="99776-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="99776-251">最佳化查詢計劃您的 SQL Server 2014 的基數估計工具 hello 與</span><span class="sxs-lookup"><span data-stu-id="99776-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="99776-252">資料行存放區索引指南</span><span class="sxs-lookup"><span data-stu-id="99776-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="99776-253">落格︰改善 Azure SQL Database 中相容性層級 130 的查詢效能 (Alain Lissoir，2016 年 5 月 6 日)</span><span class="sxs-lookup"><span data-stu-id="99776-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
