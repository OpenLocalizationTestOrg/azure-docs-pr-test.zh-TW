---
title: "Azure 服務匯流排中處理交易的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="82857-103">服務匯流排交易處理概觀</span><span class="sxs-lookup"><span data-stu-id="82857-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="82857-104">這篇文章討論 Azure 服務匯流排 hello 交易功能。</span><span class="sxs-lookup"><span data-stu-id="82857-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="82857-105">大部分的 hello 討論說明 hello[不可部分完成交易與服務匯流排範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)。</span><span class="sxs-lookup"><span data-stu-id="82857-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="82857-106">這篇文章是有限的 tooan 概觀交易處理和 hello*透過傳送*Service bus，hello 不可部分完成交易的範例是在範圍更大且更複雜的功能。</span><span class="sxs-lookup"><span data-stu-id="82857-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="82857-107">服務匯流排中的交易</span><span class="sxs-lookup"><span data-stu-id="82857-107">Transactions in Service Bus</span></span>
<span data-ttu-id="82857-108">[交易](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions)會將兩個以上的作業一起分組到「執行範圍」。</span><span class="sxs-lookup"><span data-stu-id="82857-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="82857-109">本質上，屬於 tooa 假設的作業群組的所有作業成功或失敗共同，必須確定在這種交易。</span><span class="sxs-lookup"><span data-stu-id="82857-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="82857-110">在這一方面交易做為一個單位，通常會參考的 tooas*不可部份完成性*。</span><span class="sxs-lookup"><span data-stu-id="82857-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="82857-111">服務匯流排是交易訊息代理人，並確保其訊息存放區之所有內部作業的交易完整性。</span><span class="sxs-lookup"><span data-stu-id="82857-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="82857-112">所有傳輸的服務匯流排內的訊息，例如移動訊息 tooa[寄不出的信件佇列](service-bus-dead-letter-queues.md)或[自動轉送](service-bus-auto-forwarding.md)個實體之間的訊息，為交易式。</span><span class="sxs-lookup"><span data-stu-id="82857-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="82857-113">這麼一來，如果服務匯流排接受訊息，表示訊息已經儲存並標上序號。</span><span class="sxs-lookup"><span data-stu-id="82857-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="82857-114">從那時起，Service Bus 中的任何訊息傳輸會協調的作業，跨實體，而將兩者都不會導致 tooloss （來源成功和失敗的目標） 或 tooduplication （來源成功與失敗目標） 的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="82857-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="82857-115">服務匯流排支援針對單一訊息實體 （佇列、 主題、 訂用帳戶） hello 範圍內的交易的分組作業。</span><span class="sxs-lookup"><span data-stu-id="82857-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="82857-116">例如，您可以將來自數個訊息 tooone 佇列傳送的交易範圍內，而 hello 訊息才會認可的 toohello 佇列記錄 hello 交易成功完成時。</span><span class="sxs-lookup"><span data-stu-id="82857-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="82857-117">交易範圍內的作業</span><span class="sxs-lookup"><span data-stu-id="82857-117">Operations within a transaction scope</span></span>
<span data-ttu-id="82857-118">可以在交易範圍內執行的 hello 作業如下所示：</span><span class="sxs-lookup"><span data-stu-id="82857-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="82857-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)、[MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)、[TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**：Send、SendAsync、SendBatch、SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="82857-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="82857-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**：Complete、CompleteAsync、Abandon、AbandonAsync、Deadletter、DeadletterAsync、Defer、DeferAsync、RenewLock、RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="82857-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="82857-121">接收作業並不包含在內，因為它會假設 hello 應用程式會取得使用 hello 訊息[ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中的，在某些接收迴圈或[OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_)回呼，以及只然後開啟交易範圍處理 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="82857-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="82857-122">hello hello 訊息 （完成，放棄，寄不出的信件、 延遲） 的配置就會發生在 hello 範圍，以及依存於，hello hello 交易的整體結果。</span><span class="sxs-lookup"><span data-stu-id="82857-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="82857-123">傳輸和「傳送方式」</span><span class="sxs-lookup"><span data-stu-id="82857-123">Transfers and "send via"</span></span>
<span data-ttu-id="82857-124">tooenable 和資料的佇列 tooa 處理器，然後 tooanother 佇列的交易移，服務匯流排支援*傳輸*。</span><span class="sxs-lookup"><span data-stu-id="82857-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="82857-125">在傳送作業中，寄件者先傳送訊息 tooa 「 傳送佇列 」 和 hello 傳輸佇列立即移 hello 訊息 toohello 適合使用的 hello 強固相同傳輸實作 hello 自動轉送功能相依的目的地佇列上。</span><span class="sxs-lookup"><span data-stu-id="82857-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="82857-126">hello 訊息永遠不會認可的 toohello 傳輸佇列的記錄檔，它會變成可見 hello 傳輸佇列的取用者的方式。</span><span class="sxs-lookup"><span data-stu-id="82857-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="82857-127">hello hello 寄件者的輸入訊息來源 hello 傳輸佇列本身時，此交易式功能的 hello 電源就顯而易見。</span><span class="sxs-lookup"><span data-stu-id="82857-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="82857-128">換句話說，服務匯流排可以傳送 hello 訊息 toohello 目的地佇列"via"hello 傳輸佇列中，執行完成時 (或延遲，或寄不出信件) 在 hello 輸入訊息中，所有在一個不可部分完成的作業中的作業。</span><span class="sxs-lookup"><span data-stu-id="82857-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="82857-129">透過程式碼查看</span><span class="sxs-lookup"><span data-stu-id="82857-129">See it in code</span></span>
<span data-ttu-id="82857-130">tooset 總這類傳輸，您會建立訊息寄件者為目標 hello 透過 hello 傳輸佇列的目的地佇列。</span><span class="sxs-lookup"><span data-stu-id="82857-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="82857-131">您也要有從相同佇列提取訊息的收件者。</span><span class="sxs-lookup"><span data-stu-id="82857-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="82857-132">例如：</span><span class="sxs-lookup"><span data-stu-id="82857-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="82857-133">然後簡單交易是使用這些項目，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="82857-133">A simple transaction then uses these elements, as in hello following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="82857-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82857-134">Next steps</span></span>

<span data-ttu-id="82857-135">請參閱下列文章中的服務匯流排佇列的詳細資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="82857-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="82857-136">使用自動轉寄鏈結服務匯流排實體</span><span class="sxs-lookup"><span data-stu-id="82857-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="82857-137">自動轉寄範例</span><span class="sxs-lookup"><span data-stu-id="82857-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="82857-138">使用服務匯流排的不可部分完成交易範例</span><span class="sxs-lookup"><span data-stu-id="82857-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="82857-139">比較 Azure 佇列和服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="82857-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="82857-140">如何 toouse 服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="82857-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

