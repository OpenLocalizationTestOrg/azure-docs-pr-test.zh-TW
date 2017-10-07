---
title: "aaaExplore.NET 追蹤記錄，在 Application Insights"
description: "搜尋使用 Trace、NLog 或 Log4Net 產生的記錄檔。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>在 Application Insights 中探索 .NET 追蹤記錄
如果您使用 NLog、 log4Net 或 System.Diagnostics.Trace 進行診斷追蹤 ASP.NET 應用程式中，您就可以讓您傳送的記錄[Azure Application Insights][start]，其中您可以瀏覽和搜尋它們。 要與其他 hello 合併您的記錄檔，讓您可以識別即將從您的應用程式的遙測 hello 與每個使用者要求提供服務相關聯的追蹤，並將它們與其他事件和例外狀況報告相互關聯。

> [!NOTE]
> 您需要 hello 記錄擷取模組嗎？ 對於第三方記錄器來說，它是一個有用的配接器，但是如果您還沒使用 NLog、log4Net 或 System.Diagnostics.Trace，請考慮直接呼叫 [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 。
>
>

## <a name="install-logging-on-your-app"></a>在您的 app 上安裝記錄
在專案中安裝您選擇的記錄架構。 這應該會在 app.config 或 web.config 中產生一個項目。

如果您使用 System.Diagnostics.Trace，您會需要 tooadd 項目 tooweb.config:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>設定 Application Insights toocollect 記錄檔
**[將 Application Insights tooyour 專案](app-insights-asp-net.md)**如果您沒有執行此步驟。 您會看到選項 tooinclude hello 記錄檔收集器。

或者，在 [方案總管] 中以滑鼠右鍵按一下專案，來 **設定 Application Insights** 。 選取 hello 選項太**設定追蹤集合**。

*沒有 Application Insights 功能表或記錄收集器選項嗎？* 請嘗試進行[疑難排解](#troubleshooting)。

## <a name="manual-installation"></a>手動安裝
如果您的專案類型不支援 hello Application Insights 安裝程式 （例如 Windows 桌面專案），請使用這個方法。

1. 如果您計劃 toouse log4Net 或 NLog，請將它安裝在您的專案。
2. 在 [方案總管] 中，以滑鼠右鍵按一下您的專案並選擇 [ **管理 NuGet 封裝**]。
3. 搜尋「Application Insights」
4. 選取 hello 適當套件的其中一個：

   * Microsoft.ApplicationInsights.TraceListener （toocapture System.Diagnostics.Trace 呼叫）
   * Microsoft.ApplicationInsights.EventSourceListener （toocapture EventSource 事件）
   * Microsoft.ApplicationInsights.EtwListener （toocapture ETW 事件）
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

hello NuGet 封裝會安裝 hello 必要組件，並也會修改 web.config 或 app.config。

## <a name="insert-diagnostic-log-calls"></a>插入診斷記錄呼叫
如果您使用 System.Diagnostics.Trace，典型的呼叫如下：

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

如果您偏好 log4net 或 NLog：

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>使用 EventSource 事件
您可以設定[System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)事件傳送 toobe tooApplication 為追蹤的深入資訊。 首先，安裝 hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet 封裝。 然後編輯`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

每個來源，您可以設定下列參數的 hello:
 * `Name`指定 hello EventSource toocollect hello 名稱。
 * `Level`指定記錄層級 toocollect hello。 可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。
 * `Keywords`（選擇性） 指定關鍵字組合 toouse hello 整數的值。

## <a name="using-diagnosticsource-events"></a>使用 DiagnosticSource 事件
您可以設定[System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)事件傳送 toobe tooApplication 為追蹤的深入資訊。 首先，安裝 hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet 封裝。 然後編輯 hello`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

您要為每個 DiagnosticSource tootrace，加入一個項目以 hello`Name`您 DiagnosticSource toohello 名稱的屬性設定。

## <a name="using-etw-events"></a>使用 ETW 事件
您可以設定 ETW 事件 toobe tooApplication Insights 當做追蹤。 首先，安裝 hello `Microsoft.ApplicationInsights.EtwCollector` NuGet 封裝。 然後編輯`TelemetryModules`區段 hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)檔案。

> [!NOTE] 
> 如果 hello 處理序主控 hello SDK 執行的 「 效能記錄使用者 」 或系統管理員成員的身分識別，您可以只收集 ETW 事件。

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

每個來源，您可以設定下列參數的 hello:
 * `ProviderName`這是 hello ETW 提供者 toocollect hello 名稱。
 * `ProviderGuid`指定 hello 的 hello ETW 提供者 toocollect，GUID 可以使用而不是`ProviderName`。
 * `Level`設定記錄層級 toocollect hello。 可以是 `Critical`、`Error`、`Informational`、`LogAlways`、`Verbose`、`Warning` 其中一個。
 * `Keywords`（選擇性） 設定 hello 關鍵字組合 toouse 的整數的值。

## <a name="using-hello-trace-api-directly"></a>直接使用 hello 追蹤應用程式開發介面
您可以直接呼叫 hello Application Insights 追蹤應用程式開發介面。 hello 記錄配接器會使用此 API。

例如：

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

TrackTrace 的優點是您可以將較長的資料放在 hello 訊息。 例如，您可以在該處編碼 POST 資料。

此外，您可以加入嚴重性層級 tooyour 訊息。 與其他遙測，例如，您可以加入您可以使用 toohelp 篩選或搜尋不同的追蹤集合的屬性值。 例如：

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

這可讓您在[搜尋][diagnostic]，tooeasily 篩選出特定嚴重性等級相關 tooa 特定資料庫的所有 hello 訊息。

## <a name="explore-your-logs"></a>探索記錄
在偵錯模式中執行您的 app 或即時部署它。

在您的應用程式概觀刀鋒視窗中[hello Application Insights 入口網站][portal]，選擇[搜尋][diagnostic]。

![在 Application Insights 中，選擇 [搜尋]](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![搜尋](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

例如，您可以：

* 篩選記錄追蹤，或具有特定屬性的項目
* 詳細檢查特定項目。
* 尋找有關 toohello 其他遙測同一個使用者要求 (亦即，與 hello 相同 OperationId)
* 此頁面的 hello 組態儲存為我的最愛

> [!NOTE]
> **取樣** 如果您的應用程式傳送大量資料，您使用 hello Application Insights SDK 或更新版本的 ASP.NET 版本 2.0.0-beta3 hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。 [深入了解取樣。](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>後續步驟
[在 ASP.NET 中診斷失敗和例外狀況][exceptions]

[深入了解搜尋][diagnostic]。

## <a name="troubleshooting"></a>疑難排解
### <a name="how-do-i-do-this-for-java"></a>如果是 Java，我要怎麼做？
使用 hello [Java 記錄配接器](app-insights-java-trace-logs.md)。

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>沒有 hello 專案操作功能表上的 Application Insights 選項
* 請檢查已在此開發電腦上安裝 Application Insights 工具。 在 Visual Studio 功能表 [工具、擴充功能和更新] 中，尋找 Application Insights 工具。 如果沒有 hello 已安裝 索引標籤中，開啟線上 hello 索引標籤，並安裝它。
* 這可能是 Application Insights 工具不支援的一種專案類型。 請使用 [手動安裝](#manual-installation)。

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Hello 組態工具中沒有記錄配接器選項
* 您首先需要 tooinstall hello 記錄架構。
* 如果您使用 System.Diagnostics.Trace，請確定您[已在 `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx) 中設定它。
* 您已有 hello 最新版 Application Insights 嗎？ 在 Visual Studio**工具**功能表上，選擇**擴充功能和更新**，並開啟 hello**更新** 索引標籤。如果開發人員分析工具已存在，請按一下 tooupdate 它。

### <a name="emptykey"></a>我收到「檢測金鑰不能是空白」的錯誤
似乎您已安裝而不需要安裝 Application Insights 記錄配接器的 Nuget 套件 hello。

在 [方案總管] 中，以滑鼠右鍵按一下 `ApplicationInsights.config` ，然後選擇 [ **更新 Application Insights**]。 就會顯示一個對話方塊，邀請您 toosign tooAzure 中，然後建立 Application Insights 資源，或重複使用現有的我的最愛。 這樣應該可以解決。

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>我可以看見追蹤在診斷搜尋中，但不是 hello 其他事件
有時可能需要一些所有 hello 事件和要求 tooget hello 管線。

### <a name="limits"></a>保留多少資料？
數個因素會影響 hello 保留的資料量。 請參閱 hello[限制](app-insights-api-custom-events-metrics.md#limits)hello 客戶事件如需詳細資訊 度量頁面的區段。 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>我沒有看到一些預期 hello 記錄項目
如果您的應用程式傳送大量資料，您使用 hello Application Insights SDK 或更新版本的 ASP.NET 版本 2.0.0-beta3 hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。 [深入了解取樣。](app-insights-sampling.md)

## <a name="add"></a>接續步驟
* [設定可用性和回應性測試][availability]
* [疑難排解][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
