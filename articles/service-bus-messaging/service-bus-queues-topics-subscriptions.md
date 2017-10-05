---
title: "Azure 服務匯流排傳訊佇列、主題和訂用帳戶的概觀 | Microsoft Docs"
description: "服務匯流排訊息實體的概觀。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 00f9f38fbae028486270053dedb4df580a3f1a44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a><span data-ttu-id="64a5f-103">服務匯流排佇列、主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="64a5f-103">Service Bus queues, topics, and subscriptions</span></span>

<span data-ttu-id="64a5f-104">Microsoft Azure 服務匯流排支援一組以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-104">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="64a5f-105">這些「代理」傳訊功能可以視為低耦合傳訊功能，這些功能可使用「服務匯流排」訊息網狀架構來支援發佈-訂閱、時脈解離及負載平衡案例。</span><span class="sxs-lookup"><span data-stu-id="64a5f-105">These "brokered" messaging capabilities can be thought of as decoupled messaging features that support publish-subscribe, temporal decoupling, and load balancing scenarios using the Service Bus messaging fabric.</span></span> <span data-ttu-id="64a5f-106">低耦合通訊有許多優點︰例如，用戶端和伺服器可視需要連接並以非同步方式執行其作業。</span><span class="sxs-lookup"><span data-stu-id="64a5f-106">Decoupled communication has many advantages; for example, clients and servers can connect as needed and perform their operations in an asynchronous fashion.</span></span>

<span data-ttu-id="64a5f-107">構成「服務匯流排」中傳訊功能核心的傳訊實體是佇列、主題與訂用帳戶，以及規則/動作。</span><span class="sxs-lookup"><span data-stu-id="64a5f-107">The messaging entities that form the core of the messaging capabilities in Service Bus are queues, topics and subscriptions, and rules/actions.</span></span>

## <a name="queues"></a><span data-ttu-id="64a5f-108">佇列</span><span class="sxs-lookup"><span data-stu-id="64a5f-108">Queues</span></span>

<span data-ttu-id="64a5f-109">如果有一或多個競爭取用者，佇列會採取「先進先出」(FIFO) 訊息傳遞機制。</span><span class="sxs-lookup"><span data-stu-id="64a5f-109">Queues offer *First In, First Out* (FIFO) message delivery to one or more competing consumers.</span></span> <span data-ttu-id="64a5f-110">亦即，通常預計由接收者依訊息加入佇列的順序來接收和處理訊息，而且每則訊息只能由一個訊息取用者接收和處理。</span><span class="sxs-lookup"><span data-stu-id="64a5f-110">That is, messages are typically expected to be received and processed by the receivers in the order in which they were added to the queue, and each message is received and processed by only one message consumer.</span></span> <span data-ttu-id="64a5f-111">使用佇列的主要優點是達成應用程式元件的「時脈解離」。</span><span class="sxs-lookup"><span data-stu-id="64a5f-111">A key benefit of using queues is to achieve "temporal decoupling" of application components.</span></span> <span data-ttu-id="64a5f-112">換句話說，產生者 (傳送者) 和取用者 (接收者) 不必同時傳送和接收訊息，因為訊息會長期儲存在佇列中。</span><span class="sxs-lookup"><span data-stu-id="64a5f-112">In other words, the producers (senders) and consumers (receivers) do not have to be sending and receiving messages at the same time, because messages are stored durably in the queue.</span></span> <span data-ttu-id="64a5f-113">此外，產生者不必等待取用者的回覆，即可繼續處理及傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-113">Furthermore, the producer does not have to wait for a reply from the consumer in order to continue to process and send messages.</span></span>

