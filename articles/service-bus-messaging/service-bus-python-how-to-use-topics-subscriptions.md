---
title: "如何搭配 Python 使用 Azure 服務匯流排主題 | Microsoft Docs"
description: "了解如何從 Python 使用 Azure 服務匯流排主題和訂用帳戶。"
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 15269f9728e9dc45e6436e53b1859f76d4a7a0c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="25325-103">如何透過 Python 使用服務匯流排主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25325-103">How to use Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="25325-104">本文說明如何使用服務匯流排主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="25325-104">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="25325-105">相關範例是以 Python 撰寫，並且使用 [Azure Python SDK 套件][Azure Python package]。</span><span class="sxs-lookup"><span data-stu-id="25325-105">The samples are written in Python and use the [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="25325-106">涵蓋的案例包括**建立主題和訂用帳戶**、**建立訂用帳戶篩選器**、**傳送訊息至主題**、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="25325-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="25325-107">如需主題和訂用帳戶的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="25325-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="25325-108">如果您需要安裝 Python 或 [Azure Python 套件][Azure Python package]，請參閱 [Python 安裝指南](../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="25325-108">If you need to install Python or the [Azure Python package][Azure Python package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="25325-109">建立主題</span><span class="sxs-lookup"><span data-stu-id="25325-109">Create a topic</span></span>
<span data-ttu-id="25325-110">**ServiceBusService** 物件可讓您使用主題。</span><span class="sxs-lookup"><span data-stu-id="25325-110">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="25325-111">將下列內容新增至您想要在其中以程式設計方式存取服務匯流排之任何 Python 檔案內的頂端附近：</span><span class="sxs-lookup"><span data-stu-id="25325-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="25325-112">下列程式碼將建立 **ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="25325-112">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="25325-113">請使用真實的命名空間、共用存取簽章 (SAS) 金鑰名稱和金鑰值來取代 `mynamespace`、`sharedaccesskeyname` 和 `sharedaccesskey`。</span><span class="sxs-lookup"><span data-stu-id="25325-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="25325-114">您可以從 [Azure 入口網站][Azure portal]取得 SAS 金鑰名稱和值的值。</span><span class="sxs-lookup"><span data-stu-id="25325-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="25325-115">`create_topic` 方法也支援其他選項，而可讓您覆寫訊息存留時間或主題大小上限等預設主題設定。</span><span class="sxs-lookup"><span data-stu-id="25325-115">The `create_topic` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="25325-116">下列範例會將主題大小上限設為 5 GB，並將存留時間 (TTL) 的值設為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="25325-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="25325-117">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25325-117">Create subscriptions</span></span>
<span data-ttu-id="25325-118">**ServiceBusService** 物件也能用來建立主題的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="25325-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="25325-119">訂閱是具名的，它們能擁有選用的篩選器，以限制傳遞至訂閱之虛擬佇列的訊息集合。</span><span class="sxs-lookup"><span data-stu-id="25325-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="25325-120">訂用帳戶是持續性的，它們會持續存在，直到本身或它們訂閱的主題遭到刪除為止。</span><span class="sxs-lookup"><span data-stu-id="25325-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="25325-121">使用預設 (MatchAll) 篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25325-121">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="25325-122">如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。</span><span class="sxs-lookup"><span data-stu-id="25325-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="25325-123">使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。</span><span class="sxs-lookup"><span data-stu-id="25325-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="25325-124">下列範例將建立名為 `AllMessages` 的訂用帳戶，並使用預設的 **MatchAll** 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="25325-124">The following example creates a subscription named `AllMessages` and uses the default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="25325-125">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25325-125">Create subscriptions with filters</span></span>
<span data-ttu-id="25325-126">您也可以定義篩選器，讓您指定傳送至主題的哪些訊息應顯示在特定主題訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="25325-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="25325-127">在訂用帳戶支援的篩選器中，實作 SQL92 子集的 **SqlFilter** 是最具彈性的類型。</span><span class="sxs-lookup"><span data-stu-id="25325-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="25325-128">SQL 篩選器會對發佈至主題之訊息的屬性運作。</span><span class="sxs-lookup"><span data-stu-id="25325-128">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="25325-129">如需可與 SQL 篩選器搭配使用的運算式詳細資訊，請參閱 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 語法。</span><span class="sxs-lookup"><span data-stu-id="25325-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="25325-130">您可以使用 **ServiceBusService** 物件的 **create\_rule** 方法將篩選器新增至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="25325-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="25325-131">此方法可讓您將篩選器新增至現有的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="25325-131">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="25325-132">由於預設篩選器會自動套用至所有新的訂用帳戶，因此您必須先移除預設篩選器，否則 **MatchAll** 將會覆寫您指定的任何其他篩選器。</span><span class="sxs-lookup"><span data-stu-id="25325-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="25325-133">您可以使用 **ServiceBusService** 物件的 `delete_rule` 方法移除預設規則。</span><span class="sxs-lookup"><span data-stu-id="25325-133">You can remove the default rule by using the `delete_rule` method of the **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="25325-134">以下範例將建立名為 `HighMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取自訂 `messagenumber` 屬性大於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="25325-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="25325-135">同樣地，下列範例將建立名為 `LowMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取 `messagenumber` 屬性小於或等於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="25325-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="25325-136">現在當訊息傳送到 `mytopic` 時，一律會將該訊息傳遞到已訂閱 **AllMessages** 主題訂用帳戶的接收者，並選擇性地將它傳遞到已訂閱 **HighMessages** 和 **LowMessages** 主題訂用帳戶的接收者 (視訊息內容而定)。</span><span class="sxs-lookup"><span data-stu-id="25325-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="25325-137">傳送訊息至主題</span><span class="sxs-lookup"><span data-stu-id="25325-137">Send messages to a topic</span></span>
<span data-ttu-id="25325-138">若要將訊息傳送至服務匯流排主題，應用程式必須使用 **ServiceBusService** 物件的 `send_topic_message` 方法。</span><span class="sxs-lookup"><span data-stu-id="25325-138">To send a message to a Service Bus topic, your application must use the `send_topic_message` method of the **ServiceBusService** object.</span></span>

<span data-ttu-id="25325-139">下列範例說明如何將五個測試訊息傳送至 `mytopic`。</span><span class="sxs-lookup"><span data-stu-id="25325-139">The following example demonstrates how to send five test messages to `mytopic`.</span></span> <span data-ttu-id="25325-140">請注意，迴圈反覆運算上每個訊息的 `messagenumber` 屬性值會有變化 (這可判斷接收訊息的訂用帳戶為何)：</span><span class="sxs-lookup"><span data-stu-id="25325-140">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="25325-141">服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="25325-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="25325-142">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="25325-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="25325-143">主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="25325-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="25325-144">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="25325-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="25325-145">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="25325-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="25325-146">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="25325-146">Receive messages from a subscription</span></span>
<span data-ttu-id="25325-147">對於 **ServiceBusService** 物件使用 `receive_subscription_message` 方法即可從佇列接收訊息：</span><span class="sxs-lookup"><span data-stu-id="25325-147">Messages are received from a subscription using the `receive_subscription_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="25325-148">將 `peek_lock` 參數設為 **False** 時，則當讀取訊息後，訊息便會從訂用帳戶中刪除。</span><span class="sxs-lookup"><span data-stu-id="25325-148">Messages are deleted from the subscription as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="25325-149">您可以將參數 `peek_lock` 設為 **True**，來讀取 (查看) 並鎖定訊息，避免系統從佇列刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="25325-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="25325-150">隨著接收作業讀取及刪除訊息之行為是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="25325-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="25325-151">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="25325-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="25325-152">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="25325-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="25325-153">如果您將 `peek_lock` 參數設為 **True**，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="25325-153">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="25325-154">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="25325-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="25325-155">在應用程式完成訊息處理 (或可靠地儲存此訊息以供未來處理) 之後，它會在 **Message** 物件上呼叫 `delete` 方法，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="25325-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete` method on the **Message** object.</span></span> <span data-ttu-id="25325-156">`delete` 方法會將訊息標示為已取用，並將其從訂用帳戶中移除。</span><span class="sxs-lookup"><span data-stu-id="25325-156">The `delete` method marks the message as being consumed and removes it from the subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="25325-157">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="25325-157">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="25325-158">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="25325-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="25325-159">如果接收者應用程式因為某些原因無法處理訊息，它可以在 **Message** 物件上呼叫 `unlock` 方法。</span><span class="sxs-lookup"><span data-stu-id="25325-159">If a receiver application is unable to process the message for some reason, then it can call the `unlock` method on the **Message** object.</span></span> <span data-ttu-id="25325-160">這將導致服務匯流排將訂用帳戶中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="25325-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="25325-161">與在訂閱內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="25325-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="25325-162">如果應用程式在處理訊息之後，尚未呼叫 `delete` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="25325-162">In the event that the application crashes after processing the message but before the `delete` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="25325-163">這通常稱為*至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="25325-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="25325-164">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="25325-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="25325-165">通常您可使用訊息的 **MessageId** 屬性來達到此目的，該屬性將在各個傳遞嘗試中會保持不變。</span><span class="sxs-lookup"><span data-stu-id="25325-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="25325-166">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25325-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="25325-167">主題和訂用帳戶是持續性的，您必須透過 [Azure 入口網站][Azure portal]或以程式設計方式明確地刪除它們。</span><span class="sxs-lookup"><span data-stu-id="25325-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="25325-168">下列範例示範如何刪除名為 `mytopic` 的主題：</span><span class="sxs-lookup"><span data-stu-id="25325-168">The following example shows how to delete the topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="25325-169">刪除主題也將會刪除對主題註冊的任何訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="25325-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="25325-170">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="25325-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="25325-171">下列程式碼示範如何從 `mytopic` 主題刪除名為 `HighMessages` 的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="25325-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="25325-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25325-172">Next steps</span></span>
<span data-ttu-id="25325-173">了解基本的服務匯流排主題之後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="25325-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="25325-174">請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。</span><span class="sxs-lookup"><span data-stu-id="25325-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="25325-175">[SqlFilter.SqlExpression][SqlFilter.SqlExpression] 的參考資料。</span><span class="sxs-lookup"><span data-stu-id="25325-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
