---
title: "Azure Application Insights 中具有自訂計量和診斷功能的即時計量資料流 | Microsoft Docs"
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
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="a51c1-103">即時計量資料流︰以 1 秒的延遲進行監視與診斷</span><span class="sxs-lookup"><span data-stu-id="a51c1-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="a51c1-104">使用 [Application Insights](app-insights-overview.md) 中的即時計量資料流，探查您即時生產環境 Web 應用程式中的活動訊號。</span><span class="sxs-lookup"><span data-stu-id="a51c1-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a51c1-105">選取並篩選要即時監看的計量和效能計數器，而不會對您的服務造成任何干擾。</span><span class="sxs-lookup"><span data-stu-id="a51c1-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="a51c1-106">檢查失敗要求和例外狀況範例中的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="a51c1-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="a51c1-107">即時計量資料流可搭配[分析工具](app-insights-profiler.md)、[快照集偵錯工具](app-insights-snapshot-debugger.md)和[效能測試](app-insights-monitor-web-app-availability.md#performance-tests)，為您的即時網站提供強大且非侵入性的診斷工具。</span><span class="sxs-lookup"><span data-stu-id="a51c1-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="a51c1-108">您可以使用即時計量資料流：</span><span class="sxs-lookup"><span data-stu-id="a51c1-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="a51c1-109">藉由監看效能和失敗計數，在發行修正程式時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="a51c1-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="a51c1-110">監看測試負載的影響，並即時診斷問題。</span><span class="sxs-lookup"><span data-stu-id="a51c1-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="a51c1-111">藉由選取並篩選您想要監看的計量，專注於特定測試工作階段或篩選出已知問題。</span><span class="sxs-lookup"><span data-stu-id="a51c1-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="a51c1-112">在發生例外狀況時取得其追蹤。</span><span class="sxs-lookup"><span data-stu-id="a51c1-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="a51c1-113">試驗篩選，以尋找最相關的 KPI。</span><span class="sxs-lookup"><span data-stu-id="a51c1-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="a51c1-114">即時監看任何 Windows 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="a51c1-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="a51c1-115">輕鬆識別有問題的伺服器，並將所有 KPI/即時摘要篩選到只有該伺服器。</span><span class="sxs-lookup"><span data-stu-id="a51c1-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="a51c1-116">[![即時計量資料流影片](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="a51c1-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="a51c1-117">即時計量資料流目前適用於在內部部署或雲端中執行的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a51c1-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="a51c1-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="a51c1-118">Get started</span></span>

1. <span data-ttu-id="a51c1-119">如果您尚未在 ASP.NET Web 應用程式或 [Windows Server 應用程式](app-insights-windows-services.md)中[安裝 Application Insights](app-insights-asp-net.md)，請立即安裝。</span><span class="sxs-lookup"><span data-stu-id="a51c1-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="a51c1-120">**更新至最新版本**的 Application Insights 套件。</span><span class="sxs-lookup"><span data-stu-id="a51c1-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="a51c1-121">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。</span><span class="sxs-lookup"><span data-stu-id="a51c1-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="a51c1-122">開啟 [更新] 索引標籤，核取 [包含發行前版本]，然後選取所有 Microsoft.ApplicationInsights.* 套件。</span><span class="sxs-lookup"><span data-stu-id="a51c1-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="a51c1-123">重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a51c1-123">Redeploy your app.</span></span>

3. <span data-ttu-id="a51c1-124">在 [Azure 入口網站](https://portal.azure.com)中，開啟您應用程式的 Application Insights 資源，然後開啟 [即時資料流]。</span><span class="sxs-lookup"><span data-stu-id="a51c1-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="a51c1-125">如果您可能在篩選中使用客戶名稱等敏感性資料，請[保護控制通道](#secure-the-control-channel)。</span><span class="sxs-lookup"><span data-stu-id="a51c1-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![在 [概觀] 刀鋒視窗中，按一下 [即時資料流]](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="a51c1-127">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="a51c1-127">No data?</span></span> <span data-ttu-id="a51c1-128">請檢查您的伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="a51c1-128">Check your server firewall</span></span>

<span data-ttu-id="a51c1-129">檢查是否已開啟您伺服器防火牆中[即時計量資料流的連出連接埠](app-insights-ip-addresses.md#outgoing-ports)。</span><span class="sxs-lookup"><span data-stu-id="a51c1-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="a51c1-130">即時計量資料流與計量瀏覽器和分析有何不同？</span><span class="sxs-lookup"><span data-stu-id="a51c1-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="a51c1-131">即時資料流</span><span class="sxs-lookup"><span data-stu-id="a51c1-131">Live Stream</span></span> | <span data-ttu-id="a51c1-132">計量瀏覽器和分析</span><span class="sxs-lookup"><span data-stu-id="a51c1-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="a51c1-133">延遲</span><span class="sxs-lookup"><span data-stu-id="a51c1-133">Latency</span></span>|<span data-ttu-id="a51c1-134">在一秒內顯示資料</span><span class="sxs-lookup"><span data-stu-id="a51c1-134">Data displayed within one second</span></span>|<span data-ttu-id="a51c1-135">在幾分鐘後進行彙總</span><span class="sxs-lookup"><span data-stu-id="a51c1-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="a51c1-136">沒有保留</span><span class="sxs-lookup"><span data-stu-id="a51c1-136">No retention</span></span>|<span data-ttu-id="a51c1-137">資料在圖表上就會保存，之後便會捨棄該資料</span><span class="sxs-lookup"><span data-stu-id="a51c1-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="a51c1-138">資料會保留 90 天</span><span class="sxs-lookup"><span data-stu-id="a51c1-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="a51c1-139">隨選</span><span class="sxs-lookup"><span data-stu-id="a51c1-139">On demand</span></span>|<span data-ttu-id="a51c1-140">當您開啟即時計量時會串流處理資料</span><span class="sxs-lookup"><span data-stu-id="a51c1-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="a51c1-141">每當安裝並啟用 SDK 時都會傳送資料</span><span class="sxs-lookup"><span data-stu-id="a51c1-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="a51c1-142">免費</span><span class="sxs-lookup"><span data-stu-id="a51c1-142">Free</span></span>|<span data-ttu-id="a51c1-143">即時資料流資料免費</span><span class="sxs-lookup"><span data-stu-id="a51c1-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="a51c1-144">依[價格](app-insights-pricing.md)付費</span><span class="sxs-lookup"><span data-stu-id="a51c1-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="a51c1-145">取樣</span><span class="sxs-lookup"><span data-stu-id="a51c1-145">Sampling</span></span>|<span data-ttu-id="a51c1-146">傳輸所有選取的計量和計數器。</span><span class="sxs-lookup"><span data-stu-id="a51c1-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="a51c1-147">取樣失敗和堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="a51c1-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="a51c1-148">不會套用 TelemetryProcessors。</span><span class="sxs-lookup"><span data-stu-id="a51c1-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="a51c1-149">可能[取樣](app-insights-api-filtering-sampling.md)事件</span><span class="sxs-lookup"><span data-stu-id="a51c1-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="a51c1-150">控制通道</span><span class="sxs-lookup"><span data-stu-id="a51c1-150">Control channel</span></span>|<span data-ttu-id="a51c1-151">篩選控制項訊號會傳送至 SDK。</span><span class="sxs-lookup"><span data-stu-id="a51c1-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="a51c1-152">建議您[保護這個通道](#secure-channel)。</span><span class="sxs-lookup"><span data-stu-id="a51c1-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="a51c1-153">對入口網站的單向通訊</span><span class="sxs-lookup"><span data-stu-id="a51c1-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="a51c1-154">選取並篩選您的計量</span><span class="sxs-lookup"><span data-stu-id="a51c1-154">Select and filter your metrics</span></span>

<span data-ttu-id="a51c1-155">(適用於具有最新 SDK 的傳統 ASP.NET 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="a51c1-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="a51c1-156">您可以從入口網站將任何篩選條件套用在任何 Application Insights 遙測上，以便即時監視自訂 KPI。</span><span class="sxs-lookup"><span data-stu-id="a51c1-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="a51c1-157">按一下您將滑鼠移過任何圖表時所顯示的篩選條件控制項。</span><span class="sxs-lookup"><span data-stu-id="a51c1-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="a51c1-158">下列圖表是使用 URL 和 Duration 屬性的篩選條件來繪製自訂要求計數 KPI。</span><span class="sxs-lookup"><span data-stu-id="a51c1-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="a51c1-159">利用可顯示符合您在任一時間點所指定準則之遙測即時摘要的「串流預覽」區段來驗證您的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="a51c1-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![自訂要求 KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="a51c1-161">您可以監視與計數不同的值。</span><span class="sxs-lookup"><span data-stu-id="a51c1-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="a51c1-162">選項取決於串流的類型，可能是任何的 Application Insights 遙測︰要求、相依性、例外狀況、追蹤、事件或計量。</span><span class="sxs-lookup"><span data-stu-id="a51c1-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="a51c1-163">它可以是您自己的[自訂測量](app-insights-api-custom-events-metrics.md#properties)：</span><span class="sxs-lookup"><span data-stu-id="a51c1-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![值選項](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="a51c1-165">除了 Application Insights 遙測之外，您也可以監視任何 Windows 效能計數器，方法是從串流選項中選取，並提供效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a51c1-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="a51c1-166">即時計量會在兩個地方進行彙總︰在每一部伺服器上本機進行，以及在所有伺服器上進行。</span><span class="sxs-lookup"><span data-stu-id="a51c1-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="a51c1-167">您可以選取個別下拉式清單中的其他選項，在任一位置變更預設。</span><span class="sxs-lookup"><span data-stu-id="a51c1-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="a51c1-168">範例遙測︰自訂即時診斷事件</span><span class="sxs-lookup"><span data-stu-id="a51c1-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="a51c1-169">依預設，事件的即時摘要會顯示失敗要求和相依性呼叫、例外狀況、事件以及追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="a51c1-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="a51c1-170">按一下篩選圖示可查看任一時間點套用的準則。</span><span class="sxs-lookup"><span data-stu-id="a51c1-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![預設的即時摘要](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="a51c1-172">如同計量，您可以將任意準則指定為任何的 Application Insights 遙測類型。</span><span class="sxs-lookup"><span data-stu-id="a51c1-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="a51c1-173">在此範例中，我們要選取特定的要求失敗、追蹤及事件。</span><span class="sxs-lookup"><span data-stu-id="a51c1-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="a51c1-174">我們還會選取所有的例外狀況和相依性失敗。</span><span class="sxs-lookup"><span data-stu-id="a51c1-174">We are also selecting all exceptions and dependency failures.</span></span>

![自訂即時摘要](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="a51c1-176">請注意︰目前針對以例外狀況訊息為基礎的準則，請使用最外部的例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="a51c1-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="a51c1-177">在上述範例中，若要使用內部例外狀況訊息 (後接 "<--" 分隔符號)「用戶端中斷連線。」將良性的例外狀況篩選掉，</span><span class="sxs-lookup"><span data-stu-id="a51c1-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="a51c1-178">請使用不包含「讀取要求內容時發生錯誤」準則的訊息。</span><span class="sxs-lookup"><span data-stu-id="a51c1-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="a51c1-179">按一下即時摘要中的項目，以查看它的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a51c1-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="a51c1-180">您可以按一下 [暫停] 或只向下捲動，或是按一下項目來將摘要暫停。</span><span class="sxs-lookup"><span data-stu-id="a51c1-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="a51c1-181">在您捲動回到頂端後，或是按一下暫停時所收集到的項目計數器，即時摘要就會繼續進行。</span><span class="sxs-lookup"><span data-stu-id="a51c1-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![取樣的即時失敗](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="a51c1-183">依伺服器執行個體篩選</span><span class="sxs-lookup"><span data-stu-id="a51c1-183">Filter by server instance</span></span>

<span data-ttu-id="a51c1-184">如果您想要監視特定伺服器角色執行個體，可以依伺服器篩選。</span><span class="sxs-lookup"><span data-stu-id="a51c1-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![取樣的即時失敗](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="a51c1-186">SDK 需求</span><span class="sxs-lookup"><span data-stu-id="a51c1-186">SDK Requirements</span></span>
<span data-ttu-id="a51c1-187">[Application Insights SDK for Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 的 2.4.0-beta2 版或更新版本提供「自訂即時計量串流」。</span><span class="sxs-lookup"><span data-stu-id="a51c1-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="a51c1-188">請記得選取 NuGet 套件管理員的 [包括預先發行] 選項。</span><span class="sxs-lookup"><span data-stu-id="a51c1-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="a51c1-189">保護控制通道</span><span class="sxs-lookup"><span data-stu-id="a51c1-189">Secure the control channel</span></span>
<span data-ttu-id="a51c1-190">您指定的自訂篩選條件準則會傳回給 Application Insights SDK 中的即時計量元件。</span><span class="sxs-lookup"><span data-stu-id="a51c1-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="a51c1-191">篩選條件可能會包含機密資訊，例如 customerIDs。</span><span class="sxs-lookup"><span data-stu-id="a51c1-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="a51c1-192">除了檢測金鑰之外，您還可以利用祕密 API 金鑰來保護頻道安全。</span><span class="sxs-lookup"><span data-stu-id="a51c1-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="a51c1-193">建立 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="a51c1-193">Create an API Key</span></span>

![建立 API 金鑰](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="a51c1-195">將 API 金鑰新增至設定</span><span class="sxs-lookup"><span data-stu-id="a51c1-195">Add API key to Configuration</span></span>
<span data-ttu-id="a51c1-196">在 applicationinsights.config 檔案中，將 AuthenticationApiKey 新增至 QuickPulseTelemetryModule：</span><span class="sxs-lookup"><span data-stu-id="a51c1-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="a51c1-197">或在程式碼中，在 QuickPulseTelemetryModule 上設定它：</span><span class="sxs-lookup"><span data-stu-id="a51c1-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="a51c1-198">不過，如果您認得並信任所有連線的伺服器，則無需透驗證的頻道就可以嘗試自訂篩選器。</span><span class="sxs-lookup"><span data-stu-id="a51c1-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="a51c1-199">這個選項有六個月可供使用。</span><span class="sxs-lookup"><span data-stu-id="a51c1-199">This option is available for six months.</span></span> <span data-ttu-id="a51c1-200">一旦每個新的工作階段或是新的伺服器上線後，就需要此覆寫。</span><span class="sxs-lookup"><span data-stu-id="a51c1-200">This override is required once every new session, or when a new server comes online.</span></span>

![即時計量驗證選項](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="a51c1-202">我們強烈建議您在篩選條件準則中輸入潛在的機密資訊 (例如 CustomerID) 之前，先設定驗證的頻道。</span><span class="sxs-lookup"><span data-stu-id="a51c1-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="a51c1-203">產生效能測試負載</span><span class="sxs-lookup"><span data-stu-id="a51c1-203">Generating a performance test load</span></span>

<span data-ttu-id="a51c1-204">如果您想要監看負載增加的影響，請使用 [效能測試] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a51c1-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="a51c1-205">它會模擬來自許多同時使用者的要求。</span><span class="sxs-lookup"><span data-stu-id="a51c1-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="a51c1-206">它可以執行單一 URL 的「手動測試」(Ping 測試)，或執行您上傳的[多重步驟 Web 效能測試](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (上傳方式與可用性測試相同)。</span><span class="sxs-lookup"><span data-stu-id="a51c1-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="a51c1-207">建立效能測試之後，在不同的視窗中開啟測試和 [即時資料流] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a51c1-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="a51c1-208">您可以查看已排入佇列之效能測試的開始時間，並同時監看即時資料流。</span><span class="sxs-lookup"><span data-stu-id="a51c1-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="a51c1-209">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a51c1-209">Troubleshooting</span></span>

<span data-ttu-id="a51c1-210">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="a51c1-210">No data?</span></span> <span data-ttu-id="a51c1-211">如果您的應用程式是在受保護的網路中︰即時計量串流會使用與其他 Application Insights 遙測不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a51c1-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="a51c1-212">請確定[這些 IP 位址](app-insights-ip-addresses.md)在您的防火牆中為開啟狀態。</span><span class="sxs-lookup"><span data-stu-id="a51c1-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a51c1-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a51c1-213">Next steps</span></span>
* [<span data-ttu-id="a51c1-214">使用 Application Insights 監視使用情況</span><span class="sxs-lookup"><span data-stu-id="a51c1-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="a51c1-215">使用診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="a51c1-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a51c1-216">分析工具</span><span class="sxs-lookup"><span data-stu-id="a51c1-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="a51c1-217">快照集偵錯工具</span><span class="sxs-lookup"><span data-stu-id="a51c1-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
