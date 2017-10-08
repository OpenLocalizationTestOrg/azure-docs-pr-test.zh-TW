---
title: "aaaUsing.NET 類別庫來搭配 Azure 函式 |Microsoft 文件"
description: "了解如何 tooauthor.NET 類別庫使用的 Azure 函式"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>使用 .NET 類別庫搭配 Azure Functions

此外 tooscript 檔案，Azure 函式支援發行類別庫做為一或多個函式的 hello 實作。 我們建議您改用 hello [Azure 函式 Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)。

## <a name="prerequisites"></a>必要條件 

這篇文章有 hello 下列必要條件：

- [Visual Studio 2017 15.3 預覽](https://www.visualstudio.com/vs/preview/)。 安裝 hello 工作負載**ASP.NET 及 web 開發**和**Azure 開發**。
- [Azure Function Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Functions 類別庫專案

從 Visual Studio 中建立 Azure Functions 專案。 hello 新的專案範本建立 hello 檔案*host.json*和*local.settings.json*。 您可以[在 host.json 中自訂 Azure Functions 執行階段設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。 

hello 檔案*local.settings.json*儲存應用程式設定、 連接字串和 Azure 函式的核心工具的設定。 toolearn 進一步了解它的結構，請參閱[程式碼和測試 Azure 函式在本機](functions-run-local.md#local-settings)。

### <a name="functionname-attribute"></a>FunctionName 屬性

hello 屬性[ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs)標記做為函式進入點方法。 它必須剛好僅與一個觸發程序以及 0 個以上的輸入和輸出繫結搭配使用。

### <a name="conversion-toofunctionjson"></a>轉換 toofunction.json

Azure 函式專案建置時，它會產生一個檔案`function.json`hello 目錄中符合 hello 函式名稱所定義`[FunctionName]`。 它會指定觸發程序和繫結和點 toohello 專案的組件檔。

Hello NuGet 封裝會執行此轉換[Microsoft\.NET\.Sdk\.函式](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions)。 hello 來源可供使用 hello GitHub 儲存機制內[azure\-函式\-vs\-建置\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk)。

## <a name="triggers-and-bindings"></a>觸發和繫結

hello 下表列出 hello 觸發程序和 Azure 函式的類別庫專案中可用的繫結。 Hello 命名空間中的所有屬性都是`Microsoft.Azure.WebJobs`。

| 繫結 | 屬性 | Nuget 套件 |
|------   | ------    | ------        |
| [Blob 儲存體觸發程序, 輸入, 輸出](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Blob 儲存體] |
| [Cosmos DB 輸入和輸出繫結](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [事件中心觸發程序和輸出](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [外部檔案輸入和輸出](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [HTTP 和 Webhook 觸發程序](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Mobile Apps 輸入和輸出](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [通知中樞輸出](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [佇列儲存體觸發程序和輸出](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [SendGrid 輸出](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [服務匯流排觸發程序和輸出](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [資料表儲存體輸入和輸出](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [計時器觸發程序](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Twilio 輸出](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Blob 儲存體觸發程序、輸入和輸出繫結

Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。 如需有關繫結運算式和中繼資料的詳細資訊，請參閱 [Azure Functions Blob 儲存體繫結](functions-bindings-storage-blob.md)。

Blob 的觸發程序定義以 hello`[BlobTrigger]`屬性。 您可以使用 hello 屬性`[StorageAccount]`toodefine hello 儲存體帳戶所使用的整個函式或類別。

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

Blob 輸入和輸出定義使用 hello`[Blob]`屬性，以及與`FileAccess`參數，表示讀取或寫入。 下列範例會使用 hello blob 觸發程序和 blob 輸出繫結。

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Cosmos DB 輸入和輸出繫結

Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。 toolearn hello 功能 hello Cosmos DB，繫結的詳細資料請參閱[Azure 函式 Cosmos DB 繫結](functions-bindings-documentdb.md)。

toobind tooa Cosmos DB 文件中，使用 hello 屬性`[DocumentDB]`hello NuGet 封裝中[Microsoft.Azure.WebJobs.Extensions.DocumentDB]。 下列範例中的 hello 具有佇列觸發程序和輸出繫結 DocumentDB API:

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>事件中心觸發程序和輸出

Azure Functions 支援事件中樞的觸發程序和輸出繫結。 如需詳細資訊，請參閱 [Azure Functions 事件中樞繫結](functions-bindings-event-hubs.md)。

hello 類型`[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]`和`[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.ServiceBus]。 

hello 下列範例會使用事件中心觸發程序：

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

hello 下列範例包含事件中心輸出時，使用 hello 方法的傳回值為 hello 輸出：

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>外部檔案輸入和輸出

Azure Functions 支援適用於外部檔案 (例如 Google Drive、Dropbox 和 OneDrive) 的觸發程序、輸入和輸出繫結。 詳細資訊，請參閱 toolearn [Azure 函式的外部檔案繫結](functions-bindings-external-file.md)。 hello 屬性`[ExternalFileTrigger]`和`[ExternalFile]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.ApiHub]。

hello 下列 C# 範例示範外部檔案輸入和輸出繫結。 hello 程式碼複製 hello 輸入的檔 toohello 輸出檔。

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP 和 Webhook

使用 hello`HttpTrigger`屬性 toodefine HTTP 觸發程序或 webhook。 這個屬性定義在 hello NuGet 封裝[Microsoft.Azure.WebJobs.Extensions.Http]。 您可以自訂 hello 授權層級、 webhook 類型、 route 和方法。 hello 下列範例會定義匿名驗證的 HTTP 觸發程序和_genericJson_ webhook 型別。

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Mobile Apps 輸入和輸出

Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。 詳細資訊，請參閱 toolearn [Azure 函式行動應用程式繫結](functions-bindings-mobile-apps.md)。 hello 屬性`[MobileTable]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.MobileApps]。

hello 下列範例會示範行動應用程式輸出繫結：

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>通知中樞輸出

Azure Functions 會支援通知中樞的輸出繫結。 詳細資訊，請參閱 toolearn [Azure 函式的通知中樞輸出繫結](functions-bindings-notification-hubs.md)。 hello 屬性`[NotificationHub]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]。

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>佇列儲存體觸發程序和輸出

Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。 如需詳細資訊，請參閱 [Azure Functions 佇列儲存體繫結](functions-bindings-storage-queue.md)。

hello 下列範例示範如何 toouse hello 函式傳回型別具有佇列輸出繫結、 使用 hello`[Queue]`屬性。 toodefine 佇列觸發程序，使用 hello`[QueueTrigger]`屬性。

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>SendGrid 輸出

Azure Functions 支援用於以程式設計方式傳送電子郵件的 SendGrid 輸出繫結。 詳細資訊，請參閱 toolearn [Azure 函式 SendGrid 繫結](functions-bindings-sendgrid.md)。

hello 屬性`[SendGrid]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.Extensions.SendGrid]。

hello 以下是使用服務匯流排佇列觸發程序和 SendGrid 輸出繫結使用的範例`SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>服務匯流排觸發程序和輸出

Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。 如需有關如何設定繫結的詳細資訊，請參閱 [Azure Functions 服務匯流排繫結](functions-bindings-service-bus.md)。

hello 屬性`[ServiceBusTrigger]`和`[ServiceBus]`hello NuGet 封裝中定義[Microsoft.Azure.WebJobs.ServiceBus]。 

hello 下列是服務匯流排佇列觸發程序的範例：

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

hello 下列是服務匯流排輸出繫結、 使用 hello 方法的傳回型別做為 hello 輸出的範例：

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>資料表儲存體輸入和輸出

Azure Functions 支援 Azure 資料表儲存體的輸入和輸出繫結。 詳細資訊，請參閱 toolearn [Azure 函式的資料表儲存體繫結](functions-bindings-storage-table.md)。

hello 下列範例是具有兩個函式，示範資料表儲存體輸出和輸入的繫結的類別。 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>計時器觸發程序

Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。 toolearn hello 功能，hello 繫結的詳細資料請參閱[排程與 Azure 函式的程式碼執行](functions-bindings-timer.md)。

在 hello 耗用量計劃，您可以定義排程與[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)。 如果您是使用 App Service 方案，也可以使用 TimeSpan 字串。 

下列範例中的 hello 定義執行每隔 5 分鐘的計時器觸發程序：

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Twilio 輸出

Azure 函式支援 Twilio 輸出繫結 tooenable 函式 toosend SMS 文字訊息。 詳細資訊，請參閱 toolearn[傳送 SMS 訊息使用 hello Twilio Azure 函式的輸出繫結](functions-bindings-twilio.md)。 

hello 屬性`[TwilioSms]`hello 封裝中定義[Microsoft.Azure.WebJobs.Extensions.Twilio]。

hello 下列 C# 範例會使用佇列觸發程序和 Twilio 輸出繫結：

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>後續步驟

如需有關如何在 C# 指令碼中使用 Azure Functions 的詳細資訊，請參閱 [Azure Functions C\# 指令碼開發人員參考](functions-reference-csharp.md)。

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
