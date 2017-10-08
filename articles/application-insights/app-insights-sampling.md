---
title: "在 Azure Application Insights aaaTelemetry 取樣 |Microsoft 文件"
description: "如何 tookeep hello 控制下的遙測資料的磁碟的區。"
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Application Insights 中的取樣


取樣是 [Azure Application Insights](app-insights-overview.md) 中的一個功能。 它是 hello 的建議方式 tooreduce 遙測流量和儲存體，同時保留應用程式資料的正確統計分析。 hello 篩選選取項目相關，如此您可以瀏覽項目，當您在進行診斷調查之間。
當度量的計數呈現 tooyou hello 入口網站中時，它們會重新正規化 tootake hello 取樣，toominimize 任何生效的 hello 統計帳戶。

取樣可減少流量與資料成本，而且可以協助您避免節流。

## <a name="in-brief"></a>簡單地說︰
* 取樣會保留 1  *n* 記錄，並捨棄 hello rest。 比方說，它可能會保留 5 個事件的其中 1 個，取樣率為 20%。 
* 如果您的應用程式傳送大量遙測，ASP.NET Web 伺服器應用程式便會自動進行取樣。
* 您也可以設定取樣以手動方式，是在 hello 入口網站上 hello 定價頁面。或在 hello hello.config 檔案中的 ASP.NET SDK，tooalso 減少 hello 網路流量。
* 如果您自訂的事件記錄，而且您想要確定，一組事件是保留或一起捨棄 toomake，確定它們有 hello OperationId 值相同。
* hello 取樣除數 *n*  hello 屬性中的每一筆記錄來報告`itemCount`，hello 易記名稱的 「 要求計數 」 或 「 事件計數 」 下出現的搜尋中。 當取樣不在作業中，則 `itemCount==1`。
* 如果您要撰寫分析查詢，請 [考慮到取樣](app-insights-analytics-tour.md#counting-sampled-data)。 特別是，您應該使用 `summarize sum(itemCount)`，而非只計算記錄。

## <a name="types-of-sampling"></a>取樣類型
有三個替代的取樣方法：

* **自動調整取樣**自動調整的遙測資料從您的 ASP.NET 應用程式中的 hello SDK 傳送 hello 磁碟區。 預設從 SDK v 2.0.0-beta3 傳送。 目前僅供 ASP.NET 伺服器端遙測使用。 
* **固定速率取樣**減少 hello 的遙測資料傳送，從這兩個 ASP.NET 伺服器從使用者的瀏覽器的磁碟區。 您設定 hello 速率。 hello 用戶端和伺服器將會同步處理其取樣因此，在搜尋中，您可以瀏覽相關的頁面檢視及要求。
* **擷取取樣**hello Azure 入口網站中的運作方式。 它會捨棄一些 hello 遙測來自您的應用程式，您所設定的速率。 這不會減少遙測流量，但可協助您讓流量不要超過每月配額。 您可以將其設定而不必重新部署您的應用程式，而一致的方式適用於所有伺服器和用戶端 hello 能夠取樣最大好處。 

如果自適性或固定速率取樣正在作業中，則會停用擷取取樣。

## <a name="ingestion-sampling"></a>擷取取樣
這種形式的取樣點 hello 從您網頁伺服器、 瀏覽器和裝置 hello 遙測當達到 hello Application Insights 服務端點的運作方式。 雖然它不會減少從您的應用程式傳送 hello 遙測流量，減少 hello 量處理，並保留 （和支付） 由 Application Insights。

如果您的應用程式通常會超過每月配額，而且不需要 hello 選項使用的取樣 hello SDK 為基礎類型，請使用這種類型的取樣。 

設定 hello 取樣率，以 hello 配額和定價刀鋒視窗中：

![從 hello 應用程式概觀刀鋒視窗中，按一下設定、 配額、 範例，然後選取取樣率，並按一下 [更新]。](./media/app-insights-sampling/04.png)

如同其他類型的取樣，hello 演算法會保留相關的遙測項目。 例如，當您檢查在搜尋中的 hello 遙測，您可以 toofind hello 要求相關的 tooa 特定例外狀況。 度量計量 (例如要求率及例外狀況率) 會正確地保留。

遭到取樣捨棄的資料點將無法在任何 Application Insights 功能中使用，例如 [連續匯出](app-insights-export-telemetry.md)。

進行 SDK 自適性或固定速率取樣時，不執行擷取取樣。 如果在 hello SDK hello 取樣率小於 100%，則 hello 擷取您所設定的取樣率會忽略。

> [!WARNING]
> hello hello 磚上顯示的值表示您將擷取取樣的 hello 值。 如果 SDK 取樣是作業中，它不代表 hello 實際取樣率。
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>在您 Web 伺服器上的調適性取樣
自動調整取樣供 hello Application Insights SDK ASP.NET v 2.0.0-beta3 和更新版本，而且預設會啟用。 

自動調整取樣會影響遙測資料從您網頁伺服器應用程式 toohello Application Insights 服務傳送嗨磁碟的區。 hello 磁碟區會自動調整 tookeep 內指定的最大速率的流量。

它無法在低遙測量的情況下運作，因此偵錯中的應用程式或使用率低的網站不會受到影響。

tooachieve hello 目標磁碟區，某些產生的 hello 遙測會被捨棄。 但其他類型的取樣，類似 hello 演算法會保留相關的遙測項目。 例如，當您檢查在搜尋中的 hello 遙測，您可以 toofind hello 要求相關的 tooa 特定例外狀況。 

度量會計算例如要求率和例外狀況率，調整的 toocompensate hello 取樣率，使它們在度量總管 中顯示大約正確的值。

**更新您的專案 NuGet**最新封裝 toohello*發行前版本*新版 Application Insights： 以滑鼠右鍵按一下方案總管] 中的 hello 專案中，選擇 [管理 NuGet 封裝，請檢查**Include發行前版本**並 Microsoft.ApplicationInsights.Web 搜尋。 

在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)，您可以調整幾個參數，在 hello`AdaptiveSamplingTelemetryProcessor`節點。 hello 圖表所示為 hello 預設值：

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    hello hello 調整演算法的目標速率目標在於**每個伺服器主機上**。 若您的 web 應用程式執行許多主機上，所以當 tooremain 內您目標的速率在 hello Application Insights 入口網站的流量減少這個值。
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    hello 間隔在哪一個 hello 的遙測資料的目前速率會重新評估。 評估是以移動平均來執行。 如果您的遙測對於 toosudden 暴增您可能想指定 tooshorten 此時間間隔。
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    取樣百分比值變更時，多久之後我們允許一次取樣百分比 toolower toocapture 較少的資料。
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    取樣百分比值變更時，多久之後我們允許一次取樣百分比 tooincrease toocapture 更多資料。
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    隨著取樣百分比改變，什麼是 hello 最小值我們要允許 tooset。
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    隨著取樣百分比改變，什麼是 hello 最大值我們要允許 tooset。
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    在 hello 計算中的 hello 移動平均，hello 權數指派 toohello 最新的值。 使用小於 1 的值等於 tooor。 較小的值變更 hello 演算法較不反應式 toosudden。
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    hello hello 應用程式剛開始時指派的值。 不要在偵錯時減少此值。 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    以分號分隔不想讓 toobe 取樣的型別的清單。 可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。 Hello 的所有執行個體指定傳輸類型。未指定的 hello 類型會取樣。

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    您要取樣的 toobe 類型以分號分隔的清單。 可辨識的類型為：相依性、事件、例外狀況、頁面檢視、要求、追蹤。 hello 指定類型所取樣。所有執行個體的 hello 其他類型會永遠傳輸。


