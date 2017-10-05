---
title: "Azure Service Fabric 應用程式層級監視 | Microsoft Docs"
description: "了解用來監視和診斷 Azure Service Fabric 叢集的應用程式與服務層級事件和記錄。"
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="7198a-103">產生應用程式與服務層級事件和記錄</span><span class="sxs-lookup"><span data-stu-id="7198a-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="7198a-104">使用自訂事件檢測程式碼</span><span class="sxs-lookup"><span data-stu-id="7198a-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="7198a-105">檢測程式碼是其他監視服務層面的基礎。</span><span class="sxs-lookup"><span data-stu-id="7198a-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="7198a-106">為了讓您知道有問題發生，並診斷有什麼需要修正，檢測是唯一方式。</span><span class="sxs-lookup"><span data-stu-id="7198a-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="7198a-107">雖然技術上可以將偵錯工具連線至生產服務，但這不是常見的做法。</span><span class="sxs-lookup"><span data-stu-id="7198a-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="7198a-108">因此，取得詳細的檢測資料很重要。</span><span class="sxs-lookup"><span data-stu-id="7198a-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="7198a-109">某些產品會自動檢測您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7198a-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="7198a-110">雖然這些產品的效果不錯，但幾乎都還是需要手動檢測。</span><span class="sxs-lookup"><span data-stu-id="7198a-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="7198a-111">最後您還是要有足夠資訊，才能以抽絲剝繭的方式對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="7198a-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="7198a-112">本文件說明檢測程式碼的不同方法，以及在何種情況下應選擇什麼方法。</span><span class="sxs-lookup"><span data-stu-id="7198a-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="7198a-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="7198a-113">EventSource</span></span>
<span data-ttu-id="7198a-114">當您在 Visual Studio 中從範本建立 Service Fabric 解決方案時，將會產生 **EventSource** 衍生類別 (**ServiceEventSource** 或 **ActorEventSource**)。</span><span class="sxs-lookup"><span data-stu-id="7198a-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="7198a-115">建立的範本可讓您為應用程式或服務新增事件。</span><span class="sxs-lookup"><span data-stu-id="7198a-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="7198a-116">**EventSource** 名稱**必須**是獨一無二，並應該將預設範本字串 MyCompany-&lt;solution&gt;-&lt;project&gt; 重新命名。</span><span class="sxs-lookup"><span data-stu-id="7198a-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="7198a-117">多個同名的 **EventSource** 定義會導致執行階段發生問題。</span><span class="sxs-lookup"><span data-stu-id="7198a-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="7198a-118">每個已定義事件都必須有獨一無二的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7198a-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="7198a-119">如果識別碼並非獨一無二，會發生執行階段失敗。</span><span class="sxs-lookup"><span data-stu-id="7198a-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="7198a-120">有些組織會預先指派識別碼的值範圍，以避免不同開發小組之間用法不一致。</span><span class="sxs-lookup"><span data-stu-id="7198a-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="7198a-121">如需詳細資訊，請參閱 [Vance 的部落格](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)或 [MSDN 文件](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx)。</span><span class="sxs-lookup"><span data-stu-id="7198a-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="7198a-122">使用結構化 EventSource 事件</span><span class="sxs-lookup"><span data-stu-id="7198a-122">Using structured EventSource events</span></span>

<span data-ttu-id="7198a-123">在本節的程式碼範例中，每個事件都是針對特定案例而定義，例如註冊服務類型。</span><span class="sxs-lookup"><span data-stu-id="7198a-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="7198a-124">當您依使用案例定義訊息時，資料可以和錯誤文字一起封裝，讓您依據指定屬性的名稱或值，更輕鬆地搜尋和篩選。</span><span class="sxs-lookup"><span data-stu-id="7198a-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="7198a-125">建構檢測輸出可讓您更容易取用，但需要更多考量和時間為每個使用案例定義新事件。</span><span class="sxs-lookup"><span data-stu-id="7198a-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="7198a-126">某些事件定義可以在整個應用程式內共用。</span><span class="sxs-lookup"><span data-stu-id="7198a-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="7198a-127">例如，應用程式內的許多不同服務會重複使用方法啟動或停止事件。</span><span class="sxs-lookup"><span data-stu-id="7198a-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="7198a-128">特定網域服務有自己的獨特事件，例如，訂單系統可能有 **CreateOrder** 事件。</span><span class="sxs-lookup"><span data-stu-id="7198a-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="7198a-129">此方法可能產生很多事件，專案小組之間可能需要協調識別碼。</span><span class="sxs-lookup"><span data-stu-id="7198a-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="7198a-130">以一般方式使用 EventSource</span><span class="sxs-lookup"><span data-stu-id="7198a-130">Using EventSource generically</span></span>

