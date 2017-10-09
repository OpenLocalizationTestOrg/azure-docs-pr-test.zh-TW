---
title: "aaaHow toouse Service Bus 主題 (Ruby) |Microsoft 文件"
description: "深入了解如何 toouse Service Bus 主題和訂用帳戶在 Azure 中的。 程式碼範例專為 Ruby 應用程式撰寫。"
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
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="fabab-104">如何 toouse Service Bus 主題和訂閱與 Ruby</span><span class="sxs-lookup"><span data-stu-id="fabab-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="fabab-105">本文說明如何 toouse Service Bus 主題和訂閱從 Ruby 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fabab-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="fabab-106">hello 涵蓋案例包括**建立主題和訂用帳戶，來建立訂用帳戶篩選，將訊息傳送**tooa 主題**從訂閱接收訊息**，和**主題和訂用帳戶刪除**。</span><span class="sxs-lookup"><span data-stu-id="fabab-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="fabab-107">如需有關主題和訂閱的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="fabab-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="fabab-108">建立主題</span><span class="sxs-lookup"><span data-stu-id="fabab-108">Create a topic</span></span>
<span data-ttu-id="fabab-109">hello **Azure::ServiceBusService**物件可讓您 toowork 與主題。</span><span class="sxs-lookup"><span data-stu-id="fabab-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="fabab-110">hello 下列程式碼會建立**Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-111">toocreate 主題，使用 hello`create_topic()`方法。</span><span class="sxs-lookup"><span data-stu-id="fabab-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="fabab-112">下列範例中的 hello 建立主題，或如果有的話，會列印出 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fabab-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="fabab-113">您也可以傳遞**Azure::ServiceBus::Topic**其他選項，可讓您 toooverride 預設主題設定，例如訊息時間 toolive 或最大佇列大小的物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="fabab-114">hello 下列範例所示設定 hello 最大佇列大小 too5 GB 和時間 toolive too1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="fabab-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="fabab-115">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fabab-115">Create subscriptions</span></span>
<span data-ttu-id="fabab-116">主題訂用帳戶也會建立以 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-117">訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="fabab-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="fabab-118">訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題它們相關聯，則會被刪除。</span><span class="sxs-lookup"><span data-stu-id="fabab-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="fabab-119">如果您的應用程式包含邏輯 toocreate 訂用帳戶，它應該先檢查 hello 訂用帳戶已經有使用 hello getSubscription 方法。</span><span class="sxs-lookup"><span data-stu-id="fabab-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="fabab-120">建立訂用帳戶與 hello 預設 (MatchAll) 篩選器</span><span class="sxs-lookup"><span data-stu-id="fabab-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="fabab-121">hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="fabab-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="fabab-122">當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="fabab-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="fabab-123">hello 下列範例會建立名為"all messages"訂用帳戶，並使用 hello 預設**MatchAll**篩選器。</span><span class="sxs-lookup"><span data-stu-id="fabab-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="fabab-124">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fabab-124">Create subscriptions with filters</span></span>
<span data-ttu-id="fabab-125">您也可以定義可讓您 toospecify tooa 主題應該會顯示特定的訂用帳戶內傳送的訊息篩選器。</span><span class="sxs-lookup"><span data-stu-id="fabab-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="fabab-126">hello 最有彈性的訂用帳戶支援的篩選器的類型為 hello **Azure::ServiceBus::SqlFilter**，它會實作 SQL92 的子集。</span><span class="sxs-lookup"><span data-stu-id="fabab-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="fabab-127">SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="fabab-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="fabab-128">如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter](service-bus-messaging-sql-filter.md)語法。</span><span class="sxs-lookup"><span data-stu-id="fabab-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="fabab-129">您可以加入篩選 tooa 訂用帳戶使用 hello`create_rule()`方法 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-130">這個方法可讓您 tooadd 新篩選 tooan 現有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fabab-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="fabab-131">因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器，或 hello **MatchAll**將會覆寫任何其他您可以指定的篩選器。</span><span class="sxs-lookup"><span data-stu-id="fabab-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="fabab-132">您可以藉由使用 hello 移除 hello 預設規則`delete_rule()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="fabab-133">hello 下列範例會建立名為 「 高訊息 」 的訂閱**Azure::ServiceBus::SqlFilter**只選取自訂的訊息`message_number`大於 3 的屬性：</span><span class="sxs-lookup"><span data-stu-id="fabab-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="fabab-134">同樣地，hello 下列範例會建立名為訂用帳戶`low-messages`與**Azure::ServiceBus::SqlFilter**只選取有訊息`message_number`屬性小於或等於 too3:</span><span class="sxs-lookup"><span data-stu-id="fabab-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="fabab-135">當訊息現在是否傳送太`test-topic`，它會一律為訂閱的傳遞的 tooreceivers toohello`all-messages`主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`high-messages`和`low-messages`主題訂用帳戶 (視 hello 訊息內容）。</span><span class="sxs-lookup"><span data-stu-id="fabab-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="fabab-136">傳送訊息 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="fabab-136">Send messages tooa topic</span></span>
<span data-ttu-id="fabab-137">toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用 hello`send_topic_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-138">TooService 匯流排主題是 hello 的執行個體傳送訊息**Azure::ServiceBus::BrokeredMessage**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="fabab-139">**Azure::ServiceBus::BrokeredMessage**物件具有一組標準屬性 (例如`label`和`time_to_live`) 的字典，其中使用的 toohold 自訂應用程式特定屬性，和字串資料的主體。</span><span class="sxs-lookup"><span data-stu-id="fabab-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="fabab-140">應用程式可以藉由傳遞字串值 toohello 設定 hello hello 訊息本文`send_topic_message()`方法和任何所需標準屬性將會填入預設值。</span><span class="sxs-lookup"><span data-stu-id="fabab-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="fabab-141">hello 下列範例會示範如何 toosend 五個測試訊息太`test-topic`。</span><span class="sxs-lookup"><span data-stu-id="fabab-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="fabab-142">請注意該 hello `message_number` hello hello 迴圈反覆運算上的每個訊息的自訂屬性值而有所不同 （這會決定哪一個訂閱能收到它）：</span><span class="sxs-lookup"><span data-stu-id="fabab-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="fabab-143">服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="fabab-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="fabab-144">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="fabab-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="fabab-145">訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="fabab-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="fabab-146">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="fabab-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="fabab-147">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="fabab-147">Receive messages from a subscription</span></span>
<span data-ttu-id="fabab-148">訊息會從訂用帳戶使用 hello 接收`receive_subscription_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-149">根據預設，訊息會 read(peak)，但不會刪除從 hello 訂用帳戶已鎖定。</span><span class="sxs-lookup"><span data-stu-id="fabab-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="fabab-150">您可以讀取並刪除 hello 訂用帳戶中的 hello 訊息，所設定的 hello`peek_lock`太選項**false**。</span><span class="sxs-lookup"><span data-stu-id="fabab-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="fabab-151">hello 預設行為可讓 hello 讀取和刪除兩階段作業，也使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fabab-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="fabab-152">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fabab-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="fabab-153">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete_subscription_message()`方法並提供 hello 訊息 toobe 刪除做為參數。</span><span class="sxs-lookup"><span data-stu-id="fabab-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="fabab-154">hello`delete_subscription_message()`方法會標示為正在使用的 hello 訊息，並移除從 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fabab-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="fabab-155">如果 hello`:peek_lock`參數設定太**false**，讀取和刪除 hello 訊息會變成 hello 最簡單的模型，並且適合用於應用程式可以容許不處理訊息的 hello 事件中的案例失敗。</span><span class="sxs-lookup"><span data-stu-id="fabab-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="fabab-156">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="fabab-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="fabab-157">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="fabab-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="fabab-158">hello 下列範例示範如何可以接收和處理使用`receive_subscription_message()`。</span><span class="sxs-lookup"><span data-stu-id="fabab-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="fabab-159">hello 範例先接收並刪除 hello 訊息`low-messages`訂用帳戶使用`:peek_lock`設定得**false**，然後在另一則訊息收到 hello `high-messages` ，然後刪除 hello 訊息使用`delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="fabab-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="fabab-160">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="fabab-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="fabab-161">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="fabab-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="fabab-162">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock_subscription_message()`方法上 hello **Azure::ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fabab-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="fabab-163">這樣會導致服務匯流排 toounlock hello 訊息 hello 訂用帳戶內，並將其可用 toobe 接收一次，可能是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="fabab-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="fabab-164">另外還有 hello 訂閱內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排會解除鎖定 hello 訊息自動，並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="fabab-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="fabab-165">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete_subscription_message()`呼叫方法時，則 hello 訊息時，已重新傳遞的 toohello 應用程式會在重新啟動。</span><span class="sxs-lookup"><span data-stu-id="fabab-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="fabab-166">這通常稱為*至少一旦處理*; 也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="fabab-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="fabab-167">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="fabab-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="fabab-168">這個邏輯通常用來達成 hello `message_id` hello 訊息，將會維持所有傳遞嘗試的屬性。</span><span class="sxs-lookup"><span data-stu-id="fabab-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="fabab-169">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fabab-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="fabab-170">主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="fabab-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="fabab-171">下列的 hello 範例示範如何命名 toodelete hello 主題`test-topic`。</span><span class="sxs-lookup"><span data-stu-id="fabab-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="fabab-172">刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="fabab-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="fabab-173">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fabab-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="fabab-174">hello 下列程式碼示範如何 toodelete hello 訂用帳戶命名`high-messages`從 hello`test-topic`主題：</span><span class="sxs-lookup"><span data-stu-id="fabab-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="fabab-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fabab-175">Next steps</span></span>
<span data-ttu-id="fabab-176">現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="fabab-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="fabab-177">請參閱[佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)。</span><span class="sxs-lookup"><span data-stu-id="fabab-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="fabab-178">[SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) 的 API 參考資料。</span><span class="sxs-lookup"><span data-stu-id="fabab-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="fabab-179">請瀏覽 hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fabab-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
