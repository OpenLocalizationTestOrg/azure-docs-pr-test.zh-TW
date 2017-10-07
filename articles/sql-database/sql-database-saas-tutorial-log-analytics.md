---
title: "使用 SQL 資料庫的多租用戶應用程式的記錄分析 aaaUse |Microsoft 文件"
description: "設定並使用與 hello Azure SQL Database 範例 Wingtip SaaS 應用程式的記錄分析 (OMS)"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a><span data-ttu-id="5a7a9-104">設定並使用與 hello Wingtip SaaS 應用程式的記錄分析 (OMS)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-104">Setup and use Log Analytics (OMS) with hello Wingtip SaaS app</span></span>

<span data-ttu-id="5a7a9-105">在本教學課程中，您會設定及使用 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*，以便監視彈性集區和資料庫。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="5a7a9-106">它是在 hello 基礎[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)，並示範如何 toouse*記錄分析*hello Azure 入口網站中提供的 tooaugment hello 監視和警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-106">It builds on hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how toouse *Log Analytics* tooaugment hello monitoring and alerting provided in hello Azure portal.</span></span> <span data-ttu-id="5a7a9-107">Log Analytics 特別適合用於大規模監視和警示，因為它可支援數百個集區和數十萬個資料庫。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="5a7a9-108">它也提供單一監視解決方案，可以跨多個 Azure 訂用帳戶，整合不同應用程式和 Azure 服務的監視。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="5a7a9-109">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a7a9-110">安裝及設定 Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="5a7a9-111">使用記錄分析 toomonitor 集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="5a7a9-111">Use Log Analytics toomonitor pools and databases</span></span>

<span data-ttu-id="5a7a9-112">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-112">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="5a7a9-113">hello Wingtip SaaS 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-113">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="5a7a9-114">toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-114">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="5a7a9-115">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="5a7a9-116">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="5a7a9-117">請參閱 hello[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)hello SaaS 案例和模式，以及它們如何影響 hello 需求上監控解決方案的討論。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-117">See hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of hello SaaS scenarios and patterns, and how they affect hello requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="5a7a9-118">使用 Log Analytics (OMS) 監視和管理效能</span><span class="sxs-lookup"><span data-stu-id="5a7a9-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="5a7a9-119">針對 SQL Database，可使用資料庫和集區監視與警示功能。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="5a7a9-120">監視和警示，此內建特定資源且方便的數量不多的資源，但較不適合的 toomonitoring 大型的安裝或在不同的資源和訂用帳戶提供統一的檢視。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited toomonitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="5a7a9-121">對於高容量的情況，可以使用 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="5a7a9-122">這是不同的 Azure 服務，以提供分析發出診斷記錄檔，可以從許多收集遙測記錄分析工作區中收集的遙測服務與要使用的 tooquery，設定警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used tooquery and set alerts.</span></span> <span data-ttu-id="5a7a9-123">Log Analytics 可提供內建的查詢語言和資料視覺化工具，以便進行操作資料分析和視覺化。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="5a7a9-124">hello SQL 分析解決方案提供了許多預先定義的彈性集區和資料庫的監視和警示檢視和查詢，並可讓您新增您自己的臨機操作查詢，並視需要儲存這些。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-124">hello SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="5a7a9-125">OMS 也提供自訂檢視設計工具。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="5a7a9-126">Hello Azure 入口網站中，在 OMS 中，您可以開啟記錄分析工作區和分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-126">Log Analytics workspaces and analytics solutions can be opened both in hello Azure portal and in OMS.</span></span> <span data-ttu-id="5a7a9-127">hello Azure 入口網站是 hello 較新存取點，但動作可能落後 hello OMS 入口網站上某些區域中。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-127">hello Azure portal is hello newer access point but may be behind hello OMS portal in some areas.</span></span>

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a><span data-ttu-id="5a7a9-128">啟動 hello 負載產生器 toocreate 資料 tooanalyze</span><span class="sxs-lookup"><span data-stu-id="5a7a9-128">Start hello load generator toocreate data tooanalyze</span></span>

1. <span data-ttu-id="5a7a9-129">開啟**示範 PerformanceMonitoringAndManagement.ps1**在 hello **PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in hello **PowerShell ISE**.</span></span> <span data-ttu-id="5a7a9-130">保持此指令碼開啟您可能會想 toorun 幾個 hello 負載產生案例在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-130">Keep this script open as you may want toorun several of hello load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="5a7a9-131">如果您有不超過五個租用戶，佈建租用戶 tooprovide 更有趣的監視內容的批次：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-131">If you have less than five tenants, provision a batch of tenants tooprovide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="5a7a9-132">設定 **$DemoScenario = 1**，**佈建一批租用戶**</span><span class="sxs-lookup"><span data-stu-id="5a7a9-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="5a7a9-133">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-133">Press **F5** toorun hello script.</span></span>

