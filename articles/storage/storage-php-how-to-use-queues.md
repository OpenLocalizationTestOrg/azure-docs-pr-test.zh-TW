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
# <a name="how-toouse-queue-storage-from-php"></a>如何 toouse 來自 PHP 的佇列儲存體
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。 hello 範例透過類別從寫入 hello Windows SDK for PHP。 hello 涵蓋的案例包括插入，其內、 取得，和刪除佇列訊息，以及建立和刪除佇列。

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>建立 PHP 應用程式
hello 僅需求建立 PHP 應用程式存取 Azure 佇列儲存體是 hello hello Azure SDK 中的類別的參考從 PHP 的程式碼內。 您可以使用任何開發工具 toocreate 您的應用程式，包括 [記事本]。

在本指南中，您將使用可從 PHP 應用程式內本機呼叫的佇列儲存體功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的佇列儲存體功能。

## <a name="get-hello-azure-client-libraries"></a>取得 hello Azure 用戶端程式庫
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>設定您的應用程式 tooaccess 佇列儲存體
toouse hello Api 針對 Azure 佇列儲存體，您需要：

1. 參考 hello 自動換片器檔案使用 hello [require_once]陳述式。
2. 參考任何您可能使用的類別。

hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServicesBuilder**類別。

> [!NOTE]
> 此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。 如果您手動安裝 hello 程式庫，您將需要 tooreference hello`WindowsAzure.php`自動換片器檔案。
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

在以下範例 hello，hello`require_once`陳述式會一律，不會顯示，但會參考所需的 hello 範例 tooexecute hello 類別。

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
tooinstantiate Azure 佇列儲存體用戶端，您必須先取得有效的連接字串。 hello 針對 hello 佇列服務的連接字串的格式如下所示。

用於存取即時服務：

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

存取 hello 模擬器儲存體：

```php
UseDevelopmentStorage=true
```

toocreate 任何 Azure 服務用戶端，您需要 toouse hello **ServicesBuilder**類別。 您可以使用其中一個 hello 下列技術：

* 傳送嗨連接字串直接 tooit。
* 使用**CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：
  * 預設已支援一種外部來源，即環境變數。
  * 您可以新增新的來源延伸 hello **ConnectionStringSource**類別。

如需此處所述的 hello 範例，將直接傳遞 hello 連接字串。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>建立佇列
A **QueueRestProxy**物件可讓您建立佇列使用 hello **createQueue**方法。 在建立佇列時，您可以設定 hello 佇列上的選項，但這麼做是不需要。 (如何 hello 範例所示 tooset 佇列上的中繼資料。)

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
> 您不應該倚賴大小寫來區分中繼資料索引鍵。 從以小寫的 hello 服務讀取所有索引鍵。
> 
> 

## <a name="add-a-message-tooa-queue"></a>新增訊息 tooa 佇列
tooadd 訊息 tooa 佇列中，使用**QueueRestProxy]-> [createMessage**。 hello 方法會接受 hello 佇列名稱、 hello 訊息文字，以及訊息的選項 （這是選擇性的）。

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

## <a name="peek-at-hello-next-message"></a>查看 hello 下一個訊息
您可以查看在訊息 （或訊息） 佇列的 hello 前端而不需移除 hello 佇列中藉由呼叫**QueueRestProxy]-> [peekMessages**。 根據預設，hello **peekMessage**方法會傳回單一訊息，但您可以變更這個值使用 hello **PeekMessagesOptions]-> [setNumberOfMessages**方法。

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

## <a name="de-queue-hello-next-message"></a>清除佇列 hello 下一個訊息
您的程式碼可以使用兩個步驟來將訊息從佇列中移除。 首先，呼叫**QueueRestProxy]-> [listMessages**，讓 hello 訊息不可見 tooany hello 佇列正在讀取的其他程式碼。 依預設，此訊息會維持 30 秒的不可見狀態。 （如果這段期間沒有刪除 hello 訊息，就會變成可見 hello 佇列上一次。）您必須呼叫 toofinish 移除 hello 訊息從佇列中的 hello， **QueueRestProxy]-> [deleteMessage**。 這兩個步驟的程序中移除訊息可確保當訊息因為 toohardware 或軟體失敗，另一個執行個體的程式碼可以取得您的程式碼失敗 tooprocess 可 hello 相同訊息，然後再試一次。 您的程式碼呼叫**deleteMessage**處理 hello 訊息之後，以滑鼠右鍵。

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

## <a name="change-hello-contents-of-a-queued-message"></a>變更佇列的訊息 hello 內容
您可以藉由呼叫變更的訊息就地 hello 佇列中的 hello 內容**QueueRestProxy]-> [updateMessage**。 如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。 下列程式碼的 hello 與新的內容更新 hello 佇列訊息，並設定 hello 可見性逾時 tooextend 另一個 60 秒。 這可以節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。 您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。 一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。 這麼做可防止每次處理時便觸發應用程式錯誤的訊息。

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

## <a name="additional-options-for-de-queuing-messages"></a>其他將訊息移出佇列的選項
自訂從佇列中擷取訊息的方法有兩種。 首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短的可見性逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。 hello 下列程式碼範例會使用 hello **getMessages**方法 tooget 16 訊息在單一呼叫中的。 接著它會使用 **for** 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。

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

## <a name="get-queue-length"></a>取得佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 hello **QueueRestProxy]-> [getQueueMetadata**方法詢問 hello 佇列中的 hello 佇列服務 tooreturn 中繼資料。 呼叫 hello **getApproximateMessageCount**上 hello 方法會傳回物件提供的訊息數量是在佇列中的計數。 hello 計數只是近似的因為可以新增或移除之後 hello 佇列服務會回應 tooyour 要求訊息。

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

## <a name="delete-a-queue"></a>刪除佇列
toodelete 佇列和所有 hello 訊息，請呼叫 hello **QueueRestProxy]-> [deletequeue 等**方法。

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

## <a name="next-steps"></a>後續步驟
現在，您學到的 Azure 佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn:

* 請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。

如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

