---
title: "aaaMonitor 應用程式的健全狀況和使用 Application Insights 的使用方式"
description: "開始使用 Application Insights。 分析內部部署或 Microsoft Azure 應用程式的使用情況、可用性和效能。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="9d478-104">監視 Web 應用程式的效能</span><span class="sxs-lookup"><span data-stu-id="9d478-104">Monitor performance in web applications</span></span>


<span data-ttu-id="9d478-105">確認應用程式的運作狀況良好，以及迅速找出任何失敗。</span><span class="sxs-lookup"><span data-stu-id="9d478-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="9d478-106">[Application Insights] [ start]會告訴您有關任何效能問題和例外狀況，以及可協助您尋找並診斷 hello 根本原因。</span><span class="sxs-lookup"><span data-stu-id="9d478-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="9d478-107">Application Insights 可以監視 Java 和 ASP.NET Web 應用程式與服務、WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="9d478-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="9d478-108">這些服務可以裝載在內部部署、虛擬機器上，或作為 Microsoft Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="9d478-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="9d478-109">Hello 用戶端，Application Insights 可以採取網頁和各種不同的裝置，包括 iOS、 Android 和 Windows 市集應用程式的遙測。</span><span class="sxs-lookup"><span data-stu-id="9d478-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="9d478-110">我們讓尋找您的 Web 應用程式中緩慢執行分頁有新的體驗。</span><span class="sxs-lookup"><span data-stu-id="9d478-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="9d478-111">如果您沒有存取 tooit，啟用以 hello 設定預覽選項[預覽刀鋒伺服器](app-insights-previews.md)。</span><span class="sxs-lookup"><span data-stu-id="9d478-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="9d478-112">了解這個新體驗中[找出並修正與 hello 互動式效能調查的效能瓶頸](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation)。</span><span class="sxs-lookup"><span data-stu-id="9d478-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="9d478-113"><a name="setup"></a>設定效能監視</span><span class="sxs-lookup"><span data-stu-id="9d478-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="9d478-114">如果您還沒有加入 Application Insights tooyour （亦即，如果它沒有 ApplicationInsights.config） 專案，選擇下列其中一種 tooget 啟動：</span><span class="sxs-lookup"><span data-stu-id="9d478-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="9d478-115">ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d478-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="9d478-116">加入例外狀況監視</span><span class="sxs-lookup"><span data-stu-id="9d478-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="9d478-117">加入相依性監視</span><span class="sxs-lookup"><span data-stu-id="9d478-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="9d478-118">J2EE Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d478-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="9d478-119">加入相依性監視</span><span class="sxs-lookup"><span data-stu-id="9d478-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="9d478-120"><a name="view"></a>探索效能度量</span><span class="sxs-lookup"><span data-stu-id="9d478-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="9d478-121">在[hello Azure 入口網站](https://portal.azure.com)，瀏覽 toohello 設定您的應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="9d478-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="9d478-122">hello 概觀刀鋒視窗會顯示基本的效能資料：</span><span class="sxs-lookup"><span data-stu-id="9d478-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="9d478-123">按一下詳細資料，因而 toosee 任何圖表 toosee 更長的時間。</span><span class="sxs-lookup"><span data-stu-id="9d478-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="9d478-124">例如，按一下 hello 要求磚，然後選取 時間範圍：</span><span class="sxs-lookup"><span data-stu-id="9d478-124">For example, click hello Requests tile and then select a time range:</span></span>

![瀏覽 toomore 的資料，並選取時間範圍](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="9d478-126">按一下圖表 toochoose 它會顯示，或將新的圖表，並選取其度量的度量：</span><span class="sxs-lookup"><span data-stu-id="9d478-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![按一下圖形 toochoose 度量](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="9d478-128">**取消選取所有 hello 度量**toosee hello 完整選取項目所提供。</span><span class="sxs-lookup"><span data-stu-id="9d478-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="9d478-129">hello 度量分成群組。選取任何群組的成員時，只有 hello 該群組的其他成員會出現。</span><span class="sxs-lookup"><span data-stu-id="9d478-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="9d478-130"><a name="metrics"></a>這具有哪些意義？</span><span class="sxs-lookup"><span data-stu-id="9d478-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="9d478-131">效能磚和報告</span><span class="sxs-lookup"><span data-stu-id="9d478-131">Performance tiles and reports</span></span>
<span data-ttu-id="9d478-132">您可以取用多種效能計量。</span><span class="sxs-lookup"><span data-stu-id="9d478-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="9d478-133">讓我們開始與 hello 應用程式 刀鋒視窗預設會出現。</span><span class="sxs-lookup"><span data-stu-id="9d478-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="9d478-134">Requests</span><span class="sxs-lookup"><span data-stu-id="9d478-134">Requests</span></span>
<span data-ttu-id="9d478-135">hello 指定期間內收到的 HTTP 要求數。</span><span class="sxs-lookup"><span data-stu-id="9d478-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="9d478-136">請比較這上隨著 hello 負載而改變，您的應用程式的行為方式的其他報表 toosee hello 結果。</span><span class="sxs-lookup"><span data-stu-id="9d478-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="9d478-137">HTTP 要求包括分頁、資料及映像的所有 GET 或 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="9d478-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="9d478-138">按一下特定 Url 的 hello 磚 tooget 計數。</span><span class="sxs-lookup"><span data-stu-id="9d478-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="9d478-139">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="9d478-139">Average response time</span></span>
<span data-ttu-id="9d478-140">輸入您的應用程式和 hello 回應所傳回的 web 要求之間的量值 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="9d478-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="9d478-141">hello 點顯示移動平均。</span><span class="sxs-lookup"><span data-stu-id="9d478-141">hello points show a moving average.</span></span> <span data-ttu-id="9d478-142">如果有許多要求，可能會有一些偏離 hello 平均沒有明顯的尖峰或大大 hello 圖形中。</span><span class="sxs-lookup"><span data-stu-id="9d478-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="9d478-143">找尋異常的高峰。</span><span class="sxs-lookup"><span data-stu-id="9d478-143">Look for unusual peaks.</span></span> <span data-ttu-id="9d478-144">一般情況下，預期升高要求與回應時間 toorise。</span><span class="sxs-lookup"><span data-stu-id="9d478-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="9d478-145">如果不相稱 hello 上升，您的應用程式可能會達到資源限制，例如 CPU 或 hello 容量的服務，它會使用。</span><span class="sxs-lookup"><span data-stu-id="9d478-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="9d478-146">按一下 hello 磚 tooget 時間特定的 url。</span><span class="sxs-lookup"><span data-stu-id="9d478-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="9d478-147">最慢的要求</span><span class="sxs-lookup"><span data-stu-id="9d478-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="9d478-148">顯示可能需要進行效能調整的要求。</span><span class="sxs-lookup"><span data-stu-id="9d478-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="9d478-149">失敗的要求</span><span class="sxs-lookup"><span data-stu-id="9d478-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="9d478-150">丟出無法攔截之例外狀況的要求計數。</span><span class="sxs-lookup"><span data-stu-id="9d478-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="9d478-151">按一下 hello 磚 toosee hello 詳細資料的特定失敗，並選取個別要求 toosee 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9d478-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="9d478-152">系統只會針對各項檢查保留一個具代表性的失敗範例。</span><span class="sxs-lookup"><span data-stu-id="9d478-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="9d478-153">其他度量</span><span class="sxs-lookup"><span data-stu-id="9d478-153">Other metrics</span></span>
<span data-ttu-id="9d478-154">toosee 哪些其他度量可以顯示，並按一下圖形，然後取消選取所有 hello 度量 toosee hello 完整可用組。</span><span class="sxs-lookup"><span data-stu-id="9d478-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="9d478-155">按一下 (i) toosee 每個度量定義。</span><span class="sxs-lookup"><span data-stu-id="9d478-155">Click (i) toosee each metric's definition.</span></span>

![取消選取所有度量 toosee hello 整個組](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="9d478-157">其他不可以出現在選取的任何度量會停用 hello hello 相同的圖表。</span><span class="sxs-lookup"><span data-stu-id="9d478-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="9d478-158">設定警示</span><span class="sxs-lookup"><span data-stu-id="9d478-158">Set alerts</span></span>
<span data-ttu-id="9d478-159">收到的異常值的任何度量，電子郵件通知的 toobe 加入警示。</span><span class="sxs-lookup"><span data-stu-id="9d478-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="9d478-160">您可以選擇 toosend hello 電子郵件 toohello 帳戶系統管理員或 toospecific 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9d478-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="9d478-161">設定前 hello hello 資源的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="9d478-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="9d478-162">如果您想 tooset 效能或使用量度量的警示，不要選擇 hello webtest 資源。</span><span class="sxs-lookup"><span data-stu-id="9d478-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="9d478-163">能謹慎 toonote hello 單位中，系統會詢問 tooenter hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="9d478-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="9d478-164">*看不見 hello 新增警示 按鈕。*</span><span class="sxs-lookup"><span data-stu-id="9d478-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="9d478-165">-這是具有唯讀存取權的群組帳戶 toowhich 嗎？</span><span class="sxs-lookup"><span data-stu-id="9d478-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="9d478-166">請檢查與 hello 帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9d478-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="9d478-167"><a name="diagnosis"></a>診斷問題</span><span class="sxs-lookup"><span data-stu-id="9d478-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="9d478-168">以下是幾個尋找及診斷效能問題的訣竅：</span><span class="sxs-lookup"><span data-stu-id="9d478-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="9d478-169">設定[web 測試][ availability] toobe 如果網站當機，或不正確或速度很慢回應警示。</span><span class="sxs-lookup"><span data-stu-id="9d478-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="9d478-170">如果失敗或緩慢的回應相關的 tooload，比較與其他度量 toosee hello 要求計數。</span><span class="sxs-lookup"><span data-stu-id="9d478-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="9d478-171">[插入和搜尋追蹤陳述式][ diagnostic]中程式碼 toohelp 找出問題。</span><span class="sxs-lookup"><span data-stu-id="9d478-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="9d478-172">使用[即時計量資料流][livestream]監視作業中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d478-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="9d478-173">擷取您的.Net 應用程式的 hello 狀態[快照偵錯工具][snapshot]。</span><span class="sxs-lookup"><span data-stu-id="9d478-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="9d478-174">使用互動式效能調查尋找及修正效能瓶頸</span><span class="sxs-lookup"><span data-stu-id="9d478-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="9d478-175">您可以使用 hello 新 Application Insights 互動式效能調查 toolocate 您 Web 應用程式的區域會減緩整體效能。</span><span class="sxs-lookup"><span data-stu-id="9d478-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="9d478-176">您可以快速地尋找特定頁面的速度變慢，並使用 hello[程式碼剖析工具](app-insights-profiler.md)toosee 如果沒有這些網頁之間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="9d478-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="9d478-177">建立一份執行緩慢分頁的清單</span><span class="sxs-lookup"><span data-stu-id="9d478-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="9d478-178">hello 尋找效能問題的第一個步驟是 tooget hello 慢回應頁面的清單。</span><span class="sxs-lookup"><span data-stu-id="9d478-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="9d478-179">hello 下列螢幕擷取畫面將示範如何使用 hello 效能刀鋒視窗 tooget 潛在頁面 tooinvestigate 進一步的清單。</span><span class="sxs-lookup"><span data-stu-id="9d478-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="9d478-180">您可以快速查看從這個頁面時發生 slow-down hello 回應 hello 應用程式時間下午約 6:00，然後又在大約 10 PM。</span><span class="sxs-lookup"><span data-stu-id="9d478-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="9d478-181">您也可以查看 hello 取得客戶/詳細資料的作業有一些長時間執行作業中間值回應時間為 507.05 毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="9d478-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Application Insights 互動式效能](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="9d478-183">向下鑽研特定分頁</span><span class="sxs-lookup"><span data-stu-id="9d478-183">Drill down on specific pages</span></span>

<span data-ttu-id="9d478-184">您有了應用程式效能的快照集之後，您可以取得更多特定執行緩慢作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9d478-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="9d478-185">按一下任何作業中 hello 清單 toosee hello 詳細資料如下所示。</span><span class="sxs-lookup"><span data-stu-id="9d478-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="9d478-186">從 hello 圖表中，您可以看到 hello 效能為基礎的相依性。</span><span class="sxs-lookup"><span data-stu-id="9d478-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="9d478-187">您也可以查看多少使用者經驗的 hello 不同回應時間。</span><span class="sxs-lookup"><span data-stu-id="9d478-187">You can also see how many users experienced hello various response times.</span></span> 

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="9d478-189">在特定時間週期向下鑽研</span><span class="sxs-lookup"><span data-stu-id="9d478-189">Drill down on a specific time period</span></span>

<span data-ttu-id="9d478-190">識別 tooinvestigate 時間點之後，甚至進一步 toolook 在 hello 特定作業可能會造成 hello 效能 slow-down 的向下鑽研。</span><span class="sxs-lookup"><span data-stu-id="9d478-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="9d478-191">當您按一下特定點上的時間就 hello 頁面如下所示的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9d478-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="9d478-192">在 hello 低於您的範例可以看到 hello 作業列出指定的時段內以及 hello 伺服器回應碼和 hello 作業持續時間。</span><span class="sxs-lookup"><span data-stu-id="9d478-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="9d478-193">您也具有開啟 TFS 工作項目，如果您需要此資訊 tooyour 開發團隊 toosend hello url。</span><span class="sxs-lookup"><span data-stu-id="9d478-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Application Insights 時間配量](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="9d478-195">在特定作業向下鑽研</span><span class="sxs-lookup"><span data-stu-id="9d478-195">Drill down on a specific operation</span></span>

<span data-ttu-id="9d478-196">識別 tooinvestigate 時間點之後，甚至進一步 toolook 在 hello 特定作業可能會造成 hello 效能 slow-down 的向下鑽研。</span><span class="sxs-lookup"><span data-stu-id="9d478-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="9d478-197">按一下 hello 清單 toosee hello 作業的詳細資料 hello 如下所示的作業。</span><span class="sxs-lookup"><span data-stu-id="9d478-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="9d478-198">在此範例中的 hello 作業失敗，以及 Application Insights 所提供的 hello hello 詳細資料，您可以看到擲回例外狀況 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d478-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="9d478-199">同樣地，您可以從這個刀鋒視窗輕鬆地建立 TFS 工作項目。</span><span class="sxs-lookup"><span data-stu-id="9d478-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="9d478-201"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="9d478-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="9d478-202">[Web 測試][ availability] -web 要求傳送 tooyour 應用程式定期從 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="9d478-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="9d478-203">[擷取和搜尋診斷追蹤][ diagnostic] -插入追蹤呼叫和詳查 hello 結果 toopinpoint 問題。</span><span class="sxs-lookup"><span data-stu-id="9d478-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="9d478-204">[流量追蹤][usage] - 了解使用者使用應用程式的情況。</span><span class="sxs-lookup"><span data-stu-id="9d478-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="9d478-205">[疑難排解][qna] - 以及問答集</span><span class="sxs-lookup"><span data-stu-id="9d478-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



