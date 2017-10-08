---
title: "aaaApplicationInsights.config 參考-Azure |Microsoft 文件"
description: "啟用或停用資料收集模組，以及加入效能計數器和其他參數。"
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>設定 Application Insights SDK hello ApplicationInsights.config 或.xml
hello Application Insights.NET SDK 的 NuGet 套件的數字所組成。 [Core 套件](http://www.nuget.org/packages/Microsoft.ApplicationInsights)提供 hello API，以將遙測傳送至 Application Insights hello。 [其他套件](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights)提供遙測*模組*和*初始設定式*，用於自動從您的應用程式和其內容追蹤遙測。 藉由調整 hello 設定檔，您可以啟用或停用遙測模組和初始設定式，和設定其中部分的參數。

hello 設定檔的名稱為`ApplicationInsights.config`或`ApplicationInsights.xml`，視您的應用程式的 hello 型別。 它會自動加入 tooyour 專案時您[安裝大部分的 hello SDK 版本][start]。 它也會加入 tooa web 應用程式由[IIS 伺服器上的狀態監視][redfield]，或當您選取 hello Appplication Insights[延伸模組的 Azure 網站或 VM](app-insights-azure-web-apps.md)。

沒有對等檔案 toocontrol hello[在網頁中的 SDK][client]。

本文件描述您看到 hello 組態檔案，控制 hello hello SDK 元件的方式，以及哪些 NuGet 封裝會載入這些元件的 hello 區段。

## <a name="telemetry-modules-aspnet"></a>遙測模組 (ASP.NET)
每個遙測模組收集特定類型的資料，並使用 hello 核心 API toosend hello 資料。 hello 模組會安裝由不同的 NuGet 封裝，也加入 hello 需要的線條 toohello.config 檔案中。

每個模組的 hello 組態檔中沒有節點。 toodisable 模組，請刪除 hello 節點，或加以註解化。

### <a name="dependency-tracking"></a>相依性追蹤
[相依性追蹤](app-insights-asp-net-dependencies.md)收集呼叫 toodatabases 和外部服務，以及資料庫，可讓您的應用程式的相關遙測。 tooallow 此模組會 toowork 在 IIS 伺服器，您需要太[安裝狀態監視器][redfield]。 toouse 在 Azure web 應用程式或 Vm，[選取 hello Application Insights 擴充功能](app-insights-azure-web-apps.md)。

您也可以撰寫您自己的相依性追蹤程式碼使用 hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency)。

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet 封裝。

### <a name="performance-collector"></a>效能收集器
[收集系統效能計數器](app-insights-performance-counters.md)，例如 CPU、記憶體和網路負載 (從 IIS 安裝)。 您可以指定哪些計數器 toocollect，包括您已設定您自己的效能計數器。

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet 封裝。

### <a name="application-insights-diagnostics-telemetry"></a>Application Insights 診斷遙測
hello`DiagnosticsTelemetryModule`報告 hello 本身 Application Insights 檢測程式碼中的錯誤。 例如，如果 hello 程式碼無法存取效能計數器或`ITelemetryInitializer`擲回例外狀況。 此模組所追蹤的追蹤遙測會出現在 hello[診斷搜尋][diagnostic]。 傳送診斷資料 toodc.services.vsallin.net。

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。 如果您只安裝這個套件，不會自動建立 hello ApplicationInsights.config 檔案。

### <a name="developer-mode"></a>開發人員模式
`DeveloperModeWithDebuggerAttachedTelemetryModule`強制 hello Application Insights `TelemetryChannel` toosend 資料立即一個遙測項目一次，當偵錯工具附加 toohello 應用程式處理序。 這會減少 hello hello 時間之間的時間量，以及出現在 hello Application Insights 入口網站時您的應用程式會追蹤遙測。 但是會造成 CPU 和網路頻寬明顯的負擔。

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝

### <a name="web-request-tracking"></a>Web 要求追蹤
報表 hello[回應時間與結果碼](app-insights-asp-net.md)的 HTTP 要求。

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。

### <a name="exception-tracking"></a>例外狀況追蹤
`ExceptionTrackingTelemetryModule` 追蹤 Web 應用程式中未處理的例外狀況。 請參閱[失敗和例外狀況][exceptions]。

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet 封裝。
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - 追蹤 [未觀察到的工作例外狀況](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx)。
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - 追蹤背景工作角色、Windows 服務和主控台應用程式的未處理例外狀況。
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet 封裝。

