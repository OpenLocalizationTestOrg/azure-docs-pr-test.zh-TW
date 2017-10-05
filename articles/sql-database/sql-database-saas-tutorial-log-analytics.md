---
title: "使用 Log Analytics 搭配 SQL Database 多租用戶應用程式 | Microsoft Docs"
description: "設定及使用 Log Analytics (OMS) 搭配 Azure SQL Database 範例 Wingtip SaaS 應用程式"
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
ms.openlocfilehash: 26f6f519ecb3abf6343dc2776aa141dff99ced15
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="setup-and-use-log-analytics-oms-with-the-wingtip-saas-app"></a><span data-ttu-id="4ef32-104">設定及使用 Log Analytics (OMS) 搭配 Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ef32-104">Setup and use Log Analytics (OMS) with the Wingtip SaaS app</span></span>

<span data-ttu-id="4ef32-105">在本教學課程中，您會設定及使用 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*，以便監視彈性集區和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4ef32-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="4ef32-106">它是以[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)為基礎，並示範如何使用 *Log Analytics*，以增強 Azure 入口網站中提供的監視和警示功能。</span><span class="sxs-lookup"><span data-stu-id="4ef32-106">It builds on the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how to use *Log Analytics* to augment the monitoring and alerting provided in the Azure portal.</span></span> <span data-ttu-id="4ef32-107">Log Analytics 特別適合用於大規模監視和警示，因為它可支援數百個集區和數十萬個資料庫。</span><span class="sxs-lookup"><span data-stu-id="4ef32-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="4ef32-108">它也提供單一監視解決方案，可以跨多個 Azure 訂用帳戶，整合不同應用程式和 Azure 服務的監視。</span><span class="sxs-lookup"><span data-stu-id="4ef32-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="4ef32-109">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="4ef32-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ef32-110">安裝及設定 Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="4ef32-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="4ef32-111">使用 Log Analytics 來監視集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="4ef32-111">Use Log Analytics to monitor pools and databases</span></span>

<span data-ttu-id="4ef32-112">若要完成本教學課程，請確定已完成下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="4ef32-112">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="4ef32-113">已部署 Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ef32-113">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="4ef32-114">若要在五分鐘內完成部署，請參閱[部署及探索 Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="4ef32-114">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="4ef32-115">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4ef32-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="4ef32-116">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="4ef32-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="4ef32-117">請參閱[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)，以取得 SaaS 案例和模式的討論區，及其對於監視解決方案需求的影響。</span><span class="sxs-lookup"><span data-stu-id="4ef32-117">See the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of the SaaS scenarios and patterns, and how they affect the requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="4ef32-118">使用 Log Analytics (OMS) 監視和管理效能</span><span class="sxs-lookup"><span data-stu-id="4ef32-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="4ef32-119">針對 SQL Database，可使用資料庫和集區監視與警示功能。</span><span class="sxs-lookup"><span data-stu-id="4ef32-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="4ef32-120">此內建監視與警示為資源特定功能且便於處理少量資源，但比較不適合監視大型安裝，或提供橫跨不同資源和訂用帳戶的統一檢視。</span><span class="sxs-lookup"><span data-stu-id="4ef32-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited to monitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="4ef32-121">對於高容量的情況，可以使用 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="4ef32-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="4ef32-122">這是個別的 Azure 服務，可針對發出的診斷紀錄和 Log Analytics 工作區中蒐集的遙測提供分析，這可以收集來自許多服務的遙測並用來查詢和設定警示。</span><span class="sxs-lookup"><span data-stu-id="4ef32-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used to query and set alerts.</span></span> <span data-ttu-id="4ef32-123">Log Analytics 可提供內建的查詢語言和資料視覺化工具，以便進行操作資料分析和視覺化。</span><span class="sxs-lookup"><span data-stu-id="4ef32-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="4ef32-124">SQL 分析解決方案提供了數個預先定義的彈性集區及資料庫監視與警示檢視和查詢，讓您新增自己的臨機操作查詢並視需要加以儲存。</span><span class="sxs-lookup"><span data-stu-id="4ef32-124">The SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="4ef32-125">OMS 也提供自訂檢視設計工具。</span><span class="sxs-lookup"><span data-stu-id="4ef32-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="4ef32-126">您可以在 Azure 入口網站和 OMS 中開啟 Log Analytics 工作區和分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="4ef32-126">Log Analytics workspaces and analytics solutions can be opened both in the Azure portal and in OMS.</span></span> <span data-ttu-id="4ef32-127">Azure 入口網站是較新的存取點，但在某些區域可能位於 OMS 入口網站的後面。</span><span class="sxs-lookup"><span data-stu-id="4ef32-127">The Azure portal is the newer access point but may be behind the OMS portal in some areas.</span></span>

