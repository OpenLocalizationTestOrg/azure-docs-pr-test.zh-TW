---
title: "如何將服務匯流排佇列搭配 PHP 使用 | Microsoft Docs"
description: "了解如何使用 Azure 中的服務匯流排佇列。 程式碼範例以 PHP 撰寫。"
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="9b49f-104">如何將服務匯流排佇列搭配 PHP 使用</span><span class="sxs-lookup"><span data-stu-id="9b49f-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="9b49f-105">本指南將說明如何使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="9b49f-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="9b49f-106">這些範例均是以 PHP 撰寫，並使用 [Azure SDK for PHP](../php-download-sdk.md) (英文)。</span><span class="sxs-lookup"><span data-stu-id="9b49f-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="9b49f-107">本文說明的案例包括**建立佇列**、**傳送並接收訊息**，以及**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="9b49f-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="9b49f-108">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="9b49f-108">Create a PHP application</span></span>
<span data-ttu-id="9b49f-109">若要建立 PHP 應用程式並使其存取 Azure Blob 服務，唯一要求就是在您的程式碼中參考 [Azure SDK for PHP](../php-download-sdk.md) 中的類別。</span><span class="sxs-lookup"><span data-stu-id="9b49f-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="9b49f-110">您可以使用任何開發工具來建立應用程式，或記事本。</span><span class="sxs-lookup"><span data-stu-id="9b49f-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="9b49f-111">您的 PHP 安裝也必須已安裝並啟用 [OpenSSL 延伸模組](http://php.net/openssl)。</span><span class="sxs-lookup"><span data-stu-id="9b49f-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="9b49f-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的服務功能，或可從 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的資料表服務功能。</span><span class="sxs-lookup"><span data-stu-id="9b49f-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="9b49f-113">取得 Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="9b49f-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="9b49f-114">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="9b49f-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="9b49f-115">若要使用服務匯流排佇列 API，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9b49f-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="9b49f-116">使用 [require_once][require_once] 陳述式來參考自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="9b49f-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="9b49f-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="9b49f-117">Reference any classes you might use.</span></span>

<span data-ttu-id="9b49f-118">下列範例顯示如何納入自動換片器檔案及參考 `ServicesBuilder` 類別。</span><span class="sxs-lookup"><span data-stu-id="9b49f-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="9b49f-119">此範例 (和本文中的其他範例) 假設您已透過編輯器安裝 PHP Client Libraries for Azure。</span><span class="sxs-lookup"><span data-stu-id="9b49f-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="9b49f-120">如果您以手動方式或以 PEAR 套件方式安裝程式庫，則必須參考 **WindowsAzure.php** 自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="9b49f-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="9b49f-121">在下列各範例中，一律會顯示 `require_once` 陳述式，但只會參考要執行之範例所需的類別。</span><span class="sxs-lookup"><span data-stu-id="9b49f-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="9b49f-122">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="9b49f-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="9b49f-123">若要具現化服務匯流排用戶端，您必須具備符合下列格式的有效連接字串：</span><span class="sxs-lookup"><span data-stu-id="9b49f-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="9b49f-124">其中，`Endpoint` 的格式通常是 `[yourNamespace].servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="9b49f-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="9b49f-125">若要建立任何 Azure 服務用戶端，您必須使用 `ServicesBuilder` 類別。</span><span class="sxs-lookup"><span data-stu-id="9b49f-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="9b49f-126">您可以：</span><span class="sxs-lookup"><span data-stu-id="9b49f-126">You can:</span></span>

* <span data-ttu-id="9b49f-127">直接將連接字串傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="9b49f-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="9b49f-128">使用 **CloudConfigurationManager (CCM)** 到多種外部來源檢查連接字串：</span><span class="sxs-lookup"><span data-stu-id="9b49f-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="9b49f-129">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="9b49f-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="9b49f-130">您可以擴充 `ConnectionStringSource` 類別以加入新來源</span><span class="sxs-lookup"><span data-stu-id="9b49f-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="9b49f-131">在本文的各範例中，將會直接傳遞連接字串。</span><span class="sxs-lookup"><span data-stu-id="9b49f-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="9b49f-132">建立佇列</span><span class="sxs-lookup"><span data-stu-id="9b49f-132">Create a queue</span></span>
<span data-ttu-id="9b49f-133">您可以使用 `ServiceBusRestProxy` 類別來執行服務匯流排佇列的管理作業。</span><span class="sxs-lookup"><span data-stu-id="9b49f-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="9b49f-134">`ServiceBusRestProxy` 物件可透過 `ServicesBuilder::createServiceBusService` Factory 方法，使用含有權杖權限加以管理的適當連接字串來建構。</span><span class="sxs-lookup"><span data-stu-id="9b49f-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="9b49f-135">下列範例將說明如何具現化 `ServiceBusRestProxy` 並呼叫 `ServiceBusRestProxy->createQueue`，以便在 `MySBNamespace` 服務命名空間內建立名為 `myqueue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="9b49f-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
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
> <span data-ttu-id="9b49f-136">您可以在 `ServiceBusRestProxy` 物件上使用 `listQueues` 方法，來檢查命名空間內是否已有指定名稱的佇列存在。</span><span class="sxs-lookup"><span data-stu-id="9b49f-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="9b49f-137">傳送訊息至佇列</span><span class="sxs-lookup"><span data-stu-id="9b49f-137">Send messages to a queue</span></span>
<span data-ttu-id="9b49f-138">若要將訊息傳送至服務匯流排佇列，應用程式會呼叫 `ServiceBusRestProxy->sendQueueMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="9b49f-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="9b49f-139">下列程式碼示範如何將訊息傳送至先前在 `MySBNamespace` 服務命名空間中建立的 `myqueue` 佇列。</span><span class="sxs-lookup"><span data-stu-id="9b49f-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
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

<span data-ttu-id="9b49f-140">傳送至 (和接收自) 服務匯流排佇列的訊息是 [BrokeredMessage][BrokeredMessage] 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9b49f-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="9b49f-141">[BrokeredMessage][BrokeredMessage] 物件具有一組標準方法和屬性，可用來保存自訂的應用程式特定屬性，以及任意的應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="9b49f-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="9b49f-142">服務匯流排佇列支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="9b49f-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="9b49f-143">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="9b49f-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="9b49f-144">佇列中所保存的訊息數目沒有限制，但佇列所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="9b49f-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="9b49f-145">佇列大小的這項上限為 5 GB。</span><span class="sxs-lookup"><span data-stu-id="9b49f-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="9b49f-146">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="9b49f-146">Receive messages from a queue</span></span>

<span data-ttu-id="9b49f-147">從佇列接收訊息的最佳方式是使用 `ServiceBusRestProxy->receiveQueueMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="9b49f-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="9b49f-148">訊息可以兩種不同的模式接收：[*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 和 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)。</span><span class="sxs-lookup"><span data-stu-id="9b49f-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="9b49f-149">**PeekLock** 是預設值。</span><span class="sxs-lookup"><span data-stu-id="9b49f-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="9b49f-150">使用 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 模式時，接收是單發作業；也就是說，當服務匯流排收到佇列中訊息的讀取要求時，它會將此訊息標示為已使用，並將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b49f-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="9b49f-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 模式是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="9b49f-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="9b49f-152">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="9b49f-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="9b49f-153">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="9b49f-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="9b49f-154">在預設的 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 模式中，接收訊息會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b49f-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="9b49f-155">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b49f-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="9b49f-156">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它會將已接收的訊息傳遞至 `ServiceBusRestProxy->deleteMessage`，以完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="9b49f-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="9b49f-157">當服務匯流排看到 `deleteMessage` 呼叫時，它會將訊息標示為已取用，並將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="9b49f-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="9b49f-158">下列範例說明如何使用 [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) 模式 (預設模式) 來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="9b49f-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="9b49f-159">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="9b49f-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="9b49f-160">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="9b49f-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="9b49f-161">如果接收者應用程式因為某些原因無法處理訊息，它可以在接收訊息上呼叫 `unlockMessage` 方法 (而不是 `deleteMessage` 方法)。</span><span class="sxs-lookup"><span data-stu-id="9b49f-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="9b49f-162">這將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="9b49f-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="9b49f-163">與在佇列內鎖定之訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="9b49f-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="9b49f-164">如果應用程式在處理訊息之後，但尚未發出 `deleteMessage` 要求時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b49f-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="9b49f-165">這通常稱為「至少處理一次」，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="9b49f-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="9b49f-166">如果案例無法容許重複處理，建議您在應用程式中新增其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="9b49f-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="9b49f-167">通常您可使用訊息的 `getMessageId` 方法來達到此目的，該方法在各個傳遞嘗試中保持不變。</span><span class="sxs-lookup"><span data-stu-id="9b49f-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b49f-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b49f-168">Next steps</span></span>
<span data-ttu-id="9b49f-169">現在您已了解服務匯流排佇列的基本概念，請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9b49f-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="9b49f-170">如需詳細資訊，另請造訪 [PHP 開發人員中心](https://azure.microsoft.com/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="9b49f-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


