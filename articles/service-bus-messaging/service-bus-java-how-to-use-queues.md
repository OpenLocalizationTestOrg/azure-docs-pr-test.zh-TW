---
title: "如何搭配 Java 使用 Azure 服務匯流排佇列 | Microsoft Docs"
description: "了解如何使用 Azure 中的服務匯流排佇列。 程式碼範例以 Java 撰寫。"
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
ms.openlocfilehash: 170f431525ffdc93a01fc085e48e69c3a774968e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-java"></a><span data-ttu-id="acc9f-104">如何將服務匯流排佇列搭配 Java 使用</span><span class="sxs-lookup"><span data-stu-id="acc9f-104">How to use Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="acc9f-105">本文說明如何使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="acc9f-105">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="acc9f-106">相關範例是以 Java 撰寫，並且使用 [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="acc9f-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="acc9f-107">本文說明的案例包括**建立佇列**、**傳送並接收訊息**，以及**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="acc9f-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="acc9f-108">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="acc9f-108">Configure your application to use Service Bus</span></span>
<span data-ttu-id="acc9f-109">在建置此範例之前，請先確定您已安裝 [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="acc9f-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="acc9f-110">如果您使用的是 Eclipse，則可以安裝包含 Azure SDK for Java 的[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="acc9f-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="acc9f-111">然後您可以將 **Microsoft Azure Libraries for Java** 新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="acc9f-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="acc9f-112">在 Java 檔案頂端新增下列 `import` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="acc9f-112">Add the following `import` statements to the top of the Java file:</span></span>

```java
// Include the following imports to use Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="acc9f-113">建立佇列</span><span class="sxs-lookup"><span data-stu-id="acc9f-113">Create a queue</span></span>
<span data-ttu-id="acc9f-114">可以透過 **ServiceBusContract** 類別，來執行服務匯流排佇列的管理作業。</span><span class="sxs-lookup"><span data-stu-id="acc9f-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="acc9f-115">**ServiceBusContract** 物件是利用使用權限來封裝 SAS 權杖以加以管理的適當組態所建構，而 **ServiceBusContract** 類別是唯一可與 Azure 通訊的點。</span><span class="sxs-lookup"><span data-stu-id="acc9f-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="acc9f-116">**ServiceBusService** 類別提供建立、列舉及刪除佇列的方法。</span><span class="sxs-lookup"><span data-stu-id="acc9f-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span></span> <span data-ttu-id="acc9f-117">以下範例顯示如何使用 **ServiceBusService** 物件建立名稱為 `TestQueue` 的佇列及名稱為 `HowToSample`的命名空間：</span><span class="sxs-lookup"><span data-stu-id="acc9f-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

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

<span data-ttu-id="acc9f-118">`QueueInfo` 有相關方法可讓您調整佇列的屬性 (例如，針對要在傳送至佇列的訊息所套用的存留時間 (TTL) 設定預設值)。</span><span class="sxs-lookup"><span data-stu-id="acc9f-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span></span> <span data-ttu-id="acc9f-119">下列範例示範如何使用大小上限為 5 GB 的設定，來建立名為 `TestQueue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="acc9f-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="acc9f-120">請注意，您可以在 **ServiceBusContract** 物件上使用 `listQueues` 方法，來檢查服務命名空間內是否已有指定名稱的佇列存在。</span><span class="sxs-lookup"><span data-stu-id="acc9f-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="acc9f-121">傳送訊息至佇列</span><span class="sxs-lookup"><span data-stu-id="acc9f-121">Send messages to a queue</span></span>
<span data-ttu-id="acc9f-122">若要將訊息傳送至服務匯流排佇列，應用程式會取得 **ServiceBusContract** 物件。</span><span class="sxs-lookup"><span data-stu-id="acc9f-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="acc9f-123">下列程式碼示範如何針對先前在 `HowToSample` 命名空間中建立的 `TestQueue` 佇列傳送訊息：</span><span class="sxs-lookup"><span data-stu-id="acc9f-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span></span>

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

<span data-ttu-id="acc9f-124">傳送至 (及接收自)「服務匯流排」佇列的訊息是 [BrokeredMessage][BrokeredMessage] 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="acc9f-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="acc9f-125">[BrokeredMessage][BrokeredMessage] 物件具有一組標準屬性 (例如 [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 和 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive))、一個用來保存自訂應用程式特定屬性的字典，以及一堆任意的應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="acc9f-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="acc9f-126">應用程式可以設定訊息本文，方法是將任何可序列化物件傳遞到 [BrokeredMessage][BrokeredMessage] 的建構函式，接著系統便會使用適當的序列化程式將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="acc9f-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span></span> <span data-ttu-id="acc9f-127">此外，您也可以提供 **java.IO.InputStream** 物件。</span><span class="sxs-lookup"><span data-stu-id="acc9f-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="acc9f-128">下列範例示範如何將五則測試訊息傳送至上述程式碼片段中所取得的 `TestQueue` **MessageSender**：</span><span class="sxs-lookup"><span data-stu-id="acc9f-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for the body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message to the queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="acc9f-129">服務匯流排佇列支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="acc9f-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="acc9f-130">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="acc9f-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="acc9f-131">佇列中所保存的訊息數目沒有限制，但佇列所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="acc9f-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="acc9f-132">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="acc9f-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="acc9f-133">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="acc9f-133">Receive messages from a queue</span></span>
<span data-ttu-id="acc9f-134">自佇列接收訊息的主要方式是使用 **ServiceBusContract** 物件。</span><span class="sxs-lookup"><span data-stu-id="acc9f-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="acc9f-135">接收的訊息可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。</span><span class="sxs-lookup"><span data-stu-id="acc9f-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="acc9f-136">使用 **ReceiveAndDelete** 模式時，接收是一次性作業；也就是說，當服務匯流排在佇列中收到訊息的讀取要求時，它會將此訊息標示為已使用，並將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc9f-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="acc9f-137">**ReceiveAndDelete** 模式 (此為預設模式) 是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="acc9f-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="acc9f-138">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="acc9f-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span>
<span data-ttu-id="acc9f-139">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="acc9f-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="acc9f-140">在 **PeekLock** 模式中，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc9f-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="acc9f-141">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc9f-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="acc9f-142">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它會在已接收的訊息上呼叫 **Delete**，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="acc9f-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="acc9f-143">當服務匯流排看到 **Delete** 呼叫時，它會將訊息標示為已取用，並將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="acc9f-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="acc9f-144">以下範例示範如何使用 **PeekLock** 模式 (非預設模式) 來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="acc9f-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="acc9f-145">下列範例會建立一個無限迴圈，並處理 `TestQueue` 的訊息：</span><span class="sxs-lookup"><span data-stu-id="acc9f-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

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
            // Display the queue message.
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
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="acc9f-146">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="acc9f-146">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="acc9f-147">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="acc9f-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="acc9f-148">如果接收者應用程式因為某些原因無法處理訊息，它可以在已接收的訊息上呼叫 **unlockMessage** 方法 (而不是 **deleteMessage** 方法)。</span><span class="sxs-lookup"><span data-stu-id="acc9f-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="acc9f-149">這將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="acc9f-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="acc9f-150">與在佇列內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="acc9f-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="acc9f-151">在處理訊息之後和發出 **deleteMessage** 要求之前，如果應用程式當機，則會在應用程式重新啟動時，將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc9f-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="acc9f-152">這通常稱為 *至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="acc9f-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="acc9f-153">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="acc9f-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="acc9f-154">通常您可使用訊息的 **getMessageId** 方法來達到此目的，該方法將在各個傳遞嘗試中保持不變。</span><span class="sxs-lookup"><span data-stu-id="acc9f-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acc9f-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acc9f-155">Next Steps</span></span>
<span data-ttu-id="acc9f-156">既然您已了解「服務匯流排」佇列的基本概念，請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]來取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="acc9f-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="acc9f-157">如需詳細資訊，請參閱 [Java 開發人員中心](https://azure.microsoft.com/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="acc9f-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
