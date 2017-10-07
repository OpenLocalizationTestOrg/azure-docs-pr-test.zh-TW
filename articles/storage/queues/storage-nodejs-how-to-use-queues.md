---
title: "aaaHow toouse 佇列儲存體從 Node.js |Microsoft 文件"
description: "了解 toouse hello Azure 佇列服務 toocreate 和刪除佇列，以及插入、 取得，並刪除訊息。 範例以 Node.js 撰寫。"
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>如何 toouse 從 Node.js 佇列儲存體
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>概觀
本指南也說明如何使用 tooperform 常見案例 hello Microsoft Azure 佇列服務。 使用 hello Node.js 應用程式開發介面撰寫 hello 範例。 hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式
建立空白的 Node.js 應用程式。 建立 Node.js 應用程式的指示，請參閱[Node.js web 應用程式建立 Azure App Service 中](../../app-service-web/app-service-web-get-started-nodejs.md)，[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)使用 Windows PowerShell 或[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure](https://www.microsoft.com/web/webmatrix/)。

## <a name="configure-your-application-tooaccess-storage"></a>設定您的應用程式 tooAccess 儲存體
toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>使用節點封裝管理員 (NPM) tooobtain hello 套件
1. 使用命令列介面，例如**PowerShell** (Windows，)**終端機**(Mac，) 或**撞**(Unix)，瀏覽 toohello 資料夾建立範例應用程式的位置。
2. 型別**npm 安裝 azure 儲存體**hello 命令視窗中。 Hello 命令的輸出會類似下列範例的 toohello。
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. 您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。 在該資料夾中，您會發現 hello **azure 儲存體**套件，其中包含您需要存取儲存體的 hello 程式庫。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用 [記事本] 或其他文字編輯器，新增下列 toohello 頂端的 hello**立即轉譯 server.js** hello 應用程式檔案，但您想 toouse 儲存體：

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello azure 模組會讀取 hello 環境變數 AZURE\_儲存體\_帳戶和 AZURE\_儲存體\_存取\_索引鍵或 AZURE\_儲存體\_連線\_所需的資訊 tooconnect tooyour Azure 儲存體帳戶的字串。 如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**createQueueService**。

如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure 網站，請參閱 [Node.js web 應用程式使用 hello Azure 資料表服務]。

## <a name="how-to-create-a-queue"></a>作法：建立佇列
hello 下列程式碼會建立**QueueService**物件，可讓您與佇列搭配 toowork。

```
var queueSvc = azure.createQueueService();
```

使用 hello **createQueueIfNotExists**方法，傳回 hello 指定的佇列是否已經存在，或建立新的佇列與 hello 指定名稱，如果不存在。

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

建立 hello 佇列時，如果`result.created`為 true。 如果 hello 佇列存在，`result.created`為 false。

### <a name="filters"></a>篩選器
選擇性的篩選作業可能會使用執行套用的 toooperations **QueueService**。 篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：

```
function handle (requestOptions, next)
```

在執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步 以下列簽章的 hello 傳遞回呼：

```
function (returnObject, finalCallback, next)
```

Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback 否則 tooend 向上 hello叫用服務。

實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。 hello 下列範例會建立**QueueService**物件，使用 hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>作法：將訊息插入佇列中
將訊息插入佇列中，使用 hello tooinsert **createMessage**方法來建立新的訊息，並將它加入 toohello 佇列。

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>如何： 檢視 hello 下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **peekMessages**方法。 **peekMessages** 預設會查看單一訊息。

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

hello`result`包含 hello 訊息。

> [!NOTE]
> 使用**peekMessages** hello 佇列中不有任何訊息時將不會傳回錯誤，但是會不傳回任何訊息。
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>如何： 清除佇列 hello 下一個訊息
處理訊息是兩階段的過程：

1. 清除佇列 hello 訊息。
2. 刪除 hello 訊息。

toodequeue 訊息時，使用**getMessages**。 這會 hello 訊息在 hello 佇列中不可見以便讓其他用戶端可以處理它們。 一旦您的應用程式已處理訊息，呼叫**deleteMessage** toodelete 從 hello 佇列。 下列範例中的 hello 取得訊息時，則會將它刪除：

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> 根據預設，只是 30 秒之後，它便可見 tooother 用戶端隱藏訊息。 您可以使用具有 **getMessages** 的 `options.visibilityTimeout` 指定其他值。
> 
> [!NOTE]
> 使用**getMessages** hello 佇列中不有任何訊息時將不會傳回錯誤，但是會不傳回任何訊息。
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>如何： 變更 hello 排入佇列的訊息內容
您可以變更的訊息中就地 hello 佇列使用的 hello 內容**updateMessage**。 下列範例中的 hello 更新訊息的 hello 文字：

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>作法：清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種：

* `options.numOfMessages`-擷取一批訊息 （向上 too32。)
* `options.visibilityTimeout` - 設定較長或較短的隱藏逾時。

