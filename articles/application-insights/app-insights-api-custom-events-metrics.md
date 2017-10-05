---
title: "自訂事件和度量的 Application Insights API | Microsoft Docs"
description: "在您的裝置或桌面應用程式、網頁或服務中插入幾行程式碼，來追蹤使用狀況及診斷問題。"
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
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="df466-103">自訂事件和度量的 Application Insights API</span><span class="sxs-lookup"><span data-stu-id="df466-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="df466-104">在您的應用程式中插入幾行程式碼，以了解使用者對它進行的動作或協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="df466-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="df466-105">您可以從裝置和桌面應用程式、Web 用戶端以及 Web 伺服器傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="df466-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="df466-106">使用 [Azure Application Insights](app-insights-overview.md) 核心遙測 API 來傳送自訂的事件和度量，以及您自己的標準遙測版本。</span><span class="sxs-lookup"><span data-stu-id="df466-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="df466-107">這個 API 與標準 Application Insights 資料收集器所使用的 API 相同。</span><span class="sxs-lookup"><span data-stu-id="df466-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="df466-108">API summary</span><span class="sxs-lookup"><span data-stu-id="df466-108">API summary</span></span>
<span data-ttu-id="df466-109">API 是跨所有平台統一的，除了一些小變化形式。</span><span class="sxs-lookup"><span data-stu-id="df466-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="df466-110">方法</span><span class="sxs-lookup"><span data-stu-id="df466-110">Method</span></span> | <span data-ttu-id="df466-111">用於</span><span class="sxs-lookup"><span data-stu-id="df466-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="df466-112">頁面、畫面、刀鋒視窗或表單。</span><span class="sxs-lookup"><span data-stu-id="df466-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="df466-113">使用者動作和其他事件。</span><span class="sxs-lookup"><span data-stu-id="df466-113">User actions and other events.</span></span> <span data-ttu-id="df466-114">用來追蹤使用者行為，或監視效能。</span><span class="sxs-lookup"><span data-stu-id="df466-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="df466-115">效能度量，例如與特定事件不相關的佇列長度。</span><span class="sxs-lookup"><span data-stu-id="df466-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="df466-116">記錄例外狀況以供診斷。</span><span class="sxs-lookup"><span data-stu-id="df466-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="df466-117">追蹤與其他事件的發生相對位置，並且檢查堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="df466-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="df466-118">記錄伺服器要求的頻率和持續時間以進行效能分析。</span><span class="sxs-lookup"><span data-stu-id="df466-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="df466-119">診斷記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="df466-119">Diagnostic log messages.</span></span> <span data-ttu-id="df466-120">您也可以擷取第三方記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df466-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="df466-121">記錄應用程式所依賴之外部元件呼叫的持續時間及頻率。</span><span class="sxs-lookup"><span data-stu-id="df466-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="df466-122">您可以 [附加屬性和度量](#properties) 至這裡大部分的遙測呼叫。</span><span class="sxs-lookup"><span data-stu-id="df466-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="df466-123"><a name="prep"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="df466-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="df466-124">如果您還沒有 Application Insights SDK 的參考：</span><span class="sxs-lookup"><span data-stu-id="df466-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="df466-125">將 Application Insights SDK 加入至專案：</span><span class="sxs-lookup"><span data-stu-id="df466-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="df466-126">ASP.NET 專案</span><span class="sxs-lookup"><span data-stu-id="df466-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="df466-127">Java 專案</span><span class="sxs-lookup"><span data-stu-id="df466-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="df466-128">每個網頁中的 JavaScript</span><span class="sxs-lookup"><span data-stu-id="df466-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="df466-129">在裝置或 Web 伺服器程式碼中，加入：</span><span class="sxs-lookup"><span data-stu-id="df466-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="df466-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="df466-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="df466-131">*Visual Basic：*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="df466-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="df466-132">*Java：* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="df466-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="df466-133">建構 TelemetryClient 執行個體</span><span class="sxs-lookup"><span data-stu-id="df466-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="df466-134">建構 `TelemetryClient` 的執行個體 (除了網頁中的 JavaScript)：</span><span class="sxs-lookup"><span data-stu-id="df466-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="df466-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="df466-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="df466-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="df466-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="df466-138">TelemetryClient 具備執行緒安全。</span><span class="sxs-lookup"><span data-stu-id="df466-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="df466-139">我們建議針對您每個應用程式的模組使用 TelemetryClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="df466-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="df466-140">比方說，您可能在 Web 服務中有一個 TelemetryClient 執行個體用來報告傳入的 HTTP 要求，以及中介類別中的另一個執行個體用來告報商業邏輯事件。</span><span class="sxs-lookup"><span data-stu-id="df466-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="df466-141">您可以設定如 `TelemetryClient.Context.User.Id` 的屬性以追蹤使用者和工作階段，或 `TelemetryClient.Context.Device.Id` 來識別電腦。</span><span class="sxs-lookup"><span data-stu-id="df466-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="df466-142">這項資訊會附加至執行個體所傳送的所有事件。</span><span class="sxs-lookup"><span data-stu-id="df466-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="df466-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="df466-143">TrackEvent</span></span>
<span data-ttu-id="df466-144">在 Application Insights 中，「自訂事件」是您可以在[計量瀏覽器](app-insights-metrics-explorer.md)顯示為彙總計數，以及在[診斷搜尋](app-insights-diagnostic-search.md)中顯示為個別發生點的資料點。</span><span class="sxs-lookup"><span data-stu-id="df466-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="df466-145">(它與 MVC 或其他架構的「事件」不相關。)</span><span class="sxs-lookup"><span data-stu-id="df466-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="df466-146">在您的程式碼中插入 `TrackEvent` 呼叫，以計算各種事件。</span><span class="sxs-lookup"><span data-stu-id="df466-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="df466-147">使用者選擇特定功能的頻率、達成特定目標的頻率，或他們犯特定類型錯誤的頻率。</span><span class="sxs-lookup"><span data-stu-id="df466-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="df466-148">例如，在遊戲應用程式中，每當使用者贏得遊戲時傳送事件：</span><span class="sxs-lookup"><span data-stu-id="df466-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="df466-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="df466-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="df466-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="df466-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="df466-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="df466-153">在 Microsoft Azure 入口網站中檢視您的事件</span><span class="sxs-lookup"><span data-stu-id="df466-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="df466-154">若要查看事件計數，請開啟 [[計量瀏覽器](app-insights-metrics-explorer.md)] 刀鋒視窗、新增圖表，然後再選取 [事件]。</span><span class="sxs-lookup"><span data-stu-id="df466-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![查看自訂事件的計數](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="df466-156">若要比較不同事件的計數，請將圖表類型設為 [方格]，並依事件名稱進行分組：</span><span class="sxs-lookup"><span data-stu-id="df466-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![設定圖表類型和群組](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="df466-158">在方格中逐一點選事件名稱，以查看該事件的個別發生次數。</span><span class="sxs-lookup"><span data-stu-id="df466-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="df466-159">若要查看詳細資料 - 按一下清單中的任何發生項目。</span><span class="sxs-lookup"><span data-stu-id="df466-159">To see more detail - click any occurrence in the list.</span></span>

![鑽研事件](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="df466-161">若要在「搜尋」或「計量瀏覽器」中專注查看特定事件，請將刀鋒視窗篩選器設為您感興趣的事件名稱：</span><span class="sxs-lookup"><span data-stu-id="df466-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![開啟 [篩選器]，展開 [事件名稱]，然後選取一或多個值](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="df466-163">分析中的自訂事件</span><span class="sxs-lookup"><span data-stu-id="df466-163">Custom events in Analytics</span></span>

<span data-ttu-id="df466-164">[Application Insights 分析](app-insights-analytics.md)的 `customEvents` 資料表中有提供遙測資料。</span><span class="sxs-lookup"><span data-stu-id="df466-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="df466-165">每個資料列各代表應用程式中的一個 `trackEvent(..)` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="df466-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="df466-166">如果[取樣](app-insights-sampling.md)運作中，itemCount 屬性會顯示大於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="df466-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="df466-167">例如，itemCount==10 表示在 trackEvent() 的 10 個呼叫中，取樣處理序只會傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="df466-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="df466-168">若要取得正確的自訂事件計數，您應該使用程式碼，例如 `customEvent | summarize sum(itemCount)`。</span><span class="sxs-lookup"><span data-stu-id="df466-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="df466-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="df466-169">TrackMetric</span></span>

<span data-ttu-id="df466-170">Application Insights 可以將未附加至特定事件的計量繪製成圖表。</span><span class="sxs-lookup"><span data-stu-id="df466-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="df466-171">例如，您可以定期監視佇列長度。</span><span class="sxs-lookup"><span data-stu-id="df466-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="df466-172">當您使用計量時，個別測量的重要性就不如變化和趨勢，因此統計圖表很有用。</span><span class="sxs-lookup"><span data-stu-id="df466-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="df466-173">為了將計量傳送至 Application Insights，您可以使用 `TrackMetric(..)` API。</span><span class="sxs-lookup"><span data-stu-id="df466-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="df466-174">您有兩種方式可以傳送計量：</span><span class="sxs-lookup"><span data-stu-id="df466-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="df466-175">單一值：</span><span class="sxs-lookup"><span data-stu-id="df466-175">Single value.</span></span> <span data-ttu-id="df466-176">每次在應用程式中執行一個測量，都會將對應值傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="df466-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="df466-177">例如，假設您有一個描述容器中項目數的計量。</span><span class="sxs-lookup"><span data-stu-id="df466-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="df466-178">在特定期間內，您先將 3 個項目放入容器中，再移除 2 個項目。</span><span class="sxs-lookup"><span data-stu-id="df466-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="df466-179">因此，您會呼叫 `TrackMetric` 兩次：先傳遞值 `3`，再傳遞值 `-2`。</span><span class="sxs-lookup"><span data-stu-id="df466-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="df466-180">Application Insights 會代替您儲存這兩個值。</span><span class="sxs-lookup"><span data-stu-id="df466-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="df466-181">彙總：</span><span class="sxs-lookup"><span data-stu-id="df466-181">Aggregation.</span></span> <span data-ttu-id="df466-182">使用計量時，每個單一測量並不重要。</span><span class="sxs-lookup"><span data-stu-id="df466-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="df466-183">相反地，在特定期間內發生的狀況摘要才重要。</span><span class="sxs-lookup"><span data-stu-id="df466-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="df466-184">這類摘要稱為_彙總_。</span><span class="sxs-lookup"><span data-stu-id="df466-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="df466-185">在上述範例中，該期間的彙總計量總和為 `1`，而計量值的計數為 `2`。</span><span class="sxs-lookup"><span data-stu-id="df466-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="df466-186">使用彙總方法時，您只會在每段期間叫用 `TrackMetric` 一次，並傳送彙總值。</span><span class="sxs-lookup"><span data-stu-id="df466-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="df466-187">這是建議的方法，因為它可以藉由傳送較少資料點至 Application Insights，同時仍收集所有相關資訊，來大幅降低成本和效能負擔。</span><span class="sxs-lookup"><span data-stu-id="df466-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="df466-188">範例：</span><span class="sxs-lookup"><span data-stu-id="df466-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="df466-189">單一值</span><span class="sxs-lookup"><span data-stu-id="df466-189">Single values</span></span>

<span data-ttu-id="df466-190">若要傳送單一計量值︰</span><span class="sxs-lookup"><span data-stu-id="df466-190">To send a single metric value:</span></span>

<span data-ttu-id="df466-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="df466-192">C#、Java</span><span class="sxs-lookup"><span data-stu-id="df466-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="df466-193">彙總計量</span><span class="sxs-lookup"><span data-stu-id="df466-193">Aggregating metrics</span></span>

<span data-ttu-id="df466-194">建議先彙總計量再從應用程式傳送計量，以降低頻寬、成本，並提升效能。</span><span class="sxs-lookup"><span data-stu-id="df466-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="df466-195">程式碼的彙總範例如下：</span><span class="sxs-lookup"><span data-stu-id="df466-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="df466-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-196">*C#*</span></span>

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
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
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
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="df466-197">[計量瀏覽器] 中的自訂計量</span><span class="sxs-lookup"><span data-stu-id="df466-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="df466-198">若要查看結果，開啟 [計量瀏覽器] 並加入新的圖表。</span><span class="sxs-lookup"><span data-stu-id="df466-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="df466-199">請編輯圖表以顯示您的計量。</span><span class="sxs-lookup"><span data-stu-id="df466-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="df466-200">自訂計量可能需要幾分鐘的時間才會出現在可用計量清單中。</span><span class="sxs-lookup"><span data-stu-id="df466-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![新增圖表或選取圖表，並在 [自訂] 底下選取您的度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="df466-202">Analytics 中的自訂計量</span><span class="sxs-lookup"><span data-stu-id="df466-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="df466-203">[Application Insights 分析](app-insights-analytics.md)的 `customMetrics` 資料表中有提供遙測資料。</span><span class="sxs-lookup"><span data-stu-id="df466-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="df466-204">每個資料列各代表應用程式中的一個 `trackMetric(..)` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="df466-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="df466-205">`valueSum` - 這是測量結果的總和。</span><span class="sxs-lookup"><span data-stu-id="df466-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="df466-206">若要取得平均值，請將它除以 `valueCount`。</span><span class="sxs-lookup"><span data-stu-id="df466-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="df466-207">`valueCount` - 彙總到這個 `trackMetric(..)` 呼叫的測量數目。</span><span class="sxs-lookup"><span data-stu-id="df466-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="df466-208">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="df466-208">Page views</span></span>
<span data-ttu-id="df466-209">在裝置或網頁應用程式中，每個畫面或頁面載入時預設會傳送頁面檢視遙測。</span><span class="sxs-lookup"><span data-stu-id="df466-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="df466-210">但是，您可以變更為在其他或不同的時間追蹤頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="df466-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="df466-211">例如，在顯示索引標籤或刀鋒視窗的應用程式中，您可能想要在使用者每次開啟新的刀鋒視窗時追蹤頁面。</span><span class="sxs-lookup"><span data-stu-id="df466-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![[概觀] 刀鋒視窗上的使用方式透鏡](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="df466-213">使用者和工作階段資料會與頁面檢視一起傳送為屬性，當有頁面檢視遙測時，讓使用者與工作階段圖表顯現。</span><span class="sxs-lookup"><span data-stu-id="df466-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="df466-214">自訂頁面檢視</span><span class="sxs-lookup"><span data-stu-id="df466-214">Custom page views</span></span>
<span data-ttu-id="df466-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="df466-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="df466-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="df466-218">如果您在不同的 HTML 網頁內有數個索引標籤，您也可以指定 URL：</span><span class="sxs-lookup"><span data-stu-id="df466-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="df466-219">計時頁面檢視</span><span class="sxs-lookup"><span data-stu-id="df466-219">Timing page views</span></span>
<span data-ttu-id="df466-220">根據預設，回報為**頁面檢視載入時間**的時間是測量從瀏覽器傳送要求開始，直到呼叫瀏覽器的頁面載入事件為止的時間。</span><span class="sxs-lookup"><span data-stu-id="df466-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="df466-221">相反地，您可以：</span><span class="sxs-lookup"><span data-stu-id="df466-221">Instead, you can either:</span></span>

* <span data-ttu-id="df466-222">在 [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) 呼叫中設定明確的持續時間：`appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`。</span><span class="sxs-lookup"><span data-stu-id="df466-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="df466-223">使用頁面檢視計時呼叫 `startTrackPage` 和 `stopTrackPage`。</span><span class="sxs-lookup"><span data-stu-id="df466-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="df466-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="df466-225">...</span><span class="sxs-lookup"><span data-stu-id="df466-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="df466-226">做為第一個參數的名稱會將開始和停止呼叫相關聯。</span><span class="sxs-lookup"><span data-stu-id="df466-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="df466-227">預設為目前的頁面名稱。</span><span class="sxs-lookup"><span data-stu-id="df466-227">It defaults to the current page name.</span></span>

<span data-ttu-id="df466-228">產生後顯示在計量瀏覽器中的頁面載入持續時間是衍生自開始和停止呼叫之間的間隔。</span><span class="sxs-lookup"><span data-stu-id="df466-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="df466-229">取決於您實際計時的間隔。</span><span class="sxs-lookup"><span data-stu-id="df466-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="df466-230">分析中的頁面遙測</span><span class="sxs-lookup"><span data-stu-id="df466-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="df466-231">在[分析](app-insights-analytics.md)中，有兩個資料表顯示瀏覽器作業的資料：</span><span class="sxs-lookup"><span data-stu-id="df466-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="df466-232">`pageViews` 資料表包含 URL 和網頁標題的相關資料</span><span class="sxs-lookup"><span data-stu-id="df466-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="df466-233">`browserTimings` 資料表包含用戶端效能的相關資料，例如處理傳入資料所花費的時間</span><span class="sxs-lookup"><span data-stu-id="df466-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="df466-234">若要了解瀏覽器處理不同頁面所花費的時間：</span><span class="sxs-lookup"><span data-stu-id="df466-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="df466-235">若要探索不同瀏覽器的熱門程度：</span><span class="sxs-lookup"><span data-stu-id="df466-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="df466-236">若要將頁面檢視與 AJAX 呼叫產生關聯，請聯結相依性：</span><span class="sxs-lookup"><span data-stu-id="df466-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="df466-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="df466-237">TrackRequest</span></span>
<span data-ttu-id="df466-238">伺服器 SDK 會使用 TrackRequest 來記錄 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="df466-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="df466-239">如果您想要在沒有 Web 服務模組執行的內容中模擬要求，您也可以自行呼叫。</span><span class="sxs-lookup"><span data-stu-id="df466-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="df466-240">不過，建議用來傳送要求遙測的方式是在要求作為<a href="#operation-context">作業內容</a>的地方。</span><span class="sxs-lookup"><span data-stu-id="df466-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="df466-241">作業內容</span><span class="sxs-lookup"><span data-stu-id="df466-241">Operation context</span></span>
<span data-ttu-id="df466-242">您可藉由為遙測項目附加通用的作業識別碼，讓它們能夠關聯在一起。</span><span class="sxs-lookup"><span data-stu-id="df466-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="df466-243">標準的要求追蹤模組會針對在處理 HTTP 要求時傳送的例外狀況和其他事件執行此動作。</span><span class="sxs-lookup"><span data-stu-id="df466-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="df466-244">在[搜尋](app-insights-diagnostic-search.md)和[分析](app-insights-analytics.md)中，您可以使用此識別碼，輕易地找出任何與要求相關聯的事件。</span><span class="sxs-lookup"><span data-stu-id="df466-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="df466-245">設定此識別碼的最簡單方式是使用下列模式來設定作業內容：</span><span class="sxs-lookup"><span data-stu-id="df466-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="df466-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="df466-247">在設定作業內容時，`StartOperation` 會建立所指定類型的遙測項目。</span><span class="sxs-lookup"><span data-stu-id="df466-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="df466-248">它會在您處置作業時或您明確地呼叫 `StopOperation` 時傳送遙測項目。</span><span class="sxs-lookup"><span data-stu-id="df466-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="df466-249">如果您使用 `RequestTelemetry` 做為遙測類型，則其持續時間會設定為開始與停止之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="df466-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="df466-250">作業內容不可為巢狀。</span><span class="sxs-lookup"><span data-stu-id="df466-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="df466-251">如果已經有作業內容，則其識別碼會與所有內含項目 (包括使用 `StartOperation` 建立的項目) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="df466-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="df466-252">在搜尋中，會使用作業內容來建立 [相關項目] 清單：</span><span class="sxs-lookup"><span data-stu-id="df466-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![相關項目](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="df466-254">如需有關自訂作業追蹤的詳細資訊，請參閱 [application-insights-custom-operations-tracking.md]。</span><span class="sxs-lookup"><span data-stu-id="df466-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="df466-255">分析中的要求</span><span class="sxs-lookup"><span data-stu-id="df466-255">Requests in Analytics</span></span> 

<span data-ttu-id="df466-256">在 [Application Insights 分析](app-insights-analytics.md)中，要求會顯示在 `requests` 資料表中。</span><span class="sxs-lookup"><span data-stu-id="df466-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="df466-257">如果[取樣](app-insights-sampling.md)運作中，itemCount 屬性將會顯示大於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="df466-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="df466-258">例如，itemCount==10 表示在 trackRequest() 的 10 個呼叫中，取樣處理序只會傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="df466-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="df466-259">若要取得依要求名稱分割的正確要求計數和平均持續時間，請使用類似如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="df466-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="df466-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="df466-260">TrackException</span></span>
<span data-ttu-id="df466-261">傳送例外狀況至 Application Insights︰</span><span class="sxs-lookup"><span data-stu-id="df466-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="df466-262">以[計算數目](app-insights-metrics-explorer.md)，來指出問題的頻率。</span><span class="sxs-lookup"><span data-stu-id="df466-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="df466-263">以[檢查個別出現次數](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="df466-264">報告包含堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="df466-264">The reports include the stack traces.</span></span>

<span data-ttu-id="df466-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="df466-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="df466-267">SDK 將自動攔截許多例外狀況，所以您不一定需要明確呼叫 TrackException。</span><span class="sxs-lookup"><span data-stu-id="df466-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="df466-268">ASP.NET：[撰寫程式碼以攔截例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="df466-269">J2EE：[自動攔截例外狀況](app-insights-java-get-started.md#exceptions-and-request-failures)。</span><span class="sxs-lookup"><span data-stu-id="df466-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="df466-270">JavaScript：自動攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="df466-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="df466-271">如果您想要停用自動收集，請在您插入網頁的程式碼片段中加入一行：</span><span class="sxs-lookup"><span data-stu-id="df466-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="df466-272">分析中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="df466-272">Exceptions in Analytics</span></span>

<span data-ttu-id="df466-273">在 [Application Insights 分析](app-insights-analytics.md)中，例外狀況會顯示在 `exceptions` 資料表中。</span><span class="sxs-lookup"><span data-stu-id="df466-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="df466-274">如果[取樣](app-insights-sampling.md)運作中，`itemCount` 屬性會顯示大於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="df466-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="df466-275">例如，itemCount==10 表示在 trackException() 的 10 個呼叫中，取樣處理序只會傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="df466-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="df466-276">若要取得依例外狀況類型分割的正確例外狀況計數，請使用類似如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="df466-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="df466-277">大多數重要堆疊資訊已擷取到不同的變數中，但您可以拉開 `details` 結構以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="df466-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="df466-278">由於這是動態結構，因此您應該將結果轉換成預期的類型。</span><span class="sxs-lookup"><span data-stu-id="df466-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="df466-279">例如：</span><span class="sxs-lookup"><span data-stu-id="df466-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="df466-280">若要將例外狀況與其相關要求產生關聯，請使用聯結：</span><span class="sxs-lookup"><span data-stu-id="df466-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="df466-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="df466-281">TrackTrace</span></span>
<span data-ttu-id="df466-282">使用 TrackTrace 可協助您藉由將 "breadcrumb trail" 傳送至 Application Insights 來診斷問題。</span><span class="sxs-lookup"><span data-stu-id="df466-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="df466-283">您可以傳送診斷資料區塊，並且在[診斷搜尋](app-insights-diagnostic-search.md)中檢查。</span><span class="sxs-lookup"><span data-stu-id="df466-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="df466-284">[記錄配接器](app-insights-asp-net-trace-logs.md)使用此 API 將第三方記錄傳送至入口網站。</span><span class="sxs-lookup"><span data-stu-id="df466-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="df466-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="df466-286">您可以搜尋訊息內容，但是 (不同於屬性值) 您無法在其中進行篩選。</span><span class="sxs-lookup"><span data-stu-id="df466-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="df466-287">`message` 上的大小限制比屬性上的限制高得多。</span><span class="sxs-lookup"><span data-stu-id="df466-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="df466-288">TrackTrace 的優點在於您可以將較長的資料放在訊息中。</span><span class="sxs-lookup"><span data-stu-id="df466-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="df466-289">例如，您可以在該處編碼 POST 資料。</span><span class="sxs-lookup"><span data-stu-id="df466-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="df466-290">此外，您可以在訊息中新增嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="df466-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="df466-291">就像其他遙測一樣，您可以新增屬性值以供協助篩選或搜尋不同的追蹤集。</span><span class="sxs-lookup"><span data-stu-id="df466-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="df466-292">例如：</span><span class="sxs-lookup"><span data-stu-id="df466-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="df466-293">在[搜尋](app-insights-diagnostic-search.md)中，您便可以輕鬆地篩選出與特定資料庫相關且具有特定嚴重性層級的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="df466-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="df466-294">分析中的追蹤</span><span class="sxs-lookup"><span data-stu-id="df466-294">Traces in Analytics</span></span>

<span data-ttu-id="df466-295">在 [Application Insights 分析](app-insights-analytics.md)中，TrackTrace 的呼叫會顯示在 `traces` 資料表中。</span><span class="sxs-lookup"><span data-stu-id="df466-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="df466-296">如果[取樣](app-insights-sampling.md)運作中，itemCount 屬性會顯示大於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="df466-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="df466-297">例如，itemCount==10 表示在 `trackTrace()` 的 10 個呼叫中，取樣處理序只會傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="df466-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="df466-298">若要取得正確的追蹤呼叫計數，您應該使用程式碼，例如 `traces | summarize sum(itemCount)`。</span><span class="sxs-lookup"><span data-stu-id="df466-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="df466-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="df466-299">TrackDependency</span></span>
<span data-ttu-id="df466-300">您可以使用 TrackDependency 呼叫來追蹤回應時間以及呼叫外部程式碼片段的成功率。</span><span class="sxs-lookup"><span data-stu-id="df466-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="df466-301">結果會出現在入口網站中的相依性圖表中。</span><span class="sxs-lookup"><span data-stu-id="df466-301">The results appear in the dependency charts in the portal.</span></span>

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

<span data-ttu-id="df466-302">請記住，伺服器 SDK 包含[相依性模組](app-insights-asp-net-dependencies.md)，可用來自動探索和追蹤特定相依性呼叫 (例如資料庫和 REST API)。</span><span class="sxs-lookup"><span data-stu-id="df466-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="df466-303">您必須在伺服器上安裝代理程式才能讓模組正常運作。</span><span class="sxs-lookup"><span data-stu-id="df466-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="df466-304">如果您想要追蹤自動化追蹤不會攔截的呼叫，或不想安裝代理程式，您可以使用這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="df466-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="df466-305">若要關閉標準的相依性追蹤模組，請編輯 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 並刪除 `DependencyCollector.DependencyTrackingTelemetryModule` 的參考。</span><span class="sxs-lookup"><span data-stu-id="df466-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="df466-306">分析中的相依性</span><span class="sxs-lookup"><span data-stu-id="df466-306">Dependencies in Analytics</span></span>

<span data-ttu-id="df466-307">在 [Application Insights 分析](app-insights-analytics.md)中，trackDependency 呼叫會顯示在 `dependencies` 資料表中。</span><span class="sxs-lookup"><span data-stu-id="df466-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="df466-308">如果[取樣](app-insights-sampling.md)運作中，itemCount 屬性會顯示大於 1 的值。</span><span class="sxs-lookup"><span data-stu-id="df466-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="df466-309">例如，itemCount==10 表示在 trackDependency() 的 10 個呼叫中，取樣處理序只會傳輸其中一個。</span><span class="sxs-lookup"><span data-stu-id="df466-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="df466-310">若要取得依目標元件分割的正確相依性計數，請使用類似如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="df466-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="df466-311">若要將相依性與其相關要求產生關聯，請使用聯結：</span><span class="sxs-lookup"><span data-stu-id="df466-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="df466-312">排清資料</span><span class="sxs-lookup"><span data-stu-id="df466-312">Flushing data</span></span>
<span data-ttu-id="df466-313">通常 SDK 會在選擇的時間傳送資料以將對使用者的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="df466-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="df466-314">不過，在某些情況下您可能想要排清緩衝區，例如，如果您在會關閉的應用程式中使用 SDK。</span><span class="sxs-lookup"><span data-stu-id="df466-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="df466-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="df466-316">請注意，此函式對[伺服器遙測通道](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)而言是非同步的。</span><span class="sxs-lookup"><span data-stu-id="df466-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="df466-317">驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="df466-317">Authenticated users</span></span>
<span data-ttu-id="df466-318">在 Web 應用程式中，預設是透過 Cookie 來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="df466-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="df466-319">如果使用者從不同的電腦或瀏覽器存取您的 app 或刪除 Cookie，就可能多次計算他們。</span><span class="sxs-lookup"><span data-stu-id="df466-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="df466-320">如果使用者登入您的 app，您可以藉由在瀏覽器程式碼中設定經過驗證的使用者識別碼，來取得更正確的計數：</span><span class="sxs-lookup"><span data-stu-id="df466-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="df466-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="df466-322">在 ASP.NET Web MVC 應用程式，例如：</span><span class="sxs-lookup"><span data-stu-id="df466-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="df466-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="df466-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="df466-324">這不需要用到使用者的實際登入名稱。</span><span class="sxs-lookup"><span data-stu-id="df466-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="df466-325">只需是使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="df466-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="df466-326">其中不能包含空格或任何 `,;=|` 字元。</span><span class="sxs-lookup"><span data-stu-id="df466-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="df466-327">使用者識別碼也會設定於工作階段 Cookie 中，並傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="df466-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="df466-328">如果安裝了伺服器 SDK，則會傳送經過驗證的使用者識別碼以作為用戶端和伺服器遙測的內容屬性一部分。</span><span class="sxs-lookup"><span data-stu-id="df466-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="df466-329">您可以接著對它進行篩選和搜尋。</span><span class="sxs-lookup"><span data-stu-id="df466-329">You can then filter and search on it.</span></span>

<span data-ttu-id="df466-330">如果您的 app 會將使用者群組為帳戶，您也可以傳遞該帳戶的識別碼 (具有相同的字元限制)。</span><span class="sxs-lookup"><span data-stu-id="df466-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="df466-331">在[計量瀏覽器](app-insights-metrics-explorer.md)中，您可建立可計算 [已驗證的使用者] 和 [使用者帳戶] 的圖表。</span><span class="sxs-lookup"><span data-stu-id="df466-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="df466-332">您也可以[搜尋](app-insights-diagnostic-search.md)具有特定使用者名稱和帳戶的用戶端資料點。</span><span class="sxs-lookup"><span data-stu-id="df466-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="df466-333"><a name="properties"></a>使用屬性篩選、搜尋和分割資料</span><span class="sxs-lookup"><span data-stu-id="df466-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="df466-334">您可以將屬性和測量結果附加至您的事件 (同時還有度量，頁面檢視、例外狀況和其他的遙測資料)。</span><span class="sxs-lookup"><span data-stu-id="df466-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="df466-335">*屬性* 是可在使用情況報告中用來篩選遙測的字串值。</span><span class="sxs-lookup"><span data-stu-id="df466-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="df466-336">例如，如果您的應用程式提供數個遊戲，則您可以將遊戲的名稱附加至每個事件，以了解哪些遊戲較受歡迎。</span><span class="sxs-lookup"><span data-stu-id="df466-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="df466-337">字串長度限制為 8192 個。</span><span class="sxs-lookup"><span data-stu-id="df466-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="df466-338">(如果您想要傳送大量的資料區塊，請使用訊息參數 [TrackTrace](#track-trace)。)</span><span class="sxs-lookup"><span data-stu-id="df466-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="df466-339">*度量* 是可以用圖表方式呈現的數值。</span><span class="sxs-lookup"><span data-stu-id="df466-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="df466-340">例如，您可能想要查看玩家達到的分數是否逐漸增加。</span><span class="sxs-lookup"><span data-stu-id="df466-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="df466-341">圖表可以依據隨事件傳送的屬性分割，讓您可以針對不同遊戲取得個別或堆疊圖表。</span><span class="sxs-lookup"><span data-stu-id="df466-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="df466-342">若要讓計量值正確顯示，這些值應該大於或等於 0。</span><span class="sxs-lookup"><span data-stu-id="df466-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="df466-343">有一些 [屬性、屬性值和度量的數目限制](#limits) 可供您使用。</span><span class="sxs-lookup"><span data-stu-id="df466-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="df466-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-344">*JavaScript*</span></span>

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


<span data-ttu-id="df466-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="df466-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="df466-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="df466-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="df466-348">切勿在屬性中記錄個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="df466-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="df466-349">*如果您使用度量*，請開啟 [計量瀏覽器]，然後從**自訂**群組中選取度量：</span><span class="sxs-lookup"><span data-stu-id="df466-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![開啟計量瀏覽器，選取圖表，並選取度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="df466-351">若未顯示您的計量或 [自訂] 標題不存在，請關閉選取的刀鋒視窗並於稍後重試。</span><span class="sxs-lookup"><span data-stu-id="df466-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="df466-352">有時候度量經由管線彙總時可能需要一個小時。</span><span class="sxs-lookup"><span data-stu-id="df466-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="df466-353">*如果您使用屬性和度量*，依據屬性分割度量：</span><span class="sxs-lookup"><span data-stu-id="df466-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![設定群組，然後在 [群組依據] 底下選取屬性](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="df466-355">*在「診斷搜尋」中*，您可以檢視事件個別發生次數的屬性和度量。</span><span class="sxs-lookup"><span data-stu-id="df466-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![選取執行個體，然後選取 [...]](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="df466-357">使用 [搜尋] 欄位來查看具有特定屬性值的事件出現次數。</span><span class="sxs-lookup"><span data-stu-id="df466-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![將詞彙輸入 [搜尋] 中](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="df466-359">[深入了解搜尋運算式](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="df466-360">設定屬性和度量的替代方式</span><span class="sxs-lookup"><span data-stu-id="df466-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="df466-361">如果更加方便，您可以收集個別物件中事件的參數：</span><span class="sxs-lookup"><span data-stu-id="df466-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="df466-362">不要重複使用相同的遙測項目執行個體 (此範例中的 `event`) 來呼叫 Track*() 多次。</span><span class="sxs-lookup"><span data-stu-id="df466-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="df466-363">這可能會讓遙測隨著不正確的組態傳送。</span><span class="sxs-lookup"><span data-stu-id="df466-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="df466-364">分析中的自訂測量和屬性</span><span class="sxs-lookup"><span data-stu-id="df466-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="df466-365">在[分析](app-insights-analytics.md)中，自訂計量和屬性會顯示在每個遙測記錄的 `customMeasurements` 和 `customDimensions` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="df466-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="df466-366">例如，如果您將一個名為 "game" 的屬性新增至您的要求遙測，此查詢將會計算不同 "game" 值出現的次數，並顯示自訂計量 "score" 的平均值：</span><span class="sxs-lookup"><span data-stu-id="df466-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="df466-367">請注意：</span><span class="sxs-lookup"><span data-stu-id="df466-367">Notice that:</span></span>

* <span data-ttu-id="df466-368">當您從 customDimensions 或 customMeasurements JSON 中擷取值時，其類型為動態，因此您必須將它轉換成 `tostring` 或 `todouble`。</span><span class="sxs-lookup"><span data-stu-id="df466-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="df466-369">考量到[取樣](app-insights-sampling.md)的可能性，您應該使用 `sum(itemCount)`，而不是 `count()`。</span><span class="sxs-lookup"><span data-stu-id="df466-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="df466-370"><a name="timed"></a> 計時事件</span><span class="sxs-lookup"><span data-stu-id="df466-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="df466-371">有時候您想要繪製執行某些動作耗費多少時間的圖表。</span><span class="sxs-lookup"><span data-stu-id="df466-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="df466-372">例如，您可能想要知道使用者在遊戲中思考選項時花費多少時間。</span><span class="sxs-lookup"><span data-stu-id="df466-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="df466-373">您可以對此使用測量參數。</span><span class="sxs-lookup"><span data-stu-id="df466-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="df466-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="df466-375"><a name="defaults"></a>自訂遙測資料的預設屬性</span><span class="sxs-lookup"><span data-stu-id="df466-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="df466-376">如果您想為您撰寫的一些自訂事件設定預設屬性值，您可以在 TelemetryClient 執行個體中設定它們。</span><span class="sxs-lookup"><span data-stu-id="df466-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="df466-377">它們會附加至從該用戶端傳送的每個遙測項目。</span><span class="sxs-lookup"><span data-stu-id="df466-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="df466-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="df466-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="df466-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="df466-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="df466-381">個別遙測呼叫可以覆寫其屬性字典中的預設值。</span><span class="sxs-lookup"><span data-stu-id="df466-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="df466-382">*針對 JavaScript Web 用戶端*， [請使用 JavaScript 遙測初始設定式](#js-initializer)。</span><span class="sxs-lookup"><span data-stu-id="df466-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="df466-383">*若要將屬性新增至所有遙測*，並包括來自標準集合模組的資料，請[實作 `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties)。</span><span class="sxs-lookup"><span data-stu-id="df466-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="df466-384">取樣、篩選及處理遙測資料</span><span class="sxs-lookup"><span data-stu-id="df466-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="df466-385">您可以撰寫程式碼，在從 SDK 傳送遙測資料前加以處理。</span><span class="sxs-lookup"><span data-stu-id="df466-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="df466-386">處理包括從標準遙測模組 (如 HTTP 要求收集和相依性收集) 的資料。</span><span class="sxs-lookup"><span data-stu-id="df466-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="df466-387">實作 `ITelemetryInitializer` 以[屬性](app-insights-api-filtering-sampling.md#add-properties)至遙測資料。</span><span class="sxs-lookup"><span data-stu-id="df466-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="df466-388">例如，您可以新增版本號碼或從其他屬性計算得出的值。</span><span class="sxs-lookup"><span data-stu-id="df466-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="df466-389">[篩選](app-insights-api-filtering-sampling.md#filtering)可以先修改或捨棄遙測，再藉由實作 `ITelemetryProcesor` 從 SDK 傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="df466-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="df466-390">您可控制要傳送或捨棄的項目，但是您必須考量這對您的度量的影響。</span><span class="sxs-lookup"><span data-stu-id="df466-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="df466-391">視您捨棄項目的方式而定，您可能會喪失在相關項目之間瀏覽的能力。</span><span class="sxs-lookup"><span data-stu-id="df466-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="df466-392">[取樣](app-insights-api-filtering-sampling.md)是減少從應用程式傳送至入口網站的資料量的套件方案。</span><span class="sxs-lookup"><span data-stu-id="df466-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="df466-393">它在這麼做時並不會影響顯示的度量。</span><span class="sxs-lookup"><span data-stu-id="df466-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="df466-394">而且它在這麼做時可藉由在相關項目 (如例外狀況、要求和頁面檢視) 之間瀏覽，而不會影響您診斷問題的能力。</span><span class="sxs-lookup"><span data-stu-id="df466-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="df466-395">[深入了解](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="df466-396">停用遙測</span><span class="sxs-lookup"><span data-stu-id="df466-396">Disabling telemetry</span></span>
<span data-ttu-id="df466-397">*動態停止和開始* 收集及傳輸遙測資料：</span><span class="sxs-lookup"><span data-stu-id="df466-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="df466-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="df466-399">若要*停用選取的標準收集器* (例如效能計數器、HTTP 要求或相依性)，請刪除或註解化 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 中的相關行。例如，如果您想要傳送自己的 TrackRequest 資料，可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="df466-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="df466-400"><a name="debug"></a>開發人員模式</span><span class="sxs-lookup"><span data-stu-id="df466-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="df466-401">偵錯期間，讓您的遙測透過管線加速很有用，如此您就可以立即看到結果。</span><span class="sxs-lookup"><span data-stu-id="df466-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="df466-402">您也會取得額外的訊息，協助您追蹤任何遙測的問題。</span><span class="sxs-lookup"><span data-stu-id="df466-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="df466-403">在生產環境中將它關閉，因為它可能會拖慢您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="df466-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="df466-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="df466-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="df466-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="df466-406"><a name="ikey"></a>設定已選取自訂遙測的檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="df466-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="df466-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="df466-408"><a name="dynamic-ikey"></a> 動態檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="df466-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="df466-409">若要避免混合來自開發、測試和實際執行環境的遙測，您可以[建立個別的 Application Insights 資源](app-insights-create-new-resource.md)，並且依據環境變更其金鑰。</span><span class="sxs-lookup"><span data-stu-id="df466-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="df466-410">而不是從組態檔取得檢測金鑰，您可以在程式碼中設定。</span><span class="sxs-lookup"><span data-stu-id="df466-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="df466-411">在初始化方法中設定金鑰，例如 ASP.NET 服務中的 global.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="df466-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="df466-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="df466-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="df466-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="df466-414">在網頁中，您可能想要從 Web 伺服器的狀態設定，而不是按其原義編碼至指令碼。</span><span class="sxs-lookup"><span data-stu-id="df466-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="df466-415">例如，在 ASP.NET 應用程式中產生的網頁：</span><span class="sxs-lookup"><span data-stu-id="df466-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="df466-416">*Razor 中的 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="df466-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="df466-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="df466-417">TelemetryContext</span></span>
<span data-ttu-id="df466-418">TelemetryClient 具有內容屬性，其中包含與所有遙測資料一起傳送的值。</span><span class="sxs-lookup"><span data-stu-id="df466-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="df466-419">它們通常由標準遙測模組設定，但是您也可以自行設定它們。</span><span class="sxs-lookup"><span data-stu-id="df466-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="df466-420">例如：</span><span class="sxs-lookup"><span data-stu-id="df466-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="df466-421">如果您自行設定這些值，請考慮從 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 移除相關的程式碼行，讓您的值和標準值不致混淆。</span><span class="sxs-lookup"><span data-stu-id="df466-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="df466-422">**元件**：應用程式及其版本。</span><span class="sxs-lookup"><span data-stu-id="df466-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="df466-423">**裝置**︰應用程式執行所在裝置的相關資料 </span><span class="sxs-lookup"><span data-stu-id="df466-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="df466-424">(在 Web 應用程式中，這是傳送遙測的伺服器或用戶端裝置)。</span><span class="sxs-lookup"><span data-stu-id="df466-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="df466-425">**InstrumentationKey**：Azure 中遙測顯示之位置的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="df466-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="df466-426">通常會揀選自 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="df466-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="df466-427">**位置**：裝置的地理位置。</span><span class="sxs-lookup"><span data-stu-id="df466-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="df466-428">**作業**：在 Web 應用程式中，目前的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="df466-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="df466-429">在其他應用程式類型中，您可以設定以將事件群組在一起。</span><span class="sxs-lookup"><span data-stu-id="df466-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="df466-430">**識別碼**：產生的值，與不同事件相互關聯，如此當您在診斷搜尋中檢查任何事件時，您可以發現相關項目。</span><span class="sxs-lookup"><span data-stu-id="df466-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="df466-431">**名稱**：識別碼，通常是 HTTP 要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="df466-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="df466-432">**SyntheticSource**：如果不為 null 或空白，這個字串表示要求的來源已被識別為傀儡程式或 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="df466-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="df466-433">根據預設，會從計量瀏覽器的計算中排除。</span><span class="sxs-lookup"><span data-stu-id="df466-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="df466-434">**屬性**：與所有遙測資料一起傳送的屬性。</span><span class="sxs-lookup"><span data-stu-id="df466-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="df466-435">可以在個別 Track* 呼叫中覆寫。</span><span class="sxs-lookup"><span data-stu-id="df466-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="df466-436">**工作階段**︰使用者的工作階段。</span><span class="sxs-lookup"><span data-stu-id="df466-436">**Session**: The user's session.</span></span> <span data-ttu-id="df466-437">識別碼會設為產生的值，當使用者一段時間沒有作用時會變更。</span><span class="sxs-lookup"><span data-stu-id="df466-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="df466-438">**使用者**：使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="df466-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="df466-439">限制</span><span class="sxs-lookup"><span data-stu-id="df466-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="df466-440">若要避免達到資料速率限制，請使用[取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="df466-441">若要決定資料的保留時間，請參閱[資料保留和隱私權](app-insights-data-retention-privacy.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="df466-442">參考文件</span><span class="sxs-lookup"><span data-stu-id="df466-442">Reference docs</span></span>
* [<span data-ttu-id="df466-443">ASP.NET 參考</span><span class="sxs-lookup"><span data-stu-id="df466-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="df466-444">Java 參考</span><span class="sxs-lookup"><span data-stu-id="df466-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="df466-445">JavaScript 參考</span><span class="sxs-lookup"><span data-stu-id="df466-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="df466-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="df466-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="df466-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="df466-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="df466-448">SDK 程式碼</span><span class="sxs-lookup"><span data-stu-id="df466-448">SDK code</span></span>
* [<span data-ttu-id="df466-449">ASP.NET 核心 SDK</span><span class="sxs-lookup"><span data-stu-id="df466-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="df466-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="df466-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="df466-451">Windows Server 套件</span><span class="sxs-lookup"><span data-stu-id="df466-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="df466-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="df466-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="df466-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="df466-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="df466-454">所有平台</span><span class="sxs-lookup"><span data-stu-id="df466-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="df466-455">問題</span><span class="sxs-lookup"><span data-stu-id="df466-455">Questions</span></span>
* <span data-ttu-id="df466-456">*Track_() 呼叫會擲回什麼例外狀況？*</span><span class="sxs-lookup"><span data-stu-id="df466-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="df466-457">無。</span><span class="sxs-lookup"><span data-stu-id="df466-457">None.</span></span> <span data-ttu-id="df466-458">您不需要將它們包裝在 try-catch 子句中。</span><span class="sxs-lookup"><span data-stu-id="df466-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="df466-459">如果 SDK 發生問題，它會在偵錯主控台輸出以及 (若訊息得以傳輸過去) 診斷搜尋中記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="df466-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="df466-460">*是否有 REST API 可供從入口網站中取得資料？*</span><span class="sxs-lookup"><span data-stu-id="df466-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="df466-461">是，[資料存取 API](https://dev.applicationinsights.io/)。</span><span class="sxs-lookup"><span data-stu-id="df466-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="df466-462">其他擷取資料的方法包括[從分析匯出至 Power BI](app-insights-export-power-bi.md) 和[連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="df466-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="df466-463"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="df466-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="df466-464">搜尋事件和記錄</span><span class="sxs-lookup"><span data-stu-id="df466-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="df466-465">疑難排解</span><span class="sxs-lookup"><span data-stu-id="df466-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


