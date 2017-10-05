---
title: "如何透過 WebJobs SDK 使用 Azure 服務匯流排"
description: "瞭解如何搭配使用 Azure 服務匯流排佇列和有關 WebJobs SDK 的主題。"
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a>如何透過 WebJobs SDK 使用 Azure 服務匯流排
## <a name="overview"></a>概觀
本指南提供 C# 程式碼範例，示範如何在接收到 Azure 服務匯流排訊息時觸發程序。 此程式碼範例會使用 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 1.x 版。

本指南假設您知道 [如何使用指向您儲存體帳戶的連接字串，在 Visual Studio 中建立 WebJob 專案](websites-dotnet-webjobs-sdk-get-started.md)。

程式碼片段只會顯示函數，不會顯示建立 `JobHost` 物件的程式碼，如此範例所示：

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

[完整的服務匯流排程式碼範例](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) 可在 GitHub.com 的 azure-webjobs-sdk-samples 存放庫中找到。

## <a id="prerequisites"></a> 必要條件
若要使用服務匯流排，除了其他的 WebJobs SDK 封裝之外，您還必須安裝 [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 封裝。 

除了儲存體連接字串之外，您也必須設定 AzureWebJobsServiceBus 連接字串。  您可以在 App.config 檔案的 `connectionStrings` 區段中執行這個動作，如下列範例所示：

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

如需包含 App.config 檔案中服務匯流排連接字串設定的範例專案，請參閱 [服務匯流排範例](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)。 

連接字串也可以在 Azure 執行階段環境中設定，然後會在 Azure 中執行 WebJob 時覆寫 App.config。如需詳細資訊，請參閱[開始使用 WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)。

## <a id="trigger"></a> 如何在收到服務匯流排佇列訊息時觸發函數
若要撰寫 WebJobs SDK 在收到佇列訊息時所呼叫的函數，請使用 `ServiceBusTrigger` 屬性。 屬性建構函式會接受一個參數，以指定要輪詢的佇列名稱。

### <a name="how-servicebustrigger-works"></a>ServiceBusTrigger 的運作方式
SDK 會在 `PeekLock` 模式中收到訊息，並在函數成功完成時，於訊息中呼叫 `Complete`，或是在函數失敗時呼叫 `Abandon`。 如果函數執行時間較 `PeekLock` 逾時還長，即會自動更新鎖定。

服務匯流排會自行處理 WebJobs SDK 無法控制或設定的有害佇列。 

### <a name="string-queue-message"></a>字串佇列訊息
下列程式碼範例會讀取包含字串的佇列訊息，並將字串寫入 WebJobs SDK 儀表板。

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**注意：** 如果您在沒有 WebJobs SDK 的應用程式中建立佇列訊息，請務必將 [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) 設為 "text/plain"。

### <a name="poco-queue-message"></a>POCO 佇列訊息
SDK 會針對 POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 類型，自動將包含 JSON 的佇列訊息還原序列化。 下列程式碼範例會讀取包含 `BlobInformation` 物件的佇列訊息，該物件具有 `BlobName` 屬性：

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

如需示範如何使用 POCO 的屬性，在同一個函數中使用 Blob 和資料表的程式碼範例，請參閱 [本文的儲存體佇列版本](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)。

如果您建立佇列訊息的程式碼不使用 WebJobs SDK，請使用類似下列範例的程式碼：

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>ServiceBusTrigger 使用的類型
除了 `string` 和 POCO 類型之外，您可以使用 `ServiceBusTrigger` 屬性搭配位元組陣列或 `BrokeredMessage` 物件。

## <a id="create"></a> 如何建立服務匯流排佇列訊息
若要撰寫建立新佇列訊息的函數，請使用 `ServiceBus` 屬性，並在佇列名稱中傳遞至屬性建構函式。 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>在同步函數中建立單一佇列訊息
下列程式碼範例會使用輸出參數，使用與在名為 "inputqueue" 的佇列中收到的訊息相同的內容，在名為 "outputqueue" 的佇列中建立新訊息。

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

用來建立單一佇列訊息的輸出參數可以是下列任一類型：

* `string`
* `byte[]`
* `BrokeredMessage`
* 您定義的可序列化 POCO 類型。 自動序列化為 JSON。

若為 POCO 類型參數，一定會在函式結束時建立佇列訊息；如果參數是 Null，SDK 會建立在接收和還原序列化訊息將傳回 Null 的佇列訊息。 針對其他類型，如果參數為 Null，就不會建立任何佇列訊息。

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>建立多個佇列訊息或在非同步函式中
若要建立多個訊息，請使用 `ServiceBus` 屬性搭配 `ICollector<T>` 或 `IAsyncCollector<T>`，如下列程式碼範例所示：

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

呼叫 `Add` 方法時，就會立即建立每個佇列訊息。

## <a id="topics"></a>如何使用服務匯流排主題
若要撰寫 SDK 在服務匯流排主題上收到訊息時所呼叫的函數，請使用 `ServiceBusTrigger` 屬性搭配採用主題名稱和訂用帳戶名稱的建構函式，如下列程式碼範例所示：

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

若要在主題上建立訊息，請使用 `ServiceBus` 屬性搭配主題名稱，方法和您將它與佇列名稱搭配使用的方式相同。

## <a name="features-added-in-release-11"></a>在 1.1 版中新增的功能
以下是在 1.1 版中新增的功能：

* 允許透過 `ServiceBusConfiguration.MessagingProvider`深層自訂訊息處理。
* `MessagingProvider` 支援自訂服務匯流排 `MessagingFactory` 和 `NamespaceManager`。
* `MessageProcessor` 策略模式可讓您為每個佇列/主題指定處理器。
* 訊息處理並行依預設支援。 
* 透過 `ServiceBusConfiguration.MessageOptions` 輕鬆自訂 `OnMessageOptions`。
* 允許在 `ServiceBusTriggerAttribute`/`ServiceBusAttribute` 上指定 [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) (針對您可能沒有管理權限的情況)。 請注意，Azure WebJobs 無法在沒有管理 AccessRights 的情況下，自動佈建不存在的佇列和主題。

## <a id="queues"></a>儲存體佇列做法文章所涵蓋的相關主題
如需與特定服務匯流排無關的 WebJobs SDK 案例的相關資訊，請參閱 [如何透過 WebJobs SDK 使用 Azure 佇列儲存體](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。 

該文章涵蓋下列主題：

* Async 函數
* 多個執行個體
* 正常關機
* 在函式主體中使用 WebJobs SDK 屬性
* 在程式碼中設定 SDK 連接字串
* 在程式碼中設定 WebJobs SDK 建構函式參數的值
* 手動觸發函式
* 寫入記錄檔

## <a id="nextsteps"></a> 後續步驟
本指南提供了程式碼範例，示範如何處理使用 Azure Service Bus 的常見案例。 如需 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。

