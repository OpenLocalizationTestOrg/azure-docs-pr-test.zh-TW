---
title: "Azure Service Bus 訊息佇列、 主題和訂用帳戶的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a><span data-ttu-id="b4f48-103">服務匯流排佇列、主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b4f48-103">Service Bus queues, topics, and subscriptions</span></span>

<span data-ttu-id="b4f48-104">Microsoft Azure 服務匯流排支援一組以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-104">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="b4f48-105">這些 「 代理 」 訊息功能可以被視為低耦合訊息支援發行-訂閱的功能、 時態解除結合及負載平衡案例使用 hello 服務匯流排傳訊網狀架構。</span><span class="sxs-lookup"><span data-stu-id="b4f48-105">These "brokered" messaging capabilities can be thought of as decoupled messaging features that support publish-subscribe, temporal decoupling, and load balancing scenarios using hello Service Bus messaging fabric.</span></span> <span data-ttu-id="b4f48-106">低耦合通訊有許多優點︰例如，用戶端和伺服器可視需要連接並以非同步方式執行其作業。</span><span class="sxs-lookup"><span data-stu-id="b4f48-106">Decoupled communication has many advantages; for example, clients and servers can connect as needed and perform their operations in an asynchronous fashion.</span></span>

<span data-ttu-id="b4f48-107">hello 訊息實體所構成訊息功能，在 Service Bus 中的 hello 核心是 hello 的佇列、 主題和訂閱和規則/動作。</span><span class="sxs-lookup"><span data-stu-id="b4f48-107">hello messaging entities that form hello core of hello messaging capabilities in Service Bus are queues, topics and subscriptions, and rules/actions.</span></span>

## <a name="queues"></a><span data-ttu-id="b4f48-108">佇列</span><span class="sxs-lookup"><span data-stu-id="b4f48-108">Queues</span></span>

<span data-ttu-id="b4f48-109">佇列提供*先進先出*(FIFO) 訊息傳遞 tooone 或更多的競爭取用者。</span><span class="sxs-lookup"><span data-stu-id="b4f48-109">Queues offer *First In, First Out* (FIFO) message delivery tooone or more competing consumers.</span></span> <span data-ttu-id="b4f48-110">也就是說，訊息是通常預期的 toobe 接收和處理由 hello 接收者 hello 順序，在其中加入 toohello 佇列，以及每個訊息是接收並處理一個訊息取用者。</span><span class="sxs-lookup"><span data-stu-id="b4f48-110">That is, messages are typically expected toobe received and processed by hello receivers in hello order in which they were added toohello queue, and each message is received and processed by only one message consumer.</span></span> <span data-ttu-id="b4f48-111">使用佇列的主要優點是 tooachieve 「 時間解除結合 」 的應用程式元件。</span><span class="sxs-lookup"><span data-stu-id="b4f48-111">A key benefit of using queues is tooachieve "temporal decoupling" of application components.</span></span> <span data-ttu-id="b4f48-112">換句話說，hello 產生者 （傳送者） 和消費者 （接收者） 不需要 toobe 傳送和接收訊息在 hello 相同的時間，因為訊息長期儲存 hello 佇列中。</span><span class="sxs-lookup"><span data-stu-id="b4f48-112">In other words, hello producers (senders) and consumers (receivers) do not have toobe sending and receiving messages at hello same time, because messages are stored durably in hello queue.</span></span> <span data-ttu-id="b4f48-113">此外，hello 生產者沒有 toowait hello 消費者的回覆順序 toocontinue tooprocess 中，以及傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-113">Furthermore, hello producer does not have toowait for a reply from hello consumer in order toocontinue tooprocess and send messages.</span></span>

