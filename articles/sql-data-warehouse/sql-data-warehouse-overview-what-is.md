---
title: "什麼是 Azure SQL 資料倉儲？ | Microsoft Docs"
description: "企業級分散式資料庫，可處理資料量高達 PB 的關聯式與非關聯式資料。 它是業界首見能在幾秒內增加、縮減和暫停的雲端資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 575c49f83c8845edcea984459f3907490c62d269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a><span data-ttu-id="ffbc2-105">什麼是 Azure SQL 資料倉儲？</span><span class="sxs-lookup"><span data-stu-id="ffbc2-105">What is Azure SQL Data Warehouse?</span></span>
<span data-ttu-id="ffbc2-106">Azure SQL 資料倉儲是一種巨量平行處理 (MPP) 以雲端為基礎、相應放大的關聯式資料庫，可處理大量的資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-106">Azure SQL Data Warehouse is a massively parallel processing (MPP) cloud-based, scale-out, relational database capable of processing massive volumes of data.</span></span> 

<span data-ttu-id="ffbc2-107">SQL 資料倉儲：</span><span class="sxs-lookup"><span data-stu-id="ffbc2-107">SQL Data Warehouse:</span></span>

* <span data-ttu-id="ffbc2-108">結合 SQL Server 關聯式資料庫與 Azure 雲端相應放大功能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-108">Combines the SQL Server relational database with Azure cloud scale-out capabilities.</span></span> 
* <span data-ttu-id="ffbc2-109">從計算減少儲存體。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-109">Decouples storage from compute.</span></span>
* <span data-ttu-id="ffbc2-110">啟用增加、減少、暫停或繼續計算。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-110">Enables increasing, decreasing, pausing, or resuming compute.</span></span> 
* <span data-ttu-id="ffbc2-111">跨 Azure 平台間整合。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-111">Integrates across the Azure platform.</span></span>
* <span data-ttu-id="ffbc2-112">利用 SQL Server Transact-SQL (T-SQL) 和工具。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-112">Utilizes SQL Server Transact-SQL (T-SQL) and tools.</span></span>
* <span data-ttu-id="ffbc2-113">遵守各種法律和商務安全性需求，例如 SOC 和 ISO。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-113">Complies with various legal and business security requirements such as SOC and ISO.</span></span>

<span data-ttu-id="ffbc2-114">本文說明 SQL 資料倉儲的重要功能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-114">This article describes the key features of SQL Data Warehouse.</span></span>

## <a name="massively-parallel-processing-architecture"></a><span data-ttu-id="ffbc2-115">巨量平行處理架構</span><span class="sxs-lookup"><span data-stu-id="ffbc2-115">Massively parallel processing architecture</span></span>
<span data-ttu-id="ffbc2-116">SQL 資料倉儲是大量平行處理 (MPP) 分散式資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-116">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span> <span data-ttu-id="ffbc2-117">在幕後，SQL 資料倉儲會將您的資料分散於多個不共用的儲存和處理單元。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-117">Behind the scenes, SQL Data Warehouse spreads your data across many shared-nothing storage and processing units.</span></span> <span data-ttu-id="ffbc2-118">資料會儲存在進階本地備援儲存體層級，在其頂端動態連結的計算節點會執行查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-118">The data is stored in a Premium locally redundant storage layer on top of which dynamically linked Compute nodes execute queries.</span></span> <span data-ttu-id="ffbc2-119">SQL 資料倉儲可以採用「分治法」來執行載入和複雜的查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-119">SQL Data Warehouse takes a "divide and conquer" approach to running loads and complex queries.</span></span> <span data-ttu-id="ffbc2-120">要求是由控制節點接收、針對分佈最佳化，然後傳遞至計算節點來平行執行其工作。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-120">Requests are received by a Control node, optimized for distribution, and then passed to Compute nodes to do their work in parallel.</span></span>

