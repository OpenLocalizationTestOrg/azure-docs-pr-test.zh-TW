---
title: "服務網狀架構應用程式層級監視 aaaAzure |Microsoft 文件"
description: "了解應用程式及服務層級的事件和記錄檔使用 toomonitor，並診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>產生應用程式與服務層級事件和記錄

## <a name="instrumenting-hello-code-with-custom-events"></a>檢測 hello 與自訂事件的程式碼

檢測 hello 程式碼是 hello 基礎其他大部分層面的監視您的服務。 檢測是您可以知道有問題，而且需要固定 toobe toodiagnose hello 唯一方式。 雖然技術上來說很可能 tooconnect 偵錯工具 tooa 實際執行服務，它並不常見的作法。 因此，取得詳細的檢測資料很重要。

某些產品會自動檢測您的程式碼。 雖然這些產品的效果不錯，但幾乎都還是需要手動檢測。 在 hello 結束時，您必須擁有 hello 應用程式進行偵錯的足夠資訊 tooforensically。 本文件將說明不同的方法 tooinstrumenting 程式碼，和一個 toochoose 透過另一個的方法時。

## <a name="eventsource"></a>EventSource
當您在 Visual Studio 中從範本建立 Service Fabric 解決方案時，將會產生 **EventSource** 衍生類別 (**ServiceEventSource** 或 **ActorEventSource**)。 建立的範本可讓您為應用程式或服務新增事件。 hello **EventSource**名稱**必須**是唯一的而且應該從 hello 預設範本字串 MyCompany-重新命名&lt;方案&gt;- &lt;專案&gt;。 有多個**EventSource**使用定義 hello 的問題，在執行階段的相同名稱原因。 每個已定義事件都必須有獨一無二的識別碼。 如果識別碼並非獨一無二，會發生執行階段失敗。 某些組織 preassign 範圍之識別項 tooavoid 衝突，個別的開發團隊之間的值。 如需詳細資訊，請參閱[Vance 的部落格](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)或 hello [MSDN 文件](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx)。

### <a name="using-structured-eventsource-events"></a>使用結構化 EventSource 事件

每個 hello 程式碼範例，本節中的 hello 事件會定義特定的情況下，比方說，註冊服務類型。 當您定義使用大小寫的訊息時，資料可以封裝與 hello 錯誤的文字 hello，而您可以更輕鬆地搜尋和指定屬性的 hello 名稱或值的 hello 為基礎的篩選條件。 建構 hello 檢測設備輸出可讓您更輕鬆 tooconsume，但需要更多的思考和新的事件時間 toodefine 在每個使用案例。 某些事件定義可 hello 整個應用程式之間共用。 例如，應用程式內的許多不同服務會重複使用方法啟動或停止事件。 特定網域服務有自己的獨特事件，例如，訂單系統可能有 **CreateOrder** 事件。 此方法可能產生很多事件，專案小組之間可能需要協調識別碼。 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>以一般方式使用 EventSource

因為定義特定事件可能很困難，許多人會以一組常用的參數定義少量事件，且通常會將資訊輸出為字串。 大部分的結構化的 hello 外觀已遺失，而更難 toosearch 和篩選 hello 結果。 在這種方式，被定義少數通常對應 toohello 記錄層級的事件。 下列程式碼片段的 hello 定義偵錯和錯誤訊息：

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

使用混合式的結構化和泛型檢測也可行。 結構化檢測用於報告錯誤和計量。 泛型事件可用於 hello 詳細的記錄也就由工程師進行疑難排解。

## <a name="aspnet-core-logging"></a>ASP.NET Core 記錄

它的重要 toocarefully 計劃將檢測程式碼的方式。 hello 右檢測計劃可協助您避免在可能會造成不穩定程式碼基底，再接著需要 tooreinstrument hello 程式碼。 tooreduce 風險，您可以選擇檢測程式庫如[Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)，這是 Microsoft ASP.NET Core 的部分。 具有 ASP.NET Core [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger)降至最低 hello 會對現有的程式碼使用您選擇的 hello 提供者的介面。 您可以使用在 Windows 和 Linux 上的 ASP.NET Core hello 的程式碼，並在 hello 完整.NET Framework 中，讓您檢測程式碼已標準化。 下方會進一步探討這項資訊：

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>使用 Service Fabric 中的 Microsoft.Extensions.Logging