<span data-ttu-id="b4f48-114">相關的優點是 「 負載調節 」 這可讓產生者和消費者 toosend 和接收訊息至不同的費率。</span><span class="sxs-lookup"><span data-stu-id="b4f48-114">A related benefit is "load leveling," which enables producers and consumers toosend and receive messages at different rates.</span></span> <span data-ttu-id="b4f48-115">在許多應用程式，hello 系統負載會隨著時間;不過，所需每個工作單位的 hello 處理時間通常不變。</span><span class="sxs-lookup"><span data-stu-id="b4f48-115">In many applications, hello system load varies over time; however, hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="b4f48-116">調解訊息產生者和消費者與佇列表示耗用僅應用程式的 hello toobe 佈建的 toobe 無法 toohandle 平均負載而非尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="b4f48-116">Intermediating message producers and consumers with a queue means that hello consuming application only has toobe provisioned toobe able toohandle average load instead of peak load.</span></span> <span data-ttu-id="b4f48-117">hello 深度 hello 佇列成長，且合約會隨著 hello 連入負載而改變。</span><span class="sxs-lookup"><span data-stu-id="b4f48-117">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="b4f48-118">這與基礎結構需要的 tooservice hello 應用程式負載而考慮 toohello 數量可直接節省金錢。</span><span class="sxs-lookup"><span data-stu-id="b4f48-118">This directly saves money with regard toohello amount of infrastructure required tooservice hello application load.</span></span> <span data-ttu-id="b4f48-119">為 hello 負載增加，多個背景工作處理序可以是加入的 tooread hello 佇列中。</span><span class="sxs-lookup"><span data-stu-id="b4f48-119">As hello load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="b4f48-120">只有其中一個 hello 背景工作處理序處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-120">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="b4f48-121">此外，此提取為基礎的負載平衡能充分利用 hello 背景工作電腦即使 hello 背景工作電腦不同而考慮 tooprocessing 電源，因為它們會在他們自己的最大速率提取訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-121">Furthermore, this pull-based load balancing allows for optimum use of hello worker computers even if hello worker computers differ with regard tooprocessing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="b4f48-122">此模式通常稱為 hello 「 競爭消費者 」 模式。</span><span class="sxs-lookup"><span data-stu-id="b4f48-122">This pattern is often termed hello "competing consumer" pattern.</span></span>

<span data-ttu-id="b4f48-123">使用訊息產生者與取用者之間的佇列 toointermediate 提供 hello 元件之間的固有鬆散結合。</span><span class="sxs-lookup"><span data-stu-id="b4f48-123">Using queues toointermediate between message producers and consumers provides an inherent loose coupling between hello components.</span></span> <span data-ttu-id="b4f48-124">因為產生者和消費者不知道彼此的存在，取用者可以在 hello 生產者影響的情況下升級。</span><span class="sxs-lookup"><span data-stu-id="b4f48-124">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on hello producer.</span></span>

