---
title: "如何使用服務匯流排主題 (Ruby) | Microsoft Docs"
description: "了解如何在 Azure 使用服務匯流排主題及訂用帳戶。 程式碼範例專為 Ruby 應用程式撰寫。"
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="15781-104">如何透過 Ruby 使用服務匯流排主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="15781-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="15781-105">本文說明如何從 Ruby 應用程式使用服務匯流排主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15781-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="15781-106">涵蓋的案例包括**建立主題和訂用帳戶、建立訂用帳戶篩選器、傳送訊息**至主題、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="15781-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="15781-107">如需主題和訂用帳戶的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="15781-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="15781-108">建立主題</span><span class="sxs-lookup"><span data-stu-id="15781-108">Create a topic</span></span>
<span data-ttu-id="15781-109">**Azure::ServiceBusService** 物件可讓您使用主題。</span><span class="sxs-lookup"><span data-stu-id="15781-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="15781-110">下列程式碼將建立 **Azure::ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="15781-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-111">若要建立主題，請使用 `create_topic()` 方法。</span><span class="sxs-lookup"><span data-stu-id="15781-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="15781-112">下列範例將建立主題或列印出錯誤 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="15781-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="15781-113">您也可以使用其他選項傳遞 **Azure::ServiceBus::Topic** 物件，這可讓您覆寫訊息存留時間或佇列大小上限等預設主題設定。</span><span class="sxs-lookup"><span data-stu-id="15781-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="15781-114">下列範例說明將佇列大小上限設為 5 GB，將存留時間設為 1 分鐘的設定：</span><span class="sxs-lookup"><span data-stu-id="15781-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="15781-115">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="15781-115">Create subscriptions</span></span>
<span data-ttu-id="15781-116">**Azure::ServiceBusService** 物件也能用來建立主題訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15781-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-117">訂閱是具名的，它們能擁有選用的篩選器，以限制傳遞至訂閱之虛擬佇列的訊息集合。</span><span class="sxs-lookup"><span data-stu-id="15781-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="15781-118">訂用帳戶是持續性的，它們會持續存在，直到本身或相關的主題遭到刪除為止。</span><span class="sxs-lookup"><span data-stu-id="15781-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="15781-119">如果應用程式含有建立訂用帳戶的邏輯，它應該會先使用 getSubscription 方法檢查訂用帳戶是否存在。</span><span class="sxs-lookup"><span data-stu-id="15781-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="15781-120">使用預設 (MatchAll) 篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="15781-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="15781-121">如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。</span><span class="sxs-lookup"><span data-stu-id="15781-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="15781-122">使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。</span><span class="sxs-lookup"><span data-stu-id="15781-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="15781-123">下列範例將建立名為「all-messages」的訂用帳戶，並使用預設的 **MatchAll** 篩選器。</span><span class="sxs-lookup"><span data-stu-id="15781-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="15781-124">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="15781-124">Create subscriptions with filters</span></span>
<span data-ttu-id="15781-125">您也可以定義篩選器，讓您指定傳送至主題的哪些訊息應顯示在特定訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="15781-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="15781-126">在訂用帳戶支援的篩選器中，實作 SQL92 子集的 **Azure::ServiceBus::SqlFilter** 是最具彈性的類型。</span><span class="sxs-lookup"><span data-stu-id="15781-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="15781-127">SQL 篩選器會對發佈至主題之訊息的屬性運作。</span><span class="sxs-lookup"><span data-stu-id="15781-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="15781-128">如需可與 SQL 篩選條件搭配使用的運算式詳細資料，請檢閱 [SqlFilter](service-bus-messaging-sql-filter.md) 語法。</span><span class="sxs-lookup"><span data-stu-id="15781-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="15781-129">您可以使用 **Azure::ServiceBusService** 物件的 `create_rule()` 方法將篩選器新增至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15781-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-130">此方法可讓您將篩選器新增至現有的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="15781-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="15781-131">由於預設篩選器會自動套用至所有新訂用帳戶，因此您必須先移除預設篩選器，否則 **MatchAll** 會覆寫您指定的其他任何篩選器。</span><span class="sxs-lookup"><span data-stu-id="15781-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="15781-132">您可以使用 **Azure::ServiceBusService** 物件上的 `delete_rule()` 方法移除預設規則。</span><span class="sxs-lookup"><span data-stu-id="15781-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="15781-133">以下範例將建立名為 "high-messages" 的訂用帳戶，而且所含的 **Azure::ServiceBus::SqlFilter** 只選取自訂 `message_number` 屬性大於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="15781-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="15781-134">同樣地，下列範例將建立名為 `low-messages` 的訂用帳戶，而且所含的 **Azure::ServiceBus::SqlFilter** 只會選取 `message_number` 屬性小於或等於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="15781-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="15781-135">當訊息傳送至 `test-topic` 時，一律會將該訊息傳遞至已訂閱 `all-messages` 主題訂用帳戶的接收者，並選擇性地傳遞至已訂閱 `high-messages` 和 `low-messages` 主題訂用帳戶的接收者 (視訊息內容而定)。</span><span class="sxs-lookup"><span data-stu-id="15781-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="15781-136">傳送訊息至主題</span><span class="sxs-lookup"><span data-stu-id="15781-136">Send messages to a topic</span></span>
<span data-ttu-id="15781-137">若要將訊息傳送至服務匯流排主題，應用程式必須使用 **Azure::ServiceBusService** 物件的 `send_topic_message()` 方法。</span><span class="sxs-lookup"><span data-stu-id="15781-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-138">傳送至服務匯流排主題的訊息是 **Azure::ServiceBus::BrokeredMessage** 物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="15781-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="15781-139">**Azure::ServiceBus::BrokeredMessage** 物件具有一組標準屬性 (例如 `label` 和 `time_to_live`)、一個用來保存自訂應用程式特定屬性的字典，以及一堆字串資料。</span><span class="sxs-lookup"><span data-stu-id="15781-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="15781-140">應用程式能將字串值傳遞至 `send_topic_message()` 方法以設定訊息本文，系統會將預設值填入任何需要的標準屬性中。</span><span class="sxs-lookup"><span data-stu-id="15781-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="15781-141">下列範例說明如何將五個測試訊息傳送至 `test-topic`。</span><span class="sxs-lookup"><span data-stu-id="15781-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="15781-142">請注意，迴圈反覆運算上每個訊息的 `message_number` 自訂屬性值會有變化 (這可判斷接收訊息的訂用帳戶為何)：</span><span class="sxs-lookup"><span data-stu-id="15781-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="15781-143">服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="15781-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="15781-144">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="15781-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="15781-145">主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="15781-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="15781-146">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="15781-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="15781-147">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="15781-147">Receive messages from a subscription</span></span>
<span data-ttu-id="15781-148">對於 **Azure::ServiceBusService** 物件使用 `receive_subscription_message()` 方法即可從佇列接收訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-149">根據預設，在讀取 (查看) 及鎖定訊息後，並不會從訂用帳戶中刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="15781-150">您可以將 `peek_lock` 選項設為 **false**，而在讀取訊息後從訂用帳戶中刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="15781-151">預設行為會使讀取和刪除變成兩階段作業，因此也可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="15781-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="15781-152">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="15781-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="15781-153">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫 `delete_subscription_message()` 方法和以參數形式提供要刪除的訊息，完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="15781-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="15781-154">`delete_subscription_message()` 方法會將訊息標示為已取用，並將其從訂用帳戶中移除。</span><span class="sxs-lookup"><span data-stu-id="15781-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="15781-155">如果 `:peek_lock` 參數設為 **false**，讀取和刪除訊息將會變成最簡單的模型，且最適用於應用程式容許在發生失敗時不處理訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="15781-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="15781-156">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="15781-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="15781-157">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="15781-158">以下範例將示範如何使用預設的 `receive_subscription_message()` 模式來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="15781-159">此範例會先使用設為 **false** 的 `:peek_lock` 接收及刪除來自 `low-messages` 訂用帳戶的訊息，然後接收另一個來自 `high-messages` 的訊息，接著使用 `delete_subscription_message()` 刪除該訊息：</span><span class="sxs-lookup"><span data-stu-id="15781-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="15781-160">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="15781-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="15781-161">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="15781-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="15781-162">如果接收者應用程式因為某些原因無法處理訊息，它可以呼叫 **Azure::ServiceBusService** 物件上的 `unlock_subscription_message()` 方法。</span><span class="sxs-lookup"><span data-stu-id="15781-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="15781-163">這導致服務匯流排將訂閱中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="15781-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="15781-164">與訂用帳戶內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，讓訊息可以再次被接收。</span><span class="sxs-lookup"><span data-stu-id="15781-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="15781-165">如果應用程式在處理訊息之後，尚未呼叫 `delete_subscription_message()` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="15781-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="15781-166">這通常稱為*至少處理一次*；也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="15781-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="15781-167">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="15781-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="15781-168">通常您可使用訊息的 `message_id` 屬性來達到此邏輯，該屬性將在各個傳遞嘗試中會保持不變。</span><span class="sxs-lookup"><span data-stu-id="15781-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="15781-169">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="15781-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="15781-170">主題和訂用帳戶是持續性的，您必須透過 [Azure 入口網站][Azure portal]或以程式設計方式明確地刪除它們。</span><span class="sxs-lookup"><span data-stu-id="15781-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="15781-171">下列範例說明如何刪除名為 `test-topic` 的主題。</span><span class="sxs-lookup"><span data-stu-id="15781-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="15781-172">刪除主題也將會刪除對主題註冊的任何訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15781-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="15781-173">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15781-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="15781-174">下列程式碼將示範如何將名為 `high-messages` 的訂用帳戶從 `test-topic` 主題中刪除：</span><span class="sxs-lookup"><span data-stu-id="15781-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="15781-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15781-175">Next steps</span></span>
<span data-ttu-id="15781-176">了解基本的服務匯流排主題之後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="15781-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="15781-177">請參閱[佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)。</span><span class="sxs-lookup"><span data-stu-id="15781-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="15781-178">[SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) 的 API 參考資料。</span><span class="sxs-lookup"><span data-stu-id="15781-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="15781-179">請造訪 GitHub 上的 [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="15781-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
