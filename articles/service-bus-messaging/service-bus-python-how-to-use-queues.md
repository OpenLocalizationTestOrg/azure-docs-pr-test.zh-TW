---
title: "如何搭配 Python 使用 Azure 服務匯流排佇列 | Microsoft Docs"
description: "了解如何從 Python 使用 Azure 服務匯流排佇列。"
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="f9537-103">如何將服務匯流排佇列搭配 Python 使用</span><span class="sxs-lookup"><span data-stu-id="f9537-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="f9537-104">本文說明如何使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="f9537-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="f9537-105">相關範例是以 Python 撰寫，並且使用 [Python Azure 服務匯流排封裝][Python Azure Service Bus package]。</span><span class="sxs-lookup"><span data-stu-id="f9537-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="f9537-106">本文說明的案例包括**建立佇列、傳送並接收訊息**，以及**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="f9537-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="f9537-107">若要安裝 Python 或 [Python Azure 服務匯流排封裝][Python Azure Service Bus package]，請參閱 [Python 安裝指南](../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="f9537-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="f9537-108">建立佇列</span><span class="sxs-lookup"><span data-stu-id="f9537-108">Create a queue</span></span>
<span data-ttu-id="f9537-109">**ServiceBusService** 物件可讓您使用佇列。</span><span class="sxs-lookup"><span data-stu-id="f9537-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="f9537-110">將下列程式碼新增至您想要在其中以程式設計方式存取服務匯流排之任何 Python 檔案內的頂端附近：</span><span class="sxs-lookup"><span data-stu-id="f9537-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="f9537-111">下列程式碼將建立 **ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="f9537-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="f9537-112">請使用您的命名空間、共用存取簽章 (SAS) 金鑰名稱和值來取代 `mynamespace`、`sharedaccesskeyname` 和 `sharedaccesskey`。</span><span class="sxs-lookup"><span data-stu-id="f9537-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="f9537-113">SAS 金鑰名稱和值的值可以在 [Azure 入口網站][Azure portal]連線資訊中找到，或在 Visual Studio 的 [伺服器總管] 中選取「服務匯流排」命名空間時於 [屬性] 窗格中找到 (如上一節所示)。</span><span class="sxs-lookup"><span data-stu-id="f9537-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="f9537-114">`create_queue` 方法也支援其他選項，而可讓您覆寫訊息存留時間 (TTL) 或佇列大小上限等預設佇列設定。</span><span class="sxs-lookup"><span data-stu-id="f9537-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="f9537-115">下列範例會將佇列大小上限設為 5GB，並將 TTL 時間設為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="f9537-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="f9537-116">傳送訊息至佇列</span><span class="sxs-lookup"><span data-stu-id="f9537-116">Send messages to a queue</span></span>
<span data-ttu-id="f9537-117">若要傳送訊息至服務匯流排佇列，應用程式將呼叫 **ServiceBusService** 物件上的 `send_queue_message` 方法。</span><span class="sxs-lookup"><span data-stu-id="f9537-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="f9537-118">下列範例示範如何使用 `send_queue_message` 將測試訊息傳送至名為 `taskqueue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="f9537-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="f9537-119">服務匯流排佇列支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="f9537-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="f9537-120">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="f9537-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="f9537-121">佇列中所保存的訊息數目沒有限制，但佇列所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="f9537-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="f9537-122">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="f9537-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="f9537-123">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="f9537-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="f9537-124">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="f9537-124">Receive messages from a queue</span></span>
<span data-ttu-id="f9537-125">對於 **ServiceBusService** 物件使用 `receive_queue_message` 方法即可從佇列接收訊息：</span><span class="sxs-lookup"><span data-stu-id="f9537-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="f9537-126">如果將 `peek_lock` 參數設為 **False**，則當讀取訊息後，訊息便會從佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="f9537-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="f9537-127">您可以將參數 `peek_lock` 設為 **True**，來讀取 (查看) 並鎖定訊息，避免系統從佇列刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="f9537-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="f9537-128">隨著接收作業讀取及刪除訊息之行為是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="f9537-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="f9537-129">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="f9537-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="f9537-130">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="f9537-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="f9537-131">如果您將 `peek_lock` 參數設為 **True**，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9537-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="f9537-132">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9537-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="f9537-133">在應用程式完成訊息處理 (或可靠地儲存此訊息以供未來處理) 之後，它會在 **Message** 物件上呼叫 **delete** 方法，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="f9537-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="f9537-134">**delete** 方法會將訊息標示為已取用，並將其從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="f9537-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="f9537-135">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="f9537-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="f9537-136">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="f9537-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="f9537-137">如果接收者應用程式因為某些原因無法處理訊息，它可以在 **Message** 物件上呼叫 **unlock** 方法。</span><span class="sxs-lookup"><span data-stu-id="f9537-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="f9537-138">這將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="f9537-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="f9537-139">與在佇列內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排將自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="f9537-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="f9537-140">如果應用程式在處理訊息之後，尚未呼叫 **delete** 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9537-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="f9537-141">這通常稱為**至少處理一次**，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="f9537-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="f9537-142">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="f9537-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="f9537-143">通常您可使用訊息的 **MessageId** 屬性來達到此目的，該屬性將在各個傳遞嘗試中會保持不變。</span><span class="sxs-lookup"><span data-stu-id="f9537-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9537-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9537-144">Next steps</span></span>
<span data-ttu-id="f9537-145">既然您已經了解「服務匯流排」佇列的基本概念，您現在可以閱讀下列文章來深入了解。</span><span class="sxs-lookup"><span data-stu-id="f9537-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="f9537-146">[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="f9537-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

