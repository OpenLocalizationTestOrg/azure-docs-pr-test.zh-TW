---
title: "aaaAuto 轉送 Azure Service Bus 訊息實體 |Microsoft 文件"
description: "如何 toochain 服務匯流排佇列或訂閱 tooanother 佇列或主題。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="c1fbb-103">使用自動轉寄鏈結服務匯流排實體</span><span class="sxs-lookup"><span data-stu-id="c1fbb-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="c1fbb-104">服務匯流排 hello*自動轉送*功能可讓您 toochain 佇列或訂閱 tooanother 佇列或主題 hello 屬於相同的命名空間。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="c1fbb-105">啟用自動轉送時，服務匯流排自動移除 hello 第一個佇列或訂閱 （來源） 中放置的訊息，並將它們置於 hello 第二個佇列或主題 （目的地）。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="c1fbb-106">請注意，它仍可能 toosend 訊息 toohello 目的地實體直接。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="c1fbb-107">此外，它不可能 toochain 子佇列，例如無效信件佇列、 tooanother 佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="c1fbb-108">使用自動轉寄</span><span class="sxs-lookup"><span data-stu-id="c1fbb-108">Using auto-forwarding</span></span>
<span data-ttu-id="c1fbb-109">您可以啟用自動轉送設定 hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo]或[SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo]屬性上 hello [QueueDescription] [ QueueDescription]或[SubscriptionDescription] [ SubscriptionDescription] hello 來源，例如 hello 的物件下列範例。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="c1fbb-110">hello 目的地實體必須存在於建立 hello 來源實體的 hello 階段。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="c1fbb-111">如果 hello 目的地實體不存在，服務匯流排集的 toocreate hello 來源實體時，就會傳回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="c1fbb-112">您可以使用自動轉送 tooscale 個別的主題。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="c1fbb-113">服務匯流排限制 hello[的特定主題的訂用帳戶數目](service-bus-quotas.md)too2，000。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="c1fbb-114">您可以藉由建立第二層主題來容納其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="c1fbb-115">請注意，即使您未繫結的 hello 服務匯流排訂用帳戶，加入第二層主題的 hello 數目限制可以改善 hello 主題的整體輸送量。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![自動轉寄案例][0]

<span data-ttu-id="c1fbb-117">您也可以使用自動轉送 toodecouple 訊息傳送者和接收者。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="c1fbb-118">例如，請考慮包含三個模組的 ERP 系統︰訂單處理、庫存管理及客戶關係管理。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="c1fbb-119">上述每一個模組會產生加入對應主題中的訊息。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="c1fbb-120">Alice 和 Bob 是銷售人員感興趣 tootheir 客戶與相關聯的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="c1fbb-121">tooreceive 這些訊息，Alice 和 Bob 都建立個人佇列和訂閱 hello 自動轉寄所有郵件 tootheir 佇列的 ERP 主題的每個上。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![自動轉寄案例][1]

<span data-ttu-id="c1fbb-123">如果 Alice 渡假，她個人佇列，而不是 hello ERP 主題，則會填滿。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="c1fbb-124">在此案例中，銷售代表未收到任何訊息，因為無 hello ERP 主題不會達到配額。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="c1fbb-125">自動轉寄考量</span><span class="sxs-lookup"><span data-stu-id="c1fbb-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="c1fbb-126">如果 hello 目的地實體太多的訊息會累積及超過 hello 配額或 hello 目的地實體已停用，hello 來源實體會加入 hello 訊息 tooits[寄不出的信件佇列](service-bus-dead-letter-queues.md)直到 hello 目的地中的空間（或 hello 實體已重新啟用）。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="c1fbb-127">這些訊息會繼續 toolive hello 寄不出信件佇列中，因此您必須明確地接收與處理 hello 寄不出的信件佇列。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="c1fbb-128">當鏈結在一起個別主題 tooobtain 具有多個訂閱的複合主題，建議您有少量的 hello 第一層主題訂閱和許多 hello 第二層主題訂閱。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="c1fbb-129">例如，第一層主題包含 20 個訂閱中的，每個鏈結 tooa 第二層主題包含 200 個訂閱，允許更高的輸送量比第一層主題包含 200 個訂閱，每個鏈結 tooa 第二層主題包含 20 個訂閱.</span><span class="sxs-lookup"><span data-stu-id="c1fbb-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="c1fbb-130">服務匯流排會針對每一則轉寄的訊息向一個作業計費。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="c1fbb-131">例如，每個傳送訊息 tooa 主題包含 20 個訂閱，設定 tooauto 轉寄訊息 tooanother 佇列或主題，以計費 21 次作業如果第一層的所有訂閱都收到 hello 訊息的複本。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="c1fbb-132">hello hello 訂用帳戶的建立者必須具有 toocreate 鏈結的 tooanother 佇列或主題的訂用帳戶，**管理**hello 來源和 hello 目的地實體的權限。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="c1fbb-133">傳送訊息 toohello 來源主題只需要**傳送**hello 來源主題上的權限。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1fbb-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1fbb-134">Next steps</span></span>

<span data-ttu-id="c1fbb-135">如需自動轉送的詳細資訊，請參閱下列參考主題的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1fbb-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="c1fbb-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="c1fbb-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="c1fbb-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="c1fbb-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="c1fbb-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="c1fbb-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="c1fbb-139">toolearn 進一步了解服務匯流排效能增強功能，請參閱</span><span class="sxs-lookup"><span data-stu-id="c1fbb-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="c1fbb-140">使用服務匯流排傳訊的效能改進最佳作法</span><span class="sxs-lookup"><span data-stu-id="c1fbb-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="c1fbb-141">[分割的傳訊實體][Partitioned messaging entities]。</span><span class="sxs-lookup"><span data-stu-id="c1fbb-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