<span data-ttu-id="b4f48-125">建立佇列是一個多步驟的程序。</span><span class="sxs-lookup"><span data-stu-id="b4f48-125">Creating a queue is a multi-step process.</span></span> <span data-ttu-id="b4f48-126">執行管理作業，如 Service Bus 訊息實體 （佇列和主題） 透過 hello [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)類別，建構藉由提供基底位址 hello Service Bus hello命名空間和 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="b4f48-126">You perform management operations for Service Bus messaging entities (both queues and topics) via hello [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, which is constructed by supplying hello base address of hello Service Bus namespace and hello user credentials.</span></span> <span data-ttu-id="b4f48-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)提供方法 toocreate 列舉和刪除訊息實體。</span><span class="sxs-lookup"><span data-stu-id="b4f48-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) provides methods toocreate, enumerate and delete messaging entities.</span></span> <span data-ttu-id="b4f48-128">在建立之後[Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) hello SAS 名稱和金鑰，以及服務命名空間管理來自物件的物件，您可以使用 hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_)方法 toocreate hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="b4f48-128">After creating a [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object from hello SAS name and key, and a service namespace management object, you can use hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method toocreate hello queue.</span></span> <span data-ttu-id="b4f48-129">例如：</span><span class="sxs-lookup"><span data-stu-id="b4f48-129">For example:</span></span>

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

<span data-ttu-id="b4f48-130">然後您可以建立佇列物件和訊息 factory 以 hello 服務匯流排 URI 做為引數。</span><span class="sxs-lookup"><span data-stu-id="b4f48-130">You can then create a queue object and a messaging factory with hello Service Bus URI as an argument.</span></span> <span data-ttu-id="b4f48-131">例如：</span><span class="sxs-lookup"><span data-stu-id="b4f48-131">For example:</span></span>

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

<span data-ttu-id="b4f48-132">然後，您可以傳送郵件 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="b4f48-132">You can then send messages toohello queue.</span></span> <span data-ttu-id="b4f48-133">例如，如果您有呼叫代理訊息清單`MessageList`，hello 程式碼會顯示類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b4f48-133">For example, if you have a list of brokered messages called `MessageList`, hello code appears similar toohello following:</span></span>

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

<span data-ttu-id="b4f48-134">您再從佇列接收訊息 hello，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4f48-134">You then receive messages from hello queue as follows:</span></span>

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

<span data-ttu-id="b4f48-135">在 hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式，hello 接收作業是單發式的也就是服務匯流排收到 hello 要求時，它會標示為正在使用的 hello 訊息，並傳回它 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4f48-135">In hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, hello receive operation is single-shot; that is, when Service Bus receives hello request, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="b4f48-136">**ReceiveAndDelete**模式是 hello 簡單的模式，最適合用於中的 hello 應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="b4f48-136">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which hello application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="b4f48-137">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="b4f48-137">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="b4f48-138">因為服務匯流排會標示為正在使用，當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="b4f48-138">Because Service Bus marks hello message as being consumed, when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="b4f48-139">在[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式，hello 接收作業變成兩階段，讓它不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4f48-139">In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, hello receive operation becomes two-stage, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b4f48-140">服務匯流排收到 hello 要求時，它找到 hello 耗用下一個訊息 toobe、 tooprevent 將它鎖定，接收其他取用者，然後傳回 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4f48-140">When Service Bus receives hello request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="b4f48-141">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)上收到 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-141">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on hello received message.</span></span> <span data-ttu-id="b4f48-142">當服務匯流排會看見 hello**完成**呼叫時，它會將標示為正在使用的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-142">When Service Bus sees hello **Complete** call, it marks hello message as being consumed.</span></span>

<span data-ttu-id="b4f48-143">如果 hello 應用程式無法 tooprocess hello 訊息，因為某些原因，它可以呼叫 hello[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)收到 hello 訊息上的方法 (而不是[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete))。</span><span class="sxs-lookup"><span data-stu-id="b4f48-143">If hello application is unable tooprocess hello message for some reason, it can call hello [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) method on hello received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="b4f48-144">這可讓服務匯流排 toounlock hello 訊息，並讓它再次接收可用 toobe、 由 hello 相同的消費者或其他競爭消費者。</span><span class="sxs-lookup"><span data-stu-id="b4f48-144">This enables Service Bus toounlock hello message and make it available toobe received again, either by hello same consumer or by another competing consumer.</span></span> <span data-ttu-id="b4f48-145">其次，那里已逾時與鎖定相關聯 hello 和 hello 應用程式如果無法 tooprocess hello 訊息 hello 鎖定逾時到期前 （例如，如果 hello 應用程式當機），則服務匯流排解除鎖定 hello 訊息，並使其可用 toobe接收一次 (基本上執行[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)作業依預設)。</span><span class="sxs-lookup"><span data-stu-id="b4f48-145">Secondly, there is a timeout associated with hello lock and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message and makes it available toobe received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="b4f48-146">請注意，在 hello hello 應用程式的事件發生當機之後處理 hello 訊息，但之前 hello**完成**發出要求，hello 訊息已重新傳遞的 toohello 應用程式重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="b4f48-146">Note that in hello event that hello application crashes after processing hello message, but before hello **Complete** request is issued, hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="b4f48-147">這通常稱為「至少一次」處理機制；也就是說，會至少將每個訊息都處理一次。</span><span class="sxs-lookup"><span data-stu-id="b4f48-147">This is often called *At Least Once* processing; that is, each message is processed at least once.</span></span> <span data-ttu-id="b4f48-148">不過，在某些情況下 hello 可能傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-148">However, in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="b4f48-149">如果 hello 案例無法容許重複處理，則需要額外的邏輯在 hello 應用程式 toodetect 重複項目可以根據 hello 達成**MessageId** hello 訊息，會保留屬性所有傳遞嘗試的常數。</span><span class="sxs-lookup"><span data-stu-id="b4f48-149">If hello scenario cannot tolerate duplicate processing, then additional logic is required in hello application toodetect duplicates which can be achieved based upon hello **MessageId** property of hello message, which remains constant across delivery attempts.</span></span> <span data-ttu-id="b4f48-150">這就是所謂的「剛好一次」處理。</span><span class="sxs-lookup"><span data-stu-id="b4f48-150">This is known as *Exactly Once* processing.</span></span>

