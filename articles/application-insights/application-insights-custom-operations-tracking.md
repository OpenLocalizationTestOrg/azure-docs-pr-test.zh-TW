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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>使用 Application Insights .NET SDK 追蹤自訂作業

Azure 的 Application Insights Sdk 自動連入 HTTP 要求，並呼叫 toodependent 追蹤服務，，例如 HTTP 要求和 SQL 查詢。 追蹤和相互關聯的要求和相依性讓您掌握 hello 整個應用程式的回應速度和可靠性跨所有 microservices 結合此應用程式。 

有一類應用程式模式無法以一般方式支援。 適當監視這類模式時，需要進行手動程式碼檢測。 本文涵蓋可能需要手動檢測的一些模式，例如自訂佇列處理和執行長時間執行背景工作。

本文提供指引 tootrack 自訂作業與 hello Application Insights SDK 的方式。 本文件相關於：

- 適用於 .NET (也稱為 Base SDK) 的 Application Insights 版本 2.4+。
- 適用於 Web 應用程式 (執行 ASP.NET) 的 Application Insights 版本 2.4+。
- Application Insights for ASP.NET Core 版本 2.1+。

## <a name="overview"></a>概觀
作業是應用程式執行的邏輯部分。 它具有名稱、開始時間、持續時間、結果和執行的內容，例如使用者名稱、屬性和結果。 如果作業 A 是由作業 B 起始，則作業 B 設為 A 的父代。作業只能有一個父代，但是可以有多個子系作業。 如需有關作業和遙測相互關聯的詳細資訊，請參閱 [Azure Application Insights 遙測相互關聯](application-insights-correlation.md)。