<span data-ttu-id="64a5f-114">相關的優點是「負載調節」，這可讓產生者和取用者以不同的速率傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-114">A related benefit is "load leveling," which enables producers and consumers to send and receive messages at different rates.</span></span> <span data-ttu-id="64a5f-115">在許多應用程式中，系統負載會隨時間改變；然而，處理每個工作單位所需的時間卻通常固定不變。</span><span class="sxs-lookup"><span data-stu-id="64a5f-115">In many applications, the system load varies over time; however, the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="64a5f-116">有佇列作為訊息生產者與取用者之間的中間者後，只需佈建取用方應用程式，就能夠處理平均負載而非尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="64a5f-116">Intermediating message producers and consumers with a queue means that the consuming application only has to be provisioned to be able to handle average load instead of peak load.</span></span> <span data-ttu-id="64a5f-117">佇列的深度會隨著連入負載的改變而增加和縮短。</span><span class="sxs-lookup"><span data-stu-id="64a5f-117">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="64a5f-118">就處理應用程式負載所需的基礎結構數量而言，如此可直接節省金錢。</span><span class="sxs-lookup"><span data-stu-id="64a5f-118">This directly saves money with regard to the amount of infrastructure required to service the application load.</span></span> <span data-ttu-id="64a5f-119">當負載增加時，可以新增更多的背景工作角色程序來讀取佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-119">As the load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="64a5f-120">每個訊息僅由其中一個背景工作程序處理。</span><span class="sxs-lookup"><span data-stu-id="64a5f-120">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="64a5f-121">此外，這個提取型負載平衡機制可讓背景工作電腦獲得最佳利用，即使背景工作電腦的處理能力有所不同也一樣，因為背景工作電腦將以自己的最大速率提取訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-121">Furthermore, this pull-based load balancing allows for optimum use of the worker computers even if the worker computers differ with regard to processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="64a5f-122">此模式通常稱為「競爭取用者」模式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-122">This pattern is often termed the "competing consumer" pattern.</span></span>

<span data-ttu-id="64a5f-123">使用佇列在訊息產生者與取用者之間居中協調，可提供元件之間的固有鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="64a5f-123">Using queues to intermediate between message producers and consumers provides an inherent loose coupling between the components.</span></span> <span data-ttu-id="64a5f-124">因為產生者和取用者不知道彼此的存在，所以取用者可以升級，而不會對產生者造成任何影響。</span><span class="sxs-lookup"><span data-stu-id="64a5f-124">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on the producer.</span></span>

