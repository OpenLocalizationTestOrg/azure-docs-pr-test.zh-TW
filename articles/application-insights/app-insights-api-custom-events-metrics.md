---
title: "自訂事件和度量 aaaApplication Insights API，|Microsoft 文件"
description: "在您的裝置或桌面應用程式、 網頁或服務，tootrack 使用量中插入幾行程式碼，以及診斷問題。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="13f57-103">自訂事件和度量的 Application Insights API</span><span class="sxs-lookup"><span data-stu-id="13f57-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="13f57-104">在您的應用程式 toofind 出使用者做什麼，插入幾行程式碼或 toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="13f57-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="13f57-105">您可以從裝置和桌面應用程式、Web 用戶端以及 Web 伺服器傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="13f57-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="13f57-106">使用 hello [Azure Application Insights](app-insights-overview.md)核心遙測 API toosend 自訂事件和度量和您自己的標準遙測資料的版本。</span><span class="sxs-lookup"><span data-stu-id="13f57-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="13f57-107">這個 API 是 hello hello 標準 Application Insights 資料收集器使用相同的 API。</span><span class="sxs-lookup"><span data-stu-id="13f57-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="13f57-108">API summary</span><span class="sxs-lookup"><span data-stu-id="13f57-108">API summary</span></span>
<span data-ttu-id="13f57-109">所有平台，除了少數小型變化 hello API 是一致的。</span><span class="sxs-lookup"><span data-stu-id="13f57-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="13f57-110">方法</span><span class="sxs-lookup"><span data-stu-id="13f57-110">Method</span></span> | <span data-ttu-id="13f57-111">用於</span><span class="sxs-lookup"><span data-stu-id="13f57-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="13f57-112">頁面、畫面、刀鋒視窗或表單。</span><span class="sxs-lookup"><span data-stu-id="13f57-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="13f57-113">使用者動作和其他事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-113">User actions and other events.</span></span> <span data-ttu-id="13f57-114">使用 tootrack 使用者行為或 toomonitor 效能。</span><span class="sxs-lookup"><span data-stu-id="13f57-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="13f57-115">例如，佇列長度的效能測量資料不相關 toospecific 事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="13f57-116">記錄例外狀況以供診斷。</span><span class="sxs-lookup"><span data-stu-id="13f57-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="13f57-117">追蹤位置中的關聯 tooother 事件發生和檢查堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="13f57-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="13f57-118">Hello 頻率和持續期間的效能分析伺服器要求的記錄。</span><span class="sxs-lookup"><span data-stu-id="13f57-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="13f57-119">診斷記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="13f57-119">Diagnostic log messages.</span></span> <span data-ttu-id="13f57-120">您也可以擷取第三方記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13f57-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="13f57-121">Hello 持續時間與頻率取決於您的應用程式的呼叫 tooexternal 元件的記錄。</span><span class="sxs-lookup"><span data-stu-id="13f57-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="13f57-122">您可以[附加的屬性和度量](#properties)toomost 這些遙測呼叫。</span><span class="sxs-lookup"><span data-stu-id="13f57-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="13f57-123"><a name="prep"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="13f57-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="13f57-124">如果您還沒有 Application Insights SDK 的參考：</span><span class="sxs-lookup"><span data-stu-id="13f57-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="13f57-125">加入 hello Application Insights SDK tooyour 專案：</span><span class="sxs-lookup"><span data-stu-id="13f57-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="13f57-126">ASP.NET 專案</span><span class="sxs-lookup"><span data-stu-id="13f57-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="13f57-127">Java 專案</span><span class="sxs-lookup"><span data-stu-id="13f57-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="13f57-128">每個網頁中的 JavaScript</span><span class="sxs-lookup"><span data-stu-id="13f57-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="13f57-129">在裝置或 Web 伺服器程式碼中，加入：</span><span class="sxs-lookup"><span data-stu-id="13f57-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="13f57-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="13f57-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="13f57-131">*Visual Basic：*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="13f57-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="13f57-132">*Java：* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="13f57-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="13f57-133">建構 TelemetryClient 執行個體</span><span class="sxs-lookup"><span data-stu-id="13f57-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="13f57-134">建構 `TelemetryClient` 的執行個體 (除了網頁中的 JavaScript)：</span><span class="sxs-lookup"><span data-stu-id="13f57-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="13f57-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="13f57-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="13f57-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="13f57-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="13f57-138">TelemetryClient 具備執行緒安全。</span><span class="sxs-lookup"><span data-stu-id="13f57-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="13f57-139">我們建議針對您每個應用程式的模組使用 TelemetryClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="13f57-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="13f57-140">比方說，您可能必須一個 TelemetryClient 執行個體，在您 web 服務 tooreport 連入 HTTP 要求，以及另一個中介軟體類別 tooreport 商務邏輯事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="13f57-141">您可以設定屬性，例如`TelemetryClient.Context.User.Id`tootrack 使用者與工作階段，或`TelemetryClient.Context.Device.Id`tooidentify hello 機器。</span><span class="sxs-lookup"><span data-stu-id="13f57-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="13f57-142">這項資訊會附加的 tooall hello 執行個體傳送的事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="13f57-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="13f57-143">TrackEvent</span></span>
<span data-ttu-id="13f57-144">在 Application Insights 中，「自訂事件」是您可以在[計量瀏覽器](app-insights-metrics-explorer.md)顯示為彙總計數，以及在[診斷搜尋](app-insights-diagnostic-search.md)中顯示為個別發生點的資料點。</span><span class="sxs-lookup"><span data-stu-id="13f57-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="13f57-145">（不相關的 tooMVC 或其他架構 」 的事件。"）</span><span class="sxs-lookup"><span data-stu-id="13f57-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="13f57-146">插入`TrackEvent`呼叫中程式碼 toocount 各種事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="13f57-147">使用者選擇特定功能的頻率、達成特定目標的頻率，或他們犯特定類型錯誤的頻率。</span><span class="sxs-lookup"><span data-stu-id="13f57-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="13f57-148">例如，在遊戲的應用程式中時傳送事件使用者 wins hello 遊戲：</span><span class="sxs-lookup"><span data-stu-id="13f57-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="13f57-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="13f57-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="13f57-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="13f57-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="13f57-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="13f57-153">在 hello Microsoft Azure 入口網站中檢視您的事件</span><span class="sxs-lookup"><span data-stu-id="13f57-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="13f57-154">開啟您的事件計數 toosee[計量瀏覽器](app-insights-metrics-explorer.md)刀鋒視窗中，加入新的圖表，並選取**事件**。</span><span class="sxs-lookup"><span data-stu-id="13f57-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![查看自訂事件的計數](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="13f57-156">不同的事件，toocompare hello 計數太設定 hello 圖表類型**方格**，並依事件名稱的群組：</span><span class="sxs-lookup"><span data-stu-id="13f57-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![設定 hello 圖表類型和群組](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="13f57-158">在 hello 方格中，按一下 事件名稱 toosee 個別項目間的該事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="13f57-159">toosee 更多詳細資料-按一下 hello 清單中的任何項目。</span><span class="sxs-lookup"><span data-stu-id="13f57-159">toosee more detail - click any occurrence in hello list.</span></span>

![鑽研 hello 事件](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="13f57-161">toofocus 上特定事件中搜尋或計量瀏覽器組 hello 刀鋒視窗的篩選器 toohello 事件名稱，您感興趣：</span><span class="sxs-lookup"><span data-stu-id="13f57-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![開啟 [篩選器]，展開 [事件名稱]，然後選取一或多個值](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="13f57-163">分析中的自訂事件</span><span class="sxs-lookup"><span data-stu-id="13f57-163">Custom events in Analytics</span></span>

<span data-ttu-id="13f57-164">hello 遙測位於 hello`customEvents`資料表中[應用程式 Insights 分析](app-insights-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="13f57-165">每個資料列代表呼叫太`trackEvent(..)`應用程式中。</span><span class="sxs-lookup"><span data-stu-id="13f57-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="13f57-166">如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。</span><span class="sxs-lookup"><span data-stu-id="13f57-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="13f57-167">範例 itemCount = = 10，10 呼叫 tootrackEvent() 的 hello 取樣程序時，才傳輸其中的表示。</span><span class="sxs-lookup"><span data-stu-id="13f57-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="13f57-168">tooget 正確的自訂事件計數，您應該使用因此使用程式碼，例如`customEvent | summarize sum(itemCount)`。</span><span class="sxs-lookup"><span data-stu-id="13f57-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="13f57-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="13f57-169">TrackMetric</span></span>

<span data-ttu-id="13f57-170">Application Insights 可以不附加的 tooparticular 事件的度量的圖表。</span><span class="sxs-lookup"><span data-stu-id="13f57-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="13f57-171">例如，您可以定期監視佇列長度。</span><span class="sxs-lookup"><span data-stu-id="13f57-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="13f57-172">（包括計量），hello 個別的度量感興趣的較少比 hello 變化和趨勢，並因此統計圖表很有用。</span><span class="sxs-lookup"><span data-stu-id="13f57-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="13f57-173">在排序 toosend 度量 tooApplication Insights，您可以使用 hello`TrackMetric(..)`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="13f57-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="13f57-174">有兩種方式 toosend 度量：</span><span class="sxs-lookup"><span data-stu-id="13f57-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="13f57-175">單一值：</span><span class="sxs-lookup"><span data-stu-id="13f57-175">Single value.</span></span> <span data-ttu-id="13f57-176">每次您執行應用程式中的度量，您傳送 hello 對應值 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="13f57-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="13f57-177">例如，假設您有描述項目容器中的 hello 數目的度量。</span><span class="sxs-lookup"><span data-stu-id="13f57-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="13f57-178">在特定時間週期內，您必須先三個項目放入 hello 容器，然後您移除兩個項目。</span><span class="sxs-lookup"><span data-stu-id="13f57-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="13f57-179">因此，您可以呼叫`TrackMetric`兩次： 第一次傳遞 hello 值`3`，然後 hello 值`-2`。</span><span class="sxs-lookup"><span data-stu-id="13f57-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="13f57-180">Application Insights 會代替您儲存這兩個值。</span><span class="sxs-lookup"><span data-stu-id="13f57-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="13f57-181">彙總：</span><span class="sxs-lookup"><span data-stu-id="13f57-181">Aggregation.</span></span> <span data-ttu-id="13f57-182">使用計量時，每個單一測量並不重要。</span><span class="sxs-lookup"><span data-stu-id="13f57-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="13f57-183">相反地，在特定期間內發生的狀況摘要才重要。</span><span class="sxs-lookup"><span data-stu-id="13f57-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="13f57-184">這類摘要稱為_彙總_。</span><span class="sxs-lookup"><span data-stu-id="13f57-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="13f57-185">在上述範例中的 hello，hello 彙總度量的加總該時間週期是`1`hello hello 度量值計數，且`2`。</span><span class="sxs-lookup"><span data-stu-id="13f57-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="13f57-186">使用 hello 彙總方式時，您只能叫用`TrackMetric`每一次的時間週期，並將傳送 hello 彙總值。</span><span class="sxs-lookup"><span data-stu-id="13f57-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="13f57-187">這是建議的方法，因為它可以大幅降低 hello 成本和效能負擔是藉由傳送較少的資料點 tooApplication Insights 時仍在收集所有相關資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="13f57-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="13f57-188">範例：</span><span class="sxs-lookup"><span data-stu-id="13f57-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="13f57-189">單一值</span><span class="sxs-lookup"><span data-stu-id="13f57-189">Single values</span></span>

<span data-ttu-id="13f57-190">toosend 單一公制值：</span><span class="sxs-lookup"><span data-stu-id="13f57-190">toosend a single metric value:</span></span>

<span data-ttu-id="13f57-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="13f57-192">C#、Java</span><span class="sxs-lookup"><span data-stu-id="13f57-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="13f57-193">彙總計量</span><span class="sxs-lookup"><span data-stu-id="13f57-193">Aggregating metrics</span></span>

<span data-ttu-id="13f57-194">然後才傳送從您的應用程式、 tooreduce 頻寬、 成本和 tooimprove 效能建議 tooaggregate 度量。</span><span class="sxs-lookup"><span data-stu-id="13f57-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="13f57-195">程式碼的彙總範例如下：</span><span class="sxs-lookup"><span data-stu-id="13f57-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="13f57-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="13f57-197">[計量瀏覽器] 中的自訂計量</span><span class="sxs-lookup"><span data-stu-id="13f57-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="13f57-198">toosee hello 結果中，開啟計量瀏覽器，並加入新的圖表。</span><span class="sxs-lookup"><span data-stu-id="13f57-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="13f57-199">編輯 hello 圖表 tooshow 您度量。</span><span class="sxs-lookup"><span data-stu-id="13f57-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="13f57-200">您的自訂公制可能需要幾分鐘的時間 tooappear hello 可用的度量清單中。</span><span class="sxs-lookup"><span data-stu-id="13f57-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![新增圖表或選取圖表，並在 [自訂] 底下選取您的度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="13f57-202">Analytics 中的自訂計量</span><span class="sxs-lookup"><span data-stu-id="13f57-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="13f57-203">hello 遙測位於 hello`customMetrics`資料表中[應用程式 Insights 分析](app-insights-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="13f57-204">每個資料列代表呼叫太`trackMetric(..)`應用程式中。</span><span class="sxs-lookup"><span data-stu-id="13f57-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="13f57-205">`valueSum`-這是 hello 度量 hello 總和。</span><span class="sxs-lookup"><span data-stu-id="13f57-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="13f57-206">tooget hello 平均值，除以`valueCount`。</span><span class="sxs-lookup"><span data-stu-id="13f57-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="13f57-207">`valueCount`-hello 度量所彙總成這數目`trackMetric(..)`呼叫。</span><span class="sxs-lookup"><span data-stu-id="13f57-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="13f57-208">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="13f57-208">Page views</span></span>
<span data-ttu-id="13f57-209">在裝置或網頁應用程式中，每個畫面或頁面載入時預設會傳送頁面檢視遙測。</span><span class="sxs-lookup"><span data-stu-id="13f57-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="13f57-210">但是，您可以變更該 tootrack 網頁檢視，在其他或不同的時間。</span><span class="sxs-lookup"><span data-stu-id="13f57-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="13f57-211">比方說，在索引標籤或刀鋒視窗會顯示應用程式中，您可能想 tootrack 頁面每當 hello 使用者開啟的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="13f57-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![[概觀] 刀鋒視窗上的使用方式透鏡](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="13f57-213">使用者與工作階段資料會傳送內容頁面檢視，以及因此 hello 使用者與工作階段時沒有網頁檢視遙測開始運作的圖表。</span><span class="sxs-lookup"><span data-stu-id="13f57-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="13f57-214">自訂頁面檢視</span><span class="sxs-lookup"><span data-stu-id="13f57-214">Custom page views</span></span>
<span data-ttu-id="13f57-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="13f57-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="13f57-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="13f57-218">如果您有數個索引標籤，在不同的 HTML 網頁中，您可以指定 hello URL 太：</span><span class="sxs-lookup"><span data-stu-id="13f57-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="13f57-219">計時頁面檢視</span><span class="sxs-lookup"><span data-stu-id="13f57-219">Timing page views</span></span>
<span data-ttu-id="13f57-220">根據預設，hello 時間回報為**網頁檢視載入時間**hello 瀏覽器傳送 hello 要求，直到呼叫 hello 瀏覽器網頁載入事件是當從算起。</span><span class="sxs-lookup"><span data-stu-id="13f57-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="13f57-221">相反地，您可以：</span><span class="sxs-lookup"><span data-stu-id="13f57-221">Instead, you can either:</span></span>

* <span data-ttu-id="13f57-222">設定明確的持續時間在 hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview)呼叫： `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`。</span><span class="sxs-lookup"><span data-stu-id="13f57-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="13f57-223">使用 hello 頁面檢視計時呼叫`startTrackPage`和`stopTrackPage`。</span><span class="sxs-lookup"><span data-stu-id="13f57-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="13f57-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="13f57-225">...</span><span class="sxs-lookup"><span data-stu-id="13f57-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="13f57-226">hello 名稱，讓您做為 hello 第一個參數產生關聯的 hello 開始和停止的呼叫。</span><span class="sxs-lookup"><span data-stu-id="13f57-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="13f57-227">預設 toohello 目前頁面名稱。</span><span class="sxs-lookup"><span data-stu-id="13f57-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="13f57-228">hello 計量瀏覽器中顯示的持續時間衍生自 hello hello 間隔產生頁面載入啟動和停止的呼叫。</span><span class="sxs-lookup"><span data-stu-id="13f57-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="13f57-229">它是最多 tooyou 哪些實際時間的間隔。</span><span class="sxs-lookup"><span data-stu-id="13f57-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="13f57-230">分析中的頁面遙測</span><span class="sxs-lookup"><span data-stu-id="13f57-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="13f57-231">在[分析](app-insights-analytics.md)中，有兩個資料表顯示瀏覽器作業的資料：</span><span class="sxs-lookup"><span data-stu-id="13f57-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="13f57-232">hello`pageViews`資料表包含有關 hello URL 及頁面標題的資料</span><span class="sxs-lookup"><span data-stu-id="13f57-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="13f57-233">hello`browserTimings`資料表包含有關用戶端效能資料，例如 hello 所花費時間 tooprocess hello 內送的資料</span><span class="sxs-lookup"><span data-stu-id="13f57-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="13f57-234">toofind 多久 hello 瀏覽器會採用 tooprocess 不同頁面：</span><span class="sxs-lookup"><span data-stu-id="13f57-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="13f57-235">不同的瀏覽器的 toodiscover hello popularities:</span><span class="sxs-lookup"><span data-stu-id="13f57-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="13f57-236">tooassociate 頁面檢視 tooAJAX 呼叫，將具有相依性：</span><span class="sxs-lookup"><span data-stu-id="13f57-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="13f57-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="13f57-237">TrackRequest</span></span>
<span data-ttu-id="13f57-238">hello 伺服器 SDK 會使用 TrackRequest toolog HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="13f57-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="13f57-239">您也可以呼叫它自己如果您要在內容中的 toosimulate 要求中並沒有 hello web 服務模組執行。</span><span class="sxs-lookup"><span data-stu-id="13f57-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="13f57-240">不過，hello 建議的方式 toosend 要求遙測是 hello 要求做為<a href="#operation-context">作業內容</a>。</span><span class="sxs-lookup"><span data-stu-id="13f57-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="13f57-241">作業內容</span><span class="sxs-lookup"><span data-stu-id="13f57-241">Operation context</span></span>
<span data-ttu-id="13f57-242">您可以一起關聯遙測項目，藉由附加 toothem 通用的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="13f57-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="13f57-243">hello 標準的要求追蹤模組會對例外狀況和其他事件，在處理 HTTP 要求時傳送。</span><span class="sxs-lookup"><span data-stu-id="13f57-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="13f57-244">在[搜尋](app-insights-diagnostic-search.md)和[分析](app-insights-analytics.md)，您可以使用 hello 識別碼 tooeasily 尋找與 hello 要求相關聯的任何事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="13f57-245">hello 最簡單方式 tooset hello 識別碼是 tooset 作業內容使用這種模式：</span><span class="sxs-lookup"><span data-stu-id="13f57-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="13f57-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="13f57-247">設定作業內容，以及`StartOperation`建立您指定的 hello 類型的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="13f57-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="13f57-248">它會傳送 hello 遙測項目時處置 hello 作業，或明確地呼叫`StopOperation`。</span><span class="sxs-lookup"><span data-stu-id="13f57-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="13f57-249">如果您使用`RequestTelemetry`hello 遙測類型，其持續時間設定為啟動和停止的逾時的 toohello 間隔。</span><span class="sxs-lookup"><span data-stu-id="13f57-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="13f57-250">作業內容不可為巢狀。</span><span class="sxs-lookup"><span data-stu-id="13f57-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="13f57-251">如果已經有相同的作業內容，則其識別碼是所有的 hello 包含項目，包括建立 hello 項目相關聯`StartOperation`。</span><span class="sxs-lookup"><span data-stu-id="13f57-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="13f57-252">在搜尋中，hello 作業內容是使用的 toocreate hello**相關項目**清單：</span><span class="sxs-lookup"><span data-stu-id="13f57-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![相關項目](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="13f57-254">如需有關自訂作業追蹤的詳細資訊，請參閱 [application-insights-custom-operations-tracking.md]。</span><span class="sxs-lookup"><span data-stu-id="13f57-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="13f57-255">分析中的要求</span><span class="sxs-lookup"><span data-stu-id="13f57-255">Requests in Analytics</span></span> 

<span data-ttu-id="13f57-256">在[應用程式 Insights 分析](app-insights-analytics.md)，hello 的總要求顯示`requests`資料表。</span><span class="sxs-lookup"><span data-stu-id="13f57-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="13f57-257">如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。</span><span class="sxs-lookup"><span data-stu-id="13f57-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="13f57-258">範例 itemCount = = 10，10 呼叫 tootrackRequest() 的 hello 取樣程序時，才傳輸其中的表示。</span><span class="sxs-lookup"><span data-stu-id="13f57-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="13f57-259">tooget 正確的要求 」 和 「 平均持續時間的計數要求的名稱來區隔，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="13f57-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="13f57-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="13f57-260">TrackException</span></span>
<span data-ttu-id="13f57-261">TooApplication Insights 傳送例外狀況：</span><span class="sxs-lookup"><span data-stu-id="13f57-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="13f57-262">太[計算](app-insights-metrics-explorer.md)，做為有問題的 hello 頻率的表示。</span><span class="sxs-lookup"><span data-stu-id="13f57-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="13f57-263">太[檢查個別項目](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="13f57-264">hello 報告包含 hello 堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="13f57-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="13f57-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="13f57-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="13f57-267">hello Sdk 自動攔截許多例外狀況，所以您不一定會明確需要 toocall TrackException。</span><span class="sxs-lookup"><span data-stu-id="13f57-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="13f57-268">ASP.NET:[撰寫程式碼 toocatch 例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="13f57-269">J2EE：[自動攔截例外狀況](app-insights-java-get-started.md#exceptions-and-request-failures)。</span><span class="sxs-lookup"><span data-stu-id="13f57-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="13f57-270">JavaScript：自動攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="13f57-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="13f57-271">如果您想 toodisable 自動集合時，加入您在您的網頁中插入的行 toohello 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="13f57-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="13f57-272">分析中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="13f57-272">Exceptions in Analytics</span></span>

<span data-ttu-id="13f57-273">在[應用程式 Insights 分析](app-insights-analytics.md)，例外狀況出現在 hello`exceptions`資料表。</span><span class="sxs-lookup"><span data-stu-id="13f57-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="13f57-274">如果[取樣](app-insights-sampling.md)是在作業中，hello`itemCount`屬性顯示的值大於 1。</span><span class="sxs-lookup"><span data-stu-id="13f57-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="13f57-275">範例 itemCount = = 10，10 呼叫 tootrackException() 的 hello 取樣程序時，才傳輸其中的表示。</span><span class="sxs-lookup"><span data-stu-id="13f57-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="13f57-276">tooget 正確的例外狀況計數區隔的例外狀況類型，請使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="13f57-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="13f57-277">大部分的 hello 重要堆疊資訊已擷取到不同的變數，但您可以拉相距 hello`details`結構 tooget 更多。</span><span class="sxs-lookup"><span data-stu-id="13f57-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="13f57-278">由於這個結構是動態的您應該轉換 hello 您預期的結果 toohello 類型。</span><span class="sxs-lookup"><span data-stu-id="13f57-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="13f57-279">例如：</span><span class="sxs-lookup"><span data-stu-id="13f57-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="13f57-280">tooassociate 例外狀況，其相關的要求，其使用聯結：</span><span class="sxs-lookup"><span data-stu-id="13f57-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="13f57-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="13f57-281">TrackTrace</span></span>
<span data-ttu-id="13f57-282">使用 TrackTrace toohelp 診斷問題傳送"階層連結軌跡"tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="13f57-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="13f57-283">您可以傳送診斷資料區塊，並且在[診斷搜尋](app-insights-diagnostic-search.md)中檢查。</span><span class="sxs-lookup"><span data-stu-id="13f57-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="13f57-284">[記錄配接器](app-insights-asp-net-trace-logs.md)使用此 API toosend 協力廠商記錄 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="13f57-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="13f57-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="13f57-286">您可以搜尋訊息內容，但是 (不同於屬性值) 您無法在其中進行篩選。</span><span class="sxs-lookup"><span data-stu-id="13f57-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="13f57-287">hello 大小限制`message`遠高於 hello 屬性限制。</span><span class="sxs-lookup"><span data-stu-id="13f57-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="13f57-288">TrackTrace 的優點是您可以將較長的資料放在 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="13f57-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="13f57-289">例如，您可以在該處編碼 POST 資料。</span><span class="sxs-lookup"><span data-stu-id="13f57-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="13f57-290">此外，您可以加入嚴重性層級 tooyour 訊息。</span><span class="sxs-lookup"><span data-stu-id="13f57-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="13f57-291">此外，其他的遙測，例如，您可以加入屬性值 toohelp 您篩選或搜尋不同組的追蹤。</span><span class="sxs-lookup"><span data-stu-id="13f57-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="13f57-292">例如：</span><span class="sxs-lookup"><span data-stu-id="13f57-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="13f57-293">在[搜尋](app-insights-diagnostic-search.md)，您可以輕鬆地篩選出所有特定嚴重性等級的相關 tooa 特定資料庫的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="13f57-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="13f57-294">分析中的追蹤</span><span class="sxs-lookup"><span data-stu-id="13f57-294">Traces in Analytics</span></span>

<span data-ttu-id="13f57-295">在[應用程式 Insights 分析](app-insights-analytics.md)，呼叫 tooTrackTrace 顯示在 hello`traces`資料表。</span><span class="sxs-lookup"><span data-stu-id="13f57-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="13f57-296">如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。</span><span class="sxs-lookup"><span data-stu-id="13f57-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="13f57-297">範例 itemCount = = 10，10 個呼叫過，即表示`trackTrace()`，hello 取樣程序時，才傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="13f57-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="13f57-298">tooget 追蹤呼叫正確計數，您應該使用因此程式碼例如`traces | summarize sum(itemCount)`。</span><span class="sxs-lookup"><span data-stu-id="13f57-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="13f57-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="13f57-299">TrackDependency</span></span>
<span data-ttu-id="13f57-300">使用 hello TrackDependency 呼叫 tootrack hello 回應時間與成功率呼叫 tooan 外部程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="13f57-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="13f57-301">hello 結果會出現在 hello hello 入口網站中的相依性圖表中。</span><span class="sxs-lookup"><span data-stu-id="13f57-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="13f57-302">請記住 Sdk 包含該 hello 伺服器[相依模組](app-insights-asp-net-dependencies.md)，會探索並自動追蹤特定相依性呼叫，例如 toodatabases 和 REST Api。</span><span class="sxs-lookup"><span data-stu-id="13f57-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="13f57-303">您有 tooinstall 伺服器 toomake hello 模組上的代理程式工作。</span><span class="sxs-lookup"><span data-stu-id="13f57-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="13f57-304">如果您想 hello 自動化的追蹤的 tootrack 呼叫未攔截，或如果您不想 tooinstall hello 代理程式，您可以使用這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="13f57-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="13f57-305">一般相依性追蹤模組 hello，關閉 tooturn 編輯[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)和太刪除 hello 參考`DependencyCollector.DependencyTrackingTelemetryModule`。</span><span class="sxs-lookup"><span data-stu-id="13f57-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="13f57-306">分析中的相依性</span><span class="sxs-lookup"><span data-stu-id="13f57-306">Dependencies in Analytics</span></span>

<span data-ttu-id="13f57-307">在[應用程式 Insights 分析](app-insights-analytics.md)，trackDependency 呼叫顯示在 hello`dependencies`資料表。</span><span class="sxs-lookup"><span data-stu-id="13f57-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="13f57-308">如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。</span><span class="sxs-lookup"><span data-stu-id="13f57-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="13f57-309">範例 itemCount = = 10，10 呼叫 tootrackDependency() 的 hello 取樣程序時，才傳輸其中的表示。</span><span class="sxs-lookup"><span data-stu-id="13f57-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="13f57-310">目標元件的 tooget 正確的相依性計數分割，使用程式碼，例如：</span><span class="sxs-lookup"><span data-stu-id="13f57-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="13f57-311">tooassociate 相依性，其相關的要求與使用聯結：</span><span class="sxs-lookup"><span data-stu-id="13f57-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="13f57-312">排清資料</span><span class="sxs-lookup"><span data-stu-id="13f57-312">Flushing data</span></span>
<span data-ttu-id="13f57-313">一般來說，hello SDK 傳送有時候選擇 toominimize hello hello 使用者影響的資料。</span><span class="sxs-lookup"><span data-stu-id="13f57-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="13f57-314">不過，在某些情況下，您可能想 tooflush hello 緩衝區-比方說，如果您使用，如此會關閉應用程式中的 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="13f57-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="13f57-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="13f57-316">請注意 hello 函式是非同步的 hello[伺服器遙測通道](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)。</span><span class="sxs-lookup"><span data-stu-id="13f57-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="13f57-317">驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="13f57-317">Authenticated users</span></span>
<span data-ttu-id="13f57-318">在 Web 應用程式中，預設是透過 Cookie 來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="13f57-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="13f57-319">如果使用者從不同的電腦或瀏覽器存取您的 app 或刪除 Cookie，就可能多次計算他們。</span><span class="sxs-lookup"><span data-stu-id="13f57-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="13f57-320">如果使用者登入 tooyour 應用程式，您可以藉由設定 hello 驗證使用者識別碼 hello 瀏覽器程式碼中取得更精確的計數：</span><span class="sxs-lookup"><span data-stu-id="13f57-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="13f57-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="13f57-322">在 ASP.NET Web MVC 應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="13f57-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="13f57-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="13f57-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="13f57-324">它不是必要的 toouse hello 使用者的實際登入名稱。</span><span class="sxs-lookup"><span data-stu-id="13f57-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="13f57-325">它只需要 toobe 唯一 toothat 使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="13f57-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="13f57-326">它不能包含空格或任何 hello 字元`,;=|`。</span><span class="sxs-lookup"><span data-stu-id="13f57-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="13f57-327">也在工作階段 cookie 中設定並傳送 toohello 伺服器 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="13f57-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="13f57-328">如果已安裝 hello 伺服器 SDK，hello 驗證的使用者識別碼會傳送 hello 內容屬性的用戶端和伺服器的遙測資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="13f57-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="13f57-329">您可以接著對它進行篩選和搜尋。</span><span class="sxs-lookup"><span data-stu-id="13f57-329">You can then filter and search on it.</span></span>

<span data-ttu-id="13f57-330">如果您的應用程式會將使用者分組帳戶，您也可以傳遞 hello 帳戶的識別項 （以 hello 相同字元限制）。</span><span class="sxs-lookup"><span data-stu-id="13f57-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="13f57-331">在[計量瀏覽器](app-insights-metrics-explorer.md)中，您可建立可計算 [已驗證的使用者] 和 [使用者帳戶] 的圖表。</span><span class="sxs-lookup"><span data-stu-id="13f57-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="13f57-332">您也可以[搜尋](app-insights-diagnostic-search.md)具有特定使用者名稱和帳戶的用戶端資料點。</span><span class="sxs-lookup"><span data-stu-id="13f57-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="13f57-333"><a name="properties"></a>使用屬性篩選、搜尋和分割資料</span><span class="sxs-lookup"><span data-stu-id="13f57-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="13f57-334">您可以附加屬性和度量 tooyour 事件 （和也 toometrics、 頁面檢視、 例外狀況，以及其他遙測資料）。</span><span class="sxs-lookup"><span data-stu-id="13f57-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="13f57-335">*屬性*是字串值，您可以使用 toofilter 您遙測 hello 的使用情況報告。</span><span class="sxs-lookup"><span data-stu-id="13f57-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="13f57-336">例如，如果您的應用程式提供數個遊戲，您可以附加 hello hello 遊戲 tooeach 事件名稱，讓您可以查看哪些遊戲是普遍。</span><span class="sxs-lookup"><span data-stu-id="13f57-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="13f57-337">沒有 8192 hello 字串長度的限制。</span><span class="sxs-lookup"><span data-stu-id="13f57-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="13f57-338">(如果您想 toosend 大量的資料區塊時，使用 hello 訊息參數[TrackTrace](#track-trace)。)</span><span class="sxs-lookup"><span data-stu-id="13f57-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="13f57-339">*度量* 是可以用圖表方式呈現的數值。</span><span class="sxs-lookup"><span data-stu-id="13f57-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="13f57-340">比方說，您可能想 toosee，如果沒有達到您玩家正面對決的 hello 分數中逐漸增加。</span><span class="sxs-lookup"><span data-stu-id="13f57-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="13f57-341">hello 圖形分隔屬性，讓您可取得與 hello 事件傳送嗨可以區隔，或堆疊之不同遊戲的圖形。</span><span class="sxs-lookup"><span data-stu-id="13f57-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="13f57-342">正確顯示的度量值 toobe，它們應該大於或等於 too0。</span><span class="sxs-lookup"><span data-stu-id="13f57-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="13f57-343">有一些[屬性、 屬性值和度量的 hello 數目限制](#limits)，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="13f57-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="13f57-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="13f57-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="13f57-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="13f57-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="13f57-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="13f57-348">請注意不 toolog 中的個人識別資訊內容。</span><span class="sxs-lookup"><span data-stu-id="13f57-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="13f57-349">*如果您使用度量*，開啟計量瀏覽器，並從 hello 選取 hello 度量**自訂**群組：</span><span class="sxs-lookup"><span data-stu-id="13f57-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![開啟度量總管 中，選取 hello 圖表，並選取 hello 度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="13f57-351">如果未出現您度量，或如果 hello**自訂**標題不存在，關閉 hello 選取範圍 刀鋒視窗並再試一次。</span><span class="sxs-lookup"><span data-stu-id="13f57-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="13f57-352">度量有時可能需要一小時 toobe hello 管線的彙總資料。</span><span class="sxs-lookup"><span data-stu-id="13f57-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="13f57-353">*如果您使用屬性和度量*，根據 hello 屬性區隔 hello 度量：</span><span class="sxs-lookup"><span data-stu-id="13f57-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![設定群組，然後選取 依群組下的 hello 屬性](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="13f57-355">*在搜尋中診斷*，您可以檢視 hello 屬性和事件的個別發生次數的度量。</span><span class="sxs-lookup"><span data-stu-id="13f57-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![選取執行個體，然後選取 [...]](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="13f57-357">使用 hello**搜尋**欄位 toosee 事件項目具有特定屬性值。</span><span class="sxs-lookup"><span data-stu-id="13f57-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![將詞彙輸入 [搜尋] 中](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="13f57-359">[深入了解搜尋運算式](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="13f57-360">另一種方式 tooset 屬性和度量</span><span class="sxs-lookup"><span data-stu-id="13f57-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="13f57-361">如果是更方便，您可以收集 hello 參數中的個別物件的事件：</span><span class="sxs-lookup"><span data-stu-id="13f57-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="13f57-362">不要重複使用 hello 相同遙測項目執行個體 (`event`在此範例中) toocall Track*() 多次。</span><span class="sxs-lookup"><span data-stu-id="13f57-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="13f57-363">這可能會導致不正確的設定以傳送遙測 toobe。</span><span class="sxs-lookup"><span data-stu-id="13f57-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="13f57-364">分析中的自訂測量和屬性</span><span class="sxs-lookup"><span data-stu-id="13f57-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="13f57-365">在[分析](app-insights-analytics.md)，自訂的度量和屬性會顯示在 hello`customMeasurements`和`customDimensions`每個遙測記錄屬性。</span><span class="sxs-lookup"><span data-stu-id="13f57-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="13f57-366">比方說，如果您已經加入名為 「 遊戲 」 tooyour 要求遙測的屬性，此查詢 hello 次數的 「 遊戲 」 時，有不同的值會計算並顯示 hello 平均 hello 的自訂度量 「 分數 」:</span><span class="sxs-lookup"><span data-stu-id="13f57-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="13f57-367">請注意：</span><span class="sxs-lookup"><span data-stu-id="13f57-367">Notice that:</span></span>

* <span data-ttu-id="13f57-368">當您從 hello customDimensions 或 customMeasurements JSON 中擷取值時，它具有動態類型，以及因此您必須將它轉換`tostring`或`todouble`。</span><span class="sxs-lookup"><span data-stu-id="13f57-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="13f57-369">hello 可能性 tootake 帳戶[取樣](app-insights-sampling.md)，您應該使用`sum(itemCount)`，而非`count()`。</span><span class="sxs-lookup"><span data-stu-id="13f57-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="13f57-370"><a name="timed"></a> 計時事件</span><span class="sxs-lookup"><span data-stu-id="13f57-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="13f57-371">有時候您會想 toochart 多久採取 tooperform 動作。</span><span class="sxs-lookup"><span data-stu-id="13f57-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="13f57-372">例如，您可能想 tooknow 使用者採取 tooconsider 選擇在遊戲的時間長度。</span><span class="sxs-lookup"><span data-stu-id="13f57-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="13f57-373">您可以在這個使用 hello 度量參數。</span><span class="sxs-lookup"><span data-stu-id="13f57-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="13f57-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="13f57-375"><a name="defaults"></a>自訂遙測資料的預設屬性</span><span class="sxs-lookup"><span data-stu-id="13f57-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="13f57-376">如果您想 tooset 預設屬性值的某些 hello 您撰寫的自訂事件時，您可以設定它們 TelemetryClient 執行個體中。</span><span class="sxs-lookup"><span data-stu-id="13f57-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="13f57-377">它們是從該用戶端傳送的附加的 tooevery 遙測項目。</span><span class="sxs-lookup"><span data-stu-id="13f57-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="13f57-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="13f57-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="13f57-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="13f57-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="13f57-381">個別的遙測呼叫可以覆寫其屬性字典中的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="13f57-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="13f57-382">*針對 JavaScript Web 用戶端*， [請使用 JavaScript 遙測初始設定式](#js-initializer)。</span><span class="sxs-lookup"><span data-stu-id="13f57-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="13f57-383">*tooadd 屬性 tooall 遙測*，包括標準集合模組中的 hello 資料[實作`ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties)。</span><span class="sxs-lookup"><span data-stu-id="13f57-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="13f57-384">取樣、篩選及處理遙測資料</span><span class="sxs-lookup"><span data-stu-id="13f57-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="13f57-385">傳送嗨 SDK 從之前您可以撰寫指定碼 tooprocess 您遙測。</span><span class="sxs-lookup"><span data-stu-id="13f57-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="13f57-386">hello 處理包括傳送 hello 標準遙測模組，例如 HTTP 要求的集合和相依性集合中的資料。</span><span class="sxs-lookup"><span data-stu-id="13f57-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="13f57-387">[將屬性加入](app-insights-api-filtering-sampling.md#add-properties)藉由實作 tootelemetry `ITelemetryInitializer`。</span><span class="sxs-lookup"><span data-stu-id="13f57-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="13f57-388">例如，您可以新增版本號碼或從其他屬性計算得出的值。</span><span class="sxs-lookup"><span data-stu-id="13f57-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="13f57-389">[篩選](app-insights-api-filtering-sampling.md#filtering)可以修改或捨棄遙測之前它會傳送 hello SDK 藉由實作, `ITelemetryProcesor`。</span><span class="sxs-lookup"><span data-stu-id="13f57-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="13f57-390">您控制所傳送或捨棄，但有 tooaccount hello 效果，在您的指標。</span><span class="sxs-lookup"><span data-stu-id="13f57-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="13f57-391">根據如何捨棄的項目，您可能會遺失 hello 能力 toonavigate 相關的項目之間。</span><span class="sxs-lookup"><span data-stu-id="13f57-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="13f57-392">[取樣](app-insights-api-filtering-sampling.md)是從您的應用程式 toohello 入口網站傳送資料的已封裝的方案 tooreduce hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="13f57-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="13f57-393">它會以不會影響顯示 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="13f57-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="13f57-394">它會以不影響能力 toodiagnose 問題相關的項目，例如例外狀況、 要求和頁面檢視之間巡覽。</span><span class="sxs-lookup"><span data-stu-id="13f57-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="13f57-395">[深入了解](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="13f57-396">停用遙測</span><span class="sxs-lookup"><span data-stu-id="13f57-396">Disabling telemetry</span></span>
<span data-ttu-id="13f57-397">太*動態停止和啟動*hello 遙測的收集和傳輸：</span><span class="sxs-lookup"><span data-stu-id="13f57-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="13f57-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="13f57-399">太*停用選取的標準收集器*-例如，效能計數器、 HTTP 要求或相依性-刪除或標記為註解中的 hello 相關行[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。例如，如果您想 toosend TrackRequest 資料，您可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="13f57-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="13f57-400"><a name="debug"></a>開發人員模式</span><span class="sxs-lookup"><span data-stu-id="13f57-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="13f57-401">偵錯期間，就很有用的 toohave 您遙測加速 hello 管線，讓您可以立即查看結果。</span><span class="sxs-lookup"><span data-stu-id="13f57-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="13f57-402">您也取得額外的訊息可協助您追蹤 hello 遙測的任何問題。</span><span class="sxs-lookup"><span data-stu-id="13f57-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="13f57-403">在生產環境中將它關閉，因為它可能會拖慢您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13f57-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="13f57-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="13f57-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="13f57-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="13f57-406"><a name="ikey"></a>設定所選自訂遙測的 hello 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="13f57-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="13f57-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="13f57-408"><a name="dynamic-ikey"></a> 動態檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="13f57-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="13f57-409">tooavoid 混遙測從開發、 測試和生產環境中，您可以[建立個別的 Application Insights 資源](app-insights-create-new-resource.md)並變更其索引鍵，視 hello 環境而定。</span><span class="sxs-lookup"><span data-stu-id="13f57-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="13f57-410">而不是從 hello 設定檔中取得 hello 檢測金鑰，您可以在程式碼中設定。</span><span class="sxs-lookup"><span data-stu-id="13f57-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="13f57-411">在初始設定方法，例如 global.aspx.cs ASP.NET 服務中設定 hello 機碼：</span><span class="sxs-lookup"><span data-stu-id="13f57-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="13f57-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="13f57-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="13f57-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="13f57-414">在網頁中，您可能想 tooset 從 hello web 伺服器的狀態，而不是常值到 hello 指令碼編碼。</span><span class="sxs-lookup"><span data-stu-id="13f57-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="13f57-415">例如，在 ASP.NET 應用程式中產生的網頁：</span><span class="sxs-lookup"><span data-stu-id="13f57-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="13f57-416">*Razor 中的 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="13f57-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="13f57-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="13f57-417">TelemetryContext</span></span>
<span data-ttu-id="13f57-418">TelemetryClient 具有內容屬性，其中包含與所有遙測資料一起傳送的值。</span><span class="sxs-lookup"><span data-stu-id="13f57-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="13f57-419">它們通常設定 hello 標準遙測模組，但您也可以設定他們自己。</span><span class="sxs-lookup"><span data-stu-id="13f57-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="13f57-420">例如：</span><span class="sxs-lookup"><span data-stu-id="13f57-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="13f57-421">如果您設定了任何這些值的自行，請考慮移除 hello 相關行[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，如此混淆不到您的 hello 標準值和值。</span><span class="sxs-lookup"><span data-stu-id="13f57-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="13f57-422">**元件**: hello 應用程式和其版本。</span><span class="sxs-lookup"><span data-stu-id="13f57-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="13f57-423">**裝置**: hello hello 應用程式執行所在的裝置相關資料。</span><span class="sxs-lookup"><span data-stu-id="13f57-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="13f57-424">（在 web 應用程式，這是 hello 伺服器或用戶端裝置從傳送嗨遙測。）</span><span class="sxs-lookup"><span data-stu-id="13f57-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="13f57-425">**InstrumentationKey**: hello Azure hello 遙測出現的位置中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="13f57-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="13f57-426">通常會揀選自 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="13f57-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="13f57-427">**位置**: hello hello 裝置的地理位置。</span><span class="sxs-lookup"><span data-stu-id="13f57-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="13f57-428">**作業**： 在 web 應用程式，hello 目前 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="13f57-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="13f57-429">在其他應用程式類型，您可以一起設定，這個 toogroup 事件。</span><span class="sxs-lookup"><span data-stu-id="13f57-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="13f57-430">**識別碼**：產生的值，與不同事件相互關聯，如此當您在診斷搜尋中檢查任何事件時，您可以發現相關項目。</span><span class="sxs-lookup"><span data-stu-id="13f57-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="13f57-431">**名稱**： 識別項通常 hello 的 hello HTTP 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="13f57-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="13f57-432">**SyntheticSource**： 如果不為 null 或空白，表示該 hello 要求的來源 hello 的字串已經被識別為機器人或 web 測試。</span><span class="sxs-lookup"><span data-stu-id="13f57-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="13f57-433">根據預設，會從計量瀏覽器的計算中排除。</span><span class="sxs-lookup"><span data-stu-id="13f57-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="13f57-434">**屬性**：與所有遙測資料一起傳送的屬性。</span><span class="sxs-lookup"><span data-stu-id="13f57-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="13f57-435">可以在個別 Track* 呼叫中覆寫。</span><span class="sxs-lookup"><span data-stu-id="13f57-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="13f57-436">**工作階段**: hello 使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="13f57-436">**Session**: hello user's session.</span></span> <span data-ttu-id="13f57-437">設定 hello 識別碼 hello 使用者已使用一段時間後會變更的 tooa 產生值。</span><span class="sxs-lookup"><span data-stu-id="13f57-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="13f57-438">**使用者**：使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="13f57-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="13f57-439">限制</span><span class="sxs-lookup"><span data-stu-id="13f57-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="13f57-440">達到 hello 資料速率限制，使用 tooavoid[取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="13f57-441">toodetermine 如何保持 long 資料，請參閱[資料保留和隱私權](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="13f57-442">參考文件</span><span class="sxs-lookup"><span data-stu-id="13f57-442">Reference docs</span></span>
* [<span data-ttu-id="13f57-443">ASP.NET 參考</span><span class="sxs-lookup"><span data-stu-id="13f57-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="13f57-444">Java 參考</span><span class="sxs-lookup"><span data-stu-id="13f57-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="13f57-445">JavaScript 參考</span><span class="sxs-lookup"><span data-stu-id="13f57-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="13f57-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="13f57-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="13f57-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="13f57-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="13f57-448">SDK 程式碼</span><span class="sxs-lookup"><span data-stu-id="13f57-448">SDK code</span></span>
* [<span data-ttu-id="13f57-449">ASP.NET 核心 SDK</span><span class="sxs-lookup"><span data-stu-id="13f57-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="13f57-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="13f57-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="13f57-451">Windows Server 套件</span><span class="sxs-lookup"><span data-stu-id="13f57-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="13f57-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="13f57-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="13f57-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="13f57-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="13f57-454">所有平台</span><span class="sxs-lookup"><span data-stu-id="13f57-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="13f57-455">問題</span><span class="sxs-lookup"><span data-stu-id="13f57-455">Questions</span></span>
* <span data-ttu-id="13f57-456">*Track_() 呼叫會擲回什麼例外狀況？*</span><span class="sxs-lookup"><span data-stu-id="13f57-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="13f57-457">無。</span><span class="sxs-lookup"><span data-stu-id="13f57-457">None.</span></span> <span data-ttu-id="13f57-458">您不需要 toowrap try catch 子句中。</span><span class="sxs-lookup"><span data-stu-id="13f57-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="13f57-459">如果 hello SDK 發生問題時，它就會在 hello 偵錯主控台輸出中記錄訊息和--如果 hello 訊息取得-中診斷的搜尋。</span><span class="sxs-lookup"><span data-stu-id="13f57-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="13f57-460">*是否有從 hello 入口網站 REST API tooget 資料？*</span><span class="sxs-lookup"><span data-stu-id="13f57-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="13f57-461">是，hello[資料存取 API](https://dev.applicationinsights.io/)。</span><span class="sxs-lookup"><span data-stu-id="13f57-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="13f57-462">其他方式 tooextract 資料包含[從分析 tooPower BI 匯出](app-insights-export-power-bi.md)和[連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="13f57-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="13f57-463"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="13f57-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="13f57-464">搜尋事件和記錄</span><span class="sxs-lookup"><span data-stu-id="13f57-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="13f57-465">疑難排解</span><span class="sxs-lookup"><span data-stu-id="13f57-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