<span data-ttu-id="ffbc2-121">使用減少的儲存體和計算，SQL 資料倉儲可以︰</span><span class="sxs-lookup"><span data-stu-id="ffbc2-121">With decoupled storage and compute, SQL Data Warehouse can:</span></span>

* <span data-ttu-id="ffbc2-122">擴大或縮小獨立計算的儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-122">Grow or shrink storage size independent of compute.</span></span>
* <span data-ttu-id="ffbc2-123">擴大或縮小計算能力，而不移動資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-123">Grow or shrink compute power without moving data.</span></span>
* <span data-ttu-id="ffbc2-124">暫停計算容量，同時讓資料保持不變，只需要支付儲存體的費用。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-124">Pause compute capacity while leaving data intact, only paying for storage.</span></span>
* <span data-ttu-id="ffbc2-125">在營運時間期間繼續計算容量。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-125">Resume compute capacity during operational hours.</span></span>

<span data-ttu-id="ffbc2-126">下圖更詳細說明此架構。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-126">The following diagram shows the architecture in more detail.</span></span>

![SQL 資料倉儲架構][1]

<span data-ttu-id="ffbc2-128">**控制節點︰** 控制節點會管理及最佳化查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-128">**Control node:** The Control node manages and optimizes queries.</span></span> <span data-ttu-id="ffbc2-129">它是與所有應用程式與連接互動的前端。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-129">It is the front end that interacts with all applications and connections.</span></span> <span data-ttu-id="ffbc2-130">在 SQL 資料倉儲中，控制節點採用 SQL Database 計算，而且連接它時的外觀及操作方式相同。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-130">In SQL Data Warehouse, the Control node is powered by SQL Database, and connecting to it looks and feels the same.</span></span> <span data-ttu-id="ffbc2-131">控制節點會暗中協調對分散式資料執行平行查詢所需的所有資料移動和計算。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-131">Under the surface, the Control node coordinates all the data movement and computation required to run parallel queries on your distributed data.</span></span> <span data-ttu-id="ffbc2-132">當您將 TSQL 查詢提交到 SQL 資料倉儲時，控制節點會將其轉換為會在每個計算節點上平行執行的個別查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-132">When you submit a T-SQL query to SQL Data Warehouse, the Control node transforms it into separate queries that run on each Compute node in parallel.</span></span>

<span data-ttu-id="ffbc2-133">**計算節點︰** 計算節點是 SQL 資料倉儲背後的動力。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-133">**Compute nodes:** The Compute nodes serve as the power behind SQL Data Warehouse.</span></span> <span data-ttu-id="ffbc2-134">它們是儲存資料和處理查詢的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-134">They are SQL Databases that store your data and process your query.</span></span> <span data-ttu-id="ffbc2-135">當您新增資料時，SQL 資料倉儲會將資料列分散到各個計算節點。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-135">When you add data, SQL Data Warehouse distributes the rows to your Compute nodes.</span></span> <span data-ttu-id="ffbc2-136">計算節點是會對您的資料執行平行查詢的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-136">The Compute nodes are the workers that run the parallel queries on your data.</span></span> <span data-ttu-id="ffbc2-137">經過處理後，它們會將結果傳回控制節點。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-137">After processing, they pass the results back to the Control node.</span></span> <span data-ttu-id="ffbc2-138">為了完成查詢，控制節點會彙總結果並傳回最終的結果。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-138">To finish the query, the Control node aggregates the results and returns the final result.</span></span>