## <a name="topics-and-subscriptions"></a><span data-ttu-id="b4f48-151">主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b4f48-151">Topics and subscriptions</span></span>
<span data-ttu-id="b4f48-152">在對比 tooqueues，在每個訊息處理由單一消費者，*主題*和*訂閱*-一對多通訊的形式，提供在*發佈/訂閱*模式。</span><span class="sxs-lookup"><span data-stu-id="b4f48-152">In contrast tooqueues, in which each message is processed by a single consumer, *topics* and *subscriptions* provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="b4f48-153">適用於調整 toovery 收件者數目很大，每個已發行的訊息是由可用 tooeach 註冊 hello 主題的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4f48-153">Useful for scaling toovery large numbers of recipients, each published message is made available tooeach subscription registered with hello topic.</span></span> <span data-ttu-id="b4f48-154">Tooa 主題和傳遞的 tooone 或更多相關聯的訂閱，根據您可以將每個訂用帳戶為基礎的篩選規則，會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-154">Messages are sent tooa topic and delivered tooone or more associated subscriptions, depending on filter rules that can be set on a per-subscription basis.</span></span> <span data-ttu-id="b4f48-155">hello 訂閱可以使用其他篩選 toorestrict hello 訊息，他們想 tooreceive。</span><span class="sxs-lookup"><span data-stu-id="b4f48-155">hello subscriptions can use additional filters toorestrict hello messages that they want tooreceive.</span></span> <span data-ttu-id="b4f48-156">訊息會傳送 tooa 主題在 hello 相同方式會傳送它們 tooa 佇列，但會在收到訊息從 hello 主題直接。</span><span class="sxs-lookup"><span data-stu-id="b4f48-156">Messages are sent tooa topic in hello same way they are sent tooa queue, but messages are not received from hello topic directly.</span></span> <span data-ttu-id="b4f48-157">反而會從訂用帳戶接收。</span><span class="sxs-lookup"><span data-stu-id="b4f48-157">Instead, they are received from subscriptions.</span></span> <span data-ttu-id="b4f48-158">主題訂閱類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。</span><span class="sxs-lookup"><span data-stu-id="b4f48-158">A topic subscription resembles a virtual queue that receives copies of hello messages that are sent toohello topic.</span></span> <span data-ttu-id="b4f48-159">訊息會從訂閱接收相同 toohello 方法已從佇列接收。</span><span class="sxs-lookup"><span data-stu-id="b4f48-159">Messages are received from a subscription identically toohello way they are received from a queue.</span></span>

