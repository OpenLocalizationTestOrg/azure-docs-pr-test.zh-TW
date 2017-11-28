---
title: "aaaHow toouse 服務匯流排佇列與 PHP |Microsoft 文件"
description: "了解如何 toouse Service Bus 佇列在 Azure 中。 程式碼範例以 PHP 撰寫。"
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="81d12-104">服務匯流排 toouse 排入佇列與 PHP</span><span class="sxs-lookup"><span data-stu-id="81d12-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="81d12-105">本指南也說明如何 toouse 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="81d12-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="81d12-106">hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP](../php-download-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="81d12-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="81d12-107">hello 涵蓋案例包括**建立佇列**，**傳送和接收訊息**，和**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="81d12-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="81d12-108">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="81d12-108">Create a PHP application</span></span>
<span data-ttu-id="81d12-109">只有建立 PHP 應用程式存取 hello Azure Blob 服務的需求為 hello hello 參考中的 hello 類別[Azure SDK for PHP](../php-download-sdk.md)從程式碼內。</span><span class="sxs-lookup"><span data-stu-id="81d12-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="81d12-110">您可以使用任何開發工具 toocreate，您的應用程式或 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="81d12-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="81d12-111">您的 PHP 安裝也必須擁有 hello [OpenSSL 延伸](http://php.net/openssl)安裝並啟用。</span><span class="sxs-lookup"><span data-stu-id="81d12-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="81d12-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的服務功能，或可從 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的資料表服務功能。</span><span class="sxs-lookup"><span data-stu-id="81d12-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="81d12-113">取得 hello Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="81d12-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="81d12-114">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="81d12-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="81d12-115">toouse hello Service Bus 佇列應用程式開發介面，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="81d12-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="81d12-116">參考 hello 自動換片器檔案使用 hello [require_once] [ require_once]陳述式。</span><span class="sxs-lookup"><span data-stu-id="81d12-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="81d12-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="81d12-117">Reference any classes you might use.</span></span>

<span data-ttu-id="81d12-118">hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello`ServicesBuilder`類別。</span><span class="sxs-lookup"><span data-stu-id="81d12-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="81d12-119">此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="81d12-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="81d12-120">如果您是手動或以西洋梨封裝安裝 hello 程式庫，您必須參考 hello **WindowsAzure.php**自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="81d12-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="81d12-121">在以下範例 hello，hello`require_once`永遠不會顯示陳述式，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。</span><span class="sxs-lookup"><span data-stu-id="81d12-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="81d12-122">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="81d12-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="81d12-123">tooinstantiate 服務匯流排用戶端，您必須先具備有效的連接字串格式如下：</span><span class="sxs-lookup"><span data-stu-id="81d12-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="81d12-124">其中`Endpoint`的 hello 格式通常是`[yourNamespace].servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="81d12-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="81d12-125">toocreate 任何 Azure 服務用戶端，您必須使用 hello`ServicesBuilder`類別。</span><span class="sxs-lookup"><span data-stu-id="81d12-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="81d12-126">您可以：</span><span class="sxs-lookup"><span data-stu-id="81d12-126">You can:</span></span>

* <span data-ttu-id="81d12-127">傳送嗨連接字串直接 tooit。</span><span class="sxs-lookup"><span data-stu-id="81d12-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="81d12-128">使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：</span><span class="sxs-lookup"><span data-stu-id="81d12-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="81d12-129">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="81d12-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="81d12-130">您可以新增新的來源延伸 hello`ConnectionStringSource`類別</span><span class="sxs-lookup"><span data-stu-id="81d12-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="81d12-131">如需此處所述的 hello 範例，hello 連接字串會直接傳遞。</span><span class="sxs-lookup"><span data-stu-id="81d12-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="81d12-132">建立佇列</span><span class="sxs-lookup"><span data-stu-id="81d12-132">Create a queue</span></span>
<span data-ttu-id="81d12-133">您可以執行 hello 透過服務匯流排佇列的管理作業`ServiceBusRestProxy`類別。</span><span class="sxs-lookup"><span data-stu-id="81d12-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="81d12-134">A`ServiceBusRestProxy`透過 hello 建構物件`ServicesBuilder::createServiceBusService`factory 方法搭配適當的連接字串會封裝 hello 語彙基元的權限 toomanage 它。</span><span class="sxs-lookup"><span data-stu-id="81d12-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="81d12-135">下列範例會示範如何 hello tooinstantiate`ServiceBusRestProxy`呼叫`ServiceBusRestProxy->createQueue`toocreate 名為的佇列`myqueue`內`MySBNamespace`服務命名空間：</span><span class="sxs-lookup"><span data-stu-id="81d12-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="81d12-136">您可以使用 hello`listQueues`方法`ServiceBusRestProxy`物件 toocheck，如果在命名空間已經存在具有指定名稱的佇列。</span><span class="sxs-lookup"><span data-stu-id="81d12-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="81d12-137">傳送訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="81d12-137">Send messages tooa queue</span></span>
<span data-ttu-id="81d12-138">toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`ServiceBusRestProxy->sendQueueMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="81d12-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="81d12-139">hello 下列程式碼會示範如何 toosend 訊息 toohello`myqueue`先前中建立的佇列`MySBNamespace`服務命名空間。</span><span class="sxs-lookup"><span data-stu-id="81d12-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="81d12-140">訊息已傳送太 （和從接收的資料） 的服務匯流排佇列是 hello 的執行個體[BrokeredMessage] [ BrokeredMessage]類別。</span><span class="sxs-lookup"><span data-stu-id="81d12-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="81d12-141">[BrokeredMessage] [ BrokeredMessage]物件具有一組標準的方法和屬性都使用的 toohold 自訂應用程式特定的屬性和任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="81d12-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="81d12-142">服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="81d12-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="81d12-143">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="81d12-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="81d12-144">訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="81d12-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="81d12-145">佇列大小的這項上限為 5 GB。</span><span class="sxs-lookup"><span data-stu-id="81d12-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="81d12-146">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="81d12-146">Receive messages from a queue</span></span>

<span data-ttu-id="81d12-147">hello 最佳方式 tooreceive 來自佇列的訊息是 toouse`ServiceBusRestProxy->receiveQueueMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="81d12-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="81d12-148">訊息可以兩種不同的模式接收：[*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 和 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)。</span><span class="sxs-lookup"><span data-stu-id="81d12-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="81d12-149">**PeekLock** hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="81d12-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="81d12-150">當使用[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete)模式中，接收是單發式作業; 也就是當服務匯流排佇列中接收訊息的讀取的要求，它會標示為正在使用的 hello 訊息，就傳回該 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d12-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="81d12-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete)模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="81d12-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="81d12-152">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="81d12-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="81d12-153">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="81d12-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="81d12-154">在預設的 hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)模式中，接收訊息會變成兩階段作業，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d12-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="81d12-155">當服務匯流排收到要求時，會尋找 hello 耗用下一個訊息 toobe、 tooprevent 將它鎖定，接收其他取用者，然後傳回 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d12-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="81d12-156">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段接收處理序藉由傳遞收到 hello 訊息太`ServiceBusRestProxy->deleteMessage`。</span><span class="sxs-lookup"><span data-stu-id="81d12-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="81d12-157">當服務匯流排會看見 hello`deleteMessage`呼叫，它會將標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="81d12-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="81d12-158">下列範例會示範如何 hello tooreceive 和處理訊息，使用[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)模式 （hello 預設模式）。</span><span class="sxs-lookup"><span data-stu-id="81d12-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="81d12-159">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="81d12-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="81d12-160">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="81d12-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="81d12-161">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`收到 hello 訊息上的方法 (而不是 hello`deleteMessage`方法)。</span><span class="sxs-lookup"><span data-stu-id="81d12-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="81d12-162">這將導致 hello 佇列內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="81d12-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="81d12-163">另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則 Service Bus hello 訊息將會解除鎖定自動，並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="81d12-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="81d12-164">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="81d12-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="81d12-165">這通常稱為*至少一旦*處理; 亦即，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="81d12-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="81d12-166">如果 hello 案例無法容許重複處理，則建議您增加額外的邏輯 tooapplications toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="81d12-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="81d12-167">這通常用來達成 hello `getMessageId` hello 訊息，嘗試傳遞都維持不變的方法。</span><span class="sxs-lookup"><span data-stu-id="81d12-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d12-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81d12-168">Next steps</span></span>
<span data-ttu-id="81d12-169">現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[佇列、 主題和訂用帳戶][ Queues, topics, and subscriptions]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="81d12-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="81d12-170">如需詳細資訊，也請瀏覽 hello [PHP 開發人員中心](https://azure.microsoft.com/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="81d12-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