<span data-ttu-id="ffbc2-139">**儲存體：** 您的資料會儲存在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-139">**Storage:** Your data is stored in Azure Blob storage.</span></span> <span data-ttu-id="ffbc2-140">當計算節點與您的資料互動時，它們會直接從 Blob 儲存體來回寫入和讀取。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-140">When Compute nodes interact with your data, they write and read directly to and from blob storage.</span></span> <span data-ttu-id="ffbc2-141">由於 Azure 儲存體可大幅地明確擴充，SQL 資料倉儲同樣也可以。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-141">Since Azure storage expands transparently and vastly, SQL Data Warehouse can do the same.</span></span> <span data-ttu-id="ffbc2-142">計算和儲存體各自獨立，所以 SQL 資料倉儲可以自動調整儲存體，與計算分開調整，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-142">Since compute and storage are independent, SQL Data Warehouse can automatically scale storage separately from scaling compute, and vice-versa.</span></span> <span data-ttu-id="ffbc2-143">Azure Blob 儲存體也是完全容錯，並可簡化備份和還原程序。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-143">Azure Blob storage is also fully fault tolerant, and streamlines the backup and restore process.</span></span>

<span data-ttu-id="ffbc2-144">**資料移動服務︰** 資料移動服務 (DMS) 可在節點之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-144">**Data Movement Service:** Data Movement Service (DMS) moves data between the nodes.</span></span> <span data-ttu-id="ffbc2-145">DMS 可讓計算節點存取聯結和彙總所需的資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-145">DMS gives the Compute nodes access to data they need for joins and aggregations.</span></span> <span data-ttu-id="ffbc2-146">DMS 不是 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-146">DMS is not an Azure service.</span></span> <span data-ttu-id="ffbc2-147">它是一項在所有節點上與 SQL Database 並排執行的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-147">It is a Windows service that runs alongside SQL Database on all the nodes.</span></span> <span data-ttu-id="ffbc2-148">DMS 是背景處理序，無法直接互動。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-148">DMS is a background process that cannot be interacted with directly.</span></span> <span data-ttu-id="ffbc2-149">不過，您可以查閱查詢計劃以查看 DMS 作業的發生時機，因為資料移動必須平行執行每項查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-149">However, you can look at query plans to see when DMS operations occur, since data movement is necessary to run each query in parallel.</span></span>

## <a name="optimized-for-data-warehouse-workloads"></a><span data-ttu-id="ffbc2-150">已針對資料倉儲工作負載最佳化</span><span class="sxs-lookup"><span data-stu-id="ffbc2-150">Optimized for data warehouse workloads</span></span>
<span data-ttu-id="ffbc2-151">MPP 方法由許多資料倉儲特定效能最佳化輔助，包括：</span><span class="sxs-lookup"><span data-stu-id="ffbc2-151">The MPP approach is aided by several data warehousing specific performance optimizations, including:</span></span>

