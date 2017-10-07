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
# <a name="application-insights-api-for-custom-events-and-metrics"></a>自訂事件和度量的 Application Insights API

在您的應用程式 toofind 出使用者做什麼，插入幾行程式碼或 toohelp 診斷問題。 您可以從裝置和桌面應用程式、Web 用戶端以及 Web 伺服器傳送遙測。 使用 hello [Azure Application Insights](app-insights-overview.md)核心遙測 API toosend 自訂事件和度量和您自己的標準遙測資料的版本。 這個 API 是 hello hello 標準 Application Insights 資料收集器使用相同的 API。

## <a name="api-summary"></a>API summary
所有平台，除了少數小型變化 hello API 是一致的。

| 方法 | 用於 |
| --- | --- |
| [`TrackPageView`](#page-views) |頁面、畫面、刀鋒視窗或表單。 |
| [`TrackEvent`](#trackevent) |使用者動作和其他事件。 使用 tootrack 使用者行為或 toomonitor 效能。 |
| [`TrackMetric`](#trackmetric) |例如，佇列長度的效能測量資料不相關 toospecific 事件。 |
| [`TrackException`](#trackexception) |記錄例外狀況以供診斷。 追蹤位置中的關聯 tooother 事件發生和檢查堆疊追蹤。 |
| [`TrackRequest`](#trackrequest) |Hello 頻率和持續期間的效能分析伺服器要求的記錄。 |
| [`TrackTrace`](#tracktrace) |診斷記錄訊息。 您也可以擷取第三方記錄檔。 |
| [`TrackDependency`](#trackdependency) |Hello 持續時間與頻率取決於您的應用程式的呼叫 tooexternal 元件的記錄。 |

您可以[附加的屬性和度量](#properties)toomost 這些遙測呼叫。

## <a name="prep"></a>開始之前
如果您還沒有 Application Insights SDK 的參考：

* 加入 hello Application Insights SDK tooyour 專案：

  * [ASP.NET 專案](app-insights-asp-net.md)
  * [Java 專案](app-insights-java-get-started.md)
  * [每個網頁中的 JavaScript](app-insights-javascript.md) 
* 在裝置或 Web 伺服器程式碼中，加入：

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic：*`Imports Microsoft.ApplicationInsights`

    *Java：* `import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>建構 TelemetryClient 執行個體
建構 `TelemetryClient` 的執行個體 (除了網頁中的 JavaScript)：

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient 具備執行緒安全。

我們建議針對您每個應用程式的模組使用 TelemetryClient 執行個體。 比方說，您可能必須一個 TelemetryClient 執行個體，在您 web 服務 tooreport 連入 HTTP 要求，以及另一個中介軟體類別 tooreport 商務邏輯事件。 您可以設定屬性，例如`TelemetryClient.Context.User.Id`tootrack 使用者與工作階段，或`TelemetryClient.Context.Device.Id`tooidentify hello 機器。 這項資訊會附加的 tooall hello 執行個體傳送的事件。

## <a name="trackevent"></a>TrackEvent
在 Application Insights 中，「自訂事件」是您可以在[計量瀏覽器](app-insights-metrics-explorer.md)顯示為彙總計數，以及在[診斷搜尋](app-insights-diagnostic-search.md)中顯示為個別發生點的資料點。 （不相關的 tooMVC 或其他架構 」 的事件。"）

插入`TrackEvent`呼叫中程式碼 toocount 各種事件。 使用者選擇特定功能的頻率、達成特定目標的頻率，或他們犯特定類型錯誤的頻率。

例如，在遊戲的應用程式中時傳送事件使用者 wins hello 遊戲：

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>在 hello Microsoft Azure 入口網站中檢視您的事件
開啟您的事件計數 toosee[計量瀏覽器](app-insights-metrics-explorer.md)刀鋒視窗中，加入新的圖表，並選取**事件**。  

![查看自訂事件的計數](./media/app-insights-api-custom-events-metrics/01-custom.png)

不同的事件，toocompare hello 計數太設定 hello 圖表類型**方格**，並依事件名稱的群組：

![設定 hello 圖表類型和群組](./media/app-insights-api-custom-events-metrics/07-grid.png)

在 hello 方格中，按一下 事件名稱 toosee 個別項目間的該事件。 toosee 更多詳細資料-按一下 hello 清單中的任何項目。

![鑽研 hello 事件](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus 上特定事件中搜尋或計量瀏覽器組 hello 刀鋒視窗的篩選器 toohello 事件名稱，您感興趣：

![開啟 [篩選器]，展開 [事件名稱]，然後選取一或多個值](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>分析中的自訂事件

hello 遙測位於 hello`customEvents`資料表中[應用程式 Insights 分析](app-insights-analytics.md)。 每個資料列代表呼叫太`trackEvent(..)`應用程式中。 

如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。 範例 itemCount = = 10，10 呼叫 tootrackEvent() 的 hello 取樣程序時，才傳輸其中的表示。 tooget 正確的自訂事件計數，您應該使用因此使用程式碼，例如`customEvent | summarize sum(itemCount)`。


## <a name="trackmetric"></a>TrackMetric

Application Insights 可以不附加的 tooparticular 事件的度量的圖表。 例如，您可以定期監視佇列長度。 （包括計量），hello 個別的度量感興趣的較少比 hello 變化和趨勢，並因此統計圖表很有用。

在排序 toosend 度量 tooApplication Insights，您可以使用 hello`TrackMetric(..)`應用程式開發介面。 有兩種方式 toosend 度量： 

* 單一值： 每次您執行應用程式中的度量，您傳送 hello 對應值 tooApplication 深入資訊。 例如，假設您有描述項目容器中的 hello 數目的度量。 在特定時間週期內，您必須先三個項目放入 hello 容器，然後您移除兩個項目。 因此，您可以呼叫`TrackMetric`兩次： 第一次傳遞 hello 值`3`，然後 hello 值`-2`。 Application Insights 會代替您儲存這兩個值。 

* 彙總： 使用計量時，每個單一測量並不重要。 相反地，在特定期間內發生的狀況摘要才重要。 這類摘要稱為_彙總_。 在上述範例中的 hello，hello 彙總度量的加總該時間週期是`1`hello hello 度量值計數，且`2`。 使用 hello 彙總方式時，您只能叫用`TrackMetric`每一次的時間週期，並將傳送 hello 彙總值。 這是建議的方法，因為它可以大幅降低 hello 成本和效能負擔是藉由傳送較少的資料點 tooApplication Insights 時仍在收集所有相關資訊的 hello。

### <a name="examples"></a>範例：

#### <a name="single-values"></a>單一值

toosend 單一公制值：

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

C#、Java

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>彙總計量

然後才傳送從您的應用程式、 tooreduce 頻寬、 成本和 tooimprove 效能建議 tooaggregate 度量。
程式碼的彙總範例如下：

*C#*

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

### <a name="custom-metrics-in-metrics-explorer"></a>[計量瀏覽器] 中的自訂計量

toosee hello 結果中，開啟計量瀏覽器，並加入新的圖表。 編輯 hello 圖表 tooshow 您度量。

> [!NOTE]
> 您的自訂公制可能需要幾分鐘的時間 tooappear hello 可用的度量清單中。
>

![新增圖表或選取圖表，並在 [自訂] 底下選取您的度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Analytics 中的自訂計量

hello 遙測位於 hello`customMetrics`資料表中[應用程式 Insights 分析](app-insights-analytics.md)。 每個資料列代表呼叫太`trackMetric(..)`應用程式中。
* `valueSum`-這是 hello 度量 hello 總和。 tooget hello 平均值，除以`valueCount`。
* `valueCount`-hello 度量所彙總成這數目`trackMetric(..)`呼叫。

## <a name="page-views"></a>頁面檢視
在裝置或網頁應用程式中，每個畫面或頁面載入時預設會傳送頁面檢視遙測。 但是，您可以變更該 tootrack 網頁檢視，在其他或不同的時間。 比方說，在索引標籤或刀鋒視窗會顯示應用程式中，您可能想 tootrack 頁面每當 hello 使用者開啟的新刀鋒視窗。

![[概觀] 刀鋒視窗上的使用方式透鏡](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

使用者與工作階段資料會傳送內容頁面檢視，以及因此 hello 使用者與工作階段時沒有網頁檢視遙測開始運作的圖表。

### <a name="custom-page-views"></a>自訂頁面檢視
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


如果您有數個索引標籤，在不同的 HTML 網頁中，您可以指定 hello URL 太：

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>計時頁面檢視
根據預設，hello 時間回報為**網頁檢視載入時間**hello 瀏覽器傳送 hello 要求，直到呼叫 hello 瀏覽器網頁載入事件是當從算起。

相反地，您可以：

* 設定明確的持續時間在 hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview)呼叫： `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`。
* 使用 hello 頁面檢視計時呼叫`startTrackPage`和`stopTrackPage`。

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

hello 名稱，讓您做為 hello 第一個參數產生關聯的 hello 開始和停止的呼叫。 預設 toohello 目前頁面名稱。

hello 計量瀏覽器中顯示的持續時間衍生自 hello hello 間隔產生頁面載入啟動和停止的呼叫。 它是最多 tooyou 哪些實際時間的間隔。

### <a name="page-telemetry-in-analytics"></a>分析中的頁面遙測

在[分析](app-insights-analytics.md)中，有兩個資料表顯示瀏覽器作業的資料：

* hello`pageViews`資料表包含有關 hello URL 及頁面標題的資料
* hello`browserTimings`資料表包含有關用戶端效能資料，例如 hello 所花費時間 tooprocess hello 內送的資料

toofind 多久 hello 瀏覽器會採用 tooprocess 不同頁面：

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

不同的瀏覽器的 toodiscover hello popularities:

```
pageViews | summarize count() by client_Browser
```

tooassociate 頁面檢視 tooAJAX 呼叫，將具有相依性：

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
hello 伺服器 SDK 會使用 TrackRequest toolog HTTP 要求。

您也可以呼叫它自己如果您要在內容中的 toosimulate 要求中並沒有 hello web 服務模組執行。

不過，hello 建議的方式 toosend 要求遙測是 hello 要求做為<a href="#operation-context">作業內容</a>。

## <a name="operation-context"></a>作業內容
您可以一起關聯遙測項目，藉由附加 toothem 通用的作業識別碼。 hello 標準的要求追蹤模組會對例外狀況和其他事件，在處理 HTTP 要求時傳送。 在[搜尋](app-insights-diagnostic-search.md)和[分析](app-insights-analytics.md)，您可以使用 hello 識別碼 tooeasily 尋找與 hello 要求相關聯的任何事件。

hello 最簡單方式 tooset hello 識別碼是 tooset 作業內容使用這種模式：

*C#*

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

設定作業內容，以及`StartOperation`建立您指定的 hello 類型的遙測項目。 它會傳送 hello 遙測項目時處置 hello 作業，或明確地呼叫`StopOperation`。 如果您使用`RequestTelemetry`hello 遙測類型，其持續時間設定為啟動和停止的逾時的 toohello 間隔。

作業內容不可為巢狀。 如果已經有相同的作業內容，則其識別碼是所有的 hello 包含項目，包括建立 hello 項目相關聯`StartOperation`。

在搜尋中，hello 作業內容是使用的 toocreate hello**相關項目**清單：

![相關項目](./media/app-insights-api-custom-events-metrics/21.png)

如需有關自訂作業追蹤的詳細資訊，請參閱 [application-insights-custom-operations-tracking.md]。

### <a name="requests-in-analytics"></a>分析中的要求 

在[應用程式 Insights 分析](app-insights-analytics.md)，hello 的總要求顯示`requests`資料表。

如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。 範例 itemCount = = 10，10 呼叫 tootrackRequest() 的 hello 取樣程序時，才傳輸其中的表示。 tooget 正確的要求 」 和 「 平均持續時間的計數要求的名稱來區隔，請使用下列程式碼：

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
TooApplication Insights 傳送例外狀況：

* 太[計算](app-insights-metrics-explorer.md)，做為有問題的 hello 頻率的表示。
* 太[檢查個別項目](app-insights-diagnostic-search.md)。

hello 報告包含 hello 堆疊追蹤。

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

hello Sdk 自動攔截許多例外狀況，所以您不一定會明確需要 toocall TrackException。

* ASP.NET:[撰寫程式碼 toocatch 例外狀況](app-insights-asp-net-exceptions.md)。
* J2EE：[自動攔截例外狀況](app-insights-java-get-started.md#exceptions-and-request-failures)。
* JavaScript：自動攔截例外狀況。 如果您想 toodisable 自動集合時，加入您在您的網頁中插入的行 toohello 程式碼片段：

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>分析中的例外狀況

在[應用程式 Insights 分析](app-insights-analytics.md)，例外狀況出現在 hello`exceptions`資料表。

如果[取樣](app-insights-sampling.md)是在作業中，hello`itemCount`屬性顯示的值大於 1。 範例 itemCount = = 10，10 呼叫 tootrackException() 的 hello 取樣程序時，才傳輸其中的表示。 tooget 正確的例外狀況計數區隔的例外狀況類型，請使用下列程式碼：

```
exceptions | summarize sum(itemCount) by type
```

大部分的 hello 重要堆疊資訊已擷取到不同的變數，但您可以拉相距 hello`details`結構 tooget 更多。 由於這個結構是動態的您應該轉換 hello 您預期的結果 toohello 類型。 例如：

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

tooassociate 例外狀況，其相關的要求，其使用聯結：

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
使用 TrackTrace toohelp 診斷問題傳送"階層連結軌跡"tooApplication 深入資訊。 您可以傳送診斷資料區塊，並且在[診斷搜尋](app-insights-diagnostic-search.md)中檢查。

[記錄配接器](app-insights-asp-net-trace-logs.md)使用此 API toosend 協力廠商記錄 toohello 入口網站。

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


您可以搜尋訊息內容，但是 (不同於屬性值) 您無法在其中進行篩選。

hello 大小限制`message`遠高於 hello 屬性限制。
TrackTrace 的優點是您可以將較長的資料放在 hello 訊息。 例如，您可以在該處編碼 POST 資料。  

此外，您可以加入嚴重性層級 tooyour 訊息。 此外，其他的遙測，例如，您可以加入屬性值 toohelp 您篩選或搜尋不同組的追蹤。 例如：

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

在[搜尋](app-insights-diagnostic-search.md)，您可以輕鬆地篩選出所有特定嚴重性等級的相關 tooa 特定資料庫的 hello 訊息。


### <a name="traces-in-analytics"></a>分析中的追蹤

在[應用程式 Insights 分析](app-insights-analytics.md)，呼叫 tooTrackTrace 顯示在 hello`traces`資料表。

如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。 範例 itemCount = = 10，10 個呼叫過，即表示`trackTrace()`，hello 取樣程序時，才傳輸其中一個。 tooget 追蹤呼叫正確計數，您應該使用因此程式碼例如`traces | summarize sum(itemCount)`。

## <a name="trackdependency"></a>TrackDependency
使用 hello TrackDependency 呼叫 tootrack hello 回應時間與成功率呼叫 tooan 外部程式碼片段。 hello 結果會出現在 hello hello 入口網站中的相依性圖表中。

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

請記住 Sdk 包含該 hello 伺服器[相依模組](app-insights-asp-net-dependencies.md)，會探索並自動追蹤特定相依性呼叫，例如 toodatabases 和 REST Api。 您有 tooinstall 伺服器 toomake hello 模組上的代理程式工作。 如果您想 hello 自動化的追蹤的 tootrack 呼叫未攔截，或如果您不想 tooinstall hello 代理程式，您可以使用這個呼叫。

一般相依性追蹤模組 hello，關閉 tooturn 編輯[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)和太刪除 hello 參考`DependencyCollector.DependencyTrackingTelemetryModule`。

### <a name="dependencies-in-analytics"></a>分析中的相依性

在[應用程式 Insights 分析](app-insights-analytics.md)，trackDependency 呼叫顯示在 hello`dependencies`資料表。

如果[取樣](app-insights-sampling.md)是在作業中，hello itemCount 屬性會顯示值大於 1。 範例 itemCount = = 10，10 呼叫 tootrackDependency() 的 hello 取樣程序時，才傳輸其中的表示。 目標元件的 tooget 正確的相依性計數分割，使用程式碼，例如：

```
dependencies | summarize sum(itemCount) by target
```

tooassociate 相依性，其相關的要求與使用聯結：

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>排清資料
一般來說，hello SDK 傳送有時候選擇 toominimize hello hello 使用者影響的資料。 不過，在某些情況下，您可能想 tooflush hello 緩衝區-比方說，如果您使用，如此會關閉應用程式中的 hello SDK。

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

請注意 hello 函式是非同步的 hello[伺服器遙測通道](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/)。

## <a name="authenticated-users"></a>驗證的使用者
在 Web 應用程式中，預設是透過 Cookie 來識別使用者。 如果使用者從不同的電腦或瀏覽器存取您的 app 或刪除 Cookie，就可能多次計算他們。

如果使用者登入 tooyour 應用程式，您可以藉由設定 hello 驗證使用者識別碼 hello 瀏覽器程式碼中取得更精確的計數：

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

在 ASP.NET Web MVC 應用程式，例如：

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

它不是必要的 toouse hello 使用者的實際登入名稱。 它只需要 toobe 唯一 toothat 使用者的識別碼。 它不能包含空格或任何 hello 字元`,;=|`。

也在工作階段 cookie 中設定並傳送 toohello 伺服器 hello 使用者識別碼。 如果已安裝 hello 伺服器 SDK，hello 驗證的使用者識別碼會傳送 hello 內容屬性的用戶端和伺服器的遙測資料的一部分。 您可以接著對它進行篩選和搜尋。

如果您的應用程式會將使用者分組帳戶，您也可以傳遞 hello 帳戶的識別項 （以 hello 相同字元限制）。

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

在[計量瀏覽器](app-insights-metrics-explorer.md)中，您可建立可計算 [已驗證的使用者] 和 [使用者帳戶] 的圖表。

您也可以[搜尋](app-insights-diagnostic-search.md)具有特定使用者名稱和帳戶的用戶端資料點。

## <a name="properties"></a>使用屬性篩選、搜尋和分割資料
您可以附加屬性和度量 tooyour 事件 （和也 toometrics、 頁面檢視、 例外狀況，以及其他遙測資料）。

*屬性*是字串值，您可以使用 toofilter 您遙測 hello 的使用情況報告。 例如，如果您的應用程式提供數個遊戲，您可以附加 hello hello 遊戲 tooeach 事件名稱，讓您可以查看哪些遊戲是普遍。

沒有 8192 hello 字串長度的限制。 (如果您想 toosend 大量的資料區塊時，使用 hello 訊息參數[TrackTrace](#track-trace)。)

*度量* 是可以用圖表方式呈現的數值。 比方說，您可能想 toosee，如果沒有達到您玩家正面對決的 hello 分數中逐漸增加。 hello 圖形分隔屬性，讓您可取得與 hello 事件傳送嗨可以區隔，或堆疊之不同遊戲的圖形。

正確顯示的度量值 toobe，它們應該大於或等於 too0。

有一些[屬性、 屬性值和度量的 hello 數目限制](#limits)，您可以使用。

*JavaScript*

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


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> 請注意不 toolog 中的個人識別資訊內容。
>
>

*如果您使用度量*，開啟計量瀏覽器，並從 hello 選取 hello 度量**自訂**群組：

![開啟度量總管 中，選取 hello 圖表，並選取 hello 度量](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> 如果未出現您度量，或如果 hello**自訂**標題不存在，關閉 hello 選取範圍 刀鋒視窗並再試一次。 度量有時可能需要一小時 toobe hello 管線的彙總資料。

*如果您使用屬性和度量*，根據 hello 屬性區隔 hello 度量：

![設定群組，然後選取 依群組下的 hello 屬性](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*在搜尋中診斷*，您可以檢視 hello 屬性和事件的個別發生次數的度量。

![選取執行個體，然後選取 [...]](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

使用 hello**搜尋**欄位 toosee 事件項目具有特定屬性值。

![將詞彙輸入 [搜尋] 中](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[深入了解搜尋運算式](app-insights-diagnostic-search.md)。

### <a name="alternative-way-tooset-properties-and-metrics"></a>另一種方式 tooset 屬性和度量
如果是更方便，您可以收集 hello 參數中的個別物件的事件：

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> 不要重複使用 hello 相同遙測項目執行個體 (`event`在此範例中) toocall Track*() 多次。 這可能會導致不正確的設定以傳送遙測 toobe。
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>分析中的自訂測量和屬性

在[分析](app-insights-analytics.md)，自訂的度量和屬性會顯示在 hello`customMeasurements`和`customDimensions`每個遙測記錄屬性。

比方說，如果您已經加入名為 「 遊戲 」 tooyour 要求遙測的屬性，此查詢 hello 次數的 「 遊戲 」 時，有不同的值會計算並顯示 hello 平均 hello 的自訂度量 「 分數 」:

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

請注意：

* 當您從 hello customDimensions 或 customMeasurements JSON 中擷取值時，它具有動態類型，以及因此您必須將它轉換`tostring`或`todouble`。
* hello 可能性 tootake 帳戶[取樣](app-insights-sampling.md)，您應該使用`sum(itemCount)`，而非`count()`。



## <a name="timed"></a> 計時事件
有時候您會想 toochart 多久採取 tooperform 動作。 例如，您可能想 tooknow 使用者採取 tooconsider 選擇在遊戲的時間長度。 您可以在這個使用 hello 度量參數。

*C#*

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



## <a name="defaults"></a>自訂遙測資料的預設屬性
如果您想 tooset 預設屬性值的某些 hello 您撰寫的自訂事件時，您可以設定它們 TelemetryClient 執行個體中。 它們是從該用戶端傳送的附加的 tooevery 遙測項目。

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



個別的遙測呼叫可以覆寫其屬性字典中的 hello 預設值。

*針對 JavaScript Web 用戶端*， [請使用 JavaScript 遙測初始設定式](#js-initializer)。

*tooadd 屬性 tooall 遙測*，包括標準集合模組中的 hello 資料[實作`ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties)。

## <a name="sampling-filtering-and-processing-telemetry"></a>取樣、篩選及處理遙測資料
傳送嗨 SDK 從之前您可以撰寫指定碼 tooprocess 您遙測。 hello 處理包括傳送 hello 標準遙測模組，例如 HTTP 要求的集合和相依性集合中的資料。

[將屬性加入](app-insights-api-filtering-sampling.md#add-properties)藉由實作 tootelemetry `ITelemetryInitializer`。 例如，您可以新增版本號碼或從其他屬性計算得出的值。

[篩選](app-insights-api-filtering-sampling.md#filtering)可以修改或捨棄遙測之前它會傳送 hello SDK 藉由實作, `ITelemetryProcesor`。 您控制所傳送或捨棄，但有 tooaccount hello 效果，在您的指標。 根據如何捨棄的項目，您可能會遺失 hello 能力 toonavigate 相關的項目之間。

[取樣](app-insights-api-filtering-sampling.md)是從您的應用程式 toohello 入口網站傳送資料的已封裝的方案 tooreduce hello 磁碟區。 它會以不會影響顯示 hello 度量。 它會以不影響能力 toodiagnose 問題相關的項目，例如例外狀況、 要求和頁面檢視之間巡覽。

[深入了解](app-insights-api-filtering-sampling.md)。

## <a name="disabling-telemetry"></a>停用遙測
太*動態停止和啟動*hello 遙測的收集和傳輸：

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

太*停用選取的標準收集器*-例如，效能計數器、 HTTP 要求或相依性-刪除或標記為註解中的 hello 相關行[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。例如，如果您想 toosend TrackRequest 資料，您可以這麼做。

## <a name="debug"></a>開發人員模式
偵錯期間，就很有用的 toohave 您遙測加速 hello 管線，讓您可以立即查看結果。 您也取得額外的訊息可協助您追蹤 hello 遙測的任何問題。 在生產環境中將它關閉，因為它可能會拖慢您的應用程式。

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>設定所選自訂遙測的 hello 檢測金鑰
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> 動態檢測金鑰
tooavoid 混遙測從開發、 測試和生產環境中，您可以[建立個別的 Application Insights 資源](app-insights-create-new-resource.md)並變更其索引鍵，視 hello 環境而定。

而不是從 hello 設定檔中取得 hello 檢測金鑰，您可以在程式碼中設定。 在初始設定方法，例如 global.aspx.cs ASP.NET 服務中設定 hello 機碼：

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



在網頁中，您可能想 tooset 從 hello web 伺服器的狀態，而不是常值到 hello 指令碼編碼。 例如，在 ASP.NET 應用程式中產生的網頁：

*Razor 中的 JavaScript*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient 具有內容屬性，其中包含與所有遙測資料一起傳送的值。 它們通常設定 hello 標準遙測模組，但您也可以設定他們自己。 例如：

    telemetry.Context.Operation.Name = "MyOperationName";

如果您設定了任何這些值的自行，請考慮移除 hello 相關行[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，如此混淆不到您的 hello 標準值和值。

* **元件**: hello 應用程式和其版本。
* **裝置**: hello hello 應用程式執行所在的裝置相關資料。 （在 web 應用程式，這是 hello 伺服器或用戶端裝置從傳送嗨遙測。）
* **InstrumentationKey**: hello Azure hello 遙測出現的位置中的 Application Insights 資源。 通常會揀選自 ApplicationInsights.config。
* **位置**: hello hello 裝置的地理位置。
* **作業**： 在 web 應用程式，hello 目前 HTTP 要求。 在其他應用程式類型，您可以一起設定，這個 toogroup 事件。
  * **識別碼**：產生的值，與不同事件相互關聯，如此當您在診斷搜尋中檢查任何事件時，您可以發現相關項目。
  * **名稱**： 識別項通常 hello 的 hello HTTP 要求的 URL。
  * **SyntheticSource**： 如果不為 null 或空白，表示該 hello 要求的來源 hello 的字串已經被識別為機器人或 web 測試。 根據預設，會從計量瀏覽器的計算中排除。
* **屬性**：與所有遙測資料一起傳送的屬性。 可以在個別 Track* 呼叫中覆寫。
* **工作階段**: hello 使用者工作階段。 設定 hello 識別碼 hello 使用者已使用一段時間後會變更的 tooa 產生值。
* **使用者**：使用者資訊。

## <a name="limits"></a>限制
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

達到 hello 資料速率限制，使用 tooavoid[取樣](app-insights-sampling.md)。

toodetermine 如何保持 long 資料，請參閱[資料保留和隱私權](app-insights-data-retention-privacy.md)。

## <a name="reference-docs"></a>參考文件
* [ASP.NET 參考](https://msdn.microsoft.com/library/dn817570.aspx)
* [Java 參考](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [JavaScript 參考](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>SDK 程式碼
* [ASP.NET 核心 SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Windows Server 套件](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)
* [所有平台](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>問題
* *Track_() 呼叫會擲回什麼例外狀況？*

    無。 您不需要 toowrap try catch 子句中。 如果 hello SDK 發生問題時，它就會在 hello 偵錯主控台輸出中記錄訊息和--如果 hello 訊息取得-中診斷的搜尋。
* *是否有從 hello 入口網站 REST API tooget 資料？*

    是，hello[資料存取 API](https://dev.applicationinsights.io/)。 其他方式 tooextract 資料包含[從分析 tooPower BI 匯出](app-insights-export-power-bi.md)和[連續匯出](app-insights-export-telemetry.md)。

## <a name="next"></a>接續步驟
* [搜尋事件和記錄](app-insights-diagnostic-search.md)

* [疑難排解](app-insights-troubleshoot-faq.md)


