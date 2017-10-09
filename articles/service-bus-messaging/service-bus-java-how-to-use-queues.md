---
title: "aaaHow toouse Azure 服務匯流排佇列與 Java |Microsoft 文件"
description: "了解如何 toouse Service Bus 佇列在 Azure 中。 程式碼範例以 Java 撰寫。"
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="cdac3-104">服務匯流排 toouse 排入佇列 java</span><span class="sxs-lookup"><span data-stu-id="cdac3-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="cdac3-105">本文說明如何 toouse 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="cdac3-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="cdac3-106">hello 範例以 Java 撰寫，並使用 hello [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="cdac3-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="cdac3-107">hello 涵蓋案例包括**建立佇列**，**傳送和接收訊息**，和**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="cdac3-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="cdac3-108">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="cdac3-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="cdac3-109">請確定您已安裝 hello [Azure SDK for Java] [ Azure SDK for Java]之前建置此範例。</span><span class="sxs-lookup"><span data-stu-id="cdac3-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="cdac3-110">如果您使用 Eclipse，您可以安裝 hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse]包含 hello Azure SDK for Java。</span><span class="sxs-lookup"><span data-stu-id="cdac3-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="cdac3-111">然後，您可以加入 hello **Microsoft Azure Libraries for Java** tooyour 專案：</span><span class="sxs-lookup"><span data-stu-id="cdac3-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="cdac3-112">新增下列 hello `import` hello Java 檔案的陳述式 toohello 頂端：</span><span class="sxs-lookup"><span data-stu-id="cdac3-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="cdac3-113">建立佇列</span><span class="sxs-lookup"><span data-stu-id="cdac3-113">Create a queue</span></span>
<span data-ttu-id="cdac3-114">可以透過 **ServiceBusContract** 類別，來執行服務匯流排佇列的管理作業。</span><span class="sxs-lookup"><span data-stu-id="cdac3-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="cdac3-115">A **ServiceBusContract**物件建構適當的設定封裝的權限 toomanage SAS 權杖，且 hello **ServiceBusContract**類別是 hello 唯一點使用 Azure 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="cdac3-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="cdac3-116">hello **ServiceBusService**類別會提供方法 toocreate、 列舉和刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="cdac3-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="cdac3-117">如何 hello 範例所示**ServiceBusService**物件可以是使用名為佇列的 toocreate `TestQueue`，具有名為命名空間`HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="cdac3-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="cdac3-118">上有方法`QueueInfo`，讓 hello 佇列 toobe 微調的屬性 (例如： tooset hello 預設存留時間 (TTL) 值套用 toobe toomessages 傳送 toohello 佇列)。</span><span class="sxs-lookup"><span data-stu-id="cdac3-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="cdac3-119">hello 下列範例示範如何 toocreate 佇列名為`TestQueue`5 GB 的大小上限：</span><span class="sxs-lookup"><span data-stu-id="cdac3-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="cdac3-120">請注意，您可以使用 hello`listQueues`方法**ServiceBusContract**物件 toocheck，如果在服務命名空間已經存在具有指定名稱的佇列。</span><span class="sxs-lookup"><span data-stu-id="cdac3-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="cdac3-121">傳送訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="cdac3-121">Send messages tooa queue</span></span>
<span data-ttu-id="cdac3-122">toosend 訊息 tooa Service Bus 佇列，您的應用程式會取得**ServiceBusContract**物件。</span><span class="sxs-lookup"><span data-stu-id="cdac3-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="cdac3-123">hello 下列程式碼會示範如何 toosend hello 訊息`TestQueue`hello 中先前建立的佇列`HowToSample`命名空間：</span><span class="sxs-lookup"><span data-stu-id="cdac3-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="cdac3-124">訊息傳送至，並收到來自服務匯流排佇列都是執行個體的 hello [BrokeredMessage] [ BrokeredMessage]類別。</span><span class="sxs-lookup"><span data-stu-id="cdac3-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="cdac3-125">[BrokeredMessage] [ BrokeredMessage]物件具有一組標準屬性 (例如[標籤](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)和[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive))，是使用的 toohold 自訂字典應用程式特定的屬性和任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="cdac3-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="cdac3-126">應用程式可以將任何可序列化的物件傳遞至 hello 建構函式的 hello 設定 hello hello 訊息本文[BrokeredMessage][BrokeredMessage]，，然後才使用 hello 適當的序列化程式tooserialize hello 物件。</span><span class="sxs-lookup"><span data-stu-id="cdac3-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="cdac3-127">此外，您也可以提供 **java.IO.InputStream** 物件。</span><span class="sxs-lookup"><span data-stu-id="cdac3-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="cdac3-128">hello 下列範例會示範如何 toosend 五個測試訊息 toothe `TestQueue` **MessageSender**我們取得 hello 之前的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="cdac3-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="cdac3-129">服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="cdac3-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="cdac3-130">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="cdac3-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="cdac3-131">訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="cdac3-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="cdac3-132">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="cdac3-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="cdac3-133">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="cdac3-133">Receive messages from a queue</span></span>
<span data-ttu-id="cdac3-134">從佇列中的 hello 主要方式 tooreceive 訊息是 toouse **ServiceBusContract**物件。</span><span class="sxs-lookup"><span data-stu-id="cdac3-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="cdac3-135">接收的訊息可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。</span><span class="sxs-lookup"><span data-stu-id="cdac3-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="cdac3-136">當使用 hello **ReceiveAndDelete**模式中，接收是單發式作業-也就是當服務匯流排佇列中接收訊息的讀取的要求，它會標示為正在使用的 hello 訊息，就傳回該 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdac3-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="cdac3-137">**ReceiveAndDelete** （即 hello 預設模式） 的模式是 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="cdac3-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="cdac3-138">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="cdac3-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="cdac3-139">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="cdac3-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="cdac3-140">在**PeekLock**模式中，接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdac3-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="cdac3-141">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdac3-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="cdac3-142">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序**刪除**上收到 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="cdac3-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="cdac3-143">當服務匯流排會看見 hello**刪除**呼叫，它會將標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="cdac3-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="cdac3-144">hello 下列範例示範如何可以接收和處理使用**PeekLock**模式 （未 hello 預設模式）。</span><span class="sxs-lookup"><span data-stu-id="cdac3-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="cdac3-145">hello 下面範例沒有無限迴圈，處理訊息抵達到我們`TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="cdac3-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="cdac3-146">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="cdac3-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="cdac3-147">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="cdac3-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="cdac3-148">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello **unlockMessage**收到 hello 訊息上的方法 (而不是 hello **deleteMessage**方法)。</span><span class="sxs-lookup"><span data-stu-id="cdac3-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="cdac3-149">這樣會導致服務匯流排 toounlock hello hello 佇列訊息，並將其可用 toobe 接收一次，可能是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="cdac3-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="cdac3-150">另外還有相關聯的訊息佇列內鎖定的逾時，如果 hello 應用程式就會失敗 tooprocess hello 訊息之前的鎖定逾時到期 （例如，如果 hello 應用程式當機），則 Service Bus hello 訊息會自動解除鎖定和可讓可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="cdac3-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="cdac3-151">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello **deleteMessage**發出要求，然後 hello 訊息時，已重新傳遞的 toohello 應用程式會在重新啟動。</span><span class="sxs-lookup"><span data-stu-id="cdac3-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="cdac3-152">這通常稱為*至少一旦處理*; 也就是說，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="cdac3-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="cdac3-153">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="cdac3-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="cdac3-154">這通常用來達成 hello **getMessageId** hello 訊息，嘗試傳遞都維持不變的方法。</span><span class="sxs-lookup"><span data-stu-id="cdac3-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdac3-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdac3-155">Next Steps</span></span>
<span data-ttu-id="cdac3-156">現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[佇列、 主題和訂用帳戶][ Queues, topics, and subscriptions]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cdac3-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="cdac3-157">如需詳細資訊，請參閱 hello [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="cdac3-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
