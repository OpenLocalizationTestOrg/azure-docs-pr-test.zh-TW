---
title: "跨多個 Azure SQL Database 執行臨機操作分析查詢 | Microsoft Docs"
description: "在 Wingtip SaaS 多租用戶應用程式中，跨多個 SQL Database 執行臨機操作分析查詢。"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: c287fe5d6b333c749b0580b5253e7e46ac27232b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a><span data-ttu-id="d1146-104">對所有 Wingtip SaaS 租用戶執行臨機操作分析查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-104">Run ad-hoc analytics queries across all Wingtip SaaS tenants</span></span>

<span data-ttu-id="d1146-105">在本教學課程中，您會在整個租用戶資料庫集合執行分散式查詢以啟用臨機操作分析。</span><span class="sxs-lookup"><span data-stu-id="d1146-105">In this tutorial, you run distributed queries across the entire set of tenant databases to enable ad-hoc analytics.</span></span> <span data-ttu-id="d1146-106">利用「彈性查詢」來啟用分散式查詢，這需要部署額外的分析資料庫 (到目錄伺服器)。</span><span class="sxs-lookup"><span data-stu-id="d1146-106">Elastic Query is used to enable distributed queries, which requires an additional analytics database is deployed (to the catalog server).</span></span> <span data-ttu-id="d1146-107">這些查詢可以擷取藏在 Wingtip SaaS 應用程式日常操作資料中的深入解析。</span><span class="sxs-lookup"><span data-stu-id="d1146-107">These queries can extract insights buried in the day-to-day operational data of the Wingtip SaaS app.</span></span>


<span data-ttu-id="d1146-108">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="d1146-108">In this tutorial you learn:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="d1146-109">每個資料庫中可跨租用戶執行高效率查詢的全域檢視</span><span class="sxs-lookup"><span data-stu-id="d1146-109">About the global views in each database, that enable efficient querying across tenants</span></span>
> * <span data-ttu-id="d1146-110">如何部署臨機操作分析資料庫</span><span class="sxs-lookup"><span data-stu-id="d1146-110">How to deploy an ad-hoc analytics database</span></span>
> * <span data-ttu-id="d1146-111">如何對所有租用戶資料庫執行分散式查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-111">How to run distributed queries across all tenant databases</span></span>