### <a name="eventsource-tracking"></a>EventSource 追蹤
`EventSourceTelemetryModule`可讓您 tooconfigure EventSource 事件 toobe tooApplication Insights 當做追蹤。 如需追蹤 EventSource 事件的資訊，請參閱[使用 EventSource 事件](app-insights-asp-net-trace-logs.md#using-eventsource-events)。

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>ETW 事件追蹤
`EtwCollectorTelemetryModule`可讓您從以追蹤傳送 tooApplication Insights ETW 提供者 toobe tooconfigure 事件。 如需追蹤 ETW 事件的資訊，請參閱[使用 ETW 事件](app-insights-asp-net-trace-logs.md#using-etw-events)。

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
hello Microsoft.ApplicationInsights 套件提供 hello[核心 API](https://msdn.microsoft.com/library/mt420197.aspx)的 hello SDK。 hello 其他遙測模組使用，而且您也可以[toodefine 使用它自己的遙測](app-insights-api-custom-events-metrics.md)。

* ApplicationInsights.config 中沒有項目。
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet 封裝。 如果您只安裝此 NuGet，不會產生任何 .config 檔案。

## <a name="telemetry-channel"></a>遙測通道
hello 遙測通道會管理緩衝和遙測 toohello Application Insights 服務的傳輸。

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`是服務的 hello 預設通道。 它會在記憶體中緩衝資料。
* `Microsoft.ApplicationInsights.PersistenceChannel` 是主控台應用程式的替代通道。 當您的應用程式關閉，並會將它傳送 hello 應用程式一次啟動時，便可以節省任何 unflushed 的資料 toopersistent 存放裝置。

## <a name="telemetry-initializers-aspnet"></a>遙測初始設定式 (ASP.NET)
遙測初始設定式設定與遙測的每個項目一起傳送的內容屬性。

您可以[撰寫您自己的初始設定式](app-insights-api-filtering-sampling.md#add-properties)tooset 內容屬性。

hello 標準初始設定式已設定完畢由 hello Web 或 WindowsServer NuGet 封裝：

* `AccountIdTelemetryInitializer`設定 hello AccountId 屬性。
* `AuthenticatedUserIdTelemetryInitializer`hello JavaScript SDK hello AuthenticatedUserId 屬性設定為集合。
* `AzureRoleEnvironmentTelemetryInitializer`更新 hello`RoleName`和`RoleInstance`屬性 hello`Device`從 hello Azure 執行階段環境中擷取資訊的所有遙測項目內容。
* `BuildInfoConfigComponentVersionTelemetryInitializer`更新 hello`Version`屬性 hello `Component` hello 值 hello 從擷取的所有遙測項目內容`BuildInfo.config`由 MS Build 所產生的檔案。
* `ClientIpHeaderTelemetryInitializer`更新`Ip`屬性 hello`Location`所有遙測項目的內容根據 hello `X-Forwarded-For` hello 要求的 HTTP 標頭。
* `DeviceTelemetryInitializer`下列屬性的 hello 更新 hello`Device`遙測的所有項目內容。
  * `Type`設定得 「 電腦 」
  * `Id`已設定 hello web 應用程式執行所在 toohello hello 電腦網域名稱。
  * `OemName`設定為擷取自 hello toohello 值`Win32_ComputerSystem.Manufacturer`欄位使用 WMI。
  * `Model`設定為擷取自 hello toohello 值`Win32_ComputerSystem.Model`欄位使用 WMI。
  * `NetworkType`設定為擷取自 hello toohello 值`NetworkInterface`。
  * `Language`設定的 hello toohello 名稱`CurrentCulture`。
* `DomainNameRoleInstanceTelemetryInitializer`更新 hello`RoleInstance`屬性 hello`Device`遙測的所有項目 hello 網域名稱與 hello hello web 應用程式執行所在的電腦內容。
* `OperationNameTelemetryInitializer`更新 hello`Name`屬性 hello`RequestTelemetry`和 hello`Name`屬性 hello`Operation`所有遙測項目的內容根據 hello HTTP 方法，以及 ASP.NET MVC 控制器和動作叫用的 tooprocess hello 的名稱要求。
* `OperationIdTelemetryInitializer`或`OperationCorrelationTelemetryInitializer`更新 hello`Operation.Id`內容屬性的所有遙測項目追蹤同時處理要求，以自動產生的 hello `RequestTelemetry.Id`。
* `SessionTelemetryInitializer`更新 hello`Id`屬性 hello `Session` hello 從擷取值的所有遙測項目內容`ai_session`cookie 所 hello ApplicationInsights JavaScript hello 使用者的瀏覽器中執行的檢測程式碼產生。
* `SyntheticTelemetryInitializer`或`SyntheticUserAgentTelemetryInitializer`更新 hello `User`，`Session`和`Operation`時處理的要求的綜合的來源，例如可用性測試，或搜尋引擎 bot 追蹤這些內容屬性的所有遙測項目。 根據預設， [計量瀏覽器](app-insights-metrics-explorer.md) 不會顯示綜合的遙測。

    hello`<Filters>`設定識別之 hello 要求的內容。
* `UserAgentTelemetryInitializer`更新 hello`UserAgent`屬性 hello`User`所有遙測項目的內容根據 hello `User-Agent` hello 要求的 HTTP 標頭。
* `UserTelemetryInitializer`更新 hello`Id`和`AcquisitionDate`屬性`User`內容擷取自 hello 值的所有遙測項目`ai_user`hello 中執行的 hello Application Insights JavaScript 檢測程式碼所產生的 cookie使用者的瀏覽器。
* `WebTestTelemetryInitializer`設定 hello 使用者 id、 工作階段識別碼和綜合的來源屬性的 HTTP 要求，來自[可用性測試](app-insights-monitor-web-app-availability.md)。
  hello`<Filters>`設定識別之 hello 要求的內容。

Service Fabric 中執行的.NET 應用程式，您可以包含 hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet 封裝。 這個套件包括`FabricTelemetryInitializer`，這樣會將 Service Fabric 屬性 tootelemetry 項目。 如需詳細資訊，請參閱 hello [GitHub 頁面](https://go.microsoft.com/fwlink/?linkid=848457)有關 hello 屬性加入此 NuGet 封裝。

## <a name="telemetry-processors-aspnet"></a>遙測處理器 (ASP.NET)
遙測處理器可以篩選和寄 hello SDK toohello 入口網站之前，請修改每個遙測項目。

您可以 [撰寫您自己的遙測處理器](app-insights-api-filtering-sampling.md#filtering)。

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>自適性取樣遙測處理器 (自 2.0.0-beta3 起)
此選項預設為啟用狀態。 如果您的應用程式傳送許多遙測，此處理器會移除其中一些遙測。

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

hello 參數提供 hello 演算法的 hello 目標嘗試 tooachieve。 Hello SDK 可獨立作業，因此如果您的伺服器是叢集的多部電腦，將據此相乘 hello 的遙測資料的實際磁碟區的每個執行個體。

[深入了解取樣](app-insights-sampling.md)。

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>固定取樣遙測處理器 (自 2.0.0-beta1 起)
還有一種標準的 [取樣遙測處理器](app-insights-api-filtering-sampling.md) (自 2.0.1 起)：

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>通道參數 (Java)
這些參數會影響 hello Java SDK 應該如何儲存及排清 hello 它所收集的遙測資料。

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
hello hello SDK 的記憶體中儲存體可以儲存的遙測項目數目。 當到達此數目時，hello 遙測緩衝區排清-也就是 hello 遙測項目會傳送 toohello Application Insights 的伺服器。

* 最小值：1
* 最大值：1000
* 預設值：500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
決定多久 hello hello 記憶體中儲存體中儲存的資料應排清 (傳送的 tooApplication Insights)。

* 最小值：1
* 最大值：300
* 預設值：5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
決定 hello 以 mb 為單位配置 toohello hello 本機磁碟上的永續性儲存體大小上限。 這個儲存體用於保存無法傳輸 toobe toohello Application Insights 端點的遙測項目。 當已符合 hello 儲存體大小時，將會捨棄新的遙測項目。

* 最小值：1
* 最大值：100
* 預設值：10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
這會決定您的資料會顯示 hello Application Insights 資源。 通常您會針對每個應用程式，用個別的金鑰建立個別資源。

如果您想 tooset hello 金鑰動態-例如如果您希望 toosend 結果從您的應用程式的 toodifferent 資源-您可以省略 hello 組態檔中的 hello 金鑰並將它設定在程式碼中。

tooset hello TelemetryClient，包括標準遙測模組的所有執行個體索引鍵在 TelemetryConfiguration.Active 設定 hello 索引。 請在初始化方法中這麼做，例如 ASP.NET 服務中的 global.aspx.cs：

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

如果您只想 toosend 一組特定的事件 tooa 不同的資源，您可以設定特定 TelemetryClient hello 索引鍵：

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

新機碼 tooget [hello Application Insights 入口網站中建立新的資源][new]。

## <a name="next-steps"></a>後續步驟
[深入了解 hello API][api]。

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
