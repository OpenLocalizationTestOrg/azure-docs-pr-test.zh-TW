---
title: "aaaGet 開始使用 Azure 監視器 |Microsoft 文件"
description: "開始使用 Azure 監視器 toogain 深入了解您的資源 hello 作業，並採取根據資料的動作。"
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
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a><span data-ttu-id="bd64f-103">開始使用 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="bd64f-103">Get started with Azure Monitor</span></span>
<span data-ttu-id="bd64f-104">Azure 監視器是 hello 平台服務，提供單一來源，Azure 資源的監視。</span><span class="sxs-lookup"><span data-stu-id="bd64f-104">Azure Monitor is hello platform service that provides a single source for monitoring Azure resources.</span></span> <span data-ttu-id="bd64f-105">Azure 監視，您可以以視覺化方式檢視、 查詢、 路由、 封存，並採取行動 hello 度量和來自 Azure 中的資源記錄。</span><span class="sxs-lookup"><span data-stu-id="bd64f-105">With Azure Monitor, you can visualize, query, route, archive, and take action on hello metrics and logs coming from resources in Azure.</span></span> <span data-ttu-id="bd64f-106">您可以使用使用 hello 監視入口網站刀鋒視窗中，此資料[監視 PowerShell Cmdlet](insights-powershell-samples.md)，[跨平台 CLI](insights-cli-samples.md)，或[Azure 監視 REST Api](https://msdn.microsoft.com/library/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bd64f-106">You can work with this data using hello Monitor portal blade, [Monitor PowerShell Cmdlets](insights-powershell-samples.md), [Cross-Platform CLI](insights-cli-samples.md), or [Azure Monitor REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span> <span data-ttu-id="bd64f-107">在本文中，我們逐步幾個 hello 的 Azure 監視，用於示範 hello 入口網站的主要元件。</span><span class="sxs-lookup"><span data-stu-id="bd64f-107">In this article, we walk through a few of hello key components of Azure Monitor, using hello portal for demonstration.</span></span>

1. <span data-ttu-id="bd64f-108">在 hello 入口網站中，瀏覽過**更多服務**並尋找 hello**監視器**選項。</span><span class="sxs-lookup"><span data-stu-id="bd64f-108">In hello portal, navigate too**More services** and find hello **Monitor** option.</span></span> <span data-ttu-id="bd64f-109">按一下 hello 星狀圖示 tooadd 這個選項 tooyour [我的最愛] 清單，因此一律會在 hello 左側導覽列中更容易存取。</span><span class="sxs-lookup"><span data-stu-id="bd64f-109">Click hello star icon tooadd this option tooyour favorites list so that it is always easily accessible from hello left-hand navigation bar.</span></span>
   
    ![在 hello 服務清單中監視](./media/monitoring-get-started/monitor-more-services.png)
2. <span data-ttu-id="bd64f-111">按一下 hello**監視器**向上 hello 選項 tooopen**監視器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bd64f-111">Click hello **Monitor** option tooopen up hello **Monitor** blade.</span></span> <span data-ttu-id="bd64f-112">此刀鋒視窗會將您所有的監視設定和資料結合成一個彙總檢視。</span><span class="sxs-lookup"><span data-stu-id="bd64f-112">This blade brings together all your monitoring settings and data into one consolidated view.</span></span> <span data-ttu-id="bd64f-113">它第一次開啟 toohello**活動記錄檔**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bd64f-113">It first opens toohello **Activity log** section.</span></span>
   
    ![監視刀鋒視窗瀏覽](./media/monitoring-get-started/monitor-blade-nav.png)
   
    <span data-ttu-id="bd64f-115">Azure 監視有三個監視資料的基本分類： hello**活動記錄檔**，**度量**，和**診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="bd64f-115">Azure Monitor has three basic categories of monitoring data: hello **activity log**, **metrics**, and **diagnostic logs**.</span></span>
3. <span data-ttu-id="bd64f-116">按一下**活動記錄檔**hello 活動記錄檔區段的 tooensure 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bd64f-116">Click **Activity log** tooensure that hello activity log section is displayed.</span></span>
   
    ![活動記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    <span data-ttu-id="bd64f-118">hello [**活動記錄檔**](monitoring-overview-activity-logs.md)描述您的訂用帳戶中的資源上執行的所有作業。</span><span class="sxs-lookup"><span data-stu-id="bd64f-118">hello [**activity log**](monitoring-overview-activity-logs.md) describes all operations performed on resources in your subscription.</span></span> <span data-ttu-id="bd64f-119">使用 hello 活動記錄檔，您可以決定 hello '功能，對象、 及何時' 用於任何建立、 更新或刪除您的訂用帳戶中的資源上的作業。</span><span class="sxs-lookup"><span data-stu-id="bd64f-119">Using hello Activity Log, you can determine hello ‘what, who, and when’ for any create, update, or delete operations on resources in your subscription.</span></span> <span data-ttu-id="bd64f-120">比方說，hello 活動記錄檔會告知您，當 web 應用程式已停止，而且使用者已停止。</span><span class="sxs-lookup"><span data-stu-id="bd64f-120">For example, hello Activity Log tells you when a web app was stopped and who stopped it.</span></span> <span data-ttu-id="bd64f-121">活動記錄檔事件會儲存在 hello 平台和可用 tooquery 90 天。</span><span class="sxs-lookup"><span data-stu-id="bd64f-121">Activity Log events are stored in hello platform and available tooquery for 90 days.</span></span>
   
    <span data-ttu-id="bd64f-122">您可以建立及儲存查詢的一般篩選器，然後 pin hello 最重要查詢 tooa 入口網站儀表板，就一定會知道是否發生符合您準則的事件。</span><span class="sxs-lookup"><span data-stu-id="bd64f-122">You can create and save queries for common filters, then pin hello most important queries tooa portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>
4. <span data-ttu-id="bd64f-123">透過 hello 過去一週，篩選 hello 檢視 tooa 特定資源群組，然後按一下 [hello**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bd64f-123">Filter hello view tooa particular resource group over hello last week, then click hello **Save** button.</span></span>
   
    ![儲存活動記錄檔查詢](./media/monitoring-get-started/monitor-act-log-save.png)
5. <span data-ttu-id="bd64f-125">現在，按一下 [hello **Pin** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bd64f-125">Now, click hello **Pin** button.</span></span>
   
    ![按一下 [釘選] 取得活動記錄檔](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    <span data-ttu-id="bd64f-127">大部分的此逐步解說中的 hello 檢視可以是已釘選的 tooa 儀表板。</span><span class="sxs-lookup"><span data-stu-id="bd64f-127">Most of hello views in this walkthrough can be pinned tooa dashboard.</span></span> <span data-ttu-id="bd64f-128">這可協助您在服務上建立作業資料的單一資訊來源。</span><span class="sxs-lookup"><span data-stu-id="bd64f-128">This helps you create a single source of information for operational data on your services.</span></span> 
6. <span data-ttu-id="bd64f-129">傳回 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="bd64f-129">Return tooyour dashboard.</span></span> <span data-ttu-id="bd64f-130">您現在可以看到您儀表板中會顯示 hello 查詢 （和結果數目）。</span><span class="sxs-lookup"><span data-stu-id="bd64f-130">You can now see that hello query (and number of results) is displayed in your dashboard.</span></span> <span data-ttu-id="bd64f-131">這非常有用，如果您想 tooquickly，請參閱中所發生最近您訂用帳戶，例如任何很重要的動作。</span><span class="sxs-lookup"><span data-stu-id="bd64f-131">This is useful if you want tooquickly see any high-profile actions that have occurred recently in your subscription, eg.</span></span> <span data-ttu-id="bd64f-132">已指派的新角色或已刪除的 VM。</span><span class="sxs-lookup"><span data-stu-id="bd64f-132">a new role was assigned or a VM was deleted.</span></span>
   
    ![活動記錄檔已釘選 toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. <span data-ttu-id="bd64f-134">傳回 toohello**監視器**磚，按一下 hello**度量**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bd64f-134">Return toohello **Monitor** tile and click hello **Metrics** section.</span></span> <span data-ttu-id="bd64f-135">您必須先 tooselect 資源篩選，然後選取 [使用在 hello hello 刀鋒視窗頂端的 hello] 下拉式清單選項。</span><span class="sxs-lookup"><span data-stu-id="bd64f-135">You first need tooselect a resource by filtering and selecting using hello drop down options at hello top of hello blade.</span></span>
   
    ![度量的篩選器資源](./media/monitoring-get-started/monitor-met-filter.png)
   
    <span data-ttu-id="bd64f-137">所有 Azure 資源皆會發出[**度量**](monitoring-overview-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="bd64f-137">All Azure resources emit [**metrics**](monitoring-overview-metrics.md).</span></span> <span data-ttu-id="bd64f-138">這個檢視將所有度量結合在具單一管理平台下，讓您可以輕鬆地了解執行資源的狀況。</span><span class="sxs-lookup"><span data-stu-id="bd64f-138">This view brings together all metrics in a single pane of glass so you can easily understand how your resources are performing.</span></span>
8. <span data-ttu-id="bd64f-139">一旦您選取的資源，所有可用的度量會出現在 hello hello 刀鋒視窗的左邊。</span><span class="sxs-lookup"><span data-stu-id="bd64f-139">Once you have selected a resource, all available metrics appear on hello left side of hello blade.</span></span> <span data-ttu-id="bd64f-140">您可以一次選取度量圖表多種度量資訊，並修改 hello 圖形類型和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="bd64f-140">You can chart multiple metrics at once by selecting metrics and modify hello graph type and time range.</span></span> <span data-ttu-id="bd64f-141">您也可以檢視此資源上設定的所有度量警示。</span><span class="sxs-lookup"><span data-stu-id="bd64f-141">You can also view all metric alerts set on this resource.</span></span>
   
    ![Metric blade](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > <span data-ttu-id="bd64f-143">部分度量僅可藉由啟用資源上的 [Application Insights](../application-insights/app-insights-overview.md) 及/或 Windows 或 Linux Azure 診斷提供使用。</span><span class="sxs-lookup"><span data-stu-id="bd64f-143">Some metrics are only available by enabling [Application Insights](../application-insights/app-insights-overview.md) and/or Windows or Linux Azure Diagnostics on your resource.</span></span>
   > 
   > 
9. <span data-ttu-id="bd64f-144">當您滿意您的圖表時，您可以使用 hello **Pin**按鈕 toopin 它 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="bd64f-144">When you are happy with your chart, you can use hello **Pin** button toopin it tooyour dashboard.</span></span>
10. <span data-ttu-id="bd64f-145">傳回 toohello**監視器**刀鋒視窗，然後按一下**診斷記錄**。</span><span class="sxs-lookup"><span data-stu-id="bd64f-145">Return toohello **Monitor** blade and click **Diagnostic logs**.</span></span>
    
    ![診斷記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    <span data-ttu-id="bd64f-147">[**診斷記錄檔**](monitoring-overview-of-diagnostic-logs.md)是記錄發出*由*提供該特定資源的 hello 作業的相關資料的資源。</span><span class="sxs-lookup"><span data-stu-id="bd64f-147">[**Diagnostic logs**](monitoring-overview-of-diagnostic-logs.md) are logs emitted *by* a resource that provide data about hello operation of that particular resource.</span></span> <span data-ttu-id="bd64f-148">例如，網路安全性群組規則計數器和邏輯應用程式工作流程記錄檔皆為診斷記錄檔的類型。</span><span class="sxs-lookup"><span data-stu-id="bd64f-148">For example, Network Security Group Rule Counters and Logic App Workflow Logs are both types of diagnostic logs.</span></span> <span data-ttu-id="bd64f-149">這些記錄檔可以是儲存在儲存體帳戶，資料流處理 tooan 事件中樞和/或傳送太[記錄分析](../log-analytics/log-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bd64f-149">These logs can be stored in a storage account, streamed tooan Event Hub, and/or sent too[Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="bd64f-150">Log Analytics 是 Microsoft 的營運情報產品，用以進行進階搜尋和警示。</span><span class="sxs-lookup"><span data-stu-id="bd64f-150">Log Analytics is Microsoft's operational intelligence product for advanced searching and alerting.</span></span>
    
    <span data-ttu-id="bd64f-151">Hello 入口網站中，您可以檢視和篩選的所有資源的清單中訂用帳戶 tooidentify，如果他們已啟用的診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bd64f-151">In hello portal you can view and filter a list of all resources in your subscription tooidentify if they have diagnostic logs enabled.</span></span>
11. <span data-ttu-id="bd64f-152">按一下 hello 診斷記錄檔 刀鋒視窗中的資源。</span><span class="sxs-lookup"><span data-stu-id="bd64f-152">Click a resource in hello diagnostic logs blade.</span></span> <span data-ttu-id="bd64f-153">如果診斷記錄檔儲存於儲存體帳戶，您會看到每小時記錄檔的清單，可供您直接下載。</span><span class="sxs-lookup"><span data-stu-id="bd64f-153">If diagnostic logs are being stored in a storage account, you will see a list of hourly logs that you can directly download.</span></span>
    
    ![一項資源的診斷記錄檔](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    <span data-ttu-id="bd64f-155">您也可以按一下**診斷設定**，這可讓您設定的 tooset 或修改設定封存 tooa 儲存體帳戶，串流 tooEvent 集線器或傳送 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="bd64f-155">You can also click **Diagnostic Settings**, which allows you tooset up or modify your settings for archival tooa storage account, streaming tooEvent Hubs, or sending tooa Log Analytics workspace.</span></span>
    
    ![啟用診斷記錄](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    <span data-ttu-id="bd64f-157">如果您已經設定診斷記錄檔 tooLog 分析，您即可搜尋它們在 hello**記錄搜尋**hello 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="bd64f-157">If you have set up diagnostic logs tooLog Analytics, you can then search them in hello **Log search** section of hello portal.</span></span>
12. <span data-ttu-id="bd64f-158">瀏覽 toohello**警示**hello 監視器 刀鋒視窗的區段。</span><span class="sxs-lookup"><span data-stu-id="bd64f-158">Navigate toohello **Alerts** section of hello Monitor blade.</span></span>
    
    ![公用警示刀鋒視窗](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    <span data-ttu-id="bd64f-160">您可以在這裡管理 Azure 資源上的所有[**警示**](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="bd64f-160">Here you can manage all [**alerts**](monitoring-overview-alerts.md) on your Azure resources.</span></span> <span data-ttu-id="bd64f-161">這包括計量、活動記錄事件、Application Insights Web 測試 (位置) 和 Application Insights 主動診斷的警示。</span><span class="sxs-lookup"><span data-stu-id="bd64f-161">This includes alerts on metrics, activity log events, Application Insights web tests (Locations), and Application Insights proactive diagnostics.</span></span> <span data-ttu-id="bd64f-162">傳送電子郵件 toobe 或 HTTP POST tooa webhook URL，可以觸發警示。</span><span class="sxs-lookup"><span data-stu-id="bd64f-162">Alerts can trigger an email toobe sent or an HTTP POST tooa webhook URL.</span></span>
13. <span data-ttu-id="bd64f-163">按一下**新增度量的警示**toocreate 警示。</span><span class="sxs-lookup"><span data-stu-id="bd64f-163">Click **Add metric alert** toocreate an alert.</span></span>
    
    ![新增度量警示](./media/monitoring-get-started/monitor-alerts-add.png)
    
    <span data-ttu-id="bd64f-165">接著，您可以釘選的警示 tooyour 儀表板 tooeasily 隨時查看其狀態。</span><span class="sxs-lookup"><span data-stu-id="bd64f-165">You can then pin an alert tooyour dashboard tooeasily see its state at any time.</span></span>
14. <span data-ttu-id="bd64f-166">hello 監視器 > 一節也包含連結太[Application Insights](../application-insights/app-insights-overview.md)應用程式和[記錄分析](../log-analytics/log-analytics-overview.md)管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd64f-166">hello Monitor section also includes links too[Application Insights](../application-insights/app-insights-overview.md) applications and [Log Analytics](../log-analytics/log-analytics-overview.md) management solutions.</span></span> <span data-ttu-id="bd64f-167">這些其他的 Microsoft 產品與 Azure 監視器深入整合。</span><span class="sxs-lookup"><span data-stu-id="bd64f-167">These other Microsoft products have deep integration with Azure Monitor.</span></span>
15. <span data-ttu-id="bd64f-168">如果您不使用 Application Insights 或 Log Analytics，有可能是 Azure 監視器已與您目前的監視、記錄和警示產品建立合作關係。</span><span class="sxs-lookup"><span data-stu-id="bd64f-168">If you are not using Application Insights or Log Analytics, chances are that Azure Monitor has a partnership with your current monitoring, logging, and alerting products.</span></span> <span data-ttu-id="bd64f-169">請參閱我們[夥伴頁面](monitoring-partners.md)的完整清單以及有關如何 toointegrate。</span><span class="sxs-lookup"><span data-stu-id="bd64f-169">See our [partners page](monitoring-partners.md) for a full list and instructions for how toointegrate.</span></span>

<span data-ttu-id="bd64f-170">藉由執行下列步驟和所有相關的磚 tooa 儀表板釘選，您可以建立應用程式和基礎結構，這類的完整的檢視：</span><span class="sxs-lookup"><span data-stu-id="bd64f-170">By following these steps and pinning all relevant tiles tooa dashboard, you can create comprehensive views of your application and infrastructure like this one:</span></span>

![Azure 監視器儀表板](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a><span data-ttu-id="bd64f-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd64f-172">Next Steps</span></span>
* <span data-ttu-id="bd64f-173">讀取 hello [Azure 監視器概觀](monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd64f-173">Read hello [Overview of Azure Monitor](monitoring-overview.md)</span></span>