<span data-ttu-id="d1146-112">若要完成本教學課程，請確定已完成下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="d1146-112">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="d1146-113">已部署 Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1146-113">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="d1146-114">若要在五分鐘內完成部署，請參閱[部署及探索 Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="d1146-114">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="d1146-115">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d1146-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="d1146-116">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="d1146-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="d1146-117">已安裝 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="d1146-117">SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="d1146-118">若要下載和安裝 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="d1146-118">To download and install SSMS, see [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


## <a name="ad-hoc-analytics-pattern"></a><span data-ttu-id="d1146-119">臨機操作分析模式</span><span class="sxs-lookup"><span data-stu-id="d1146-119">Ad-hoc analytics pattern</span></span>

<span data-ttu-id="d1146-120">SaaS 應用程式的其中一個絕佳機會是使用集中儲存在雲端的大量租用戶資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-120">One of the great opportunities with SaaS applications is to use the vast amount of tenant data stored centrally in the cloud.</span></span> <span data-ttu-id="d1146-121">使用此資料可深入了解應用程式的作業與使用方式、租用戶、其使用者、喜好設定、行為等。這些深入解析可以引導應用程式和服務中的功能開發、使用性改進及其他投資。</span><span class="sxs-lookup"><span data-stu-id="d1146-121">Use this data to gain insights into the operation and usage of your application, your tenants, their users, preferences, behaviors, etc. These insights can guide feature development, usability improvements, and other investments in your apps and services.</span></span>

<span data-ttu-id="d1146-122">在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。</span><span class="sxs-lookup"><span data-stu-id="d1146-122">Accessing this data in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="d1146-123">其中一個方法是使用[彈性查詢](sql-database-elastic-query-overview.md)，這可對一組具有共用結構描述的分散式資料庫啟用查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-123">One approach is to use [Elastic Query](sql-database-elastic-query-overview.md), which enables querying across a distributed set of databases with common schema.</span></span> <span data-ttu-id="d1146-124">彈性查詢會使用單一 head 資料庫，其中定義的外部資料表會鏡射分散式 (租用戶) 資料庫中的資料表或檢視。</span><span class="sxs-lookup"><span data-stu-id="d1146-124">Elastic Query uses a single *head* database in which external tables are defined that mirror tables or views in the distributed (tenant) databases.</span></span> <span data-ttu-id="d1146-125">提交至此 head 資料庫的查詢會經過編譯，以產生分散式查詢計劃 (包含視需要往下推送到租用戶資料庫的查詢部分)。</span><span class="sxs-lookup"><span data-stu-id="d1146-125">Queries submitted to this head database are compiled to produce a distributed query plan, with portions of the query pushed down to the tenant databases as needed.</span></span> <span data-ttu-id="d1146-126">彈性查詢會使用目錄資料庫中的分區對應，提供租用戶資料庫的位置。</span><span class="sxs-lookup"><span data-stu-id="d1146-126">Elastic Query uses the shard map in the catalog database to provide the location of the tenant databases.</span></span> <span data-ttu-id="d1146-127">安裝程式和查詢會直接使用標準 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)，以及支援從 Power BI 和 Excel 等工具進行臨機操作查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-127">Setup and query are straightforward using standard [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference), and support ad-hoc querying from tools like Power BI and Excel.</span></span>

<span data-ttu-id="d1146-128">彈性查詢將查詢分散到整個租用戶資料庫，能夠立即深入了解即時的實際執行資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-128">By distributing queries across the tenant databases, Elastic Query provides immediate insight into live production data.</span></span> <span data-ttu-id="d1146-129">不過，因為彈性查詢可能會從多個資料庫提取資料，所以查詢延遲有時可能會高於提交至單一多租用戶資料庫的對等查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-129">However, as Elastic Query pulls data from potentially many databases, query latency can sometimes be higher than for equivalent queries submitted to a single multi-tenant database.</span></span> <span data-ttu-id="d1146-130">設計查詢來最小化傳回的資料時請務必小心。</span><span class="sxs-lookup"><span data-stu-id="d1146-130">Care should be taken when designing queries to minimize the data that is returned.</span></span> <span data-ttu-id="d1146-131">彈性查詢通常最適合查詢少量的即時資料，而非建立常用或複雜的分析查詢或報告。</span><span class="sxs-lookup"><span data-stu-id="d1146-131">Elastic Query is often best suited for querying small amounts of real-time data, as opposed to building frequently used or complex analytics queries or reports.</span></span> <span data-ttu-id="d1146-132">如果查詢的效能不佳，請查看[執行計畫](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan)以查看查詢的哪個部分已向下推送至遠端資料庫，以及傳回多少資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-132">If queries don't perform well, look at the [execution plan](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) to see what part of the query has been pushed down to the remote database and how much data is being returned.</span></span> <span data-ttu-id="d1146-133">需要複雜分析處理的查詢，在某些情況下透過將租用戶資料擷取到針對分析查詢最佳化的專用資料庫或資料倉儲來提供服務，可能會比較好。</span><span class="sxs-lookup"><span data-stu-id="d1146-133">Queries that require complex analytical processing may be better served in some cases by extracting tenant data into a dedicated database or data warehouse optimized for analytics queries.</span></span> <span data-ttu-id="d1146-134">[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)會說明此模式。</span><span class="sxs-lookup"><span data-stu-id="d1146-134">This pattern is explained in the [tenant analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md).</span></span> 

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="d1146-135">取得 Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="d1146-135">Get the Wingtip application scripts</span></span>

<span data-ttu-id="d1146-136">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) Github 存放庫可取得 Wingtip Tickets 指令碼和應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1146-136">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="d1146-137">[用於下載 Wingtip SaaS 指令碼的步驟](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="d1146-137">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-ticket-sales-data"></a><span data-ttu-id="d1146-138">建立票證銷售資料</span><span class="sxs-lookup"><span data-stu-id="d1146-138">Create ticket sales data</span></span>

<span data-ttu-id="d1146-139">若要針對更有趣的資料集執行查詢，請執行票證產生器來建立票證銷售資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-139">To run queries against a more interesting data set, create ticket sales data by running the ticket-generator.</span></span>

