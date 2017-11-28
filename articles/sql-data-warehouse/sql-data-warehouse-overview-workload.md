---
title: "深入了解 Azure SQL 資料倉儲作業 |Microsoft Docs"
description: "SQL 資料倉儲的彈性可讓您以滑動的方式調整資料倉儲單位 (DWU)，來增加、縮減或暫停計算能力。 本文說明資料倉儲指標以及它們與 DWU 之間的關係。 "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 629ce22bf669a760d041bbd006b836d2da5d237b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="data-warehouse-workload"></a><span data-ttu-id="aa221-104">資料倉儲工作負載</span><span class="sxs-lookup"><span data-stu-id="aa221-104">Data warehouse workload</span></span>
<span data-ttu-id="aa221-105">資料倉儲工作負載是指所有針對資料倉儲所發生的作業。</span><span class="sxs-lookup"><span data-stu-id="aa221-105">A data warehouse workload refers to all of the operations that transpire against a data warehouse.</span></span> <span data-ttu-id="aa221-106">資料倉儲工作負載包含將資料載入倉儲、對資料倉儲執行分析和報告、管理資料倉儲中的資料，以及從資料倉儲匯出資料的整個程序。</span><span class="sxs-lookup"><span data-stu-id="aa221-106">The data warehouse workload encompasses the entire process of loading data into the warehouse, performing analysis and reporting on the data warehouse, managing data in the data warehouse, and exporting data from the data warehouse.</span></span> <span data-ttu-id="aa221-107">這些元件的廣度與深度多半與資料倉儲的成熟度相當。</span><span class="sxs-lookup"><span data-stu-id="aa221-107">The depth and breadth of these components are often commensurate with the maturity level of the data warehouse.</span></span>

## <a name="new-to-data-warehousing"></a><span data-ttu-id="aa221-108">您是資料倉儲新手嗎？</span><span class="sxs-lookup"><span data-stu-id="aa221-108">New to data warehousing?</span></span>
<span data-ttu-id="aa221-109">資料倉儲是從一或多個資料來源載入的資料集合，並可用來執行商業智慧工作，例如報告和資料分析。</span><span class="sxs-lookup"><span data-stu-id="aa221-109">A data warehouse is a collection of data that is loaded from one or more data sources and is used to perform business intelligence tasks such as reporting and data analysis.</span></span>

<span data-ttu-id="aa221-110">資料倉儲的特點在於查詢可以掃描數量較大的資料列、大範圍的資料，還可以傳回相對大量的結果以供用於分析和報告目的。</span><span class="sxs-lookup"><span data-stu-id="aa221-110">Data warehouses are characterized by queries that scan larger numbers of rows, large ranges of data and may return relatively large results for the purposes of analysis and reporting.</span></span> <span data-ttu-id="aa221-111">與小量交易層級的插入/更新/刪除作業相比，可載入相對大量的資料，也是資料倉儲的特點。</span><span class="sxs-lookup"><span data-stu-id="aa221-111">Data warehouses are also characterized by relatively large data loads versus small transaction-level inserts/updates/deletes.</span></span>

* <span data-ttu-id="aa221-112">如果以掃描大量資料列或大範圍資料所需的最佳化查詢方式儲存資料，資料倉儲便能提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="aa221-112">A data warehouse performs best when the data is stored in a way that optimizes queries that need to scan large numbers of rows or large ranges of data.</span></span> <span data-ttu-id="aa221-113">如果資料是依資料行 (而非資料列) 來儲存和搜尋，這種掃描類型便能提供最佳效果。</span><span class="sxs-lookup"><span data-stu-id="aa221-113">This type of scanning works best when the data is stored and searched by columns, instead of by rows.</span></span>

> [!NOTE]
> <span data-ttu-id="aa221-114">和用來報告和分析查詢的傳統二進位樹狀目錄相比，使用資料行儲存體的記憶體內部資料行存放區索引，最多可提升 10 倍壓縮速度與 100 倍查詢效能。</span><span class="sxs-lookup"><span data-stu-id="aa221-114">The in-memory columnstore index, which uses column storage, provides up to 10x compression gains and 100x query performance gains over traditional binary trees for reporting and analytics queries.</span></span> <span data-ttu-id="aa221-115">我們將資料行存放區索引視為在資料倉儲中儲存和掃描大量資料的標準。</span><span class="sxs-lookup"><span data-stu-id="aa221-115">We consider columnstore indexes as the standard for storing and scanning large data in a data warehouse.</span></span>
> 
> 

