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
# <a name="how-toouse-service-bus-queues-with-php"></a>服務匯流排 toouse 排入佇列與 PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

本指南也說明如何 toouse 服務匯流排佇列。 hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP](../php-download-sdk.md)。 hello 涵蓋案例包括**建立佇列**，**傳送和接收訊息**，和**刪除佇列**。

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>建立 PHP 應用程式
只有建立 PHP 應用程式存取 hello Azure Blob 服務的需求為 hello hello 參考中的 hello 類別[Azure SDK for PHP](../php-download-sdk.md)從程式碼內。 您可以使用任何開發工具 toocreate，您的應用程式或 [記事本]。

> [!NOTE]
> 您的 PHP 安裝也必須擁有 hello [OpenSSL 延伸](http://php.net/openssl)安裝並啟用。
> 
> 

在本指南中，您將使用可從 PHP 應用程式內本機呼叫的服務功能，或可從 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的資料表服務功能。

## <a name="get-hello-azure-client-libraries"></a>取得 hello Azure 用戶端程式庫
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>設定您的應用程式 toouse 服務匯流排
toouse hello Service Bus 佇列應用程式開發介面，請勿 hello 遵循：

1. 參考 hello 自動換片器檔案使用 hello [require_once] [ require_once]陳述式。
2. 參考任何您可能使用的類別。

hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello`ServicesBuilder`類別。

> [!NOTE]
> 此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。 如果您是手動或以西洋梨封裝安裝 hello 程式庫，您必須參考 hello **WindowsAzure.php**自動換片器檔案。
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

在以下範例 hello，hello`require_once`永遠不會顯示陳述式，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。

## <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
tooinstantiate 服務匯流排用戶端，您必須先具備有效的連接字串格式如下：

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

其中`Endpoint`的 hello 格式通常是`[yourNamespace].servicebus.windows.net`。

toocreate 任何 Azure 服務用戶端，您必須使用 hello`ServicesBuilder`類別。 您可以：

* 傳送嗨連接字串直接 tooit。
* 使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：
  * 預設已支援一種外部來源，即環境變數
  * 您可以新增新的來源延伸 hello`ConnectionStringSource`類別

如需此處所述的 hello 範例，hello 連接字串會直接傳遞。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>建立佇列
您可以執行 hello 透過服務匯流排佇列的管理作業`ServiceBusRestProxy`類別。 A`ServiceBusRestProxy`透過 hello 建構物件`ServicesBuilder::createServiceBusService`factory 方法搭配適當的連接字串會封裝 hello 語彙基元的權限 toomanage 它。

下列範例會示範如何 hello tooinstantiate`ServiceBusRestProxy`呼叫`ServiceBusRestProxy->createQueue`toocreate 名為的佇列`myqueue`內`MySBNamespace`服務命名空間：

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
> 您可以使用 hello`listQueues`方法`ServiceBusRestProxy`物件 toocheck，如果在命名空間已經存在具有指定名稱的佇列。
> 
> 

## <a name="send-messages-tooa-queue"></a>傳送訊息 tooa 佇列
toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`ServiceBusRestProxy->sendQueueMessage`方法。 hello 下列程式碼會示範如何 toosend 訊息 toohello`myqueue`先前中建立的佇列`MySBNamespace`服務命名空間。

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

訊息已傳送太 （和從接收的資料） 的服務匯流排佇列是 hello 的執行個體[BrokeredMessage] [ BrokeredMessage]類別。 [BrokeredMessage] [ BrokeredMessage]物件具有一組標準的方法和屬性都使用的 toohold 自訂應用程式特定的屬性和任意應用程式資料的主體。

服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。 佇列大小的這項上限為 5 GB。

## <a name="receive-messages-from-a-queue"></a>從佇列接收訊息

hello 最佳方式 tooreceive 來自佇列的訊息是 toouse`ServiceBusRestProxy->receiveQueueMessage`方法。 訊息可以兩種不同的模式接收：[*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) 和 [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)。 **PeekLock** hello 預設值。

當使用[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete)模式中，接收是單發式作業; 也就是當服務匯流排佇列中接收訊息的讀取的要求，它會標示為正在使用的 hello 訊息，就傳回該 toohello 應用程式。 [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete)模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

在預設的 hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)模式中，接收訊息會變成兩階段作業，使其不容許遺失訊息的可能 toosupport 應用程式。 當服務匯流排收到要求時，會尋找 hello 耗用下一個訊息 toobe、 tooprevent 將它鎖定，接收其他取用者，然後傳回 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段接收處理序藉由傳遞收到 hello 訊息太`ServiceBusRestProxy->deleteMessage`。 當服務匯流排會看見 hello`deleteMessage`呼叫，它會將標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。

下列範例會示範如何 hello tooreceive 和處理訊息，使用[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock)模式 （hello 預設模式）。

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息

服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`收到 hello 訊息上的方法 (而不是 hello`deleteMessage`方法)。 這將導致 hello 佇列內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則 Service Bus hello 訊息將會解除鎖定自動，並將其可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為*至少一旦*處理; 亦即，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，則建議您增加額外的邏輯 tooapplications toohandle 重複的訊息傳遞。 這通常用來達成 hello `getMessageId` hello 訊息，嘗試傳遞都維持不變的方法。

## <a name="next-steps"></a>後續步驟
現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[佇列、 主題和訂用帳戶][ Queues, topics, and subscriptions]如需詳細資訊。

如需詳細資訊，也請瀏覽 hello [PHP 開發人員中心](https://azure.microsoft.com/develop/php/)。

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


