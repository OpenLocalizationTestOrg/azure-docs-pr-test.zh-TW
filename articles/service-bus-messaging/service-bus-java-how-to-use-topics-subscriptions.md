---
title: "使用 Java aaaHow toouse Azure 服務匯流排主題 |Microsoft 文件"
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
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="7da45-103">如何 toouse Service Bus 主題和訂閱與 Java</span><span class="sxs-lookup"><span data-stu-id="7da45-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7da45-104">本指南說明如何 toouse Service Bus 主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="7da45-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="7da45-105">hello 範例以 Java 撰寫，並使用 hello [Azure SDK for Java][Azure SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="7da45-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="7da45-106">hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。</span><span class="sxs-lookup"><span data-stu-id="7da45-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="7da45-107">什麼是服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="7da45-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="7da45-108">服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。</span><span class="sxs-lookup"><span data-stu-id="7da45-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="7da45-109">使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="7da45-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![主題概念](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="7da45-111">有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="7da45-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="7da45-112">就可以註冊多個訂用帳戶 tooa 主題。</span><span class="sxs-lookup"><span data-stu-id="7da45-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="7da45-113">當訊息傳送 tooa 主題時，它就可使用可用 tooeach 訂用帳戶 toohandle/處理序分開。</span><span class="sxs-lookup"><span data-stu-id="7da45-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="7da45-114">訂用帳戶 tooa 主題類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。</span><span class="sxs-lookup"><span data-stu-id="7da45-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="7da45-115">您可以選擇性地註冊主題以每個訂用帳戶為基礎，可讓您 toofilter/限制哪些主題訂用帳戶所收到的訊息 tooa 主題上的篩選規則。</span><span class="sxs-lookup"><span data-stu-id="7da45-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="7da45-116">服務匯流排主題和訂用帳戶可讓您 tooscale tooprocess 非常大量的訊息在非常大量的使用者和應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da45-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="7da45-117">建立服務命名空間</span><span class="sxs-lookup"><span data-stu-id="7da45-117">Create a service namespace</span></span>
<span data-ttu-id="7da45-118">toobegin 使用服務匯流排主題和訂用帳戶在 Azure 中，您必須先建立的命名空間提供範圍的容器應用程式中的服務匯流排資源定址。</span><span class="sxs-lookup"><span data-stu-id="7da45-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="7da45-119">toocreate 命名空間：</span><span class="sxs-lookup"><span data-stu-id="7da45-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="7da45-120">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="7da45-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="7da45-121">請確定您已安裝 hello [Azure SDK for Java] [ Azure SDK for Java]之前建置此範例。</span><span class="sxs-lookup"><span data-stu-id="7da45-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="7da45-122">如果您使用 Eclipse，您可以安裝 hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse]包含 hello Azure SDK for Java。</span><span class="sxs-lookup"><span data-stu-id="7da45-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="7da45-123">然後，您可以加入 hello **Microsoft Azure Libraries for Java** tooyour 專案：</span><span class="sxs-lookup"><span data-stu-id="7da45-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="7da45-124">新增下列 hello `import` hello Java 檔案的陳述式 toohello 頂端：</span><span class="sxs-lookup"><span data-stu-id="7da45-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="7da45-125">新增 hello Azure Libraries for Java tooyour 建置路徑，並將它加入您的專案部署組件中。</span><span class="sxs-lookup"><span data-stu-id="7da45-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="7da45-126">建立主題</span><span class="sxs-lookup"><span data-stu-id="7da45-126">Create a topic</span></span>
<span data-ttu-id="7da45-127">服務匯流排主題的管理作業可透過 **ServiceBusContract** 類別來執行。</span><span class="sxs-lookup"><span data-stu-id="7da45-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="7da45-128">A **ServiceBusContract**物件建構適當的設定封裝的權限 toomanage SAS 權杖，且 hello **ServiceBusContract**類別是 hello 唯一點使用 Azure 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="7da45-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="7da45-129">hello **ServiceBusService**類別會提供方法 toocreate、 列舉和刪除的主題。</span><span class="sxs-lookup"><span data-stu-id="7da45-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="7da45-130">下列範例會示範如何 hello **ServiceBusService**物件可以用的 toocreate 主題名為`TestTopic`，與呼叫的命名空間`HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="7da45-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="7da45-131">上有方法**TopicInfo**可讓 hello 主題設定的屬性 (例如： tooset hello 預設存留時間 (TTL) 值套用 toobe toomessages 傳送 toohello 主題)。</span><span class="sxs-lookup"><span data-stu-id="7da45-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="7da45-132">hello 下列範例示範如何 toocreate 主題命名`TestTopic`5 GB 的大小上限：</span><span class="sxs-lookup"><span data-stu-id="7da45-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="7da45-133">請注意，您可以使用 hello **listTopics**方法**ServiceBusContract**物件 toocheck，如果在服務命名空間已經存在具有指定名稱的主題。</span><span class="sxs-lookup"><span data-stu-id="7da45-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="7da45-134">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7da45-134">Create subscriptions</span></span>
<span data-ttu-id="7da45-135">訂用帳戶 tootopics 也會建立以 hello **ServiceBusService**類別。</span><span class="sxs-lookup"><span data-stu-id="7da45-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="7da45-136">訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="7da45-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="7da45-137">建立訂用帳戶與 hello 預設 (MatchAll) 篩選器</span><span class="sxs-lookup"><span data-stu-id="7da45-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="7da45-138">hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7da45-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7da45-139">當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題會放在訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="7da45-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="7da45-140">hello 下列範例會建立名為"AllMessages 」 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。</span><span class="sxs-lookup"><span data-stu-id="7da45-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7da45-141">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7da45-141">Create subscriptions with filters</span></span>
<span data-ttu-id="7da45-142">您也可以建立可讓您篩選器 tooscope tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="7da45-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="7da45-143">hello 最有彈性的訂用帳戶支援的篩選器的類型是[SqlFilter][SqlFilter]，它會實作 SQL92 的子集。</span><span class="sxs-lookup"><span data-stu-id="7da45-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="7da45-144">SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="7da45-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="7da45-145">如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。</span><span class="sxs-lookup"><span data-stu-id="7da45-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="7da45-146">hello 下列範例會建立名為訂用帳戶`HighMessages`與[SqlFilter] [ SqlFilter]物件只會選取自訂的訊息， **MessageNumber**大於 3 的內容：</span><span class="sxs-lookup"><span data-stu-id="7da45-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="7da45-147">同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與[SqlFilter] [ SqlFilter]物件，以只選取有訊息**MessageNumber**屬性小於或等於 too3:</span><span class="sxs-lookup"><span data-stu-id="7da45-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="7da45-148">當訊息現在是否傳送太`TestTopic`，它會一律傳送訂閱的 tooreceivers toohello`AllMessages`訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`訂用帳戶 (根據訊息內容）。</span><span class="sxs-lookup"><span data-stu-id="7da45-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="7da45-149">傳送訊息 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="7da45-149">Send messages tooa topic</span></span>
<span data-ttu-id="7da45-150">toosend 訊息 tooa Service Bus 主題，您的應用程式會取得**ServiceBusContract**物件。</span><span class="sxs-lookup"><span data-stu-id="7da45-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="7da45-151">hello 下列程式碼示範如何 toosend hello 訊息`TestTopic`hello 內先前建立的主題`HowToSample`命名空間：</span><span class="sxs-lookup"><span data-stu-id="7da45-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="7da45-152">傳送 tooService 匯流排主題的訊息是的執行個體[BrokeredMessage] [ BrokeredMessage]類別。</span><span class="sxs-lookup"><span data-stu-id="7da45-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="7da45-153">[BrokeredMessage][BrokeredMessage]* 物件具有一組標準方法 (例如**setLabel**和**TimeToLive**)，是使用的 toohold 自訂字典應用程式特定的屬性和任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="7da45-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="7da45-154">應用程式可以將任何可序列化的物件傳遞至 hello 建構函式設定 hello 訊息本文[BrokeredMessage][BrokeredMessage]，並適當 hello **DataContractSerializer**就會使用的 tooserialize hello 物件。</span><span class="sxs-lookup"><span data-stu-id="7da45-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="7da45-155">或者，也可以提供 **java.io.InputStream**。</span><span class="sxs-lookup"><span data-stu-id="7da45-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="7da45-156">hello 下列範例會示範如何 toosend 五個測試訊息 toothe `TestTopic` **MessageSender**我們取得 hello 上述程式碼片段中。</span><span class="sxs-lookup"><span data-stu-id="7da45-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="7da45-157">請注意如何 hello **MessageNumber** hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：</span><span class="sxs-lookup"><span data-stu-id="7da45-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="7da45-158">服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="7da45-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7da45-159">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="7da45-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7da45-160">訊息保留在主題中的 hello 數目沒有限制，但 hello 主題所持有的 hello 訊息總大小沒有限制。</span><span class="sxs-lookup"><span data-stu-id="7da45-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="7da45-161">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="7da45-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="7da45-162">Tooreceive 從訂用帳戶的郵件</span><span class="sxs-lookup"><span data-stu-id="7da45-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="7da45-163">從訂用帳戶，tooreceive 訊息使用**ServiceBusContract**物件。</span><span class="sxs-lookup"><span data-stu-id="7da45-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="7da45-164">接收的訊息可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。</span><span class="sxs-lookup"><span data-stu-id="7da45-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="7da45-165">當使用 hello **ReceiveAndDelete**模式中，接收是單發式作業-也就是當服務匯流排接收訊息的讀取的要求時，它會標示為正在使用的 hello 訊息，就傳回該 toothe 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da45-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="7da45-166">**ReceiveAndDelete**模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="7da45-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="7da45-167">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="7da45-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="7da45-168">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="7da45-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="7da45-169">在**PeekLock**模式中，接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da45-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7da45-170">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da45-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="7da45-171">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序**刪除**上收到 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7da45-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="7da45-172">當服務匯流排會看見 hello**刪除**呼叫，它會將標示為正在使用的 hello 訊息，並移除 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="7da45-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="7da45-173">hello 以下範例示範如何收到訊息的方式，以及處理使用**PeekLock**模式 （未 hello 預設模式）。</span><span class="sxs-lookup"><span data-stu-id="7da45-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="7da45-174">hello 下面範例會執行迴圈和處理 hello"HighMessages 」 訂用帳戶中的訊息，並結束作業沒有任何訊息時 （或者，它無法設定新郵件 toowait）。</span><span class="sxs-lookup"><span data-stu-id="7da45-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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
            // Display hello topic message.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7da45-175">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="7da45-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="7da45-176">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="7da45-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7da45-177">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello **unlockMessage**收到 hello 訊息上的方法 (而不是 hello **deleteMessage**方法)。</span><span class="sxs-lookup"><span data-stu-id="7da45-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="7da45-178">這將導致 hello 主題內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="7da45-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7da45-179">也沒有逾時 > 主題內鎖定的訊息相關聯，而且如果 hello 應用程式失敗 tooprocess hello 訊息之前鎖定逾時 （例如，如果 hello 應用程式當機），然後服務匯流排會自動解除鎖定 hello 訊息並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="7da45-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="7da45-180">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello **deleteMessage**發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="7da45-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="7da45-181">這通常稱為**至少一旦處理**，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="7da45-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="7da45-182">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="7da45-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="7da45-183">這通常用來達成 hello **getMessageId** hello 訊息，將會維持所有傳遞嘗試的方法。</span><span class="sxs-lookup"><span data-stu-id="7da45-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7da45-184">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7da45-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="7da45-185">hello 主要方式 toodelete 主題和訂用帳戶是 toouse **ServiceBusContract**物件。</span><span class="sxs-lookup"><span data-stu-id="7da45-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="7da45-186">刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="7da45-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="7da45-187">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7da45-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="7da45-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7da45-188">Next Steps</span></span>
<span data-ttu-id="7da45-189">現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[服務匯流排佇列、 主題和訂用帳戶][ Service Bus queues, topics, and subscriptions]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7da45-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
