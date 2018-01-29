---
title: "如何搭配 Node.js 使用 Azure 服務匯流排主題和訂用帳戶 | Microsoft Docs"
description: "了解如何從 Node.js 應用程式，在 Azure 中使用服務匯流排主題和訂用帳戶。"
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
ms.openlocfilehash: d9e463273fff0ecc198b0574443c4241dde7be79
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a>如何透過 Node.js 使用服務匯流排主題和訂用帳戶

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本指南說明如何從 Node.js 應用程式使用服務匯流排主題和訂閱。 涵蓋的案例包括**建立主題和訂用帳戶**、**建立訂用帳戶篩選器**、**傳送訊息至主題**、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。 如需主題和訂用帳戶的詳細資訊，請參閱[後續步驟](#next-steps)一節。

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式
建立空白的 Node.js 應用程式。 如需有關建立 Node.js 應用程式的指示，請參閱[建立 Node.js 應用程式並將其部署到 Azure 網站]、[Node.js 雲端服務][Node.js Cloud Service] (使用 Windows PowerShell) 或使用 WebMatrix 的網站。

## <a name="configure-your-application-to-use-service-bus"></a>設定應用程式以使用服務匯流排
若要使用服務匯流排，請下載 Node.js Azure 封裝。 此封裝含有一組能與服務匯流排 REST 服務通訊的便利程式庫。

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a>使用 Node Package Manager (NPM) 取得封裝
1. 使用命令列介面，例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Unix)，瀏覽到您建立範例應用程式的資料夾。
2. 在命令視窗中輸入 **npm install azure**，這應該會產生下列輸出：

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
3. 您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。 在該資料夾內找出 **azure** 封裝，其中含有存取服務匯流排主題所需的程式庫。

### <a name="import-the-module"></a>匯入模組
使用記事本或其他文字編輯器將以下內容新增至應用程式 **server.js** 檔案的頂端：

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>設定服務匯流排連接
Azure 模組會讀取環境變數 `AZURE_SERVICEBUS_CONNECTION_STRING` 以取得您從前面的步驟＜取得認證＞所取得的連接字串。 如未設定此環境變數，必須在呼叫 `createServiceBusService` 時指定帳戶資訊。

如需在 Azure 雲端服務的環境變數設定範例，請參閱[使用儲存體的 Node.js 雲端服務][Node.js Cloud Service with Storage]。

如需 Azure 網站的環境變數設定範例，請參閱[使用儲存體的 Node.js Web 應用程式][Node.js Web Application with Storage]。

## <a name="create-a-topic"></a>建立主題
**ServiceBusService** 物件可讓您使用主題。 下列程式碼將建立 **ServiceBusService** 物件。 請將程式碼新增至 **server.js** 檔案的頂端附近，放置在匯入 azure 模型的陳述式後方：

```javascript
var serviceBusService = azure.createServiceBusService();
```

藉由在 **ServiceBusService** 物件上呼叫 `createTopicIfNotExists`，系統將傳回指定的主題 (若有的話) 或建立具有指定名稱的新主題。 下列程式碼使用 `createTopicIfNotExists` 建立或連接至名稱為 `MyTopic` 的主題：

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

`createServiceBusService` 方法也支援其他選項，而可讓您覆寫訊息存留時間或主題大小上限等預設主題設定。 下列範例會將主題大小上限設為 5GB，並將存留時間設為 1 分鐘：

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
您可以將選用的篩選作業套用至使用 **ServiceBusService** 執行的作業。 篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：

```javascript
function handle (requestOptions, next)
```

對要求選項執行前置處理之後，方法會呼叫 `next`，並傳遞具有下列簽章的回呼：

```javascript
function (returnObject, finalCallback, next)
```

