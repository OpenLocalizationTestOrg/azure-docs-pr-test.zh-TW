---
title: "Azure 服務匯流排的交易處理概觀 | Microsoft Docs"
description: "Azure 服務匯流排不可部分完成交易和傳送方式概觀"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="32e1f-103">服務匯流排交易處理概觀</span><span class="sxs-lookup"><span data-stu-id="32e1f-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="32e1f-104">本文討論 Azure 服務匯流排的交易功能。</span><span class="sxs-lookup"><span data-stu-id="32e1f-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="32e1f-105">[使用服務匯流排的不可部分完成交易範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)會說明大部分的討論。</span><span class="sxs-lookup"><span data-stu-id="32e1f-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="32e1f-106">本文只包含交易處理概觀以及服務匯流排中的「傳送方式」功能，而「不可部分完成交易」範例的範圍更廣且更複雜。</span><span class="sxs-lookup"><span data-stu-id="32e1f-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="32e1f-107">服務匯流排中的交易</span><span class="sxs-lookup"><span data-stu-id="32e1f-107">Transactions in Service Bus</span></span>
<span data-ttu-id="32e1f-108">[交易](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions)會將兩個以上的作業一起分組到「執行範圍」。</span><span class="sxs-lookup"><span data-stu-id="32e1f-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="32e1f-109">本質上，這類交易必須確定屬於指定作業群組的所有作業都一起成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="32e1f-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="32e1f-110">在這部分，所有交易都會當成一個單位，通常稱為「不可部分完成性」。</span><span class="sxs-lookup"><span data-stu-id="32e1f-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="32e1f-111">服務匯流排是交易訊息代理人，並確保其訊息存放區之所有內部作業的交易完整性。</span><span class="sxs-lookup"><span data-stu-id="32e1f-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="32e1f-112">服務匯流排內的所有訊息傳輸 (例如，將訊息移至[寄不出的信件佇列](service-bus-dead-letter-queues.md)，或[自動轉寄](service-bus-auto-forwarding.md)實體之間的訊息) 為交易式。</span><span class="sxs-lookup"><span data-stu-id="32e1f-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="32e1f-113">這麼一來，如果服務匯流排接受訊息，表示訊息已經儲存並標上序號。</span><span class="sxs-lookup"><span data-stu-id="32e1f-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="32e1f-114">從那時開始，服務匯流排內的任何訊息傳輸都是跨實體的協調作業，並且不會導致訊息遺失 (來源成功，但目標失敗) 或重複 (來源失敗，但目標成功)。</span><span class="sxs-lookup"><span data-stu-id="32e1f-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="32e1f-115">服務匯流排支援交易範圍內單一傳訊實體 (佇列、主題、訂用帳戶) 的分組作業。</span><span class="sxs-lookup"><span data-stu-id="32e1f-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="32e1f-116">例如，您可以將數個訊息傳送至交易範圍內的一個佇列；而且，在交易順利完成時，只會將訊息認可到佇列的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="32e1f-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="32e1f-117">交易範圍內的作業</span><span class="sxs-lookup"><span data-stu-id="32e1f-117">Operations within a transaction scope</span></span>
<span data-ttu-id="32e1f-118">可在交易範圍內執行的作業如下︰</span><span class="sxs-lookup"><span data-stu-id="32e1f-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="32e1f-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)、[MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)、[TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**：Send、SendAsync、SendBatch、SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="32e1f-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="32e1f-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**：Complete、CompleteAsync、Abandon、AbandonAsync、Deadletter、DeadletterAsync、Defer、DeferAsync、RenewLock、RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="32e1f-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="32e1f-121">不包括接收作業，因為假設應用程式使用 [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式、在一些接收迴圈內或使用 [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) 回呼來取得訊息，然後只會開啟交易範圍來處理訊息。</span><span class="sxs-lookup"><span data-stu-id="32e1f-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="32e1f-122">訊息的處置 (完成、放棄、寄不出的信件、延遲) 接著發生於整體交易結果的範圍內，並與整體交易結果相依。</span><span class="sxs-lookup"><span data-stu-id="32e1f-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="32e1f-123">傳輸和「傳送方式」</span><span class="sxs-lookup"><span data-stu-id="32e1f-123">Transfers and "send via"</span></span>
<span data-ttu-id="32e1f-124">若要啟用從佇列到處理器再到另一個佇列的交易式資料送交，服務匯流排支援「傳輸」。</span><span class="sxs-lookup"><span data-stu-id="32e1f-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="32e1f-125">在傳輸作業中，寄件者會先將訊息傳送至「傳輸佇列」，而傳輸佇列會使用自動轉寄功能所依賴的相同穩固傳輸實作，立即將訊息移至想要的目的地佇列。</span><span class="sxs-lookup"><span data-stu-id="32e1f-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="32e1f-126">訊息絕不會認可到傳輸佇列的記錄檔，因此，傳輸佇列的取用者可以看到它。</span><span class="sxs-lookup"><span data-stu-id="32e1f-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="32e1f-127">傳輸佇列本身是寄件者輸入訊息的來源時，就能知道這個交易式功能的能力。</span><span class="sxs-lookup"><span data-stu-id="32e1f-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="32e1f-128">換句話說，服務匯流排可以「透過」傳輸佇列將訊息傳輸到目的地佇列，同時對輸入訊息執行完整 (或延遲，或寄不出信件) 作業 (全部都在一個不可部分完成作業中)。</span><span class="sxs-lookup"><span data-stu-id="32e1f-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="32e1f-129">透過程式碼查看</span><span class="sxs-lookup"><span data-stu-id="32e1f-129">See it in code</span></span>
<span data-ttu-id="32e1f-130">若要設定這類傳輸，您可以建立將目標設為透過傳輸佇列之目的地佇列的訊息寄件者。</span><span class="sxs-lookup"><span data-stu-id="32e1f-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="32e1f-131">您也要有從相同佇列提取訊息的收件者。</span><span class="sxs-lookup"><span data-stu-id="32e1f-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="32e1f-132">例如：</span><span class="sxs-lookup"><span data-stu-id="32e1f-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="32e1f-133">簡單交易接著會使用這些元素，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="32e1f-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="32e1f-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32e1f-134">Next steps</span></span>

<span data-ttu-id="32e1f-135">如需服務匯流排佇列的詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="32e1f-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="32e1f-136">使用自動轉寄鏈結服務匯流排實體</span><span class="sxs-lookup"><span data-stu-id="32e1f-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="32e1f-137">自動轉寄範例</span><span class="sxs-lookup"><span data-stu-id="32e1f-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="32e1f-138">使用服務匯流排的不可部分完成交易範例</span><span class="sxs-lookup"><span data-stu-id="32e1f-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="32e1f-139">比較 Azure 佇列和服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="32e1f-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="32e1f-140">如何使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="32e1f-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