<span data-ttu-id="b4f48-160">透過比較，hello 訊息傳送功能佇列對應直接 tooa 主題，而其訊息接收功能對應 tooa 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4f48-160">By way of comparison, hello message-sending functionality of a queue maps directly tooa topic and its message-receiving functionality maps tooa subscription.</span></span> <span data-ttu-id="b4f48-161">除此之外，這表示訂閱支援的 hello 與考慮 tooqueues 本章節稍早描述相同的模式： 競爭消費者、 時間解除結合、 負載調節和負載平衡。</span><span class="sxs-lookup"><span data-stu-id="b4f48-161">Among other things, this means that subscriptions support hello same patterns described earlier in this section with regard tooqueues: competing consumer, temporal decoupling, load leveling, and load balancing.</span></span>

<span data-ttu-id="b4f48-162">建立主題為類似 toocreating 佇列，hello 前一節中的 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="b4f48-162">Creating a topic is similar toocreating a queue, as shown in hello example in hello previous section.</span></span> <span data-ttu-id="b4f48-163">建立 hello 服務 URI，然後再使用 hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)類別 toocreate hello 命名空間的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b4f48-163">Create hello service URI, and then use hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class toocreate hello namespace client.</span></span> <span data-ttu-id="b4f48-164">然後，您可以建立主題，使用 hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_)方法。</span><span class="sxs-lookup"><span data-stu-id="b4f48-164">You can then create a topic using hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method.</span></span> <span data-ttu-id="b4f48-165">例如：</span><span class="sxs-lookup"><span data-stu-id="b4f48-165">For example:</span></span>

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="b4f48-166">接下來，新增所需的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="b4f48-166">Next, add subscriptions as desired:</span></span>

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

<span data-ttu-id="b4f48-167">您可以接著建立主題用戶端。</span><span class="sxs-lookup"><span data-stu-id="b4f48-167">You can then create a topic client.</span></span> <span data-ttu-id="b4f48-168">例如：</span><span class="sxs-lookup"><span data-stu-id="b4f48-168">For example:</span></span>

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

<span data-ttu-id="b4f48-169">使用 hello 訊息寄件者，您可以傳送和訊息 tooand 收到 hello 主題 hello 上一節中所示。</span><span class="sxs-lookup"><span data-stu-id="b4f48-169">Using hello message sender, you can send and receive messages tooand from hello topic, as shown in hello previous section.</span></span> <span data-ttu-id="b4f48-170">例如：</span><span class="sxs-lookup"><span data-stu-id="b4f48-170">For example:</span></span>

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

<span data-ttu-id="b4f48-171">類似 tooqueues，訊息來自訂用帳戶使用[SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient)物件而非[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)物件。</span><span class="sxs-lookup"><span data-stu-id="b4f48-171">Similar tooqueues, messages are received from a subscription using a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object instead of a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object.</span></span> <span data-ttu-id="b4f48-172">建立 hello 訂閱用戶端，傳送 hello hello 主題，hello hello 訂用帳戶名稱，名稱和 （選擇性） hello 接收模式做為參數。</span><span class="sxs-lookup"><span data-stu-id="b4f48-172">Create hello subscription client, passing hello name of hello topic, hello name of hello subscription, and (optionally) hello receive mode as parameters.</span></span> <span data-ttu-id="b4f48-173">例如，以 hello**清查**訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="b4f48-173">For example, with hello **Inventory** subscription:</span></span>