**關閉 tooswitch**調整取樣，移除 hello AdaptiveSamplingTelemetryProcessor 節點從 applicationinsights 設定。

### <a name="alternative-configure-adaptive-sampling-in-code"></a>替代方法：在程式碼中設定調適性取樣
而不是調整取樣 hello.config 檔案中的，您可以使用程式碼。 這可讓您 toospecify hello 取樣率會重新評估時叫用的回呼函式。 您可以使用此，例如，使用 toofind 出哪些取樣率。

移除 hello `AdaptiveSamplingTelemetryProcessor` hello.config 檔案中的節點。

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>具有 JavaScript 的網頁的取樣
您可以從任何伺服器設定固定取樣率的網頁。 

當您[hello 網頁設定為 Application Insights](app-insights-javascript.md)，修改您從 hello Application Insights 入口網站取得的 hello 片段。 （在 ASP.NET 應用程式，hello 片段通常會出現在 _Layout.cshtml。）插入行像`samplingPercentage: 10,`hello 檢測金鑰之前：

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Hello 取樣百分比，選擇的百分比是關閉的 too100 N，其中 N 是整數。  目前取樣並不支援其他值。

如果您也可以啟用在 hello 伺服器固定速率取樣，hello 用戶端和伺服器將會同步，讓該，在搜尋時，您可以瀏覽相關的頁面檢視及要求。

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>適用於 ASP.NET 網站的固定取樣率
固定取樣可以減少從您網頁伺服器和網頁瀏覽器傳送的 hello 流量。 但它會依照您設定的速率來降低遙測，這與調適性取樣不同。 它也會同步 hello 用戶端和伺服器取樣讓相關的項目，就會保留-例如，因此如果您看一下檢視中搜尋的頁面，您可以找到其相關的要求。

