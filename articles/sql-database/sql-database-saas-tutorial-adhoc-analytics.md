---
title: "跨多個 Azure SQL database aaaRun 臨機操作分析查詢 |Microsoft 文件"
description: "跨多個 hello Wingtip SaaS 多租用戶應用程式中的 SQL 資料庫執行特定分析查詢。"
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
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a><span data-ttu-id="2ca5d-104">對所有 Wingtip SaaS 租用戶執行臨機操作分析查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-104">Run ad-hoc analytics queries across all Wingtip SaaS tenants</span></span>

<span data-ttu-id="2ca5d-105">在本教學課程中，您執行分散式的查詢 hello 整個租用戶資料庫集合 tooenable 臨機操作分析。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-105">In this tutorial, you run distributed queries across hello entire set of tenant databases tooenable ad-hoc analytics.</span></span> <span data-ttu-id="2ca5d-106">彈性查詢是使用的 tooenable 分散式查詢，這需要部署額外的分析資料庫 （toohello 類別目錄伺服器）。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-106">Elastic Query is used tooenable distributed queries, which requires an additional analytics database is deployed (toohello catalog server).</span></span> <span data-ttu-id="2ca5d-107">這些查詢可以擷取埋藏在 hello 日常操作的資料的 hello Wingtip SaaS 應用程式的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-107">These queries can extract insights buried in hello day-to-day operational data of hello Wingtip SaaS app.</span></span>


<span data-ttu-id="2ca5d-108">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-108">In this tutorial you learn:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="2ca5d-109">有關每個資料庫中的 hello 全域檢視，可讓在租用戶之間的有效率查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-109">About hello global views in each database, that enable efficient querying across tenants</span></span>
> * <span data-ttu-id="2ca5d-110">如何 toodeploy 臨機操作分析資料庫</span><span class="sxs-lookup"><span data-stu-id="2ca5d-110">How toodeploy an ad-hoc analytics database</span></span>
> * <span data-ttu-id="2ca5d-111">Toorun 如何跨所有租用戶資料庫分散式查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-111">How toorun distributed queries across all tenant databases</span></span>



<span data-ttu-id="2ca5d-112">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-112">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="2ca5d-113">hello Wingtip SaaS 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-113">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="2ca5d-114">toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="2ca5d-114">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="2ca5d-115">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="2ca5d-116">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="2ca5d-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="2ca5d-117">已安裝 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-117">SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="2ca5d-118">toodownload 並安裝 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-118">toodownload and install SSMS, see [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


## <a name="ad-hoc-analytics-pattern"></a><span data-ttu-id="2ca5d-119">臨機操作分析模式</span><span class="sxs-lookup"><span data-stu-id="2ca5d-119">Ad-hoc analytics pattern</span></span>

<span data-ttu-id="2ca5d-120">Toouse hello 大量集中儲存在 hello 雲端中的租用戶資料的其中一個 hello 與 SaaS 應用程式的絕佳機會。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-120">One of hello great opportunities with SaaS applications is toouse hello vast amount of tenant data stored centrally in hello cloud.</span></span> <span data-ttu-id="2ca5d-121">使用此資料 toogain 深入了解 hello 作業和使用您的應用程式、 您的租用戶、 使用者、 喜好設定、 行為、 等等。這些深入解析可以引導應用程式和服務中的功能開發、使用性改進及其他投資。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-121">Use this data toogain insights into hello operation and usage of your application, your tenants, their users, preferences, behaviors, etc. These insights can guide feature development, usability improvements, and other investments in your apps and services.</span></span>

