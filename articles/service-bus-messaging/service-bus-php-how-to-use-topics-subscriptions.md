---
title: "使用 PHP aaaHow toouse Service Bus 主題 |Microsoft 文件"
description: "深入了解如何使用 Azure 中的 PHP toouse 服務匯流排主題。"
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="128a0-103">如何 toouse Service Bus 主題和訂閱與 PHP</span><span class="sxs-lookup"><span data-stu-id="128a0-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="128a0-104">本文章將示範如何 toouse Service Bus 主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="128a0-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="128a0-105">hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP](../php-download-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="128a0-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="128a0-106">hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。</span><span class="sxs-lookup"><span data-stu-id="128a0-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="128a0-107">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="128a0-107">Create a PHP application</span></span>
<span data-ttu-id="128a0-108">僅建立 PHP 應用程式存取 hello Azure Blob 服務的需求是在 hello tooreference 類別 hello [Azure SDK for PHP](../php-download-sdk.md)從您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="128a0-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="128a0-109">您可以使用任何開發工具 toocreate，您的應用程式或 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="128a0-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="128a0-110">您的 PHP 安裝也必須擁有 hello [OpenSSL 延伸](http://php.net/openssl)安裝並啟用。</span><span class="sxs-lookup"><span data-stu-id="128a0-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="128a0-111">本文說明如何 toouse 服務內的 PHP 應用程式在本機，或在 Azure web 角色、 背景工作角色或網站中執行程式碼可以呼叫的功能。</span><span class="sxs-lookup"><span data-stu-id="128a0-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="128a0-112">取得 hello Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="128a0-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="128a0-113">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="128a0-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="128a0-114">toouse hello 服務匯流排 Api:</span><span class="sxs-lookup"><span data-stu-id="128a0-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="128a0-115">參考 hello 自動換片器檔案使用 hello [require_once] [ require-once]陳述式。</span><span class="sxs-lookup"><span data-stu-id="128a0-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="128a0-116">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-116">Reference any classes you might use.</span></span>

<span data-ttu-id="128a0-117">hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServiceBusService**類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="128a0-118">此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="128a0-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="128a0-119">如果您是手動或以西洋梨封裝安裝 hello 程式庫，您必須參考 hello **WindowsAzure.php**自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="128a0-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="128a0-120">在下列範例的 hello，hello`require_once`永遠不會顯示陳述式，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。</span><span class="sxs-lookup"><span data-stu-id="128a0-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="128a0-121">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="128a0-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="128a0-122">tooinstantiate 服務匯流排用戶端，您必須先有有效的連接字串格式如下：</span><span class="sxs-lookup"><span data-stu-id="128a0-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="128a0-123">其中`Endpoint`的 hello 格式通常是`https://[yourNamespace].servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="128a0-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="128a0-124">toocreate 任何 Azure 服務用戶端，您必須使用 hello`ServicesBuilder`類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="128a0-125">您可以：</span><span class="sxs-lookup"><span data-stu-id="128a0-125">You can:</span></span>

* <span data-ttu-id="128a0-126">傳送嗨連接字串直接 tooit。</span><span class="sxs-lookup"><span data-stu-id="128a0-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="128a0-127">使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：</span><span class="sxs-lookup"><span data-stu-id="128a0-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="128a0-128">預設已支援一種外部來源，即環境變數。</span><span class="sxs-lookup"><span data-stu-id="128a0-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="128a0-129">您可以新增新的來源延伸 hello`ConnectionStringSource`類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="128a0-130">如需此處所述的 hello 範例，hello 連接字串會直接傳遞。</span><span class="sxs-lookup"><span data-stu-id="128a0-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="128a0-131">建立主題</span><span class="sxs-lookup"><span data-stu-id="128a0-131">Create a topic</span></span>
<span data-ttu-id="128a0-132">您可以執行管理作業的服務匯流排主題透過 hello`ServiceBusRestProxy`類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="128a0-133">A`ServiceBusRestProxy`透過 hello 建構物件`ServicesBuilder::createServiceBusService`factory 方法搭配適當的連接字串會封裝 hello 語彙基元的權限 toomanage 它。</span><span class="sxs-lookup"><span data-stu-id="128a0-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="128a0-134">下列範例會示範如何 hello tooinstantiate`ServiceBusRestProxy`呼叫`ServiceBusRestProxy->createTopic`toocreate 的主題`mytopic`內`MySBNamespace`命名空間：</span><span class="sxs-lookup"><span data-stu-id="128a0-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="128a0-135">您可以使用 hello`listTopics`方法`ServiceBusRestProxy`物件 toocheck，如果在服務命名空間已經存在具有指定名稱的主題。</span><span class="sxs-lookup"><span data-stu-id="128a0-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="128a0-136">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="128a0-136">Create a subscription</span></span>
<span data-ttu-id="128a0-137">主題訂用帳戶也會建立以 hello`ServiceBusRestProxy->createSubscription`方法。</span><span class="sxs-lookup"><span data-stu-id="128a0-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="128a0-138">訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="128a0-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="128a0-139">建立訂用帳戶與 hello 預設 (MatchAll) 篩選器</span><span class="sxs-lookup"><span data-stu-id="128a0-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="128a0-140">hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="128a0-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="128a0-141">當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="128a0-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="128a0-142">hello 下列範例會建立名為 'mysubscription' 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。</span><span class="sxs-lookup"><span data-stu-id="128a0-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="128a0-143">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="128a0-143">Create subscriptions with filters</span></span>
<span data-ttu-id="128a0-144">您也可以設定可讓您 toospecify tooa 主題應該會出現特定主題的訂用帳戶內傳送的訊息篩選器。</span><span class="sxs-lookup"><span data-stu-id="128a0-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="128a0-145">hello 最有彈性的訂用帳戶支援的篩選器的類型為 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)，它會實作 SQL92 的子集。</span><span class="sxs-lookup"><span data-stu-id="128a0-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="128a0-146">SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="128a0-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="128a0-147">如需 SqlFilters 的詳細資訊，請參閱 [SqlFilter.SqlExpression 屬性][sqlfilter]。</span><span class="sxs-lookup"><span data-stu-id="128a0-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="128a0-148">每個訂用帳戶的規則處理內送訊息獨立地將其結果訊息 toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="128a0-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="128a0-149">此外，每個新的訂用帳戶具有預設**規則**可將所有訊息從 hello 主題 toohello 訂用帳戶都加入的篩選物件。</span><span class="sxs-lookup"><span data-stu-id="128a0-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="128a0-150">tooreceive 僅訊息符合您篩選條件，您必須移除 hello 預設規則。</span><span class="sxs-lookup"><span data-stu-id="128a0-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="128a0-151">您可以藉由使用 hello 移除 hello 預設規則`ServiceBusRestProxy->deleteRule`方法。</span><span class="sxs-lookup"><span data-stu-id="128a0-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="128a0-152">hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`MessageNumber`大於 3 的屬性。</span><span class="sxs-lookup"><span data-stu-id="128a0-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="128a0-153">請參閱[傳送訊息 tooa 主題](#send-messages-to-a-topic)新增自訂屬性 toomessages 相關資訊。</span><span class="sxs-lookup"><span data-stu-id="128a0-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="128a0-154">請注意，此程式碼需要 hello 使用其他的命名空間： `WindowsAzure\ServiceBus\Models\SubscriptionInfo`。</span><span class="sxs-lookup"><span data-stu-id="128a0-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="128a0-155">同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與`SqlFilter`只選取有訊息`MessageNumber`屬性小於或等於 too3。</span><span class="sxs-lookup"><span data-stu-id="128a0-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="128a0-156">現在，當訊息傳送 toohello`mytopic`主題，它永遠傳遞訂閱 tooreceivers toohello`mysubscription`訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`訂用帳戶 (視 hello 訊息內容）。</span><span class="sxs-lookup"><span data-stu-id="128a0-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="128a0-157">傳送訊息 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="128a0-157">Send messages tooa topic</span></span>
<span data-ttu-id="128a0-158">toosend 訊息 tooa Service Bus 主題，您的應用程式呼叫 hello`ServiceBusRestProxy->sendTopicMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="128a0-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="128a0-159">hello 下列程式碼會示範如何 toosend 訊息 toohello`mytopic`先前中建立的主題`MySBNamespace`服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="128a0-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="128a0-160">TooService 匯流排主題是 hello 的執行個體傳送訊息[BrokeredMessage] [ BrokeredMessage]類別。</span><span class="sxs-lookup"><span data-stu-id="128a0-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="128a0-161">[BrokeredMessage] [ BrokeredMessage]物件具有一組標準的屬性和方法，以及可以使用的 toohold 自訂應用程式特定屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="128a0-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="128a0-162">hello 下列範例示範如何 toosend 5 測試訊息 toohello`mytopic`先前建立的主題。</span><span class="sxs-lookup"><span data-stu-id="128a0-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="128a0-163">hello`setProperty`方法是使用的 tooadd 自訂屬性 (`MessageNumber`) tooeach 訊息。</span><span class="sxs-lookup"><span data-stu-id="128a0-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="128a0-164">請注意該 hello`MessageNumber`屬性值會變動，每個訊息 (hello 中所示，您可以使用哪些訂閱接收，此值 toodetermine[建立訂用帳戶](#create-a-subscription)> 一節):</span><span class="sxs-lookup"><span data-stu-id="128a0-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="128a0-165">服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="128a0-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="128a0-166">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="128a0-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="128a0-167">訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="128a0-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="128a0-168">主題大小的這項上限為 5 GB。</span><span class="sxs-lookup"><span data-stu-id="128a0-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="128a0-169">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="128a0-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="128a0-170">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="128a0-170">Receive messages from a subscription</span></span>
<span data-ttu-id="128a0-171">hello 最佳 tooreceive 訊息方式來自訂用帳戶是 toouse`ServiceBusRestProxy->receiveSubscriptionMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="128a0-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="128a0-172">訊息可以兩種不同的模式接收：[*ReceiveAndDelete* 和 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)。</span><span class="sxs-lookup"><span data-stu-id="128a0-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="128a0-173">**PeekLock** hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="128a0-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="128a0-174">當使用 hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中，接收是單發式作業; 也就是當服務匯流排訂用帳戶中收到訊息的讀取的要求時，它會標示為正在使用的 hello 訊息，就傳回該 toohello應用程式。</span><span class="sxs-lookup"><span data-stu-id="128a0-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="128a0-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="128a0-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="128a0-176">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="128a0-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="128a0-177">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="128a0-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="128a0-178">在預設的 hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中，接收訊息會變成兩階段作業，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="128a0-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="128a0-179">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="128a0-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="128a0-180">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段接收處理序藉由傳遞收到 hello 訊息太`ServiceBusRestProxy->deleteMessage`。</span><span class="sxs-lookup"><span data-stu-id="128a0-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="128a0-181">當服務匯流排會看見 hello`deleteMessage`呼叫，它會將標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="128a0-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="128a0-182">下列範例會示範如何 hello tooreceive 和處理訊息，使用[PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式 （hello 預設模式）。</span><span class="sxs-lookup"><span data-stu-id="128a0-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="128a0-183">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="128a0-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="128a0-184">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="128a0-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="128a0-185">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`收到 hello 訊息上的方法 (而不是 hello`deleteMessage`方法)。</span><span class="sxs-lookup"><span data-stu-id="128a0-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="128a0-186">這將導致 hello 佇列內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="128a0-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="128a0-187">另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則 Service Bus hello 訊息將會解除鎖定自動，並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="128a0-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="128a0-188">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="128a0-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="128a0-189">這通常稱為*至少一旦*處理; 亦即，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="128a0-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="128a0-190">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tooapplications toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="128a0-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="128a0-191">這通常用來達成 hello `getMessageId` hello 訊息，嘗試傳遞都維持不變的方法。</span><span class="sxs-lookup"><span data-stu-id="128a0-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="128a0-192">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="128a0-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="128a0-193">主題或訂用帳戶，使用 hello toodelete`ServiceBusRestProxy->deleteTopic`或 hello`ServiceBusRestProxy->deleteSubscripton`方法，分別。</span><span class="sxs-lookup"><span data-stu-id="128a0-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="128a0-194">請注意，刪除主題也會刪除任何訂用帳戶註冊的 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="128a0-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="128a0-195">hello 下列範例示範如何 toodelete 主題命名`mytopic`和其已註冊的訂閱。</span><span class="sxs-lookup"><span data-stu-id="128a0-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="128a0-196">使用 hello`deleteSubscription`方法，您可以個別刪除訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="128a0-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="128a0-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="128a0-197">Next steps</span></span>
<span data-ttu-id="128a0-198">現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[佇列、 主題和訂用帳戶][ Queues, topics, and subscriptions]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="128a0-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
