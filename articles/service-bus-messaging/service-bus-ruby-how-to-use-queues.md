---
title: "aaaHow toouse Azure 服務匯流排佇列與 Ruby |Microsoft 文件"
description: "了解如何 toouse Service Bus 佇列在 Azure 中。 程式碼範例以 Ruby 撰寫。"
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a><span data-ttu-id="45121-104">服務匯流排 toouse 排入佇列以 Ruby</span><span class="sxs-lookup"><span data-stu-id="45121-104">How toouse Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="45121-105">本指南說明如何 toouse 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="45121-105">This guide describes how toouse Service Bus queues.</span></span> <span data-ttu-id="45121-106">hello 範例以 Ruby 所撰寫，並使用 hello Azure 健身。</span><span class="sxs-lookup"><span data-stu-id="45121-106">hello samples are written in Ruby and use hello Azure gem.</span></span> <span data-ttu-id="45121-107">hello 涵蓋案例包括**建立佇列，傳送和接收訊息**，和**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="45121-107">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="45121-108">如需有關 Service Bus 佇列的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="45121-108">For more information about Service Bus queues, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a><span data-ttu-id="45121-109">如何 toocreate 佇列</span><span class="sxs-lookup"><span data-stu-id="45121-109">How toocreate a queue</span></span>
<span data-ttu-id="45121-110">hello **Azure::ServiceBusService**物件可讓您與佇列搭配 toowork。</span><span class="sxs-lookup"><span data-stu-id="45121-110">hello **Azure::ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="45121-111">toocreate 佇列中，使用 hello`create_queue()`方法。</span><span class="sxs-lookup"><span data-stu-id="45121-111">toocreate a queue, use hello `create_queue()` method.</span></span> <span data-ttu-id="45121-112">hello 下列範例會建立佇列或列印出任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="45121-112">hello following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="45121-113">您也可以傳遞**Azure::ServiceBus::Queue**物件與其他選項，可讓您 toooverride hello 預設佇列設定中的，例如訊息時間 toolive 或最大佇列大小。</span><span class="sxs-lookup"><span data-stu-id="45121-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you toooverride hello default queue settings, such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="45121-114">hello 下列範例顯示如何 tooset hello 最大佇列大小 too5 GB 和 toolive too1 分鐘的時間：</span><span class="sxs-lookup"><span data-stu-id="45121-114">hello following example shows how tooset hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a><span data-ttu-id="45121-115">如何 toosend 訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="45121-115">How toosend messages tooa queue</span></span>
<span data-ttu-id="45121-116">toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`send_queue_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="45121-116">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="45121-117">訊息太傳送 （與從接收的資料） 的服務匯流排佇列是**Azure::ServiceBus::BrokeredMessage**物件，並有一組標準屬性 (例如`label`和`time_to_live`)，是使用的 toohold 字典自訂應用程式特有的屬性和任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="45121-117">Messages sent too(and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="45121-118">應用程式可以設定 hello hello 訊息本文藉由傳遞字串值為 hello 訊息和任何必要的標準屬性會填入預設值。</span><span class="sxs-lookup"><span data-stu-id="45121-118">An application can set hello body of hello message by passing a string value as hello message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="45121-119">hello 下列範例會示範如何 toosend 測試訊息 toohello 佇列名為`test-queue`使用`send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="45121-119">hello following example demonstrates how toosend a test message toohello queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="45121-120">服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="45121-120">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="45121-121">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="45121-121">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="45121-122">訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="45121-122">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="45121-123">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="45121-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-queue"></a><span data-ttu-id="45121-124">Tooreceive 從佇列的訊息</span><span class="sxs-lookup"><span data-stu-id="45121-124">How tooreceive messages from a queue</span></span>
<span data-ttu-id="45121-125">訊息會使用從佇列接收 hello`receive_queue_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="45121-125">Messages are received from a queue using hello `receive_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="45121-126">根據預設，會讀取及鎖定而不從 hello 佇列刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="45121-126">By default, messages are read and locked without being deleted from hello queue.</span></span> <span data-ttu-id="45121-127">不過，您可以刪除訊息從 hello 佇列設定 hello 讀取`:peek_lock`太選項**false**。</span><span class="sxs-lookup"><span data-stu-id="45121-127">However, you can delete messages from hello queue as they are read by setting hello `:peek_lock` option too**false**.</span></span>

<span data-ttu-id="45121-128">hello 預設行為可讓 hello 讀取和刪除兩階段作業，也使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45121-128">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="45121-129">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45121-129">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="45121-130">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete_queue_message()`方法並提供 hello 訊息 toobe 刪除做為參數。</span><span class="sxs-lookup"><span data-stu-id="45121-130">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_queue_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="45121-131">hello`delete_queue_message()`方法會標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="45121-131">hello `delete_queue_message()` method will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="45121-132">如果 hello`:peek_lock`參數設定太**false**，讀取和刪除 hello 訊息會變成 hello 最簡單的模型，並且適合用於應用程式可以容許不處理訊息的 hello 事件中的案例失敗。</span><span class="sxs-lookup"><span data-stu-id="45121-132">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="45121-133">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="45121-133">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="45121-134">服務匯流排已標示為正在使用，當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="45121-134">Because Service Bus has marked hello message as being consumed, when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="45121-135">hello 下列範例會示範如何 tooreceive 和處理序訊息使用`receive_queue_message()`。</span><span class="sxs-lookup"><span data-stu-id="45121-135">hello following example demonstrates how tooreceive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="45121-136">hello 範例先接收並刪除訊息使用`:peek_lock`設定得**false**、 收到另一則訊息，然後再刪除 hello 訊息使用`delete_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="45121-136">hello example first receives and deletes a message by using `:peek_lock` set too**false**, then it receives another message and then deletes hello message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="45121-137">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="45121-137">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="45121-138">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="45121-138">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="45121-139">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock_queue_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="45121-139">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="45121-140">服務匯流排 toounlock hello hello 佇列訊息，並將其可用 toobe 同樣地，收到此呼叫原因可能是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="45121-140">This call causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="45121-141">另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="45121-141">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="45121-142">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete_queue_message()`呼叫方法時，則 hello 訊息時，已重新傳遞的 toohello 應用程式會在重新啟動。</span><span class="sxs-lookup"><span data-stu-id="45121-142">In hello event that hello application crashes after processing hello message but before hello `delete_queue_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="45121-143">此程序通常稱為*至少一旦處理*; 也就是說，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="45121-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="45121-144">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="45121-144">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="45121-145">這通常用來達成 hello `message_id` hello 訊息，嘗試傳遞都維持不變的屬性。</span><span class="sxs-lookup"><span data-stu-id="45121-145">This is often achieved using hello `message_id` property of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45121-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45121-146">Next steps</span></span>
<span data-ttu-id="45121-147">現在，您學到的服務匯流排佇列的 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="45121-147">Now that you've learned hello basics of Service Bus queues, follow these links toolearn more.</span></span>

* <span data-ttu-id="45121-148">[佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)概觀。</span><span class="sxs-lookup"><span data-stu-id="45121-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="45121-149">請瀏覽 hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="45121-149">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="45121-150">如需本文所討論的 hello Azure 服務匯流排佇列和 Azure 佇列中 hello 討論之間的比較[如何 toouse 佇列儲存體從 Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md)發行項，請參閱[Azure 佇列和 Azure Service Bus 佇列-比較和對比](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="45121-150">For a comparison between hello Azure Service Bus queues discussed in this article and Azure Queues discussed in hello [How toouse Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

