---
title: "如何使用 PHP 的佇列儲存體 | Microsoft Docs"
description: "了解如何使用 Azure 佇列儲存體服務來建立和刪除佇列，以及插入、取得和刪除訊息。 範例是以 PHP 撰寫的。"
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3c8f799a917cfc9d74412d90f27f2ea8c21265d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="e4efe-104">如何使用 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e4efe-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="e4efe-105">Overview</span><span class="sxs-lookup"><span data-stu-id="e4efe-105">Overview</span></span>
<span data-ttu-id="e4efe-106">本指南將示範如何使用 Azure 佇列儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="e4efe-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="e4efe-107">這些範例均是以 Windows SDK for PHP 中的類別撰寫。</span><span class="sxs-lookup"><span data-stu-id="e4efe-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="e4efe-108">所涵蓋的案例包括插入、查看、取得和刪除佇列訊息，以及建立和刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="e4efe-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e4efe-109">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4efe-109">Create a PHP application</span></span>
<span data-ttu-id="e4efe-110">若要建立 PHP 應用程式並使其存取 Azure 佇列儲存體，唯一要求就是在您的程式碼中參考 Azure SDK for PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="e4efe-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="e4efe-111">您可以使用任何開發工具來建立應用程式 (包括 [記事本])。</span><span class="sxs-lookup"><span data-stu-id="e4efe-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="e4efe-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的佇列儲存體功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的佇列儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="e4efe-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="e4efe-113">取得 Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e4efe-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="e4efe-114">設定您的應用程式以存取佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e4efe-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="e4efe-115">若要使用 Azure 佇列儲存體的 API，您需要：</span><span class="sxs-lookup"><span data-stu-id="e4efe-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="e4efe-116">使用 [require_once] 陳述式來參考自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="e4efe-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="e4efe-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="e4efe-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="e4efe-118">下列範例顯示如何納入自動載入器檔案及參考 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="e4efe-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="e4efe-119">此範例 (和本文中的其他範例) 假設您已透過編輯器安裝 PHP Client Libraries for Azure。</span><span class="sxs-lookup"><span data-stu-id="e4efe-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e4efe-120">如果您是以手動方式安裝程式庫，則必須參考 `WindowsAzure.php` 自動載入器檔案。</span><span class="sxs-lookup"><span data-stu-id="e4efe-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="e4efe-121">在下列各範例中，一律會顯示 `require_once` 陳述式，但只會參考要執行之範例所需的類別。</span><span class="sxs-lookup"><span data-stu-id="e4efe-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e4efe-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="e4efe-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="e4efe-123">若要具現化 Azure 佇列儲存體用戶端，您必須先具備有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="e4efe-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="e4efe-124">佇列服務的連接字串格式如下。</span><span class="sxs-lookup"><span data-stu-id="e4efe-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="e4efe-125">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="e4efe-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="e4efe-126">用於存取模擬器儲存體：</span><span class="sxs-lookup"><span data-stu-id="e4efe-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="e4efe-127">若要建立任何 Azure 服務用戶端，您必須使用 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="e4efe-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="e4efe-128">您可以使用下列其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="e4efe-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="e4efe-129">直接將連接字串傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="e4efe-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="e4efe-130">使用 **CloudConfigurationManager (CCM)** 檢查多種外部來源的連接字串：</span><span class="sxs-lookup"><span data-stu-id="e4efe-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="e4efe-131">預設已支援一種外部來源，即環境變數。</span><span class="sxs-lookup"><span data-stu-id="e4efe-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="e4efe-132">您可以擴充 **ConnectionStringSource** 類別以加入新來源。</span><span class="sxs-lookup"><span data-stu-id="e4efe-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="e4efe-133">在本文的各範例中，將會直接傳遞連接字串。</span><span class="sxs-lookup"><span data-stu-id="e4efe-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="e4efe-134">建立佇列</span><span class="sxs-lookup"><span data-stu-id="e4efe-134">Create a queue</span></span>
<span data-ttu-id="e4efe-135">**QueueRestProxy** 物件可讓您使用 **createQueue** 方法建立佇列。</span><span class="sxs-lookup"><span data-stu-id="e4efe-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="e4efe-136">建立佇列時，您可以在佇列上設定選項，但這並非必要動作。</span><span class="sxs-lookup"><span data-stu-id="e4efe-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="e4efe-137">(下列範例示範如何在佇列上設定中繼資料。)</span><span class="sxs-lookup"><span data-stu-id="e4efe-137">(The example below shows how to set metadata on a queue.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="e4efe-138">您不應該倚賴大小寫來區分中繼資料索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e4efe-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="e4efe-139">從服務讀取索引鍵時，所有索引鍵都是視為小寫。</span><span class="sxs-lookup"><span data-stu-id="e4efe-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="e4efe-140">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="e4efe-140">Add a message to a queue</span></span>
<span data-ttu-id="e4efe-141">若要將訊息新增至佇列，請使用 **QueueRestProxy->createMessage**。</span><span class="sxs-lookup"><span data-stu-id="e4efe-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="e4efe-142">此方法會接受佇列名稱、訊息文字以及訊息選項 (選用)。</span><span class="sxs-lookup"><span data-stu-id="e4efe-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="e4efe-143">查看下一個訊息</span><span class="sxs-lookup"><span data-stu-id="e4efe-143">Peek at the next message</span></span>
<span data-ttu-id="e4efe-144">透過呼叫 **QueueRestProxy->peekMessages** 方法，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="e4efe-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="e4efe-145">**peekMessage** 預設會傳回單一訊息，但是您可以使用 **PeekMessagesOptions->setNumberOfMessages** 方法變更該值。</span><span class="sxs-lookup"><span data-stu-id="e4efe-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="e4efe-146">將下一個訊息清除佇列</span><span class="sxs-lookup"><span data-stu-id="e4efe-146">De-queue the next message</span></span>
<span data-ttu-id="e4efe-147">您的程式碼可以使用兩個步驟來將訊息從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="e4efe-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="e4efe-148">首先，您需呼叫 **QueueRestProxy->listMessages**，這會讓從佇列讀取資料的任何其他程式碼無法看見此訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="e4efe-149">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="e4efe-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="e4efe-150">(如果未在此期間內刪除訊息，訊息就會再次於佇列中變成可見。)若要完成從佇列中移除訊息，您必須呼叫 **QueueRestProxy->deleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="e4efe-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="e4efe-151">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="e4efe-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="e4efe-152">您的程式碼會在處理完訊息之後立即呼叫 **deleteMessage** 。</span><span class="sxs-lookup"><span data-stu-id="e4efe-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="e4efe-153">變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="e4efe-153">Change the contents of a queued message</span></span>
<span data-ttu-id="e4efe-154">透過呼叫 **QueueRestProxy->updateMessage**，您可以在佇列中就地變更訊息的內容。</span><span class="sxs-lookup"><span data-stu-id="e4efe-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="e4efe-155">如果訊息代表工作作業，則您可以使用此功能來更新工作作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="e4efe-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="e4efe-156">下列程式碼將使用新的內容更新佇列訊息，並將可見度逾時設定延長 60 秒。</span><span class="sxs-lookup"><span data-stu-id="e4efe-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="e4efe-157">這可儲存與訊息相關的工作狀態，並提供用戶端多一分鐘的時間繼續處理訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="e4efe-158">您可以使用此技巧來追蹤佇列訊息上的多步驟工作流程，如果因為硬體或軟體故障而導致某個處理步驟失敗，將無需從頭開始。</span><span class="sxs-lookup"><span data-stu-id="e4efe-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="e4efe-159">通常，您也會保留重試計數，如果訊息重試超過 *n* 次，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="e4efe-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="e4efe-160">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-160">This protects against a message that triggers an application error each time it is processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="e4efe-161">其他將訊息移出佇列的選項</span><span class="sxs-lookup"><span data-stu-id="e4efe-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="e4efe-162">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="e4efe-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="e4efe-163">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="e4efe-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="e4efe-164">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完整處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="e4efe-165">下列程式碼範例將使用 **getMessages** 方法，在一次呼叫中取得 16 個訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="e4efe-166">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="e4efe-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="e4efe-167">它也會將可見度逾時設定為每個訊息五分鐘。</span><span class="sxs-lookup"><span data-stu-id="e4efe-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a><span data-ttu-id="e4efe-168">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="e4efe-168">Get queue length</span></span>
<span data-ttu-id="e4efe-169">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="e4efe-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="e4efe-170">**QueueRestProxy->getQueueMetadata** 方法會要求佇列服務傳回佇列本身的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e4efe-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="e4efe-171">在傳回的物件上呼叫 **getApproximateMessageCount** 方法會提供佇列中的訊息計數。</span><span class="sxs-lookup"><span data-stu-id="e4efe-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="e4efe-172">此計數只是一個約略值，因為在佇列服務回應您的要求之後，仍有新增或移除訊息的可能。</span><span class="sxs-lookup"><span data-stu-id="e4efe-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a><span data-ttu-id="e4efe-173">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="e4efe-173">Delete a queue</span></span>
<span data-ttu-id="e4efe-174">若要刪除佇列及其所有訊息，請呼叫 **QueueRestProxy->deleteQueue** 方法。</span><span class="sxs-lookup"><span data-stu-id="e4efe-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="e4efe-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4efe-175">Next steps</span></span>
<span data-ttu-id="e4efe-176">既然已了解 Azure 佇列儲存體的基本概念，請遵循下列連結以了解更複雜的儲存體工作。</span><span class="sxs-lookup"><span data-stu-id="e4efe-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="e4efe-177">造訪 [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。</span><span class="sxs-lookup"><span data-stu-id="e4efe-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="e4efe-178">如需詳細資訊，另請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="e4efe-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
<span data-ttu-id="e4efe-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span><span class="sxs-lookup"><span data-stu-id="e4efe-179">[require_once]: http://www.php.net/manual/en/function.require-once.php</span></span>
[Azure Portal]: https://portal.azure.com

