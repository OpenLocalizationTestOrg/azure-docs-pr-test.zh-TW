---
title: "aaaHow toouse Azure 服務匯流排主題和訂閱以 Node.js |Microsoft 文件"
description: "深入了解如何 toouse Service Bus 主題和訂用帳戶在 Azure 中的從 Node.js 應用程式。"
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>如何 tooUse Service Bus 主題和訂閱以 Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本指南說明如何 toouse Service Bus 主題和訂閱從 Node.js 應用程式。 hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息**tooa 主題**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。 如需主題和訂閱的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式
建立空白的 Node.js 應用程式。 如需建立 Node.js 應用程式的指示，請參閱[建立和部署 Azure 網站 Node.js 應用程式 tooan]， [Node.js 雲端服務][ Node.js Cloud Service]使用 WindowsPowerShell 中或使用 WebMatrix 的網站。

## <a name="configure-your-application-toouse-service-bus"></a>設定您的應用程式 toouse 服務匯流排
服務匯流排 toouse 下載 hello Node.js 的 Azure 套件。 此套件包含一組與 hello 服務匯流排 REST 服務通訊的程式庫。

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>使用節點封裝管理員 (NPM) tooobtain hello 套件
1. 使用命令列介面，例如**PowerShell** (Windows，)**終端機**(Mac，) 或**撞**(Unix)，瀏覽 toohello 資料夾建立範例應用程式的位置。
2. 型別**npm 安裝 azure**在 hello 命令視窗中，這應該會導致 hello 下列輸出：

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. 您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。 在該資料夾內尋找**azure**套件，其中包含需要 tooaccess Service Bus 主題 hello 程式庫。

### <a name="import-hello-module"></a>匯入 hello 模組
使用 [記事本] 或其他文字編輯器，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案：

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
hello Azure 模組會讀取 hello 環境變數`AZURE_SERVICEBUS_NAMESPACE`和`AZURE_SERVICEBUS_ACCESS_KEY`資訊所需 tooconnect tooService 匯流排。 如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊`createServiceBusService`。

如需設定 Azure 雲端服務的 hello 環境變數的範例，請參閱[Node.js 雲端服務與儲存體][Node.js Cloud Service with Storage]。

如需設定 Azure 網站的 hello 環境變數的範例，請參閱[Node.js Web 應用程式，與儲存體][Node.js Web Application with Storage]。

## <a name="create-a-topic"></a>建立主題
hello **ServiceBusService**物件可讓您 toowork 與主題。 下列程式碼將建立 **ServiceBusService** 物件。 將最上方的 hello**立即轉譯 server.js** hello 陳述式 tooimport hello azure 模組之後的檔案：

```javascript
var serviceBusService = azure.createServiceBusService();
```

藉由呼叫`createTopicIfNotExists`上 hello **ServiceBusService**物件、 hello 指定 （是否存在的話，），就會傳回主題，或將會建立新主題與 hello 指定的名稱。 hello 下列程式碼使用`createTopicIfNotExists`toocreate 或連接具名 toohello 主題`MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

hello`createServiceBusService`方法也支援其他選項，可讓您 toooverride 預設主題設定，例如訊息存留時間或主題大小上限。 hello 下列範例會設定具有時間 hello 最大主題大小 too5GB toolive 1 分鐘：

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>篩選器
選擇性的篩選作業可能會使用執行套用的 toooperations **ServiceBusService**。 篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：

```javascript
function handle (requestOptions, next)
```

執行前置處理 hello 要求選項之後, hello 方法呼叫`next`，將回呼傳遞具有下列簽章的 hello:

```javascript
function (returnObject, finalCallback, next)
```

在此回呼，然後之後處理 hello `returnObject` (hello 回應 hello 要求 toohello 伺服器)，hello 回呼需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或叫用`finalCallback`否則 tooend hello叫用服務。

實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。 hello 下列範例會建立**ServiceBusService**物件，使用 hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>建立訂用帳戶
主題訂用帳戶也會建立以 hello **ServiceBusService**物件。 訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。

> [!NOTE]
> 訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題它們相關聯，則會被刪除。 如果您的應用程式包含邏輯 toocreate 訂用帳戶，它應該先查看 hello 訂用帳戶已經有使用`getSubscription`方法。
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>建立訂用帳戶與 hello 預設 (MatchAll) 篩選器
hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。 當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題會放在訂用帳戶的虛擬佇列。 hello 下列範例會建立名為 'AllMessages' 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以建立篩選器可讓您 tooscope tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息。

hello 最有彈性的訂用帳戶支援的篩選器的類型是**SqlFilter**，它會實作 SQL92 的子集。 SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。 如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。

加入篩選條件可以 tooa 訂用帳戶使用 hello`createRule`方法 hello **ServiceBusService**物件。 這個方法可讓您將加入新篩選 tooan 現有訂用帳戶。

> [!NOTE]
> 因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器或**MatchAll**將會覆寫任何其他您可以指定的篩選器。 您可以藉由使用 hello 移除 hello 預設規則`deleteRule`方法**ServiceBusService**物件。
>
>

hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`messagenumber`大於 3 的屬性：

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與**SqlFilter**只選取有訊息`messagenumber`屬性小於或等於 too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

當訊息現在是否傳送太`MyTopic`，它會一律會將傳遞至訂閱的接收者 toohello`AllMessages`主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`主題訂用帳戶（視 hello 訊息內容）。