* <span data-ttu-id="ffbc2-152">一項分散式查詢最佳化工具和一組複雜的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-152">A distributed query optimizer and set of complex statistics across all data.</span></span> <span data-ttu-id="ffbc2-153">使用資料大小和散發的資訊，服務就能夠藉由評估特定分散式查詢作業的成本來最佳化查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-153">Using information on data size and distribution, the service is able to optimize queries by assessing the cost of specific distributed query operations.</span></span>
* <span data-ttu-id="ffbc2-154">整合到資料移動程序中的進階演算法和技術，能夠視需要在計算資源之間有效率地移動資料以執行查詢。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-154">Advanced algorithms and techniques integrated into the data movement process to efficiently move data among computing resources as necessary to perform the query.</span></span> <span data-ttu-id="ffbc2-155">這些資料移動作業均為內建，且資料移動服務的所有最佳化都會自動進行。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-155">These data movement operations are built in, and all optimizations to the Data Movement Service happen automatically.</span></span>
* <span data-ttu-id="ffbc2-156">預設的叢集 **資料行存放** 區索引。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-156">Clustered **columnstore** indexes by default.</span></span> <span data-ttu-id="ffbc2-157">與傳統的資料列導向儲存體相比，使用資料行儲存體的 SQL 資料倉儲最多可讓壓縮平均提升 5 倍，查詢效能提升 10 倍以上。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-157">By using column-based storage, SQL Data Warehouse gets on average 5x compression gains over traditional row-oriented storage, and up to 10x or more query performance gains.</span></span> <span data-ttu-id="ffbc2-158">需要掃描大量資料列的分析查詢更適合使用資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-158">Analytics queries that need to scan a large number of rows work better with columnstore indexes.</span></span>


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a><span data-ttu-id="ffbc2-159">可預測且可調整的效能與資料倉儲單位</span><span class="sxs-lookup"><span data-stu-id="ffbc2-159">Predictable and scalable performance With Data Warehouse Units</span></span>
<span data-ttu-id="ffbc2-160">SQL 資料倉儲是使用與 SQL Database 類似的技術建置，表示使用者對於分析查詢可以預期一致且可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-160">SQL Data Warehouse is built with similar technologies as SQL Database, which means that users can expect consistent and predictable performance for analytical queries.</span></span> <span data-ttu-id="ffbc2-161">當使用者新增或減去計算節點時，他們應該會看到以線性方式調整的效能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-161">Users should expect to see performance scale linearly as they add or subtract Compute nodes.</span></span> <span data-ttu-id="ffbc2-162">SQL 資料倉儲的資源配置是使用資料倉儲單位 (DWU) 測量。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-162">Allocation of resources to your SQL Data Warehouse is measured in Data Warehouse Units (DWUs).</span></span> <span data-ttu-id="ffbc2-163">DWU 是配置給 SQL 資料倉儲的基礎資源 (例如 CPU、記憶體、IOPS) 的量值。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-163">DWUs are a measure of underlying resources like CPU, memory, IOPS, which are allocated to your SQL Data Warehouse.</span></span> <span data-ttu-id="ffbc2-164">增加 DWU 數目可增加資源和效能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-164">Increasing the number of DWUs increases resources and performance.</span></span> <span data-ttu-id="ffbc2-165">具體而言，DWU 有助於確保：</span><span class="sxs-lookup"><span data-stu-id="ffbc2-165">Specifically, DWUs help ensure that:</span></span>

* <span data-ttu-id="ffbc2-166">您可以調整您的資料倉儲，而不必擔心基礎硬體或軟體。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-166">You are able to scale your data warehouse without worrying about the underlying hardware or software.</span></span>
* <span data-ttu-id="ffbc2-167">您可以在變更資料倉儲的計算之前，預測 DWU 層級的效能改進程度。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-167">You can predict performance improvement for a DWU level before changing the compute of your data warehouse.</span></span>
* <span data-ttu-id="ffbc2-168">可以變更或移動您的執行個體的基礎硬體與軟體，而不會影響工作負載效能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-168">The underlying hardware and software of your instance can change or move without affecting your workload performance.</span></span>
* <span data-ttu-id="ffbc2-169">Microsoft 可以改善服務的基礎架構，而不會影響工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-169">Microsoft can improve the underlying architecture of the service without affecting the performance of your workload.</span></span>
* <span data-ttu-id="ffbc2-170">Microsoft 可以快速提升 SQL 資料倉儲的效能，以可調整及平均影響系統的方式執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-170">Microsoft can rapidly improve performance in SQL Data Warehouse, in a way that is scalable and evenly effects the system.</span></span>

<span data-ttu-id="ffbc2-171">資料倉儲單位會提供包含三個度量的量值，而這些度量與資料倉儲工作負載效能高度相互關聯。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-171">Data Warehouse Units provide a measure of three metrics that are highly correlated with data warehousing workload performance.</span></span> <span data-ttu-id="ffbc2-172">下列主要工作負載度量以線性方式調整 DWU。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-172">The following key workload metrics scale linearly with the DWUs.</span></span>

<span data-ttu-id="ffbc2-173">**掃描/彙總**：標準資料倉儲查詢，該查詢會掃描大量資料列，然後執行複雜的彙總。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-173">**Scan/Aggregation:** A standard data warehousing query that scans a large number of rows and then performs a complex aggregation.</span></span> <span data-ttu-id="ffbc2-174">這是 I/O 和 CPU 密集作業。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-174">This is an I/O and CPU intensive operation.</span></span>