* <span data-ttu-id="aa221-116">資料倉儲和最佳化線上交易處理 (OLTP) 系統各有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="aa221-116">A data warehouse has different requirements than a system that optimizes for online transaction processing (OLTP).</span></span> <span data-ttu-id="aa221-117">OLTP 系統有許多插入、更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="aa221-117">The OLTP system has many insert, update, and delete operations.</span></span> <span data-ttu-id="aa221-118">這些作業會搜尋資料表中的特定資料列。</span><span class="sxs-lookup"><span data-stu-id="aa221-118">These operations seek to specific rows in the table.</span></span> <span data-ttu-id="aa221-119">如果資料以逐列方式儲存，資料表搜尋便能提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="aa221-119">Table seeks perform best when the data is stored in a row-by-row manner.</span></span> <span data-ttu-id="aa221-120">資料可以使用分治法 (稱為二進位樹狀目錄或 btree 搜尋) 來排序和快速搜尋。</span><span class="sxs-lookup"><span data-stu-id="aa221-120">The data can be sorted and quickly searched with a divide and conquer approach called a binary tree or btree search.</span></span>

## <a name="data-loading"></a><span data-ttu-id="aa221-121">載入資料</span><span class="sxs-lookup"><span data-stu-id="aa221-121">Data loading</span></span>
<span data-ttu-id="aa221-122">資料倉儲工作負載大部分都是在載入資料。</span><span class="sxs-lookup"><span data-stu-id="aa221-122">Data loading is a big part of the data warehouse workload.</span></span> <span data-ttu-id="aa221-123">企業的 OLTP 系統通常忙於追蹤客戶一整天下來產生的商務交易變更。</span><span class="sxs-lookup"><span data-stu-id="aa221-123">Businesses usually have a busy OLTP system that tracks changes throughout the day when customers are generating business transactions.</span></span> <span data-ttu-id="aa221-124">通常在夜間進行的維護作業會定期將交易移動或複製到資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="aa221-124">Periodically, often at night during a maintenance window, the transactions are moved or copied to the data warehouse.</span></span> <span data-ttu-id="aa221-125">資料一旦進入資料倉儲，分析師就能夠執行分析，並根據資料做出商業決策。</span><span class="sxs-lookup"><span data-stu-id="aa221-125">Once the data is in the data warehouse, analysts can perform analysis and make business decisions on the data.</span></span>

* <span data-ttu-id="aa221-126">傳統上，載入的程序稱為 ETL，也就是「擷取」(Extract)、「轉換」(Transform) 及「載入」(Load)。</span><span class="sxs-lookup"><span data-stu-id="aa221-126">Traditionally, the process of loading is called ETL for Extract, Transform, and Load.</span></span> <span data-ttu-id="aa221-127">資料通常需要進行轉換，才能與資料倉儲中的其他資料保持一致。</span><span class="sxs-lookup"><span data-stu-id="aa221-127">Data usually needs to be transformed so it is consistent with other data in the data warehouse.</span></span> <span data-ttu-id="aa221-128">以前企業會使用專用的 ETL 伺服器來執行轉換。</span><span class="sxs-lookup"><span data-stu-id="aa221-128">Previously, businesses used dedicated ETL servers to perform the transformations.</span></span> <span data-ttu-id="aa221-129">現在要進行如此快速的大量平行處理程序，您可以先將資料載入 SQL 資料倉儲，然後再執行轉換。</span><span class="sxs-lookup"><span data-stu-id="aa221-129">Now, with such fast massively parallel processing you can load data into SQL Data Warehouse first, and then perform the transformations.</span></span> <span data-ttu-id="aa221-130">這個稱為擷取、載入及轉換 (ELT) 的程序，正逐漸成為資料倉儲工作負載的全新標準。</span><span class="sxs-lookup"><span data-stu-id="aa221-130">This process is called Extract, Load, and Transform (ELT), and is becoming a new standard for the data warehouse workload.</span></span>

