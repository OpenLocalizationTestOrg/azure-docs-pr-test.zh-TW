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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>如何 toouse Service Bus 主題和訂閱與 PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本文章將示範如何 toouse Service Bus 主題和訂閱。 hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP](../php-download-sdk.md)。 hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>建立 PHP 應用程式
僅建立 PHP 應用程式存取 hello Azure Blob 服務的需求是在 hello tooreference 類別 hello [Azure SDK for PHP](../php-download-sdk.md)從您的程式碼中。 您可以使用任何開發工具 toocreate，您的應用程式或 [記事本]。

> [!NOTE]
> 您的 PHP 安裝也必須擁有 hello [OpenSSL 延伸](http://php.net/openssl)安裝並啟用。
> 
> 

本文說明如何 toouse 服務內的 PHP 應用程式在本機，或在 Azure web 角色、 背景工作角色或網站中執行程式碼可以呼叫的功能。

## <a name="get-hello-azure-client-libraries"></a>取得 hello Azure 用戶端程式庫
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>設定您的應用程式 toouse 服務匯流排
toouse hello 服務匯流排 Api:

1. 參考 hello 自動換片器檔案使用 hello [require_once] [ require-once]陳述式。
2. 參考任何您可能使用的類別。

hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServiceBusService**類別。

> [!NOTE]
> 此範例 （和本文中的其他範例） 假設您已安裝 Azure 透過編輯器的 hello PHP 用戶端程式庫。 如果您是手動或以西洋梨封裝安裝 hello 程式庫，您必須參考 hello **WindowsAzure.php**自動換片器檔案。
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

在下列範例的 hello，hello`require_once`永遠不會顯示陳述式，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。

## <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
tooinstantiate 服務匯流排用戶端，您必須先有有效的連接字串格式如下：

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

其中`Endpoint`的 hello 格式通常是`https://[yourNamespace].servicebus.windows.net`。

toocreate 任何 Azure 服務用戶端，您必須使用 hello`ServicesBuilder`類別。 您可以：

* 傳送嗨連接字串直接 tooit。
* 使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：
  * 預設已支援一種外部來源，即環境變數。
  * 您可以新增新的來源延伸 hello`ConnectionStringSource`類別。

如需此處所述的 hello 範例，hello 連接字串會直接傳遞。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>建立主題
您可以執行管理作業的服務匯流排主題透過 hello`ServiceBusRestProxy`類別。 A`ServiceBusRestProxy`透過 hello 建構物件`ServicesBuilder::createServiceBusService`factory 方法搭配適當的連接字串會封裝 hello 語彙基元的權限 toomanage 它。

下列範例會示範如何 hello tooinstantiate`ServiceBusRestProxy`呼叫`ServiceBusRestProxy->createTopic`toocreate 的主題`mytopic`內`MySBNamespace`命名空間：

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
> 您可以使用 hello`listTopics`方法`ServiceBusRestProxy`物件 toocheck，如果在服務命名空間已經存在具有指定名稱的主題。
> 
> 

## <a name="create-a-subscription"></a>建立訂用帳戶
主題訂用帳戶也會建立以 hello`ServiceBusRestProxy->createSubscription`方法。 訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>建立訂用帳戶與 hello 預設 (MatchAll) 篩選器
hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。 當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。 hello 下列範例會建立名為 'mysubscription' 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。

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

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以設定可讓您 toospecify tooa 主題應該會出現特定主題的訂用帳戶內傳送的訊息篩選器。 hello 最有彈性的訂用帳戶支援的篩選器的類型為 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter)，它會實作 SQL92 的子集。 SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。 如需 SqlFilters 的詳細資訊，請參閱 [SqlFilter.SqlExpression 屬性][sqlfilter]。

> [!NOTE]
> 每個訂用帳戶的規則處理內送訊息獨立地將其結果訊息 toohello 訂用帳戶。 此外，每個新的訂用帳戶具有預設**規則**可將所有訊息從 hello 主題 toohello 訂用帳戶都加入的篩選物件。 tooreceive 僅訊息符合您篩選條件，您必須移除 hello 預設規則。 您可以藉由使用 hello 移除 hello 預設規則`ServiceBusRestProxy->deleteRule`方法。
> 
> 

hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`MessageNumber`大於 3 的屬性。 請參閱[傳送訊息 tooa 主題](#send-messages-to-a-topic)新增自訂屬性 toomessages 相關資訊。

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

請注意，此程式碼需要 hello 使用其他的命名空間： `WindowsAzure\ServiceBus\Models\SubscriptionInfo`。

同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與`SqlFilter`只選取有訊息`MessageNumber`屬性小於或等於 too3。

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

現在，當訊息傳送 toohello`mytopic`主題，它永遠傳遞訂閱 tooreceivers toohello`mysubscription`訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`訂用帳戶 (視 hello 訊息內容）。

## <a name="send-messages-tooa-topic"></a>傳送訊息 tooa 主題
toosend 訊息 tooa Service Bus 主題，您的應用程式呼叫 hello`ServiceBusRestProxy->sendTopicMessage`方法。 hello 下列程式碼會示範如何 toosend 訊息 toohello`mytopic`先前中建立的主題`MySBNamespace`服務命名空間。

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

TooService 匯流排主題是 hello 的執行個體傳送訊息[BrokeredMessage] [ BrokeredMessage]類別。 [BrokeredMessage] [ BrokeredMessage]物件具有一組標準的屬性和方法，以及可以使用的 toohold 自訂應用程式特定屬性的屬性。 hello 下列範例示範如何 toosend 5 測試訊息 toohello`mytopic`先前建立的主題。 hello`setProperty`方法是使用的 tooadd 自訂屬性 (`MessageNumber`) tooeach 訊息。 請注意該 hello`MessageNumber`屬性值會變動，每個訊息 (hello 中所示，您可以使用哪些訂閱接收，此值 toodetermine[建立訂用帳戶](#create-a-subscription)> 一節):

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

服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。 主題大小的這項上限為 5 GB。 如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。

## <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
hello 最佳 tooreceive 訊息方式來自訂用帳戶是 toouse`ServiceBusRestProxy->receiveSubscriptionMessage`方法。 訊息可以兩種不同的模式接收：[*ReceiveAndDelete* 和 *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)。 **PeekLock** hello 預設值。

當使用 hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中，接收是單發式作業; 也就是當服務匯流排訂用帳戶中收到訊息的讀取的要求時，它會標示為正在使用的 hello 訊息，就傳回該 toohello應用程式。 [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * 模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

在預設的 hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中，接收訊息會變成兩階段作業，使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段接收處理序藉由傳遞收到 hello 訊息太`ServiceBusRestProxy->deleteMessage`。 當服務匯流排會看見 hello`deleteMessage`呼叫，它會將標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。

下列範例會示範如何 hello tooreceive 和處理訊息，使用[PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode)模式 （hello 預設模式）。 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>如何處理應用程式當機與無法讀取的訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`收到 hello 訊息上的方法 (而不是 hello`deleteMessage`方法)。 這將導致 hello 佇列內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則 Service Bus hello 訊息將會解除鎖定自動，並將其可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為*至少一旦*處理; 亦即，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tooapplications toohandle 重複的訊息傳遞。 這通常用來達成 hello `getMessageId` hello 訊息，嘗試傳遞都維持不變的方法。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
主題或訂用帳戶，使用 hello toodelete`ServiceBusRestProxy->deleteTopic`或 hello`ServiceBusRestProxy->deleteSubscripton`方法，分別。 請注意，刪除主題也會刪除任何訂用帳戶註冊的 hello 主題。

hello 下列範例示範如何 toodelete 主題命名`mytopic`和其已註冊的訂閱。

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

使用 hello`deleteSubscription`方法，您可以個別刪除訂用帳戶：

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>後續步驟
現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[佇列、 主題和訂用帳戶][ Queues, topics, and subscriptions]如需詳細資訊。

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