<span data-ttu-id="ffbc2-175">**負載**將資料擷取至服務的能力。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-175">**Load:** The ability to ingest data into the service.</span></span> <span data-ttu-id="ffbc2-176">使用來自 Azure 儲存體 Blob 或 Azure Data Lake 的 PolyBase 時的負載效能最佳。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-176">Loads are best performed with PolyBase from Azure Storage Blobs or Azure Data Lake.</span></span> <span data-ttu-id="ffbc2-177">這項度量是設計來對服務的網路和 CPU 層面給予壓力。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-177">This metric is designed to stress network and CPU aspects of the service.</span></span>

<span data-ttu-id="ffbc2-178">**Create Table As Select (CTAS)** ：CTAS 會測量複製資料表的能力。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-178">**Create Table As Select (CTAS):** CTAS measures the ability to copy a table.</span></span> <span data-ttu-id="ffbc2-179">這牽涉到從儲存體讀取資料、跨應用裝置的節點散發，以及重新寫入至儲存體。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-179">This involves reading data from storage, distributing it across the nodes of the appliance and writing to storage again.</span></span> <span data-ttu-id="ffbc2-180">這是 CPU、IO 和網路密集作業。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-180">It is a CPU, IO, and network intensive operation.</span></span>

## <a name="built-on-sql-server"></a><span data-ttu-id="ffbc2-181">建置在 SQL Server 上</span><span class="sxs-lookup"><span data-stu-id="ffbc2-181">Built on SQL Server</span></span>
<span data-ttu-id="ffbc2-182">SQL 資料倉儲以 SQL Server 關聯式資料庫引擎為基礎，且包含企業資料倉儲的許多功能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-182">SQL Data Warehouse is based on the SQL Server relational database engine, and includes many of the features you expect from an enterprise data warehouse.</span></span> <span data-ttu-id="ffbc2-183">如果您已經熟悉 T-SQL，則可輕鬆地將您的知識傳輸到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-183">If you already know T-SQL, it's easy to transfer your knowledge to SQL Data Warehouse.</span></span> <span data-ttu-id="ffbc2-184">無論您是進階或新手使用者，文件範例都能夠協助您開始著手。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-184">Whether you are advanced or just getting started, the examples across the documentation will help begin.</span></span> <span data-ttu-id="ffbc2-185">整體來說，您可以考慮我們建構 SQL 資料倉儲的語言元素的方式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ffbc2-185">Overall, you can think about the way that we've constructed the language elements of SQL Data Warehouse as follows:</span></span>

* <span data-ttu-id="ffbc2-186">SQL 資料倉儲會將 T-SQL 語法用於許多作業。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-186">SQL Data Warehouse uses T-SQL syntax for many operations.</span></span> <span data-ttu-id="ffbc2-187">並且支援一組廣泛的傳統 SQL 建構，例如預存程序、使用者定義函式、資料表資料分割、索引和定序。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-187">It also supports a broad set of traditional SQL constructs, such as stored procedures, user-defined functions, table partitioning, indexes, and collations.</span></span>
* <span data-ttu-id="ffbc2-188">SQL 資料倉儲也包含各種較新的 SQL Server 功能，包括叢集**資料行存放區**索引、PolyBase 整合和資料稽核 (完整的威脅評估)。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-188">SQL Data Warehouse also contains various newer SQL Server features, including: clustered **columnstore** indexes, PolyBase integration, and data auditing (complete with threat assessment).</span></span>
* <span data-ttu-id="ffbc2-189">較不常用於資料倉儲工作負載或是比 SQL Server 還新的特定 TSQL 語言元素目前可能無法使用。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-189">Certain T-SQL language elements that are less common for data warehousing workloads, or are newer to SQL Server, may not be currently available.</span></span> <span data-ttu-id="ffbc2-190">如需詳細資訊，請參閱[移轉文件][Migration documentation]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-190">For more information, see the [Migration documentation][Migration documentation].</span></span>