### <a name="start-the-load-generator-to-create-data-to-analyze"></a><span data-ttu-id="4ef32-128">啟動負載產生器來建立要分析的資料</span><span class="sxs-lookup"><span data-stu-id="4ef32-128">Start the load generator to create data to analyze</span></span>

1. <span data-ttu-id="4ef32-129">在 **PowerShell ISE** 中開啟 **Demo-PerformanceMonitoringAndManagement.ps1**。</span><span class="sxs-lookup"><span data-stu-id="4ef32-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in the **PowerShell ISE**.</span></span> <span data-ttu-id="4ef32-130">讓此指令碼保持開啟，因為您會在本教學課程期間執行數個負載產生案例。</span><span class="sxs-lookup"><span data-stu-id="4ef32-130">Keep this script open as you may want to run several of the load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="4ef32-131">如果您擁有少於五個租用戶，請佈建一批租用戶以提供更有趣的監視內容︰</span><span class="sxs-lookup"><span data-stu-id="4ef32-131">If you have less than five tenants, provision a batch of tenants to provide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="4ef32-132">設定 **$DemoScenario = 1**，**佈建一批租用戶**</span><span class="sxs-lookup"><span data-stu-id="4ef32-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="4ef32-133">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="4ef32-133">Press **F5** to run the script.</span></span>

1. <span data-ttu-id="4ef32-134">設定 **$DemoScenario** = 2，**產生一般強度負載 (約為 40 DTU)**。</span><span class="sxs-lookup"><span data-stu-id="4ef32-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="4ef32-135">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="4ef32-135">Press **F5** to run the script.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="4ef32-136">取得 Wingtip 應用程式指令碼</span><span class="sxs-lookup"><span data-stu-id="4ef32-136">Get the Wingtip application scripts</span></span>

