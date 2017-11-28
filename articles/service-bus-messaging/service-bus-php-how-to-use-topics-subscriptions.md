---
title: "如何將服務匯流排主題搭配 PHP 使用 | Microsoft Docs"
description: "了解如何在 Azure 中搭配使用服務匯流排主題與 PHP。"
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
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="7ec82-103">如何透過 PHP 使用服務匯流排主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ec82-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7ec82-104">本文示範如何使用服務匯流排主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="7ec82-105">這些範例均是以 PHP 撰寫，並使用 [Azure SDK for PHP](../php-download-sdk.md) (英文)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="7ec82-106">涵蓋的案例包括**建立主題和訂用帳戶**、**建立訂用帳戶篩選器**、**傳送訊息至主題**、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7ec82-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="7ec82-107">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ec82-107">Create a PHP application</span></span>
<span data-ttu-id="7ec82-108">若要建立 PHP 應用程式並使其存取 Azure Blob 服務，唯一要求就是在您的程式碼中參考 [Azure SDK for PHP](../php-download-sdk.md) 中的類別。</span><span class="sxs-lookup"><span data-stu-id="7ec82-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="7ec82-109">您可以使用任何開發工具來建立應用程式，或記事本。</span><span class="sxs-lookup"><span data-stu-id="7ec82-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec82-110">您的 PHP 安裝也必須已安裝並啟用 [OpenSSL 延伸模組](http://php.net/openssl)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="7ec82-111">本文說明如何使用可從 PHP 應用程式內本機呼叫的服務功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的服務功能。</span><span class="sxs-lookup"><span data-stu-id="7ec82-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="7ec82-112">取得 Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="7ec82-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="7ec82-113">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="7ec82-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="7ec82-114">若要使用服務匯流排 API：</span><span class="sxs-lookup"><span data-stu-id="7ec82-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="7ec82-115">使用 [require_once][require-once] 陳述式來參考自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="7ec82-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="7ec82-116">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="7ec82-116">Reference any classes you might use.</span></span>

<span data-ttu-id="7ec82-117">下列範例說明如何納入自動換片器檔案及參考 **ServiceBusService** 類別。</span><span class="sxs-lookup"><span data-stu-id="7ec82-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec82-118">此範例 (和本文中的其他範例) 假設您已透過編輯器安裝 PHP Client Libraries for Azure。</span><span class="sxs-lookup"><span data-stu-id="7ec82-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="7ec82-119">如果您以手動方式或以 PEAR 套件方式安裝程式庫，則必須參考 **WindowsAzure.php** 自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="7ec82-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="7ec82-120">在下列各範例中，一律會顯示 `require_once` 陳述式，但只會參考要執行之範例所需的類別。</span><span class="sxs-lookup"><span data-stu-id="7ec82-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="7ec82-121">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="7ec82-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="7ec82-122">若要具現化服務匯流排用戶端，您必須具備符合下列格式的有效連接字串：</span><span class="sxs-lookup"><span data-stu-id="7ec82-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="7ec82-123">其中，`Endpoint` 的格式通常是 `https://[yourNamespace].servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="7ec82-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="7ec82-124">若要建立任何 Azure 服務用戶端，您必須使用 `ServicesBuilder` 類別。</span><span class="sxs-lookup"><span data-stu-id="7ec82-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="7ec82-125">您可以：</span><span class="sxs-lookup"><span data-stu-id="7ec82-125">You can:</span></span>