<span data-ttu-id="7198a-131">因為定義特定事件可能很困難，許多人會以一組常用的參數定義少量事件，且通常會將資訊輸出為字串。</span><span class="sxs-lookup"><span data-stu-id="7198a-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="7198a-132">大部分的結構層面會遺失，因此更難搜尋和篩選結果。</span><span class="sxs-lookup"><span data-stu-id="7198a-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="7198a-133">此方法定義的少量事件通常對應至記錄層級。</span><span class="sxs-lookup"><span data-stu-id="7198a-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="7198a-134">下列程式碼片段定義偵錯和錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="7198a-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="7198a-135">使用混合式的結構化和泛型檢測也可行。</span><span class="sxs-lookup"><span data-stu-id="7198a-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="7198a-136">結構化檢測用於報告錯誤和計量。</span><span class="sxs-lookup"><span data-stu-id="7198a-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="7198a-137">泛型事件可用來產生詳細記錄，讓工程師用於疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7198a-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="7198a-138">ASP.NET Core 記錄</span><span class="sxs-lookup"><span data-stu-id="7198a-138">ASP.NET Core logging</span></span>

<span data-ttu-id="7198a-139">必須仔細規劃您檢測程式碼的方式。</span><span class="sxs-lookup"><span data-stu-id="7198a-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="7198a-140">正確規劃檢測有助於避免可能使程式碼基底不穩定，導致需要重新檢測程式碼。</span><span class="sxs-lookup"><span data-stu-id="7198a-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="7198a-141">為了降低風險，開發人員可以選擇檢測程式庫，例如 Microsoft ASP.NET Core 中的 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)。</span><span class="sxs-lookup"><span data-stu-id="7198a-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="7198a-142">ASP.NET Core 提供 [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) 介面，可搭配您選擇的提供者一起使用，讓現有程式碼所受的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="7198a-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="7198a-143">您可以在 Windows 和 Linux 上使用 ASP.NET Core 中的程式碼，也可以使用完整 .NET Framework 中的程式碼，使檢測程式碼標準化。</span><span class="sxs-lookup"><span data-stu-id="7198a-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="7198a-144">下方會進一步探討這項資訊：</span><span class="sxs-lookup"><span data-stu-id="7198a-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="7198a-145">使用 Service Fabric 中的 Microsoft.Extensions.Logging</span><span class="sxs-lookup"><span data-stu-id="7198a-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="7198a-146">將 Microsoft.Extensions.Logging NuGet 套件新增至您要檢測的專案。</span><span class="sxs-lookup"><span data-stu-id="7198a-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="7198a-147">另外也新增任何提供者套件 (若是協力廠商套件，請參閱下列範例)。</span><span class="sxs-lookup"><span data-stu-id="7198a-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="7198a-148">如需詳細資訊，請參閱 [ASP.NET Core 中的記錄](https://docs.microsoft.com/aspnet/core/fundamentals/logging)。</span><span class="sxs-lookup"><span data-stu-id="7198a-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="7198a-149">為 Microsoft.Extensions.Logging 將 **using** 指示詞新增至您的服務檔案。</span><span class="sxs-lookup"><span data-stu-id="7198a-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="7198a-150">在服務類別內定義私用變數。</span><span class="sxs-lookup"><span data-stu-id="7198a-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="7198a-151">在服務類別的建構函式中，新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="7198a-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="7198a-152">開始用您的方法檢測程式碼。</span><span class="sxs-lookup"><span data-stu-id="7198a-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="7198a-153">以下是幾個範例：</span><span class="sxs-lookup"><span data-stu-id="7198a-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="7198a-154">使用其他記錄提供者</span><span class="sxs-lookup"><span data-stu-id="7198a-154">Using other logging providers</span></span>