<span data-ttu-id="ffbc2-191">透過 SQL Server、SQL 資料倉儲、SQL Database 和「分析平台系統」之間的 Transact-SQL 與功能共通性，您能夠開發符合您資料需求的解決方案。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-191">With the Transact-SQL and feature commonality between SQL Server, SQL Data Warehouse, SQL Database, and Analytics Platform System, you can develop a solution that fits your data needs.</span></span> <span data-ttu-id="ffbc2-192">您可以根據效能、安全性和調整需求，決定儲存資料的位置，然後視需要在不同系統之間傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-192">You can decide where to keep your data, based on performance, security, and scale requirements, and then transfer data as necessary between different systems.</span></span>

## <a name="data-protection"></a><span data-ttu-id="ffbc2-193">資料保護</span><span class="sxs-lookup"><span data-stu-id="ffbc2-193">Data protection</span></span>
<span data-ttu-id="ffbc2-194">SQL 資料倉儲會將所有資料儲存在 Azure Premium 本地備援儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-194">SQL Data Warehouse stores all data in Azure Premium locally redundant storage.</span></span> <span data-ttu-id="ffbc2-195">並在當地資料中心維護多份資料的同步複本，確保當地語系化失敗時能夠提供透明的資料保護。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-195">Multiple synchronous copies of the data are maintained in the local data center to guarantee transparent data protection against localized failures.</span></span> <span data-ttu-id="ffbc2-196">此外，SQL 資料倉儲會使用 Azure 儲存體快照集，定期自動備份作用中 (未暫停) 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-196">In addition, SQL Data Warehouse automatically backs up your active (unpaused) databases at regular intervals using Azure Storage Snapshots.</span></span> <span data-ttu-id="ffbc2-197">若要深入了解備份和還原的運作方式，請參閱[備份與還原概觀][Backup and restore overview]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-197">To learn more about how backup and restore works, see the [Backup and restore overview][Backup and restore overview].</span></span>

## <a name="integrated-with-microsoft-tools"></a><span data-ttu-id="ffbc2-198">與 Microsoft 工具整合</span><span class="sxs-lookup"><span data-stu-id="ffbc2-198">Integrated with Microsoft tools</span></span>
<span data-ttu-id="ffbc2-199">SQL 資料倉儲也整合了許多 SQL Server 使用者可能很熟悉的工具。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-199">SQL Data Warehouse also integrates many of the tools that SQL Server users may be familiar with.</span></span> <span data-ttu-id="ffbc2-200">這些工具包括：</span><span class="sxs-lookup"><span data-stu-id="ffbc2-200">These tools include:</span></span>

<span data-ttu-id="ffbc2-201">**傳統的 SQL Server 工具** ：SQL 資料倉儲會與 SQL Server Analysis Services、Integration Services 和 Reporting Services 完整整合。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-201">**Traditional SQL Server tools:** SQL Data Warehouse is fully integrated with SQL Server Analysis Services, Integration Services, and Reporting Services.</span></span>

<span data-ttu-id="ffbc2-202">**以雲端為基礎的工具**：SQL 資料倉儲可以與 Azure 中的各種服務整合，包括 Data Factory、串流分析、機器學習服務和 Power BI。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-202">**Cloud-based tools:** SQL Data Warehouse can be integarated with various services in Azure, including Data Factory, Stream Analytics, Machine Learning, and Power BI.</span></span> <span data-ttu-id="ffbc2-203">如需更完整的清單，請參閱[整合式工具概觀][Integrated tools overview]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-203">For a more complete list, see [Integrated tools overview][Integrated tools overview].</span></span>