hello 的採樣演算法會保留相關項目。 對於每個 HTTP 要求事件，它及其相關事件會遭到捨棄或傳輸。 

計量瀏覽器中速度，例如要求和例外狀況計數會乘以 hello 取樣率的因數 toocompensate，使其大約正確。

1. **更新您的專案 NuGet 套件**toohello 最新*發行前版本*新版 Application Insights。 以滑鼠右鍵按一下方案總管] 中的 hello 專案中，選擇 [管理 NuGet 封裝，請檢查**包含發行前版本**並 Microsoft.ApplicationInsights.Web 搜尋。 
2. **停用自動調整取樣**： 在[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)、 移除或註解 hello`AdaptiveSamplingTelemetryProcessor`節點。
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **啟用 hello 固定速率取樣模組。** 加入這個程式碼片段太[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Hello 取樣百分比，選擇的百分比是關閉的 too100 N，其中 N 是整數。  目前取樣並不支援其他值。
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>替代方法：在伺服器程式碼中啟用固定取樣率
而不是設定 hello 取樣參數 hello.config 檔案中，您可以使用程式碼。 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([深入了解遙測處理器](app-insights-api-filtering-sampling.md#filtering))。

## <a name="when-toouse-sampling"></a>當 toouse 取樣嗎？
如果您使用 ASP.NET 的 SDK 版本 2.0.0-beta3 hello，會自動啟用自動調整取樣或更新版本。 無論您使用哪個版本的 SDK，都可以 (在我們的伺服器上) 使用擷取取樣 。

對大多數小型和中型大小應用程式，您不需要取樣。 hello 最有用的診斷資訊，並最精確的統計資料後所取得您所有的使用者活動上收集資料。 

hello 的取樣的主要優點包括：

* 當您的應用程式在短時間間隔傳送非常高比率的遙測時，Application Insights 服務會將資料點卸除 (「節流」)。 
* hello 內 tookeep[配額](app-insights-pricing.md)的定價層的資料點。 
* tooreduce hello 收集的遙測資料從網路流量。 

### <a name="which-type-of-sampling-should-i-use"></a>我應該使用哪種類型的取樣？
**如果是下列情形，請使用擷取取樣：**

* 您的遙測經常會超出每月配額。
* 您用 hello SDK 不支援取樣-例如，hello Java SDK 或 ASP.NET 版本的版本早於 2。
* 您收到大量來自使用者網頁瀏覽器的遙測。

**如果是下列情形，則使用固定取樣率：**

* 您使用 ASP.NET web 服務版本 2.0.0 的 hello Application Insights SDK 或更新版本，以及
* 您想要用戶端與伺服器之間的同步處理取樣如此，當您想調查中的事件[搜尋](app-insights-diagnostic-search.md)，您可以巡覽 hello 用戶端上的相關的事件與伺服器，例如頁面檢視和 http 要求。
* 您自信 hello 適當取樣百分比的應用程式。 應該夠高 tooget 精確的衡量標準，但以下 hello 速率超過定價配額並 hello 節流限制。 

**使用調適性取樣：**

否則，建議使用調適性取樣。 啟用此選項預設會在 hello ASP.NET 伺服器 SDK，2.0.0-beta3 版本或更新版本。 它只會影響速率達到某個最低值的流量，因此不會影響使用率較低的網站。

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>如何得知取樣是否正在運作中？
取樣率，不論它有已套用的位置，使用 toodiscover hello 實際[分析查詢](app-insights-analytics.md)如下：

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

在每個保留的記錄，`itemCount`指出 hello 原始記錄數目，它代表相等 too1 + hello 先前已捨棄的記錄數目。 

## <a name="how-does-sampling-work"></a>取樣運作方式？
固定速率和彈性的取樣是 hello 的從 2.0.0 及更新版本的 ASP.NET 版本中 SDK 的功能。 擷取取樣是 hello Application Insights 服務的功能，而且可以在作業中如果 hello SDK 不會執行取樣。 

hello 的採樣演算法來決定哪些遙測項目 toodrop，以及哪些是 tookeep （不論它是否在 hello SDK 或在 hello Application Insights 服務）。 hello 取樣決策根據目標 toopreserve 保持不變，維持可採取動作，而且即使有一組縮減資料可靠的 Application Insights 中的診斷經驗的所有相互關聯的資料點的數個規則。 比方說，如果是失敗的要求，您的應用程式會傳送其他遙測項目 (例如從此要求記錄的例外狀況和追蹤)，取樣將不會分割此要求和其他遙測。 它會一起保留或卸除。 如此一來，當您查看 Application Insights 中的 hello 要求詳細資料，您可以永遠看到 hello 要求以及其相關聯的遙測項目。 

定義 「 使用者 」 的應用程式 (也就是最常見的 web 應用程式)，hello 取樣決策根據 hello 使用者識別碼，這表示，任何特定使用者的所有遙測已保留或卸除 hello 雜湊。 Hello 類型未定義的使用者 （例如 web 服務） 的應用程式的 hello 取樣決策根據 hello hello 要求的作業識別碼。 最後，兩者都不具有設定 （如範例遙測項目從無 http 內容的非同步執行緒報告） 的使用者，也不作業識別碼 hello 遙測項目取樣只會擷取遙測項目，每個類型的百分比表示。 

當呈現遙測後 tooyou，hello Application Insights 服務調整 hello 度量的 hello 相同的集合，如遺漏資料點的 hello toocompensate hello 次中使用的取樣百分比。 因此，當查看 Application Insights 中的 hello 遙測，hello 使用者會看到以統計方式正確會非常接近 toohello 實際數字的近似值。

hello 近似值 hello 精確度主要是取決於設定的 hello 取樣百分比。 此外，hello 精確度會增加處理大量的大量使用者通常類似要求的應用程式。 在 hello 換句話說，應用程式，不適用於大量負載的取樣不需要為這些應用程式通常可以傳送其所有的遙測資料仍 hello 配額，而不會造成資料遺失的節流。 

請注意，Application Insights 不範例度量和工作階段遙測類型，因為這些類型，減少 hello 有效位數可以是非常讓人困擾。 

### <a name="adaptive-sampling"></a>調適性取樣
自動調整取樣 hello SDK，從目前的傳輸速率該監視器 hello 新增元件，並調整 hello 取樣百分比 tootry toostay 內 hello 目標的最大速率。 hello 調整定期重新計算，並且根據移動平均值的 hello 外寄傳輸速率。

## <a name="sampling-and-hello-javascript-sdk"></a>取樣和 hello JavaScript SDK
hello 用戶端 (JavaScript) SDK 參與固定速率取樣搭配 hello 伺服器端 SDK。 hello 檢測頁面只會從相同的 hello 伺服器端所做的決策的使用者太 」 範例中。"hello 傳送用戶端遙測 此邏輯會是跨用戶端-伺服器-端及設計的 toomaintain 完整性的使用者工作階段。 如此一來，您可以從 Application Insights 中的任何特定遙測項目找到這個使用者或工作階段的所有其他遙測項目。 

*我的用戶端和伺服器端遙測未顯示您上方描述的協調範例。*

* 請確認您在伺服器及用戶端上都已啟用固定取樣率。
* 請確定該 hello SDK 版本 2.0 或更新版本。
* 您所設定的核取 hello 相同取樣 hello 用戶端和伺服器中的百分比。

## <a name="frequently-asked-questions"></a>常見問題集
*為什麼不取樣簡單的「收集每個遙測類型百分之 X」？*

* 雖然此取樣方法會提供極高的有效位數中度量的近似值，它會破壞每個使用者、 工作階段和要求，這相當重要的診斷能力 toocorrelate 診斷資料。 因此，對於「收集應用程式使用者百分之 X 的所有遙測項目」或「收集應用程式要求百分之 X 的所有遙測」邏輯，取樣的效果更佳。 Hello 遙測項目未與 hello 要求 （例如背景非同步處理） 相關聯，hello 改回是太"收集的每個遙測類型的所有項目 %x。 」 

*經過一段時間，可以 hello 取樣百分比變更嗎？*

* 是，自動調整取樣逐漸變更 hello 目前觀察到的 hello 遙測資料的磁碟區所根據的 hello 取樣百分比。

*如果我使用固定速率取樣時，如何知道哪些取樣百分比運作 hello 最適合我的應用程式？*

* 其中一個方法是使用自動調整取樣 toostart，找出它評分 settles （請參閱上述問題的 hello） 和交換器 toofixed 速率然後取樣使用的速率。 
  
    否則，您必須 tooguess。 分析目前的遙測 AI 使用量中出現任何節流也就是發生，以及評估 hello 磁碟區的 hello 收集遙測資料。 下列三個輸入，以及您選取的定價層建議多少，您可能會想 tooreduce hello 磁碟區的 hello 收集遙測資料。 不過，hello 您的使用者數目的增加或其他某些 shift hello 的遙測資料的磁碟區中可能會使您的評估。

*如果將取樣百分比設定成太低會發生什麼事？*

* Application Insights 嘗試 toocompensate hello 視覺效果的 hello 減少 hello 資料磁碟區的資料時，極低取樣百分比 （over-aggressive 取樣） 可減少 hello 精確度的 hello 近似值。 此外，診斷體驗可能會受到負面影響，與 hello 不常失敗的或慢速要求出取樣。

*如果將取樣百分比設定成太高會發生什麼事？*

* 設定太高取樣百分比 （不變得積極夠） 導致 hello hello 數量不足，無法減少收集的遙測。 仍可能會發生資料遺失相關 toothrottling，以及使用 Application Insights hello 成本可能會高於您計劃，因為 toooverage 費用的遙測。

*我可以在何種平台上使用取樣？*

* 特定磁碟區，上述任何遙測，如果 hello SDK 目前並未在執行取樣擷取取樣會自動發生。 這會運作，例如，如果您的應用程式使用 Java 伺服器，或如果您使用較舊版本的 hello ASP.NET SDK。
* 如果您使用 ASP.NET 的 SDK 版本 2.0.0 和更新版本 （裝載在 Azure 或您自己的伺服器上），您會收到自動調整取樣根據預設，但如上面所述，您可以切換 toofixed 速率。 使用固定速率取樣 hello 瀏覽器 SDK 會自動同步 toosample 相關事件。 

*有希望 toosee 某些罕見的事件。如何取得其過去的 hello 取樣模組？*

* 初始化新 TelemetryConfiguration （不 hello 預設作用中） 與 TelemetryClient 個別執行個體。 使用該 toosend 罕見的事件。

## <a name="next-steps"></a>後續步驟
* [篩選](app-insights-api-filtering-sampling.md) 可以對您的 SDK 所傳送的內容，提供更嚴格的控制。