在此回呼中，以及處理 `returnObject` (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是改為叫用 `finalCallback` 結束服務叫用。

Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。 下列程式碼將建立使用 **ExponentialRetryPolicyFilter** 的 **ServiceBusService** 物件：

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>建立訂用帳戶
**ServiceBusService** 物件也能用來建立主題訂閱。 訂閱是具名的，它們能擁有選用的篩選器，以限制傳遞至訂閱之虛擬佇列的訊息集合。

> [!NOTE]
> 訂用帳戶是持續性的，它們會持續存在，直到本身或相關的主題遭到刪除為止。 如果應用程式含有建立訂用帳戶的邏輯，它應該會先使用 `getSubscription` 方法檢查訂用帳戶是否存在。
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a>使用預設 (MatchAll) 篩選器建立訂用帳戶
如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。 使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。 下列範例將建立名為「AllMessages」的訂用帳戶，並使用預設的 **MatchAll** 篩選器。

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以建立篩選器，讓您界定傳送至主題的哪些訊息應出現在特定主題訂用帳戶中。

訂用帳戶所支援的最具彈性篩選器類型是實作 SQL92 子集的 **SqlFilter**。 SQL 篩選器會對發佈至主題之訊息的屬性運作。 如需有關可與 SQL 篩選器搭配使用的運算式詳細資料，請檢閱 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 語法。

您可以使用 **ServiceBusService** 物件的 `createRule` 方法將篩選器新增至訂用帳戶。 此方法可讓您將篩選器新增至現有的訂用帳戶中。

> [!NOTE]
> 由於預設篩選器會自動套用至所有新的訂用帳戶，因此您必須先移除預設篩選器，否則 **MatchAll** 將會覆寫您指定的任何其他篩選器。 您可以使用 **ServiceBusService** 物件的 `deleteRule` 方法移除預設規則。
>
>

以下範例將建立名為 `HighMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取自訂 `messagenumber` 屬性大於 3 的訊息：

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

同樣地，下列範例將建立名為 `LowMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取 `messagenumber` 屬性小於或等於 3 的訊息：

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

當訊息傳送至 `MyTopic` 時，一律會將該訊息傳遞至已訂閱 `AllMessages` 主題訂用帳戶的接收者，並選擇性地傳遞至已訂閱 `HighMessages` 和 `LowMessages` 主題訂用帳戶的接收者 (視訊息內容而定)。

## <a name="how-to-send-messages-to-a-topic"></a>如何將訊息傳送至主題
若要將訊息傳送至服務匯流排主題，應用程式必須使用 **ServiceBusService** 物件的 `sendTopicMessage` 方法。
傳送至服務匯流排主題的訊息是 **BrokeredMessage** 物件。
**BrokeredMessage** 物件具有一組標準屬性 (例如 `Label` 和 `TimeToLive`)、一個用來保存自訂應用程式特定屬性的字典，以及一堆字串資料。 應用程式能將字串值傳遞至 `sendTopicMessage` 以設定訊息本文，系統會將預設值填入任何需要的標準屬性中。

下列範例說明如何將五個測試訊息傳送至 `MyTopic`。 請注意，迴圈反覆運算上每個訊息的`messagenumber` 屬性值會有變化 (這可判斷接收訊息的訂用帳戶為何)：

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

服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。 標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。 主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有最高限制。 此主題大小會在建立時定義，上限是 5 GB。

## <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
對於 **ServiceBusService** 物件使用 `receiveSubscriptionMessage` 方法即可從訂用帳戶接收訊息。 依預設，當您讀取訊息後，系統便會從訂用帳戶刪除訊息，不過您可以將選用參數 `isPeekLock` 設定為 **true**，藉此讀取 (查看) 並鎖定訊息，避免從訂用帳戶中刪除訊息。

隨著接收作業讀取及刪除訊息之預設行為是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。 若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。 因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。

如果您將 `isPeekLock` 參數設為 **true**，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。 當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。
在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫 **deleteMessage** 方法和以參數形式提供要刪除的訊息，完成接收程序的第二個階段。 **deleteMessage** 方法會將訊息標示為已取用，並將其自訂用帳戶移除。

以下範例將示範如何使用預設的 `receiveSubscriptionMessage` 模式來接收與處理訊息。 此範例會先接收來自 'LowMessages' 訂閱的訊息並加以刪除，然後再使用設定為 true 的 `isPeekLock` 接收來自 'HighMessages' 訂用帳戶的訊息。 接著再使用 `deleteMessage` 刪除訊息：

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
        })
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>如何處理應用程式當機與無法讀取的訊息
服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。 如果接收者應用程式因為某些原因無法處理訊息，它可以呼叫 **ServiceBusService** 物件上的 `unlockMessage` 方法。 這將導致服務匯流排將訂用帳戶中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。

與在訂閱內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。

如果應用程式在處理訊息之後，尚未呼叫 `deleteMessage` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。 這通常稱為*至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。 如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。 通常您可使用訊息的 **MessageId** 屬性來達到此目的，該屬性將在各個傳遞嘗試中會保持不變。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
主題和訂用帳戶是持續性的，您必須透過 [Azure 入口網站][Azure portal]或以程式設計方式明確地刪除它們。
下列範例示範如何刪除名為 `MyTopic` 的主題：

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

刪除主題也將會刪除對主題註冊的任何訂用帳戶。 您也可以個別刪除訂用帳戶。 下列範例示範如何從 `MyTopic` 主題刪除名為 `HighMessages` 的訂用帳戶：

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>後續步驟
了解基本的服務匯流排主題之後，請參考下列連結以取得更多資訊。

* 請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。
* [SqlFilter][SqlFilter] 的 API 參考資料。
* 瀏覽 GitHub 上的 [Azure SDK for Node][Azure SDK for Node] 儲存機制。

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[建立 Node.js 應用程式並將其部署到 Azure 網站]: ../app-service/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