<span data-ttu-id="2ca5d-122">在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-122">Accessing this data in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="2ca5d-123">其中一個方法是 toouse[彈性查詢](sql-database-elastic-query-overview.md)，可讓在一組具有通用的結構描述的資料庫的分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-123">One approach is toouse [Elastic Query](sql-database-elastic-query-overview.md), which enables querying across a distributed set of databases with common schema.</span></span> <span data-ttu-id="2ca5d-124">彈性查詢會使用單一*head*外部資料表定義之鏡像資料表或檢視表中 hello 分散式 （租用戶） 資料庫的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-124">Elastic Query uses a single *head* database in which external tables are defined that mirror tables or views in hello distributed (tenant) databases.</span></span> <span data-ttu-id="2ca5d-125">Toothis 前端資料庫提交的查詢會編譯的 tooproduce 分散式的查詢計劃，與 hello 查詢推 toohello 租用戶資料庫所需的部分。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-125">Queries submitted toothis head database are compiled tooproduce a distributed query plan, with portions of hello query pushed down toohello tenant databases as needed.</span></span> <span data-ttu-id="2ca5d-126">彈性查詢會使用 hello 分區對應中 hello 類別目錄資料庫 tooprovide hello hello 租用戶資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-126">Elastic Query uses hello shard map in hello catalog database tooprovide hello location of hello tenant databases.</span></span> <span data-ttu-id="2ca5d-127">安裝程式和查詢會直接使用標準 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)，以及支援從 Power BI 和 Excel 等工具進行臨機操作查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-127">Setup and query are straightforward using standard [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference), and support ad-hoc querying from tools like Power BI and Excel.</span></span>