<span data-ttu-id="64a5f-125">建立佇列是一個多步驟的程序。</span><span class="sxs-lookup"><span data-stu-id="64a5f-125">Creating a queue is a multi-step process.</span></span> <span data-ttu-id="64a5f-126">您會透過 [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別對服務匯流排傳訊實體 (佇列和主題) 執行管理作業，而該類別的建構方式為提供服務匯流排命名空間的基底位址和使用者認證。</span><span class="sxs-lookup"><span data-stu-id="64a5f-126">You perform management operations for Service Bus messaging entities (both queues and topics) via the [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, which is constructed by supplying the base address of the Service Bus namespace and the user credentials.</span></span> <span data-ttu-id="64a5f-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 提供用以建立、列舉及刪除訊息實體的方法。</span><span class="sxs-lookup"><span data-stu-id="64a5f-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) provides methods to create, enumerate and delete messaging entities.</span></span> <span data-ttu-id="64a5f-128">從 SAS 名稱和金鑰以及服務命名空間管理物件建立 [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 物件之後，您可以使用 [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) 方法來建立佇列。</span><span class="sxs-lookup"><span data-stu-id="64a5f-128">After creating a [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object from the SAS name and key, and a service namespace management object, you can use the [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method to create the queue.</span></span> <span data-ttu-id="64a5f-129">例如：</span><span class="sxs-lookup"><span data-stu-id="64a5f-129">For example:</span></span>

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

<span data-ttu-id="64a5f-130">您接著可以服務匯流排 URI 作為引數，建立佇列物件和訊息工廠。</span><span class="sxs-lookup"><span data-stu-id="64a5f-130">You can then create a queue object and a messaging factory with the Service Bus URI as an argument.</span></span> <span data-ttu-id="64a5f-131">例如：</span><span class="sxs-lookup"><span data-stu-id="64a5f-131">For example:</span></span>

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

<span data-ttu-id="64a5f-132">您接著可以將訊息傳送至佇列。</span><span class="sxs-lookup"><span data-stu-id="64a5f-132">You can then send messages to the queue.</span></span> <span data-ttu-id="64a5f-133">例如，如果您有稱為 `MessageList` 的代理訊息清單，程式碼會如下所示︰</span><span class="sxs-lookup"><span data-stu-id="64a5f-133">For example, if you have a list of brokered messages called `MessageList`, the code appears similar to the following:</span></span>

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

<span data-ttu-id="64a5f-134">您會接著從佇列接收訊息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64a5f-134">You then receive messages from the queue as follows:</span></span>

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

<span data-ttu-id="64a5f-135">在 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式中，接收是一次性作業；也就是說，當服務匯流排收到要求時，它會將此訊息標示為已取用，並將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-135">In the [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation is single-shot; that is, when Service Bus receives the request, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="64a5f-136">**ReceiveAndDelete** 模式是最簡單的模型，最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="64a5f-136">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which the application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="64a5f-137">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="64a5f-137">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="64a5f-138">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-138">Because Service Bus marks the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="64a5f-139">在 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式中，接收作業會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-139">In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation becomes two-stage, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="64a5f-140">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-140">When Service Bus receives the request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="64a5f-141">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫所接收訊息上的 [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) ，來完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="64a5f-141">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="64a5f-142">當服務匯流排看到 **Complete** 呼叫時，它會將訊息標示為已取用。</span><span class="sxs-lookup"><span data-stu-id="64a5f-142">When Service Bus sees the **Complete** call, it marks the message as being consumed.</span></span>

<span data-ttu-id="64a5f-143">如果應用程式因為某些原因無法處理訊息，它可以呼叫所接收訊息上的 [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 方法 (而不是 [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete))。</span><span class="sxs-lookup"><span data-stu-id="64a5f-143">If the application is unable to process the message for some reason, it can call the [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) method on the received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="64a5f-144">這可讓服務匯流排將訊息解除鎖定，讓此訊息可被相同的取用者或其他競爭取用取再次接收。</span><span class="sxs-lookup"><span data-stu-id="64a5f-144">This enables Service Bus to unlock the message and make it available to be received again, either by the same consumer or by another competing consumer.</span></span> <span data-ttu-id="64a5f-145">其次，鎖定有相關聯的逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會將訊息解除鎖定，並讓訊息可以被重新接收 (根據預設，基本上會執行 [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) 作業)。</span><span class="sxs-lookup"><span data-stu-id="64a5f-145">Secondly, there is a timeout associated with the lock and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message and makes it available to be received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="64a5f-146">請注意，如果應用程式在處理訊息之後，尚未發出 **Complete** 要求時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-146">Note that in the event that the application crashes after processing the message, but before the **Complete** request is issued, the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="64a5f-147">這通常稱為「至少一次」處理機制；也就是說，會至少將每個訊息都處理一次。</span><span class="sxs-lookup"><span data-stu-id="64a5f-147">This is often called *At Least Once* processing; that is, each message is processed at least once.</span></span> <span data-ttu-id="64a5f-148">不過，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-148">However, in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="64a5f-149">如果此案例不容許重複處理，則應用程式中需要額外的邏輯才能根據訊息的 **MessageId** 屬性偵測可達成的重複項目，而該屬性在所有傳遞嘗試中維持不變。</span><span class="sxs-lookup"><span data-stu-id="64a5f-149">If the scenario cannot tolerate duplicate processing, then additional logic is required in the application to detect duplicates which can be achieved based upon the **MessageId** property of the message, which remains constant across delivery attempts.</span></span> <span data-ttu-id="64a5f-150">這就是所謂的「剛好一次」處理。</span><span class="sxs-lookup"><span data-stu-id="64a5f-150">This is known as *Exactly Once* processing.</span></span>

## <a name="topics-and-subscriptions"></a><span data-ttu-id="64a5f-151">主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="64a5f-151">Topics and subscriptions</span></span>
<span data-ttu-id="64a5f-152">有別於佇列，佇列中的每個訊息只會由單一取用者處理，「主題」和「訂用帳戶」採用「發佈/訂閱」模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="64a5f-152">In contrast to queues, in which each message is processed by a single consumer, *topics* and *subscriptions* provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="64a5f-153">適合用於相應增加為非常大量的收件者，每個發佈的訊息都會提供給每個已註冊主題的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="64a5f-153">Useful for scaling to very large numbers of recipients, each published message is made available to each subscription registered with the topic.</span></span> <span data-ttu-id="64a5f-154">根據可依每個訂用帳戶設定的篩選規則，訊息會傳送至主題並傳遞給一或多個相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="64a5f-154">Messages are sent to a topic and delivered to one or more associated subscriptions, depending on filter rules that can be set on a per-subscription basis.</span></span> <span data-ttu-id="64a5f-155">訂用帳戶可以使用其他篩選器來限制他們想要接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-155">The subscriptions can use additional filters to restrict the messages that they want to receive.</span></span> <span data-ttu-id="64a5f-156">訊息會以其傳送至佇列的相同方式傳送至主題，但不會從主題直接接收訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-156">Messages are sent to a topic in the same way they are sent to a queue, but messages are not received from the topic directly.</span></span> <span data-ttu-id="64a5f-157">反而會從訂用帳戶接收。</span><span class="sxs-lookup"><span data-stu-id="64a5f-157">Instead, they are received from subscriptions.</span></span> <span data-ttu-id="64a5f-158">主題訂用帳戶類似於虛擬佇列，同樣可接收已傳送到主題的訊息複本。</span><span class="sxs-lookup"><span data-stu-id="64a5f-158">A topic subscription resembles a virtual queue that receives copies of the messages that are sent to the topic.</span></span> <span data-ttu-id="64a5f-159">從佇列接收訊息的方式就像從訂用帳戶接收訊息一樣。</span><span class="sxs-lookup"><span data-stu-id="64a5f-159">Messages are received from a subscription identically to the way they are received from a queue.</span></span>

<span data-ttu-id="64a5f-160">藉由比較，佇列的訊息傳送功能會直接對應至主題，而其訊息接收功能會對應至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="64a5f-160">By way of comparison, the message-sending functionality of a queue maps directly to a topic and its message-receiving functionality maps to a subscription.</span></span> <span data-ttu-id="64a5f-161">除此之外，這表示訂用帳戶支援本節前面所述有關佇列的相同模式︰競爭取用者、暫時分離、負載調節和負載平衡。</span><span class="sxs-lookup"><span data-stu-id="64a5f-161">Among other things, this means that subscriptions support the same patterns described earlier in this section with regard to queues: competing consumer, temporal decoupling, load leveling, and load balancing.</span></span>

<span data-ttu-id="64a5f-162">如上一節中的範例所示，建立主題類似於建立佇列。</span><span class="sxs-lookup"><span data-stu-id="64a5f-162">Creating a topic is similar to creating a queue, as shown in the example in the previous section.</span></span> <span data-ttu-id="64a5f-163">建立服務 URI，然後使用 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 類別來建立命名空間用戶端。</span><span class="sxs-lookup"><span data-stu-id="64a5f-163">Create the service URI, and then use the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class to create the namespace client.</span></span> <span data-ttu-id="64a5f-164">您可以接著使用 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 方法建立主題。</span><span class="sxs-lookup"><span data-stu-id="64a5f-164">You can then create a topic using the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method.</span></span> <span data-ttu-id="64a5f-165">例如：</span><span class="sxs-lookup"><span data-stu-id="64a5f-165">For example:</span></span>

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="64a5f-166">接下來，新增所需的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="64a5f-166">Next, add subscriptions as desired:</span></span>

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

<span data-ttu-id="64a5f-167">您可以接著建立主題用戶端。</span><span class="sxs-lookup"><span data-stu-id="64a5f-167">You can then create a topic client.</span></span> <span data-ttu-id="64a5f-168">例如：</span><span class="sxs-lookup"><span data-stu-id="64a5f-168">For example:</span></span>

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

<span data-ttu-id="64a5f-169">如前一節中所示，您可以使用訊息傳送者，從主題來回傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-169">Using the message sender, you can send and receive messages to and from the topic, as shown in the previous section.</span></span> <span data-ttu-id="64a5f-170">例如：</span><span class="sxs-lookup"><span data-stu-id="64a5f-170">For example:</span></span>

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

<span data-ttu-id="64a5f-171">與佇列類似，從訂用帳戶接收訊息是使用 [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) 物件，而非 [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) 物件。</span><span class="sxs-lookup"><span data-stu-id="64a5f-171">Similar to queues, messages are received from a subscription using a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object instead of a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object.</span></span> <span data-ttu-id="64a5f-172">建立訂用帳戶用戶端，並將主題名稱、訂用帳戶名稱及 (選擇性) 接收模式當作參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="64a5f-172">Create the subscription client, passing the name of the topic, the name of the subscription, and (optionally) the receive mode as parameters.</span></span> <span data-ttu-id="64a5f-173">例如，以 **Inventory** 訂用帳戶為例︰</span><span class="sxs-lookup"><span data-stu-id="64a5f-173">For example, with the **Inventory** subscription:</span></span>

```csharp
// Create the subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a><span data-ttu-id="64a5f-174">執行和動作</span><span class="sxs-lookup"><span data-stu-id="64a5f-174">Rules and actions</span></span>
<span data-ttu-id="64a5f-175">在許多情況下，必須以不同的方式處理具有特定特性的訊息。</span><span class="sxs-lookup"><span data-stu-id="64a5f-175">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="64a5f-176">若要這麼做，您可以設定訂用帳戶以尋找具有所需屬性的訊息，然後對這些屬性進行一些修改。</span><span class="sxs-lookup"><span data-stu-id="64a5f-176">To enable this, you can configure subscriptions to find messages that have desired properties and then perform certain modifications to those properties.</span></span> <span data-ttu-id="64a5f-177">雖然服務匯流排訂用帳戶可看見所有傳送至主題的訊息，但您只可以將部分的訊息複製到虛擬訂用帳戶佇列。</span><span class="sxs-lookup"><span data-stu-id="64a5f-177">While Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="64a5f-178">使用訂用帳戶篩選器即可達成。</span><span class="sxs-lookup"><span data-stu-id="64a5f-178">This is accomplished using subscription filters.</span></span> <span data-ttu-id="64a5f-179">這類修改稱之為「篩選器動作」。</span><span class="sxs-lookup"><span data-stu-id="64a5f-179">Such modifications are called *filter actions*.</span></span> <span data-ttu-id="64a5f-180">建立訂用帳戶後，您可以提供篩選運算式來處理訊息的屬性，包括系統屬性 (例如 **Label**) 和自訂應用程式屬性 (例如 **StoreName**)。在此情況下，SQL 篩選運算式是選擇性的；若沒有 SQL 篩選運算式，將會對訂用帳戶的所有訊息執行在該訂用帳戶上定義的所有篩選動作。</span><span class="sxs-lookup"><span data-stu-id="64a5f-180">When a subscription is created, you can supply a filter expression that operates on the properties of the message, both the system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) The SQL filter expression is optional in this case; without a SQL filter expression, any filter action defined on a subscription will be performed on all the messages for that subscription.</span></span>

<span data-ttu-id="64a5f-181">以上述範例為例，若只要篩選來自 **Store1** 的訊息，您可建立 Dashboard 訂用帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64a5f-181">Using the previous example, to filter messages coming only from **Store1**, you would create the Dashboard subscription as follows:</span></span>

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

<span data-ttu-id="64a5f-182">使用此訂用帳戶篩選器時，只有 `StoreName` 屬性設定為 `Store1` 的訊息才會複製到 `Dashboard` 訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="64a5f-182">With this subscription filter in place, only messages that have the `StoreName` property set to `Store1` are copied to the virtual queue for the `Dashboard` subscription.</span></span>

<span data-ttu-id="64a5f-183">如需可能篩選值的詳細資訊，請參閱 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 和 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 類別的文件。</span><span class="sxs-lookup"><span data-stu-id="64a5f-183">For more information about possible filter values, see the documentation for the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) and [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes.</span></span> <span data-ttu-id="64a5f-184">此外，請參閱[代理傳訊︰進階篩選器](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)和[主題篩選器](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters)範例。</span><span class="sxs-lookup"><span data-stu-id="64a5f-184">Also, see the [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) and [Topic Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64a5f-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64a5f-185">Next steps</span></span>
<span data-ttu-id="64a5f-186">如需詳細資訊及有關使用「服務匯流排」傳訊的範例，請參閱下列進階主題。</span><span class="sxs-lookup"><span data-stu-id="64a5f-186">See the following advanced topics for more information and examples of using Service Bus messaging.</span></span>

* [<span data-ttu-id="64a5f-187">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="64a5f-187">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="64a5f-188">服務匯流排代理傳訊 .NET 教學課程</span><span class="sxs-lookup"><span data-stu-id="64a5f-188">Service Bus brokered messaging .NET tutorial</span></span>](service-bus-brokered-tutorial-dotnet.md)
* [<span data-ttu-id="64a5f-189">服務匯流排代理傳訊 REST 教學課程</span><span class="sxs-lookup"><span data-stu-id="64a5f-189">Service Bus brokered messaging REST tutorial</span></span>](service-bus-brokered-tutorial-rest.md)
* [<span data-ttu-id="64a5f-190">主題篩選器範例</span><span class="sxs-lookup"><span data-stu-id="64a5f-190">Topic Filters sample </span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [<span data-ttu-id="64a5f-191">代理傳訊︰進階篩選器範例</span><span class="sxs-lookup"><span data-stu-id="64a5f-191">Brokered Messaging: Advanced Filters sample</span></span>](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