hello 下列範例會使用 hello **getMessages**方法 tooget 15 訊息在單一呼叫中的。 接著它會使用 for 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 toofive 分鐘數的這個方法所傳回的所有訊息。

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>如何： 取得 hello 佇列長度
hello **getQueueMetadata**傳回 hello 佇列，包括 hello 大約的訊息 hello 佇列中等候的數目的相關中繼資料。

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>作法：列出佇列
tooretrieve 的佇列，使用清單**listQueuesSegmented**。 tooretrieve 特定的前置詞來篩選清單，請使用**listQueuesSegmentedWithPrefix**。

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

如果無法傳回所有佇列，`result.continuationToken`可以做為第一個參數的 hello **listQueuesSegmented** hello 第二個參數或**listQueuesSegmentedWithPrefix** tooretrieve 取得更多結果。

## <a name="how-to-delete-a-queue"></a>作法：刪除佇列
toodelete 佇列和所有 hello 訊息包含在它，請呼叫**deletequeue 等**hello 佇列物件上的方法。

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

tooclear 所有訊息從佇列中而不刪除它，會都使用**clearMessages**。

## <a name="how-to-work-with-shared-access-signatures"></a>作法：使用共用存取簽章
共用存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tooqueues，但未提供您的儲存體帳戶名稱或索引鍵。 SAS 通常是使用的 tooprovide 有限存取 tooyour 佇列，例如 toosubmit 訊息允許行動裝置應用程式。

信任的應用程式，例如雲端服務會產生 SAS 使用 hello **generateSharedAccessSignature**的 hello **QueueService**，然後將其提供 tooan 不受信任或非完全信任的應用程式。 例如行動應用程式。 hello SAS 會產生使用原則描述 hello 開始和結束日期的 hello 期間 SAS 有效，以及 hello 存取層級授與的 toohello SAS 持有者。

hello 下列範例會產生新的共用的存取原則，可讓 hello SAS 持有者 tooadd 訊息 toohello 佇列，並到期之後建立的 hello 時 100 分鐘。

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

請注意 hello 主機資訊必須提供此外，視需要當 hello SAS 持有者嘗試 tooaccess hello 佇列。

hello 用戶端應用程式，然後使用 hello 與 SAS **QueueServiceWithSAS** tooperform hello 佇列作業。 下列範例中的 hello 連接 toohello 佇列，並且建立訊息。

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Hello SAS 產生後新增存取與嘗試進行 tooread 更新或刪除訊息，則會傳回錯誤。

### <a name="access-control-lists"></a>存取控制清單
您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。 如果您想 tooallow 多個用戶端 tooaccess hello 佇列，但每個用戶端提供不同的存取原則，這非常有用。

ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。 下列範例中的 hello 定義兩個原則。其中一個 'user1' 和 'user2' 其中一個值：

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

下列範例取得 hello hello 目前 ACL **myqueue**，然後將 hello 新原則使用**setQueueAcl**。 此方法允許：

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

一次 hello 已設定 ACL，然後您可以建立根據 hello 識別碼原則 SAS。 hello 下列範例會建立新的 SAS 'user2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。

* 請瀏覽 hello [Azure 儲存體團隊部落格] [Azure 儲存體團隊部落格]。
* 請瀏覽 hello[節點的 Azure 儲存體 SDK] [ Azure Storage SDK for Node] GitHub 上的儲存機制。

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[在 Azure App Service 中建立 Node.js Web 應用程式](../../app-service-web/app-service-web-get-started-nodejs.md)   
[Node.js web 應用程式使用 hello Azure 資料表服務](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[建置和部署 Node.js 應用程式 tooan Azure 雲端服務](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Azure 儲存體小組部落格]: http://blogs.msdn.com/b/windowsazurestorage/ [建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]: https://www.microsoft.com/web/webmatrix/   
