---
title: "使用 Azure Application Insights.NET SDK aaaTrack 自訂作業 |Microsoft 文件"
description: "使用 Azure Application Insights .NET SDK 追蹤自訂作業"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="8888f-103">使用 Application Insights .NET SDK 追蹤自訂作業</span><span class="sxs-lookup"><span data-stu-id="8888f-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="8888f-104">Azure 的 Application Insights Sdk 自動連入 HTTP 要求，並呼叫 toodependent 追蹤服務，，例如 HTTP 要求和 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="8888f-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="8888f-105">追蹤和相互關聯的要求和相依性讓您掌握 hello 整個應用程式的回應速度和可靠性跨所有 microservices 結合此應用程式。</span><span class="sxs-lookup"><span data-stu-id="8888f-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="8888f-106">有一類應用程式模式無法以一般方式支援。</span><span class="sxs-lookup"><span data-stu-id="8888f-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="8888f-107">適當監視這類模式時，需要進行手動程式碼檢測。</span><span class="sxs-lookup"><span data-stu-id="8888f-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="8888f-108">本文涵蓋可能需要手動檢測的一些模式，例如自訂佇列處理和執行長時間執行背景工作。</span><span class="sxs-lookup"><span data-stu-id="8888f-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="8888f-109">本文提供指引 tootrack 自訂作業與 hello Application Insights SDK 的方式。</span><span class="sxs-lookup"><span data-stu-id="8888f-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="8888f-110">本文件相關於：</span><span class="sxs-lookup"><span data-stu-id="8888f-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="8888f-111">適用於 .NET (也稱為 Base SDK) 的 Application Insights 版本 2.4+。</span><span class="sxs-lookup"><span data-stu-id="8888f-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="8888f-112">適用於 Web 應用程式 (執行 ASP.NET) 的 Application Insights 版本 2.4+。</span><span class="sxs-lookup"><span data-stu-id="8888f-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="8888f-113">Application Insights for ASP.NET Core 版本 2.1+。</span><span class="sxs-lookup"><span data-stu-id="8888f-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="8888f-114">概觀</span><span class="sxs-lookup"><span data-stu-id="8888f-114">Overview</span></span>
<span data-ttu-id="8888f-115">作業是應用程式執行的邏輯部分。</span><span class="sxs-lookup"><span data-stu-id="8888f-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="8888f-116">它具有名稱、開始時間、持續時間、結果和執行的內容，例如使用者名稱、屬性和結果。</span><span class="sxs-lookup"><span data-stu-id="8888f-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="8888f-117">如果作業 A 是由作業 B 起始，則作業 B 設為 A 的父代。作業只能有一個父代，但是可以有多個子系作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="8888f-118">如需有關作業和遙測相互關聯的詳細資訊，請參閱 [Azure Application Insights 遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="8888f-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="8888f-119">在 hello Application Insights.NET SDK，hello 作業由 hello 抽象類別來描述[OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs)及其下階[RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs)和[DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="8888f-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="8888f-120">傳入作業追蹤</span><span class="sxs-lookup"><span data-stu-id="8888f-120">Incoming operations tracking</span></span> 
<span data-ttu-id="8888f-121">hello Application Insights web SDK 會自動收集在 IIS 管線中執行的 ASP.NET 應用程式和所有 ASP.NET Core 應用程式的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="8888f-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="8888f-122">其他平台和架構有社群支援的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8888f-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="8888f-123">不過，如果 hello 應用程式不支援任何 hello 標準或社群支援方案，您可以檢測，以手動方式。</span><span class="sxs-lookup"><span data-stu-id="8888f-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="8888f-124">需要自訂追蹤的另一個範例是項目收到 hello 佇列的 hello 背景工作。</span><span class="sxs-lookup"><span data-stu-id="8888f-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="8888f-125">對於某些佇列，hello 呼叫 tooadd toothis 佇列做為相依性追蹤的訊息。</span><span class="sxs-lookup"><span data-stu-id="8888f-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="8888f-126">不過，hello 高層級描述處理訊息的作業才不會自動收集。</span><span class="sxs-lookup"><span data-stu-id="8888f-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="8888f-127">我們來看看要如何追蹤這類作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="8888f-128">在較高的層次，hello 工作是 toocreate`RequestTelemetry`並設定已知的屬性。</span><span class="sxs-lookup"><span data-stu-id="8888f-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="8888f-129">Hello 作業完成之後，您會追蹤 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="8888f-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="8888f-130">hello 下列範例會示範這項工作。</span><span class="sxs-lookup"><span data-stu-id="8888f-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="8888f-131">Owin 自我裝載應用程式中的 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="8888f-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="8888f-132">在此範例中，我們會遵循 hello[相互關聯的 HTTP 通訊協定](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md)。</span><span class="sxs-lookup"><span data-stu-id="8888f-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="8888f-133">您應該會那里說明 tooreceive 標頭。</span><span class="sxs-lookup"><span data-stu-id="8888f-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="8888f-134">hello 相互關聯的 HTTP 通訊協定也會宣告 hello`Correlation-Context`標頭。</span><span class="sxs-lookup"><span data-stu-id="8888f-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="8888f-135">不過，為了簡單起見在這裡省略。</span><span class="sxs-lookup"><span data-stu-id="8888f-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="8888f-136">佇列檢測</span><span class="sxs-lookup"><span data-stu-id="8888f-136">Queue instrumentation</span></span>
<span data-ttu-id="8888f-137">適用於 HTTP 通訊，我們建立了一種通訊協定 toopass 交互關聯詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8888f-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="8888f-138">有些佇列的通訊協定，您可以傳遞其他中繼資料及 hello 訊息，並與其他您不能。</span><span class="sxs-lookup"><span data-stu-id="8888f-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="8888f-139">服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="8888f-139">Service Bus queue</span></span>
<span data-ttu-id="8888f-140">以 hello Azure [Service Bus 佇列](../service-bus-messaging/index.md)，您可以將屬性包，以及 hello 訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="8888f-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="8888f-141">我們使用 toopass hello 相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="8888f-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="8888f-142">hello Service Bus 佇列使用 tcp 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8888f-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="8888f-143">Application Insights 不會自動追蹤佇列作業，所以我們會以手動方式進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="8888f-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="8888f-144">hello 清除佇列作業是推送型 API，而我們目前無法 tootrack 它。</span><span class="sxs-lookup"><span data-stu-id="8888f-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8888f-145">加入佇列</span><span class="sxs-lookup"><span data-stu-id="8888f-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="8888f-146">Process</span><span class="sxs-lookup"><span data-stu-id="8888f-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="8888f-147">Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="8888f-147">Azure Storage queue</span></span>
<span data-ttu-id="8888f-148">下列範例會示範如何 hello tootrack hello [Azure 儲存體佇列](../storage/queues/storage-dotnet-how-to-use-queues.md)作業和 hello 生產者、 hello 消費者和 Azure 儲存體之間的交互關聯遙測。</span><span class="sxs-lookup"><span data-stu-id="8888f-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="8888f-149">hello 儲存體佇列有 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="8888f-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="8888f-150">所有呼叫 toohello 佇列會都追蹤 hello 應用程式 Insights 相依性收集器的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="8888f-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="8888f-151">請確保您在 `applicationInsights.config` 中具有 `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`。</span><span class="sxs-lookup"><span data-stu-id="8888f-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="8888f-152">如果您沒有它，將它加入以程式設計的方式中所述[篩選和 hello Azure Application Insights SDK 中前置處理](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="8888f-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="8888f-153">如果您手動設定 Application Insights，請務必建立並初始化 `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`，類似於：</span><span class="sxs-lookup"><span data-stu-id="8888f-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="8888f-154">您也可能想 toocorrelate hello Application Insights 與 hello 儲存體要求識別碼的作業識別碼</span><span class="sxs-lookup"><span data-stu-id="8888f-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="8888f-155">如需如何 tooset，以及如何取得儲存體要求用戶端和伺服器要求 ID，請參閱[監視、 診斷和疑難排解 Azure 儲存體](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing)。</span><span class="sxs-lookup"><span data-stu-id="8888f-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8888f-156">加入佇列</span><span class="sxs-lookup"><span data-stu-id="8888f-156">Enqueue</span></span>
<span data-ttu-id="8888f-157">因為儲存體佇列支援 hello HTTP API，與 hello 佇列的所有作業會自動都追蹤 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="8888f-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="8888f-158">在許多情況下，此檢測應該就足夠了。</span><span class="sxs-lookup"><span data-stu-id="8888f-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="8888f-159">不過，toocorrelate 追蹤 hello 取用者端產生的追蹤，您必須傳遞一些相互關聯的內容同樣 toohow 我們以進行 hello 相互關聯的 HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8888f-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="8888f-160">在此範例中，我們會追蹤 hello 選擇性`Enqueue`作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="8888f-161">您可以：</span><span class="sxs-lookup"><span data-stu-id="8888f-161">You can:</span></span>

 - <span data-ttu-id="8888f-162">**相互關聯的重試次數 （如果有的話）**： 它們都有一個常見的父代為 hello`Enqueue`作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="8888f-163">否則，會在追蹤做為 hello 連入要求的子系。</span><span class="sxs-lookup"><span data-stu-id="8888f-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="8888f-164">如果有多個邏輯要求 toohello 佇列，可能很難 toofind 哪一個呼叫會導致重試次數。</span><span class="sxs-lookup"><span data-stu-id="8888f-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="8888f-165">**相互關聯儲存體記錄 (必要時)**：與 Application Insights 遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8888f-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="8888f-166">hello`Enqueue`作業是在父作業 （例如，傳入的 HTTP 要求） 的 hello 子系。</span><span class="sxs-lookup"><span data-stu-id="8888f-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="8888f-167">hello HTTP 的相依性呼叫是 hello 子系的 hello `Enqueue` hello 連入要求的作業和 hello 孫系：</span><span class="sxs-lookup"><span data-stu-id="8888f-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="8888f-168">遙測 tooreduce hello 量您的應用程式報告，或者如果您不想 tootrack hello`Enqueue`作業，因為其他原因，使用 hello `Activity` API 直接：</span><span class="sxs-lookup"><span data-stu-id="8888f-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="8888f-169">建立 （和開始） 的新`Activity`而不是 hello Application Insights 作業開始。</span><span class="sxs-lookup"><span data-stu-id="8888f-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="8888f-170">您執行*不*需要 tooassign 上面 hello 作業名稱以外的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="8888f-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="8888f-171">序列化`yourActivity.Id`hello 訊息承載，而不是`operation.Telemetry.Id`。</span><span class="sxs-lookup"><span data-stu-id="8888f-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="8888f-172">您也可以使用 `Activity.Current.Id`。</span><span class="sxs-lookup"><span data-stu-id="8888f-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="8888f-173">清除佇列</span><span class="sxs-lookup"><span data-stu-id="8888f-173">Dequeue</span></span>
<span data-ttu-id="8888f-174">同樣地太`Enqueue`，Application Insights 自動追蹤實際 HTTP 要求 toohello 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="8888f-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="8888f-175">不過，hello`Enqueue`作業可能會發生在 hello 父內容，例如內送的要求內容。</span><span class="sxs-lookup"><span data-stu-id="8888f-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="8888f-176">Application Insights Sdk 會自動關聯這類作業 （和其 HTTP 部分） 與 hello 父要求與其他遙測中回報 hello 相同範圍內。</span><span class="sxs-lookup"><span data-stu-id="8888f-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="8888f-177">hello`Dequeue`作業是很難解釋。</span><span class="sxs-lookup"><span data-stu-id="8888f-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="8888f-178">hello Application Insights SDK 會自動追蹤 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="8888f-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="8888f-179">不過，它並不知道 hello 相互關聯的內容會剖析 hello 訊息之前。</span><span class="sxs-lookup"><span data-stu-id="8888f-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="8888f-180">不可能 toocorrelate hello HTTP 要求 tooget hello 訊息與 hello 遙測 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="8888f-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="8888f-181">在許多情況下，可能很有用 toocorrelate hello HTTP 要求 toohello 佇列以及其他的追蹤。</span><span class="sxs-lookup"><span data-stu-id="8888f-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="8888f-182">hello 下列範例會示範如何 toodo 它：</span><span class="sxs-lookup"><span data-stu-id="8888f-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="8888f-183">Process</span><span class="sxs-lookup"><span data-stu-id="8888f-183">Process</span></span>

<span data-ttu-id="8888f-184">在下列範例的 hello，我們會追蹤內送訊息的方式類似 toohow 我們追蹤連入 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="8888f-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="8888f-185">同樣地，可能會檢測其他佇列作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="8888f-186">預覽 (Peek) 作業應以類似清除佇列作業的方式進行檢測。</span><span class="sxs-lookup"><span data-stu-id="8888f-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="8888f-187">不一定要檢測佇列管理作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="8888f-188">Application Insights 會追蹤 HTTP 這類作業，這在大多數情況下已足夠。</span><span class="sxs-lookup"><span data-stu-id="8888f-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="8888f-189">當您檢測刪除郵件時，請確定設定 hello 作業 （相互關聯） 的識別項。</span><span class="sxs-lookup"><span data-stu-id="8888f-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="8888f-190">或者，您可以使用 hello`Activity`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8888f-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="8888f-191">然後您不需要 tooset hello 遙測項目上的作業識別碼，因為 Application Insights 為您做：</span><span class="sxs-lookup"><span data-stu-id="8888f-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="8888f-192">建立新`Activity`你 hello 佇列的項目之後。</span><span class="sxs-lookup"><span data-stu-id="8888f-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="8888f-193">使用`Activity.SetParentId(message.ParentId)`toocorrelate 取用者和產生者記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8888f-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="8888f-194">啟動 hello `Activity`。</span><span class="sxs-lookup"><span data-stu-id="8888f-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="8888f-195">使用 `Start/StopOperation` 協助程式追蹤清除佇列、處理和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="8888f-196">執行從 hello 相同非同步控制流程 （執行內容）。</span><span class="sxs-lookup"><span data-stu-id="8888f-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="8888f-197">如此一來，這些作業就會正確地相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8888f-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="8888f-198">停止 hello `Activity`。</span><span class="sxs-lookup"><span data-stu-id="8888f-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="8888f-199">使用 `Start/StopOperation` 或手動呼叫 `Track` 遙測。</span><span class="sxs-lookup"><span data-stu-id="8888f-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="8888f-200">批次處理</span><span class="sxs-lookup"><span data-stu-id="8888f-200">Batch processing</span></span>
<span data-ttu-id="8888f-201">有些佇列中，您可以使用一個要求清除佇列多個訊息。</span><span class="sxs-lookup"><span data-stu-id="8888f-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="8888f-202">處理此類訊息會假定無關，並且所屬 toohello 不同的邏輯作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="8888f-203">在此情況下，它不可能 toocorrelate hello`Dequeue`作業 tooparticular 訊息處理。</span><span class="sxs-lookup"><span data-stu-id="8888f-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="8888f-204">每個訊息應該在自己的非同步控制流程中處理。</span><span class="sxs-lookup"><span data-stu-id="8888f-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="8888f-205">如需詳細資訊，請參閱 hello[連出相依性追蹤](#outgoing-dependencies-tracking)> 一節。</span><span class="sxs-lookup"><span data-stu-id="8888f-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="8888f-206">長時間執行的背景工作</span><span class="sxs-lookup"><span data-stu-id="8888f-206">Long-running background tasks</span></span>
<span data-ttu-id="8888f-207">有些應用程式可能會應使用者要求，啟動長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="8888f-208">Hello 追蹤/檢測的觀點而言，不要求或相依性的檢測不同：</span><span class="sxs-lookup"><span data-stu-id="8888f-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="8888f-209">在此範例中，我們使用`telemetryClient.StartOperation`toocreate`RequestTelemetry`和填滿 hello 相互關聯的內容。</span><span class="sxs-lookup"><span data-stu-id="8888f-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="8888f-210">例如，假設您有在父作業所建立的排程 hello 作業的傳入要求。</span><span class="sxs-lookup"><span data-stu-id="8888f-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="8888f-211">只要`BackgroundTask`開始在 hello 與傳入的要求相同的非同步控制流程，該父作業相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8888f-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="8888f-212">`BackgroundTask`和所有的巢狀的遙測項目都與 hello 要求造成它，即使在 hello 要求結束之後自動相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8888f-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="8888f-213">當 hello 工作可啟動從 hello 背景執行緒沒有任何作業 (`Activity`) 相關聯，`BackgroundTask`沒有任何父項。</span><span class="sxs-lookup"><span data-stu-id="8888f-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="8888f-214">不過，它可以有巢狀作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-214">However, it can have nested operations.</span></span> <span data-ttu-id="8888f-215">從 hello 工作回報的所有遙測項目都是相互關聯的 toohello`RequestTelemetry`中建立`BackgroundTask`。</span><span class="sxs-lookup"><span data-stu-id="8888f-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="8888f-216">連出相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="8888f-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="8888f-217">您可以追蹤自己的相依性種類或 Application Insights 不支援的作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="8888f-218">hello `Enqueue` hello 服務匯流排佇列或 hello 儲存體佇列中的方法可以做為這類自訂追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="8888f-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="8888f-219">自訂相依性追蹤的 hello 一般方法是：</span><span class="sxs-lookup"><span data-stu-id="8888f-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="8888f-220">呼叫 hello `TelemetryClient.StartOperation` （擴充） 方法用來填滿 hello`DependencyTelemetry`所需的相互關聯與其他屬性的內容 (開始時間戳記，持續時間)。</span><span class="sxs-lookup"><span data-stu-id="8888f-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="8888f-221">設定其他自訂的屬性上 hello `DependencyTelemetry`，例如 hello 名稱和您需要的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="8888f-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="8888f-222">進行相依性呼叫並且等候。</span><span class="sxs-lookup"><span data-stu-id="8888f-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="8888f-223">停止與 hello 作業`StopOperation`完成時。</span><span class="sxs-lookup"><span data-stu-id="8888f-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="8888f-224">處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8888f-224">Handle exceptions.</span></span>

<span data-ttu-id="8888f-225">`StopOperation`只會停止啟動 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="8888f-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="8888f-226">如果 hello 目前執行的作業不符合 hello 其中一個要 toostop，`StopOperation`不做任何動作。</span><span class="sxs-lookup"><span data-stu-id="8888f-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="8888f-227">如果您以平行方式在 hello 中啟動多項作業，這種情況可能會發生相同的執行內容：</span><span class="sxs-lookup"><span data-stu-id="8888f-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="8888f-228">請確定一律呼叫 `StartOperation` 並在其自己的內容中執行您的工作：</span><span class="sxs-lookup"><span data-stu-id="8888f-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8888f-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8888f-229">Next steps</span></span>

- <span data-ttu-id="8888f-230">了解 hello 基本概念的[遙測相互關聯](application-insights-correlation.md)Application Insights 中。</span><span class="sxs-lookup"><span data-stu-id="8888f-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="8888f-231">請參閱 hello[資料模型](application-insights-data-model.md)Application Insights 的類型和資料模型。</span><span class="sxs-lookup"><span data-stu-id="8888f-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8888f-232">報告自訂[事件和度量](app-insights-api-custom-events-metrics.md)tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="8888f-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="8888f-233">請查看內容屬性集合的標準[設定](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。</span><span class="sxs-lookup"><span data-stu-id="8888f-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="8888f-234">檢查 hello [System.Diagnostics.Activity 使用者指南](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)toosee 我們相互遙測的關聯。</span><span class="sxs-lookup"><span data-stu-id="8888f-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
