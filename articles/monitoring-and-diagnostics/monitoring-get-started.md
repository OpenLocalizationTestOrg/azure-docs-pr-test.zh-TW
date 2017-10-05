---
title: "開始使用 Azure 監視器 | Microsoft Docs"
description: "開始使用 Azure 監視器，深入了解資源的作業，並以資料為基礎採取動作。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: a4871cdee882fae8e43f84ce4f2fa0b4c0a8e1de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-monitor"></a><span data-ttu-id="d11a8-103">開始使用 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="d11a8-103">Get started with Azure Monitor</span></span>
<span data-ttu-id="d11a8-104">Azure 監視器是平台服務，提供監視 Azure 資源的單一來源。</span><span class="sxs-lookup"><span data-stu-id="d11a8-104">Azure Monitor is the platform service that provides a single source for monitoring Azure resources.</span></span> <span data-ttu-id="d11a8-105">您可以使用 Azure 監視器來視覺化、查詢、路由、封存及針對來自 Azure 資源的度量和記錄檔採取行動。</span><span class="sxs-lookup"><span data-stu-id="d11a8-105">With Azure Monitor, you can visualize, query, route, archive, and take action on the metrics and logs coming from resources in Azure.</span></span> <span data-ttu-id="d11a8-106">您可以利用監視入口網站刀鋒視窗、[Monitor PowerShell Cmdlets](insights-powershell-samples.md)、[Cross-Platform CLI](insights-cli-samples.md) 或 [Azure 監視器 REST API](https://msdn.microsoft.com/library/dn931943.aspx) 來使用此資料。</span><span class="sxs-lookup"><span data-stu-id="d11a8-106">You can work with this data using the Monitor portal blade, [Monitor PowerShell Cmdlets](insights-powershell-samples.md), [Cross-Platform CLI](insights-cli-samples.md), or [Azure Monitor REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span> <span data-ttu-id="d11a8-107">在本文中，我們會逐步解說幾個 Azure 監視器的重要元件，並使用入口網站進行示範。</span><span class="sxs-lookup"><span data-stu-id="d11a8-107">In this article, we walk through a few of the key components of Azure Monitor, using the portal for demonstration.</span></span>

1. <span data-ttu-id="d11a8-108">在入口網站中，瀏覽至 [更多服務] 並尋找 [監視] 選項。</span><span class="sxs-lookup"><span data-stu-id="d11a8-108">In the portal, navigate to **More services** and find the **Monitor** option.</span></span> <span data-ttu-id="d11a8-109">按一下星號圖示，將此選項新增至我的最愛清單，讓您可輕鬆從左側導覽列存取。</span><span class="sxs-lookup"><span data-stu-id="d11a8-109">Click the star icon to add this option to your favorites list so that it is always easily accessible from the left-hand navigation bar.</span></span>
   
    ![在服務清單中監視](./media/monitoring-get-started/monitor-more-services.png)
2. <span data-ttu-id="d11a8-111">按一下 [監視] 選項來開啟 [監視] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d11a8-111">Click the **Monitor** option to open up the **Monitor** blade.</span></span> <span data-ttu-id="d11a8-112">此刀鋒視窗會將您所有的監視設定和資料結合成一個彙總檢視。</span><span class="sxs-lookup"><span data-stu-id="d11a8-112">This blade brings together all your monitoring settings and data into one consolidated view.</span></span> <span data-ttu-id="d11a8-113">它會先開啟 [活動記錄檔]  區段。</span><span class="sxs-lookup"><span data-stu-id="d11a8-113">It first opens to the **Activity log** section.</span></span>
   
    ![監視刀鋒視窗瀏覽](./media/monitoring-get-started/monitor-blade-nav.png)
   
    <span data-ttu-id="d11a8-115">Azure 監視器有三個監視資料的基本類別︰[活動記錄檔]、[度量] 和 [診斷紀錄]。</span><span class="sxs-lookup"><span data-stu-id="d11a8-115">Azure Monitor has three basic categories of monitoring data: The **activity log**, **metrics**, and **diagnostic logs**.</span></span>
3. <span data-ttu-id="d11a8-116">按一下 [活動記錄檔]  確認已顯示活動記錄檔區段。</span><span class="sxs-lookup"><span data-stu-id="d11a8-116">Click **Activity log** to ensure that the activity log section is displayed.</span></span>
   
    ![活動記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    <span data-ttu-id="d11a8-118">[**活動記錄檔**](monitoring-overview-activity-logs.md)描述訂用帳戶中資源所執行的所有作業。</span><span class="sxs-lookup"><span data-stu-id="d11a8-118">The [**activity log**](monitoring-overview-activity-logs.md) describes all operations performed on resources in your subscription.</span></span> <span data-ttu-id="d11a8-119">您可以使用 [活動記錄檔] 來判斷訂用帳戶中的資源上任何建立、更新或刪除作業的「內容、對象和時間」。</span><span class="sxs-lookup"><span data-stu-id="d11a8-119">Using the Activity Log, you can determine the ‘what, who, and when’ for any create, update, or delete operations on resources in your subscription.</span></span> <span data-ttu-id="d11a8-120">例如，活動記錄檔會告訴您 Web 應用程式停止的時間，及將 Web 應用程式停止的人員。</span><span class="sxs-lookup"><span data-stu-id="d11a8-120">For example, the Activity Log tells you when a web app was stopped and who stopped it.</span></span> <span data-ttu-id="d11a8-121">活動記錄檔事件會儲存在平台中並供查詢 90 天。</span><span class="sxs-lookup"><span data-stu-id="d11a8-121">Activity Log events are stored in the platform and available to query for 90 days.</span></span>
   
    <span data-ttu-id="d11a8-122">您可以建立並儲存一般篩選的查詢，然後將最重要的查詢釘選至入口網站儀表板，這樣只要發生符合您準則的事件時就會通知您。</span><span class="sxs-lookup"><span data-stu-id="d11a8-122">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>
4. <span data-ttu-id="d11a8-123">篩選上週特定資源群組的檢視，然後按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d11a8-123">Filter the view to a particular resource group over the last week, then click the **Save** button.</span></span>
   
    ![儲存活動記錄檔查詢](./media/monitoring-get-started/monitor-act-log-save.png)
5. <span data-ttu-id="d11a8-125">現在，按一下 [釘選]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d11a8-125">Now, click the **Pin** button.</span></span>
   
    ![按一下 [釘選] 取得活動記錄檔](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    <span data-ttu-id="d11a8-127">此逐步解說中大部分的檢視皆可釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="d11a8-127">Most of the views in this walkthrough can be pinned to a dashboard.</span></span> <span data-ttu-id="d11a8-128">這可協助您在服務上建立作業資料的單一資訊來源。</span><span class="sxs-lookup"><span data-stu-id="d11a8-128">This helps you create a single source of information for operational data on your services.</span></span> 
6. <span data-ttu-id="d11a8-129">返回儀表板。</span><span class="sxs-lookup"><span data-stu-id="d11a8-129">Return to your dashboard.</span></span> <span data-ttu-id="d11a8-130">您現在可以看到查詢 (和結果數目) 顯示在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="d11a8-130">You can now see that the query (and number of results) is displayed in your dashboard.</span></span> <span data-ttu-id="d11a8-131">如果您想要快速查看最近在訂用帳戶中發生的任何高設定檔動作，這非常有用，例如：</span><span class="sxs-lookup"><span data-stu-id="d11a8-131">This is useful if you want to quickly see any high-profile actions that have occurred recently in your subscription, eg.</span></span> <span data-ttu-id="d11a8-132">已指派的新角色或已刪除的 VM。</span><span class="sxs-lookup"><span data-stu-id="d11a8-132">a new role was assigned or a VM was deleted.</span></span>
   
    ![活動記錄檔釘選到儀表板](./media/monitoring-get-started/monitor-act-log-db.png)
7. <span data-ttu-id="d11a8-134">返回 [監視] 圖格然後按一下 [度量] 區段。</span><span class="sxs-lookup"><span data-stu-id="d11a8-134">Return to the **Monitor** tile and click the **Metrics** section.</span></span> <span data-ttu-id="d11a8-135">您必須先使用刀鋒視窗頂端的下拉式選項，進行篩選及選取來選取資源。</span><span class="sxs-lookup"><span data-stu-id="d11a8-135">You first need to select a resource by filtering and selecting using the drop down options at the top of the blade.</span></span>
   
    ![度量的篩選器資源](./media/monitoring-get-started/monitor-met-filter.png)
   
    <span data-ttu-id="d11a8-137">所有 Azure 資源皆會發出[**度量**](monitoring-overview-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="d11a8-137">All Azure resources emit [**metrics**](monitoring-overview-metrics.md).</span></span> <span data-ttu-id="d11a8-138">這個檢視將所有度量結合在具單一管理平台下，讓您可以輕鬆地了解執行資源的狀況。</span><span class="sxs-lookup"><span data-stu-id="d11a8-138">This view brings together all metrics in a single pane of glass so you can easily understand how your resources are performing.</span></span>
8. <span data-ttu-id="d11a8-139">一旦您選取資源後，所有可用的度量會出現在刀鋒視窗的左邊。</span><span class="sxs-lookup"><span data-stu-id="d11a8-139">Once you have selected a resource, all available metrics appear on the left side of the blade.</span></span> <span data-ttu-id="d11a8-140">您可以選取度量並修改圖形類型和時間範圍，一次繪製多個度量圖表。</span><span class="sxs-lookup"><span data-stu-id="d11a8-140">You can chart multiple metrics at once by selecting metrics and modify the graph type and time range.</span></span> <span data-ttu-id="d11a8-141">您也可以檢視此資源上設定的所有度量警示。</span><span class="sxs-lookup"><span data-stu-id="d11a8-141">You can also view all metric alerts set on this resource.</span></span>
   
    ![Metric blade](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > <span data-ttu-id="d11a8-143">部分度量僅可藉由啟用資源上的 [Application Insights](../application-insights/app-insights-overview.md) 及/或 Windows 或 Linux Azure 診斷提供使用。</span><span class="sxs-lookup"><span data-stu-id="d11a8-143">Some metrics are only available by enabling [Application Insights](../application-insights/app-insights-overview.md) and/or Windows or Linux Azure Diagnostics on your resource.</span></span>
   > 
   > 
9. <span data-ttu-id="d11a8-144">當您對圖表感到滿意時，可以使用 [釘選]  按鈕將它釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="d11a8-144">When you are happy with your chart, you can use the **Pin** button to pin it to your dashboard.</span></span>
10. <span data-ttu-id="d11a8-145">返回 [監視] 刀鋒視窗然後按一下 [診斷記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="d11a8-145">Return to the **Monitor** blade and click **Diagnostic logs**.</span></span>
    
    ![診斷記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    <span data-ttu-id="d11a8-147">[**診斷記錄檔**](monitoring-overview-of-diagnostic-logs.md)是*由*特定資源發出的記錄檔，提供有關該資源的作業資料。</span><span class="sxs-lookup"><span data-stu-id="d11a8-147">[**Diagnostic logs**](monitoring-overview-of-diagnostic-logs.md) are logs emitted *by* a resource that provide data about the operation of that particular resource.</span></span> <span data-ttu-id="d11a8-148">例如，網路安全性群組規則計數器和邏輯應用程式工作流程記錄檔皆為診斷記錄檔的類型。</span><span class="sxs-lookup"><span data-stu-id="d11a8-148">For example, Network Security Group Rule Counters and Logic App Workflow Logs are both types of diagnostic logs.</span></span> <span data-ttu-id="d11a8-149">這些記錄檔可以儲存於儲存體帳戶、串流至事件中樞，及/或傳送至 [Log Analytics](../log-analytics/log-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d11a8-149">These logs can be stored in a storage account, streamed to an Event Hub, and/or sent to [Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="d11a8-150">Log Analytics 是 Microsoft 的營運情報產品，用以進行進階搜尋和警示。</span><span class="sxs-lookup"><span data-stu-id="d11a8-150">Log Analytics is Microsoft's operational intelligence product for advanced searching and alerting.</span></span>
    
    <span data-ttu-id="d11a8-151">在入口網站中，您可以檢視及篩選訂用帳戶中所有資源的清單，來識別它們是否已啟用診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d11a8-151">In the portal you can view and filter a list of all resources in your subscription to identify if they have diagnostic logs enabled.</span></span>
11. <span data-ttu-id="d11a8-152">按一下診斷記錄檔刀鋒視窗中的資源。</span><span class="sxs-lookup"><span data-stu-id="d11a8-152">Click a resource in the diagnostic logs blade.</span></span> <span data-ttu-id="d11a8-153">如果診斷記錄檔儲存於儲存體帳戶，您會看到每小時記錄檔的清單，可供您直接下載。</span><span class="sxs-lookup"><span data-stu-id="d11a8-153">If diagnostic logs are being stored in a storage account, you will see a list of hourly logs that you can directly download.</span></span>
    
    ![一項資源的診斷記錄檔](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    <span data-ttu-id="d11a8-155">您也可以按一下 [診斷設定]，讓您可設定或修改保存至儲存體帳戶、串流至事件中樞，或傳送至 Log Analytics 工作區的設定。</span><span class="sxs-lookup"><span data-stu-id="d11a8-155">You can also click **Diagnostic Settings**, which allows you to set up or modify your settings for archival to a storage account, streaming to Event Hubs, or sending to a Log Analytics workspace.</span></span>
    
    ![啟用診斷記錄](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    <span data-ttu-id="d11a8-157">如果您已將記錄檔分析設定至 Log Analytics，則可以在入口網站的 [搜尋]  區段中搜尋它們。</span><span class="sxs-lookup"><span data-stu-id="d11a8-157">If you have set up diagnostic logs to Log Analytics, you can then search them in the **Log search** section of the portal.</span></span>
12. <span data-ttu-id="d11a8-158">瀏覽至 [監視] 刀鋒視窗的 [警示]  區段。</span><span class="sxs-lookup"><span data-stu-id="d11a8-158">Navigate to the **Alerts** section of the Monitor blade.</span></span>
    
    ![公用警示刀鋒視窗](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    <span data-ttu-id="d11a8-160">您可以在這裡管理 Azure 資源上的所有[**警示**](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="d11a8-160">Here you can manage all [**alerts**](monitoring-overview-alerts.md) on your Azure resources.</span></span> <span data-ttu-id="d11a8-161">這包括計量、活動記錄事件、Application Insights Web 測試 (位置) 和 Application Insights 主動診斷的警示。</span><span class="sxs-lookup"><span data-stu-id="d11a8-161">This includes alerts on metrics, activity log events, Application Insights web tests (Locations), and Application Insights proactive diagnostics.</span></span> <span data-ttu-id="d11a8-162">警示可以觸發將電子郵件或 HTTP POST 傳送到 webhook。</span><span class="sxs-lookup"><span data-stu-id="d11a8-162">Alerts can trigger an email to be sent or an HTTP POST to a webhook URL.</span></span>
13. <span data-ttu-id="d11a8-163">按一下 [新增度量警示]  建立警示。</span><span class="sxs-lookup"><span data-stu-id="d11a8-163">Click **Add metric alert** to create an alert.</span></span>
    
    ![新增度量警示](./media/monitoring-get-started/monitor-alerts-add.png)
    
    <span data-ttu-id="d11a8-165">然後您可以將警示釘選到儀表板，輕鬆地隨時查看其狀態。</span><span class="sxs-lookup"><span data-stu-id="d11a8-165">You can then pin an alert to your dashboard to easily see its state at any time.</span></span>
14. <span data-ttu-id="d11a8-166">[監視] 區段也包含 [Application Insights](../application-insights/app-insights-overview.md) 應用程式和 [Log Analytics](../log-analytics/log-analytics-overview.md) 管理解決方案的連結。</span><span class="sxs-lookup"><span data-stu-id="d11a8-166">The Monitor section also includes links to [Application Insights](../application-insights/app-insights-overview.md) applications and [Log Analytics](../log-analytics/log-analytics-overview.md) management solutions.</span></span> <span data-ttu-id="d11a8-167">這些其他的 Microsoft 產品與 Azure 監視器深入整合。</span><span class="sxs-lookup"><span data-stu-id="d11a8-167">These other Microsoft products have deep integration with Azure Monitor.</span></span>
15. <span data-ttu-id="d11a8-168">如果您不使用 Application Insights 或 Log Analytics，有可能是 Azure 監視器已與您目前的監視、記錄和警示產品建立合作關係。</span><span class="sxs-lookup"><span data-stu-id="d11a8-168">If you are not using Application Insights or Log Analytics, chances are that Azure Monitor has a partnership with your current monitoring, logging, and alerting products.</span></span> <span data-ttu-id="d11a8-169">請參閱我們的 [合作夥伴頁面](monitoring-partners.md) ，取得如何進行整合的完整清單和指示。</span><span class="sxs-lookup"><span data-stu-id="d11a8-169">See our [partners page](monitoring-partners.md) for a full list and instructions for how to integrate.</span></span>

<span data-ttu-id="d11a8-170">您可以藉由執行下列步驟並將所有相關圖格釘選到儀表板，建立應用程式與基礎結構的完整檢視，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="d11a8-170">By following these steps and pinning all relevant tiles to a dashboard, you can create comprehensive views of your application and infrastructure like this one:</span></span>

![Azure 監視器儀表板](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a><span data-ttu-id="d11a8-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d11a8-172">Next Steps</span></span>
* <span data-ttu-id="d11a8-173">閱讀 [的概觀](monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d11a8-173">Read the [Overview of Azure Monitor](monitoring-overview.md)</span></span>

