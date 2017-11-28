---
title: "Azure web 應用程式效能 aaaMonitor |Microsoft 文件"
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
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="ca87b-104">監視 Azure Web 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="ca87b-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="ca87b-105">在 hello [Azure 入口網站](https://portal.azure.com)您可以設定應用程式效能監視您[Azure web 應用程式](../app-service-web/app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="ca87b-106">[Azure 的 Application Insights](app-insights-overview.md)檢測其活動 toohello Application Insights 服務，其中會儲存並分析您應用程式 toosend 遙測。</span><span class="sxs-lookup"><span data-stu-id="ca87b-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="ca87b-107">可以用度量圖表和搜尋工具 toohelp 診斷問題、 改善效能，以及評估使用。</span><span class="sxs-lookup"><span data-stu-id="ca87b-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="ca87b-108">執行階段或建置階段</span><span class="sxs-lookup"><span data-stu-id="ca87b-108">Run time or build time</span></span>
<span data-ttu-id="ca87b-109">您可以設定監視，可檢測 hello 應用程式在兩種方法之一：</span><span class="sxs-lookup"><span data-stu-id="ca87b-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="ca87b-110">**執行階段** - 您可以在 Web 應用程式已經上線時，選取效能監視延伸模組。</span><span class="sxs-lookup"><span data-stu-id="ca87b-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="ca87b-111">它不是必要的 toorebuild 或重新安裝您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca87b-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="ca87b-112">您會取得一組標準封裝，用以監視回應時間、成功率、例外狀況、相依性等。</span><span class="sxs-lookup"><span data-stu-id="ca87b-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="ca87b-113">**建置階段** - 您可以在開發應用程式中安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="ca87b-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="ca87b-114">此選項比較靈活。</span><span class="sxs-lookup"><span data-stu-id="ca87b-114">This option is more versatile.</span></span> <span data-ttu-id="ca87b-115">在加法 toohello 相同標準的封裝，您可以撰寫程式碼 toocustomize hello 遙測或 toosend 您自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="ca87b-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="ca87b-116">您可以記錄的特定活動或根據您的應用程式網域 toohello 語意的記錄事件。</span><span class="sxs-lookup"><span data-stu-id="ca87b-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="ca87b-117">使用 Application Insights 執行時間檢測</span><span class="sxs-lookup"><span data-stu-id="ca87b-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="ca87b-118">如果您已在 Azure 中執行 Web 應用程式，您便已得到一些監視︰要求率和錯誤率。</span><span class="sxs-lookup"><span data-stu-id="ca87b-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="ca87b-119">加入 Application Insights tooget 更多，例如回應時間、 監視呼叫 toodependencies、 智慧型偵測和 hello 功能強大的記錄分析查詢語言。</span><span class="sxs-lookup"><span data-stu-id="ca87b-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="ca87b-120">**選取 [Application Insights**控制台] 中 hello Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca87b-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![在 [監視] 之下，選擇 Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="ca87b-122">選擇 toocreate 新的資源，除非您已經設定此應用程式的 Application Insights 資源的另一個路由。</span><span class="sxs-lookup"><span data-stu-id="ca87b-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="ca87b-123">安裝 Application Insights 之後，**檢測您的 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ca87b-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![檢測 Web 應用程式](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="ca87b-125">針對頁面檢視和使用者遙測**啟用用戶端監視**。</span><span class="sxs-lookup"><span data-stu-id="ca87b-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="ca87b-126">選取 [設定] > [應用程式設定]</span><span class="sxs-lookup"><span data-stu-id="ca87b-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="ca87b-127">在 [應用程式設定] 之下，新增索引鍵值組︰</span><span class="sxs-lookup"><span data-stu-id="ca87b-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="ca87b-128">索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="ca87b-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="ca87b-129">值: `true`</span><span class="sxs-lookup"><span data-stu-id="ca87b-129">Value: `true`</span></span>
   * <span data-ttu-id="ca87b-130">**儲存**hello 設定和**重新啟動**您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca87b-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="ca87b-131">**監視 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ca87b-131">**Monitor your app**.</span></span>  <span data-ttu-id="ca87b-132">[Expore hello 資料](#explore-the-data)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="ca87b-133">稍後，您可以建立 hello 與 Application Insights 的應用程式，如果您想。</span><span class="sxs-lookup"><span data-stu-id="ca87b-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="ca87b-134">*如何移除 Application Insights 或切換 toosending tooanother 資源？*</span><span class="sxs-lookup"><span data-stu-id="ca87b-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="ca87b-135">在 Azure 中，開啟 hello web 應用程式控制項刀鋒視窗，並在開發工具，開啟**延伸**。</span><span class="sxs-lookup"><span data-stu-id="ca87b-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="ca87b-136">刪除 hello Application Insights 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ca87b-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="ca87b-137">然後在 [監視中]，選擇 Application Insights 和建立或選取您想要的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="ca87b-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="ca87b-138">建置 hello 與 Application Insights 的應用程式</span><span class="sxs-lookup"><span data-stu-id="ca87b-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="ca87b-139">Application Insights 可以提供更詳細的遙測，方法是將 SDK 安裝至您的 App。</span><span class="sxs-lookup"><span data-stu-id="ca87b-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="ca87b-140">特別是，您可以收集追蹤記錄檔、[撰寫自訂遙測](app-insights-api-custom-events-metrics.md)，並取得更詳細的例外狀況報告。</span><span class="sxs-lookup"><span data-stu-id="ca87b-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="ca87b-141">**在 Visual Studio 中** (2013 Update 2 或更新版本)，為專案設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="ca87b-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="ca87b-142">以滑鼠右鍵按一下 hello web 專案，然後選取**新增 > Application Insights**或**設定 Application Insights**。</span><span class="sxs-lookup"><span data-stu-id="ca87b-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![以滑鼠右鍵按一下 hello web 專案，然後選擇 新增或設定 Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="ca87b-144">如果您詢問 toosign 中的，使用您的 Azure 帳戶 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="ca87b-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="ca87b-145">hello 作業有兩個效果：</span><span class="sxs-lookup"><span data-stu-id="ca87b-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="ca87b-146">在 Azure 中建立 Application Insights 資源，這是存放、分析和顯示遙測資料的位置。</span><span class="sxs-lookup"><span data-stu-id="ca87b-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="ca87b-147">新增 hello Application Insights NuGet 封裝 tooyour 程式碼 （如果尚未存在），並將它設定 toosend 遙測 toohello Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ca87b-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="ca87b-148">**測試 hello 遙測**所執行的 hello 應用程式，在開發電腦 (F5)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="ca87b-149">**Hello 應用程式發行**tooAzure hello 以一般方式。</span><span class="sxs-lookup"><span data-stu-id="ca87b-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="ca87b-150">*我要如何切換 toosending tooa 不同的 Application Insights 資源？*</span><span class="sxs-lookup"><span data-stu-id="ca87b-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="ca87b-151">在 Visual Studio 中，以滑鼠右鍵按一下 hello 專案中，選擇 **設定 Application Insights**並選擇您想要的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="ca87b-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="ca87b-152">您會收到 hello 選項 toocreate 新的資源。</span><span class="sxs-lookup"><span data-stu-id="ca87b-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="ca87b-153">重建並重新部署。</span><span class="sxs-lookup"><span data-stu-id="ca87b-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="ca87b-154">瀏覽 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ca87b-154">Explore hello data</span></span>
1. <span data-ttu-id="ca87b-155">在 hello Application Insights 刀鋒視窗中的 web 應用程式控制台，您會看到即時的度量，第二個或兩個內顯示要求和失敗發生。</span><span class="sxs-lookup"><span data-stu-id="ca87b-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="ca87b-156">當您要重新發佈應用程式時，這就非常有用 - 您可以立即看到任何問題。</span><span class="sxs-lookup"><span data-stu-id="ca87b-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="ca87b-157">按一下瀏覽 toohello 完整的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="ca87b-157">Click through toohello full Application Insights resource.</span></span>

    ![點選](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="ca87b-159">您也可以直接從 Azure 資源導覽前往該處。</span><span class="sxs-lookup"><span data-stu-id="ca87b-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="ca87b-160">按一下任何圖 tooget 透過更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ca87b-160">Click through any chart tooget more detail:</span></span>
   
    ![在 hello Application Insights 概觀刀鋒視窗中，按一下 圖表](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="ca87b-162">您可以 [自訂計量刀鋒視窗](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="ca87b-163">按一下所有進一步 toosee 個別事件和其屬性：</span><span class="sxs-lookup"><span data-stu-id="ca87b-163">Click through further toosee individual events and their properties:</span></span>
   
    ![按一下 搜尋篩選該型別的事件類型 tooopen](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="ca87b-165">請注意，"…"hello 連結 tooopen 所有屬性。</span><span class="sxs-lookup"><span data-stu-id="ca87b-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="ca87b-166">您可以 [自訂搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="ca87b-167">透過您的遙測功能更強大的搜尋，請使用 hello[記錄分析查詢語言](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="ca87b-168">更多遙測</span><span class="sxs-lookup"><span data-stu-id="ca87b-168">More telemetry</span></span>

* [<span data-ttu-id="ca87b-169">網頁載入資料</span><span class="sxs-lookup"><span data-stu-id="ca87b-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="ca87b-170">自訂遙測</span><span class="sxs-lookup"><span data-stu-id="ca87b-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="ca87b-171">影片</span><span class="sxs-lookup"><span data-stu-id="ca87b-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="ca87b-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca87b-172">Next steps</span></span>
* <span data-ttu-id="ca87b-173">[即時應用程式上執行 hello 分析工具](app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="ca87b-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - 使用 Application Insights 監視 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ca87b-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="ca87b-175">[啟用 Azure 診斷](app-insights-azure-diagnostics.md)toobe 傳送 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="ca87b-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="ca87b-176">[監視服務健康狀況度量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="ca87b-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="ca87b-177">每當發生作業事件或計量超過臨界值時，[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="ca87b-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="ca87b-178">使用[Application Insights for JavaScript 應用程式及網頁](app-insights-javascript.md)tooget hello 瀏覽器瀏覽網頁用戶端遙測資料。</span><span class="sxs-lookup"><span data-stu-id="ca87b-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="ca87b-179">[設定可用性 web 測試](app-insights-monitor-web-app-availability.md)toobe 如果您的網站已關閉警示。</span><span class="sxs-lookup"><span data-stu-id="ca87b-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

