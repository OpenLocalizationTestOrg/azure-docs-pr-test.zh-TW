---
title: "aaaAzure SQL 資料庫中記憶體內部技術 |Microsoft 文件"
description: "Azure SQL Database-記憶體中技術大幅改善的交易式 hello 效能和分析工作負載。 深入了解如何 tootake 運用這些技術。"
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
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="7d90a-104">使用 SQL Database 中的記憶體內部技術將效能最佳化</span><span class="sxs-lookup"><span data-stu-id="7d90a-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="7d90a-105">您可以使用 Azure SQL Database 中的記憶體內部技術，以改善各種工作負載的效能︰交易式 (線上交易處理 (OLTP))、分析 (線上分析處理 (OLAP)) 及混合 (混合式交易/分析處理 (HTAP))。</span><span class="sxs-lookup"><span data-stu-id="7d90a-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="7d90a-106">因為 hello 更有效率的查詢和交易處理、 記憶體中技術也有助於您 tooreduce 成本。</span><span class="sxs-lookup"><span data-stu-id="7d90a-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="7d90a-107">您通常不需要 tooupgrade hello 定價層的 hello 資料庫 tooachieve 效能提升。</span><span class="sxs-lookup"><span data-stu-id="7d90a-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="7d90a-108">在某些情況下，您甚至可以降低 hello 定價層，之際，仍然使用中記憶體內部技術的效能改進。</span><span class="sxs-lookup"><span data-stu-id="7d90a-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="7d90a-109">以下是記憶體中 OLTP 如何幫助 toosignificantly 改善效能的兩個範例：</span><span class="sxs-lookup"><span data-stu-id="7d90a-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="7d90a-110">使用記憶體中 OLTP[仲裁商務解決方案時發生無法 toodouble 其工作負載改善 70%的 Dtu](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="7d90a-111">DTU 表示「資料庫輸送量單位」，其中包含對資源耗用的測量。</span><span class="sxs-lookup"><span data-stu-id="7d90a-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="7d90a-112">hello 下列影片示範以範例工作負載的資源耗用量會顯著改善： [Azure SQL Database 視訊 中的記憶體中 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="7d90a-113">如需詳細資訊，請參閱 hello 部落格文章：[記憶體中 OLTP 中 Azure SQL Database 部落格文章](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="7d90a-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="7d90a-114">記憶體中技術 hello Premium 層，包括高階彈性集區中的資料庫中的所有資料庫中可用。</span><span class="sxs-lookup"><span data-stu-id="7d90a-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="7d90a-115">hello 下列影片說明與 Azure SQL Database 中的記憶體中技術的潛在效能提升。</span><span class="sxs-lookup"><span data-stu-id="7d90a-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="7d90a-116">請記住 hello 的效能提高，請參閱一律取決於許多因素，包括 hello 的本質 hello 工作負載和資料，hello 資料庫的存取模式等等。</span><span class="sxs-lookup"><span data-stu-id="7d90a-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="7d90a-117">Azure SQL Database 具有下列記憶體中技術 hello:</span><span class="sxs-lookup"><span data-stu-id="7d90a-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="7d90a-118">「記憶體內部 OLTP」可增加輸送量並減少交易處理的延遲。</span><span class="sxs-lookup"><span data-stu-id="7d90a-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="7d90a-119">受益於記憶體內部 OLTP 的案例包括︰高輸送量的交易處理 (例如股票交易和網路遊戲)、從事件或 IoT 裝置擷取資料、快取、資料載入，以及暫存資料表和資料表變數等案例。</span><span class="sxs-lookup"><span data-stu-id="7d90a-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="7d90a-120">*叢集資料行存放區索引*減少您的儲存體使用量 （向上 too10 時間），並改善報告和分析查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="7d90a-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="7d90a-121">您可以使用它與事實資料表中您資料超市 toofit 更多的資料在資料庫中並改善效能。</span><span class="sxs-lookup"><span data-stu-id="7d90a-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="7d90a-122">此外，您可以使用歷程記錄資料中操作資料庫 tooarchive 中，而且是無法 tooquery too10 時間更多資料。</span><span class="sxs-lookup"><span data-stu-id="7d90a-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="7d90a-123">*非叢集資料行存放區索引*HTAP 說明您 toogain 即時深入了解您的企業，透過查詢 hello 操作高度耗費資源的擷取、 轉換和載入 (ETL) 處理程序直接資料庫而不 hello 需要 toorun 等如 hello 資料倉儲 toobe 填入。</span><span class="sxs-lookup"><span data-stu-id="7d90a-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="7d90a-124">非叢集資料行存放區索引會允許分析查詢的速度非常快執行 hello OLTP 資料庫，同時降低 hello hello 作業的工作負載的影響。</span><span class="sxs-lookup"><span data-stu-id="7d90a-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="7d90a-125">您也可以讓 hello 組合的記憶體最佳化資料表與資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="7d90a-126">這種組合可讓您 tooperform 的非常快速交易處理，以及太*同時*執行的分析查詢非常快速地在 hello 上相同的資料。</span><span class="sxs-lookup"><span data-stu-id="7d90a-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="7d90a-127">資料行存放區索引和記憶體內部 OLTP hello SQL Server 產品的一部分自以來 2012年和 2014，分別。</span><span class="sxs-lookup"><span data-stu-id="7d90a-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="7d90a-128">Azure SQL Database 和 SQL Server 共用 hello 相同的記憶體中技術的實作。</span><span class="sxs-lookup"><span data-stu-id="7d90a-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="7d90a-129">未來，這些技術的新功能會先在 Azure SQL Database 中推出，然後才在 SQL Server 中推出。</span><span class="sxs-lookup"><span data-stu-id="7d90a-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="7d90a-130">本主題描述記憶體內部 OLTP 和資料行存放區索引的特定 tooAzure SQL Database 的各個部分，並也包含範例：</span><span class="sxs-lookup"><span data-stu-id="7d90a-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="7d90a-131">您會看到這些技術的 hello 影響有關儲存體和資料大小限制。</span><span class="sxs-lookup"><span data-stu-id="7d90a-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="7d90a-132">您會看到 toomanage hello 的資料庫，使用這些技術 hello 不同定價層之間移動的方式。</span><span class="sxs-lookup"><span data-stu-id="7d90a-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="7d90a-133">您會看到兩個範例將示範 hello 使用的記憶體中 OLTP 為 Azure SQL Database 中的資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="7d90a-134">請參閱下列資源，如需詳細資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="7d90a-134">See hello following resources for more information.</span></span>

<span data-ttu-id="7d90a-135">深入了解 hello 技術的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="7d90a-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="7d90a-136">[記憶體中 OLTP 概觀和使用方式案例](https://msdn.microsoft.com/library/mt774593.aspx)（包括參考 toocustomer 案例研究和啟動資訊 tooget）</span><span class="sxs-lookup"><span data-stu-id="7d90a-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="7d90a-137">記憶體內部 OLTP 的文件</span><span class="sxs-lookup"><span data-stu-id="7d90a-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="7d90a-138">資料行存放區索引指南</span><span class="sxs-lookup"><span data-stu-id="7d90a-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="7d90a-139">混合式交易/分析處理 (HTAP)，也稱為[即時作業分析](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="7d90a-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="7d90a-140">在記憶體中 OLTP 的快速入門：[快速入門 1: T-SQL 效能更快的記憶體內部 OLTP 技術](http://msdn.microsoft.com/library/mt694156.aspx)(其他文章 toohelp 快速入門)</span><span class="sxs-lookup"><span data-stu-id="7d90a-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="7d90a-141">深入了解 hello 技術的相關影片：</span><span class="sxs-lookup"><span data-stu-id="7d90a-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="7d90a-142">[Azure SQL Database 中的記憶體中 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) （其中包含示範的效能優勢在於，和步驟 tooreproduce 這些結果自行）</span><span class="sxs-lookup"><span data-stu-id="7d90a-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="7d90a-143">記憶體中 OLTP 的影片： 什麼是當/如何 toouse 它</span><span class="sxs-lookup"><span data-stu-id="7d90a-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="7d90a-144">資料行存放區索引：記憶體內部分析影片 (來源：Ignite 2016)</span><span class="sxs-lookup"><span data-stu-id="7d90a-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="7d90a-145">儲存體和資料大小</span><span class="sxs-lookup"><span data-stu-id="7d90a-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="7d90a-146">記憶體內部 OLTP 的資料大小和儲存體上限</span><span class="sxs-lookup"><span data-stu-id="7d90a-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="7d90a-147">記憶體內部 OLTP 包含記憶體最佳化資料表，以用來儲存使用者資料。</span><span class="sxs-lookup"><span data-stu-id="7d90a-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="7d90a-148">這些資料表是在記憶體中的必要的 toofit。</span><span class="sxs-lookup"><span data-stu-id="7d90a-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="7d90a-149">由於管理直接在 hello SQL Database 服務中的記憶體時，我們會有配額的使用者資料的 hello 概念。</span><span class="sxs-lookup"><span data-stu-id="7d90a-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="7d90a-150">這個概念是參照的 tooas*記憶體中 OLTP 儲存體*。</span><span class="sxs-lookup"><span data-stu-id="7d90a-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="7d90a-151">每個受支援的獨立資料庫定價層以及每個彈性集區定價層都包含一定數量的記憶體內部 OLTP 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d90a-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="7d90a-152">Hello 撰寫本文時，會取得 1 gb 的儲存體每個 125 資料庫交易單位 (Dtu) 」 或 「 彈性資料庫交易單位 (Edtu)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="7d90a-153">hello [SQL Database 服務層](sql-database-service-tiers.md)發行項的 hello 官方 hello 記憶體內部 OLTP 可用存放裝置，針對每個支援獨立資料庫及定價層的彈性集區清單。</span><span class="sxs-lookup"><span data-stu-id="7d90a-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="7d90a-154">下列項目累計記憶體中 OLTP 儲存體 500mb hello:</span><span class="sxs-lookup"><span data-stu-id="7d90a-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="7d90a-155">記憶體最佳化資料表和資料表變數中的作用中使用者資料列。</span><span class="sxs-lookup"><span data-stu-id="7d90a-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="7d90a-156">請注意，舊的資料列版本不會計入 hello cap。</span><span class="sxs-lookup"><span data-stu-id="7d90a-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="7d90a-157">記憶體最佳化資料表上的索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="7d90a-158">ALTER TABLE 作業的作業負荷。</span><span class="sxs-lookup"><span data-stu-id="7d90a-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="7d90a-159">如果您遇到 hello 端點時，收到外的配額錯誤，而且您就不再能夠 tooinsert 或更新的資料。</span><span class="sxs-lookup"><span data-stu-id="7d90a-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="7d90a-160">toomitigate 這個錯誤，刪除資料，或增加 hello 定價層的 hello 資料庫或集區。</span><span class="sxs-lookup"><span data-stu-id="7d90a-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="7d90a-161">如需監視記憶體中 OLTP 儲存體使用量和幾乎叫用 hello 端點時，設定警示的詳細資訊，請參閱[監視記憶體中儲存](sql-database-in-memory-oltp-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="7d90a-162">關於彈性集區</span><span class="sxs-lookup"><span data-stu-id="7d90a-162">About elastic pools</span></span>

<span data-ttu-id="7d90a-163">彈性集區，與 hello 記憶體中 OLTP 儲存體共用 hello 集區中的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="7d90a-164">因此，在某個資料庫中的 hello 使用量可能會影響其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="7d90a-165">對此，您可以採取以下兩個對策︰</span><span class="sxs-lookup"><span data-stu-id="7d90a-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="7d90a-166">設定最大的 eDTU 資料庫低於 hello 整個 hello 集區的 eDTU 計數。</span><span class="sxs-lookup"><span data-stu-id="7d90a-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="7d90a-167">這個最大值的上限設定 hello 記憶體中 OLTP 儲存體使用率、 hello 集區，對應 toohello eDTU 計數 toohello 大小中任何資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="7d90a-168">設定大於 0 的最小 eDTU。</span><span class="sxs-lookup"><span data-stu-id="7d90a-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="7d90a-169">此最小保證 hello 集區中的每個資料庫都有可用的記憶體中 OLTP 儲存對應 toohello hello 總量設定 Min eDTU。</span><span class="sxs-lookup"><span data-stu-id="7d90a-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="7d90a-170">資料行存放區索引的資料大小和儲存體</span><span class="sxs-lookup"><span data-stu-id="7d90a-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="7d90a-171">資料行存放區索引不是必要的 toofit 在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="7d90a-172">因此，hello 只有 hello hello 索引大小上限為 hello 整體資料庫大小上限，而其記錄在 hello [SQL Database 服務層](sql-database-service-tiers.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7d90a-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="7d90a-173">當您使用叢集資料行存放區索引時，會將單欄式壓縮用於 hello 基底資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d90a-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="7d90a-174">此壓縮會大幅降低 hello 使用者資料，這表示您可以在 hello 資料庫容納更多資料的儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="7d90a-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="7d90a-175">和 hello 壓縮進一步增加了[單欄式封存壓縮](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="7d90a-176">hello，可讓您的壓縮量取決於 hello 的 hello 資料性質，但 10 次 hello 壓縮並不罕見。</span><span class="sxs-lookup"><span data-stu-id="7d90a-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="7d90a-177">例如，如果您有大小上限為 1 tb 的資料庫，而且您使用資料行存放區索引達到 10 次 hello 壓縮，您可以納入總計的 10 TB 的使用者資料 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="7d90a-178">當您使用非叢集資料行存放區索引時，hello 基底資料表仍會儲存在 hello 傳統的資料列存放區格式。</span><span class="sxs-lookup"><span data-stu-id="7d90a-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="7d90a-179">因此，hello 存放裝置節省不是與具有叢集資料行存放區索引的大小。</span><span class="sxs-lookup"><span data-stu-id="7d90a-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="7d90a-180">不過，如果您要取代傳統的非叢集索引的數目與單一資料行存放區索引，您仍然可以看到在 hello hello 資料表的儲存體使用量因而節省整體成本。</span><span class="sxs-lookup"><span data-stu-id="7d90a-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="7d90a-181">在不同定價層之間移動使用記憶體內部技術的資料庫</span><span class="sxs-lookup"><span data-stu-id="7d90a-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="7d90a-182">絕不會有任何不相容或其他問題時升級 tooa 較高的定價層，例如，從標準 tooPremium。</span><span class="sxs-lookup"><span data-stu-id="7d90a-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="7d90a-183">hello 可用的功能和資源只能增加。</span><span class="sxs-lookup"><span data-stu-id="7d90a-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="7d90a-184">但降級 hello 定價層可以對您的資料庫產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="7d90a-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="7d90a-185">hello 影響時，特別是當您從 Premium tooStandard 降級明顯或基本資料庫包含記憶體中 OLTP 物件。</span><span class="sxs-lookup"><span data-stu-id="7d90a-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="7d90a-186">記憶體最佳化資料表和資料行存放區索引，就無法使用 hello 降級之後 （即使它們保持可見）。</span><span class="sxs-lookup"><span data-stu-id="7d90a-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="7d90a-187">hello 考量同樣適用於您正在降低 hello 定價層的彈性集區，或移動資料庫與記憶體中技術，為標準或基本彈性集區時。</span><span class="sxs-lookup"><span data-stu-id="7d90a-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="7d90a-188">記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="7d90a-188">In-Memory OLTP</span></span>

<span data-ttu-id="7d90a-189">*降級 tooBasic/標準*: hello 標準或基本層中的資料庫中不支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="7d90a-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="7d90a-190">此外，它不可能 toomove 具有任何記憶體中 OLTP 物件 toohello 標準或基本層的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="7d90a-191">降級 tooStandard Basic 方式 hello 資料庫之前，請移除所有記憶體最佳化資料表和資料表類型，以及所有原生編譯的 T-SQL 模組。</span><span class="sxs-lookup"><span data-stu-id="7d90a-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="7d90a-192">沒有程式設計的方式 toounderstand 指定的資料庫是否支援 In-memory OLTP。</span><span class="sxs-lookup"><span data-stu-id="7d90a-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="7d90a-193">您可以執行下列 TRANSACT-SQL 查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="7d90a-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="7d90a-194">如果 hello 查詢傳回**1**，記憶體中 OLTP 支援此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="7d90a-195">*降級 tooa 低 Premium 層*： 記憶體最佳化資料表中的資料必須符合相關以 hello 定價層的 hello 資料庫或 hello 彈性集區中的 hello 記憶體中 OLTP 儲存區中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="7d90a-196">如果您嘗試 toolower hello 定價層或移到集區中沒有足夠的可用記憶體中 OLTP 儲存體、 hello 作業 hello 資料庫失敗。</span><span class="sxs-lookup"><span data-stu-id="7d90a-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="7d90a-197">資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="7d90a-197">Columnstore indexes</span></span>

<span data-ttu-id="7d90a-198">*降級 tooBasic 或標準*： 資料行存放區索引支援只在 hello Premium 定價層，而不是在 hello 標準或基本層。</span><span class="sxs-lookup"><span data-stu-id="7d90a-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="7d90a-199">降級您資料庫 tooStandard 或 Basic，您的資料行存放區索引會變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="7d90a-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="7d90a-200">hello 系統會維護您的資料行存放區索引，但是它絕不會運用 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="7d90a-201">如果您稍後升級後 tooPremium，資料行存放區索引是立即準備 toobe 運用一次。</span><span class="sxs-lookup"><span data-stu-id="7d90a-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="7d90a-202">如果您有**叢集**層降級之後資料行存放區索引 hello 整份資料表變成無法使用。</span><span class="sxs-lookup"><span data-stu-id="7d90a-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="7d90a-203">因此我們建議您卸除所有*叢集*降級下方 hello Premium 層資料庫之前，資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="7d90a-204">*降級 tooa 低 Premium 層*: hello 整個資料庫都符合內 hello 的資料庫大小上限 hello 目標定價層，或 hello hello 彈性集區中的可用儲存區中此降級會成功。</span><span class="sxs-lookup"><span data-stu-id="7d90a-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="7d90a-205">沒有特定的 hello 資料行存放區索引影響。</span><span class="sxs-lookup"><span data-stu-id="7d90a-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="7d90a-206">1.安裝 hello 記憶體中 OLTP 範例</span><span class="sxs-lookup"><span data-stu-id="7d90a-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="7d90a-207">您可以建立 hello 有提供 AdventureWorksLT 範例資料庫中 hello 按幾下[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7d90a-208">然後，hello 本節中的步驟說明如何擴充 AdventureWorksLT 資料庫使用記憶體中 OLTP 物件，並示範效能優勢。</span><span class="sxs-lookup"><span data-stu-id="7d90a-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="7d90a-209">如需更簡單、但更美觀的記憶體內部 OLTP 效能示範，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="7d90a-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="7d90a-210">版本︰[in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="7d90a-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="7d90a-211">原始程式碼︰[in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="7d90a-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="7d90a-212">安裝步驟</span><span class="sxs-lookup"><span data-stu-id="7d90a-212">Installation steps</span></span>

1. <span data-ttu-id="7d90a-213">在 hello [Azure 入口網站](https://portal.azure.com/)，在伺服器上建立高階資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="7d90a-214">設定 hello**來源**toohello 有提供 AdventureWorksLT 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="7d90a-215">如需詳細指示，請參閱[建立您的第一個 Azure SQL Database](sql-database-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="7d90a-216">使用 SQL Server Management Studio 連接 toohello 資料庫[(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="7d90a-217">複製 hello[記憶體中 OLTP TRANSACT-SQL 指令碼](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql)tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="7d90a-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="7d90a-218">hello T-SQL 指令碼會建立 hello 必要記憶體中物件在您在步驟 1 中建立的 hello 有提供 AdventureWorksLT 範例資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="7d90a-219">Hello T-SQL 指令碼貼到 SSMS 中，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d90a-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7d90a-220">hello`MEMORY_OPTIMIZED = ON`子句的 CREATE TABLE 陳述式很重要。</span><span class="sxs-lookup"><span data-stu-id="7d90a-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="7d90a-221">例如：</span><span class="sxs-lookup"><span data-stu-id="7d90a-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="7d90a-222">錯誤 40536</span><span class="sxs-lookup"><span data-stu-id="7d90a-222">Error 40536</span></span>


<span data-ttu-id="7d90a-223">如果您執行 hello T-SQL 指令碼時，您會收到錯誤 40536，，執行下列 T-SQL 指令碼 tooverify hello 指出資料庫是否支援記憶體中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7d90a-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="7d90a-224">結果為 **0** 表示不支援 In-Memory，而 **1** 表示提供支援。</span><span class="sxs-lookup"><span data-stu-id="7d90a-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="7d90a-225">toodiagnose hello 問題，請確定該 hello 資料庫位於 hello Premium 服務層。</span><span class="sxs-lookup"><span data-stu-id="7d90a-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="7d90a-226">關於 hello 建立記憶體最佳化的項目</span><span class="sxs-lookup"><span data-stu-id="7d90a-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="7d90a-227">**資料表**: hello 範例包含下列記憶體最佳化資料表的 hello:</span><span class="sxs-lookup"><span data-stu-id="7d90a-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="7d90a-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="7d90a-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="7d90a-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7d90a-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7d90a-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7d90a-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="7d90a-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="7d90a-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="7d90a-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="7d90a-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="7d90a-233">您可以檢查記憶體最佳化資料表透過 hello**物件總管 中**在 SSMS 中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="7d90a-234">以滑鼠右鍵按一下 [資料表] > [篩選] > [篩選設定] > [記憶體已最佳化嗎]。</span><span class="sxs-lookup"><span data-stu-id="7d90a-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="7d90a-235">hello 值等於 1。</span><span class="sxs-lookup"><span data-stu-id="7d90a-235">hello value equals 1.</span></span>


<span data-ttu-id="7d90a-236">或者，您也可以查詢 hello 目錄檢視，例如：</span><span class="sxs-lookup"><span data-stu-id="7d90a-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="7d90a-237">**原生編譯的預存程序**：您可以透過目錄檢視查詢來檢查 SalesLT.usp_InsertSalesOrder_inmem：</span><span class="sxs-lookup"><span data-stu-id="7d90a-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="7d90a-238">執行 hello 範例 OLTP 工作負載</span><span class="sxs-lookup"><span data-stu-id="7d90a-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="7d90a-239">hello 差異 hello 下列兩個*預存程序*hello 第一個程序會使用記憶體最佳化版本的 hello 資料表，在 hello 第二個程序使用 hello 一般磁碟上的資料表：</span><span class="sxs-lookup"><span data-stu-id="7d90a-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="7d90a-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="7d90a-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="7d90a-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="7d90a-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="7d90a-242">在本節中，您會看到如何 toouse hello 方便**ostress.exe**公用程式 tooexecute hello 壓力層級的兩個預存程序。</span><span class="sxs-lookup"><span data-stu-id="7d90a-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="7d90a-243">您可以比較的兩個 hello 壓力執行 toofinish 需要多久。</span><span class="sxs-lookup"><span data-stu-id="7d90a-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="7d90a-244">當您執行 ostress.exe 時，我們建議您傳遞的 hello 下列兩個設計的參數值：</span><span class="sxs-lookup"><span data-stu-id="7d90a-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="7d90a-245">使用 -n100 來執行大量的並行連線。</span><span class="sxs-lookup"><span data-stu-id="7d90a-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="7d90a-246">使用 -r500 讓每個連線執行幾百次迴圈。</span><span class="sxs-lookup"><span data-stu-id="7d90a-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="7d90a-247">不過，您可能想 toostart 類似-n10 和 r50 一切運作的 tooensure 較小的值。</span><span class="sxs-lookup"><span data-stu-id="7d90a-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="7d90a-248">Ostress.exe 的指令碼</span><span class="sxs-lookup"><span data-stu-id="7d90a-248">Script for ostress.exe</span></span>


<span data-ttu-id="7d90a-249">此區段會顯示為內嵌在我們 ostress.exe 命令列中的 hello T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d90a-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="7d90a-250">hello 指令碼會使用所建立的 hello 您先前安裝的 T-SQL 指令碼的項目。</span><span class="sxs-lookup"><span data-stu-id="7d90a-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="7d90a-251">hello 下列指令碼將具有五個明細項目範例銷售訂單插入記憶體最佳化的 hello 下列*資料表*:</span><span class="sxs-lookup"><span data-stu-id="7d90a-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="7d90a-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7d90a-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7d90a-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7d90a-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="7d90a-254">toomake hello *_ondisk*版本 hello ostress.exe 前述 T-SQL 指令碼，您必須取代出現 hello 的兩個*_inmem*與子字串*_ondisk*。</span><span class="sxs-lookup"><span data-stu-id="7d90a-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="7d90a-255">這些取代會影響 hello 資料表和預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d90a-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="7d90a-256">安裝 RML 公用程式和 ostress</span><span class="sxs-lookup"><span data-stu-id="7d90a-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="7d90a-257">在理想情況下，您應該規劃 toorun ostress.exe Azure 的虛擬機器 (VM) 上。</span><span class="sxs-lookup"><span data-stu-id="7d90a-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="7d90a-258">您可以建立[Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello 中有提供 AdventureWorksLT 資料庫所在的相同 Azure 的地理區域。</span><span class="sxs-lookup"><span data-stu-id="7d90a-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="7d90a-259">但是您可以改在您的膝上型電腦上執行 ostress.exe。</span><span class="sxs-lookup"><span data-stu-id="7d90a-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="7d90a-260">Hello VM，或您裝載任何選擇，請安裝 hello Replay 標記語言 (RML) 公用程式。</span><span class="sxs-lookup"><span data-stu-id="7d90a-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="7d90a-261">hello 公用程式包括 ostress.exe。</span><span class="sxs-lookup"><span data-stu-id="7d90a-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="7d90a-262">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7d90a-262">For more information, see:</span></span>
- <span data-ttu-id="7d90a-263">hello ostress.exe 討論[記憶體中 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7d90a-264">[記憶體內部 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7d90a-265">hello[部落格安裝 ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="7d90a-266">執行 hello *_inmem*先壓力工作負載</span><span class="sxs-lookup"><span data-stu-id="7d90a-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="7d90a-267">您可以使用*RML cmd 命令提示字元*視窗 toorun 我們 ostress.exe 命令列。</span><span class="sxs-lookup"><span data-stu-id="7d90a-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="7d90a-268">hello 命令列參數會直接以 ostress:</span><span class="sxs-lookup"><span data-stu-id="7d90a-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="7d90a-269">同時執行 100 個連線 (-n100)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="7d90a-270">有 50 次執行 hello T-SQL 指令碼的每個連接 (-r50)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="7d90a-271">toorun hello 前面 ostress.exe 命令列：</span><span class="sxs-lookup"><span data-stu-id="7d90a-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="7d90a-272">執行下列命令，在 SSMS 中，toodelete hello 已插入的任何先前執行的所有 hello 資料重設 hello 資料庫資料內容：</span><span class="sxs-lookup"><span data-stu-id="7d90a-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="7d90a-273">複製 hello 前面 ostress.exe 命令列 tooyour 剪貼簿的 hello 的文字。</span><span class="sxs-lookup"><span data-stu-id="7d90a-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="7d90a-274">取代 hello `<placeholders>` hello 參數-S-U-P-d 與 hello 更正實際值。</span><span class="sxs-lookup"><span data-stu-id="7d90a-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="7d90a-275">在 [RML 命令] 視窗中執行已編輯的命令列。</span><span class="sxs-lookup"><span data-stu-id="7d90a-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="7d90a-276">結果是持續時間</span><span class="sxs-lookup"><span data-stu-id="7d90a-276">Result is a duration</span></span>


<span data-ttu-id="7d90a-277">Ostress.exe 完成時，它會寫入 hello 做為其最後一行 hello RML Cmd 視窗中輸出的執行持續期間。</span><span class="sxs-lookup"><span data-stu-id="7d90a-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="7d90a-278">例如，較短的測試回合持續大約 1.5 分鐘：</span><span class="sxs-lookup"><span data-stu-id="7d90a-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="7d90a-279">重設，針對 _ondisk 編輯，然後重新執行</span><span class="sxs-lookup"><span data-stu-id="7d90a-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="7d90a-280">您擁有 hello hello 結果之後*_inmem*執行，請執行下列步驟 hello *_ondisk*執行：</span><span class="sxs-lookup"><span data-stu-id="7d90a-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="7d90a-281">執行下列命令，在 SSMS toodelete hello hello 先前執行所插入的所有 hello 資料重設 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="7d90a-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="7d90a-282">編輯 hello ostress.exe 命令列 tooreplace 所有*_inmem*與*_ondisk*。</span><span class="sxs-lookup"><span data-stu-id="7d90a-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="7d90a-283">重新執行 ostress.exe hello，第二次，並擷取 hello 持續時間結果。</span><span class="sxs-lookup"><span data-stu-id="7d90a-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="7d90a-284">同樣地，重設 hello 資料庫 （適用於以負責的態度刪除項目可以大量的測試資料）。</span><span class="sxs-lookup"><span data-stu-id="7d90a-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="7d90a-285">預期的比較結果</span><span class="sxs-lookup"><span data-stu-id="7d90a-285">Expected comparison results</span></span>

<span data-ttu-id="7d90a-286">我們的測試中記憶體中顯示的效能改善的**9 次**對於這個簡單的工作負載，使用 ostress 在 Azure VM 上執行 hello 相同 Azure 區域為 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="7d90a-287">2.安裝 hello 記憶體中分析範例</span><span class="sxs-lookup"><span data-stu-id="7d90a-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="7d90a-288">在本節中，您比較 hello IO 和統計資料的結果時使用的傳統 b 型樹狀目錄索引與資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="7d90a-289">針對 OLTP 工作負載進行即時分析，它是通常是最佳 toouse 非叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="7d90a-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="7d90a-290">如需詳細資訊，請參閱[已描述的資料行存放區索引](http://msdn.microsoft.com/library/gg492088.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d90a-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="7d90a-291">準備 hello 資料行存放區分析測試</span><span class="sxs-lookup"><span data-stu-id="7d90a-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="7d90a-292">使用 hello Azure 入口網站 toocreate hello 範例從全新的 AdventureWorksLT 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d90a-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="7d90a-293">使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d90a-293">Use that exact name.</span></span>
 - <span data-ttu-id="7d90a-294">選擇任何進階服務層。</span><span class="sxs-lookup"><span data-stu-id="7d90a-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="7d90a-295">複製 hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="7d90a-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="7d90a-296">hello T-SQL 指令碼會建立 hello 必要記憶體中物件在您在步驟 1 中建立的 hello 有提供 AdventureWorksLT 範例資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d90a-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="7d90a-297">hello 指令碼會建立 hello 維度資料表與兩個事實資料表。</span><span class="sxs-lookup"><span data-stu-id="7d90a-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="7d90a-298">hello 事實資料表會填入 3.5 百萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="7d90a-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="7d90a-299">hello 指令碼可能需要 15 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7d90a-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="7d90a-300">Hello T-SQL 指令碼貼到 SSMS 中，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d90a-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7d90a-301">hello**資料行存放區**關鍵字 hello **CREATE INDEX**陳述式中非常重要，做為：</span><span class="sxs-lookup"><span data-stu-id="7d90a-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="7d90a-302">將有提供 AdventureWorksLT toocompatibility 層級 130:</span><span class="sxs-lookup"><span data-stu-id="7d90a-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="7d90a-303">層級 130 不直接相關的 tooIn 記憶體內部功能。</span><span class="sxs-lookup"><span data-stu-id="7d90a-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="7d90a-304">但層級 130 通常會提供比層級 120 更快的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="7d90a-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="7d90a-305">重要資料表和資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="7d90a-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="7d90a-306">dbo。FactResellerSalesXL_CCI 是具有叢集資料行存放區索引，提供進階 hello 在壓縮的資料表*資料*層級。</span><span class="sxs-lookup"><span data-stu-id="7d90a-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="7d90a-307">dbo。FactResellerSalesXL_PageCompressed 是一份含有對等一般叢集的索引，以便壓縮只能在 hello*頁面*層級。</span><span class="sxs-lookup"><span data-stu-id="7d90a-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="7d90a-308">索引鍵查詢 toocompare hello 資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="7d90a-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="7d90a-309">有[數個您可以執行的 T-SQL 查詢類型](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql)toosee 效能改進。</span><span class="sxs-lookup"><span data-stu-id="7d90a-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="7d90a-310">在步驟 2 中 hello T-SQL 指令碼，特別注意 toothis 組的查詢。</span><span class="sxs-lookup"><span data-stu-id="7d90a-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="7d90a-311">其中的不同之處只有一行：</span><span class="sxs-lookup"><span data-stu-id="7d90a-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="7d90a-312">非叢集資料行存放區索引是在 hello FactResellerSalesXL\_CCI 資料表。</span><span class="sxs-lookup"><span data-stu-id="7d90a-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="7d90a-313">hello 下列 T-SQL 指令碼摘錄列印統計資料 IO 和每個資料表的 hello 查詢的時間。</span><span class="sxs-lookup"><span data-stu-id="7d90a-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
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


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
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

<span data-ttu-id="7d90a-314">在資料庫中的 hello P2 定價層，您可以利用 hello 叢集資料行存放區索引與 hello 傳統索引相較預期大約 9 次 hello 的效能提高，此查詢。</span><span class="sxs-lookup"><span data-stu-id="7d90a-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="7d90a-315">與 P15，您可以利用 hello 資料行存放區索引預期大約 57 次 hello 效能改善。</span><span class="sxs-lookup"><span data-stu-id="7d90a-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7d90a-316">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d90a-316">Next steps</span></span>

- [<span data-ttu-id="7d90a-317">快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術</span><span class="sxs-lookup"><span data-stu-id="7d90a-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="7d90a-318">在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="7d90a-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="7d90a-319">針對記憶體內部 OLAP [監視記憶體內部 OLTP 儲存體](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="7d90a-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7d90a-320">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d90a-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="7d90a-321">更深入的資訊</span><span class="sxs-lookup"><span data-stu-id="7d90a-321">Deeper information</span></span>

- [<span data-ttu-id="7d90a-322">了解仲裁如何透過 SQL Database 中的記憶體內部 OLTP，讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU</span><span class="sxs-lookup"><span data-stu-id="7d90a-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="7d90a-323">Azure SQL Database 中的記憶體內部 OLTP 部落格文章</span><span class="sxs-lookup"><span data-stu-id="7d90a-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="7d90a-324">了解記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="7d90a-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="7d90a-325">了解資料行存放區索引</span><span class="sxs-lookup"><span data-stu-id="7d90a-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="7d90a-326">了解即時作業分析</span><span class="sxs-lookup"><span data-stu-id="7d90a-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="7d90a-327">請參閱[一般工作負載模式和移轉考量](http://msdn.microsoft.com/library/dn673538.aspx) (其中描述記憶體內部 OLTP 經常提供顯著效能改善的工作負載模式)</span><span class="sxs-lookup"><span data-stu-id="7d90a-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="7d90a-328">應用程式設計</span><span class="sxs-lookup"><span data-stu-id="7d90a-328">Application design</span></span>

- [<span data-ttu-id="7d90a-329">記憶體內部 OLTP (記憶體內部最佳化)</span><span class="sxs-lookup"><span data-stu-id="7d90a-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="7d90a-330">在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP</span><span class="sxs-lookup"><span data-stu-id="7d90a-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="7d90a-331">工具</span><span class="sxs-lookup"><span data-stu-id="7d90a-331">Tools</span></span>

- [<span data-ttu-id="7d90a-332">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7d90a-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="7d90a-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="7d90a-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="7d90a-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="7d90a-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
