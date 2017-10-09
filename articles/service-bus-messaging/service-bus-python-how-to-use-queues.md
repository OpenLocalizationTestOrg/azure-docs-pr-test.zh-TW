---
title: "aaaHow toouse Azure 服務匯流排佇列使用 Python |Microsoft 文件"
description: "了解 Azure 服務匯流排 toouse 來自 Python 的佇列。"
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="efccc-103">服務匯流排 toouse 排入佇列使用 Python</span><span class="sxs-lookup"><span data-stu-id="efccc-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="efccc-104">本文說明如何 toouse 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="efccc-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="efccc-105">hello 範例撰寫的 Python 和使用 hello [Python Azure 服務匯流排封裝][Python Azure Service Bus package]。</span><span class="sxs-lookup"><span data-stu-id="efccc-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="efccc-106">hello 涵蓋案例包括**建立佇列，傳送和接收訊息**，和**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="efccc-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="efccc-107">Python 或 hello tooinstall [Python Azure 服務匯流排封裝][Python Azure Service Bus package]，請參閱 hello [Python 安裝指南](../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="efccc-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="efccc-108">建立佇列</span><span class="sxs-lookup"><span data-stu-id="efccc-108">Create a queue</span></span>
<span data-ttu-id="efccc-109">hello **ServiceBusService**物件可讓您與佇列搭配 toowork。</span><span class="sxs-lookup"><span data-stu-id="efccc-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="efccc-110">加入下列程式碼要在其中任何 Python 檔案 tooprogrammatically 存取服務匯流排的 hello 頂端附近的 hello:</span><span class="sxs-lookup"><span data-stu-id="efccc-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="efccc-111">hello 下列程式碼會建立**ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="efccc-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="efccc-112">請使用您的命名空間、共用存取簽章 (SAS) 金鑰名稱和值來取代 `mynamespace`、`sharedaccesskeyname` 和 `sharedaccesskey`。</span><span class="sxs-lookup"><span data-stu-id="efccc-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="efccc-113">hello hello SAS 金鑰名稱和值的值可以在 hello [Azure 入口網站][ Azure portal]連接資訊，或在 Visual Studio hello**屬性**窗格選取時（如 hello 前一節中所示），請 hello 在伺服器總管] 中的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="efccc-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="efccc-114">hello`create_queue`方法也支援其他選項，可讓您 toooverride 預設佇列設定，例如訊息時間 toolive (TTL) 或佇列大小上限。</span><span class="sxs-lookup"><span data-stu-id="efccc-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="efccc-115">hello 下列範例會設定 hello 最大佇列大小 too5 GB 和 hello TTL 值 too1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="efccc-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="efccc-116">傳送訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="efccc-116">Send messages tooa queue</span></span>
<span data-ttu-id="efccc-117">toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`send_queue_message`方法上 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="efccc-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="efccc-118">hello 下列範例會示範如何 toosend 測試訊息 toohello 佇列名為`taskqueue`使用`send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="efccc-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="efccc-119">服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="efccc-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="efccc-120">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="efccc-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="efccc-121">訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="efccc-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="efccc-122">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="efccc-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="efccc-123">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="efccc-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="efccc-124">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="efccc-124">Receive messages from a queue</span></span>
<span data-ttu-id="efccc-125">訊息會使用從佇列接收 hello`receive_queue_message`方法上 hello **ServiceBusService**物件：</span><span class="sxs-lookup"><span data-stu-id="efccc-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="efccc-126">在讀取時從 hello 佇列刪除訊息 hello 參數`peek_lock`設定得**False**。</span><span class="sxs-lookup"><span data-stu-id="efccc-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="efccc-127">您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它所設定的 hello 參數從 hello 佇列`peek_lock`太**True**。</span><span class="sxs-lookup"><span data-stu-id="efccc-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="efccc-128">hello 行為的讀取和刪除 hello 訊息，因為 hello 的一部分接收作業是 hello 最簡單的模型，並最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="efccc-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="efccc-129">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="efccc-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="efccc-130">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="efccc-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="efccc-131">如果 hello`peek_lock`參數設定太**True**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="efccc-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="efccc-132">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="efccc-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="efccc-133">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段接收程序呼叫 hello**刪除**方法上 hello**訊息**物件。</span><span class="sxs-lookup"><span data-stu-id="efccc-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="efccc-134">hello**刪除**方法會標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="efccc-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="efccc-135">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="efccc-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="efccc-136">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="efccc-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="efccc-137">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello**解除鎖定**方法上 hello**訊息**物件。</span><span class="sxs-lookup"><span data-stu-id="efccc-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="efccc-138">這將導致 hello 佇列內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="efccc-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="efccc-139">另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello tooprocess hello 訊息之前的應用程式失敗 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），服務匯流排會自動解除鎖定 hello 訊息，然後並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="efccc-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="efccc-140">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello**刪除**呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="efccc-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="efccc-141">這通常稱為**至少一旦處理**，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="efccc-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="efccc-142">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="efccc-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="efccc-143">這通常用來達成 hello **MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。</span><span class="sxs-lookup"><span data-stu-id="efccc-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efccc-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="efccc-144">Next steps</span></span>
<span data-ttu-id="efccc-145">既然您已經學會 hello 的服務匯流排佇列的基本概念，請參閱這些文章 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="efccc-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="efccc-146">[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="efccc-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

