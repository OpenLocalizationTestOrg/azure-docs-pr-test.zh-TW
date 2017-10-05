---
title: "監視 Azure Web 應用程式效能 |Microsoft Docs"
description: "Azure Web 應用程式的應用程式效能監視。 圖表載入和回應時間、相依性資訊以及設定效能警示。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="63e1d-104">監視 Azure Web 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="63e1d-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="63e1d-105">在 [Azure 入口網站](https://portal.azure.com)中，您可以為 [Azure Web 應用程式](../app-service-web/app-service-web-overview.md)設定應用程式效能監視。</span><span class="sxs-lookup"><span data-stu-id="63e1d-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="63e1d-106">[Azure Application Insights](app-insights-overview.md) 會檢測您的應用程式，將其活動的相關遙測傳送給 Application Insights 服務，以在其中儲存和分析遙測。</span><span class="sxs-lookup"><span data-stu-id="63e1d-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="63e1d-107">該處的度量圖表和搜尋工具可用於協助診斷問題、改善效能，以及評估使用方式。</span><span class="sxs-lookup"><span data-stu-id="63e1d-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="63e1d-108">執行階段或建置階段</span><span class="sxs-lookup"><span data-stu-id="63e1d-108">Run time or build time</span></span>
<span data-ttu-id="63e1d-109">您可以用任一種方式檢測應用程式，進而設定監視︰</span><span class="sxs-lookup"><span data-stu-id="63e1d-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="63e1d-110">**執行階段** - 您可以在 Web 應用程式已經上線時，選取效能監視延伸模組。</span><span class="sxs-lookup"><span data-stu-id="63e1d-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="63e1d-111">不需要重建或重新安裝您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e1d-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="63e1d-112">您會取得一組標準封裝，用以監視回應時間、成功率、例外狀況、相依性等。</span><span class="sxs-lookup"><span data-stu-id="63e1d-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="63e1d-113">**建置階段** - 您可以在開發應用程式中安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="63e1d-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="63e1d-114">此選項比較靈活。</span><span class="sxs-lookup"><span data-stu-id="63e1d-114">This option is more versatile.</span></span> <span data-ttu-id="63e1d-115">除了相同的標準封裝以外，您可以撰寫程式碼以自訂遙測，或傳送自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="63e1d-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="63e1d-116">您可以根據您的應用程式網域，記錄特定活動或記錄事件。</span><span class="sxs-lookup"><span data-stu-id="63e1d-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="63e1d-117">使用 Application Insights 執行時間檢測</span><span class="sxs-lookup"><span data-stu-id="63e1d-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="63e1d-118">如果您已在 Azure 中執行 Web 應用程式，您便已得到一些監視︰要求率和錯誤率。</span><span class="sxs-lookup"><span data-stu-id="63e1d-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="63e1d-119">新增 Application Insights 可得到更多監視，例如回應時間、監視相依性呼叫、智慧偵測，以及強大的 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="63e1d-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="63e1d-120">在 Web 應用程式的 Azure 控制台中**選取 Application Insights**。</span><span class="sxs-lookup"><span data-stu-id="63e1d-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![在 [監視] 之下，選擇 Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="63e1d-122">除非您已經由其他途徑為此應用程式設定 Application Insights 資源，否則請選擇建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="63e1d-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="63e1d-123">安裝 Application Insights 之後，**檢測您的 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63e1d-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![檢測 Web 應用程式](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="63e1d-125">針對頁面檢視和使用者遙測**啟用用戶端監視**。</span><span class="sxs-lookup"><span data-stu-id="63e1d-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="63e1d-126">選取 [設定] > [應用程式設定]</span><span class="sxs-lookup"><span data-stu-id="63e1d-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="63e1d-127">在 [應用程式設定] 之下，新增索引鍵值組︰</span><span class="sxs-lookup"><span data-stu-id="63e1d-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="63e1d-128">索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="63e1d-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="63e1d-129">值: `true`</span><span class="sxs-lookup"><span data-stu-id="63e1d-129">Value: `true`</span></span>
   * <span data-ttu-id="63e1d-130">**儲存**設定並**重新啟動**您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e1d-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="63e1d-131">**監視 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63e1d-131">**Monitor your app**.</span></span>  <span data-ttu-id="63e1d-132">[探索資料](#explore-the-data)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="63e1d-133">稍後，您可以視需要使用 Application Insights 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e1d-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="63e1d-134">如何移除 Application Insights，或切換成傳送到另一個資源？</span><span class="sxs-lookup"><span data-stu-id="63e1d-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="63e1d-135">在 Azure 中，開啟 Web 應用程式控制刀鋒視窗，在 [開發工具] 下開啟 [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="63e1d-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="63e1d-136">刪除 Application Insights 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="63e1d-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="63e1d-137">然後在 [監視] 之下，選擇 Application Insights 並建立或選取您想要的資源。</span><span class="sxs-lookup"><span data-stu-id="63e1d-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="63e1d-138">使用 Application Insights 建置應用程式</span><span class="sxs-lookup"><span data-stu-id="63e1d-138">Build the app with Application Insights</span></span>
<span data-ttu-id="63e1d-139">Application Insights 可以提供更詳細的遙測，方法是將 SDK 安裝至您的 App。</span><span class="sxs-lookup"><span data-stu-id="63e1d-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="63e1d-140">特別是，您可以收集追蹤記錄檔、[撰寫自訂遙測](app-insights-api-custom-events-metrics.md)，並取得更詳細的例外狀況報告。</span><span class="sxs-lookup"><span data-stu-id="63e1d-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="63e1d-141">**在 Visual Studio 中** (2013 Update 2 或更新版本)，為專案設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="63e1d-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="63e1d-142">以滑鼠右鍵按一下 web 專案，然後選擇 [新增 > Application Insights] 或 [設定 Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="63e1d-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![以滑鼠右鍵按一下 Web 專案，然後選擇 [新增或設定 Application Insights]。](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="63e1d-144">系統要求您登入時，請使用 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="63e1d-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="63e1d-145">此作業有兩種效果︰</span><span class="sxs-lookup"><span data-stu-id="63e1d-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="63e1d-146">在 Azure 中建立 Application Insights 資源，這是存放、分析和顯示遙測資料的位置。</span><span class="sxs-lookup"><span data-stu-id="63e1d-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="63e1d-147">將 Application Insights NuGet 套件新增至您的程式碼 (若尚未存在其中)，然後設定它將遙測傳送至 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="63e1d-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="63e1d-148">在開發電腦中執行應用程式 (F5)，以**測試遙測**。</span><span class="sxs-lookup"><span data-stu-id="63e1d-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="63e1d-149">如常**將應用程式發佈**至 Azure。</span><span class="sxs-lookup"><span data-stu-id="63e1d-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="63e1d-150">*如何切換為傳送至不同的 Application Insights 資源？*</span><span class="sxs-lookup"><span data-stu-id="63e1d-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="63e1d-151">在 Visual Studio 中，以滑鼠右鍵按一下專案，選擇 [設定 Application Insights]，然後選擇您想要的資源。</span><span class="sxs-lookup"><span data-stu-id="63e1d-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="63e1d-152">您可取得建立新資源的選項。</span><span class="sxs-lookup"><span data-stu-id="63e1d-152">You get the option to create a new resource.</span></span> <span data-ttu-id="63e1d-153">重建並重新部署。</span><span class="sxs-lookup"><span data-stu-id="63e1d-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="63e1d-154">探索資料</span><span class="sxs-lookup"><span data-stu-id="63e1d-154">Explore the data</span></span>
1. <span data-ttu-id="63e1d-155">在 Web 應用程式控制台的 Application Insights 刀鋒視窗中，您會看到「即時計量」，其顯示在一兩秒內發生的要求和失敗。</span><span class="sxs-lookup"><span data-stu-id="63e1d-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="63e1d-156">當您要重新發佈應用程式時，這就非常有用 - 您可以立即看到任何問題。</span><span class="sxs-lookup"><span data-stu-id="63e1d-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="63e1d-157">點選完整的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="63e1d-157">Click through to the full Application Insights resource.</span></span>

    ![點選](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="63e1d-159">您也可以直接從 Azure 資源導覽前往該處。</span><span class="sxs-lookup"><span data-stu-id="63e1d-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="63e1d-160">逐一點選任何圖表以取得更詳細的資料：</span><span class="sxs-lookup"><span data-stu-id="63e1d-160">Click through any chart to get more detail:</span></span>
   
    ![按一下 Application Insights 概觀刀鋒視窗上的圖表](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="63e1d-162">您可以 [自訂計量刀鋒視窗](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="63e1d-163">進一步逐一點選以查看個別事件與其屬性︰</span><span class="sxs-lookup"><span data-stu-id="63e1d-163">Click through further to see individual events and their properties:</span></span>
   
    ![按一下事件類型以開啟依該類型篩選的搜尋](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="63e1d-165">請注意 [...] 連結以開啟所有的屬性。</span><span class="sxs-lookup"><span data-stu-id="63e1d-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="63e1d-166">您可以 [自訂搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="63e1d-167">如需透過遙測功能進行更強大的搜尋，請使用 [Log Analytics 查詢語言](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="63e1d-168">更多遙測</span><span class="sxs-lookup"><span data-stu-id="63e1d-168">More telemetry</span></span>

* [<span data-ttu-id="63e1d-169">網頁載入資料</span><span class="sxs-lookup"><span data-stu-id="63e1d-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="63e1d-170">自訂遙測</span><span class="sxs-lookup"><span data-stu-id="63e1d-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="63e1d-171">影片</span><span class="sxs-lookup"><span data-stu-id="63e1d-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="63e1d-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63e1d-172">Next steps</span></span>
* <span data-ttu-id="63e1d-173">[在即時應用程式上執行分析工具](app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="63e1d-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - 使用 Application Insights 監視 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="63e1d-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="63e1d-175">[能夠讓 Azure 診斷](app-insights-azure-diagnostics.md) 傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="63e1d-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="63e1d-176">[監視服務健康狀態計量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)，確保您的服務可用且回應正常。</span><span class="sxs-lookup"><span data-stu-id="63e1d-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="63e1d-177">每當發生作業事件或計量超過臨界值時，[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="63e1d-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="63e1d-178">使用 [JavaScript 應用程式和網頁適用的 Application Insights](app-insights-javascript.md) ，以從造訪網頁的瀏覽器取得用戶端遙測。</span><span class="sxs-lookup"><span data-stu-id="63e1d-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="63e1d-179">[設定可用性 Web 測試](app-insights-monitor-web-app-availability.md) ，以在您的網站關閉時發出警示。</span><span class="sxs-lookup"><span data-stu-id="63e1d-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