* <span data-ttu-id="7ec82-126">直接將連接字串傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="7ec82-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="7ec82-127">使用 **CloudConfigurationManager (CCM)** 到多種外部來源檢查連接字串：</span><span class="sxs-lookup"><span data-stu-id="7ec82-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="7ec82-128">預設已支援一種外部來源，即環境變數。</span><span class="sxs-lookup"><span data-stu-id="7ec82-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="7ec82-129">您可以擴充 `ConnectionStringSource` 類別以加入新來源。</span><span class="sxs-lookup"><span data-stu-id="7ec82-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="7ec82-130">在本文的各範例中，將會直接傳遞連接字串。</span><span class="sxs-lookup"><span data-stu-id="7ec82-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="7ec82-131">建立主題</span><span class="sxs-lookup"><span data-stu-id="7ec82-131">Create a topic</span></span>
<span data-ttu-id="7ec82-132">您可以透過 `ServiceBusRestProxy` 類別來執行服務匯流排主題的管理作業。</span><span class="sxs-lookup"><span data-stu-id="7ec82-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="7ec82-133">`ServiceBusRestProxy` 物件可透過 `ServicesBuilder::createServiceBusService` Factory 方法，使用含有權杖權限加以管理的適當連接字串來建構。</span><span class="sxs-lookup"><span data-stu-id="7ec82-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="7ec82-134">下列範例將說明如何具現化 `ServiceBusRestProxy` 並呼叫 `ServiceBusRestProxy->createTopic`，以便在 `MySBNamespace` 命名空間內建立名為 `mytopic` 的主題：</span><span class="sxs-lookup"><span data-stu-id="7ec82-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="7ec82-135">您可以在 `ServiceBusRestProxy` 物件上使用 `listTopics` 方法，檢查服務命名空間內是否已有指定名稱的主題存在。</span><span class="sxs-lookup"><span data-stu-id="7ec82-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="7ec82-136">建立訂閱</span><span class="sxs-lookup"><span data-stu-id="7ec82-136">Create a subscription</span></span>
<span data-ttu-id="7ec82-137">`ServiceBusRestProxy->createSubscription` 方法也能用來建立主題訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="7ec82-138">為訂閱命名，且能包含選擇性篩選器，以用來限制傳遞至訂閱的虛擬佇列的訊息集合。</span><span class="sxs-lookup"><span data-stu-id="7ec82-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="7ec82-139">使用預設 (MatchAll) 篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ec82-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="7ec82-140">如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。</span><span class="sxs-lookup"><span data-stu-id="7ec82-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7ec82-141">使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。</span><span class="sxs-lookup"><span data-stu-id="7ec82-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="7ec82-142">下列範例將建立名為 'mysubscription' 的訂用帳戶，並使用預設的 **MatchAll** 篩選器。</span><span class="sxs-lookup"><span data-stu-id="7ec82-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7ec82-143">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ec82-143">Create subscriptions with filters</span></span>
<span data-ttu-id="7ec82-144">您也可以設定篩選器，讓您指定傳送至主題的哪些訊息應出現在特定主題訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7ec82-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="7ec82-145">訂用帳戶所支援的最具彈性篩選器類型是實作 SQL92 子集的 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="7ec82-146">SQL 篩選器會對發佈至主題之訊息的屬性運作。</span><span class="sxs-lookup"><span data-stu-id="7ec82-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="7ec82-147">如需 SqlFilters 的詳細資訊，請參閱 [SqlFilter.SqlExpression 屬性][sqlfilter]。</span><span class="sxs-lookup"><span data-stu-id="7ec82-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="7ec82-148">訂用帳戶的每個規則可獨立處理傳入的訊息，並將其結果訊息新增至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="7ec82-149">此外，每個新訂用帳戶都有具篩選器的預設 **Rule** 物件，而篩選器會將主題中的所有訊息新增至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="7ec82-150">To receive only messages matching your filter, you must remove the default rule.</span><span class="sxs-lookup"><span data-stu-id="7ec82-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="7ec82-151">您可以使用 `ServiceBusRestProxy->deleteRule` 方法以移除預設規則。</span><span class="sxs-lookup"><span data-stu-id="7ec82-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="7ec82-152">以下範例將建立名為 `HighMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取自訂 `MessageNumber` 屬性大於 3 的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="7ec82-153">請參閱[傳送訊息至主題](#send-messages-to-a-topic)，以取得將自訂屬性新增至訊息的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec82-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="7ec82-154">請注意，此程式碼必須使用額外的命名空間：`WindowsAzure\ServiceBus\Models\SubscriptionInfo`。</span><span class="sxs-lookup"><span data-stu-id="7ec82-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="7ec82-155">同樣地，下列範例將建立名為 `LowMessages` 的訂用帳戶，而且所含的 `SqlFilter` 只會選取 `MessageNumber` 屬性小於或等於 3 的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="7ec82-156">現在，當訊息傳送至 `mytopic` 主題時，一律會將該訊息傳遞至已訂閱 `mysubscription` 訂用帳戶的接收者，並選擇性地傳遞至已訂閱 `HighMessages` 和 `LowMessages` 訂用帳戶的接收者 (視訊息內容而定)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="7ec82-157">傳送訊息至主題</span><span class="sxs-lookup"><span data-stu-id="7ec82-157">Send messages to a topic</span></span>
<span data-ttu-id="7ec82-158">若要將訊息傳送至服務匯流排主題，應用程式會呼叫 `ServiceBusRestProxy->sendTopicMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="7ec82-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="7ec82-159">下列程式碼示範如何將訊息傳送至先前在 `MySBNamespace` 服務命名空間中建立的 `mytopic` 主題。</span><span class="sxs-lookup"><span data-stu-id="7ec82-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="7ec82-160">傳送至服務匯流排主題的訊息是 [BrokeredMessage][BrokeredMessage] 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ec82-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="7ec82-161">[BrokeredMessage][BrokeredMessage] 物件具有一組標準屬性和方法，以及可用來保存自訂應用程式特定屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="7ec82-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="7ec82-162">下列範例示範如何將 5 則測試訊息傳送至先前建立的 `mytopic` 主題。</span><span class="sxs-lookup"><span data-stu-id="7ec82-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="7ec82-163">`setProperty` 方法會用來將自訂屬性 (`MessageNumber`) 新增至每個訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="7ec82-164">請注意，每個訊息的 `MessageNumber` 屬性值有不同之處 (您可以使用此值來判斷哪些訂用帳戶會接收訊息，如[建立訂用帳戶](#create-a-subscription)一節所述)：</span><span class="sxs-lookup"><span data-stu-id="7ec82-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="7ec82-165">服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="7ec82-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7ec82-166">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="7ec82-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7ec82-167">主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="7ec82-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="7ec82-168">主題大小的這項上限為 5 GB。</span><span class="sxs-lookup"><span data-stu-id="7ec82-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="7ec82-169">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="7ec82-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="7ec82-170">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="7ec82-170">Receive messages from a subscription</span></span>
<span data-ttu-id="7ec82-171">從訂用帳戶接收訊息的最佳方式是使用 `ServiceBusRestProxy->receiveSubscriptionMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="7ec82-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="7ec82-172">訊息可以兩種不同的模式接收：[*ReceiveAndDelete* 和 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="7ec82-173">**PeekLock** 是預設值。</span><span class="sxs-lookup"><span data-stu-id="7ec82-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="7ec82-174">使用 [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式時，接收是一次性作業；也就是說，當服務匯流排在訂用帳戶中收到訊息的讀取要求時，它會將此訊息標示為已使用，並將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec82-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="7ec82-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 模式是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="7ec82-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="7ec82-176">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="7ec82-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="7ec82-177">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="7ec82-178">在預設的 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式中，接收訊息會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec82-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7ec82-179">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec82-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="7ec82-180">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它會將已接收的訊息傳遞至 `ServiceBusRestProxy->deleteMessage`，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="7ec82-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="7ec82-181">當服務匯流排看到 `deleteMessage` 呼叫時，它會將訊息標示為已取用，並將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="7ec82-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="7ec82-182">下列範例說明如何使用 [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) 模式 (預設模式) 來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7ec82-183">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="7ec82-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="7ec82-184">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="7ec82-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7ec82-185">如果接收者應用程式因為某些原因無法處理訊息，它可以在接收訊息上呼叫 `unlockMessage` 方法 (而不是 `deleteMessage` 方法)。</span><span class="sxs-lookup"><span data-stu-id="7ec82-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="7ec82-186">這將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="7ec82-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7ec82-187">與在佇列內鎖定之訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="7ec82-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="7ec82-188">如果應用程式在處理訊息之後，但尚未發出 `deleteMessage` 要求時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ec82-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="7ec82-189">這通常稱為「至少處理一次」，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="7ec82-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="7ec82-190">如果案例無法容許重複處理，則應用程式開發人員應在應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="7ec82-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="7ec82-191">通常您可使用訊息的 `getMessageId` 方法來達到此目的，該方法在各個傳遞嘗試中保持不變。</span><span class="sxs-lookup"><span data-stu-id="7ec82-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7ec82-192">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7ec82-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="7ec82-193">若要刪除主題或訂用帳戶，請分別使用 `ServiceBusRestProxy->deleteTopic` 或 `ServiceBusRestProxy->deleteSubscripton` 方法。</span><span class="sxs-lookup"><span data-stu-id="7ec82-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="7ec82-194">請注意，刪除主題也將會刪除已註冊該主題的任何訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="7ec82-195">下列範例示範如何刪除名為 `mytopic` 的主題及其註冊的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ec82-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="7ec82-196">使用 `deleteSubscription` 方法可讓您個別刪除某個訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="7ec82-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="7ec82-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ec82-197">Next steps</span></span>
<span data-ttu-id="7ec82-198">現在您已了解服務匯流排佇列的基本概念，請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec82-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
