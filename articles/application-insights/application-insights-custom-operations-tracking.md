---
title: "使用 Azure Application Insights .NET SDK 追蹤自訂作業 | Microsoft Docs"
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
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="fc715-103">使用 Application Insights .NET SDK 追蹤自訂作業</span><span class="sxs-lookup"><span data-stu-id="fc715-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="fc715-104">Azure Application Insights SDK 會自動追蹤相依服務的連入 HTTP 要求和呼叫，例如 HTTP 要求、SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="fc715-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="fc715-105">追蹤和相互關聯要求與相依性，可讓您深入了解橫跨所有微服務 (合併此應用程式) 的整體應用程式回應能力和可靠性。</span><span class="sxs-lookup"><span data-stu-id="fc715-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="fc715-106">有一類應用程式模式無法以一般方式支援。</span><span class="sxs-lookup"><span data-stu-id="fc715-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="fc715-107">適當監視這類模式時，需要進行手動程式碼檢測。</span><span class="sxs-lookup"><span data-stu-id="fc715-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="fc715-108">本文涵蓋可能需要手動檢測的一些模式，例如自訂佇列處理和執行長時間執行背景工作。</span><span class="sxs-lookup"><span data-stu-id="fc715-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="fc715-109">本文提供有關如何使用 ApplicationInsights SDK 追蹤自訂作業的指引。</span><span class="sxs-lookup"><span data-stu-id="fc715-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="fc715-110">本文件相關於：</span><span class="sxs-lookup"><span data-stu-id="fc715-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="fc715-111">適用於 .NET (也稱為 Base SDK) 的 Application Insights 版本 2.4+。</span><span class="sxs-lookup"><span data-stu-id="fc715-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="fc715-112">適用於 Web 應用程式 (執行 ASP.NET) 的 Application Insights 版本 2.4+。</span><span class="sxs-lookup"><span data-stu-id="fc715-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="fc715-113">Application Insights for ASP.NET Core 版本 2.1+。</span><span class="sxs-lookup"><span data-stu-id="fc715-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="fc715-114">概觀</span><span class="sxs-lookup"><span data-stu-id="fc715-114">Overview</span></span>
<span data-ttu-id="fc715-115">作業是應用程式執行的邏輯部分。</span><span class="sxs-lookup"><span data-stu-id="fc715-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="fc715-116">它具有名稱、開始時間、持續時間、結果和執行的內容，例如使用者名稱、屬性和結果。</span><span class="sxs-lookup"><span data-stu-id="fc715-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="fc715-117">如果作業 A 是由作業 B 起始，則作業 B 設為 A 的父代。作業只能有一個父代，但是可以有多個子系作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="fc715-118">如需有關作業和遙測相互關聯的詳細資訊，請參閱 [Azure Application Insights 遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="fc715-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="fc715-119">在 Application Insights.NET SDK 中，作業是由抽象類別 [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) 及其子系 [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) 和 [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs) 描述。</span><span class="sxs-lookup"><span data-stu-id="fc715-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="fc715-120">傳入作業追蹤</span><span class="sxs-lookup"><span data-stu-id="fc715-120">Incoming operations tracking</span></span> 
<span data-ttu-id="fc715-121">Application Insights Wb SDK 會針對在 IIS 管線中執行的 ASP.NET 應用程式和所有的 ASP.NET Core 應用程式，自動收集 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="fc715-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="fc715-122">其他平台和架構有社群支援的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fc715-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="fc715-123">不過，如果任何標準或社群支援的解決方案不支援應用程式，您可以用手動方式進行檢測。</span><span class="sxs-lookup"><span data-stu-id="fc715-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="fc715-124">接收佇列中項目的背景工作是另一個需要自訂追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="fc715-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="fc715-125">對於某些佇列，將訊息新增至此佇列的呼叫會作為相依性追蹤。</span><span class="sxs-lookup"><span data-stu-id="fc715-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="fc715-126">但是，不會自動收集描述處理訊息的高階作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="fc715-127">我們來看看要如何追蹤這類作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="fc715-128">在較高的層級中，工作是建立 `RequestTelemetry` 並且設定已知的屬性。</span><span class="sxs-lookup"><span data-stu-id="fc715-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="fc715-129">作業完成之後，您會追蹤遙測。</span><span class="sxs-lookup"><span data-stu-id="fc715-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="fc715-130">下列範例示範此工作。</span><span class="sxs-lookup"><span data-stu-id="fc715-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="fc715-131">Owin 自我裝載應用程式中的 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="fc715-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="fc715-132">在此範例中，我們遵循[相互關聯的 HTTP 通訊協定](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md)。</span><span class="sxs-lookup"><span data-stu-id="fc715-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="fc715-133">您應該預期會收到該處所述的標題。</span><span class="sxs-lookup"><span data-stu-id="fc715-133">You should expect to receive headers that are described there.</span></span>

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

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
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

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="fc715-134">相互關聯的 HTTP 通訊協定也會宣告 `Correlation-Context` 標題。</span><span class="sxs-lookup"><span data-stu-id="fc715-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="fc715-135">不過，為了簡單起見在這裡省略。</span><span class="sxs-lookup"><span data-stu-id="fc715-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="fc715-136">佇列檢測</span><span class="sxs-lookup"><span data-stu-id="fc715-136">Queue instrumentation</span></span>
<span data-ttu-id="fc715-137">對於 HTTP 通訊，我們建立了可傳遞相互關聯詳細資料的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="fc715-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="fc715-138">有些佇列通訊協定允許您將其他中繼資料隨著訊息一起傳遞，有些則不允許。</span><span class="sxs-lookup"><span data-stu-id="fc715-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="fc715-139">服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="fc715-139">Service Bus queue</span></span>
<span data-ttu-id="fc715-140">您可以使用 Azure [服務匯流排佇列](../service-bus-messaging/index.md)，將屬性包隨著訊息一起傳遞。</span><span class="sxs-lookup"><span data-stu-id="fc715-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="fc715-141">我們使用它來傳遞相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc715-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="fc715-142">服務匯流排佇列會使用以 TCP 為基礎的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="fc715-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="fc715-143">Application Insights 不會自動追蹤佇列作業，所以我們會以手動方式進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="fc715-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="fc715-144">清除佇列作業是推送型 API，無法完全加以追蹤。</span><span class="sxs-lookup"><span data-stu-id="fc715-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="fc715-145">加入佇列</span><span class="sxs-lookup"><span data-stu-id="fc715-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
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

#### <a name="process"></a><span data-ttu-id="fc715-146">Process</span><span class="sxs-lookup"><span data-stu-id="fc715-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="fc715-147">Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="fc715-147">Azure Storage queue</span></span>
<span data-ttu-id="fc715-148">下列範例示範如何追蹤 [Azure 儲存體佇列](../storage/queues/storage-dotnet-how-to-use-queues.md)作業，並且讓產生者、取用者與 Azure 儲存體之間的遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="fc715-149">儲存體佇列有 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="fc715-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="fc715-150">HTTP 要求的 Application Insights 相依性收集器會追蹤對佇列的所有呼叫。</span><span class="sxs-lookup"><span data-stu-id="fc715-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="fc715-151">請確保您在 `applicationInsights.config` 中具有 `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`。</span><span class="sxs-lookup"><span data-stu-id="fc715-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="fc715-152">如果沒有，請如同[在 Azure Application Insights SDK 中篩選和前置處理](app-insights-api-filtering-sampling.md)所述，以程式設計方式新增它。</span><span class="sxs-lookup"><span data-stu-id="fc715-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="fc715-153">如果您手動設定 Application Insights，請務必建立並初始化 `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`，類似於：</span><span class="sxs-lookup"><span data-stu-id="fc715-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="fc715-154">您可能也想要相互關聯 Application Insights 作業識別碼與儲存體要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc715-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="fc715-155">如需如何設定及取得儲存體要求用戶端和伺服器要求識別碼的詳細資訊，請參閱[監視、診斷 Azure 儲存體及進行移難排解](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing)。</span><span class="sxs-lookup"><span data-stu-id="fc715-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="fc715-156">加入佇列</span><span class="sxs-lookup"><span data-stu-id="fc715-156">Enqueue</span></span>
<span data-ttu-id="fc715-157">因為 Azure 儲存體佇列支援 HTTP API，Application Insights 會自動追蹤所有作業與佇列。</span><span class="sxs-lookup"><span data-stu-id="fc715-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="fc715-158">在許多情況下，此檢測應該就足夠了。</span><span class="sxs-lookup"><span data-stu-id="fc715-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="fc715-159">不過，若要讓取用者端追蹤與生產者追蹤相互關聯，您必須傳遞一些相互關聯內容，類似於我們在「相互關聯的 HTTP 通訊協定」中的作業方式。</span><span class="sxs-lookup"><span data-stu-id="fc715-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="fc715-160">在此範例中，我們追蹤選擇性 `Enqueue` 作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="fc715-161">您可以：</span><span class="sxs-lookup"><span data-stu-id="fc715-161">You can:</span></span>

 - <span data-ttu-id="fc715-162">**相互關聯重試 (如果有的話)**：全部都有一個通用父代，也就是 `Enqueue` 作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="fc715-163">否則會作為連入要求的子系追蹤。</span><span class="sxs-lookup"><span data-stu-id="fc715-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="fc715-164">如果佇列有多個邏輯要求，可能難以找到導致重試的呼叫。</span><span class="sxs-lookup"><span data-stu-id="fc715-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="fc715-165">**相互關聯儲存體記錄 (必要時)**：與 Application Insights 遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="fc715-166">`Enqueue` 作業是父代作業 (例如，連入 HTTP 要求) 的子系。</span><span class="sxs-lookup"><span data-stu-id="fc715-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="fc715-167">HTTP 相依性呼叫是 `Enqueue` 作業的子系，是連入要求的孫系：</span><span class="sxs-lookup"><span data-stu-id="fc715-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="fc715-168">如果您因為其他原因，而想要減少您應用程式回報的遙測資料量，或不想追蹤 `Enqueue` 作業，您可以直接使用 `Activity` API：</span><span class="sxs-lookup"><span data-stu-id="fc715-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="fc715-169">建立 (和啟動) 新的 `Activity`，而不是啟動 Application Insights 作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="fc715-170">您不需要在上面指派作業名稱以外的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="fc715-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="fc715-171">將 `yourActivity.Id` 序列化成為訊息承載，而不是 `operation.Telemetry.Id`。</span><span class="sxs-lookup"><span data-stu-id="fc715-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="fc715-172">您也可以使用 `Activity.Current.Id`。</span><span class="sxs-lookup"><span data-stu-id="fc715-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="fc715-173">清除佇列</span><span class="sxs-lookup"><span data-stu-id="fc715-173">Dequeue</span></span>
<span data-ttu-id="fc715-174">類似於 `Enqueue`，Application Insights 會自動追蹤儲存體佇列的實際 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="fc715-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="fc715-175">不過 `Enqueue` 作業可能發生於父代內容，例如連入要求內容。</span><span class="sxs-lookup"><span data-stu-id="fc715-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="fc715-176">Application Insights SDK 會使這類作業 (及其 HTTP 部分) 與父代要求和相同範圍中報告的其他遙測自動相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="fc715-177">`Dequeue` 作業有些麻煩。</span><span class="sxs-lookup"><span data-stu-id="fc715-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="fc715-178">Application Insights SDK 會自動追蹤 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="fc715-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="fc715-179">不過，它在剖析訊息之前並不知道相互關聯內容。</span><span class="sxs-lookup"><span data-stu-id="fc715-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="fc715-180">不可能相互關聯 HTTP 要求來取得包含遙測其餘部分的訊息。</span><span class="sxs-lookup"><span data-stu-id="fc715-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="fc715-181">在許多情況下，將佇列的 HTTP 要求與其他追蹤相互關聯也很有用。</span><span class="sxs-lookup"><span data-stu-id="fc715-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="fc715-182">下列範例提供如何執行的示範：</span><span class="sxs-lookup"><span data-stu-id="fc715-182">The following example demonstrates how to do it:</span></span>

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

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
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

#### <a name="process"></a><span data-ttu-id="fc715-183">Process</span><span class="sxs-lookup"><span data-stu-id="fc715-183">Process</span></span>

<span data-ttu-id="fc715-184">在下列範例中，我們追蹤連入訊息的方式類似於我們追蹤連入 HTTP 要求的方式：</span><span class="sxs-lookup"><span data-stu-id="fc715-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
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

<span data-ttu-id="fc715-185">同樣地，可能會檢測其他佇列作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="fc715-186">預覽 (Peek) 作業應以類似清除佇列作業的方式進行檢測。</span><span class="sxs-lookup"><span data-stu-id="fc715-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="fc715-187">不一定要檢測佇列管理作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="fc715-188">Application Insights 會追蹤 HTTP 這類作業，這在大多數情況下已足夠。</span><span class="sxs-lookup"><span data-stu-id="fc715-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="fc715-189">檢測訊息刪除時，請務必設定作業 (相互關聯) 識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc715-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="fc715-190">或者，您可使用 `Activity` API。</span><span class="sxs-lookup"><span data-stu-id="fc715-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="fc715-191">您就不需要在遙測項目上設定作業識別碼，因為 Application Insights 會為您設定：</span><span class="sxs-lookup"><span data-stu-id="fc715-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="fc715-192">取得佇列中的項目後，建立新的 `Activity`。</span><span class="sxs-lookup"><span data-stu-id="fc715-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="fc715-193">使用 `Activity.SetParentId(message.ParentId)` 讓取用者和產生者記錄相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="fc715-194">啟動 `Activity`。</span><span class="sxs-lookup"><span data-stu-id="fc715-194">Start the `Activity`.</span></span>
- <span data-ttu-id="fc715-195">使用 `Start/StopOperation` 協助程式追蹤清除佇列、處理和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="fc715-196">從相同的非同步控制流程 (執行內容) 執行此作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="fc715-197">如此一來，這些作業就會正確地相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="fc715-198">停止 `Activity`。</span><span class="sxs-lookup"><span data-stu-id="fc715-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="fc715-199">使用 `Start/StopOperation` 或手動呼叫 `Track` 遙測。</span><span class="sxs-lookup"><span data-stu-id="fc715-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="fc715-200">批次處理</span><span class="sxs-lookup"><span data-stu-id="fc715-200">Batch processing</span></span>
<span data-ttu-id="fc715-201">有些佇列中，您可以使用一個要求清除佇列多個訊息。</span><span class="sxs-lookup"><span data-stu-id="fc715-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="fc715-202">處理這類訊息可能是獨立的，並且屬於不同的邏輯作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="fc715-203">在此情況下，不可能使 `Dequeue` 作業與特定訊息處理相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="fc715-204">每個訊息應該在自己的非同步控制流程中處理。</span><span class="sxs-lookup"><span data-stu-id="fc715-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="fc715-205">如需詳細資訊，請參閱[連出相依性追蹤](#outgoing-dependencies-tracking)一節。</span><span class="sxs-lookup"><span data-stu-id="fc715-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="fc715-206">長時間執行的背景工作</span><span class="sxs-lookup"><span data-stu-id="fc715-206">Long-running background tasks</span></span>
<span data-ttu-id="fc715-207">有些應用程式可能會應使用者要求，啟動長時間執行的作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="fc715-208">就追蹤/檢測觀點而言，這與要求或相依性檢測並無不同：</span><span class="sxs-lookup"><span data-stu-id="fc715-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process the task.
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

<span data-ttu-id="fc715-209">在此範例中，我們使用 `telemetryClient.StartOperation` 來建立 `RequestTelemetry` 和填滿相互關聯內容。</span><span class="sxs-lookup"><span data-stu-id="fc715-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="fc715-210">假設您有一項父代作業，由排程作業的連入要求所建立。</span><span class="sxs-lookup"><span data-stu-id="fc715-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="fc715-211">只要 `BackgroundTask` 在與連入要求相同的非同步控制流程中啟動，它就會與該父代作業相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="fc715-212">`BackgroundTask` 和所有巢狀遙測項目將會自動與造成它的要求相互關聯，即使在要求結束後亦然。</span><span class="sxs-lookup"><span data-stu-id="fc715-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="fc715-213">從沒有任何相關聯作業 (`Activity`) 的背景執行緒啟動工作時，`BackgroundTask` 沒有任何父代。</span><span class="sxs-lookup"><span data-stu-id="fc715-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="fc715-214">不過，它可以有巢狀作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-214">However, it can have nested operations.</span></span> <span data-ttu-id="fc715-215">工作回報的所有遙測項目會與在 `BackgroundTask` 中建立的 `RequestTelemetry` 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="fc715-216">連出相依性追蹤</span><span class="sxs-lookup"><span data-stu-id="fc715-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="fc715-217">您可以追蹤自己的相依性種類或 Application Insights 不支援的作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="fc715-218">服務匯流排佇列或儲存體佇列中的 `Enqueue` 方法可作為這類自訂追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="fc715-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="fc715-219">自訂相依性追蹤的一般方法如下：</span><span class="sxs-lookup"><span data-stu-id="fc715-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="fc715-220">呼叫 `TelemetryClient.StartOperation` (擴充) 方法，以填滿相互關聯所需的 `DependencyTelemetry` 屬性和其他一些屬性 (開始時間戳記、持續時間)。</span><span class="sxs-lookup"><span data-stu-id="fc715-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="fc715-221">在 `DependencyTelemetry` 上設定其他自訂屬性，例如名稱與您需要的任何其他內容。</span><span class="sxs-lookup"><span data-stu-id="fc715-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="fc715-222">進行相依性呼叫並且等候。</span><span class="sxs-lookup"><span data-stu-id="fc715-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="fc715-223">完成時使用 `StopOperation` 停止作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="fc715-224">處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="fc715-224">Handle exceptions.</span></span>

<span data-ttu-id="fc715-225">`StopOperation` 只會停止已啟動的作業。</span><span class="sxs-lookup"><span data-stu-id="fc715-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="fc715-226">如果目前執行中作業不符合您想要停止的作業，則 `StopOperation` 不會有任何動作。</span><span class="sxs-lookup"><span data-stu-id="fc715-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="fc715-227">如果您以平行方式在相同的執行內容中啟動多項作業，可能會發生這種情形：</span><span class="sxs-lookup"><span data-stu-id="fc715-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="fc715-228">請確定一律呼叫 `StartOperation` 並在其自己的內容中執行您的工作：</span><span class="sxs-lookup"><span data-stu-id="fc715-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="fc715-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc715-229">Next steps</span></span>

- <span data-ttu-id="fc715-230">了解 Application Insights 中[遙測相互關聯](application-insights-correlation.md)的基本概念。</span><span class="sxs-lookup"><span data-stu-id="fc715-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="fc715-231">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="fc715-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="fc715-232">向 Application Insights 報告自訂[事件和計量](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="fc715-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="fc715-233">請查看內容屬性集合的標準[設定](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。</span><span class="sxs-lookup"><span data-stu-id="fc715-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="fc715-234">查看 [System.Diagnostics.Activity 使用者指南](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)以了解如何使遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fc715-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
