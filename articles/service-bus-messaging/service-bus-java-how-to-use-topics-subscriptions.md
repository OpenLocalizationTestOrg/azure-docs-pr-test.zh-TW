---
title: "如何搭配 Java 使用 Azure 服務匯流排主題 | Microsoft Docs"
description: "使用 Azure 中的服務匯流排主題和訂用帳戶。"
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="3f83a-103">如何透過 Java 使用服務匯流排主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f83a-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="3f83a-104">本指南說明如何使用服務匯流排主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="3f83a-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="3f83a-105">相關範例是以 Java 撰寫並使用 [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="3f83a-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="3f83a-106">涵蓋的案例包括**建立主題和訂用帳戶**、**建立訂用帳戶篩選器**、**傳送訊息至主題**、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3f83a-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="3f83a-107">什麼是服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="3f83a-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="3f83a-108">服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。</span><span class="sxs-lookup"><span data-stu-id="3f83a-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="3f83a-109">使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="3f83a-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![主題概念](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="3f83a-111">有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="3f83a-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="3f83a-112">一個主題可以登錄多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f83a-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="3f83a-113">當訊息傳送至主題時，每個訂用帳戶都可取得訊息來個別處理。</span><span class="sxs-lookup"><span data-stu-id="3f83a-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="3f83a-114">主題的訂用帳戶類似於虛擬佇列，同樣可接收已傳送到主題的訊息複本。</span><span class="sxs-lookup"><span data-stu-id="3f83a-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="3f83a-115">您可以選擇為個別訂用帳戶來登錄主題的篩選規則，以篩選/限制主題的哪些訊息由哪些主題訂用帳戶接收。</span><span class="sxs-lookup"><span data-stu-id="3f83a-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="3f83a-116">服務匯流排主題和訂用帳戶可讓您擴大處理非常多使用者和應用程式上非常大量的訊息。</span><span class="sxs-lookup"><span data-stu-id="3f83a-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="3f83a-117">建立服務命名空間</span><span class="sxs-lookup"><span data-stu-id="3f83a-117">Create a service namespace</span></span>
<span data-ttu-id="3f83a-118">若要開始在 Azure 中使用服務匯流排主題和訂用帳戶，您必須先建立命名空間，它能針對在應用程式內處理服務匯流排資源提供範圍容器。</span><span class="sxs-lookup"><span data-stu-id="3f83a-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="3f83a-119">若要建立命名空間：</span><span class="sxs-lookup"><span data-stu-id="3f83a-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="3f83a-120">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="3f83a-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="3f83a-121">在建置此範例之前，請先確定您已安裝 [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="3f83a-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="3f83a-122">如果您使用的是 Eclipse，則可以安裝包含 Azure SDK for Java 的[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]。</span><span class="sxs-lookup"><span data-stu-id="3f83a-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="3f83a-123">然後您可以將 **Microsoft Azure Libraries for Java** 新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="3f83a-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="3f83a-124">在 Java 檔案頂端新增下列 `import` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="3f83a-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="3f83a-125">將 Azure Libraries for Java 新增至您的建置路徑，並將其納入專案部署組件中。</span><span class="sxs-lookup"><span data-stu-id="3f83a-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="3f83a-126">建立主題</span><span class="sxs-lookup"><span data-stu-id="3f83a-126">Create a topic</span></span>
<span data-ttu-id="3f83a-127">服務匯流排主題的管理作業可透過 **ServiceBusContract** 類別來執行。</span><span class="sxs-lookup"><span data-stu-id="3f83a-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="3f83a-128">**ServiceBusContract** 物件是利用使用權限來封裝 SAS 權杖以加以管理的適當組態所建構，而 **ServiceBusContract** 類別是唯一可與 Azure 通訊的點。</span><span class="sxs-lookup"><span data-stu-id="3f83a-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="3f83a-129">**ServiceBusService** 類別會提供建立、列舉及刪除主題的方法。</span><span class="sxs-lookup"><span data-stu-id="3f83a-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="3f83a-130">下列範例顯示如何使用 **ServiceBusService** 物件來建立名為 `TestTopic` 且命名空間為 `HowToSample` 的主題：</span><span class="sxs-lookup"><span data-stu-id="3f83a-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="3f83a-131">**TopicInfo** 有相關方法可讓您設定主題的屬性 (例如，針對要在傳送至主題的訊息所套用的存留時間 (TTL) 設定預設值)。</span><span class="sxs-lookup"><span data-stu-id="3f83a-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="3f83a-132">下列範例將示範如何使用大小上限為 5 GB 的設定，來建立名為 `TestTopic` 的主題：</span><span class="sxs-lookup"><span data-stu-id="3f83a-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="3f83a-133">請注意，您可以在 **ServiceBusContract** 物件上使用 **listTopics** 方法，來檢查服務命名空間內是否已有指定名稱的主題存在。</span><span class="sxs-lookup"><span data-stu-id="3f83a-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="3f83a-134">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f83a-134">Create subscriptions</span></span>
<span data-ttu-id="3f83a-135">**ServiceBusService** 類別也能用來建立主題的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f83a-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="3f83a-136">為訂閱命名，且能包含選擇性篩選器，以用來限制傳遞至訂閱的虛擬佇列的訊息集合。</span><span class="sxs-lookup"><span data-stu-id="3f83a-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="3f83a-137">使用預設 (MatchAll) 篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f83a-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="3f83a-138">如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。</span><span class="sxs-lookup"><span data-stu-id="3f83a-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="3f83a-139">使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。</span><span class="sxs-lookup"><span data-stu-id="3f83a-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="3f83a-140">下列範例將建立名為 "AllMessages" 的訂用帳戶，並使用預設的 **MatchAll** 篩選器。</span><span class="sxs-lookup"><span data-stu-id="3f83a-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="3f83a-141">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f83a-141">Create subscriptions with filters</span></span>
<span data-ttu-id="3f83a-142">您也可以建立篩選器，讓您界定傳送至主題的哪些訊息應出現在特定主題訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3f83a-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="3f83a-143">訂用帳戶所支援的最具彈性篩選器類型是實作 SQL92 子集的 [SqlFilter][SqlFilter]。</span><span class="sxs-lookup"><span data-stu-id="3f83a-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="3f83a-144">SQL 篩選器會對發佈至主題之訊息的屬性運作。</span><span class="sxs-lookup"><span data-stu-id="3f83a-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="3f83a-145">如需可與 SQL 篩選器搭配使用的運算式詳細資料，請檢閱 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 語法。</span><span class="sxs-lookup"><span data-stu-id="3f83a-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="3f83a-146">以下範例將建立名為 `HighMessages` 的訂用帳戶，而且所含的 [SqlFilter][SqlFilter] 物件只會選取自訂 **MessageNumber** 屬性大於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="3f83a-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="3f83a-147">同樣地，下列範例將建立名為 `LowMessages` 的訂用帳戶，而且所含的 [SqlFilter][SqlFilter] 物件只會選取 **MessageNumber** 屬性小於或等於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="3f83a-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="3f83a-148">現在，當訊息傳送至 `TestTopic` 時，一律會將該訊息傳遞至已訂閱 `AllMessages` 訂用帳戶的接收者，並選擇性地傳遞至已訂閱 `HighMessages` 和 `LowMessages` 訂用帳戶的接收者 (視訊息內容而定)。</span><span class="sxs-lookup"><span data-stu-id="3f83a-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="3f83a-149">傳送訊息至主題</span><span class="sxs-lookup"><span data-stu-id="3f83a-149">Send messages to a topic</span></span>
<span data-ttu-id="3f83a-150">若要將訊息傳送至服務匯流排主題，應用程式會取得 **ServiceBusContract** 物件。</span><span class="sxs-lookup"><span data-stu-id="3f83a-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="3f83a-151">下列程式碼示範如何針對先前在 `HowToSample` 命名空間內建立的 `TestTopic` 主題傳送訊息：</span><span class="sxs-lookup"><span data-stu-id="3f83a-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="3f83a-152">傳送至服務匯流排主題的訊息是 [BrokeredMessage][BrokeredMessage] 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3f83a-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="3f83a-153">[BrokeredMessage][BrokeredMessage]* 物件具有一組標準方法 (例如 **setLabel** 和 **TimeToLive**)、一個用來保存自訂應用程式特定屬性的字典，以及一個任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="3f83a-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3f83a-154">應用程式可設定訊息主體，方法是將任何可序列化物件傳遞到 [BrokeredMessage][BrokeredMessage]的建構函式，接著系統便會使用適當的 **DataContractSerializer** 來將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="3f83a-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="3f83a-155">或者，也可以提供 **java.io.InputStream**。</span><span class="sxs-lookup"><span data-stu-id="3f83a-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="3f83a-156">下列範例將示範如何傳送五則測試訊息至上述程式碼片段中所取得的 `TestTopic` **MessageSender**。</span><span class="sxs-lookup"><span data-stu-id="3f83a-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="3f83a-157">請注意迴圈反覆運算上每個訊息的 **MessageNumber** 屬性值的變化 (這可判斷接收訊息的訂用帳戶為何)：</span><span class="sxs-lookup"><span data-stu-id="3f83a-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="3f83a-158">服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="3f83a-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3f83a-159">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="3f83a-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3f83a-160">主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有限制。</span><span class="sxs-lookup"><span data-stu-id="3f83a-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="3f83a-161">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="3f83a-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="3f83a-162">如何自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="3f83a-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="3f83a-163">若要從訂用帳戶接收訊息，請使用 **ServiceBusContract** 物件。</span><span class="sxs-lookup"><span data-stu-id="3f83a-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="3f83a-164">接收的訊息可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。</span><span class="sxs-lookup"><span data-stu-id="3f83a-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="3f83a-165">使用 **ReceiveAndDelete** 模式時，接收是一次性作業；也就是說，當服務匯流排收到訊息的讀取要求時，它會將此訊息標示為已使用，並將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f83a-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="3f83a-166">**ReceiveAndDelete** 模式是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="3f83a-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3f83a-167">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="3f83a-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="3f83a-168">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="3f83a-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3f83a-169">在 **PeekLock** 模式中，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f83a-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3f83a-170">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f83a-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3f83a-171">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它會在已接收的訊息上呼叫 **Delete**，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="3f83a-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="3f83a-172">當服務匯流排看到 **Delete** 呼叫時，它會將訊息標示為已取用，並將它從主題中移除。</span><span class="sxs-lookup"><span data-stu-id="3f83a-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="3f83a-173">下列範例將說明如何使用 **PeekLock** 模式 (這不是預設模式) 來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="3f83a-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="3f83a-174">下列範例將執行迴圈，並處理 "HighMessages" 訂用帳戶中的訊息，然後在沒有任何訊息時結束 (您也可以將其設為等待新訊息)。</span><span class="sxs-lookup"><span data-stu-id="3f83a-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3f83a-175">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="3f83a-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3f83a-176">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="3f83a-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3f83a-177">如果接收者應用程式因為某些原因無法處理訊息，它可以在已接收的訊息上呼叫 **unlockMessage** 方法 (而不是 **deleteMessage** 方法)。</span><span class="sxs-lookup"><span data-stu-id="3f83a-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="3f83a-178">這將導致服務匯流排將主題中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="3f83a-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3f83a-179">與主題中鎖定之訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="3f83a-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="3f83a-180">如果應用程式在處理訊息之後，尚未發出 **deleteMessage** 要求時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f83a-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="3f83a-181">這通常稱為**至少處理一次**，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="3f83a-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3f83a-182">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="3f83a-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3f83a-183">通常您可使用訊息的 **getMessageId** 方法來達到此目的，該方法將在各個傳遞嘗試中保持不變。</span><span class="sxs-lookup"><span data-stu-id="3f83a-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="3f83a-184">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f83a-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="3f83a-185">刪除主題和訂用帳戶的主要方式，是使用 **ServiceBusContract** 物件。</span><span class="sxs-lookup"><span data-stu-id="3f83a-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="3f83a-186">刪除主題也將會刪除對主題註冊的任何訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f83a-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="3f83a-187">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f83a-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="3f83a-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f83a-188">Next Steps</span></span>
<span data-ttu-id="3f83a-189">現在您已了解服務匯流排佇列的基本概念，請參閱[服務匯流排佇列、主題和訂用帳戶][Service Bus queues, topics, and subscriptions]，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3f83a-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
