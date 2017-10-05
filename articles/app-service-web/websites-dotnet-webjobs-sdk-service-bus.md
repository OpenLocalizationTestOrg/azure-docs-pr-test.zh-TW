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
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="e0ede-103">如何透過 WebJobs SDK 使用 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="e0ede-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="e0ede-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e0ede-104">Overview</span></span>
<span data-ttu-id="e0ede-105">本指南提供 C# 程式碼範例，示範如何在接收到 Azure 服務匯流排訊息時觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e0ede-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="e0ede-106">此程式碼範例會使用 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="e0ede-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="e0ede-107">本指南假設您知道 [如何使用指向您儲存體帳戶的連接字串，在 Visual Studio 中建立 WebJob 專案](websites-dotnet-webjobs-sdk-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="e0ede-108">程式碼片段只會顯示函數，不會顯示建立 `JobHost` 物件的程式碼，如此範例所示：</span><span class="sxs-lookup"><span data-stu-id="e0ede-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="e0ede-109">[完整的服務匯流排程式碼範例](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) 可在 GitHub.com 的 azure-webjobs-sdk-samples 存放庫中找到。</span><span class="sxs-lookup"><span data-stu-id="e0ede-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="e0ede-110"><a id="prerequisites"></a> 必要條件</span><span class="sxs-lookup"><span data-stu-id="e0ede-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="e0ede-111">若要使用服務匯流排，除了其他的 WebJobs SDK 封裝之外，您還必須安裝 [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="e0ede-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="e0ede-112">除了儲存體連接字串之外，您也必須設定 AzureWebJobsServiceBus 連接字串。</span><span class="sxs-lookup"><span data-stu-id="e0ede-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="e0ede-113">您可以在 App.config 檔案的 `connectionStrings` 區段中執行這個動作，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e0ede-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="e0ede-114">如需包含 App.config 檔案中服務匯流排連接字串設定的範例專案，請參閱 [服務匯流排範例](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="e0ede-115">連接字串也可以在 Azure 執行階段環境中設定，然後會在 Azure 中執行 WebJob 時覆寫 App.config。如需詳細資訊，請參閱[開始使用 WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="e0ede-116"><a id="trigger"></a> 如何在收到服務匯流排佇列訊息時觸發函數</span><span class="sxs-lookup"><span data-stu-id="e0ede-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="e0ede-117">若要撰寫 WebJobs SDK 在收到佇列訊息時所呼叫的函數，請使用 `ServiceBusTrigger` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e0ede-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="e0ede-118">屬性建構函式會接受一個參數，以指定要輪詢的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="e0ede-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="e0ede-119">ServiceBusTrigger 的運作方式</span><span class="sxs-lookup"><span data-stu-id="e0ede-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="e0ede-120">SDK 會在 `PeekLock` 模式中收到訊息，並在函數成功完成時，於訊息中呼叫 `Complete`，或是在函數失敗時呼叫 `Abandon`。</span><span class="sxs-lookup"><span data-stu-id="e0ede-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="e0ede-121">如果函數執行時間較 `PeekLock` 逾時還長，即會自動更新鎖定。</span><span class="sxs-lookup"><span data-stu-id="e0ede-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="e0ede-122">服務匯流排會自行處理 WebJobs SDK 無法控制或設定的有害佇列。</span><span class="sxs-lookup"><span data-stu-id="e0ede-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="e0ede-123">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="e0ede-123">String queue message</span></span>
<span data-ttu-id="e0ede-124">下列程式碼範例會讀取包含字串的佇列訊息，並將字串寫入 WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="e0ede-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="e0ede-125">**注意：** 如果您在沒有 WebJobs SDK 的應用程式中建立佇列訊息，請務必將 [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) 設為 "text/plain"。</span><span class="sxs-lookup"><span data-stu-id="e0ede-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="e0ede-126">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="e0ede-126">POCO queue message</span></span>
<span data-ttu-id="e0ede-127">SDK 會針對 POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 類型，自動將包含 JSON 的佇列訊息還原序列化。</span><span class="sxs-lookup"><span data-stu-id="e0ede-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="e0ede-128">下列程式碼範例會讀取包含 `BlobInformation` 物件的佇列訊息，該物件具有 `BlobName` 屬性：</span><span class="sxs-lookup"><span data-stu-id="e0ede-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="e0ede-129">如需示範如何使用 POCO 的屬性，在同一個函數中使用 Blob 和資料表的程式碼範例，請參閱 [本文的儲存體佇列版本](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="e0ede-130">如果您建立佇列訊息的程式碼不使用 WebJobs SDK，請使用類似下列範例的程式碼：</span><span class="sxs-lookup"><span data-stu-id="e0ede-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="e0ede-131">ServiceBusTrigger 使用的類型</span><span class="sxs-lookup"><span data-stu-id="e0ede-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="e0ede-132">除了 `string` 和 POCO 類型之外，您可以使用 `ServiceBusTrigger` 屬性搭配位元組陣列或 `BrokeredMessage` 物件。</span><span class="sxs-lookup"><span data-stu-id="e0ede-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="e0ede-133"><a id="create"></a> 如何建立服務匯流排佇列訊息</span><span class="sxs-lookup"><span data-stu-id="e0ede-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="e0ede-134">若要撰寫建立新佇列訊息的函數，請使用 `ServiceBus` 屬性，並在佇列名稱中傳遞至屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="e0ede-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="e0ede-135">在同步函數中建立單一佇列訊息</span><span class="sxs-lookup"><span data-stu-id="e0ede-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="e0ede-136">下列程式碼範例會使用輸出參數，使用與在名為 "inputqueue" 的佇列中收到的訊息相同的內容，在名為 "outputqueue" 的佇列中建立新訊息。</span><span class="sxs-lookup"><span data-stu-id="e0ede-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="e0ede-137">用來建立單一佇列訊息的輸出參數可以是下列任一類型：</span><span class="sxs-lookup"><span data-stu-id="e0ede-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="e0ede-138">您定義的可序列化 POCO 類型。</span><span class="sxs-lookup"><span data-stu-id="e0ede-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="e0ede-139">自動序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="e0ede-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="e0ede-140">若為 POCO 類型參數，一定會在函式結束時建立佇列訊息；如果參數是 Null，SDK 會建立在接收和還原序列化訊息將傳回 Null 的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="e0ede-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="e0ede-141">針對其他類型，如果參數為 Null，就不會建立任何佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="e0ede-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="e0ede-142">建立多個佇列訊息或在非同步函式中</span><span class="sxs-lookup"><span data-stu-id="e0ede-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="e0ede-143">若要建立多個訊息，請使用 `ServiceBus` 屬性搭配 `ICollector<T>` 或 `IAsyncCollector<T>`，如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="e0ede-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="e0ede-144">呼叫 `Add` 方法時，就會立即建立每個佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="e0ede-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="e0ede-145"><a id="topics"></a>如何使用服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="e0ede-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="e0ede-146">若要撰寫 SDK 在服務匯流排主題上收到訊息時所呼叫的函數，請使用 `ServiceBusTrigger` 屬性搭配採用主題名稱和訂用帳戶名稱的建構函式，如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="e0ede-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="e0ede-147">若要在主題上建立訊息，請使用 `ServiceBus` 屬性搭配主題名稱，方法和您將它與佇列名稱搭配使用的方式相同。</span><span class="sxs-lookup"><span data-stu-id="e0ede-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="e0ede-148">在 1.1 版中新增的功能</span><span class="sxs-lookup"><span data-stu-id="e0ede-148">Features added in release 1.1</span></span>
<span data-ttu-id="e0ede-149">以下是在 1.1 版中新增的功能：</span><span class="sxs-lookup"><span data-stu-id="e0ede-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="e0ede-150">允許透過 `ServiceBusConfiguration.MessagingProvider`深層自訂訊息處理。</span><span class="sxs-lookup"><span data-stu-id="e0ede-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="e0ede-151">`MessagingProvider` 支援自訂服務匯流排 `MessagingFactory` 和 `NamespaceManager`。</span><span class="sxs-lookup"><span data-stu-id="e0ede-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="e0ede-152">`MessageProcessor` 策略模式可讓您為每個佇列/主題指定處理器。</span><span class="sxs-lookup"><span data-stu-id="e0ede-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="e0ede-153">訊息處理並行依預設支援。</span><span class="sxs-lookup"><span data-stu-id="e0ede-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="e0ede-154">透過 `ServiceBusConfiguration.MessageOptions` 輕鬆自訂 `OnMessageOptions`。</span><span class="sxs-lookup"><span data-stu-id="e0ede-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="e0ede-155">允許在 `ServiceBusTriggerAttribute`/`ServiceBusAttribute` 上指定 [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) (針對您可能沒有管理權限的情況)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="e0ede-156">請注意，Azure WebJobs 無法在沒有管理 AccessRights 的情況下，自動佈建不存在的佇列和主題。</span><span class="sxs-lookup"><span data-stu-id="e0ede-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="e0ede-157"><a id="queues"></a>儲存體佇列做法文章所涵蓋的相關主題</span><span class="sxs-lookup"><span data-stu-id="e0ede-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="e0ede-158">如需與特定服務匯流排無關的 WebJobs SDK 案例的相關資訊，請參閱 [如何透過 WebJobs SDK 使用 Azure 佇列儲存體](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="e0ede-159">該文章涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="e0ede-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="e0ede-160">Async 函數</span><span class="sxs-lookup"><span data-stu-id="e0ede-160">Async functions</span></span>
* <span data-ttu-id="e0ede-161">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="e0ede-161">Multiple instances</span></span>
* <span data-ttu-id="e0ede-162">正常關機</span><span class="sxs-lookup"><span data-stu-id="e0ede-162">Graceful shutdown</span></span>
* <span data-ttu-id="e0ede-163">在函式主體中使用 WebJobs SDK 屬性</span><span class="sxs-lookup"><span data-stu-id="e0ede-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="e0ede-164">在程式碼中設定 SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="e0ede-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="e0ede-165">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="e0ede-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="e0ede-166">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="e0ede-166">Trigger a function manually</span></span>
* <span data-ttu-id="e0ede-167">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="e0ede-167">Write logs</span></span>

## <span data-ttu-id="e0ede-168"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0ede-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="e0ede-169">本指南提供了程式碼範例，示範如何處理使用 Azure Service Bus 的常見案例。</span><span class="sxs-lookup"><span data-stu-id="e0ede-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="e0ede-170">如需 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="e0ede-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