在 hello Application Insights.NET SDK，hello 作業由 hello 抽象類別來描述[OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs)及其下階[RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs)和[DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>傳入作業追蹤 
hello Application Insights web SDK 會自動收集在 IIS 管線中執行的 ASP.NET 應用程式和所有 ASP.NET Core 應用程式的 HTTP 要求。 其他平台和架構有社群支援的解決方案。 不過，如果 hello 應用程式不支援任何 hello 標準或社群支援方案，您可以檢測，以手動方式。

需要自訂追蹤的另一個範例是項目收到 hello 佇列的 hello 背景工作。 對於某些佇列，hello 呼叫 tooadd toothis 佇列做為相依性追蹤的訊息。 不過，hello 高層級描述處理訊息的作業才不會自動收集。

我們來看看要如何追蹤這類作業。

在較高的層次，hello 工作是 toocreate`RequestTelemetry`並設定已知的屬性。 Hello 作業完成之後，您會追蹤 hello 遙測。 hello 下列範例會示範這項工作。

### <a name="http-request-in-owin-self-hosted-app"></a>Owin 自我裝載應用程式中的 HTTP 要求
在此範例中，我們會遵循 hello[相互關聯的 HTTP 通訊協定](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md)。 您應該會那里說明 tooreceive 標頭。

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

hello 相互關聯的 HTTP 通訊協定也會宣告 hello`Correlation-Context`標頭。 不過，為了簡單起見在這裡省略。

## <a name="queue-instrumentation"></a>佇列檢測
適用於 HTTP 通訊，我們建立了一種通訊協定 toopass 交互關聯詳細資料。 有些佇列的通訊協定，您可以傳遞其他中繼資料及 hello 訊息，並與其他您不能。

### <a name="service-bus-queue"></a>服務匯流排佇列
以 hello Azure [Service Bus 佇列](../service-bus-messaging/index.md)，您可以將屬性包，以及 hello 訊息傳遞。 我們使用 toopass hello 相互關聯識別碼。

hello Service Bus 佇列使用 tcp 通訊協定。 Application Insights 不會自動追蹤佇列作業，所以我們會以手動方式進行追蹤。 hello 清除佇列作業是推送型 API，而我們目前無法 tootrack 它。

#### <a name="enqueue"></a>加入佇列

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

#### <a name="process"></a>Process
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

### <a name="azure-storage-queue"></a>Azure 儲存體佇列
下列範例會示範如何 hello tootrack hello [Azure 儲存體佇列](../storage/queues/storage-dotnet-how-to-use-queues.md)作業和 hello 生產者、 hello 消費者和 Azure 儲存體之間的交互關聯遙測。 

hello 儲存體佇列有 HTTP API。 所有呼叫 toohello 佇列會都追蹤 hello 應用程式 Insights 相依性收集器的 HTTP 要求。
請確保您在 `applicationInsights.config` 中具有 `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`。 如果您沒有它，將它加入以程式設計的方式中所述[篩選和 hello Azure Application Insights SDK 中前置處理](app-insights-api-filtering-sampling.md)。

如果您手動設定 Application Insights，請務必建立並初始化 `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`，類似於：
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

您也可能想 toocorrelate hello Application Insights 與 hello 儲存體要求識別碼的作業識別碼 如需如何 tooset，以及如何取得儲存體要求用戶端和伺服器要求 ID，請參閱[監視、 診斷和疑難排解 Azure 儲存體](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing)。

#### <a name="enqueue"></a>加入佇列
因為儲存體佇列支援 hello HTTP API，與 hello 佇列的所有作業會自動都追蹤 Application Insights。 在許多情況下，此檢測應該就足夠了。 不過，toocorrelate 追蹤 hello 取用者端產生的追蹤，您必須傳遞一些相互關聯的內容同樣 toohow 我們以進行 hello 相互關聯的 HTTP 通訊協定。 

在此範例中，我們會追蹤 hello 選擇性`Enqueue`作業。 您可以：

 - **相互關聯的重試次數 （如果有的話）**： 它們都有一個常見的父代為 hello`Enqueue`作業。 否則，會在追蹤做為 hello 連入要求的子系。 如果有多個邏輯要求 toohello 佇列，可能很難 toofind 哪一個呼叫會導致重試次數。
 - **相互關聯儲存體記錄 (必要時)**：與 Application Insights 遙測相互關聯。

hello`Enqueue`作業是在父作業 （例如，傳入的 HTTP 要求） 的 hello 子系。 hello HTTP 的相依性呼叫是 hello 子系的 hello `Enqueue` hello 連入要求的作業和 hello 孫系：

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

遙測 tooreduce hello 量您的應用程式報告，或者如果您不想 tootrack hello`Enqueue`作業，因為其他原因，使用 hello `Activity` API 直接：

- 建立 （和開始） 的新`Activity`而不是 hello Application Insights 作業開始。 您執行*不*需要 tooassign 上面 hello 作業名稱以外的任何屬性。
- 序列化`yourActivity.Id`hello 訊息承載，而不是`operation.Telemetry.Id`。 您也可以使用 `Activity.Current.Id`。


#### <a name="dequeue"></a>清除佇列
同樣地太`Enqueue`，Application Insights 自動追蹤實際 HTTP 要求 toohello 儲存體佇列。 不過，hello`Enqueue`作業可能會發生在 hello 父內容，例如內送的要求內容。 Application Insights Sdk 會自動關聯這類作業 （和其 HTTP 部分） 與 hello 父要求與其他遙測中回報 hello 相同範圍內。

hello`Dequeue`作業是很難解釋。 hello Application Insights SDK 會自動追蹤 HTTP 要求。 不過，它並不知道 hello 相互關聯的內容會剖析 hello 訊息之前。 不可能 toocorrelate hello HTTP 要求 tooget hello 訊息與 hello 遙測 hello 其餘部分。

在許多情況下，可能很有用 toocorrelate hello HTTP 要求 toohello 佇列以及其他的追蹤。 hello 下列範例會示範如何 toodo 它：

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

#### <a name="process"></a>Process

在下列範例的 hello，我們會追蹤內送訊息的方式類似 toohow 我們追蹤連入 HTTP 要求：

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

同樣地，可能會檢測其他佇列作業。 預覽 (Peek) 作業應以類似清除佇列作業的方式進行檢測。 不一定要檢測佇列管理作業。 Application Insights 會追蹤 HTTP 這類作業，這在大多數情況下已足夠。

當您檢測刪除郵件時，請確定設定 hello 作業 （相互關聯） 的識別項。 或者，您可以使用 hello`Activity`應用程式開發介面。 然後您不需要 tooset hello 遙測項目上的作業識別碼，因為 Application Insights 為您做：

- 建立新`Activity`你 hello 佇列的項目之後。
- 使用`Activity.SetParentId(message.ParentId)`toocorrelate 取用者和產生者記錄檔。
- 啟動 hello `Activity`。
- 使用 `Start/StopOperation` 協助程式追蹤清除佇列、處理和刪除作業。 執行從 hello 相同非同步控制流程 （執行內容）。 如此一來，這些作業就會正確地相互關聯。
- 停止 hello `Activity`。
- 使用 `Start/StopOperation` 或手動呼叫 `Track` 遙測。

### <a name="batch-processing"></a>批次處理
有些佇列中，您可以使用一個要求清除佇列多個訊息。 處理此類訊息會假定無關，並且所屬 toohello 不同的邏輯作業。 在此情況下，它不可能 toocorrelate hello`Dequeue`作業 tooparticular 訊息處理。

每個訊息應該在自己的非同步控制流程中處理。 如需詳細資訊，請參閱 hello[連出相依性追蹤](#outgoing-dependencies-tracking)> 一節。

## <a name="long-running-background-tasks"></a>長時間執行的背景工作
有些應用程式可能會應使用者要求，啟動長時間執行的作業。 Hello 追蹤/檢測的觀點而言，不要求或相依性的檢測不同： 

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

在此範例中，我們使用`telemetryClient.StartOperation`toocreate`RequestTelemetry`和填滿 hello 相互關聯的內容。 例如，假設您有在父作業所建立的排程 hello 作業的傳入要求。 只要`BackgroundTask`開始在 hello 與傳入的要求相同的非同步控制流程，該父作業相互關聯。 `BackgroundTask`和所有的巢狀的遙測項目都與 hello 要求造成它，即使在 hello 要求結束之後自動相互關聯。

當 hello 工作可啟動從 hello 背景執行緒沒有任何作業 (`Activity`) 相關聯，`BackgroundTask`沒有任何父項。 不過，它可以有巢狀作業。 從 hello 工作回報的所有遙測項目都是相互關聯的 toohello`RequestTelemetry`中建立`BackgroundTask`。

## <a name="outgoing-dependencies-tracking"></a>連出相依性追蹤
您可以追蹤自己的相依性種類或 Application Insights 不支援的作業。

hello `Enqueue` hello 服務匯流排佇列或 hello 儲存體佇列中的方法可以做為這類自訂追蹤的範例。

自訂相依性追蹤的 hello 一般方法是：

- 呼叫 hello `TelemetryClient.StartOperation` （擴充） 方法用來填滿 hello`DependencyTelemetry`所需的相互關聯與其他屬性的內容 (開始時間戳記，持續時間)。
- 設定其他自訂的屬性上 hello `DependencyTelemetry`，例如 hello 名稱和您需要的任何其他內容。
- 進行相依性呼叫並且等候。
- 停止與 hello 作業`StopOperation`完成時。
- 處理例外狀況。

`StopOperation`只會停止啟動 hello 作業。 如果 hello 目前執行的作業不符合 hello 其中一個要 toostop，`StopOperation`不做任何動作。 如果您以平行方式在 hello 中啟動多項作業，這種情況可能會發生相同的執行內容：

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

請確定一律呼叫 `StartOperation` 並在其自己的內容中執行您的工作：
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

## <a name="next-steps"></a>後續步驟

- 了解 hello 基本概念的[遙測相互關聯](application-insights-correlation.md)Application Insights 中。
- 請參閱 hello[資料模型](application-insights-data-model.md)Application Insights 的類型和資料模型。
- 報告自訂[事件和度量](app-insights-api-custom-events-metrics.md)tooApplication 深入資訊。
- 請查看內容屬性集合的標準[設定](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。
- 檢查 hello [System.Diagnostics.Activity 使用者指南](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)toosee 我們相互遙測的關聯。
