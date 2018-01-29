---
title: "Azure Functions C# 開發人員參考"
description: "了解如何使用 C# 開發 Azure Functions。"
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 12/12/2017
ms.author: glenga
ms.openlocfilehash: 3de1e9b042a7a356c3c88e604e1e26c256d85657
ms.sourcegitcommit: 828cd4b47fbd7d7d620fbb93a592559256f9d234
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="azure-functions-c-developer-reference"></a>Azure Functions C# 開發人員參考

<!-- When updating this article, make corresponding changes to any duplicate content in functions-reference-csharp.md -->

本文是在 .NET 類別庫中使用 C# 開發 Azure Functions 的簡介。

Azure Functions 支援 C# 和 C# 指令碼程式設計語言。 如果您需要[在 Azure 入口網站中使用 C#](functions-create-function-app-portal.md)的指引，請參閱 [C# 指令碼 (.csx) 開發人員參考](functions-reference-csharp.md)。

本文假設您已閱讀下列文章：

* [Azure Functions 開發人員指南](functions-reference.md)
* [Azure Functions Visual Studio 2017 Tools](functions-develop-vs.md)

## <a name="functions-class-library-project"></a>Functions 類別庫專案

在 Visual Studio 中，**Azure Functions** 專案範本可建立 C# 類別庫專案，其中包含下列檔案：