> [!NOTE]
> <span data-ttu-id="aa221-131">現在，使用 SQL Server 2016 就能即時在 OLTP 資料表上執行分析。</span><span class="sxs-lookup"><span data-stu-id="aa221-131">With SQL Server 2016, you can now perform analytics in real-time on an OLTP table.</span></span> <span data-ttu-id="aa221-132">雖然這不會取代資料倉儲儲存和分析資料的需求，但的確能夠用來進行即時執行分析。</span><span class="sxs-lookup"><span data-stu-id="aa221-132">This does not replace the need for a data warehouse to store and analyze data, but it does provide a way to perform analysis in real-time.</span></span>
> 
> 

### <a name="reporting-and-analysis-queries"></a><span data-ttu-id="aa221-133">報告和分析查詢</span><span class="sxs-lookup"><span data-stu-id="aa221-133">Reporting and analysis queries</span></span>
<span data-ttu-id="aa221-134">報告和分析查詢通常會根據幾個條件分成小型、中型和大型，但通常是根據時間。</span><span class="sxs-lookup"><span data-stu-id="aa221-134">Reporting and analysis queries are often categorized into small, medium and large based on a number of criteria, but usually it is based on time.</span></span> <span data-ttu-id="aa221-135">大部分的資料倉儲中，還有混合快速執行與長時間執行查詢的工作負載。</span><span class="sxs-lookup"><span data-stu-id="aa221-135">In most data warehouses, there is a mixed workload of fast-running versus long-running queries.</span></span> <span data-ttu-id="aa221-136">在每個案例都務必判斷此混合方式以及它的頻率 (每小時、每天、月末、季末等等)。</span><span class="sxs-lookup"><span data-stu-id="aa221-136">In each case, it is important to determine this mix and to determine its frequency (hourly, daily, month-end, quarter-end, and so on).</span></span> <span data-ttu-id="aa221-137">請務必了解混合式查詢工作負載搭配並行存取，為資料倉儲適當規劃容量。</span><span class="sxs-lookup"><span data-stu-id="aa221-137">It is important to understand that the mixed query workload, coupled with concurrency, lead to proper capacity planning for a data warehouse.</span></span>

* <span data-ttu-id="aa221-138">對於混合式的查詢工作負載而言，容量規劃是一項複雜的工作，尤其是當您需要很長的前置時間以將容量增加到資料倉儲時。</span><span class="sxs-lookup"><span data-stu-id="aa221-138">Capacity planning can be a complex task for a mixed query workload, especially when you need a long lead time to add capacity to the data warehouse.</span></span> <span data-ttu-id="aa221-139">SQL 資料倉儲可讓容量規劃不再急迫，因為您可以隨時增加或縮減計算容量，而且能夠獨立地調整儲存體和計算容量。</span><span class="sxs-lookup"><span data-stu-id="aa221-139">SQL Data Warehouse removes the urgency of capacity planning since you can grow and shrink compute capacity at any time, and since storage and compute capacity are independently sized.</span></span>

### <a name="data-management"></a><span data-ttu-id="aa221-140">資料管理</span><span class="sxs-lookup"><span data-stu-id="aa221-140">Data management</span></span>
<span data-ttu-id="aa221-141">管理資料相當重要，尤其是當您知道不久之後可能會用盡磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="aa221-141">Managing data is important, especially when you know you might run out of disk space in the near future.</span></span> <span data-ttu-id="aa221-142">資料倉儲通常會將資料分割成有意義的範圍，並儲存為資料表中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="aa221-142">Data warehouses usually divide the data into meaningful ranges, which are stored as partitions in a table.</span></span> <span data-ttu-id="aa221-143">所有 SQL Server 式產品都可讓您將資料分割移入和移出資料表。</span><span class="sxs-lookup"><span data-stu-id="aa221-143">All SQL Server-based products let you move partitions in and out of the table.</span></span> <span data-ttu-id="aa221-144">此資料分割切換可讓您將較舊的資料移至較便宜的儲存體，並將最新的資料保留在線上儲存體。</span><span class="sxs-lookup"><span data-stu-id="aa221-144">This partition switching lets you move older data to less expensive storage and keep the latest data available on online storage.</span></span>

