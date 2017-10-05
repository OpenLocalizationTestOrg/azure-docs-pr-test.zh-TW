---
title: "建立使用 Azure 服務匯流排主題和訂用帳戶的應用程式 | Microsoft Docs"
description: "介紹服務匯流排主題和訂用帳戶所提供的發佈/訂閱功能。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: eb01120ce9578f716e5381c107faa93f0b36e358
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a><span data-ttu-id="63e12-103">建立使用服務匯流排主題和訂用帳戶的應用程式</span><span class="sxs-lookup"><span data-stu-id="63e12-103">Create applications that use Service Bus topics and subscriptions</span></span>
<span data-ttu-id="63e12-104">Azure 服務匯流排支援一套以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。</span><span class="sxs-lookup"><span data-stu-id="63e12-104">Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="63e12-105">本文是根據[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)所提供的資訊撰寫而成，並簡介服務匯流排主題所提供的發佈/訂閱功能。</span><span class="sxs-lookup"><span data-stu-id="63e12-105">This article builds on the information provided in [Create applications that use Service Bus queues](service-bus-create-queues.md) and offers an introduction to the publish/subscribe capabilities offered by Service Bus topics.</span></span>

## <a name="evolving-retail-scenario"></a><span data-ttu-id="63e12-106">不斷演變的零售案例</span><span class="sxs-lookup"><span data-stu-id="63e12-106">Evolving retail scenario</span></span>
<span data-ttu-id="63e12-107">本文會繼續運用[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中的零售案例。</span><span class="sxs-lookup"><span data-stu-id="63e12-107">This article continues the retail scenario used in [Create applications that use Service Bus queues](service-bus-create-queues.md).</span></span> <span data-ttu-id="63e12-108">請回想一下先前提過的，個別銷售點 (POS) 終端機的銷售資料，必須路由傳送至庫存管理系統，讓系統使用該資料來判斷何時必須補充庫存。</span><span class="sxs-lookup"><span data-stu-id="63e12-108">Recall that sales data from individual Point of Sale (POS) terminals must be routed to an inventory management system which uses that data to determine when stock has to be replenished.</span></span> <span data-ttu-id="63e12-109">每個 POS 終端機會將訊息傳送至 **DataCollectionQueue** 佇列，藉此回報其銷售資料，訊息會在佇列中持續保留，直到庫存管理系統收到為止，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63e12-109">Each POS terminal reports its sales data by sending messages to the **DataCollectionQueue** queue, where they remain until they are received by the inventory management system, as shown here:</span></span>

![服務匯流排 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

<span data-ttu-id="63e12-111">為了進一步演變此案例，我們已將新的要求加入至系統：商店老闆想要能夠即時監視商店的銷售業績。</span><span class="sxs-lookup"><span data-stu-id="63e12-111">To evolve this scenario, a new requirement has been added to the system: the store owner wants to be able to monitor how the store is performing in real time.</span></span>

<span data-ttu-id="63e12-112">為了滿足這項要求，系統必須「支開」銷售資料流。</span><span class="sxs-lookup"><span data-stu-id="63e12-112">To address this requirement, the system must "tap" off the sales data stream.</span></span> <span data-ttu-id="63e12-113">我們還是需要 POS 終端機傳送的每則訊息像之前一樣，傳送至庫存管理系統，但我們想要每則訊息的另一個複本，以便對商店老闆呈現儀表板檢視。</span><span class="sxs-lookup"><span data-stu-id="63e12-113">We still want each message sent by the POS terminals to be sent to the inventory management system as before, but we want another copy of each message that we can use to present the dashboard view to the store owner.</span></span>

<span data-ttu-id="63e12-114">在任何類似情況下，如果需要每則訊息是由多方取用，您可以使用服務匯流排「主題」。</span><span class="sxs-lookup"><span data-stu-id="63e12-114">In any situation such as this, in which you require each message to be consumed by multiple parties, you can use Service Bus *topics*.</span></span> <span data-ttu-id="63e12-115">主題提供發佈/訂閱模式，亦即每則發佈的訊息會提供給向主題註冊的一或多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e12-115">Topics provide a publish/subscribe pattern in which each published message is made available to one or more subscriptions registered with the topic.</span></span> <span data-ttu-id="63e12-116">相較之下，佇列是由單一取用者收到每則訊息。</span><span class="sxs-lookup"><span data-stu-id="63e12-116">In contrast, with queues each message is received by a single consumer.</span></span>

<span data-ttu-id="63e12-117">訊息傳送至主題的方式會與傳送至佇列的方式相同。</span><span class="sxs-lookup"><span data-stu-id="63e12-117">Messages are sent to a topic in the same way as they are sent to a queue.</span></span> <span data-ttu-id="63e12-118">不過，訊息不是直接從主題處接收；而是從訂用帳戶接收的。</span><span class="sxs-lookup"><span data-stu-id="63e12-118">However, messages are not received from the topic directly; they are received from subscriptions.</span></span> <span data-ttu-id="63e12-119">您可以將主題的訂用帳戶視為虛擬佇列，可接收已傳送到該主題的訊息複本。</span><span class="sxs-lookup"><span data-stu-id="63e12-119">You can think of a subscription to a topic as a virtual queue that receives copies of the messages that are sent to that topic.</span></span> <span data-ttu-id="63e12-120">從訂用帳戶接收訊息的方式與從佇列接收訊息的方式相同。</span><span class="sxs-lookup"><span data-stu-id="63e12-120">Messages are received from a subscription the same way as they are received from a queue.</span></span>

<span data-ttu-id="63e12-121">回到零售案例中，主題會取代佇列，而新增的訂用帳戶將可由庫存管理系統元件使用。</span><span class="sxs-lookup"><span data-stu-id="63e12-121">Going back to the retail scenario, the queue is replaced by a topic, and a subscription is added, which the inventory management system component can use.</span></span> <span data-ttu-id="63e12-122">系統現在看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="63e12-122">The system now appears as follows:</span></span>

![服務匯流排 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

<span data-ttu-id="63e12-124">這裡的組態會與先前以佇列為基礎的設計的運作方式完全相同。</span><span class="sxs-lookup"><span data-stu-id="63e12-124">The configuration here performs identically to the previous queue-based design.</span></span> <span data-ttu-id="63e12-125">也就是傳送至主題的訊息，會路由傳送至 **Inventory** 訂用帳戶，然後由**庫存管理系統**從中取用。</span><span class="sxs-lookup"><span data-stu-id="63e12-125">That is, messages sent to the topic are routed to the **Inventory** subscription, from which the **Inventory Management System** consumes them.</span></span>

<span data-ttu-id="63e12-126">為了支援管理儀表板，我們在主題上建立了第二個訂用帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63e12-126">In order to support the management dashboard, we create a second subscription on the topic, as shown here:</span></span>

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

<span data-ttu-id="63e12-128">在此組態中，來自 POS 終端機的每則訊息皆會提供給 **Dashboard** 和 **Inventory** 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e12-128">With this configuration, each message from the POS terminals is made available to both the **Dashboard** and **Inventory** subscriptions.</span></span>

## <a name="show-me-the-code"></a><span data-ttu-id="63e12-129">示範程式碼</span><span class="sxs-lookup"><span data-stu-id="63e12-129">Show me the code</span></span>
<span data-ttu-id="63e12-130">[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)文章中說明如何註冊 Azure 帳戶，並建立服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="63e12-130">The article [Create applications that use Service Bus queues](service-bus-create-queues.md) describes how to sign up for an Azure account and create a service namespace.</span></span> <span data-ttu-id="63e12-131">參考服務匯流排相依性的最簡單方式是，安裝服務匯流排 [Nuget 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)。</span><span class="sxs-lookup"><span data-stu-id="63e12-131">The easiest way to reference Service Bus dependencies is to install the Service Bus [Nuget package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/).</span></span> <span data-ttu-id="63e12-132">您也可以在 Azure SDK 中找到服務匯流排程式庫。</span><span class="sxs-lookup"><span data-stu-id="63e12-132">You can also find the Service Bus libraries as part of the Azure SDK.</span></span> <span data-ttu-id="63e12-133">您可以在 [Azure SDK 下載頁面](https://azure.microsoft.com/downloads/)中下載。</span><span class="sxs-lookup"><span data-stu-id="63e12-133">The download is available at the [Azure SDK download page](https://azure.microsoft.com/downloads/).</span></span>

### <a name="create-the-topic-and-subscriptions"></a><span data-ttu-id="63e12-134">建立主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="63e12-134">Create the topic and subscriptions</span></span>
<span data-ttu-id="63e12-135">服務匯流排傳訊實體的管理作業 (佇列和發佈/訂閱主題) 是透過 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別來執行。</span><span class="sxs-lookup"><span data-stu-id="63e12-135">Management operations for Service Bus messaging entities (queues and publish/subscribe topics) are performed via the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class.</span></span> <span data-ttu-id="63e12-136">需要有適當的認證，才能建立特定命名空間的 **NamespaceManager** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="63e12-136">Appropriate credentials are required in order to create a **NamespaceManager** instance for a particular namespace.</span></span> <span data-ttu-id="63e12-137">服務匯流排會使用以[共用存取簽章 (SAS)](service-bus-sas.md) 為基礎的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="63e12-137">Service Bus uses a [Shared Access Signature (SAS)](service-bus-sas.md) based security model.</span></span> <span data-ttu-id="63e12-138">[TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 類別代表安全性權杖提供者，其具有內建 Factory 方法，可傳回部分已知的權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="63e12-138">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) class represents a security token provider with built-in factory methods returning some well-known token providers.</span></span> <span data-ttu-id="63e12-139">我們將使用 [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) 方法來保存 SAS 認證。</span><span class="sxs-lookup"><span data-stu-id="63e12-139">We’ll use a [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to hold the SAS credentials.</span></span> <span data-ttu-id="63e12-140">接著使用服務匯流排命名空間和權杖提供者的基底位址建構 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="63e12-140">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) instance is then constructed with the base address of the Service Bus namespace and the token provider.</span></span>

<span data-ttu-id="63e12-141">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別提供用以建立、列舉及刪除傳訊實體的方法。</span><span class="sxs-lookup"><span data-stu-id="63e12-141">The [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class provides methods to create, enumerate and delete messaging entities.</span></span> <span data-ttu-id="63e12-142">此處的程式碼會示範如何建立 **NamespaceManager** 執行個體，並用來建立 **DataCollectionTopic** 主題。</span><span class="sxs-lookup"><span data-stu-id="63e12-142">The code that is shown here shows how the **NamespaceManager** instance is created and used to create the **DataCollectionTopic** topic.</span></span>

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="63e12-143">請注意，您可使用 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 方法的多載來設定主題的屬性。</span><span class="sxs-lookup"><span data-stu-id="63e12-143">Note that there are overloads of the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method that enable you to set properties of the topic.</span></span> <span data-ttu-id="63e12-144">例如，您可以為傳送到主題的訊息，設定預設的存留時間 (TTL) 值。</span><span class="sxs-lookup"><span data-stu-id="63e12-144">For example, you can set the default time-to-live (TTL) value for messages sent to the topic.</span></span> <span data-ttu-id="63e12-145">接下來，新增 **Inventory** 和 **Dashboard** 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e12-145">Next, add the **Inventory** and **Dashboard** subscriptions.</span></span>

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-to-the-topic"></a><span data-ttu-id="63e12-146">將訊息傳送到主題</span><span class="sxs-lookup"><span data-stu-id="63e12-146">Send messages to the topic</span></span>
<span data-ttu-id="63e12-147">對於服務匯流排實體上的執行階段作業 (例如，傳送和接收訊息)，應用程式必須先建立 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) 物件。</span><span class="sxs-lookup"><span data-stu-id="63e12-147">For run-time operations on Service Bus entities; for example, sending and receiving messages, an application must first create a [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) object.</span></span> <span data-ttu-id="63e12-148">**MessagingFactory** 執行個體類似於 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別，是從服務命名空間和權杖提供者的基底位址建立的。</span><span class="sxs-lookup"><span data-stu-id="63e12-148">Similar to the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, the **MessagingFactory** instance is created from the base address of the service namespace and the token provider.</span></span>

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

<span data-ttu-id="63e12-149">傳送至 (和接收自) 服務匯流排主題的訊息是 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="63e12-149">Messages sent to and received from Service Bus topics, are instances of the [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) class.</span></span> <span data-ttu-id="63e12-150">此類別包含一組標準屬性 (例如 [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 和 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive))、一個用來保存應用程式屬性的字典，以及任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="63e12-150">This class consists of a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold application properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="63e12-151">應用程式可以傳入任何可序列化物件來設定主體 (以下範例傳入 **SalesData** 物件代表 POS 終端機的銷售資料)，藉此利用 [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) 將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="63e12-151">An application can set the body by passing in any serializable object (the following example passes in a **SalesData** object that represents the sales data from the POS terminal), which will use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) to serialize the object.</span></span> <span data-ttu-id="63e12-152">或者，也可以提供 [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="63e12-152">Alternatively, a [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) object can be provided.</span></span>

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

<span data-ttu-id="63e12-153">將訊息傳送至主題的最簡單方式是使用 [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_)，直接從 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 執行個體建立 [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) 物件：</span><span class="sxs-lookup"><span data-stu-id="63e12-153">The easiest way to send messages to the topic is to use [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) to create a [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instance:</span></span>

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="63e12-154">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="63e12-154">Receive messages from a subscription</span></span>
<span data-ttu-id="63e12-155">與使用佇列類似，您可以使用 [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) 物件 (可使用 [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_) 從 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 直接建立)，接收來自訂用帳戶的訊息。</span><span class="sxs-lookup"><span data-stu-id="63e12-155">Similar to using queues, to receive messages from a subscription you can use a [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) object which you create directly from the [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) using [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_).</span></span> <span data-ttu-id="63e12-156">您可以使用兩種不同接收模式的其中之一 (**ReceiveAndDelete** 和 **PeekLock**)，如[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="63e12-156">You can use one of the two different receive modes (**ReceiveAndDelete** and **PeekLock**), as discussed in [Create applications that use Service Bus queues](service-bus-create-queues.md).</span></span>

<span data-ttu-id="63e12-157">請注意，當您建立訂用帳戶的 **MessageReceiver** 時，*entityPath* 參數的形式會是 `topicPath/subscriptions/subscriptionName`。</span><span class="sxs-lookup"><span data-stu-id="63e12-157">Note that when you create a **MessageReceiver** for subscriptions, the *entityPath* parameter is of the form `topicPath/subscriptions/subscriptionName`.</span></span> <span data-ttu-id="63e12-158">因此，若要為 **DataCollectionTopic** 主題的 **Inventory** 訂用帳戶建立 **MessageReceiver**，*entityPath* 必須設為 `DataCollectionTopic/subscriptions/Inventory`。</span><span class="sxs-lookup"><span data-stu-id="63e12-158">Therefore, to create a **MessageReceiver** for the **Inventory** subscription of the **DataCollectionTopic** topic, *entityPath* must be set to `DataCollectionTopic/subscriptions/Inventory`.</span></span> <span data-ttu-id="63e12-159">程式碼看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="63e12-159">The code appears as follows:</span></span>

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a><span data-ttu-id="63e12-160">訂用帳戶篩選</span><span class="sxs-lookup"><span data-stu-id="63e12-160">Subscription filters</span></span>
<span data-ttu-id="63e12-161">到目前為止，此案例中傳送至主題的所有訊息，都會提供給所有已註冊的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63e12-161">So far, in this scenario all messages sent to the topic are made available to all registered subscriptions.</span></span> <span data-ttu-id="63e12-162">請注意「都會提供」這幾個字。</span><span class="sxs-lookup"><span data-stu-id="63e12-162">The key phrase here is "made available."</span></span> <span data-ttu-id="63e12-163">雖然服務匯流排訂用帳戶可看見所有傳送至主題的訊息，但您只能將部分訊息複製到虛擬訂用帳戶佇列。</span><span class="sxs-lookup"><span data-stu-id="63e12-163">While Service Bus subscriptions see all messages sent to the topic, you can copy only a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="63e12-164">這項工作可透過訂用帳戶「篩選」來進行。</span><span class="sxs-lookup"><span data-stu-id="63e12-164">This is performed using subscription *filters*.</span></span> <span data-ttu-id="63e12-165">當您建立訂用帳戶時，可以用 SQL92 樣式的述詞形式，提供依訊息屬性運作的篩選運算式，這之中包括系統屬性 (例如 [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) 和應用程式屬性 (例如上一個範例中的 **StoreName**)。</span><span class="sxs-lookup"><span data-stu-id="63e12-165">When you create a subscription, you can supply a filter expression in the form of a SQL92 style predicate that operates over the properties of the message, both the system properties (for example, [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) and the application properties, such as **StoreName** in the previous example.</span></span>

<span data-ttu-id="63e12-166">若要演變案例來說明這點，要將第二間商店加入我們的零售案例。</span><span class="sxs-lookup"><span data-stu-id="63e12-166">Evolving the scenario to illustrate this, a second store is to be added to our retail scenario.</span></span> <span data-ttu-id="63e12-167">兩間商店的所有 POS 終端機的銷售資料，還是必須路由傳送至集中的庫存管理系統，但使用儀表板工具的店經理只注意到商店的銷售業績。</span><span class="sxs-lookup"><span data-stu-id="63e12-167">Sales data from all of the POS terminals from both stores still have to be routed to the centralized inventory management system, but a store manager using the dashboard tool is only interested in the performance of that store.</span></span> <span data-ttu-id="63e12-168">您可以用訂用帳戶篩選來達到此目的。</span><span class="sxs-lookup"><span data-stu-id="63e12-168">You can use subscription filtering to achieve this.</span></span> <span data-ttu-id="63e12-169">請注意，當 POS 終端機發佈訊息時，會在訊息上設定 **StoreName** 應用程式屬性。</span><span class="sxs-lookup"><span data-stu-id="63e12-169">Note that when the POS terminals publish messages, they set the **StoreName** application property on the message.</span></span> <span data-ttu-id="63e12-170">假設有兩間商店，例如 **Redmond** 和 **Seattle**，Redmond 商店中的 POS 終端機將其銷售資料訊息戳記了 **StoreName** 等於 **Redmond**，而 Seattle 商店的 POS 終端機則使用 **StoreName** 等於 **Seattle**。</span><span class="sxs-lookup"><span data-stu-id="63e12-170">Given two stores, for example **Redmond** and **Seattle**, the POS terminals in the Redmond store stamp their sales data messages with a **StoreName** equal to **Redmond**, whereas the Seattle store POS terminals use a **StoreName** equal to **Seattle**.</span></span> <span data-ttu-id="63e12-171">Redmond 商店的店經理只想要查看其 POS 終端機的資料。</span><span class="sxs-lookup"><span data-stu-id="63e12-171">The store manager of the Redmond store only wants to see data from its POS terminals.</span></span> <span data-ttu-id="63e12-172">系統看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="63e12-172">The system appears as follows:</span></span>

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

<span data-ttu-id="63e12-174">若要設定此路由傳送，您必須建立 **Dashboard** 訂用帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63e12-174">To set up this routing, you create the **Dashboard** subscription as follows:</span></span>

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

<span data-ttu-id="63e12-175">使用此[訂用帳戶篩選](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)時，只有 **StoreName** 屬性設定為 **Redmond** 的訊息才會複製到 **Dashboard** 訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="63e12-175">With this [subscription filter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), only messages that have the **StoreName** property set to **Redmond** will be copied to the virtual queue for the **Dashboard** subscription.</span></span> <span data-ttu-id="63e12-176">但還有更多其他訂用帳戶篩選。</span><span class="sxs-lookup"><span data-stu-id="63e12-176">There is much more to subscription filtering, however.</span></span> <span data-ttu-id="63e12-177">除了能夠在訊息傳遞到訂用帳戶的虛擬佇列時修改訊息屬性外，應用程式還可以在每個訂用帳戶中擁有多個篩選規則。</span><span class="sxs-lookup"><span data-stu-id="63e12-177">Applications can have multiple filter rules per subscription in addition to the ability to modify the properties of a message as it passes to a subscription's virtual queue.</span></span>

## <a name="summary"></a><span data-ttu-id="63e12-178">摘要</span><span class="sxs-lookup"><span data-stu-id="63e12-178">Summary</span></span>
<span data-ttu-id="63e12-179">在[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中所有使用佇列的原因說明，具體上也適用於使用主題的原因：</span><span class="sxs-lookup"><span data-stu-id="63e12-179">All of the reasons to use queuing described in [Create applications that use Service Bus queues](service-bus-create-queues.md) also apply to topics, specifically:</span></span>

* <span data-ttu-id="63e12-180">暫時分離 – 訊息產生者和取用者不需要同時在線上。</span><span class="sxs-lookup"><span data-stu-id="63e12-180">Temporal decoupling – message producers and consumers do not have to be online at the same time.</span></span>
* <span data-ttu-id="63e12-181">負載調節 – 由主題舒緩負載尖峰，因而可針對平均負載 (而非尖峰負載) 來佈建取用應用程式。</span><span class="sxs-lookup"><span data-stu-id="63e12-181">Load leveling – peaks in load are smoothed out by the topic enabling consuming applications to be provisioned for average load instead of peak load.</span></span>
* <span data-ttu-id="63e12-182">負載平衡 – 類似於佇列，您可以有多個競爭取用者接聽單一訂用帳戶，並將每則訊息遞交給其中一個取用者，進而平衡負載。</span><span class="sxs-lookup"><span data-stu-id="63e12-182">Load balancing – similar to a queue, you can have multiple competing consumers listening on a single subscription, with each message handed off to only one of the consumers, thereby balancing load.</span></span>
* <span data-ttu-id="63e12-183">鬆散結合 – 您可以在不影響現有端點的情況下發展傳訊網路；例如，新增訂用帳戶或變更主題的篩選，以接納新的取用者。</span><span class="sxs-lookup"><span data-stu-id="63e12-183">Loose coupling – you can evolve the messaging network without affecting existing endpoints; for example, adding subscriptions or changing filters to a topic to allow for new consumers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e12-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63e12-184">Next steps</span></span>

<span data-ttu-id="63e12-185">請參閱[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)，了解如何在 POS 零售案例中使用佇列的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="63e12-185">See [Create applications that use Service Bus queues](service-bus-create-queues.md) for information about how to use queues in the POS retail scenario.</span></span>

