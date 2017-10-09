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
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="c8a05-103">產生應用程式與服務層級事件和記錄</span><span class="sxs-lookup"><span data-stu-id="c8a05-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="c8a05-104">檢測 hello 與自訂事件的程式碼</span><span class="sxs-lookup"><span data-stu-id="c8a05-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="c8a05-105">檢測 hello 程式碼是 hello 基礎其他大部分層面的監視您的服務。</span><span class="sxs-lookup"><span data-stu-id="c8a05-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="c8a05-106">檢測是您可以知道有問題，而且需要固定 toobe toodiagnose hello 唯一方式。</span><span class="sxs-lookup"><span data-stu-id="c8a05-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="c8a05-107">雖然技術上來說很可能 tooconnect 偵錯工具 tooa 實際執行服務，它並不常見的作法。</span><span class="sxs-lookup"><span data-stu-id="c8a05-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="c8a05-108">因此，取得詳細的檢測資料很重要。</span><span class="sxs-lookup"><span data-stu-id="c8a05-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="c8a05-109">某些產品會自動檢測您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8a05-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="c8a05-110">雖然這些產品的效果不錯，但幾乎都還是需要手動檢測。</span><span class="sxs-lookup"><span data-stu-id="c8a05-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="c8a05-111">在 hello 結束時，您必須擁有 hello 應用程式進行偵錯的足夠資訊 tooforensically。</span><span class="sxs-lookup"><span data-stu-id="c8a05-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="c8a05-112">本文件將說明不同的方法 tooinstrumenting 程式碼，和一個 toochoose 透過另一個的方法時。</span><span class="sxs-lookup"><span data-stu-id="c8a05-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="c8a05-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="c8a05-113">EventSource</span></span>
<span data-ttu-id="c8a05-114">當您在 Visual Studio 中從範本建立 Service Fabric 解決方案時，將會產生 **EventSource** 衍生類別 (**ServiceEventSource** 或 **ActorEventSource**)。</span><span class="sxs-lookup"><span data-stu-id="c8a05-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="c8a05-115">建立的範本可讓您為應用程式或服務新增事件。</span><span class="sxs-lookup"><span data-stu-id="c8a05-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="c8a05-116">hello **EventSource**名稱**必須**是唯一的而且應該從 hello 預設範本字串 MyCompany-重新命名&lt;方案&gt;- &lt;專案&gt;。</span><span class="sxs-lookup"><span data-stu-id="c8a05-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="c8a05-117">有多個**EventSource**使用定義 hello 的問題，在執行階段的相同名稱原因。</span><span class="sxs-lookup"><span data-stu-id="c8a05-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="c8a05-118">每個已定義事件都必須有獨一無二的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c8a05-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="c8a05-119">如果識別碼並非獨一無二，會發生執行階段失敗。</span><span class="sxs-lookup"><span data-stu-id="c8a05-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="c8a05-120">某些組織 preassign 範圍之識別項 tooavoid 衝突，個別的開發團隊之間的值。</span><span class="sxs-lookup"><span data-stu-id="c8a05-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="c8a05-121">如需詳細資訊，請參閱[Vance 的部落格](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)或 hello [MSDN 文件](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c8a05-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="c8a05-122">使用結構化 EventSource 事件</span><span class="sxs-lookup"><span data-stu-id="c8a05-122">Using structured EventSource events</span></span>

<span data-ttu-id="c8a05-123">每個 hello 程式碼範例，本節中的 hello 事件會定義特定的情況下，比方說，註冊服務類型。</span><span class="sxs-lookup"><span data-stu-id="c8a05-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="c8a05-124">當您定義使用大小寫的訊息時，資料可以封裝與 hello 錯誤的文字 hello，而您可以更輕鬆地搜尋和指定屬性的 hello 名稱或值的 hello 為基礎的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="c8a05-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="c8a05-125">建構 hello 檢測設備輸出可讓您更輕鬆 tooconsume，但需要更多的思考和新的事件時間 toodefine 在每個使用案例。</span><span class="sxs-lookup"><span data-stu-id="c8a05-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="c8a05-126">某些事件定義可 hello 整個應用程式之間共用。</span><span class="sxs-lookup"><span data-stu-id="c8a05-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="c8a05-127">例如，應用程式內的許多不同服務會重複使用方法啟動或停止事件。</span><span class="sxs-lookup"><span data-stu-id="c8a05-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="c8a05-128">特定網域服務有自己的獨特事件，例如，訂單系統可能有 **CreateOrder** 事件。</span><span class="sxs-lookup"><span data-stu-id="c8a05-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="c8a05-129">此方法可能產生很多事件，專案小組之間可能需要協調識別碼。</span><span class="sxs-lookup"><span data-stu-id="c8a05-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

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

### <a name="using-eventsource-generically"></a><span data-ttu-id="c8a05-130">以一般方式使用 EventSource</span><span class="sxs-lookup"><span data-stu-id="c8a05-130">Using EventSource generically</span></span>

<span data-ttu-id="c8a05-131">因為定義特定事件可能很困難，許多人會以一組常用的參數定義少量事件，且通常會將資訊輸出為字串。</span><span class="sxs-lookup"><span data-stu-id="c8a05-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="c8a05-132">大部分的結構化的 hello 外觀已遺失，而更難 toosearch 和篩選 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="c8a05-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="c8a05-133">在這種方式，被定義少數通常對應 toohello 記錄層級的事件。</span><span class="sxs-lookup"><span data-stu-id="c8a05-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="c8a05-134">下列程式碼片段的 hello 定義偵錯和錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="c8a05-134">hello following snippet defines a debug and error message:</span></span>

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

<span data-ttu-id="c8a05-135">使用混合式的結構化和泛型檢測也可行。</span><span class="sxs-lookup"><span data-stu-id="c8a05-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="c8a05-136">結構化檢測用於報告錯誤和計量。</span><span class="sxs-lookup"><span data-stu-id="c8a05-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="c8a05-137">泛型事件可用於 hello 詳細的記錄也就由工程師進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="c8a05-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="c8a05-138">ASP.NET Core 記錄</span><span class="sxs-lookup"><span data-stu-id="c8a05-138">ASP.NET Core logging</span></span>

<span data-ttu-id="c8a05-139">它的重要 toocarefully 計劃將檢測程式碼的方式。</span><span class="sxs-lookup"><span data-stu-id="c8a05-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="c8a05-140">hello 右檢測計劃可協助您避免在可能會造成不穩定程式碼基底，再接著需要 tooreinstrument hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8a05-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="c8a05-141">tooreduce 風險，您可以選擇檢測程式庫如[Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)，這是 Microsoft ASP.NET Core 的部分。</span><span class="sxs-lookup"><span data-stu-id="c8a05-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="c8a05-142">具有 ASP.NET Core [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger)降至最低 hello 會對現有的程式碼使用您選擇的 hello 提供者的介面。</span><span class="sxs-lookup"><span data-stu-id="c8a05-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="c8a05-143">您可以使用在 Windows 和 Linux 上的 ASP.NET Core hello 的程式碼，並在 hello 完整.NET Framework 中，讓您檢測程式碼已標準化。</span><span class="sxs-lookup"><span data-stu-id="c8a05-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="c8a05-144">下方會進一步探討這項資訊：</span><span class="sxs-lookup"><span data-stu-id="c8a05-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="c8a05-145">使用 Service Fabric 中的 Microsoft.Extensions.Logging</span><span class="sxs-lookup"><span data-stu-id="c8a05-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="c8a05-146">新增 hello 想 tooinstrument Microsoft.Extensions.Logging NuGet 封裝 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="c8a05-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="c8a05-147">此外，請加入任何提供者套件 （第三方封裝，請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="c8a05-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="c8a05-148">如需詳細資訊，請參閱 [ASP.NET Core 中的記錄](https://docs.microsoft.com/aspnet/core/fundamentals/logging)。</span><span class="sxs-lookup"><span data-stu-id="c8a05-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="c8a05-149">新增**使用**Microsoft.Extensions.Logging tooyour 服務檔指示詞。</span><span class="sxs-lookup"><span data-stu-id="c8a05-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="c8a05-150">在服務類別內定義私用變數。</span><span class="sxs-lookup"><span data-stu-id="c8a05-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="c8a05-151">在您的服務類別的 hello 建構函式，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c8a05-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="c8a05-152">開始用您的方法檢測程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8a05-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="c8a05-153">以下是幾個範例：</span><span class="sxs-lookup"><span data-stu-id="c8a05-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="c8a05-154">使用其他記錄提供者</span><span class="sxs-lookup"><span data-stu-id="c8a05-154">Using other logging providers</span></span>

<span data-ttu-id="c8a05-155">某些協力廠商提供者，請使用 hello hello 前面一節中所述的方法包括[Serilog](https://serilog.net/)， [NLog](http://nlog-project.org/)，和[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)。</span><span class="sxs-lookup"><span data-stu-id="c8a05-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="c8a05-156">您可以將這些全部插入 ASP.NET Core 記錄中，也可以分開使用。</span><span class="sxs-lookup"><span data-stu-id="c8a05-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="c8a05-157">Serilog 有一項功能讓記錄器傳來的所有訊息更豐富。</span><span class="sxs-lookup"><span data-stu-id="c8a05-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="c8a05-158">這個功能便相當有用 toooutput hello 服務名稱、 類型和資料分割資訊。</span><span class="sxs-lookup"><span data-stu-id="c8a05-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="c8a05-159">toouse hello ASP.NET 核心基礎結構，此功能，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c8a05-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="c8a05-160">新增 hello Serilog，Serilog.Extensions.Logging，並將 Serilog.Sinks.Observable NuGet 封裝 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="c8a05-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="c8a05-161">Hello 下一個範例中，也加入 Serilog.Sinks.Literate。</span><span class="sxs-lookup"><span data-stu-id="c8a05-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="c8a05-162">本文稍後會示範更好的方法。</span><span class="sxs-lookup"><span data-stu-id="c8a05-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="c8a05-163">在 Serilog，建立 LoggerConfiguration 和 hello 的記錄器執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8a05-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="c8a05-164">加入 Serilog.ILogger 引數 toohello 服務建構函式，並將傳遞 hello 新建立的記錄器。</span><span class="sxs-lookup"><span data-stu-id="c8a05-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="c8a05-165">Hello 服務建構函式中加入下列程式碼會建立 hello hello 屬性 enrichers hello **ServiceTypeName**， **ServiceName**， **PartitionId**，和**InstanceId** hello 服務的屬性。</span><span class="sxs-lookup"><span data-stu-id="c8a05-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="c8a05-166">它也會加入屬性 enricher toohello ASP.NET Core 記錄處理站，因此您可以在程式碼中使用 Microsoft.Extensions.Logging.ILogger。</span><span class="sxs-lookup"><span data-stu-id="c8a05-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="c8a05-167">檢測 hello 程式碼時，如果您使用 ASP.NET Core 沒有 Serilog hello 相同。</span><span class="sxs-lookup"><span data-stu-id="c8a05-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c8a05-168">我們建議您不要使用 hello 靜態 Log.Logger 以上述範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="c8a05-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="c8a05-169">Service Fabric 可以裝載多個執行個體的 hello 相同服務的單一處理序內的類型。</span><span class="sxs-lookup"><span data-stu-id="c8a05-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="c8a05-170">如果您使用 hello 靜態 Log.Logger，hello hello 屬性 enrichers 的最後一個寫入器會顯示正在執行的所有執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="c8a05-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="c8a05-171">這是一個原因 hello _logger 變數 hello 服務類別的私用成員變數。</span><span class="sxs-lookup"><span data-stu-id="c8a05-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="c8a05-172">此外，您必須進行 hello _logger 可用 toocommon 程式碼，這可能會在服務使用。</span><span class="sxs-lookup"><span data-stu-id="c8a05-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="c8a05-173">選擇記錄提供者</span><span class="sxs-lookup"><span data-stu-id="c8a05-173">Choosing a logging provider</span></span>

<span data-ttu-id="c8a05-174">如果您的應用程式仰賴高效能，採用 **EventSource** 通常是不錯的方法。</span><span class="sxs-lookup"><span data-stu-id="c8a05-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="c8a05-175">**EventSource** *通常*使用較少的資源並執行效能優於 ASP.NET Core 記錄或任何 hello 可用的協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="c8a05-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="c8a05-176">這對於許多服務而言並不是問題，但如果您的服務屬於效能導向，使用 **EventSource** 可能是更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="c8a05-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="c8a05-177">不過，tooget 這些優點結構化記錄、 **EventSource**需要較大的投資，從您的工程團隊。</span><span class="sxs-lookup"><span data-stu-id="c8a05-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="c8a05-178">可能的話，請執行快速少數的記錄選項的原型，然後選擇 hello 最符合您需求的其中一個。</span><span class="sxs-lookup"><span data-stu-id="c8a05-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8a05-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8a05-179">Next steps</span></span>

<span data-ttu-id="c8a05-180">一旦您已選擇您的記錄提供者 tooinstrument 應用程式和服務，將記錄檔和事件需要 toobe 之前它們可以傳送 tooany 分析平台的彙總資料。</span><span class="sxs-lookup"><span data-stu-id="c8a05-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="c8a05-181">閱讀有關[EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)和[WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter 了解一些 hello 建議的選項。</span><span class="sxs-lookup"><span data-stu-id="c8a05-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