* <span data-ttu-id="aa221-145">資料行存放區索引可支援經分割的資料表。</span><span class="sxs-lookup"><span data-stu-id="aa221-145">Columnstore indexes support partitioned tables.</span></span> <span data-ttu-id="aa221-146">資料行存放區索引會使用經分割的資料表來管理和保存資料。</span><span class="sxs-lookup"><span data-stu-id="aa221-146">For columnstore indexes, partitioned tables are used for data management and archival.</span></span> <span data-ttu-id="aa221-147">對於逐列儲存的資料表而言，資料分割在查詢效能方面的角色較為吃重。</span><span class="sxs-lookup"><span data-stu-id="aa221-147">For tables stored row-by-row, partitions have a larger role in query performance.</span></span>  
* <span data-ttu-id="aa221-148">PolyBase 在管理資料方面扮演著重要角色。</span><span class="sxs-lookup"><span data-stu-id="aa221-148">PolyBase plays an important role in managing data.</span></span> <span data-ttu-id="aa221-149">使用 PolyBase，您就能選擇將較舊的資料封存至 Hadoop 或 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="aa221-149">Using PolyBase, you have the option to archive older data to Hadoop or Azure blob storage.</span></span>  <span data-ttu-id="aa221-150">由於資料還在線上，這樣便能提供許多可用選項。</span><span class="sxs-lookup"><span data-stu-id="aa221-150">This provides lots of options since the data is still online.</span></span>  <span data-ttu-id="aa221-151">從 Hadoop 擷取資料可能需要較長的時間，但以擷取時間換取儲存體成本，可能會得不償失。</span><span class="sxs-lookup"><span data-stu-id="aa221-151">It might take longer to retrieve data from Hadoop, but the tradeoff of retrieval time might outweigh the storage cost.</span></span>

### <a name="exporting-data"></a><span data-ttu-id="aa221-152">匯出資料</span><span class="sxs-lookup"><span data-stu-id="aa221-152">Exporting data</span></span>
<span data-ttu-id="aa221-153">將資料提供給報告和分析使用的方法，就是將資料從資料倉儲傳送到專門執行報告和分析的伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa221-153">One way to make data available for reports and analysis is to send data from the data warehouse to servers dedicated for running reports and analysis.</span></span> <span data-ttu-id="aa221-154">這些伺服器稱為資料市集。</span><span class="sxs-lookup"><span data-stu-id="aa221-154">These servers are called data marts.</span></span> <span data-ttu-id="aa221-155">例如，您可以預先處理報告資料，然後將它從資料倉儲匯出至各個國家的伺服器中，以提供分佈各地的客戶和分析師使用。</span><span class="sxs-lookup"><span data-stu-id="aa221-155">For example, you could pre-process report data and then export it from the data warehouse to many servers around the world, to make it broadly available for customers and analysts.</span></span>

* <span data-ttu-id="aa221-156">您可以在每天晚上，將每天的資料快照集填入唯讀報表伺服器，以便產生報告。</span><span class="sxs-lookup"><span data-stu-id="aa221-156">For generating reports, each night you could populate read-only reporting servers with a snapshot of the daily data.</span></span> <span data-ttu-id="aa221-157">這樣可為客戶提供較高的頻寬，同時降低資料倉儲的計算資源需求。</span><span class="sxs-lookup"><span data-stu-id="aa221-157">This gives higher bandwidth for customers while lowering the compute resource needs on the data warehouse.</span></span> <span data-ttu-id="aa221-158">從安全性的角度來說，資料市集可減少存取資料倉儲的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="aa221-158">From a security aspect, data marts allow you to reduce the number of users who have access to the data warehouse.</span></span>
* <span data-ttu-id="aa221-159">如需進行分析，您可以在資料倉儲建立分析 Cube，然後針對資料倉儲執行分析，或是前置處理資料，然後再匯出到分析伺服器進行進一步分析。</span><span class="sxs-lookup"><span data-stu-id="aa221-159">For analytics, you can either build an analysis cube on the data warehouse and run analysis against the data warehouse, or pre-process data and export it to the analysis server for further analytics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa221-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa221-160">Next steps</span></span>
<span data-ttu-id="aa221-161">現在您已稍微了解 SQL 資料倉儲，請了解如何快速[建立 SQL 資料倉儲][create a SQL Data Warehouse]和[載入範例資料][load sample data]。</span><span class="sxs-lookup"><span data-stu-id="aa221-161">Now that you know a bit about SQL Data Warehouse, learn how to quickly [create a SQL Data Warehouse][create a SQL Data Warehouse] and [load sample data][load sample data].</span></span>

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