1. <span data-ttu-id="d1146-140">在 *PowerShell ISE* 中開啟 ...*Learning Modules*Operational Analytics\\Adhoc Analytics\\\\Demo-AdhocAnalytics.ps1\\ 指令碼，然後設定下列值：</span><span class="sxs-lookup"><span data-stu-id="d1146-140">In the *PowerShell ISE*, open the ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* script and set the following values:</span></span>
   * <span data-ttu-id="d1146-141">**$DemoScenario** = 1，**購買各地事件的票證**。</span><span class="sxs-lookup"><span data-stu-id="d1146-141">**$DemoScenario** = 1, **Purchase tickets for events at all venues**.</span></span>
2. <span data-ttu-id="d1146-142">按 **F5** 以執行指令碼並產生票證銷售。</span><span class="sxs-lookup"><span data-stu-id="d1146-142">Press **F5** to run the script and generate ticket sales.</span></span> <span data-ttu-id="d1146-143">執行指令碼時，請繼續本教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1146-143">While the script is running, continue the steps in this tutorial.</span></span> <span data-ttu-id="d1146-144">票證資料會在 [執行臨機操作分散式查詢] 區段中查詢，如果您進行到該練習時，票證產生器仍在執行，請等候它完成。</span><span class="sxs-lookup"><span data-stu-id="d1146-144">The ticket data is queried in the *Run ad-hoc distributed queries* section, so wait for the ticket generator to complete if it's still running when you get to that exercise.</span></span>

## <a name="explore-the-global-views"></a><span data-ttu-id="d1146-145">瀏覽全域檢視</span><span class="sxs-lookup"><span data-stu-id="d1146-145">Explore the global views</span></span>

<span data-ttu-id="d1146-146">Wingtip SaaS 應用程式是使用 tenant-per-database 模型建置，因此會從單一租用戶的觀點定義租用戶資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="d1146-146">The Wingtip SaaS application is built using a tenant-per-database model, so the tenant database schema is defined from a single-tenant perspective.</span></span> <span data-ttu-id="d1146-147">租用戶特定資訊位於一個 *Venue* 資料表中，該資料表一律有單一資料列，且會實作成一個沒有主索引鍵的堆積。</span><span class="sxs-lookup"><span data-stu-id="d1146-147">Tenant-specific information exists in one table, *Venue*, which always has a single row, and is implemented as a heap, without a primary key.</span></span> <span data-ttu-id="d1146-148">結構描述中的其他資料表不必與 Venue 資料表相關，因為正常使用時，資料屬於哪個租用戶絕對毫無疑慮。</span><span class="sxs-lookup"><span data-stu-id="d1146-148">Other tables in the schema don't need to be related to the *Venue* table, because in normal use, there is never any doubt which tenant the data belongs to.</span></span>

<span data-ttu-id="d1146-149">不過，在跨所有資料庫查詢時，務必讓彈性查詢可以將資料視為是依租用戶分區之單一邏輯資料庫的一部分。</span><span class="sxs-lookup"><span data-stu-id="d1146-149">However, when querying across all databases, it's important that Elastic Query can treat the data as if it is part of a single logical database sharded by tenant.</span></span> <span data-ttu-id="d1146-150">若要達成此目的，需將一組「全域」檢視新增至租用戶資料庫，將租用戶識別碼對應到全域查詢的每個資料表。</span><span class="sxs-lookup"><span data-stu-id="d1146-150">To achieve this, a set of 'global' views are added to the tenant database that project a tenant id into each of the tables that are queried globally.</span></span> <span data-ttu-id="d1146-151">例如，*VenueEvents* 檢視將計算的 *VenueId* 新增至從 *Events* 資料表對應的資料行。</span><span class="sxs-lookup"><span data-stu-id="d1146-151">For example, the *VenueEvents* view adds a computed *VenueId* to the columns projected from the *Events* table.</span></span> <span data-ttu-id="d1146-152">透過在 head 資料庫中針對 *VenueEvents* (而不是基礎 *Events* 資料表) 定義外部資料表，彈性查詢就能夠根據 *VenueId* 向下推送聯結，讓聯結可以在每個遠端資料庫 (而不是在 head 資料庫) 上平行執行。</span><span class="sxs-lookup"><span data-stu-id="d1146-152">By defining the external table in the head database over *VenueEvents* (rather than the underlying *Events* table), Elastic Query is able to push down joins based on *VenueId* so they can be executed in parallel on each remote database (rather than on the head database).</span></span> <span data-ttu-id="d1146-153">這會大幅減少傳回的資料量，進而大幅增加許多查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="d1146-153">This dramatically reduces the amount of data that is returned, which results in a substantial increase in performance for many queries.</span></span> <span data-ttu-id="d1146-154">這些全域檢視已在所有租用戶資料庫 (以及在*basetenantdb*) 中預先建立。</span><span class="sxs-lookup"><span data-stu-id="d1146-154">These global views have been pre-created in all tenant databases (and in *basetenantdb*).</span></span>

