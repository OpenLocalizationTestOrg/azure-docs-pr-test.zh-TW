---
title: "aaaHow toouse 來自 PHP 的佇列儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 佇列儲存體服務 toocreate 和刪除佇列，以及插入、 取得，並刪除訊息。 範例是以 PHP 撰寫的。"
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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="0f24c-104">如何 toouse 來自 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="0f24c-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="0f24c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0f24c-105">Overview</span></span>
<span data-ttu-id="0f24c-106">本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="0f24c-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="0f24c-107">hello 範例透過類別從寫入 hello Windows SDK for PHP。</span><span class="sxs-lookup"><span data-stu-id="0f24c-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="0f24c-108">hello 涵蓋的案例包括插入，其內、 取得，和刪除佇列訊息，以及建立和刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="0f24c-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="0f24c-109">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f24c-109">Create a PHP application</span></span>
<span data-ttu-id="0f24c-110">hello 僅需求建立 PHP 應用程式存取 Azure 佇列儲存體是 hello hello Azure SDK 中的類別的參考從 PHP 的程式碼內。</span><span class="sxs-lookup"><span data-stu-id="0f24c-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="0f24c-111">您可以使用任何開發工具 toocreate 您的應用程式，包括 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="0f24c-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="0f24c-112">在本指南中，您將使用可從 PHP 應用程式內本機呼叫的佇列儲存體功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的佇列儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="0f24c-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="0f24c-113">取得 hello Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="0f24c-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="0f24c-114">設定您的應用程式 tooaccess 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="0f24c-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="0f24c-115">toouse hello Api 針對 Azure 佇列儲存體，您需要：</span><span class="sxs-lookup"><span data-stu-id="0f24c-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="0f24c-116">參考 hello 自動換片器檔案使用 hello [require_once]陳述式。</span><span class="sxs-lookup"><span data-stu-id="0f24c-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="0f24c-117">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="0f24c-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="0f24c-118">hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="0f24c-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="0f24c-119">此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="0f24c-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="0f24c-120">如果您手動安裝 hello 程式庫，您將需要 tooreference hello`WindowsAzure.php`自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="0f24c-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="0f24c-121">在以下範例 hello，hello`require_once`陳述式會一律，不會顯示，但會參考所需的 hello 範例 tooexecute hello 類別。</span><span class="sxs-lookup"><span data-stu-id="0f24c-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="0f24c-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="0f24c-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="0f24c-123">tooinstantiate Azure 佇列儲存體用戶端，您必須先取得有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0f24c-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="0f24c-124">hello 針對 hello 佇列服務的連接字串的格式如下所示。</span><span class="sxs-lookup"><span data-stu-id="0f24c-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="0f24c-125">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="0f24c-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="0f24c-126">存取 hello 模擬器儲存體：</span><span class="sxs-lookup"><span data-stu-id="0f24c-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="0f24c-127">toocreate 任何 Azure 服務用戶端，您需要 toouse hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="0f24c-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="0f24c-128">您可以使用其中一個 hello 下列技術：</span><span class="sxs-lookup"><span data-stu-id="0f24c-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="0f24c-129">傳送嗨連接字串直接 tooit。</span><span class="sxs-lookup"><span data-stu-id="0f24c-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="0f24c-130">使用**CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：</span><span class="sxs-lookup"><span data-stu-id="0f24c-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="0f24c-131">預設已支援一種外部來源，即環境變數。</span><span class="sxs-lookup"><span data-stu-id="0f24c-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="0f24c-132">您可以新增新的來源延伸 hello **ConnectionStringSource**類別。</span><span class="sxs-lookup"><span data-stu-id="0f24c-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="0f24c-133">如需此處所述的 hello 範例，將直接傳遞 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="0f24c-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="0f24c-134">建立佇列</span><span class="sxs-lookup"><span data-stu-id="0f24c-134">Create a queue</span></span>
<span data-ttu-id="0f24c-135">A **QueueRestProxy**物件可讓您建立佇列使用 hello **createQueue**方法。</span><span class="sxs-lookup"><span data-stu-id="0f24c-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="0f24c-136">在建立佇列時，您可以設定 hello 佇列上的選項，但這麼做是不需要。</span><span class="sxs-lookup"><span data-stu-id="0f24c-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="0f24c-137">(如何 hello 範例所示 tooset 佇列上的中繼資料。)</span><span class="sxs-lookup"><span data-stu-id="0f24c-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="0f24c-138">您不應該倚賴大小寫來區分中繼資料索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0f24c-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="0f24c-139">從以小寫的 hello 服務讀取所有索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0f24c-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="0f24c-140">新增訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="0f24c-140">Add a message tooa queue</span></span>
<span data-ttu-id="0f24c-141">tooadd 訊息 tooa 佇列中，使用**QueueRestProxy]-> [createMessage**。</span><span class="sxs-lookup"><span data-stu-id="0f24c-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="0f24c-142">hello 方法會接受 hello 佇列名稱、 hello 訊息文字，以及訊息的選項 （這是選擇性的）。</span><span class="sxs-lookup"><span data-stu-id="0f24c-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="0f24c-143">查看 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="0f24c-143">Peek at hello next message</span></span>
<span data-ttu-id="0f24c-144">您可以查看在訊息 （或訊息） 佇列的 hello 前端而不需移除 hello 佇列中藉由呼叫**QueueRestProxy]-> [peekMessages**。</span><span class="sxs-lookup"><span data-stu-id="0f24c-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="0f24c-145">根據預設，hello **peekMessage**方法會傳回單一訊息，但您可以變更這個值使用 hello **PeekMessagesOptions]-> [setNumberOfMessages**方法。</span><span class="sxs-lookup"><span data-stu-id="0f24c-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="0f24c-146">清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="0f24c-146">De-queue hello next message</span></span>
<span data-ttu-id="0f24c-147">您的程式碼可以使用兩個步驟來將訊息從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="0f24c-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="0f24c-148">首先，呼叫**QueueRestProxy]-> [listMessages**，讓 hello 訊息不可見 tooany hello 佇列正在讀取的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="0f24c-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="0f24c-149">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="0f24c-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="0f24c-150">（如果這段期間沒有刪除 hello 訊息，就會變成可見 hello 佇列上一次。）您必須呼叫 toofinish 移除 hello 訊息從佇列中的 hello， **QueueRestProxy]-> [deleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="0f24c-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="0f24c-151">這兩個步驟的程序中移除訊息可確保當訊息因為 toohardware 或軟體失敗，另一個執行個體的程式碼可以取得您的程式碼失敗 tooprocess 可 hello 相同訊息，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="0f24c-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="0f24c-152">您的程式碼呼叫**deleteMessage**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="0f24c-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="0f24c-153">變更佇列的訊息 hello 內容</span><span class="sxs-lookup"><span data-stu-id="0f24c-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="0f24c-154">您可以藉由呼叫變更的訊息就地 hello 佇列中的 hello 內容**QueueRestProxy]-> [updateMessage**。</span><span class="sxs-lookup"><span data-stu-id="0f24c-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="0f24c-155">如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。</span><span class="sxs-lookup"><span data-stu-id="0f24c-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="0f24c-156">下列程式碼的 hello 與新的內容更新 hello 佇列訊息，並設定 hello 可見性逾時 tooextend 另一個 60 秒。</span><span class="sxs-lookup"><span data-stu-id="0f24c-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="0f24c-157">這可以節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="0f24c-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="0f24c-158">您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。</span><span class="sxs-lookup"><span data-stu-id="0f24c-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="0f24c-159">一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="0f24c-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="0f24c-160">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="0f24c-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="0f24c-161">其他將訊息移出佇列的選項</span><span class="sxs-lookup"><span data-stu-id="0f24c-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="0f24c-162">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="0f24c-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="0f24c-163">首先，您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="0f24c-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="0f24c-164">第二，您可以設定長或短的可見性逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="0f24c-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="0f24c-165">hello 下列程式碼範例會使用 hello **getMessages**方法 tooget 16 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="0f24c-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="0f24c-166">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="0f24c-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="0f24c-167">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="0f24c-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="0f24c-168">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="0f24c-168">Get queue length</span></span>
<span data-ttu-id="0f24c-169">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="0f24c-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="0f24c-170">hello **QueueRestProxy]-> [getQueueMetadata**方法詢問 hello 佇列中的 hello 佇列服務 tooreturn 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0f24c-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="0f24c-171">呼叫 hello **getApproximateMessageCount**上 hello 方法會傳回物件提供的訊息數量是在佇列中的計數。</span><span class="sxs-lookup"><span data-stu-id="0f24c-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="0f24c-172">hello 計數只是近似的因為可以新增或移除之後 hello 佇列服務會回應 tooyour 要求訊息。</span><span class="sxs-lookup"><span data-stu-id="0f24c-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="0f24c-173">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="0f24c-173">Delete a queue</span></span>
<span data-ttu-id="0f24c-174">toodelete 佇列和所有 hello 訊息，請呼叫 hello **QueueRestProxy]-> [deletequeue 等**方法。</span><span class="sxs-lookup"><span data-stu-id="0f24c-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0f24c-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f24c-175">Next steps</span></span>
<span data-ttu-id="0f24c-176">現在，您學到的 Azure 佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn:</span><span class="sxs-lookup"><span data-stu-id="0f24c-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="0f24c-177">請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。</span><span class="sxs-lookup"><span data-stu-id="0f24c-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="0f24c-178">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="0f24c-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