<span data-ttu-id="4ef32-137">在 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) Github 存放庫可取得 Wingtip Tickets 指令碼和應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="4ef32-137">The Wingtip Tickets scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="4ef32-138">指令碼檔案位於 [[Learning Modules] 資料夾](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)中。</span><span class="sxs-lookup"><span data-stu-id="4ef32-138">Script files are located in the [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="4ef32-139">請將 **Learning Modules** 資料夾下載到您的本機電腦，並維持其資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="4ef32-139">Download the **Learning Modules** folder to your local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-the-azure-sql-analytics-solution"></a><span data-ttu-id="4ef32-140">安裝及設定 Log Analytics 和 Azure SQL 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="4ef32-140">Installing and configuring Log Analytics and the Azure SQL Analytics solution</span></span>

<span data-ttu-id="4ef32-141">Log Analytics 是需要設定的個別服務。</span><span class="sxs-lookup"><span data-stu-id="4ef32-141">Log Analytics is a separate service that needs to be configured.</span></span> <span data-ttu-id="4ef32-142">Log Analytics 會收集 Log Analytics 工作區中的記錄資料和遙測以及計量。</span><span class="sxs-lookup"><span data-stu-id="4ef32-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="4ef32-143">就像 Azure 中的其他資源一樣，工作區是必須建立的資源。</span><span class="sxs-lookup"><span data-stu-id="4ef32-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="4ef32-144">雖然工作區不一定要建立在與其監視之應用程式相同的資源群組中，但這麼做通常最有意義。</span><span class="sxs-lookup"><span data-stu-id="4ef32-144">While the workspace doesn’t need to be created in the same resource group as the application(s) it is monitoring, this often makes the most sense.</span></span> <span data-ttu-id="4ef32-145">在 Wingtip SaaS 應用程式的情況下，這可讓工作區輕鬆地與應用程式一起刪除，只要刪除資源群組即可。</span><span class="sxs-lookup"><span data-stu-id="4ef32-145">In the case of the Wingtip SaaS app, this enables the workspace to be easily deleted with the application by simply deleting the resource group.</span></span>

1. <span data-ttu-id="4ef32-146">在 **PowerShell ISE** 中開啟 ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1*。</span><span class="sxs-lookup"><span data-stu-id="4ef32-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in the **PowerShell ISE**.</span></span>
1. <span data-ttu-id="4ef32-147">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="4ef32-147">Press **F5** to run the script.</span></span>

<span data-ttu-id="4ef32-148">此時，您應可在 Azure 入口網站 (或 OMS 入口網站) 中開啟 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="4ef32-148">At this point you should be able open Log Analytics in the Azure portal (or the OMS portal).</span></span> <span data-ttu-id="4ef32-149">需要花幾分鐘的時間才能在 Log Analytics 工作區中收集遙測並顯示出來。</span><span class="sxs-lookup"><span data-stu-id="4ef32-149">It will take a few minutes for telemetry to be collected in the Log Analytics workspace and to become visible.</span></span> <span data-ttu-id="4ef32-150">您讓系統蒐集資料的時間越長，體驗將會更有趣。</span><span class="sxs-lookup"><span data-stu-id="4ef32-150">The longer you leave the system gathering data the more interesting the experience will be.</span></span> <span data-ttu-id="4ef32-151">現在是放鬆一下的好時機 - 只要確定負載產生器仍在執行中！</span><span class="sxs-lookup"><span data-stu-id="4ef32-151">Now's a good time to grab a beverage - just make sure the load generator is still running!</span></span>


## <a name="use-log-analytics-and-the-sql-analytics-solution-to-monitor-pools-and-databases"></a><span data-ttu-id="4ef32-152">使用 Log Analytics 和 SQL 分析解決方案來監視集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="4ef32-152">Use Log Analytics and the SQL Analytics solution to monitor pools and databases</span></span>


<span data-ttu-id="4ef32-153">在此練習中，開啟 Log Analytics 和 OMS 入口網站以查看針對資料庫和集區蒐集的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="4ef32-153">In this exercise, open Log Analytics and the OMS portal to look at the telemetry being gathered for the databases and pools.</span></span>

1. <span data-ttu-id="4ef32-154">瀏覽至 [Azure 入口網站](https://portal.azure.com)，按一下 [更多服務] 以開啟 Log Analytics，然後搜尋 Log Analytics︰</span><span class="sxs-lookup"><span data-stu-id="4ef32-154">Browse to the [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![開啟 Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="4ef32-156">選取名為 wtploganalytics-&lt;USER&gt; 的工作區。</span><span class="sxs-lookup"><span data-stu-id="4ef32-156">Select the workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="4ef32-157">選取 [概觀] 以在 Azure 入口網站中開啟 Log Analytics 解決方案。</span><span class="sxs-lookup"><span data-stu-id="4ef32-157">Select **Overview** to open the Log Analytics solution in the Azure portal.</span></span>
   <span data-ttu-id="4ef32-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="4ef32-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="4ef32-159">**重要**︰解決方案可能需要幾分鐘的時間才能變成作用中。</span><span class="sxs-lookup"><span data-stu-id="4ef32-159">**IMPORTANT**: It may take a couple of minutes before the solution is active.</span></span> <span data-ttu-id="4ef32-160">請耐心等候！</span><span class="sxs-lookup"><span data-stu-id="4ef32-160">Be patient!</span></span>

1. <span data-ttu-id="4ef32-161">按一下 [Azure SQL 分析] 圖格加以開啟。</span><span class="sxs-lookup"><span data-stu-id="4ef32-161">Click on the Azure SQL Analytics tile to open it.</span></span>

    ![概觀](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![分析](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="4ef32-164">解決方案刀鋒視窗中的檢視會橫向捲動，其在底部有自己的捲軸列 (視需要重新整理刀鋒視窗)。</span><span class="sxs-lookup"><span data-stu-id="4ef32-164">The view in the solution blade scrolls sideways, with its own scroll bar at the bottom (refresh the blade if needed).</span></span>

1. <span data-ttu-id="4ef32-165">若要探索各種檢視，請按一下檢視或個別資源來開啟向下鑽研總管，您可以在其中使用左上方的時間滑桿或按一下垂直列，將焦點放在較小的時間配量。</span><span class="sxs-lookup"><span data-stu-id="4ef32-165">Explore the various views by clicking on them or on individual resources to open a drill-down explorer, where you can use the time-slider in the top left or click on a vertical bar to focus in on a narrower time slice.</span></span> <span data-ttu-id="4ef32-166">在這個檢視中，您可以選取個別的資料庫或集區，將焦點放在特定的資源︰</span><span class="sxs-lookup"><span data-stu-id="4ef32-166">With this view, you can select individual databases or pools to focus on specific resources:</span></span>

    ![圖表](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="4ef32-168">回到解決方案刀鋒視窗，如果您捲動到最右邊，您會看到一些已儲存的查詢，按一下即可開啟及探索這些查詢。</span><span class="sxs-lookup"><span data-stu-id="4ef32-168">Back on the solution blade, if you scroll to the far right you will see some saved queries that you can click on to open and explore.</span></span> <span data-ttu-id="4ef32-169">您可以試著修改這些查詢，然後儲存您產生的任何有趣查詢，之後您可重新開啟查詢並使用於其他資源。</span><span class="sxs-lookup"><span data-stu-id="4ef32-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="4ef32-170">回到 Log Analytics 工作區刀鋒視窗，選取 OMS 入口網站以開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="4ef32-170">Back on the Log Analytics workspace blade, select OMS Portal to open the solution there.</span></span>

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="4ef32-172">您可以在 OMS 入口網站中設定警示。</span><span class="sxs-lookup"><span data-stu-id="4ef32-172">In the OMS portal, you can configure alerts.</span></span> <span data-ttu-id="4ef32-173">按一下資料庫 DTU 檢視的警示部分。</span><span class="sxs-lookup"><span data-stu-id="4ef32-173">Click on the alert portion of the database DTU view.</span></span>

1. <span data-ttu-id="4ef32-174">在顯示的 [記錄搜尋] 檢視中，您會看到所表示計量的長條圖。</span><span class="sxs-lookup"><span data-stu-id="4ef32-174">In the Log Search view that appears you will see a bar graph of the metrics being represented.</span></span>

    ![log search](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="4ef32-176">如果您按一下工具列中的 [警示]，您將能夠看到警示組態並可加以變更。</span><span class="sxs-lookup"><span data-stu-id="4ef32-176">If you click on Alert in the toolbar you will be able to see the alert configuration and can change it.</span></span>

    ![新增警示規則](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="4ef32-178">在 Log Analytics 和 OMS 中監視和警示是以工作區中的資料查詢為基礎，不同於每個資源刀鋒視窗上的資源特定警示。</span><span class="sxs-lookup"><span data-stu-id="4ef32-178">The monitoring and alerting in Log Analytics and OMS is based on queries over the data in the workspace, unlike the alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="4ef32-179">因此，您可以定義可查看所有資料庫的警示，而不是為每個資料庫定義一個警示。</span><span class="sxs-lookup"><span data-stu-id="4ef32-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="4ef32-180">或是撰寫可使用多種資源類型之複合查詢的警示。</span><span class="sxs-lookup"><span data-stu-id="4ef32-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="4ef32-181">查詢只會受限於工作區中可用的資料。</span><span class="sxs-lookup"><span data-stu-id="4ef32-181">Queries are only limited by the data available in the workspace.</span></span>

<span data-ttu-id="4ef32-182">SQL Database 的 Log Analytics 需根據工作區中的資料量付費。</span><span class="sxs-lookup"><span data-stu-id="4ef32-182">Log Analytics for SQL Database is charged for based on the data volume in the workspace.</span></span> <span data-ttu-id="4ef32-183">在本教學課程中，您建立了一個免費工作區，其每天的限制為 500MB。</span><span class="sxs-lookup"><span data-stu-id="4ef32-183">In this tutorial, you created a Free workspace, which is limited to 500MB per day.</span></span> <span data-ttu-id="4ef32-184">一旦達到該限制，工作區就不會再新增資料。</span><span class="sxs-lookup"><span data-stu-id="4ef32-184">Once that limit is reached data is no longer added to the workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ef32-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ef32-185">Next steps</span></span>

<span data-ttu-id="4ef32-186">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="4ef32-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ef32-187">安裝及設定 Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="4ef32-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="4ef32-188">使用 Log Analytics 來監視集區和資料庫</span><span class="sxs-lookup"><span data-stu-id="4ef32-188">Use Log Analytics to monitor pools and databases</span></span>

[<span data-ttu-id="4ef32-189">租用戶分析教學課程</span><span class="sxs-lookup"><span data-stu-id="4ef32-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="4ef32-190">其他資源</span><span class="sxs-lookup"><span data-stu-id="4ef32-190">Additional resources</span></span>

* [<span data-ttu-id="4ef32-191">以初始 Wingtip SaaS 應用程式部署為基礎的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="4ef32-191">Additional tutorials that build upon the initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="4ef32-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4ef32-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="4ef32-193">OMS</span><span class="sxs-lookup"><span data-stu-id="4ef32-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
