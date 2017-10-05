---
title: "如何搭配 Ruby 使用 Azure 服務匯流排佇列 | Microsoft Docs"
description: "了解如何使用 Azure 中的服務匯流排佇列。 程式碼範例以 Ruby 撰寫。"
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
ms.openlocfilehash: 357a7277dd42b6973cf35a9f642b8eec36a745e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-ruby"></a><span data-ttu-id="dfbe5-104">如何將服務匯流排佇列搭配 Ruby 使用</span><span class="sxs-lookup"><span data-stu-id="dfbe5-104">How to use Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="dfbe5-105">本指南將說明如何使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-105">This guide describes how to use Service Bus queues.</span></span> <span data-ttu-id="dfbe5-106">這些範例均以 Ruby 撰寫，並使用 Azure gem。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-106">The samples are written in Ruby and use the Azure gem.</span></span> <span data-ttu-id="dfbe5-107">本文說明的案例包括**建立佇列、傳送並接收訊息**，以及**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-107">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="dfbe5-108">如需服務匯流排佇列的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-108">For more information about Service Bus queues, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="dfbe5-109">如何建立佇列</span><span class="sxs-lookup"><span data-stu-id="dfbe5-109">How to create a queue</span></span>
<span data-ttu-id="dfbe5-110">**Azure::ServiceBusService** 物件可讓您使用佇列。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-110">The **Azure::ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="dfbe5-111">若要建立佇列，請使用 `create_queue()` 方法。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-111">To create a queue, use the `create_queue()` method.</span></span> <span data-ttu-id="dfbe5-112">下列範例會建立佇列，或列印出任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-112">The following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="dfbe5-113">您也可以使用其他選項傳遞 **Azure::ServiceBus::Queue** 物件，這可讓您覆寫訊息存留時間或佇列大小上限等預設佇列設定。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size.</span></span> <span data-ttu-id="dfbe5-114">下列範例說明如何將佇列大小上限設為 5 GB，將存留時間設為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="dfbe5-114">The following example shows how to set the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="dfbe5-115">如何傳送訊息至佇列</span><span class="sxs-lookup"><span data-stu-id="dfbe5-115">How to send messages to a queue</span></span>
<span data-ttu-id="dfbe5-116">若要傳送訊息至服務匯流排佇列，應用程式將呼叫 **Azure::ServiceBusService** 物件上的 `send_queue_message()` 方法。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-116">To send a message to a Service Bus queue, your application calls the `send_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="dfbe5-117">傳送至 (及接收自)「服務匯流排」佇列的訊息是 **Azure::ServiceBus::BrokeredMessage** 物件，而且具有一組標準屬性 (例如 `label` 和 `time_to_live`)、一個用來保存自訂應用程式特定屬性的字典，以及一堆任意的應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-117">Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="dfbe5-118">應用程式可用訊息的形式傳遞字串值以設定訊息內文，任何必要的標準屬性都會以預設值填入。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-118">An application can set the body of the message by passing a string value as the message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="dfbe5-119">下列範例示範如何使用 `send_queue_message()` 將測試訊息傳送至名為 `test-queue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="dfbe5-119">The following example demonstrates how to send a test message to the queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="dfbe5-120">服務匯流排佇列支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-120">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="dfbe5-121">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-121">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="dfbe5-122">佇列中所保存的訊息數目沒有限制，但佇列所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-122">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="dfbe5-123">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="dfbe5-124">如何從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="dfbe5-124">How to receive messages from a queue</span></span>
<span data-ttu-id="dfbe5-125">對於 **Azure::ServiceBusService** 物件使用 `receive_queue_message()` 方法即可從佇列接收訊息。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-125">Messages are received from a queue using the `receive_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="dfbe5-126">根據預設，在讀取及鎖定訊息後並不會將其從佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-126">By default, messages are read and locked without being deleted from the queue.</span></span> <span data-ttu-id="dfbe5-127">但您可以將 `:peek_lock` 選項設為 **false**，而在讀取訊息後將其從佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-127">However, you can delete messages from the queue as they are read by setting the `:peek_lock` option to **false**.</span></span>

<span data-ttu-id="dfbe5-128">預設行為會使讀取和刪除變成兩階段作業，因此也可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-128">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="dfbe5-129">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-129">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="dfbe5-130">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫 `delete_queue_message()` 方法和以參數形式提供要刪除的訊息，完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-130">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_queue_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="dfbe5-131">`delete_queue_message()` 方法會將訊息標示為已取用，並將其從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-131">The `delete_queue_message()` method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="dfbe5-132">如果 `:peek_lock` 參數設為 **false**，讀取和刪除訊息將會變成最簡單的模型，且最適用於應用程式容許在發生失敗時不處理訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-132">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="dfbe5-133">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-133">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="dfbe5-134">因為服務匯流排已將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-134">Because Service Bus has marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="dfbe5-135">下列範例示範如何使用 `receive_queue_message()` 來接收和處理訊息。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-135">The following example demonstrates how to receive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="dfbe5-136">此範例會先使用設為 **false** 的 `:peek_lock` 來接收及刪除訊息，然後再接收另一個訊息，接著使用 `delete_queue_message()` 刪除訊息：</span><span class="sxs-lookup"><span data-stu-id="dfbe5-136">The example first receives and deletes a message by using `:peek_lock` set to **false**, then it receives another message and then deletes the message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="dfbe5-137">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="dfbe5-137">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="dfbe5-138">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-138">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="dfbe5-139">如果接收者應用程式因為某些原因無法處理訊息，它可以呼叫 **Azure::ServiceBusService** 物件上的 `unlock_queue_message()` 方法。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-139">If a receiver application is unable to process the message for some reason, then it can call the `unlock_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="dfbe5-140">此呼叫將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-140">This call causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="dfbe5-141">與在佇列內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-141">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="dfbe5-142">如果應用程式在處理訊息之後，尚未呼叫 `delete_queue_message()` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-142">In the event that the application crashes after processing the message but before the `delete_queue_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="dfbe5-143">此程序通常稱為 *至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="dfbe5-144">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-144">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="dfbe5-145">通常您可使用訊息的 `message_id` 屬性來達到此目的，該方法在各個傳遞嘗試中保持不變。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-145">This is often achieved using the `message_id` property of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfbe5-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfbe5-146">Next steps</span></span>
<span data-ttu-id="dfbe5-147">了解基本的服務匯流排佇列之後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-147">Now that you've learned the basics of Service Bus queues, follow these links to learn more.</span></span>

* <span data-ttu-id="dfbe5-148">[佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)概觀。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="dfbe5-149">請造訪 GitHub 上的 [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="dfbe5-149">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="dfbe5-150">若要比較本文所討論的 Azure 服務匯流排佇列與[如何使用 Ruby 的佇列儲存體](../storage/queues/storage-ruby-how-to-use-queue-storage.md)一文中討論的 Azure 佇列，請參閱 [Azure 佇列和 Azure 服務匯流排佇列 - 比較和對照](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="dfbe5-150">For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

