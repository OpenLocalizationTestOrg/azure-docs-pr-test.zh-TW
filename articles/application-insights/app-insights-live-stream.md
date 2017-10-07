---
title: "利用自訂計量與 Azure Application Insights 中的診斷度量資料流 aaaLive |Microsoft 文件"
description: "透過自訂計量即時監視您的 Web 應用程式，並透過失敗、追蹤和事件的即時摘要診斷問題。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="b3bb7-103">即時計量資料流︰以 1 秒的延遲進行監視與診斷</span><span class="sxs-lookup"><span data-stu-id="b3bb7-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="b3bb7-104">探查 hello 訊號核心即時、 在生產環境 web 應用程式的使用中的即時度量資料流[Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b3bb7-105">選取和篩選度量和效能計數器 toowatch 即時，沒有任何佔用 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="b3bb7-106">檢查失敗要求和例外狀況範例中的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="b3bb7-107">即時計量資料流可搭配[分析工具](app-insights-profiler.md)、[快照集偵錯工具](app-insights-snapshot-debugger.md)和[效能測試](app-insights-monitor-web-app-availability.md#performance-tests)，為您的即時網站提供強大且非侵入性的診斷工具。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="b3bb7-108">您可以使用即時計量資料流：</span><span class="sxs-lookup"><span data-stu-id="b3bb7-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="b3bb7-109">藉由監看效能和失敗計數，在發行修正程式時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="b3bb7-110">觀看 hello 影響的測試載入，並診斷問題的即時。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="b3bb7-111">專注於特定的測試工作階段，或選取和篩選您想要 toowatch hello 度量依篩選掉已知的問題。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="b3bb7-112">在發生例外狀況時取得其追蹤。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="b3bb7-113">使用篩選的實驗 toofind hello 最相關的 Kpi。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="b3bb7-114">即時監看任何 Windows 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="b3bb7-115">輕鬆地識別的伺服器時發生問題，並篩選所有 hello KPI/即時摘要的 toojust 該伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="b3bb7-116">[![即時計量資料流影片](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="b3bb7-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="b3bb7-117">在內部部署執行的 ASP.NET 應用程式或 hello 雲端目前使用即時度量資料流。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="b3bb7-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="b3bb7-118">Get started</span></span>

1. <span data-ttu-id="b3bb7-119">如果您尚未在 ASP.NET Web 應用程式或 [Windows Server 應用程式](app-insights-windows-services.md)中[安裝 Application Insights](app-insights-asp-net.md)，請立即安裝。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="b3bb7-120">**更新 toohello 最新版本**的 hello Application Insights 套件。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="b3bb7-121">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="b3bb7-122">開啟 hello**更新**索引標籤上，核取**包含發行前版本**，然後選取 所有 hello Microsoft.ApplicationInsights.* 封裝。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="b3bb7-123">重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-123">Redeploy your app.</span></span>

3. <span data-ttu-id="b3bb7-124">在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式的 hello Application Insights 資源，並開啟 即時資料流。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="b3bb7-125">[安全 hello 控制通道](#secure-the-control-channel)如果您可能會在您的篩選條件中使用機密資料，例如客戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![在 hello 概觀刀鋒視窗中，按一下 即時資料流](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="b3bb7-127">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="b3bb7-127">No data?</span></span> <span data-ttu-id="b3bb7-128">請檢查您的伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="b3bb7-128">Check your server firewall</span></span>

<span data-ttu-id="b3bb7-129">檢查 hello[即時度量資料流的傳出連接埠](app-insights-ip-addresses.md#outgoing-ports)hello 防火牆的伺服器中開啟。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="b3bb7-130">即時計量資料流與計量瀏覽器和分析有何不同？</span><span class="sxs-lookup"><span data-stu-id="b3bb7-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="b3bb7-131">即時資料流</span><span class="sxs-lookup"><span data-stu-id="b3bb7-131">Live Stream</span></span> | <span data-ttu-id="b3bb7-132">計量瀏覽器和分析</span><span class="sxs-lookup"><span data-stu-id="b3bb7-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="b3bb7-133">延遲</span><span class="sxs-lookup"><span data-stu-id="b3bb7-133">Latency</span></span>|<span data-ttu-id="b3bb7-134">在一秒內顯示資料</span><span class="sxs-lookup"><span data-stu-id="b3bb7-134">Data displayed within one second</span></span>|<span data-ttu-id="b3bb7-135">在幾分鐘後進行彙總</span><span class="sxs-lookup"><span data-stu-id="b3bb7-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="b3bb7-136">沒有保留</span><span class="sxs-lookup"><span data-stu-id="b3bb7-136">No retention</span></span>|<span data-ttu-id="b3bb7-137">資料保存在正在 hello 圖表上就會被捨棄</span><span class="sxs-lookup"><span data-stu-id="b3bb7-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="b3bb7-138">資料會保留 90 天</span><span class="sxs-lookup"><span data-stu-id="b3bb7-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="b3bb7-139">隨選</span><span class="sxs-lookup"><span data-stu-id="b3bb7-139">On demand</span></span>|<span data-ttu-id="b3bb7-140">當您開啟即時計量時會串流處理資料</span><span class="sxs-lookup"><span data-stu-id="b3bb7-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="b3bb7-141">每當 hello SDK 已安裝並啟用時，傳送資料</span><span class="sxs-lookup"><span data-stu-id="b3bb7-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="b3bb7-142">免費</span><span class="sxs-lookup"><span data-stu-id="b3bb7-142">Free</span></span>|<span data-ttu-id="b3bb7-143">即時資料流資料免費</span><span class="sxs-lookup"><span data-stu-id="b3bb7-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="b3bb7-144">主體太[定價](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="b3bb7-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="b3bb7-145">取樣</span><span class="sxs-lookup"><span data-stu-id="b3bb7-145">Sampling</span></span>|<span data-ttu-id="b3bb7-146">傳輸所有選取的計量和計數器。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="b3bb7-147">取樣失敗和堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="b3bb7-148">不會套用 TelemetryProcessors。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="b3bb7-149">可能[取樣](app-insights-api-filtering-sampling.md)事件</span><span class="sxs-lookup"><span data-stu-id="b3bb7-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="b3bb7-150">控制通道</span><span class="sxs-lookup"><span data-stu-id="b3bb7-150">Control channel</span></span>|<span data-ttu-id="b3bb7-151">篩選控制項訊號傳送 toohello SDK。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="b3bb7-152">建議您[保護這個通道](#secure-channel)。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="b3bb7-153">通訊是單向的 toohello 入口網站</span><span class="sxs-lookup"><span data-stu-id="b3bb7-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="b3bb7-154">選取並篩選您的計量</span><span class="sxs-lookup"><span data-stu-id="b3bb7-154">Select and filter your metrics</span></span>

<span data-ttu-id="b3bb7-155">(用於傳統 ASP.NET 應用程式與 hello 最新的 SDK。)</span><span class="sxs-lookup"><span data-stu-id="b3bb7-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="b3bb7-156">您可以套用任何 Application Insights 遙測的任意的篩選條件，從 hello 入口網站來監視自訂即時的 KPI。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="b3bb7-157">按一下 顯示當您滑鼠移過任何 hello 圖表的 hello 篩選控制項。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="b3bb7-158">下列圖表中的 hello 繪製自訂要求計數 KPI 與 URL 和持續時間屬性的篩選。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="b3bb7-159">驗證您的篩選條件以 hello 資料流預覽區段會顯示符合您指定在任何時間點的時間 hello 準則的遙測的即時摘要。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![自訂要求 KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="b3bb7-161">您可以監視與計數不同的值。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="b3bb7-162">hello 選項取決於資料流，這可能是任何 Application Insights 遙測 hello 類型： 要求、 相依性、 例外狀況、 追蹤、 事件或度量。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="b3bb7-163">它可以是您自己的[自訂測量](app-insights-api-custom-events-metrics.md#properties)：</span><span class="sxs-lookup"><span data-stu-id="b3bb7-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![值選項](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="b3bb7-165">此外 tooApplication Insights 遙測，您也可以監視任何 Windows 效能計數器從 hello 資料流選項中選取，並提供 hello hello 效能計數器名稱。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="b3bb7-166">即時計量會在兩個地方進行彙總︰在每一部伺服器上本機進行，以及在所有伺服器上進行。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="b3bb7-167">您可以變更 hello 預設值為 hello 各自的下拉式清單中選取其他選項。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="b3bb7-168">範例遙測︰自訂即時診斷事件</span><span class="sxs-lookup"><span data-stu-id="b3bb7-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="b3bb7-169">根據預設，hello 即時摘要的事件會顯示失敗的要求和相依性呼叫、 例外狀況、 事件和追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="b3bb7-170">按一下 hello 篩選圖示 toosee hello 套用準則的任何一點的時間。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![預設的即時摘要](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="b3bb7-172">如同度量，您可以指定 hello Application Insights 遙測型別的任何任意準則 tooany。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="b3bb7-173">在此範例中，我們要選取特定的要求失敗、追蹤及事件。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="b3bb7-174">我們還會選取所有的例外狀況和相依性失敗。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-174">We are also selecting all exceptions and dependency failures.</span></span>

![自訂即時摘要](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="b3bb7-176">注意： 目前，對於例外狀況訊息為基礎的準則，使用 hello 最外層的例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="b3bb7-177">在上述範例中，hello toofilter 出 hello 良性例外狀況的內部例外狀況訊息 (如下所示 hello"<-"分隔符號) 「 hello 用戶端中斷連接。 」</span><span class="sxs-lookup"><span data-stu-id="b3bb7-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="b3bb7-178">請使用不包含「讀取要求內容時發生錯誤」準則的訊息。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="b3bb7-179">請參閱 hello 詳細 hello 中的項目按一下即時摘要。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="b3bb7-180">您可以暫停 hello 摘要方法是按一下**暫停**或直接向下捲動，或按一下項目。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="b3bb7-181">即時摘要捲動後 toohello 頂端之後, 會繼續，或按一下 hello 計數器的項目時所收集到已暫停。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![取樣的即時失敗](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="b3bb7-183">依伺服器執行個體篩選</span><span class="sxs-lookup"><span data-stu-id="b3bb7-183">Filter by server instance</span></span>

<span data-ttu-id="b3bb7-184">如果您想 toomonitor 特定伺服器角色執行個體，您可以篩選由伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![取樣的即時失敗](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="b3bb7-186">SDK 需求</span><span class="sxs-lookup"><span data-stu-id="b3bb7-186">SDK Requirements</span></span>
<span data-ttu-id="b3bb7-187">[Application Insights SDK for Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 的 2.4.0-beta2 版或更新版本提供「自訂即時計量串流」。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="b3bb7-188">請記住 tooselect 」 包含發行前版本 」 選項，從 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="b3bb7-189">Hello 控制通道的安全</span><span class="sxs-lookup"><span data-stu-id="b3bb7-189">Secure hello control channel</span></span>
<span data-ttu-id="b3bb7-190">hello 您指定自訂篩選準則會傳送 hello Application Insights SDK 後 toohello 即時度量元件。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="b3bb7-191">hello 篩選可能包含機密資訊，例如 customerIDs。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="b3bb7-192">您可以進行 hello 通道的安全密碼的 API 金鑰與此外 toohello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="b3bb7-193">建立 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="b3bb7-193">Create an API Key</span></span>

![建立 API 金鑰](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="b3bb7-195">新增 API 金鑰 tooConfiguration</span><span class="sxs-lookup"><span data-stu-id="b3bb7-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="b3bb7-196">在 hello applicationinsights.config 檔案中加入 hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="b3bb7-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="b3bb7-197">或在程式碼中，將它在 hello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="b3bb7-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="b3bb7-198">不過，如果您辨識並信任所有 hello 連接的伺服器，您可以嘗試 hello 自訂篩選器，而不驗證 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="b3bb7-199">這個選項有六個月可供使用。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-199">This option is available for six months.</span></span> <span data-ttu-id="b3bb7-200">一旦每個新的工作階段或是新的伺服器上線後，就需要此覆寫。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-200">This override is required once every new session, or when a new server comes online.</span></span>

![即時計量驗證選項](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="b3bb7-202">我們強烈建議您在 hello 篩選準則中輸入 CustomerID 等的潛在的敏感資訊之前，先設定 hello 驗證通道。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="b3bb7-203">產生效能測試負載</span><span class="sxs-lookup"><span data-stu-id="b3bb7-203">Generating a performance test load</span></span>

<span data-ttu-id="b3bb7-204">如果您想 toowatch hello 效果，負載的增加，請使用 hello 效能測試刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="b3bb7-205">它會模擬來自許多同時使用者的要求。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="b3bb7-206">它可以執行任一個 「 手動測試 」 (ping 測試) 的單一的 URL，或執行[multi-step web 效能測試](app-insights-monitor-web-app-availability.md#multi-step-web-tests)您上傳 （在相同的方式為可用性測試的 hello)。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="b3bb7-207">建立 hello 效能測試之後，開啟 hello 測試和 hello 即時資料流刀鋒視窗，在個別視窗中。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="b3bb7-208">您可以查看當 hello 佇列效能測試啟動，並且在 hello 的監看即時資料流相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="b3bb7-209">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b3bb7-209">Troubleshooting</span></span>

<span data-ttu-id="b3bb7-210">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="b3bb7-210">No data?</span></span> <span data-ttu-id="b3bb7-211">如果您的應用程式是在受保護的網路中︰即時計量串流會使用與其他 Application Insights 遙測不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="b3bb7-212">請確定[這些 IP 位址](app-insights-ip-addresses.md)在您的防火牆中為開啟狀態。</span><span class="sxs-lookup"><span data-stu-id="b3bb7-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b3bb7-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3bb7-213">Next steps</span></span>
* [<span data-ttu-id="b3bb7-214">使用 Application Insights 監視使用情況</span><span class="sxs-lookup"><span data-stu-id="b3bb7-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="b3bb7-215">使用診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="b3bb7-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b3bb7-216">分析工具</span><span class="sxs-lookup"><span data-stu-id="b3bb7-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="b3bb7-217">快照集偵錯工具</span><span class="sxs-lookup"><span data-stu-id="b3bb7-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
