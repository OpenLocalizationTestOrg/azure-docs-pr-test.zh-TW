---
title: "Azure SQL Database 記憶體內部技術 | Microsoft Docs"
description: "SQL Database 記憶體內部技術大幅提升交易和分析工作負載的效能。 了解如何利用這些技術。"
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="240b5-104">使用 SQL Database 中的記憶體內部技術將效能最佳化</span><span class="sxs-lookup"><span data-stu-id="240b5-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="240b5-105">您可以使用 Azure SQL Database 中的記憶體內部技術，以改善各種工作負載的效能︰交易式 (線上交易處理 (OLTP))、分析 (線上分析處理 (OLAP)) 及混合 (混合式交易/分析處理 (HTAP))。</span><span class="sxs-lookup"><span data-stu-id="240b5-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="240b5-106">因為可讓查詢和交易處理變得更有效率，記憶體內部技術也有助於降低成本。</span><span class="sxs-lookup"><span data-stu-id="240b5-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="240b5-107">您通常不需要升級資料庫的定價層，就能提升效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="240b5-108">在某些情況下，您甚至可以降低定價層，而仍然發現記憶體內部技術可以提升效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="240b5-109">以下是記憶體內部 OLTP 如何幫助大幅提升效能的兩個範例︰</span><span class="sxs-lookup"><span data-stu-id="240b5-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="240b5-110">由於使用記憶體內部 OLTP，[Quorum Business Solutions 能使其工作負載倍增，同時將 DTU 提高 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="240b5-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="240b5-111">DTU 表示「資料庫輸送量單位」，其中包含對資源耗用的測量。</span><span class="sxs-lookup"><span data-stu-id="240b5-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="240b5-112">下列影片以範例工作負載示範資源耗用量的重大改進︰[Azure SQL Database 影片中的記憶體內部 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)。</span><span class="sxs-lookup"><span data-stu-id="240b5-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="240b5-113">如需詳細資訊，請參閱部落格文章︰[Azure SQL Database 中的記憶體 OLTP 部落格文章](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="240b5-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="240b5-114">記憶體內部技術適用於高階定價層的所有資料庫，包括高階彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="240b5-115">下列影片說明 Azure SQL Database 中的記憶體內部技術所可能提升的效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="240b5-116">請記住，能提升多少效能永遠取決於許多因素，包括工作負載和資料的性質、資料庫的存取模式等等。</span><span class="sxs-lookup"><span data-stu-id="240b5-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="240b5-117">Azure SQL Database 擁有下列記憶體內部技術︰</span><span class="sxs-lookup"><span data-stu-id="240b5-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="240b5-118">「記憶體內部 OLTP」可增加輸送量並減少交易處理的延遲。</span><span class="sxs-lookup"><span data-stu-id="240b5-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="240b5-119">受益於記憶體內部 OLTP 的案例包括︰高輸送量的交易處理 (例如股票交易和網路遊戲)、從事件或 IoT 裝置擷取資料、快取、資料載入，以及暫存資料表和資料表變數等案例。</span><span class="sxs-lookup"><span data-stu-id="240b5-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="240b5-120">「叢集資料行存放區索引」可減少儲存體使用量 (最多 10 倍)，並提升報告和分析查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="240b5-121">您可以將它用於資料超市中的事實資料表，在資料庫中容納更多資料並提升效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="240b5-122">另外，您還可以將它用於操作資料庫中的歷史資料，則可封存並查詢多達 10 倍以上的資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="240b5-123">「非叢集資料行存放區索引」 (適用於 HTAP) 可讓您透過直接查詢操作資料庫，即時深入了解您的業務，而不必執行昂貴的擷取、轉換和載入 (ETL) 程序並等候資料倉儲填入資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="240b5-124">非叢集資料行存放區索引可極為快速地對 OLTP 資料庫執行分析查詢，同時降低對操作工作負載的影響。</span><span class="sxs-lookup"><span data-stu-id="240b5-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="240b5-125">您也可以結合記憶體最佳化資料表與資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="240b5-126">結合它們可讓您執行非常快速的交易處理，並快速地*同時*對相同的資料執行分析查詢。</span><span class="sxs-lookup"><span data-stu-id="240b5-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="240b5-127">資料行存放區和記憶體內部 OLTP 已分別於 2012 年和 2014 年起納入成為 SQL Server 產品的一部分。</span><span class="sxs-lookup"><span data-stu-id="240b5-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="240b5-128">Azure SQL Database 和 SQL Server 共用相同的記憶體內部技術實作。</span><span class="sxs-lookup"><span data-stu-id="240b5-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="240b5-129">未來，這些技術的新功能會先在 Azure SQL Database 中推出，然後才在 SQL Server 中推出。</span><span class="sxs-lookup"><span data-stu-id="240b5-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="240b5-130">本主題從各個面向說明 Azure SQL Database 特有的記憶體內部 OLTP 和資料行存放區索引，還包含範例：</span><span class="sxs-lookup"><span data-stu-id="240b5-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="240b5-131">您將了解這些技術對儲存體和資料大小限制的影響。</span><span class="sxs-lookup"><span data-stu-id="240b5-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="240b5-132">您將了解如何管理在不同定價層之間移動採用這些技術的資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="240b5-133">您將看到兩個範例，其分別示範如何在 Azure SQL Database 中使用記憶體內部 OLTP 以及資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="240b5-134">如需詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="240b5-134">See the following resources for more information.</span></span>

<span data-ttu-id="240b5-135">有關這些技術的深入資訊：</span><span class="sxs-lookup"><span data-stu-id="240b5-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="240b5-136">[記憶體內部 OLTP 概觀和使用案例](https://msdn.microsoft.com/library/mt774593.aspx) (包括客戶案例研究參考和入門資訊)</span><span class="sxs-lookup"><span data-stu-id="240b5-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="240b5-137">記憶體內部 OLTP 的文件</span><span class="sxs-lookup"><span data-stu-id="240b5-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="240b5-138">資料行存放區索引指南</span><span class="sxs-lookup"><span data-stu-id="240b5-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="240b5-139">混合式交易/分析處理 (HTAP)，也稱為[即時作業分析](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="240b5-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="240b5-140">記憶體內部 OLTP 快速入門：[快速入門 1：獲得更快 T-SQL 效能的記憶體內部 OLTP 技術)](http://msdn.microsoft.com/library/mt694156.aspx) (另一篇協助您開始使用的文章)</span><span class="sxs-lookup"><span data-stu-id="240b5-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="240b5-141">技術的相關深入介紹影片︰</span><span class="sxs-lookup"><span data-stu-id="240b5-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="240b5-142">[Azure SQL Database 中的記憶體內部 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (包含效能優點的示範，以及自行重現這些結果的步驟)</span><span class="sxs-lookup"><span data-stu-id="240b5-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="240b5-143">記憶體內部 OLTP 影片︰其功能、使用時機和使用方式</span><span class="sxs-lookup"><span data-stu-id="240b5-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="240b5-144">資料行存放區索引：記憶體內部分析影片 (來源：Ignite 2016)</span><span class="sxs-lookup"><span data-stu-id="240b5-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="240b5-145">儲存體和資料大小</span><span class="sxs-lookup"><span data-stu-id="240b5-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="240b5-146">記憶體內部 OLTP 的資料大小和儲存體上限</span><span class="sxs-lookup"><span data-stu-id="240b5-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="240b5-147">記憶體內部 OLTP 包含記憶體最佳化資料表，以用來儲存使用者資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="240b5-148">這些資料表必須可容納於記憶體。</span><span class="sxs-lookup"><span data-stu-id="240b5-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="240b5-149">因為您是直接在 SQL Database 服務中管理記憶體，我們有使用者資料配額的概念。</span><span class="sxs-lookup"><span data-stu-id="240b5-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="240b5-150">這個概念稱為「記憶體內部 OLAP 儲存體」。</span><span class="sxs-lookup"><span data-stu-id="240b5-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="240b5-151">每個受支援的獨立資料庫定價層以及每個彈性集區定價層都包含一定數量的記憶體內部 OLTP 儲存體。</span><span class="sxs-lookup"><span data-stu-id="240b5-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="240b5-152">在撰寫本文時，每 125 個資料庫交易單位 (DTU) 或彈性資料庫交易單位 (eDTU)，您會取得 1 GB 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="240b5-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="240b5-153">[SQL Database 服務層](sql-database-service-tiers.md)一文提供一份官方清單，其中列出每個受支援獨立資料庫和彈性集區定價層可用的記憶體內部 OLTP 儲存體。</span><span class="sxs-lookup"><span data-stu-id="240b5-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="240b5-154">下列項目計入記憶體內部 OLTP 儲存體容量上限︰</span><span class="sxs-lookup"><span data-stu-id="240b5-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="240b5-155">記憶體最佳化資料表和資料表變數中的作用中使用者資料列。</span><span class="sxs-lookup"><span data-stu-id="240b5-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="240b5-156">請注意，舊資料列版本不計入上限。</span><span class="sxs-lookup"><span data-stu-id="240b5-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="240b5-157">記憶體最佳化資料表上的索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="240b5-158">ALTER TABLE 作業的作業負荷。</span><span class="sxs-lookup"><span data-stu-id="240b5-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="240b5-159">如果您達到上限，則會收到超出配額錯誤，並再也無法插入或更新資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="240b5-160">為避免此錯誤，您可以刪除資料或增加資料庫或集區的定價層。</span><span class="sxs-lookup"><span data-stu-id="240b5-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="240b5-161">如需監視記憶體內部 OLTP 儲存體使用量以及設定要在幾乎達到上限時發出警示的詳細資訊，請參閱[監視記憶體內部儲存體](sql-database-in-memory-oltp-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="240b5-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="240b5-162">關於彈性集區</span><span class="sxs-lookup"><span data-stu-id="240b5-162">About elastic pools</span></span>

<span data-ttu-id="240b5-163">使用彈性集區時，集區中的所有資料庫會共用記憶體內部 OLTP 儲存體。</span><span class="sxs-lookup"><span data-stu-id="240b5-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="240b5-164">因此，一個資料庫中的使用量可能會影響其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="240b5-165">對此，您可以採取以下兩個對策︰</span><span class="sxs-lookup"><span data-stu-id="240b5-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="240b5-166">將資料庫的最大 eDTU 設定為低於整個集區的 eDTU 計數。</span><span class="sxs-lookup"><span data-stu-id="240b5-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="240b5-167">此最大值會將集區中任何資料庫的記憶體內部 OLTP 儲存體使用量上限，限制為對應到 eDTU 計數的大小。</span><span class="sxs-lookup"><span data-stu-id="240b5-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="240b5-168">設定大於 0 的最小 eDTU。</span><span class="sxs-lookup"><span data-stu-id="240b5-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="240b5-169">此最小值可確保集區中的每個資料庫，都能擁有與所設定之最小 eDTU 相對應的可用記憶體內部 OLTP 儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="240b5-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="240b5-170">資料行存放區索引的資料大小和儲存體</span><span class="sxs-lookup"><span data-stu-id="240b5-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="240b5-171">資料行存放區索引不需要納入記憶體中。</span><span class="sxs-lookup"><span data-stu-id="240b5-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="240b5-172">因此，索引大小的唯一上限是整體資料庫大小上限，相關說明請參閱 [SQL Database 服務層](sql-database-service-tiers.md)一文。</span><span class="sxs-lookup"><span data-stu-id="240b5-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="240b5-173">當您使用叢集資料行存放區索引時，基底表格儲存體會使用單資料行式壓縮。</span><span class="sxs-lookup"><span data-stu-id="240b5-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="240b5-174">壓縮可大幅降低使用者資料的儲存體使用量，這表示您可以在資料庫中容納更多資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="240b5-175">若要再進一步壓縮，您可以使用[單資料行式封存壓縮](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)。</span><span class="sxs-lookup"><span data-stu-id="240b5-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="240b5-176">能達到多大壓縮量取決於資料性質，但 10 倍的壓縮並不罕見。</span><span class="sxs-lookup"><span data-stu-id="240b5-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="240b5-177">例如，如果您的資料庫大小上限是 1 TB，而且您使用資料行存放區達到 10 倍壓縮，您總共可以在資料庫中容納 10 TB 的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="240b5-178">當您使用非叢集資料行存放區索引時，基底資料表仍然會以傳統資料列存放區格式儲存。</span><span class="sxs-lookup"><span data-stu-id="240b5-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="240b5-179">因此，節省的儲存空間沒有像使用叢集資料行存放區索引時那樣大。</span><span class="sxs-lookup"><span data-stu-id="240b5-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="240b5-180">不過，如果您以單一資料行存放區索引來取代部分的傳統非叢集索引，整體來說仍可節省資料表的儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="240b5-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="240b5-181">在不同定價層之間移動使用記憶體內部技術的資料庫</span><span class="sxs-lookup"><span data-stu-id="240b5-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="240b5-182">當您升級到較高的定價層時 (例如從標準升級到進階)，絕不會有任何相容性問題或其他問題，</span><span class="sxs-lookup"><span data-stu-id="240b5-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="240b5-183">可用的功能和資源只會增加。</span><span class="sxs-lookup"><span data-stu-id="240b5-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="240b5-184">但是將定價層降級可能會對資料庫有負面影響。</span><span class="sxs-lookup"><span data-stu-id="240b5-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="240b5-185">當您的資料庫包含記憶體內部 OLTP 物件時，從進階降級到標準或基本會有特別顯著的影響。</span><span class="sxs-lookup"><span data-stu-id="240b5-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="240b5-186">降級之後將無法使用記憶體最佳化資料表和資料行存放區索引 (即使它們依然可見)。</span><span class="sxs-lookup"><span data-stu-id="240b5-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="240b5-187">同樣的考量也適用於降低彈性集區的定價層時，或將使用記憶體內部技術的資料庫移至標準或基本的彈性集區時。</span><span class="sxs-lookup"><span data-stu-id="240b5-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="240b5-188">記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="240b5-188">In-Memory OLTP</span></span>

<span data-ttu-id="240b5-189">降級至基本/標準：標準層或基本層的資料庫不支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="240b5-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="240b5-190">此外，也不可以將具有任何記憶體內部 OLTP 物件的資料庫移至標準層或基本層。</span><span class="sxs-lookup"><span data-stu-id="240b5-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="240b5-191">在將資料庫降級至標準層或基本層時，請移除所有記憶體最佳化資料表和資料表類型，以及所有原生編譯的 T-SQL 模組。</span><span class="sxs-lookup"><span data-stu-id="240b5-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="240b5-192">您可以透過程式設計的方式，來了解給定資料庫是否支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="240b5-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="240b5-193">您可以執行下列 Transact-SQL 查詢︰</span><span class="sxs-lookup"><span data-stu-id="240b5-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="240b5-194">如果查詢傳回 **1**，則此資料庫支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="240b5-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="240b5-195">降級至較低的進階層：記憶體最佳化資料表中的資料必須能夠容納於與資料庫定價層相關聯 (或彈性集區中可用) 的記憶體內部 OLTP 儲存體。</span><span class="sxs-lookup"><span data-stu-id="240b5-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="240b5-196">如果您嘗試降低定價層，或將資料庫移入沒有足夠之可用記憶體內部 OLTP 儲存體的集區內，則作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="240b5-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="240b5-197">資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="240b5-197">Columnstore indexes</span></span>

<span data-ttu-id="240b5-198">*降級為基本或標準*：只有在進階定價層才支援資料行存放區索引，標準或基本層則不支援。</span><span class="sxs-lookup"><span data-stu-id="240b5-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="240b5-199">當您將資料庫降級至標準或基本時，資料行存放區索引將變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="240b5-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="240b5-200">系統會維持您的資料行存放區索引，但它不會再利用索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="240b5-201">如果您之後再升級為進階，系統會立即重新利用您的資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="240b5-202">如果您有「叢集」資料行存放區索引，則降級層之後整個資料表會變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="240b5-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="240b5-203">因此我們建議您在將資料庫降級至進階以下的層之前，先捨棄所有「叢集」資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="240b5-204">*降級至較低的進階層*：只要整個資料庫大小小於目標定價層的最大資料庫大小，或小於彈性集區中可用儲存體的大小，此降級就會成功。</span><span class="sxs-lookup"><span data-stu-id="240b5-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="240b5-205">資料行存放區索引不會產生任何特定影響。</span><span class="sxs-lookup"><span data-stu-id="240b5-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="240b5-206">1.安裝記憶體內部 OLTP 範例</span><span class="sxs-lookup"><span data-stu-id="240b5-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="240b5-207">在 [Azure 入口網站](https://portal.azure.com/)中按幾下滑鼠，即可建立 AdventureWorksLT 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="240b5-208">然後，本節中的步驟會說明如何使用記憶體內部 OLTP 物件擴充 AdventureWorksLT 資料庫，並示範效能優點。</span><span class="sxs-lookup"><span data-stu-id="240b5-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="240b5-209">如需更簡單、但更美觀的記憶體內部 OLTP 效能示範，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="240b5-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="240b5-210">版本︰[in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="240b5-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="240b5-211">原始程式碼︰[in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="240b5-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="240b5-212">安裝步驟</span><span class="sxs-lookup"><span data-stu-id="240b5-212">Installation steps</span></span>

1. <span data-ttu-id="240b5-213">在 [Azure 入口網站](https://portal.azure.com/)中，於伺服器上建立進階資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="240b5-214">將 [來源]  設定為 AdventureWorksLT 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="240b5-215">如需詳細指示，請參閱[建立您的第一個 Azure SQL Database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="240b5-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="240b5-216">使用 SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="240b5-217">將 [In-Memory OLTP Transact-SQL 指令碼](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) 複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="240b5-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="240b5-218">T-SQL 指令碼會在步驟 1 建立的 AdventureWorksLT 範例資料庫中建立所需的 In-Memory 物件。</span><span class="sxs-lookup"><span data-stu-id="240b5-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="240b5-219">將 T-SQL 指令碼貼到 SSMS 中，然後執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="240b5-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="240b5-220">`MEMORY_OPTIMIZED = ON` 子句 CREATE TABLE 陳述式很重要。</span><span class="sxs-lookup"><span data-stu-id="240b5-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="240b5-221">例如：</span><span class="sxs-lookup"><span data-stu-id="240b5-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="240b5-222">錯誤 40536</span><span class="sxs-lookup"><span data-stu-id="240b5-222">Error 40536</span></span>


<span data-ttu-id="240b5-223">如果您在執行 T-SQL 指令碼時收到錯誤 40536，請執行下列 T-SQL 指令碼來確認資料庫是否支援 In-Memory：</span><span class="sxs-lookup"><span data-stu-id="240b5-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="240b5-224">結果為 **0** 表示不支援 In-Memory，而 **1** 表示提供支援。</span><span class="sxs-lookup"><span data-stu-id="240b5-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="240b5-225">若要診斷問題，請確定資料庫位於「進階」服務層。</span><span class="sxs-lookup"><span data-stu-id="240b5-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="240b5-226">關於已建立的記憶體最佳化項目</span><span class="sxs-lookup"><span data-stu-id="240b5-226">About the created memory-optimized items</span></span>

<span data-ttu-id="240b5-227">**資料表**：此範例包含下列記憶體最佳化資料表：</span><span class="sxs-lookup"><span data-stu-id="240b5-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="240b5-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="240b5-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="240b5-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="240b5-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="240b5-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="240b5-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="240b5-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="240b5-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="240b5-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="240b5-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="240b5-233">您可以透過 SSMS 中的 [物件總管]，檢查記憶體最佳化資料表。</span><span class="sxs-lookup"><span data-stu-id="240b5-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="240b5-234">以滑鼠右鍵按一下 [資料表] > [篩選] > [篩選設定] > [記憶體已最佳化嗎]。</span><span class="sxs-lookup"><span data-stu-id="240b5-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="240b5-235">值等於 1。</span><span class="sxs-lookup"><span data-stu-id="240b5-235">The value equals 1.</span></span>


<span data-ttu-id="240b5-236">或者您可以查詢目錄檢視，例如：</span><span class="sxs-lookup"><span data-stu-id="240b5-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="240b5-237">**原生編譯的預存程序**：您可以透過目錄檢視查詢來檢查 SalesLT.usp_InsertSalesOrder_inmem：</span><span class="sxs-lookup"><span data-stu-id="240b5-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="240b5-238">執行範例 OLTP 工作負載</span><span class="sxs-lookup"><span data-stu-id="240b5-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="240b5-239">下列兩個預存程序  的唯一差別在於第一個程序會使用記憶體最佳化資料表版本，而第二個程序會使用一般磁碟資料表：</span><span class="sxs-lookup"><span data-stu-id="240b5-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="240b5-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="240b5-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="240b5-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="240b5-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="240b5-242">在本節中，您會了解如何使用便利的 **ostress.exe** 公用程式，在壓力層級執行兩個預存程序。</span><span class="sxs-lookup"><span data-stu-id="240b5-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="240b5-243">您可以比較完成兩個壓力回合所需的時間。</span><span class="sxs-lookup"><span data-stu-id="240b5-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="240b5-244">當您執行 ostress.exe 時，建議您將指定的參數值傳遞至下列兩者：</span><span class="sxs-lookup"><span data-stu-id="240b5-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="240b5-245">使用 -n100 來執行大量的並行連線。</span><span class="sxs-lookup"><span data-stu-id="240b5-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="240b5-246">使用 -r500 讓每個連線執行幾百次迴圈。</span><span class="sxs-lookup"><span data-stu-id="240b5-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="240b5-247">不過，您可能想從較小的值 (-n10 和 -r50) 開始，以確保一切都運作正常。</span><span class="sxs-lookup"><span data-stu-id="240b5-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="240b5-248">Ostress.exe 的指令碼</span><span class="sxs-lookup"><span data-stu-id="240b5-248">Script for ostress.exe</span></span>


<span data-ttu-id="240b5-249">本節顯示 ostress.exe 命令列中內嵌的 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="240b5-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="240b5-250">此指令碼會使用您稍早安裝的 T-SQL 指令碼所建立的項目。</span><span class="sxs-lookup"><span data-stu-id="240b5-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="240b5-251">下列指令碼會在下列記憶體最佳化資料表 中插入有 5 個細項的範例銷售訂單：</span><span class="sxs-lookup"><span data-stu-id="240b5-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="240b5-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="240b5-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="240b5-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="240b5-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="240b5-254">若要針對 ostress.exe 製作上述 T-SQL 指令碼的 *_ondisk* 版本，請以 *_ondisk* 取代兩個出現的 *_inmem* 子字串。</span><span class="sxs-lookup"><span data-stu-id="240b5-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="240b5-255">這類取代會影響資料表和預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="240b5-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="240b5-256">安裝 RML 公用程式和 ostress</span><span class="sxs-lookup"><span data-stu-id="240b5-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="240b5-257">您最好規劃在 Azure 虛擬機器 (VM) 上執行 ostress.exe。</span><span class="sxs-lookup"><span data-stu-id="240b5-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="240b5-258">您會在 AdventureWorksLT 資料庫所在的相同 Azure 地理區域中建立 [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="240b5-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="240b5-259">但是您可以改在您的膝上型電腦上執行 ostress.exe。</span><span class="sxs-lookup"><span data-stu-id="240b5-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="240b5-260">在 VM 上或你選擇的任何主機上，安裝 Replay Markup Language (RML) 公用程式。</span><span class="sxs-lookup"><span data-stu-id="240b5-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="240b5-261">這些公用程式包括 ostress.exe。</span><span class="sxs-lookup"><span data-stu-id="240b5-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="240b5-262">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="240b5-262">For more information, see:</span></span>
- <span data-ttu-id="240b5-263">[記憶體內部 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)中的 ostress.exe 討論。</span><span class="sxs-lookup"><span data-stu-id="240b5-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="240b5-264">[記憶體內部 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)。</span><span class="sxs-lookup"><span data-stu-id="240b5-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="240b5-265">[安裝 ostress.exe 的部落格](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)。</span><span class="sxs-lookup"><span data-stu-id="240b5-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="240b5-266">先執行 _inmem 壓力工作負載</span><span class="sxs-lookup"><span data-stu-id="240b5-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="240b5-267">您可以使用 RML 命令提示字元  視窗來執行 ostress.exe 命令列。</span><span class="sxs-lookup"><span data-stu-id="240b5-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="240b5-268">命令列參數會將 ostress 導向至：</span><span class="sxs-lookup"><span data-stu-id="240b5-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="240b5-269">同時執行 100 個連線 (-n100)。</span><span class="sxs-lookup"><span data-stu-id="240b5-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="240b5-270">每個連線會執行 T-SQL 指令碼 50 次 (-r50)。</span><span class="sxs-lookup"><span data-stu-id="240b5-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="240b5-271">若要執行上述的 ostress.exe 命令列：</span><span class="sxs-lookup"><span data-stu-id="240b5-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="240b5-272">在 SSMS 中執行下列命令來重設資料庫資料內容，以刪除先前執行插入的所有資料：</span><span class="sxs-lookup"><span data-stu-id="240b5-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="240b5-273">將上述 ostress.exe 命令列的文字複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="240b5-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="240b5-274">以正確的實數值取代參數 -S -U -P -d 的 `<placeholders>` 。</span><span class="sxs-lookup"><span data-stu-id="240b5-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="240b5-275">在 [RML 命令] 視窗中執行已編輯的命令列。</span><span class="sxs-lookup"><span data-stu-id="240b5-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="240b5-276">結果是持續時間</span><span class="sxs-lookup"><span data-stu-id="240b5-276">Result is a duration</span></span>


<span data-ttu-id="240b5-277">當 ostress.exe 完成時，它會在 RML 命令視窗中寫入執行持續時間做為輸出的最後一行。</span><span class="sxs-lookup"><span data-stu-id="240b5-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="240b5-278">例如，較短的測試回合持續大約 1.5 分鐘：</span><span class="sxs-lookup"><span data-stu-id="240b5-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="240b5-279">重設，針對 _ondisk 編輯，然後重新執行</span><span class="sxs-lookup"><span data-stu-id="240b5-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="240b5-280">在獲得 _inmem 執行的結果之後，請針對 _ondisk 執行回合執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="240b5-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="240b5-281">在 SSMS 中執行下列命令來重設資料庫，以刪除先前執行插入的所有資料：</span><span class="sxs-lookup"><span data-stu-id="240b5-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="240b5-282">編輯 ostress.exe 命令列，以 *_ondisk* 取代所有的 *_inmem*。</span><span class="sxs-lookup"><span data-stu-id="240b5-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="240b5-283">第二次重新執行 ostress.exe，並擷取持續時間結果。</span><span class="sxs-lookup"><span data-stu-id="240b5-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="240b5-284">再次重設資料庫 (以負責刪除可能的大量測試資料)。</span><span class="sxs-lookup"><span data-stu-id="240b5-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="240b5-285">預期的比較結果</span><span class="sxs-lookup"><span data-stu-id="240b5-285">Expected comparison results</span></span>

<span data-ttu-id="240b5-286">就這個過度簡單的工作負載而言，我們的「記憶體內部」測試顯示當 ostress 是在與資料庫相同 Azure 區域中的 Azure VM 上執行時，可獲得「九倍」的效能改善。</span><span class="sxs-lookup"><span data-stu-id="240b5-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="240b5-287">2.安裝記憶體內部分析範例</span><span class="sxs-lookup"><span data-stu-id="240b5-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="240b5-288">在本節中，您將比較使用資料行存放區索引與使用傳統 B 型樹狀結構索引時的 IO 和統計資料結果。</span><span class="sxs-lookup"><span data-stu-id="240b5-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="240b5-289">針對 OLTP 工作負載的即時分析，通常最好使用非叢集式資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="240b5-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="240b5-290">如需詳細資訊，請參閱[已描述的資料行存放區索引](http://msdn.microsoft.com/library/gg492088.aspx)。</span><span class="sxs-lookup"><span data-stu-id="240b5-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="240b5-291">準備資料行存放區分析測試</span><span class="sxs-lookup"><span data-stu-id="240b5-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="240b5-292">使用 Azure 入口網站，從範例建立全新的 AdventureWorksLT 資料庫。</span><span class="sxs-lookup"><span data-stu-id="240b5-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="240b5-293">使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="240b5-293">Use that exact name.</span></span>
 - <span data-ttu-id="240b5-294">選擇任何進階服務層。</span><span class="sxs-lookup"><span data-stu-id="240b5-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="240b5-295">將 [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) 複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="240b5-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="240b5-296">T-SQL 指令碼會在步驟 1 建立的 AdventureWorksLT 範例資料庫中建立所需的 In-Memory 物件。</span><span class="sxs-lookup"><span data-stu-id="240b5-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="240b5-297">此指令碼會建立維度資料表和兩個事實資料表。</span><span class="sxs-lookup"><span data-stu-id="240b5-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="240b5-298">每個事實資料表會填入 350 萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="240b5-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="240b5-299">此指令碼可能需要 15 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="240b5-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="240b5-300">將 T-SQL 指令碼貼到 SSMS 中，然後執行該指令碼。</span><span class="sxs-lookup"><span data-stu-id="240b5-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="240b5-301">**CREATE INDEX** 陳述式中的 **COLUMNSTORE** 關鍵字很重要，如下所示：</span><span class="sxs-lookup"><span data-stu-id="240b5-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="240b5-302">將 AdventureWorksLT 設為相容性層級 130：</span><span class="sxs-lookup"><span data-stu-id="240b5-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="240b5-303">層級 130 並未與 In-Memory 功能直接相關。</span><span class="sxs-lookup"><span data-stu-id="240b5-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="240b5-304">但層級 130 通常會提供比層級 120 更快的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="240b5-305">重要資料表和資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="240b5-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="240b5-306">dbo.FactResellerSalesXL_CCI 是具有叢集資料行存放區索引的資料表，此資料表已在「資料」層級進一步壓縮。</span><span class="sxs-lookup"><span data-stu-id="240b5-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="240b5-307">dbo.FactResellerSalesXL_PageCompressed 是具有對等一般叢集式索引的資料表，此資料表只在「頁面」層級壓縮。</span><span class="sxs-lookup"><span data-stu-id="240b5-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="240b5-308">用來比較資料行存放區索引的重要查詢</span><span class="sxs-lookup"><span data-stu-id="240b5-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="240b5-309">有[您可以執行的數種 T-SQL 查詢類型](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql)可用來查看效能改進。</span><span class="sxs-lookup"><span data-stu-id="240b5-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="240b5-310">在步驟 2 的 T-SQL 指令碼中，請注意這一組查詢。</span><span class="sxs-lookup"><span data-stu-id="240b5-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="240b5-311">其中的不同之處只有一行：</span><span class="sxs-lookup"><span data-stu-id="240b5-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="240b5-312">叢集資料行存放區索引位於 FactResellerSalesXL\_CCI 資料表上。</span><span class="sxs-lookup"><span data-stu-id="240b5-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="240b5-313">下列 T-SQL 指令碼摘錄列出每個資料表查詢的 IO 和 TIME 統計資料。</span><span class="sxs-lookup"><span data-stu-id="240b5-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="240b5-314">在定價層為 P2 的資料庫中，相較於傳統索引，使用叢集資料行存放區索引進行此查詢預期可提升大約九倍的效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="240b5-315">使用 P15 時，您可以預期使用資料行存放區索引大約可提升 57 倍的效能。</span><span class="sxs-lookup"><span data-stu-id="240b5-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="240b5-316">後續步驟</span><span class="sxs-lookup"><span data-stu-id="240b5-316">Next steps</span></span>

- [<span data-ttu-id="240b5-317">快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術</span><span class="sxs-lookup"><span data-stu-id="240b5-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="240b5-318">在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="240b5-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="240b5-319">針對記憶體內部 OLAP [監視記憶體內部 OLTP 儲存體](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="240b5-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="240b5-320">其他資源</span><span class="sxs-lookup"><span data-stu-id="240b5-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="240b5-321">更深入的資訊</span><span class="sxs-lookup"><span data-stu-id="240b5-321">Deeper information</span></span>

- [<span data-ttu-id="240b5-322">了解仲裁如何透過 SQL Database 中的記憶體內部 OLTP，讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU</span><span class="sxs-lookup"><span data-stu-id="240b5-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="240b5-323">Azure SQL Database 中的記憶體內部 OLTP 部落格文章</span><span class="sxs-lookup"><span data-stu-id="240b5-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="240b5-324">了解記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="240b5-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="240b5-325">了解資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="240b5-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="240b5-326">了解即時作業分析</span><span class="sxs-lookup"><span data-stu-id="240b5-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="240b5-327">請參閱[一般工作負載模式和移轉考量](http://msdn.microsoft.com/library/dn673538.aspx) (其中描述記憶體內部 OLTP 經常提供顯著效能改善的工作負載模式)</span><span class="sxs-lookup"><span data-stu-id="240b5-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="240b5-328">應用程式設計</span><span class="sxs-lookup"><span data-stu-id="240b5-328">Application design</span></span>

- [<span data-ttu-id="240b5-329">記憶體內部 OLTP (記憶體內部最佳化)</span><span class="sxs-lookup"><span data-stu-id="240b5-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="240b5-330">在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="240b5-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="240b5-331">工具</span><span class="sxs-lookup"><span data-stu-id="240b5-331">Tools</span></span>

- [<span data-ttu-id="240b5-332">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="240b5-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="240b5-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="240b5-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="240b5-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="240b5-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