```csharp
// Create hello subscription client
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

### <a name="rules-and-actions"></a><span data-ttu-id="b4f48-174">執行和動作</span><span class="sxs-lookup"><span data-stu-id="b4f48-174">Rules and actions</span></span>
<span data-ttu-id="b4f48-175">在許多情況下，必須以不同的方式處理具有特定特性的訊息。</span><span class="sxs-lookup"><span data-stu-id="b4f48-175">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="b4f48-176">tooenable，您可以設定訂閱 toofind 訊息，具有所需的屬性，然後再執行特定修改 toothose 屬性。</span><span class="sxs-lookup"><span data-stu-id="b4f48-176">tooenable this, you can configure subscriptions toofind messages that have desired properties and then perform certain modifications toothose properties.</span></span> <span data-ttu-id="b4f48-177">服務匯流排訂閱可看見所有傳送 toohello 主題的訊息，而您僅能複製這些訊息 toohello 虛擬訂閱佇列的子集。</span><span class="sxs-lookup"><span data-stu-id="b4f48-177">While Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="b4f48-178">使用訂用帳戶篩選器即可達成。</span><span class="sxs-lookup"><span data-stu-id="b4f48-178">This is accomplished using subscription filters.</span></span> <span data-ttu-id="b4f48-179">這類修改稱之為「篩選器動作」。</span><span class="sxs-lookup"><span data-stu-id="b4f48-179">Such modifications are called *filter actions*.</span></span> <span data-ttu-id="b4f48-180">建立訂用帳戶時，您可以提供 hello hello 訊息屬性運作的篩選運算式，兩者 hello 系統屬性 (例如，**標籤**) 和自訂應用程式屬性 (例如， **StoreName**。) hello SQL 篩選運算式是選擇性的在此情況下。SQL 篩選運算式，沒有任何訂用帳戶上所定義的篩選器動作將會執行所有的 hello 訊息，該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4f48-180">When a subscription is created, you can supply a filter expression that operates on hello properties of hello message, both hello system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) hello SQL filter expression is optional in this case; without a SQL filter expression, any filter action defined on a subscription will be performed on all hello messages for that subscription.</span></span>

<span data-ttu-id="b4f48-181">使用 hello 上述範例中，只有來自 toofilter 訊息**Store1**，您會建立 hello 儀表板訂用帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4f48-181">Using hello previous example, toofilter messages coming only from **Store1**, you would create hello Dashboard subscription as follows:</span></span>

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

<span data-ttu-id="b4f48-182">只有具有 hello 訊息的位置，此訂閱篩選`StoreName`屬性設定太`Store1`會複製的 toohello 虛擬佇列 hello`Dashboard`訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4f48-182">With this subscription filter in place, only messages that have hello `StoreName` property set too`Store1` are copied toohello virtual queue for hello `Dashboard` subscription.</span></span>

<span data-ttu-id="b4f48-183">如需可能的篩選值的詳細資訊，請參閱 hello 文件以 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)和[SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)類別。</span><span class="sxs-lookup"><span data-stu-id="b4f48-183">For more information about possible filter values, see hello documentation for hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) and [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes.</span></span> <span data-ttu-id="b4f48-184">此外，請參閱 hello[代理訊息： 進階篩選器](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)和[主題篩選](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters)範例。</span><span class="sxs-lookup"><span data-stu-id="b4f48-184">Also, see hello [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) and [Topic Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4f48-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4f48-185">Next steps</span></span>
<span data-ttu-id="b4f48-186">Hello 下列進階主題，如需詳細資訊和使用服務匯流排傳訊的範例，請參閱。</span><span class="sxs-lookup"><span data-stu-id="b4f48-186">See hello following advanced topics for more information and examples of using Service Bus messaging.</span></span>

* [<span data-ttu-id="b4f48-187">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="b4f48-187">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="b4f48-188">服務匯流排代理傳訊 .NET 教學課程</span><span class="sxs-lookup"><span data-stu-id="b4f48-188">Service Bus brokered messaging .NET tutorial</span></span>](service-bus-brokered-tutorial-dotnet.md)
* [<span data-ttu-id="b4f48-189">服務匯流排代理傳訊 REST 教學課程</span><span class="sxs-lookup"><span data-stu-id="b4f48-189">Service Bus brokered messaging REST tutorial</span></span>](service-bus-brokered-tutorial-rest.md)
* [<span data-ttu-id="b4f48-190">主題篩選器範例</span><span class="sxs-lookup"><span data-stu-id="b4f48-190">Topic Filters sample </span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [<span data-ttu-id="b4f48-191">代理傳訊︰進階篩選器範例</span><span class="sxs-lookup"><span data-stu-id="b4f48-191">Brokered Messaging: Advanced Filters sample</span></span>](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

