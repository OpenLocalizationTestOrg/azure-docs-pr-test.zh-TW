---
title: "使用 Python aaaHow toouse Azure 服務匯流排主題 |Microsoft 文件"
description: "深入了解如何 toouse Azure 服務匯流排主題和訂閱來自 Python。"
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
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="1ce39-103">如何 toouse Service Bus 主題和訂閱使用 Python</span><span class="sxs-lookup"><span data-stu-id="1ce39-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="1ce39-104">本文說明如何 toouse Service Bus 主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="1ce39-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="1ce39-105">hello 範例撰寫的 Python 和使用 hello [Azure Python SDK 封裝][Azure Python package]。</span><span class="sxs-lookup"><span data-stu-id="1ce39-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="1ce39-106">hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。</span><span class="sxs-lookup"><span data-stu-id="1ce39-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="1ce39-107">如需主題和訂閱的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1ce39-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="1ce39-108">如果您需要 tooinstall Python 或 hello [Azure Python 封裝][Azure Python package]，請參閱 hello [Python 安裝指南](../python-how-to-install.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce39-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="1ce39-109">建立主題</span><span class="sxs-lookup"><span data-stu-id="1ce39-109">Create a topic</span></span>
<span data-ttu-id="1ce39-110">hello **ServiceBusService**物件可讓您 toowork 與主題。</span><span class="sxs-lookup"><span data-stu-id="1ce39-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="1ce39-111">加入要在其中任何 Python 檔案 tooprogrammatically 存取服務匯流排的 hello 頂端附近的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1ce39-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="1ce39-112">hello 下列程式碼會建立**ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="1ce39-113">請使用真實的命名空間、共用存取簽章 (SAS) 金鑰名稱和金鑰值來取代 `mynamespace`、`sharedaccesskeyname` 和 `sharedaccesskey`。</span><span class="sxs-lookup"><span data-stu-id="1ce39-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="1ce39-114">您可以從 hello 取得 hello 值 hello SAS 金鑰名稱和值[Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="1ce39-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="1ce39-115">hello`create_topic`方法也支援其他選項，可讓您 toooverride 預設主題設定，例如訊息時間 toolive 或最大主題大小。</span><span class="sxs-lookup"><span data-stu-id="1ce39-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="1ce39-116">hello 下列範例會設定 hello 最大主題大小 too5 GB，而時間 toolive (TTL) 值為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="1ce39-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="1ce39-117">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce39-117">Create subscriptions</span></span>
<span data-ttu-id="1ce39-118">訂用帳戶 tootopics 也會建立以 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="1ce39-119">訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="1ce39-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce39-120">訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題 toowhich 它們所訂用，則會刪除。</span><span class="sxs-lookup"><span data-stu-id="1ce39-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="1ce39-121">建立訂用帳戶與 hello 預設 (MatchAll) 篩選器</span><span class="sxs-lookup"><span data-stu-id="1ce39-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="1ce39-122">hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="1ce39-123">當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="1ce39-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="1ce39-124">hello 下列範例會建立名為訂用帳戶`AllMessages`和使用 hello 預設**MatchAll**篩選器。</span><span class="sxs-lookup"><span data-stu-id="1ce39-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="1ce39-125">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce39-125">Create subscriptions with filters</span></span>
<span data-ttu-id="1ce39-126">您也可以定義可讓您 toospecify tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息篩選器。</span><span class="sxs-lookup"><span data-stu-id="1ce39-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="1ce39-127">hello 最有彈性的訂用帳戶支援的篩選器的類型是**SqlFilter**，它會實作 SQL92 的子集。</span><span class="sxs-lookup"><span data-stu-id="1ce39-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="1ce39-128">SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce39-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="1ce39-129">如需可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請參閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。</span><span class="sxs-lookup"><span data-stu-id="1ce39-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="1ce39-130">您可以加入篩選 tooa 訂用帳戶使用 hello**建立\_規則**方法 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="1ce39-131">這個方法可讓您 tooadd 新篩選 tooan 現有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ce39-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce39-132">因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器或 hello **MatchAll**將會覆寫任何其他您可以指定的篩選器。</span><span class="sxs-lookup"><span data-stu-id="1ce39-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="1ce39-133">您可以藉由使用 hello 移除 hello 預設規則`delete_rule`方法 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="1ce39-134">hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`messagenumber`大於 3 的屬性：</span><span class="sxs-lookup"><span data-stu-id="1ce39-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="1ce39-135">同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與**SqlFilter**只選取有訊息`messagenumber`屬性小於或等於 too3:</span><span class="sxs-lookup"><span data-stu-id="1ce39-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="1ce39-136">現在，當訊息傳送太`mytopic`它永遠傳遞訂閱 tooreceivers toohello **AllMessages**主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello **HighMessages**和**LowMessages**主題訂用帳戶 （取決於 hello 訊息內容）。</span><span class="sxs-lookup"><span data-stu-id="1ce39-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="1ce39-137">傳送訊息 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="1ce39-137">Send messages tooa topic</span></span>
<span data-ttu-id="1ce39-138">toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用 hello`send_topic_message`方法 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="1ce39-139">hello 下列範例會示範如何 toosend 五個測試訊息太`mytopic`。</span><span class="sxs-lookup"><span data-stu-id="1ce39-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="1ce39-140">請注意該 hello `messagenumber` hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：</span><span class="sxs-lookup"><span data-stu-id="1ce39-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="1ce39-141">服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce39-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1ce39-142">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="1ce39-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1ce39-143">訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="1ce39-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="1ce39-144">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="1ce39-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="1ce39-145">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="1ce39-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="1ce39-146">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="1ce39-146">Receive messages from a subscription</span></span>
<span data-ttu-id="1ce39-147">訊息會從訂用帳戶使用 hello 接收`receive_subscription_message`方法上 hello **ServiceBusService**物件：</span><span class="sxs-lookup"><span data-stu-id="1ce39-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="1ce39-148">在讀取時從 hello 訂用帳戶刪除訊息 hello 參數`peek_lock`設定得**False**。</span><span class="sxs-lookup"><span data-stu-id="1ce39-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="1ce39-149">您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它所設定的 hello 參數從 hello 佇列`peek_lock`太**True**。</span><span class="sxs-lookup"><span data-stu-id="1ce39-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="1ce39-150">hello 行為的讀取和刪除 hello 訊息，因為 hello 的一部分接收作業是 hello 最簡單的模型，並最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="1ce39-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="1ce39-151">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="1ce39-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="1ce39-152">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="1ce39-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="1ce39-153">如果 hello`peek_lock`參數設定太**True**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce39-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1ce39-154">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce39-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="1ce39-155">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete`方法上 hello**訊息**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="1ce39-156">hello`delete`方法標示為正在使用的 hello 訊息，並移除 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ce39-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1ce39-157">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="1ce39-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="1ce39-158">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="1ce39-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1ce39-159">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock`方法上 hello**訊息**物件。</span><span class="sxs-lookup"><span data-stu-id="1ce39-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="1ce39-160">這將導致 hello 訂用帳戶內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="1ce39-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1ce39-161">另外還有 hello 訂閱內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="1ce39-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="1ce39-162">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete`呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="1ce39-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="1ce39-163">這通常稱為*至少一旦處理*，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="1ce39-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="1ce39-164">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="1ce39-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="1ce39-165">這通常用來達成 hello **MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。</span><span class="sxs-lookup"><span data-stu-id="1ce39-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="1ce39-166">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce39-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="1ce39-167">主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="1ce39-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="1ce39-168">hello 下列範例顯示如何命名 toodelete hello 主題`mytopic`:</span><span class="sxs-lookup"><span data-stu-id="1ce39-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="1ce39-169">刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="1ce39-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="1ce39-170">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ce39-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="1ce39-171">hello 下列程式碼會示範如何 toodelete 訂用帳戶命名`HighMessages`從 hello`mytopic`主題：</span><span class="sxs-lookup"><span data-stu-id="1ce39-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="1ce39-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ce39-172">Next steps</span></span>
<span data-ttu-id="1ce39-173">現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1ce39-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="1ce39-174">請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。</span><span class="sxs-lookup"><span data-stu-id="1ce39-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="1ce39-175">[SqlFilter.SqlExpression][SqlFilter.SqlExpression] 的參考資料。</span><span class="sxs-lookup"><span data-stu-id="1ce39-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