1. <span data-ttu-id="d1146-155">開啟 SSMS 並[連線到 tenants1-&lt;USER&gt; 伺服器](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)。</span><span class="sxs-lookup"><span data-stu-id="d1146-155">Open SSMS and [connect to the tenants1-&lt;USER&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).</span></span>
2. <span data-ttu-id="d1146-156">展開 [資料庫]，以滑鼠右鍵按一下 **contosoconcerthall**，然後選取 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="d1146-156">Expand **Databases**, right-click **contosoconcerthall**, and select **New Query**.</span></span>
3. <span data-ttu-id="d1146-157">執行下列查詢來探索單一租用戶資料表與全域檢視之間的差異︰</span><span class="sxs-lookup"><span data-stu-id="d1146-157">Run the following queries to explore the difference between the single-tenant tables and the global views:</span></span>

   ```T-SQL
   -- The base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice the plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- The base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects the VenueId retrieved from the Venues table.
   SELECT * FROM VenueEvents
   ```

<span data-ttu-id="d1146-158">在這些檢視中，*VenueId* 是以 Venue 名稱的雜湊來計算，但您可以使用任何方法來導入唯一值。</span><span class="sxs-lookup"><span data-stu-id="d1146-158">In these views, the *VenueId* is computed as a hash of the Venue name, but any approach could be used to introduce a unique value.</span></span> <span data-ttu-id="d1146-159">這個方法與計算用於目錄中租用戶金鑰的方法類似。</span><span class="sxs-lookup"><span data-stu-id="d1146-159">This approach is similar to the way the tenant key is computed for use in the catalog.</span></span>

<span data-ttu-id="d1146-160">檢查 *Venues* 檢視的定義：</span><span class="sxs-lookup"><span data-stu-id="d1146-160">To examine the definition of the *Venues* view:</span></span>