<span data-ttu-id="7198a-155">某些協力廠商提供者會使用上節所述的方法，包括 [Serilog](https://serilog.net/)、[NLog](http://nlog-project.org/) 和 [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging)。</span><span class="sxs-lookup"><span data-stu-id="7198a-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="7198a-156">您可以將這些全部插入 ASP.NET Core 記錄中，也可以分開使用。</span><span class="sxs-lookup"><span data-stu-id="7198a-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="7198a-157">Serilog 有一項功能讓記錄器傳來的所有訊息更豐富。</span><span class="sxs-lookup"><span data-stu-id="7198a-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="7198a-158">這項功能可用來輸出服務名稱、類型和資料分割資訊。</span><span class="sxs-lookup"><span data-stu-id="7198a-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="7198a-159">若要在 ASP.NET Core 基礎結構中使用這項功能，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7198a-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="7198a-160">將 Serilog、Serilog.Extensions.Logging 和 Serilog.Sinks.Observable NuGet 套件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="7198a-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="7198a-161">下一個範例中也新增 Serilog.Sinks.Literate。</span><span class="sxs-lookup"><span data-stu-id="7198a-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="7198a-162">本文稍後會示範更好的方法。</span><span class="sxs-lookup"><span data-stu-id="7198a-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="7198a-163">在 Serilog 中，建立 LoggerConfiguration 和記錄器執行個體。</span><span class="sxs-lookup"><span data-stu-id="7198a-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="7198a-164">將 SeriLog.ILogger 引數新增至服務建構函式，並傳遞新建立的記錄器。</span><span class="sxs-lookup"><span data-stu-id="7198a-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="7198a-165">在服務建構函式中新增下列程式碼，為**ServiceTypeName**、**ServiceName**、**PartitionId** 和 **InstanceId** 等服務屬性建立屬性豐富器。</span><span class="sxs-lookup"><span data-stu-id="7198a-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="7198a-166">它也會將屬性豐富器新增至 ASP.NET Core 記錄工廠，讓您在程式碼中使用 Microsoft.Extensions.Logging.ILogger。</span><span class="sxs-lookup"><span data-stu-id="7198a-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="7198a-167">檢測程式碼，就如同在沒有 SeriLog 的情況下使用 ASP.NET Core 一樣。</span><span class="sxs-lookup"><span data-stu-id="7198a-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="7198a-168">我們建議您不要在上述範例中使用靜態 Log.Logger。</span><span class="sxs-lookup"><span data-stu-id="7198a-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="7198a-169">Service Fabric 可以在單一處理序內裝載相同服務類型的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="7198a-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="7198a-170">如果您使用靜態 Log.Logger，屬性豐富器的最後一個寫入器會顯示所有執行中執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="7198a-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="7198a-171">這是為什麼 _logger 變數是服務類別私人成員變數的其中一個原因。</span><span class="sxs-lookup"><span data-stu-id="7198a-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="7198a-172">此外，您還必須使 _logger 可供各服務可能用到的通用程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="7198a-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="7198a-173">選擇記錄提供者</span><span class="sxs-lookup"><span data-stu-id="7198a-173">Choosing a logging provider</span></span>

<span data-ttu-id="7198a-174">如果您的應用程式仰賴高效能，採用 **EventSource** 通常是不錯的方法。</span><span class="sxs-lookup"><span data-stu-id="7198a-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="7198a-175">**EventSource**「通常」耗用較少資源，效能優於 ASP.NET Core 記錄或任何可用的協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="7198a-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="7198a-176">這對於許多服務而言並不是問題，但如果您的服務屬於效能導向，使用 **EventSource** 可能是更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="7198a-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="7198a-177">不過，採用 **EventSource** 時，工程團隊需要投注大量心力，才能發揮結構化記錄的優勢。</span><span class="sxs-lookup"><span data-stu-id="7198a-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="7198a-178">可能的話，請建構幾個記錄選項的概略雛形，然後選擇最符合需求的方法。</span><span class="sxs-lookup"><span data-stu-id="7198a-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7198a-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7198a-179">Next steps</span></span>

<span data-ttu-id="7198a-180">在您選擇好要用來檢測應用程式和服務的記錄提供者之後，還需要彙總這些記錄和事件，才能將其傳送到任何分析平台。</span><span class="sxs-lookup"><span data-stu-id="7198a-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="7198a-181">請閱讀 [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) 和 [WAD](service-fabric-diagnostics-event-aggregation-wad.md) 以深入了解一些建議的選項。</span><span class="sxs-lookup"><span data-stu-id="7198a-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