<span data-ttu-id="ffbc2-204">**協力廠商工具**：許多協力廠商工具提供者與 SQL 資料倉儲整合的工具都已經過認證。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-204">**Third-party tools:** Many third-party tool providers have certified integration of their tools with SQL Data Warehouse.</span></span> <span data-ttu-id="ffbc2-205">如需完整清單，請參閱 [SQL 資料倉儲解決方案合作夥伴][SQL Data Warehouse solution partners]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-205">For a full list, see [SQL Data Warehouse solution partners][SQL Data Warehouse solution partners].</span></span>

## <a name="hybrid-data-sources-scenarios"></a><span data-ttu-id="ffbc2-206">混合式資料來源案例</span><span class="sxs-lookup"><span data-stu-id="ffbc2-206">Hybrid data sources scenarios</span></span>
<span data-ttu-id="ffbc2-207">Polybase 可讓您透過使用熟悉的 T-SQL 命令來運用不同來源的資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-207">Polybase allows you to leverage your data from different sources by using familiar T-SQL commands.</span></span> <span data-ttu-id="ffbc2-208">Polybase 讓查詢 Azure Blob 儲存體中的非關聯式資料就像查詢一般資料表般容易。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-208">Polybase enables you to query non-relational data held in Azure Blob storage as though it is a regular table.</span></span> <span data-ttu-id="ffbc2-209">使用 Polybase 即可查詢非關聯式資料，或將非關聯式資料匯入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-209">Use Polybase to query non-relational data, or to import non-relational data into SQL Data Warehouse.</span></span>

* <span data-ttu-id="ffbc2-210">PolyBase 使用外部資料表存取非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-210">PolyBase uses external tables to access non-relational data.</span></span> <span data-ttu-id="ffbc2-211">資料表定義會儲存在 SQL 資料倉儲中，您可以像存取一般關聯式資料一樣，使用 SQL 和工具進行存取。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-211">The table definitions are stored in SQL Data Warehouse, and you can access them by using SQL and tools like you would access normal relational data.</span></span>
* <span data-ttu-id="ffbc2-212">在其整合中無從得知 Polybase。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-212">Polybase is agnostic in its integration.</span></span> <span data-ttu-id="ffbc2-213">它會為其支援的所有來源提供相同的功能。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-213">It exposes the same features and functionality to all the sources that it supports.</span></span> <span data-ttu-id="ffbc2-214">Polybase 可讀取各種格式的資料，包括分隔檔案或 ORC 檔案。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-214">The data read by Polybase can be in various formats, including delimited files or ORC files.</span></span>
* <span data-ttu-id="ffbc2-215">PolyBase 可用來存取 Blob 儲存體，該儲存體也用來做為 HDInsight 叢集的儲存體。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-215">PolyBase can be used to access blob storage that is also being used as storage for an HDInsight cluster.</span></span> <span data-ttu-id="ffbc2-216">這可讓您使用關聯式與非關聯式工具，以最新的方式存取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-216">This gives you access to the same data with relational and non-relational tools.</span></span>

