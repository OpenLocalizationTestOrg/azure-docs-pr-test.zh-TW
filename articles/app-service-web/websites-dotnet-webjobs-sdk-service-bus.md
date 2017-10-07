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
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a><span data-ttu-id="fd60d-103">如何 toouse Azure 服務匯流排與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="fd60d-103">How toouse Azure Service Bus with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="fd60d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="fd60d-104">Overview</span></span>
<span data-ttu-id="fd60d-105">本指南提供 C# 程式碼範例會顯示如何 tootrigger 收到 Azure 服務匯流排訊息時的處理序。</span><span class="sxs-lookup"><span data-stu-id="fd60d-105">This guide provides C# code samples that show how tootrigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="fd60d-106">hello 程式碼範例使用[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="fd60d-106">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="fd60d-107">hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="fd60d-108">hello 程式碼片段只會顯示函式，不 hello 程式碼會建立 hello`JobHost`物件，如此範例所示：</span><span class="sxs-lookup"><span data-stu-id="fd60d-108">hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="fd60d-109">A[完成的服務匯流排程式碼範例](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs)上 GitHub.com hello azure webjobs sdk 的範例儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="fd60d-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in hello azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="fd60d-110"><a id="prerequisites"></a> 必要條件</span><span class="sxs-lookup"><span data-stu-id="fd60d-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="fd60d-111">toowork 您尚未使用服務匯流排 tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 封裝除了 toohello 其他 WebJobs SDK 封裝。</span><span class="sxs-lookup"><span data-stu-id="fd60d-111">toowork with Service Bus you have tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition toohello other WebJobs SDK packages.</span></span> 