1. <span data-ttu-id="5a7a9-134">設定 **$DemoScenario** = 2，**產生一般強度負載 (約為 40 DTU)**。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="5a7a9-135">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-135">Press **F5** toorun hello script.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="5a7a9-136">取得 hello Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="5a7a9-136">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="5a7a9-137">hello Wingtip 票證指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-137">hello Wingtip Tickets scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="5a7a9-138">指令碼檔位於 hello[學習模組資料夾](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-138">Script files are located in hello [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="5a7a9-139">下載 hello**學習模組**資料夾 tooyour 本機電腦，維護它的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-139">Download hello **Learning Modules** folder tooyour local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a><span data-ttu-id="5a7a9-140">安裝和設定記錄分析 hello Azure SQL 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="5a7a9-140">Installing and configuring Log Analytics and hello Azure SQL Analytics solution</span></span>

<span data-ttu-id="5a7a9-141">記錄分析是個別的服務需要 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-141">Log Analytics is a separate service that needs toobe configured.</span></span> <span data-ttu-id="5a7a9-142">Log Analytics 會收集 Log Analytics 工作區中的記錄資料和遙測以及計量。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="5a7a9-143">就像 Azure 中的其他資源一樣，工作區是必須建立的資源。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="5a7a9-144">雖然 hello 工作區不需要 toobe hello 中建立相同的資源群組作為其監視的 hello 應用程式，這通常最有意義 hello。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-144">While hello workspace doesn’t need toobe created in hello same resource group as hello application(s) it is monitoring, this often makes hello most sense.</span></span> <span data-ttu-id="5a7a9-145">在 hello 案例中的 hello Wingtip SaaS 應用程式，這可讓 hello 工作區 toobe 輕易刪除與 hello 應用程式只要刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-145">In hello case of hello Wingtip SaaS app, this enables hello workspace toobe easily deleted with hello application by simply deleting hello resource group.</span></span>

1. <span data-ttu-id="5a7a9-146">開啟...\\學習模組\\效能監視與管理\\記錄分析\\*示範 LogAnalytics.ps1*在 hello **PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in hello **PowerShell ISE**.</span></span>
1. <span data-ttu-id="5a7a9-147">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-147">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="5a7a9-148">此時您應該可以開啟的記錄分析 hello Azure 入口網站 （或 hello OMS 入口網站） 中。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-148">At this point you should be able open Log Analytics in hello Azure portal (or hello OMS portal).</span></span> <span data-ttu-id="5a7a9-149">需要幾分鐘，讓 hello 記錄分析工作區和 toobecome 可見中收集的遙測 toobe。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-149">It will take a few minutes for telemetry toobe collected in hello Log Analytics workspace and toobecome visible.</span></span> <span data-ttu-id="5a7a9-150">將會是較長保留 hello 系統收集資料 hello 更有趣的 hello 經驗 hello。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-150">hello longer you leave hello system gathering data hello more interesting hello experience will be.</span></span> <span data-ttu-id="5a7a9-151">現在是 toograb 飲料-只是確定 hello 負載產生器仍在執行的好時機 ！</span><span class="sxs-lookup"><span data-stu-id="5a7a9-151">Now's a good time toograb a beverage - just make sure hello load generator is still running!</span></span>


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a><span data-ttu-id="5a7a9-152">使用記錄分析和 hello SQL 分析方案 toomonitor 集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="5a7a9-152">Use Log Analytics and hello SQL Analytics solution toomonitor pools and databases</span></span>


<span data-ttu-id="5a7a9-153">在此練習中，開啟 記錄分析和 hello OMS 入口網站 toolook 在 hello hello 資料庫和集區所收集的遙測。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-153">In this exercise, open Log Analytics and hello OMS portal toolook at hello telemetry being gathered for hello databases and pools.</span></span>

1. <span data-ttu-id="5a7a9-154">瀏覽 toohello [Azure 入口網站](https://portal.azure.com)然後按一下 更多服務，以開啟記錄分析記錄分析搜尋：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-154">Browse toohello [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![開啟 Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="5a7a9-156">選取名為 hello 工作區*wtploganalytics-&lt;使用者&gt;*。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-156">Select hello workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="5a7a9-157">選取**概觀**tooopen hello hello Azure 入口網站中的記錄分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-157">Select **Overview** tooopen hello Log Analytics solution in hello Azure portal.</span></span>
   <span data-ttu-id="5a7a9-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="5a7a9-159">**重要**： 可能需要幾分鐘的時間才能 hello 方案為作用中。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-159">**IMPORTANT**: It may take a couple of minutes before hello solution is active.</span></span> <span data-ttu-id="5a7a9-160">請耐心等候！</span><span class="sxs-lookup"><span data-stu-id="5a7a9-160">Be patient!</span></span>

1. <span data-ttu-id="5a7a9-161">按一下 hello Azure SQL 分析磚 tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-161">Click on hello Azure SQL Analytics tile tooopen it.</span></span>

    ![概觀](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![分析](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="5a7a9-164">hello hello 方案刀鋒視窗中捲動兩側中的檢視與它自己的捲軸在 hello 下方 （重新整理 hello 刀鋒視窗中如有需要）。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-164">hello view in hello solution blade scrolls sideways, with its own scroll bar at hello bottom (refresh hello blade if needed).</span></span>

1. <span data-ttu-id="5a7a9-165">Hello，即可在它們或個別資源 tooopen 上向下鑽研總管 中，您可以在其中使用中 hello hello 時間滑動軸的各種檢視排名最前面的左邊，或按一下瀏覽垂直列中的 toofocus 上較窄的時間配量。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-165">Explore hello various views by clicking on them or on individual resources tooopen a drill-down explorer, where you can use hello time-slider in hello top left or click on a vertical bar toofocus in on a narrower time slice.</span></span> <span data-ttu-id="5a7a9-166">與此檢視中，您可以選取個別的資料庫或集區 toofocus 特定資源上：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-166">With this view, you can select individual databases or pools toofocus on specific resources:</span></span>

    ![圖表](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="5a7a9-168">在 hello 方案刀鋒視窗中，當您捲動 toohello 最右側您會看到一些儲存的查詢，您可以按一下 tooopen，然後瀏覽。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-168">Back on hello solution blade, if you scroll toohello far right you will see some saved queries that you can click on tooopen and explore.</span></span> <span data-ttu-id="5a7a9-169">您可以試著修改這些查詢，然後儲存您產生的任何有趣查詢，之後您可重新開啟查詢並使用於其他資源。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="5a7a9-170">在 hello 記錄分析工作區刀鋒視窗中，選取 OMS 入口網站 tooopen hello 方案那里。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-170">Back on hello Log Analytics workspace blade, select OMS Portal tooopen hello solution there.</span></span>

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="5a7a9-172">在 hello OMS 入口網站，您可以設定警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-172">In hello OMS portal, you can configure alerts.</span></span> <span data-ttu-id="5a7a9-173">按一下 hello 的 hello 資料庫 DTU 檢視警示的部分。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-173">Click on hello alert portion of hello database DTU view.</span></span>

1. <span data-ttu-id="5a7a9-174">在 hello 記錄搜尋出現您的檢視，會看到 hello 度量所表示的橫條圖。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-174">In hello Log Search view that appears you will see a bar graph of hello metrics being represented.</span></span>

    ![log search](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="5a7a9-176">如果您在 [hello] 工具列中按一下警示您將會無法 toosee hello 警示設定，而且可以變更它。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-176">If you click on Alert in hello toolbar you will be able toosee hello alert configuration and can change it.</span></span>

    ![新增警示規則](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="5a7a9-178">監視和警示記錄分析和 OMS 中的 hello 根據查詢中，透過 hello hello 的工作區中，不同於 hello 每個資源刀鋒視窗中，也就是資源特定的警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-178">hello monitoring and alerting in Log Analytics and OMS is based on queries over hello data in hello workspace, unlike hello alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="5a7a9-179">因此，您可以定義可查看所有資料庫的警示，而不是為每個資料庫定義一個警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="5a7a9-180">或是撰寫可使用多種資源類型之複合查詢的警示。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="5a7a9-181">查詢只會受到 hello hello 工作區中可用的資料。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-181">Queries are only limited by hello data available in hello workspace.</span></span>

<span data-ttu-id="5a7a9-182">記錄分析的 SQL 資料庫的計費根據 hello hello 工作區中的資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-182">Log Analytics for SQL Database is charged for based on hello data volume in hello workspace.</span></span> <span data-ttu-id="5a7a9-183">在此教學課程中，您建立可用的工作區中，這是每日限制的 too500MB。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-183">In this tutorial, you created a Free workspace, which is limited too500MB per day.</span></span> <span data-ttu-id="5a7a9-184">一旦達到該限制的資料不會再加入 toohello 工作區。</span><span class="sxs-lookup"><span data-stu-id="5a7a9-184">Once that limit is reached data is no longer added toohello workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a7a9-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a7a9-185">Next steps</span></span>

<span data-ttu-id="5a7a9-186">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="5a7a9-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a7a9-187">安裝及設定 Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="5a7a9-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="5a7a9-188">使用記錄分析 toomonitor 集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="5a7a9-188">Use Log Analytics toomonitor pools and databases</span></span>

[<span data-ttu-id="5a7a9-189">租用戶分析教學課程</span><span class="sxs-lookup"><span data-stu-id="5a7a9-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="5a7a9-190">其他資源</span><span class="sxs-lookup"><span data-stu-id="5a7a9-190">Additional resources</span></span>

* [<span data-ttu-id="5a7a9-191">Hello 初始 Wingtip SaaS 應用程式部署為基礎的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="5a7a9-191">Additional tutorials that build upon hello initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="5a7a9-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5a7a9-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="5a7a9-193">OMS</span><span class="sxs-lookup"><span data-stu-id="5a7a9-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