## <a name="sla"></a><span data-ttu-id="ffbc2-217">SLA</span><span class="sxs-lookup"><span data-stu-id="ffbc2-217">SLA</span></span>
<span data-ttu-id="ffbc2-218">SQL 資料倉儲提供產品層級的服務等級協定 (SLA) 做為 Microsoft Online Services SLA 的一部分。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-218">SQL Data Warehouse offers a product level service level agreement (SLA) as part of Microsoft Online Services SLA.</span></span> <span data-ttu-id="ffbc2-219">如需詳細資訊，請參閱 [SQL 資料倉儲的 SLA][SLA for SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-219">For more information, visit [SLA for SQL Data Warehouse][SLA for SQL Data Warehouse].</span></span> <span data-ttu-id="ffbc2-220">如需關於所有其他產品的 SLA 資訊，您可以造訪[服務等級協定] Azure 頁面，或在[大量授權][Volume Licensing]頁面上下載。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-220">For SLA information about all other products you can visit the [Service Level Agreements] Azure page or download them on the [Volume Licensing][Volume Licensing] page.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ffbc2-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ffbc2-221">Next steps</span></span>
<span data-ttu-id="ffbc2-222">現在您已稍微了解 SQL 資料倉儲，請了解如何快速[建立 SQL 資料倉儲][create a SQL Data Warehouse]和[載入範例資料][load sample data]。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-222">Now that you know a bit about SQL Data Warehouse, learn how to quickly [create a SQL Data Warehouse][create a SQL Data Warehouse] and [load sample data][load sample data].</span></span> <span data-ttu-id="ffbc2-223">如果您不熟悉 Azure，您可能會發現 [Azure 詞彙][Azure glossary]在您遇到新術語時很有幫助。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-223">If you are new to Azure, you may find the [Azure glossary][Azure glossary] helpful as you encounter new terminology.</span></span> <span data-ttu-id="ffbc2-224">或者，也可以看一下其中一些其他 SQL 資料倉儲資源。</span><span class="sxs-lookup"><span data-stu-id="ffbc2-224">Or look at some of these other SQL Data Warehouse Resources.</span></span>  

* <span data-ttu-id="ffbc2-225">[客戶成功案例]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-225">[Customer success stories]</span></span>
* <span data-ttu-id="ffbc2-226">[部落格]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-226">[Blogs]</span></span>
* <span data-ttu-id="ffbc2-227">[功能要求]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-227">[Feature requests]</span></span>
* <span data-ttu-id="ffbc2-228">[影片]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-228">[Videos]</span></span>
* <span data-ttu-id="ffbc2-229">[客戶諮詢小組部落格]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-229">[Customer Advisory Team blogs]</span></span>
* <span data-ttu-id="ffbc2-230">[建立支援票證]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-230">[Create support ticket]</span></span>
* <span data-ttu-id="ffbc2-231">[MSDN 論壇]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-231">[MSDN forum]</span></span>
* <span data-ttu-id="ffbc2-232">[Stack Overflow 論壇]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-232">[Stack Overflow forum]</span></span>
* <span data-ttu-id="ffbc2-233">[Twitter]</span><span class="sxs-lookup"><span data-stu-id="ffbc2-233">[Twitter]</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
<span data-ttu-id="ffbc2-234">[建立支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="ffbc2-234">[Create support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
<span data-ttu-id="ffbc2-235">[客戶成功案例]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="ffbc2-235">[Customer success stories]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse</span></span>
<span data-ttu-id="ffbc2-236">[部落格]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/</span><span class="sxs-lookup"><span data-stu-id="ffbc2-236">[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/</span></span>
<span data-ttu-id="ffbc2-237">[客戶諮詢小組部落格]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/</span><span class="sxs-lookup"><span data-stu-id="ffbc2-237">[Customer Advisory Team blogs]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/</span></span>
<span data-ttu-id="ffbc2-238">[功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="ffbc2-238">[Feature requests]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="ffbc2-239">[MSDN 論壇]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse</span><span class="sxs-lookup"><span data-stu-id="ffbc2-239">[MSDN forum]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse</span></span>
<span data-ttu-id="ffbc2-240">[Stack Overflow 論壇]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="ffbc2-240">[Stack Overflow forum]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="ffbc2-241">[Twitter]: https://twitter.com/hashtag/SQLDW</span><span class="sxs-lookup"><span data-stu-id="ffbc2-241">[Twitter]: https://twitter.com/hashtag/SQLDW</span></span>
<span data-ttu-id="ffbc2-242">[影片]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="ffbc2-242">[Videos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse</span></span>
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
<span data-ttu-id="ffbc2-243">[服務等級協定]: https://azure.microsoft.com/en-us/support/legal/sla/</span><span class="sxs-lookup"><span data-stu-id="ffbc2-243">[Service Level Agreements]: https://azure.microsoft.com/en-us/support/legal/sla/</span></span>