## <a name="how-toosend-messages-tooa-topic"></a>如何 toosend 訊息 tooa 主題
toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用`sendTopicMessage`方法 hello **ServiceBusService**物件。
訊息傳送 tooService 匯流排主題**BrokeredMessage**物件。
**BrokeredMessage**物件具有一組標準屬性 (例如`Label`和`TimeToLive`) 的字典，其中使用的 toohold 自訂應用程式特定屬性，和字串資料的主體。 應用程式可以將字串值傳遞至 hello 設定 hello hello 訊息本文`sendTopicMessage`和任何所需的標準屬性將會填入預設值。

hello 下列範例會示範 toosend 如何在五個測試訊息至`MyTopic`。 請注意該 hello `messagenumber` hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。 此主題大小會在建立時定義，上限是 5 GB。

## <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
訊息會從訂用帳戶使用接收`receiveSubscriptionMessage`方法上 hello **ServiceBusService**物件。 根據預設，訊息會刪除 hello 訂用帳戶的讀取。不過，您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它從 hello 訂用帳戶所設定 hello 選擇性參數`isPeekLock`太**true**。

hello 讀取及刪除 hello 訊息，接收作業的一部分是 hello 簡單的模式，以及應用程式可以容許不處理中失敗的 hello 事件訊息的案例是最適合的預設行為。 toounderstand，假設取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

如果 hello`isPeekLock`參數設定太**true**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。
藉由呼叫 hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理） 之後，完成接收程序 hello 第二個階段**deleteMessage**方法並提供訊息 toobe刪除做為參數。 hello **deleteMessage**方法會標示為正在使用的 hello 訊息，並移除從 hello 訂用帳戶。

hello 下列範例示範如何可以接收和處理使用`receiveSubscriptionMessage`。 hello 範例第一次收到並刪除 hello 'LowMessages' 訂用帳戶中的訊息，然後將訊息從接收 hello 'HighMessages' 訂用帳戶使用`isPeekLock`設定 tootrue。 然後刪除 hello 訊息使用`deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`方法**ServiceBusService**物件。 這將導致服務匯流排 toounlock hello 訂用帳戶內的訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

也是在訂閱中，鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為*至少一旦處理*，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。 這通常用來達成**MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。
hello 下列範例會示範如何命名 toodelete hello 主題`MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。 您也可以個別刪除訂用帳戶。 下列範例示範如何 toodelete 訂用帳戶命名`HighMessages`從 hello`MyTopic`主題：

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>後續步驟
現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。

* 請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。
* [SqlFilter][SqlFilter] 的 API 參考資料。
* 請瀏覽 hello [Azure SDK for 節點][ Azure SDK for Node] GitHub 上的儲存機制。

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[建立和部署 Azure 網站 Node.js 應用程式 tooan]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
