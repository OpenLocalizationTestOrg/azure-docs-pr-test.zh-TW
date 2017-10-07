---
title: "以 hello WebJobs SDK aaaHow toouse Azure 服務匯流排"
description: "了解 toouse Azure 服務匯流排佇列和主題與 hello WebJobs SDK。"
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
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>如何 toouse Azure 服務匯流排與 hello WebJobs SDK
## <a name="overview"></a>概觀
本指南提供 C# 程式碼範例會顯示如何 tootrigger 收到 Azure 服務匯流排訊息時的處理序。 hello 程式碼範例使用[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。

hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)。

hello 程式碼片段只會顯示函式，不 hello 程式碼會建立 hello`JobHost`物件，如此範例所示：

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

A[完成的服務匯流排程式碼範例](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs)上 GitHub.com hello azure webjobs sdk 的範例儲存機制中。

## <a id="prerequisites"></a> 必要條件
toowork 您尚未使用服務匯流排 tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 封裝除了 toohello 其他 WebJobs SDK 封裝。 

您也可以 tooset hello AzureWebJobsServiceBus 連接字串中加入 toohello 儲存體連接字串。  您可以在 hello`connectionStrings`區段 hello App.config 檔案，如下列範例中的 hello 中所示：

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

包含在 hello App.config 檔案中的 hello 服務匯流排連接字串設定為範例專案，請參閱[服務匯流排範例](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)。 

hello 連接字串也可以設定在 hello Azure 執行階段環境中，然後在 hello WebJob 會執行於 Azure; 時，覆寫 hello App.config 設定如需詳細資訊，請參閱[hello WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)。

## <a id="trigger"></a>收到 tootrigger 函式時，服務匯流排佇列訊息的方式
toowrite hello WebJobs SDK 的函式呼叫接收佇列訊息時，請使用 hello`ServiceBusTrigger`屬性。 hello 屬性建構函式會使用參數來指定 hello 佇列 toopoll hello 名稱。

### <a name="how-servicebustrigger-works"></a>ServiceBusTrigger 的運作方式
hello SDK 收到訊息時在`PeekLock`模式和呼叫`Complete`hello 訊息，如果成功，完成 hello 函式或呼叫`Abandon`如果 hello 函式失敗。 如果 hello 函式執行時間長於 hello `PeekLock` hello 鎖定逾時，會自動更新。

服務匯流排執行它自己的有害佇列處理無法控制或 hello WebJobs SDK 所設定。 

### <a name="string-queue-message"></a>字串佇列訊息
hello 下列程式碼範例會讀取佇列訊息，其中包含字串並寫入 hello 字串 toohello WebJobs SDK 儀表板。

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**注意：**如果您要建立 hello 訊息排入佇列，不會使用 hello WebJobs SDK 的應用程式中，請確定 tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx)太"text/plain"。

### <a name="poco-queue-message"></a>POCO 佇列訊息
hello SDK 會自動還原序列化的 POCO 包含 JSON 的佇列訊息[(純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 型別。 hello 下列程式碼範例會讀取佇列訊息，其中包含`BlobInformation`含有物件`BlobName`屬性：

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

如需程式碼範例顯示如何使用 blob 和資料表中的 hello POCO toowork toouse 屬性 hello 相同函式中，請參閱 hello[這篇文章的儲存體佇列版本](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)。

如果您建立 hello 佇列訊息的程式碼不會使用 hello WebJobs SDK，請使用下列範例程式碼類似 toohello:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>ServiceBusTrigger 使用的類型
除了`string`和 POCO 型別，您可以使用 hello`ServiceBusTrigger`的位元組陣列的屬性或`BrokeredMessage`物件。

## <a id="create"></a>Toocreate Service Bus 佇列訊息的方式
toowrite 建立新的佇列訊息的函式使用 hello`ServiceBus`屬性，並傳入 hello 佇列名稱 toohello 屬性建構函式。 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>在同步函數中建立單一佇列訊息
hello，下列程式碼範例會使用輸出參數 toocreate hello 佇列中的新訊息名為"outputqueue"hello 做為內容相同 hello 名為"inputqueue"hello 佇列中接收訊息。

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

hello 輸出參數，以建立單一佇列訊息可以是 hello 的任何下列類型:

* `string`
* `byte[]`
* `BrokeredMessage`
* 您定義的可序列化 POCO 類型。 自動序列化為 JSON。

POCO 型別參數，佇列訊息時一律會建立 hello 函式會結束。hello 參數為 null，如果 hello SDK 建立的佇列訊息，收到 hello 訊息並將其還原序列化時將會傳回 null。 如 hello 其他類型，如果 hello 參數為 null 會建立任何佇列訊息。

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>建立多個佇列訊息或在非同步函式中
toocreate 多則訊息，使用 hello`ServiceBus`屬性附帶`ICollector<T>`或`IAsyncCollector<T>`hello 下列程式碼範例所示：

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

每個佇列的訊息建立時立即 hello`Add`方法呼叫。

## <a id="topics"></a>如何與 Service Bus 主題 toowork
toowrite hello SDK 函式會呼叫服務匯流排主題接收訊息時，請使用 hello `ServiceBusTrigger` hello 建構函式會採用主題名稱與訂用帳戶名稱，hello 下列程式碼範例所示的屬性：

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate 主題時，使用 hello 訊息`ServiceBus`屬性以主題名稱 hello 相同方式使用佇列的名稱。

## <a name="features-added-in-release-11"></a>在 1.1 版中新增的功能
1.1 版中新增下列功能的 hello:

* 允許透過 `ServiceBusConfiguration.MessagingProvider`深層自訂訊息處理。
* `MessagingProvider`支援自訂 hello Service Bus`MessagingFactory`和`NamespaceManager`。
* A`MessageProcessor`策略模式可讓您 toospecify 每個佇列/主題的處理器。
* 訊息處理並行依預設支援。 
* 透過 `ServiceBusConfiguration.MessageOptions` 輕鬆自訂 `OnMessageOptions`。
* 允許[AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe 上指定`ServiceBusTriggerAttribute` / `ServiceBusAttribute` （的情況下，您可能不需要管理權限）。 請注意，Azure WebJobs 無法 tooautomatically 佈建不存在佇列和主題不管理 AccessRights。

## <a id="queues"></a>Hello 儲存體佇列如何 tooarticle 所涵蓋的相關的主題
如需 WebJobs SDK 案例不是特定 tooService 匯流排，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。 

在該文件中涵蓋的主題包括下列 hello:

* Async 函數
* 多個執行個體
* 正常關機
* 使用 WebJobs SDK hello 函式主體中的屬性
* 程式碼中設定 hello SDK 連接字串
* 在程式碼中設定 WebJobs SDK 建構函式參數的值
* 手動觸發函式
* 寫入記錄檔

## <a id="nextsteps"></a> 後續步驟
本指南提供的程式碼範例會顯示如何使用 Azure 服務匯流排 toohandle 常見案例。 如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。