1. 新增 hello 想 tooinstrument Microsoft.Extensions.Logging NuGet 封裝 toohello 專案。 此外，請加入任何提供者套件 （第三方封裝，請參閱下列範例中的 hello）。 如需詳細資訊，請參閱 [ASP.NET Core 中的記錄](https://docs.microsoft.com/aspnet/core/fundamentals/logging)。
2. 新增**使用**Microsoft.Extensions.Logging tooyour 服務檔指示詞。
3. 在服務類別內定義私用變數。

  ```csharp
  private ILogger _logger = null;

  ```
4. 在您的服務類別的 hello 建構函式，加入下列程式碼：

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. 開始用您的方法檢測程式碼。 以下是幾個範例：

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>使用其他記錄提供者

某些協力廠商提供者，請使用 hello hello 前面一節中所述的方法包括[Serilog](https://serilog.net/)， [NLog](http://nlog-project.org/)，和[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)。 您可以將這些全部插入 ASP.NET Core 記錄中，也可以分開使用。 Serilog 有一項功能讓記錄器傳來的所有訊息更豐富。 這個功能便相當有用 toooutput hello 服務名稱、 類型和資料分割資訊。 toouse hello ASP.NET 核心基礎結構，此功能，請執行下列步驟：

1. 新增 hello Serilog，Serilog.Extensions.Logging，並將 Serilog.Sinks.Observable NuGet 封裝 toohello 專案。 Hello 下一個範例中，也加入 Serilog.Sinks.Literate。 本文稍後會示範更好的方法。
2. 在 Serilog，建立 LoggerConfiguration 和 hello 的記錄器執行個體。

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. 加入 Serilog.ILogger 引數 toohello 服務建構函式，並將傳遞 hello 新建立的記錄器。

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. Hello 服務建構函式中加入下列程式碼會建立 hello hello 屬性 enrichers hello **ServiceTypeName**， **ServiceName**， **PartitionId**，和**InstanceId** hello 服務的屬性。 它也會加入屬性 enricher toohello ASP.NET Core 記錄處理站，因此您可以在程式碼中使用 Microsoft.Extensions.Logging.ILogger。

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. 檢測 hello 程式碼時，如果您使用 ASP.NET Core 沒有 Serilog hello 相同。

  >[!NOTE]
  >我們建議您不要使用 hello 靜態 Log.Logger 以上述範例中的 hello。 Service Fabric 可以裝載多個執行個體的 hello 相同服務的單一處理序內的類型。 如果您使用 hello 靜態 Log.Logger，hello hello 屬性 enrichers 的最後一個寫入器會顯示正在執行的所有執行個體的值。 這是一個原因 hello _logger 變數 hello 服務類別的私用成員變數。 此外，您必須進行 hello _logger 可用 toocommon 程式碼，這可能會在服務使用。

## <a name="choosing-a-logging-provider"></a>選擇記錄提供者

如果您的應用程式仰賴高效能，採用 **EventSource** 通常是不錯的方法。 **EventSource** *通常*使用較少的資源並執行效能優於 ASP.NET Core 記錄或任何 hello 可用的協力廠商解決方案。  這對於許多服務而言並不是問題，但如果您的服務屬於效能導向，使用 **EventSource** 可能是更好的選擇。 不過，tooget 這些優點結構化記錄、 **EventSource**需要較大的投資，從您的工程團隊。 可能的話，請執行快速少數的記錄選項的原型，然後選擇 hello 最符合您需求的其中一個。

## <a name="next-steps"></a>後續步驟

一旦您已選擇您的記錄提供者 tooinstrument 應用程式和服務，將記錄檔和事件需要 toobe 之前它們可以傳送 tooany 分析平台的彙總資料。 閱讀有關[EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)和[WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter 了解一些 hello 建議的選項。