<span data-ttu-id="2ca5d-128">將查詢分散到 hello 租用戶資料庫，彈性查詢提供立即深入了解即時的實際執行資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-128">By distributing queries across hello tenant databases, Elastic Query provides immediate insight into live production data.</span></span> <span data-ttu-id="2ca5d-129">不過，當彈性查詢會從提取資料可能有多個資料庫，查詢延遲有時可能會高於對等查詢送出 tooa 單一多租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-129">However, as Elastic Query pulls data from potentially many databases, query latency can sometimes be higher than for equivalent queries submitted tooa single multi-tenant database.</span></span> <span data-ttu-id="2ca5d-130">設計查詢所傳回的 toominimize hello 資料時請務必小心。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-130">Care should be taken when designing queries toominimize hello data that is returned.</span></span> <span data-ttu-id="2ca5d-131">彈性查詢通常最適合查詢的即時資料，少量為相對於的 toobuilding 常用或複雜的分析查詢或報告。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-131">Elastic Query is often best suited for querying small amounts of real-time data, as opposed toobuilding frequently used or complex analytics queries or reports.</span></span> <span data-ttu-id="2ca5d-132">如果查詢不佳，請查看 hello[執行計劃](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan)toosee hello 查詢的哪個部分已經按向下 toohello 遠端資料庫，然後傳回多少資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-132">If queries don't perform well, look at hello [execution plan](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee what part of hello query has been pushed down toohello remote database and how much data is being returned.</span></span> <span data-ttu-id="2ca5d-133">需要複雜分析處理的查詢，在某些情況下透過將租用戶資料擷取到針對分析查詢最佳化的專用資料庫或資料倉儲來提供服務，可能會比較好。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-133">Queries that require complex analytical processing may be better served in some cases by extracting tenant data into a dedicated database or data warehouse optimized for analytics queries.</span></span> <span data-ttu-id="2ca5d-134">此模式會說明在 hello[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-134">This pattern is explained in hello [tenant analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md).</span></span> 

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="2ca5d-135">取得 hello Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="2ca5d-135">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="2ca5d-136">hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-136">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="2ca5d-137">[步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-137">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-ticket-sales-data"></a><span data-ttu-id="2ca5d-138">建立票證銷售資料</span><span class="sxs-lookup"><span data-stu-id="2ca5d-138">Create ticket sales data</span></span>

<span data-ttu-id="2ca5d-139">toorun 查詢更有趣的資料集，針對執行 hello 票證產生器建立票證的銷售資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-139">toorun queries against a more interesting data set, create ticket sales data by running hello ticket-generator.</span></span>

1. <span data-ttu-id="2ca5d-140">在 hello *PowerShell ISE*，開啟 hello...\\學習模組\\作業分析\\臨機操作分析\\*示範 AdhocAnalytics.ps1*指令碼，然後設定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ca5d-140">In hello *PowerShell ISE*, open hello ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* script and set hello following values:</span></span>
   * <span data-ttu-id="2ca5d-141">**$DemoScenario** = 1，**購買各地事件的票證**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-141">**$DemoScenario** = 1, **Purchase tickets for events at all venues**.</span></span>
2. <span data-ttu-id="2ca5d-142">按**F5**執行 hello 指令碼，並產生票證銷售。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-142">Press **F5** to run hello script and generate ticket sales.</span></span> <span data-ttu-id="2ca5d-143">Hello 指令碼執行時，繼續 hello 步驟在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-143">While hello script is running, continue hello steps in this tutorial.</span></span> <span data-ttu-id="2ca5d-144">hello 票券資料會查詢在 hello*執行特定分散式查詢*區段中，因此會等候 hello 票證產生器 toocomplete 時仍在執行時取得 toothat 練習。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-144">hello ticket data is queried in hello *Run ad-hoc distributed queries* section, so wait for hello ticket generator toocomplete if it's still running when you get toothat exercise.</span></span>

## <a name="explore-hello-global-views"></a><span data-ttu-id="2ca5d-145">瀏覽 hello 全域檢視</span><span class="sxs-lookup"><span data-stu-id="2ca5d-145">Explore hello global views</span></span>

<span data-ttu-id="2ca5d-146">hello Wingtip SaaS 應用程式是使用租用戶每個資料庫模型，因此 hello 租用戶資料庫結構描述會定義以單一租用戶的觀點所建立。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-146">hello Wingtip SaaS application is built using a tenant-per-database model, so hello tenant database schema is defined from a single-tenant perspective.</span></span> <span data-ttu-id="2ca5d-147">租用戶特定資訊位於一個 *Venue* 資料表中，該資料表一律有單一資料列，且會實作成一個沒有主索引鍵的堆積。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-147">Tenant-specific information exists in one table, *Venue*, which always has a single row, and is implemented as a heap, without a primary key.</span></span> <span data-ttu-id="2ca5d-148">Hello 結構描述中的其他資料表不需要 toobe 相關 toohello*法院*資料表，因為在正常使用，都不會租用戶 hello 資料屬於任何不確定。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-148">Other tables in hello schema don't need toobe related toohello *Venue* table, because in normal use, there is never any doubt which tenant hello data belongs to.</span></span>

<span data-ttu-id="2ca5d-149">不過，當跨所有資料庫查詢，務必彈性查詢可以處理 hello 資料，如同它是單一邏輯資料庫分區化依租用戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-149">However, when querying across all databases, it's important that Elastic Query can treat hello data as if it is part of a single logical database sharded by tenant.</span></span> <span data-ttu-id="2ca5d-150">tooachieve 'global' 的檢視集，這是加入的 toohello 租用戶資料庫專案的全域查詢的 hello 資料表的每個租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-150">tooachieve this, a set of 'global' views are added toohello tenant database that project a tenant id into each of hello tables that are queried globally.</span></span> <span data-ttu-id="2ca5d-151">例如，hello *VenueEvents*檢視新增計算*VenueId* toohello 資料行投射從 hello*事件*資料表。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-151">For example, hello *VenueEvents* view adds a computed *VenueId* toohello columns projected from hello *Events* table.</span></span> <span data-ttu-id="2ca5d-152">藉由定義透過 hello 外部資料庫資料表中 hello 前端*VenueEvents* (而不是基礎 hello*事件*資料表)，彈性查詢是根據聯結下的能 toopush *VenueId*讓它們可以平行執行的每個遠端的資料庫 （而不是在 hello 前端資料庫）。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-152">By defining hello external table in hello head database over *VenueEvents* (rather than hello underlying *Events* table), Elastic Query is able toopush down joins based on *VenueId* so they can be executed in parallel on each remote database (rather than on hello head database).</span></span> <span data-ttu-id="2ca5d-153">這將可大幅減少 hello 傳回，則會導致許多查詢的效能大幅增加的資料量。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-153">This dramatically reduces hello amount of data that is returned, which results in a substantial increase in performance for many queries.</span></span> <span data-ttu-id="2ca5d-154">這些全域檢視已在所有租用戶資料庫 (以及在*basetenantdb*) 中預先建立。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-154">These global views have been pre-created in all tenant databases (and in *basetenantdb*).</span></span>

1. <span data-ttu-id="2ca5d-155">開啟 SSMS 和[連接 toohello tenants1-&lt;使用者&gt;伺服器](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-155">Open SSMS and [connect toohello tenants1-&lt;USER&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).</span></span>
2. <span data-ttu-id="2ca5d-156">展開 [資料庫]，以滑鼠右鍵按一下 **contosoconcerthall**，然後選取 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-156">Expand **Databases**, right-click **contosoconcerthall**, and select **New Query**.</span></span>
3. <span data-ttu-id="2ca5d-157">執行下列查詢 tooexplore hello hello 單一租用戶資料表與差異 hello 全域檢視 hello:</span><span class="sxs-lookup"><span data-stu-id="2ca5d-157">Run hello following queries tooexplore hello difference between hello single-tenant tables and hello global views:</span></span>

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

<span data-ttu-id="2ca5d-158">在這些檢視中，hello *VenueId*計算 hello 地點名稱，而任何方法的雜湊為無法使用的 toointroduce 唯一值。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-158">In these views, hello *VenueId* is computed as a hash of hello Venue name, but any approach could be used toointroduce a unique value.</span></span> <span data-ttu-id="2ca5d-159">這個方法是 hello 租用戶金鑰計算用於 hello 目錄中的類似 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-159">This approach is similar toohello way hello tenant key is computed for use in hello catalog.</span></span>

<span data-ttu-id="2ca5d-160">hello tooexamine hello 定義*管道*檢視：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-160">tooexamine hello definition of hello *Venues* view:</span></span>

1. <span data-ttu-id="2ca5d-161">在 [物件總管] 中，展開 [contosoconcethall] > [檢視]：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-161">In **Object Explorer**, expand **contosoconcethall** > **Views**:</span></span>

   ![檢視](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. <span data-ttu-id="2ca5d-163">以滑鼠右鍵按一下 **dbo.Venues**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-163">Right-click **dbo.Venues**.</span></span>
3. <span data-ttu-id="2ca5d-164">選取 [指令碼檢視] > [CREATE To] > [新的查詢編輯器視窗]</span><span class="sxs-lookup"><span data-stu-id="2ca5d-164">Select **Script View as** > **CREATE To** > **New Query Editor Window**</span></span>

<span data-ttu-id="2ca5d-165">指令碼的任何其他 hello*法院*檢視 toosee 它們如何新增 hello *VenueId*。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-165">Script any of hello other *Venue* views toosee how they add hello *VenueId*.</span></span>

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a><span data-ttu-id="2ca5d-166">部署用來進行特定分散式查詢的 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="2ca5d-166">Deploy hello database used for ad-hoc distributed queries</span></span>

<span data-ttu-id="2ca5d-167">此練習將部署的 hello *adhocanalytics*資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-167">This exercise deploys hello *adhocanalytics* database.</span></span> <span data-ttu-id="2ca5d-168">這是 hello 的前端資料庫將會包含用來查詢所有租用戶資料庫之間的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-168">This is hello head database that will contain hello schema used for querying across all tenant databases.</span></span> <span data-ttu-id="2ca5d-169">現有的類別目錄伺服器，就是用於所有與管理相關的資料庫，hello 範例應用程式中的 hello 伺服器部署的 toohello hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-169">hello database is deployed toohello existing catalog server, which is hello server used for all management-related databases in hello sample app.</span></span>

1. <span data-ttu-id="2ca5d-170">開啟...\\學習模組\\作業分析\\臨機操作分析\\*示範 AdhocAnalytics.ps1*在 hello *PowerShell ISE*和集 hello下列值：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-170">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* in hello *PowerShell ISE* and set hello following values:</span></span>
   * <span data-ttu-id="2ca5d-171">**$DemoScenario** = 2，**部署臨機操作分析資料庫**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-171">**$DemoScenario** = 2, **Deploy Ad-hoc analytics database**.</span></span>

2. <span data-ttu-id="2ca5d-172">按**F5** toorun hello 指令碼，並建立 hello *adhocanalytics*資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-172">Press **F5** toorun hello script and create hello *adhocanalytics* database.</span></span>

<span data-ttu-id="2ca5d-173">Hello 下一節，您會加入結構描述 toohello 資料庫，以便能夠使用的 toorun 分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-173">In hello next section, you add schema toohello database so it can be used toorun distributed queries.</span></span>

## <a name="configure-hello-database-for-running-distributed-queries"></a><span data-ttu-id="2ca5d-174">設定 hello 資料庫以執行分散式的查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-174">Configure hello database for running distributed queries</span></span>

<span data-ttu-id="2ca5d-175">此練習將結構描述 （hello 外部資料來源和外部資料表定義） toohello 臨機操作分析的資料庫，可讓您跨所有租用戶資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-175">This exercise adds schema (hello external data source and external table definitions) toohello ad-hoc analytics database that enables querying across all tenant databases.</span></span>

1. <span data-ttu-id="2ca5d-176">開啟 SQL Server Management Studio，並連接 toohello hello 先前步驟中建立臨機操作分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-176">Open SQL Server Management Studio, and connect toohello Adhoc Analytics database you created in hello previous step.</span></span> <span data-ttu-id="2ca5d-177">hello hello 資料庫名稱會是 adhocanalytics。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-177">hello name of hello database will be adhocanalytics.</span></span>
2. <span data-ttu-id="2ca5d-178">在 SSMS 中開啟 ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-178">Open ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* in SSMS.</span></span>
3. <span data-ttu-id="2ca5d-179">檢閱 hello SQL 指令碼，並請注意下列 hello:</span><span class="sxs-lookup"><span data-stu-id="2ca5d-179">Review hello SQL script and note hello following:</span></span>

   <span data-ttu-id="2ca5d-180">彈性查詢會使用資料庫範圍認證 tooaccess 每個的 hello 租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-180">Elastic Query uses a database-scoped credential tooaccess each of hello tenant databases.</span></span> <span data-ttu-id="2ca5d-181">這個認證需要 toobe hello 的所有資料庫中可用以及應該通常被授與 hello 最低權限所需 tooenable 這些臨機操作查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-181">This credential needs toobe available in all hello databases and should normally be granted hello minimum rights required tooenable these ad-hoc queries.</span></span>

    ![建立認證](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   <span data-ttu-id="2ca5d-183">hello 外部資料來源被定義 toouse hello 租用戶分區對應 hello 類別目錄資料庫中。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-183">hello external data source, that is defined toouse hello tenant shard map in hello catalog database.</span></span> <span data-ttu-id="2ca5d-184">使用此選項為 hello 外部資料來源，查詢是分散式的 tooall hello 查詢執行時，在 hello 目錄中註冊的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-184">By using this as hello external data source, queries are distributed tooall databases registered in hello catalog when hello query is run.</span></span> <span data-ttu-id="2ca5d-185">因為每個部署不同的伺服器名稱，此初始化指令碼會藉由擷取 hello 目前的伺服器取得 hello 類別目錄資料庫 hello 位置 (@@servername) hello 指令碼執行的所在。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-185">Because server names are different for each deployment, this initialization script gets hello location of hello catalog database by retrieving hello current server (@@servername) where hello script is executed.</span></span>

    ![建立外部資料來源](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   <span data-ttu-id="2ca5d-187">hello 參考 hello 全域檢視 hello 上一節中所述，以定義外部資料表**發佈 = SHARDED(VenueId)**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-187">hello external tables that reference hello global views described in hello previous section, and defined with **DISTRIBUTION = SHARDED(VenueId)**.</span></span> <span data-ttu-id="2ca5d-188">因為每個*VenueId*對應 tooa 單一資料庫，這可改善效能，許多情況下的，hello 下一節中所示。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-188">Because each *VenueId* maps tooa single database, this improves performance for many scenarios as shown in hello next section.</span></span>

    ![建立外部資料表](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   <span data-ttu-id="2ca5d-190">hello 本機資料表*VenueTypes* ，會建立並填入。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-190">hello local table *VenueTypes* that is created and populated.</span></span> <span data-ttu-id="2ca5d-191">此參考資料表是在所有租用戶資料庫中，常見的因此可以表示為本機資料表並填入 hello 一般資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-191">This reference data table is common in all tenant databases, so it can be represented here as a local table and populated with hello common data.</span></span> <span data-ttu-id="2ca5d-192">這可能會降低 hello 某些查詢的資料量之間移動 hello 租用戶資料庫以及 hello *adhocanalytics*資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-192">For some queries this may reduce hello amount of data moved between hello tenant databases and hello *adhocanalytics* database.</span></span>

    ![建立資料表](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   <span data-ttu-id="2ca5d-194">如果您以這種方式包含參考資料表，是確定 tooupdate hello 資料表結構描述和資料，每當您更新 hello 租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-194">If you include reference tables in this manner, be sure tooupdate hello table schema and data whenever you update hello tenant databases.</span></span>

4. <span data-ttu-id="2ca5d-195">按**F5** toorun hello 指令碼，並初始化 hello *adhocanalytics*資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-195">Press **F5** toorun hello script and initialize hello *adhocanalytics* database.</span></span> 

<span data-ttu-id="2ca5d-196">現在您可以執行分散式查詢，然後收集所有租用戶之間的深入資訊！</span><span class="sxs-lookup"><span data-stu-id="2ca5d-196">Now you can run distributed queries, and gather insights across all tenants!</span></span>

## <a name="run-ad-hoc-distributed-queries"></a><span data-ttu-id="2ca5d-197">執行臨機操作分散式查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-197">Run ad-hoc distributed queries</span></span>

<span data-ttu-id="2ca5d-198">現在該 hello *adhocanalytics*資料庫設定，請繼續並執行一些分散式的查詢。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-198">Now that hello *adhocanalytics* database is set up, go ahead and run some distributed queries.</span></span> <span data-ttu-id="2ca5d-199">包括 hello 執行計畫更深入了解 hello 查詢處理發生的位置。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-199">Include hello execution plan for a better understanding of where hello query processing is happening.</span></span> 

<span data-ttu-id="2ca5d-200">檢查時 hello 執行計劃，將滑鼠停留在 hello 計劃圖示，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-200">When inspecting hello execution plan, hover over hello plan icons for details.</span></span> 

<span data-ttu-id="2ca5d-201">重要 toonote，為該設定**發佈 = SHARDED(VenueId)**我們定義 hello 外部資料來源，可改善效能，許多案例。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-201">Important toonote, is that setting **DISTRIBUTION = SHARDED(VenueId)** when we defined hello external data source, improves performance for many scenarios.</span></span> <span data-ttu-id="2ca5d-202">因為每個*VenueId*對應 tooa 單一資料庫中，篩選是我們所需的完成輕鬆地從遠端、 傳回唯一 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-202">Because each *VenueId* maps tooa single database, filtering is easily done remotely, returning only hello data we need.</span></span>

1. <span data-ttu-id="2ca5d-203">在 SSMS 中開啟 ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\Demo-AdhocAnalyticsQueries.sql。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-203">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.</span></span>
2. <span data-ttu-id="2ca5d-204">確保您已連線的 toohello **adhocanalytics**資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-204">Ensure you are connected toohello **adhocanalytics** database.</span></span>
3. <span data-ttu-id="2ca5d-205">選取 hello**查詢**功能表，然後按一下**包括實際執行計畫**</span><span class="sxs-lookup"><span data-stu-id="2ca5d-205">Select hello **Query** menu and click **Include Actual Execution Plan**</span></span>
4. <span data-ttu-id="2ca5d-206">反白顯示 hello*目前已註冊的管道？*查詢，然後按**F5**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-206">Highlight hello *Which venues are currently registered?* query, and press **F5**.</span></span>

   <span data-ttu-id="2ca5d-207">hello 查詢會傳回 hello 整個地點清單，說明如何快速而且容易 tooquery 整個所有租用戶和每個租用戶傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-207">hello query returns hello entire venue list, illustrating how quick and easy it is tooquery across all tenants and return data from each tenant.</span></span>

   <span data-ttu-id="2ca5d-208">檢查 hello 計劃，請參閱 hello 整個成本是 hello 遠端查詢，因為我們只是進行 tooeach 租用戶資料庫，然後選取 hello 法院資訊。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-208">Inspect hello plan and see that hello entire cost is hello remote query because we're simply going tooeach tenant database and selecting hello venue information.</span></span>

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. <span data-ttu-id="2ca5d-210">選取 hello 下一個查詢，然後按**F5**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-210">Select hello next query, and press **F5**.</span></span>

   <span data-ttu-id="2ca5d-211">此查詢會聯結資料 hello 租用戶資料庫和 hello 本機*VenueTypes*資料表 (本機，因為它是資料表中 hello *adhocanalytics*資料庫)。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-211">This query joins data from hello tenant databases and hello local *VenueTypes* table (local, as its a table in hello *adhocanalytics* database).</span></span>

   <span data-ttu-id="2ca5d-212">檢查 hello 計劃，並查看該 hello 大部分的成本是 hello 遠端查詢，因為我們查詢每個租用戶法院資訊 (dbo。管道），然後執行快速的本機聯結與 hello 本機*VenueTypes*資料表 toodisplay hello 易記名稱。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-212">Inspect hello plan and see that hello majority of cost is hello remote query because we query each tenant's venue info (dbo.Venues), and then do a quick local join with hello local *VenueTypes* table toodisplay hello friendly name.</span></span>

   ![遠端資料與本機資料的聯結](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. <span data-ttu-id="2ca5d-214">現在選取 hello*哪一天是 hello 販售的大部分票證？*查詢，然後按**F5**。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-214">Now select hello *On which day were hello most tickets sold?* query, and press **F5**.</span></span>

   <span data-ttu-id="2ca5d-215">此查詢會執行比較複雜的聯結和彙總。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-215">This query does a bit more complex joining and aggregation.</span></span> <span data-ttu-id="2ca5d-216">什麼是重要的 toonote 是遠端電腦上，完成大部分的 hello 處理，同樣地，我們會傳回唯一 hello 列我們需要傳回只每天每個地點的彙總的票證銷售計數的單一資料列。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-216">What's important toonote is that most of hello processing is done remotely, and once again, we bring back only hello rows we need, returning just a single row for each venue's aggregate ticket sale count per day.</span></span>

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a><span data-ttu-id="2ca5d-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ca5d-218">Next steps</span></span>

<span data-ttu-id="2ca5d-219">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="2ca5d-219">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="2ca5d-220">對所有租用戶資料庫執行分散式查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-220">Run distributed queries across all tenant databases</span></span>
> * <span data-ttu-id="2ca5d-221">部署特定分析資料庫，並加入 tooit toorun 分散式查詢的結構描述。</span><span class="sxs-lookup"><span data-stu-id="2ca5d-221">Deploy an ad-hoc analytics database and add schema tooit toorun distributed queries.</span></span>


<span data-ttu-id="2ca5d-222">現在，請嘗試 hello[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)tooexplore 擷取資料 tooa 個別分析資料庫以進行更複雜的分析處理...</span><span class="sxs-lookup"><span data-stu-id="2ca5d-222">Now try hello [Tenant Analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md) tooexplore extracting data tooa separate analytics database for more complex analytics processing...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ca5d-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="2ca5d-223">Additional resources</span></span>

* <span data-ttu-id="2ca5d-224">其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="2ca5d-224">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="2ca5d-225">彈性查詢</span><span class="sxs-lookup"><span data-stu-id="2ca5d-225">Elastic Query</span></span>](sql-database-elastic-query-overview.md)