* [host.json](functions-host-json.md) - 儲存會影響在本機或 Azure 中執行之專案中所有函式的組態設定。
* [local.settings.json](functions-run-local.md#local-settings-file) - 儲存在本機執行時所使用的應用程式設定和連接字串。

### <a name="functionname-and-trigger-attributes"></a>FunctionName 和觸發程序屬性

在類別庫中，函式是具有 `FunctionName` 和觸發程序屬性的靜態方法，如下列範例所示：

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

`FunctionName` 屬性會將方法標記為函式進入點。 此名稱必須是專案中的唯一名稱。

觸發程序屬性可指定觸發程序類型，並將輸入資料繫結至方法參數。 範例函式是由佇列訊息所觸發，該佇列訊息會接著傳遞給 `myQueueItem` 參數中的方法。

### <a name="additional-binding-attributes"></a>其他繫結屬性

您可以使用其他輸入和輸出繫結屬性。 下列範例修改上一個範例並新增輸出佇列繫結。 此函式會將輸入佇列訊息寫入不同佇列中的新佇列訊息。

```csharp
public static class SimpleExampleWithOutput
{
    [FunctionName("CopyQueueMessage")]
    public static void Run(
        [QueueTrigger("myqueue-items-source")] string myQueueItem, 
        [Queue("myqueue-items-destination")] out string myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"CopyQueueMessage function processed: {myQueueItem}");
        myQueueItemCopy = myQueueItem;
    }
}
```

### <a name="conversion-to-functionjson"></a>轉換成 function.json

建置流程在組建資料夾的函式資料夾中建立 *function.json* 檔案。 此檔案不適合直接編輯。 您無法編輯此檔案來變更繫結設定或停用函式。 

此檔案的目的是提供資訊給縮放控制器，以用於[使用情況方案的縮放決策](functions-scale.md#how-the-consumption-plan-works)。 因此，檔案只會有觸發程序資訊，而不會有輸入或輸出繫結。

產生的 *function.json* 檔案包含 `configurationSource` 屬性 (property)，指示執行階段使用 .NET 屬性 (attribute) 屬性進行繫結，而不是使用 *function.json* 設定。 以下是範例：

```json
{
  "generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
  "configurationSource": "attributes",
  "bindings": [
    {
      "type": "queueTrigger",
      "queueName": "%input-queue-name%",
      "name": "myQueueItem"
    }
  ],
  "disabled": false,
  "scriptFile": "..\\bin\\FunctionApp1.dll",
  "entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```

*function.json* 檔案產生是由 NuGet 套件 [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions) 執行。 原始程式碼位於 GitHub 存放庫 [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk)。

## <a name="supported-types-for-bindings"></a>支援的繫結類型

每個繫結都有自己支援的類型；例如，Blob 觸發程序屬性可套用至字串參數、POCO 參數、`CloudBlockBlob` 參數或任何數個其他支援的類型。 [Blob 繫結的繫結參考文章](functions-bindings-storage-blob.md#trigger---usage)會列出所有支援的參數類型。 如需詳細資訊，請參閱[觸發程序和繫結](functions-triggers-bindings.md)以及[每個繫結類型的繫結參考文件](functions-triggers-bindings.md#next-steps)。

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="binding-to-method-return-value"></a>繫結至方法傳回值

您可以使用方法傳回值進行輸出繫結，如下列範例所示：

```csharp
public static class ReturnValueOutputBinding
{
    [FunctionName("CopyQueueMessageUsingReturnValue")]
    [return: Queue("myqueue-items-destination")]
    public static string Run(
        [QueueTrigger("myqueue-items-source-2")] string myQueueItem,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        return myQueueItem;
    }
}
```

## <a name="writing-multiple-output-values"></a>撰寫多個輸出值

若要多個值寫入至輸出繫結，請使用 [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) 類型。 這些類型是在方法完成時，寫入至輸出繫結的唯寫集合。

這個範例會使用 `ICollector` 將多個佇列訊息寫入相同佇列：

```csharp
public static class ICollectorExample
{
    [FunctionName("CopyQueueMessageICollector")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-3")] string myQueueItem,
        [Queue("myqueue-items-destination")] ICollector<string> myQueueItemCopy,
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 1: {myQueueItem}");
        myQueueItemCopy.Add($"Copy 2: {myQueueItem}");
    }
}
```

## <a name="logging"></a>記錄

若要使用 C# 將輸出記錄至串流記錄，請包含 `TraceWriter` 類型的引數。 建議您將它命名為 `log`。 避免在 Azure Functions 中使用 `Console.Write`。 

`TraceWriter` 已定義於 [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs)。 可以在 [host.json](functions-host-json.md) 中設定 `TraceWriter` 的記錄層級。

```csharp
public static class SimpleExample
{
    [FunctionName("QueueTrigger")]
    public static void Run(
        [QueueTrigger("myqueue-items")] string myQueueItem, 
        TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
} 
```

> [!NOTE]
> 如需您可使用之較新記錄架構 (而非 `TraceWriter`) 的資訊，請參閱**監視 Azure Functions** 一文中的[在 C# 函式中寫入記錄](functions-monitoring.md#write-logs-in-c-functions)。

## <a name="async"></a>非同步處理

若要讓函式變成非同步，請使用 `async` 關鍵字並傳回 `Task` 物件。

```csharp
public static class AsyncExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token,
        TraceWriter log)
    {
        log.Info($"BlobCopy function processed.");
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="cancellation-tokens"></a>取消權杖

某些作業需要正常關機。 雖然撰寫能夠處理當機情況的程式碼一律是最理想的做法，但是如果您想要處理關機要求，請定義 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) 型別引數。  提供 `CancellationToken` ，表示已觸發主機關機。

```csharp
public static class CancellationTokenExample
{
    [FunctionName("BlobCopy")]
    public static async Task RunAsync(
        [BlobTrigger("sample-images/{blobName}")] Stream blobInput,
        [Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
}
```

## <a name="environment-variables"></a>環境變數

若要取得環境變數或應用程式設定值，請使用 `System.Environment.GetEnvironmentVariable`，如下列程式碼範例所示：

```csharp
public static class EnvironmentVariablesExample
{
    [FunctionName("GetEnvironmentVariables")]
    public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
    {
        log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
        log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
        log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
    }

    public static string GetEnvironmentVariable(string name)
    {
        return name + ": " +
            System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
    }
}
```

## <a name="binding-at-runtime"></a>執行階段的繫結

在 C# 和其他 .NET 語言中，您可以使用相對於屬性中[宣告式](https://en.wikipedia.org/wiki/Declarative_programming)繫結的[命令式](https://en.wikipedia.org/wiki/Imperative_programming)繫結模式。 當繫結參數需要在執行階段而不是設計階段中計算時，命令式繫結非常有用。 利用此模式，您可以快速在您的函式程式碼中繫結至支援的輸入和輸出繫結。

定義命令式繫結，如下所示︰

- **請勿**在函式簽章中加入您所需命令式繫結的屬性。
- 傳入輸入參數 [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) 或 [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs)。
- 使用下列 C# 模式來執行資料繫結。

  ```cs
  using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
  {
      ...
  }
  ```

  `BindingTypeAttribute` 是可定義繫結的 .NET 屬性，而 `T` 是該繫結類型所支援的輸入或輸出類型。 `T` 不能是 `out` 參數類型 (例如 `out JObject`)。 例如，Mobile Apps 資料表輸出繫結支援[六個輸出類型](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22)，但您只可以搭配命令式繫結使用 [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) 或 [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)。

### <a name="single-attribute-example"></a>單一屬性範例

下列範例程式碼會使用在執行階段定義的 blob 路徑來建立[儲存體 blob 輸出繫結](functions-bindings-storage-blob.md#output)，然後將字串寫入 blob。

```cs
public static class IBinderExample
{
    [FunctionName("CreateBlobUsingBinder")]
    public static void Run(
        [QueueTrigger("myqueue-items-source-4")] string myQueueItem,
        IBinder binder,
        TraceWriter log)
    {
        log.Info($"CreateBlobUsingBinder function processed: {myQueueItem}");
        using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
                    $"samples-output/{myQueueItem}", FileAccess.Write)))
        {
            writer.Write("Hello World!");
        };
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) 會定義[儲存體 blob](functions-bindings-storage-blob.md) 輸入或輸出繫結，而 [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) 是支援的輸出繫結類型。

### <a name="multiple-attribute-example"></a>多個屬性範例

先前的範例會取得函數應用程式主要儲存體帳戶連接字串的應用程式設定 (也就是 `AzureWebJobsStorage`)。 您可以指定要用於儲存體帳戶的自訂應用程式設定，方法是新增 [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) 並將屬性陣列傳遞至 `BindAsync<T>()`。 使用 `Binder` 參數，而不是 `IBinder`。  例如︰

```cs
public static class IBinderExampleMultipleAttributes
{
    [FunctionName("CreateBlobInDifferentStorageAccount")]
    public async static Task RunAsync(
            [QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
            Binder binder,
            TraceWriter log)
    {
        log.Info($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
        var attributes = new Attribute[]
        {
        new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
        new StorageAccountAttribute("MyStorageAccount")
        };
        using (var writer = await binder.BindAsync<TextWriter>(attributes))
        {
            await writer.WriteAsync("Hello World!!");
        }
    }
}
```

## <a name="triggers-and-bindings"></a>觸發和繫結 

下表列出的觸發程序和繫結屬性可在 Azure Functions 類別庫專案中使用。 所有屬性都在 `Microsoft.Azure.WebJobs` 命名空間中。

| 觸發程序 | 輸入 | 輸出|
|------   | ------    | ------  |
| [BlobTrigger](functions-bindings-storage-blob.md#trigger---attributes)| [Blob](functions-bindings-storage-blob.md#input---attributes)| [Blob](functions-bindings-storage-blob.md#output---attributes)|
| [CosmosDBTrigger](functions-bindings-cosmosdb.md#trigger---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#input---attributes)| [DocumentDB](functions-bindings-cosmosdb.md#output---attributes) |
| [EventHubTrigger](functions-bindings-event-hubs.md#trigger---attributes)|| [EventHub](functions-bindings-event-hubs.md#output---attributes) |
| [HTTPTrigger](functions-bindings-http-webhook.md#trigger---attributes)|||
| [QueueTrigger](functions-bindings-storage-queue.md#trigger---attributes)|| [佇列](functions-bindings-storage-queue.md#output---attributes) |
| [ServiceBusTrigger](functions-bindings-service-bus.md#trigger---attributes)|| [ServiceBus](functions-bindings-service-bus.md#output---attributes) |
| [TimerTrigger](functions-bindings-timer.md#attributes) | ||
| |[ApiHubFile](functions-bindings-external-file.md)| [ApiHubFile](functions-bindings-external-file.md)|
| |[MobileTable](functions-bindings-mobile-apps.md#input---attributes)| [MobileTable](functions-bindings-mobile-apps.md#output---attributes) | 
| |[資料表](functions-bindings-storage-table.md#input---attributes)| [資料表](functions-bindings-storage-table.md#output---attributes)  | 
| ||[NotificationHub](functions-bindings-notification-hubs.md#attributes) |
| ||[SendGrid](functions-bindings-sendgrid.md#attributes) |
| ||[Twilio](functions-bindings-twilio.md#attributes)| 

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [深入了解觸發程序和繫結](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [深入了解 Azure Functions 的最佳做法](functions-best-practices.md)