1. <span data-ttu-id="d1146-161">在 [物件總管] 中，展開 [contosoconcethall] > [檢視]：</span><span class="sxs-lookup"><span data-stu-id="d1146-161">In **Object Explorer**, expand **contosoconcethall** > **Views**:</span></span>

   ![檢視](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. <span data-ttu-id="d1146-163">以滑鼠右鍵按一下 **dbo.Venues**。</span><span class="sxs-lookup"><span data-stu-id="d1146-163">Right-click **dbo.Venues**.</span></span>
3. <span data-ttu-id="d1146-164">選取 [產生檢視的指令碼為] > [CREATE To] > [新的查詢編輯器視窗]</span><span class="sxs-lookup"><span data-stu-id="d1146-164">Select **Script View as** > **CREATE To** > **New Query Editor Window**</span></span>

<span data-ttu-id="d1146-165">產生其他任何 *Venue* 檢視的指令碼，以查看如何新增 *VenueId*。</span><span class="sxs-lookup"><span data-stu-id="d1146-165">Script any of the other *Venue* views to see how they add the *VenueId*.</span></span>

## <a name="deploy-the-database-used-for-ad-hoc-distributed-queries"></a><span data-ttu-id="d1146-166">部署用於臨機操作分散式查詢的資料庫</span><span class="sxs-lookup"><span data-stu-id="d1146-166">Deploy the database used for ad-hoc distributed queries</span></span>

<span data-ttu-id="d1146-167">此練習會部署 adhocanalytics 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-167">This exercise deploys the *adhocanalytics* database.</span></span> <span data-ttu-id="d1146-168">這就是將包含用來查詢所有租用戶資料庫之結構描述的 head 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-168">This is the head database that will contain the schema used for querying across all tenant databases.</span></span> <span data-ttu-id="d1146-169">此資料庫會部署到現有的目錄伺服器，也就是在範例應用程式中供所有管理相關資料庫使用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1146-169">The database is deployed to the existing catalog server, which is the server used for all management-related databases in the sample app.</span></span>

1. <span data-ttu-id="d1146-170">在 PowerShell ISE 中開啟 ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\Demo-AdhocAnalytics.ps1 並設定下列值：</span><span class="sxs-lookup"><span data-stu-id="d1146-170">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* in the *PowerShell ISE* and set the following values:</span></span>
   * <span data-ttu-id="d1146-171">**$DemoScenario** = 2，**部署臨機操作分析資料庫**。</span><span class="sxs-lookup"><span data-stu-id="d1146-171">**$DemoScenario** = 2, **Deploy Ad-hoc analytics database**.</span></span>

2. <span data-ttu-id="d1146-172">按 **F5** 以執行指令碼並建立 adhocanalytics 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-172">Press **F5** to run the script and create the *adhocanalytics* database.</span></span>

<span data-ttu-id="d1146-173">在下節中，您要將結構描述新增至資料庫，以便能夠用來執行分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-173">In the next section, you add schema to the database so it can be used to run distributed queries.</span></span>

## <a name="configure-the-database-for-running-distributed-queries"></a><span data-ttu-id="d1146-174">設定資料庫來執行分散式查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-174">Configure the database for running distributed queries</span></span>

<span data-ttu-id="d1146-175">此練習將結構描述 (外部資料來源和外部資料表定義) 新增至臨機操作分析資料庫，讓您能跨所有租用戶資料庫進行查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-175">This exercise adds schema (the external data source and external table definitions) to the ad-hoc analytics database that enables querying across all tenant databases.</span></span>

1. <span data-ttu-id="d1146-176">開啟 SQL Server Management Studio，並連線到您在上一個步驟中建立的臨機操作分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-176">Open SQL Server Management Studio, and connect to the Adhoc Analytics database you created in the previous step.</span></span> <span data-ttu-id="d1146-177">資料庫的名稱會是 adhocanalytics。</span><span class="sxs-lookup"><span data-stu-id="d1146-177">The name of the database will be adhocanalytics.</span></span>
2. <span data-ttu-id="d1146-178">在 SSMS 中開啟 ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*。</span><span class="sxs-lookup"><span data-stu-id="d1146-178">Open ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* in SSMS.</span></span>
3. <span data-ttu-id="d1146-179">檢閱 SQL 指令碼並注意下列事項︰</span><span class="sxs-lookup"><span data-stu-id="d1146-179">Review the SQL script and note the following:</span></span>

   <span data-ttu-id="d1146-180">彈性查詢會使用資料庫範圍的認證來存取每個租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-180">Elastic Query uses a database-scoped credential to access each of the tenant databases.</span></span> <span data-ttu-id="d1146-181">此認證必須可用於所有資料庫，且通常應獲得啟用這些臨機操作查詢所需的最小權限。</span><span class="sxs-lookup"><span data-stu-id="d1146-181">This credential needs to be available in all the databases and should normally be granted the minimum rights required to enable these ad-hoc queries.</span></span>

    ![建立認證](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   <span data-ttu-id="d1146-183">外部資料來源，其已定義為在目錄資料庫中使用租用戶分區對應。</span><span class="sxs-lookup"><span data-stu-id="d1146-183">The external data source, that is defined to use the tenant shard map in the catalog database.</span></span> <span data-ttu-id="d1146-184">以此作為外部資料來源，在執行查詢時，查詢會分散到在目錄中註冊的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-184">By using this as the external data source, queries are distributed to all databases registered in the catalog when the query is run.</span></span> <span data-ttu-id="d1146-185">因為每個部署的伺服器名稱不同，所以此初始化指令碼會擷取指令碼執行所在的目前伺服器 (@@servername)，取得目錄資料庫的位置。</span><span class="sxs-lookup"><span data-stu-id="d1146-185">Because server names are different for each deployment, this initialization script gets the location of the catalog database by retrieving the current server (@@servername) where the script is executed.</span></span>

    ![建立外部資料來源](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   <span data-ttu-id="d1146-187">參考前一節所述之全域檢視，並使用 **DISTRIBUTION = SHARDED(VenueId)** 定義的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="d1146-187">The external tables that reference the global views described in the previous section, and defined with **DISTRIBUTION = SHARDED(VenueId)**.</span></span> <span data-ttu-id="d1146-188">因為每個 *VenueId* 都對應到單一資料庫，所以這可改善許多情況 (如下一節所示) 的效能。</span><span class="sxs-lookup"><span data-stu-id="d1146-188">Because each *VenueId* maps to a single database, this improves performance for many scenarios as shown in the next section.</span></span>

    ![建立外部資料表](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   <span data-ttu-id="d1146-190">已建立和填入的本機資料表 *VenueTypes*。</span><span class="sxs-lookup"><span data-stu-id="d1146-190">The local table *VenueTypes* that is created and populated.</span></span> <span data-ttu-id="d1146-191">此參考資料表在所有租用戶資料庫中很常見，因此在此可以表示為本機資料表，並使用一般的資料填入。</span><span class="sxs-lookup"><span data-stu-id="d1146-191">This reference data table is common in all tenant databases, so it can be represented here as a local table and populated with the common data.</span></span> <span data-ttu-id="d1146-192">對於某些查詢而言，這可能會減少租用戶資料庫與 *adhocanalytics* 資料庫之間移動的資料量。</span><span class="sxs-lookup"><span data-stu-id="d1146-192">For some queries this may reduce the amount of data moved between the tenant databases and the *adhocanalytics* database.</span></span>

    ![建立資料表](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   <span data-ttu-id="d1146-194">如果您以這種方式包含參考資料表，每當您更新租用戶資料庫時，請務必更新資料表結構描述和資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-194">If you include reference tables in this manner, be sure to update the table schema and data whenever you update the tenant databases.</span></span>

4. <span data-ttu-id="d1146-195">按 **F5** 以執行指令碼並初始化 adhocanalytics 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-195">Press **F5** to run the script and initialize the *adhocanalytics* database.</span></span> 

<span data-ttu-id="d1146-196">現在您可以執行分散式查詢，然後收集所有租用戶之間的深入資訊！</span><span class="sxs-lookup"><span data-stu-id="d1146-196">Now you can run distributed queries, and gather insights across all tenants!</span></span>

## <a name="run-ad-hoc-distributed-queries"></a><span data-ttu-id="d1146-197">執行臨機操作分散式查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-197">Run ad-hoc distributed queries</span></span>

<span data-ttu-id="d1146-198">既然 *adhocanalytics* 資料庫已完成設定，請繼續執行一些分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-198">Now that the *adhocanalytics* database is set up, go ahead and run some distributed queries.</span></span> <span data-ttu-id="d1146-199">請包含執行計畫，以便進一步了解發生查詢處理的位置。</span><span class="sxs-lookup"><span data-stu-id="d1146-199">Include the execution plan for a better understanding of where the query processing is happening.</span></span> 

<span data-ttu-id="d1146-200">檢查執行計畫時，將滑鼠停留在計畫圖示上方，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-200">When inspecting the execution plan, hover over the plan icons for details.</span></span> 

<span data-ttu-id="d1146-201">值得注意的是，我們定義外部資料來源時的設定 **DISTRIBUTION = SHARDED(VenueId)**，改善許多情況的效能。</span><span class="sxs-lookup"><span data-stu-id="d1146-201">Important to note, is that setting **DISTRIBUTION = SHARDED(VenueId)** when we defined the external data source, improves performance for many scenarios.</span></span> <span data-ttu-id="d1146-202">因為每個 *VenueId* 都對應到單一資料庫，所以篩選會輕鬆地在遠端完成，只傳回我們所需的資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-202">Because each *VenueId* maps to a single database, filtering is easily done remotely, returning only the data we need.</span></span>

1. <span data-ttu-id="d1146-203">在 SSMS 中開啟 ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\Demo-AdhocAnalyticsQueries.sql。</span><span class="sxs-lookup"><span data-stu-id="d1146-203">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.</span></span>
2. <span data-ttu-id="d1146-204">確定您已連線到 **adhocanalytics** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1146-204">Ensure you are connected to the **adhocanalytics** database.</span></span>
3. <span data-ttu-id="d1146-205">選取 [查詢] 功能表，然後按一下 [包括實際執行計畫]</span><span class="sxs-lookup"><span data-stu-id="d1146-205">Select the **Query** menu and click **Include Actual Execution Plan**</span></span>
4. <span data-ttu-id="d1146-206">反白顯示 [Which venues are currently registered?] \(目前註冊哪些地點?\) 查詢，然後按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="d1146-206">Highlight the *Which venues are currently registered?* query, and press **F5**.</span></span>

   <span data-ttu-id="d1146-207">此查詢會傳回整份地點清單，說明跨所有租用戶進行查詢非常快速而且容易，並傳回每個租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="d1146-207">The query returns the entire venue list, illustrating how quick and easy it is to query across all tenants and return data from each tenant.</span></span>

   <span data-ttu-id="d1146-208">檢查計畫，您會發現全部成本都是遠端查詢，因為我們只是到每個租用戶資料庫，選取地點資訊。</span><span class="sxs-lookup"><span data-stu-id="d1146-208">Inspect the plan and see that the entire cost is the remote query because we're simply going to each tenant database and selecting the venue information.</span></span>

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. <span data-ttu-id="d1146-210">選取下一個查詢，然後按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="d1146-210">Select the next query, and press **F5**.</span></span>

   <span data-ttu-id="d1146-211">此查詢會聯結租用戶資料庫的資料和本機 *VenueTypes* 資料表的資料 (本機是因為它是 *adhocanalytics* 資料庫中的資料表)。</span><span class="sxs-lookup"><span data-stu-id="d1146-211">This query joins data from the tenant databases and the local *VenueTypes* table (local, as its a table in the *adhocanalytics* database).</span></span>

   <span data-ttu-id="d1146-212">檢查計畫，您會發現大多數的成本是遠端查詢，因為我們查詢每個租用戶的地點資訊 (dbo.Venues)，然後與本機 *VenueTypes* 資料表執行快速的本機聯結，以顯示易記名稱。</span><span class="sxs-lookup"><span data-stu-id="d1146-212">Inspect the plan and see that the majority of cost is the remote query because we query each tenant's venue info (dbo.Venues), and then do a quick local join with the local *VenueTypes* table to display the friendly name.</span></span>

   ![遠端資料與本機資料的聯結](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. <span data-ttu-id="d1146-214">現在選取 [On which day were the most tickets sold?] \(哪一天銷售最多票證?\) 查詢，然後按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="d1146-214">Now select the *On which day were the most tickets sold?* query, and press **F5**.</span></span>

   <span data-ttu-id="d1146-215">此查詢會執行比較複雜的聯結和彙總。</span><span class="sxs-lookup"><span data-stu-id="d1146-215">This query does a bit more complex joining and aggregation.</span></span> <span data-ttu-id="d1146-216">值得注意的是，大部分處理都在遠端電腦上進行，同樣地，我們只取回我們所需的資料列，只傳回每天每個地點彙總的票證銷售計數的單一資料列。</span><span class="sxs-lookup"><span data-stu-id="d1146-216">What's important to note is that most of the processing is done remotely, and once again, we bring back only the rows we need, returning just a single row for each venue's aggregate ticket sale count per day.</span></span>

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a><span data-ttu-id="d1146-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1146-218">Next steps</span></span>

<span data-ttu-id="d1146-219">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="d1146-219">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="d1146-220">對所有租用戶資料庫執行分散式查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-220">Run distributed queries across all tenant databases</span></span>
> * <span data-ttu-id="d1146-221">部署臨機操作分析資料庫，並將結構描述新增至資料庫中，以執行分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="d1146-221">Deploy an ad-hoc analytics database and add schema to it to run distributed queries.</span></span>


<span data-ttu-id="d1146-222">現在嘗試[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)，了解如何將資料擷取到另一個分析資料庫，進行更複雜的分析處理...</span><span class="sxs-lookup"><span data-stu-id="d1146-222">Now try the [Tenant Analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md) to explore extracting data to a separate analytics database for more complex analytics processing...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d1146-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="d1146-223">Additional resources</span></span>

* <span data-ttu-id="d1146-224">其他[以 Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="d1146-224">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="d1146-225">彈性查詢</span><span class="sxs-lookup"><span data-stu-id="d1146-225">Elastic Query</span></span>](sql-database-elastic-query-overview.md)