<span data-ttu-id="fd60d-112">您也可以 tooset hello AzureWebJobsServiceBus 連接字串中加入 toohello 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="fd60d-112">You also have tooset hello AzureWebJobsServiceBus connection string in addition toohello storage connection strings.</span></span>  <span data-ttu-id="fd60d-113">您可以在 hello`connectionStrings`區段 hello App.config 檔案，如下列範例中的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="fd60d-113">You can do this in hello `connectionStrings` section of hello App.config file, as shown in hello following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="fd60d-114">包含在 hello App.config 檔案中的 hello 服務匯流排連接字串設定為範例專案，請參閱[服務匯流排範例](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-114">For a sample project that includes hello Service Bus connection string setting in hello App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="fd60d-115">hello 連接字串也可以設定在 hello Azure 執行階段環境中，然後在 hello WebJob 會執行於 Azure; 時，覆寫 hello App.config 設定如需詳細資訊，請參閱[hello WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-115">hello connection strings can also be set in hello Azure runtime environment, which then overrides hello App.config settings when hello WebJob runs in Azure; for more information, see [Get Started with hello WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="fd60d-116"><a id="trigger"></a>收到 tootrigger 函式時，服務匯流排佇列訊息的方式</span><span class="sxs-lookup"><span data-stu-id="fd60d-116"><a id="trigger"></a> How tootrigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="fd60d-117">toowrite hello WebJobs SDK 的函式呼叫接收佇列訊息時，請使用 hello`ServiceBusTrigger`屬性。</span><span class="sxs-lookup"><span data-stu-id="fd60d-117">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="fd60d-118">hello 屬性建構函式會使用參數來指定 hello 佇列 toopoll hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="fd60d-118">hello attribute constructor takes a parameter that specifies hello name of hello queue toopoll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="fd60d-119">ServiceBusTrigger 的運作方式</span><span class="sxs-lookup"><span data-stu-id="fd60d-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="fd60d-120">hello SDK 收到訊息時在`PeekLock`模式和呼叫`Complete`hello 訊息，如果成功，完成 hello 函式或呼叫`Abandon`如果 hello 函式失敗。</span><span class="sxs-lookup"><span data-stu-id="fd60d-120">hello SDK receives a message in `PeekLock` mode and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> <span data-ttu-id="fd60d-121">如果 hello 函式執行時間長於 hello `PeekLock` hello 鎖定逾時，會自動更新。</span><span class="sxs-lookup"><span data-stu-id="fd60d-121">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<span data-ttu-id="fd60d-122">服務匯流排執行它自己的有害佇列處理無法控制或 hello WebJobs SDK 所設定。</span><span class="sxs-lookup"><span data-stu-id="fd60d-122">Service Bus does its own poison queue handling which cannot be controlled or configured by hello WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="fd60d-123">字串佇列訊息</span><span class="sxs-lookup"><span data-stu-id="fd60d-123">String queue message</span></span>
<span data-ttu-id="fd60d-124">hello 下列程式碼範例會讀取佇列訊息，其中包含字串並寫入 hello 字串 toohello WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="fd60d-124">hello following code sample reads a queue message that contains a string and writes hello string toohello WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="fd60d-125">**注意：**如果您要建立 hello 訊息排入佇列，不會使用 hello WebJobs SDK 的應用程式中，請確定 tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx)太"text/plain"。</span><span class="sxs-lookup"><span data-stu-id="fd60d-125">**Note:** If you are creating hello queue messages in an application that doesn't use hello WebJobs SDK, make sure tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) too"text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="fd60d-126">POCO 佇列訊息</span><span class="sxs-lookup"><span data-stu-id="fd60d-126">POCO queue message</span></span>
<span data-ttu-id="fd60d-127">hello SDK 會自動還原序列化的 POCO 包含 JSON 的佇列訊息[(純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 型別。</span><span class="sxs-lookup"><span data-stu-id="fd60d-127">hello SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="fd60d-128">hello 下列程式碼範例會讀取佇列訊息，其中包含`BlobInformation`含有物件`BlobName`屬性：</span><span class="sxs-lookup"><span data-stu-id="fd60d-128">hello following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="fd60d-129">如需程式碼範例顯示如何使用 blob 和資料表中的 hello POCO toowork toouse 屬性 hello 相同函式中，請參閱 hello[這篇文章的儲存體佇列版本](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-129">For code samples showing how toouse properties of hello POCO toowork with blobs and tables in hello same function, see hello [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="fd60d-130">如果您建立 hello 佇列訊息的程式碼不會使用 hello WebJobs SDK，請使用下列範例程式碼類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="fd60d-130">If your code that creates hello queue message doesn't use hello WebJobs SDK, use code similar toohello following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="fd60d-131">ServiceBusTrigger 使用的類型</span><span class="sxs-lookup"><span data-stu-id="fd60d-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="fd60d-132">除了`string`和 POCO 型別，您可以使用 hello`ServiceBusTrigger`的位元組陣列的屬性或`BrokeredMessage`物件。</span><span class="sxs-lookup"><span data-stu-id="fd60d-132">Besides `string` and POCO  types, you can use hello `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="fd60d-133"><a id="create"></a>Toocreate Service Bus 佇列訊息的方式</span><span class="sxs-lookup"><span data-stu-id="fd60d-133"><a id="create"></a> How toocreate Service Bus queue messages</span></span>
<span data-ttu-id="fd60d-134">toowrite 建立新的佇列訊息的函式使用 hello`ServiceBus`屬性，並傳入 hello 佇列名稱 toohello 屬性建構函式。</span><span class="sxs-lookup"><span data-stu-id="fd60d-134">toowrite a function that creates a new queue message use hello `ServiceBus` attribute and pass in hello queue name toohello attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="fd60d-135">在同步函數中建立單一佇列訊息</span><span class="sxs-lookup"><span data-stu-id="fd60d-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="fd60d-136">hello，下列程式碼範例會使用輸出參數 toocreate hello 佇列中的新訊息名為"outputqueue"hello 做為內容相同 hello 名為"inputqueue"hello 佇列中接收訊息。</span><span class="sxs-lookup"><span data-stu-id="fd60d-136">hello following code sample uses an output parameter toocreate a new message in hello queue named "outputqueue" with hello same content as hello message received in hello queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="fd60d-137">hello 輸出參數，以建立單一佇列訊息可以是 hello 的任何下列類型:</span><span class="sxs-lookup"><span data-stu-id="fd60d-137">hello output parameter for creating a single queue message can be any of hello following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="fd60d-138">您定義的可序列化 POCO 類型。</span><span class="sxs-lookup"><span data-stu-id="fd60d-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="fd60d-139">自動序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="fd60d-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="fd60d-140">POCO 型別參數，佇列訊息時一律會建立 hello 函式會結束。hello 參數為 null，如果 hello SDK 建立的佇列訊息，收到 hello 訊息並將其還原序列化時將會傳回 null。</span><span class="sxs-lookup"><span data-stu-id="fd60d-140">For POCO type parameters, a queue message is always created when hello function ends; if hello parameter is null, hello SDK creates a queue message that will return null when hello message is received and deserialized.</span></span> <span data-ttu-id="fd60d-141">如 hello 其他類型，如果 hello 參數為 null 會建立任何佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="fd60d-141">For hello other types, if hello parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="fd60d-142">建立多個佇列訊息或在非同步函式中</span><span class="sxs-lookup"><span data-stu-id="fd60d-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="fd60d-143">toocreate 多則訊息，使用 hello`ServiceBus`屬性附帶`ICollector<T>`或`IAsyncCollector<T>`hello 下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="fd60d-143">toocreate multiple messages, use  hello `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="fd60d-144">每個佇列的訊息建立時立即 hello`Add`方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="fd60d-144">Each queue message is created immediately when hello `Add` method is called.</span></span>

## <span data-ttu-id="fd60d-145"><a id="topics"></a>如何與 Service Bus 主題 toowork</span><span class="sxs-lookup"><span data-stu-id="fd60d-145"><a id="topics"></a>How toowork with Service Bus topics</span></span>
<span data-ttu-id="fd60d-146">toowrite hello SDK 函式會呼叫服務匯流排主題接收訊息時，請使用 hello `ServiceBusTrigger` hello 建構函式會採用主題名稱與訂用帳戶名稱，hello 下列程式碼範例所示的屬性：</span><span class="sxs-lookup"><span data-stu-id="fd60d-146">toowrite a function that hello SDK calls when a message is received on a Service Bus topic, use hello `ServiceBusTrigger` attribute with hello constructor that takes topic name and subscription name, as shown in hello following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="fd60d-147">toocreate 主題時，使用 hello 訊息`ServiceBus`屬性以主題名稱 hello 相同方式使用佇列的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd60d-147">toocreate a message on a topic, use hello `ServiceBus` attribute with a topic name hello same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="fd60d-148">在 1.1 版中新增的功能</span><span class="sxs-lookup"><span data-stu-id="fd60d-148">Features added in release 1.1</span></span>
<span data-ttu-id="fd60d-149">1.1 版中新增下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd60d-149">hello following features were added in release 1.1:</span></span>

* <span data-ttu-id="fd60d-150">允許透過 `ServiceBusConfiguration.MessagingProvider`深層自訂訊息處理。</span><span class="sxs-lookup"><span data-stu-id="fd60d-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="fd60d-151">`MessagingProvider`支援自訂 hello Service Bus`MessagingFactory`和`NamespaceManager`。</span><span class="sxs-lookup"><span data-stu-id="fd60d-151">`MessagingProvider` supports customization of hello Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="fd60d-152">A`MessageProcessor`策略模式可讓您 toospecify 每個佇列/主題的處理器。</span><span class="sxs-lookup"><span data-stu-id="fd60d-152">A `MessageProcessor` strategy pattern allows you toospecify a processor per queue/topic.</span></span>
* <span data-ttu-id="fd60d-153">訊息處理並行依預設支援。</span><span class="sxs-lookup"><span data-stu-id="fd60d-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="fd60d-154">透過 `ServiceBusConfiguration.MessageOptions` 輕鬆自訂 `OnMessageOptions`。</span><span class="sxs-lookup"><span data-stu-id="fd60d-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="fd60d-155">允許[AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe 上指定`ServiceBusTriggerAttribute` / `ServiceBusAttribute` （的情況下，您可能不需要管理權限）。</span><span class="sxs-lookup"><span data-stu-id="fd60d-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="fd60d-156">請注意，Azure WebJobs 無法 tooautomatically 佈建不存在佇列和主題不管理 AccessRights。</span><span class="sxs-lookup"><span data-stu-id="fd60d-156">Note that Azure WebJobs is unable tooautomatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="fd60d-157"><a id="queues"></a>Hello 儲存體佇列如何 tooarticle 所涵蓋的相關的主題</span><span class="sxs-lookup"><span data-stu-id="fd60d-157"><a id="queues"></a>Related topics covered by hello storage queues how-tooarticle</span></span>
<span data-ttu-id="fd60d-158">如需 WebJobs SDK 案例不是特定 tooService 匯流排，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-158">For information about WebJobs SDK scenarios not specific tooService Bus, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="fd60d-159">在該文件中涵蓋的主題包括下列 hello:</span><span class="sxs-lookup"><span data-stu-id="fd60d-159">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="fd60d-160">Async 函數</span><span class="sxs-lookup"><span data-stu-id="fd60d-160">Async functions</span></span>
* <span data-ttu-id="fd60d-161">多個執行個體</span><span class="sxs-lookup"><span data-stu-id="fd60d-161">Multiple instances</span></span>
* <span data-ttu-id="fd60d-162">正常關機</span><span class="sxs-lookup"><span data-stu-id="fd60d-162">Graceful shutdown</span></span>
* <span data-ttu-id="fd60d-163">使用 WebJobs SDK hello 函式主體中的屬性</span><span class="sxs-lookup"><span data-stu-id="fd60d-163">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="fd60d-164">程式碼中設定 hello SDK 連接字串</span><span class="sxs-lookup"><span data-stu-id="fd60d-164">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="fd60d-165">在程式碼中設定 WebJobs SDK 建構函式參數的值</span><span class="sxs-lookup"><span data-stu-id="fd60d-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="fd60d-166">手動觸發函式</span><span class="sxs-lookup"><span data-stu-id="fd60d-166">Trigger a function manually</span></span>
* <span data-ttu-id="fd60d-167">寫入記錄檔</span><span class="sxs-lookup"><span data-stu-id="fd60d-167">Write logs</span></span>

## <span data-ttu-id="fd60d-168"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd60d-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="fd60d-169">本指南提供的程式碼範例會顯示如何使用 Azure 服務匯流排 toohandle 常見案例。</span><span class="sxs-lookup"><span data-stu-id="fd60d-169">This guide has provided code samples that show how toohandle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="fd60d-170">如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。</span><span class="sxs-lookup"><span data-stu-id="fd60d-170">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

