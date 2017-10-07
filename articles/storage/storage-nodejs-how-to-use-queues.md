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
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="11b07-104">如何 toouse 從 Node.js 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="11b07-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="11b07-105">概觀</span><span class="sxs-lookup"><span data-stu-id="11b07-105">Overview</span></span>
<span data-ttu-id="11b07-106">本指南也說明如何使用 tooperform 常見案例 hello Microsoft Azure 佇列服務。</span><span class="sxs-lookup"><span data-stu-id="11b07-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="11b07-107">使用 hello Node.js 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="11b07-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="11b07-108">hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="11b07-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="11b07-109">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="11b07-109">Create a Node.js Application</span></span>
<span data-ttu-id="11b07-110">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="11b07-110">Create a blank Node.js application.</span></span> <span data-ttu-id="11b07-111">建立 Node.js 應用程式的指示，請參閱[Node.js web 應用程式建立 Azure App Service 中]，[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan]使用 Windows PowerShell 或[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]。</span><span class="sxs-lookup"><span data-stu-id="11b07-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="11b07-112">設定您的應用程式 tooAccess 儲存體</span><span class="sxs-lookup"><span data-stu-id="11b07-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="11b07-113">toouse Azure 儲存體，您會需要 hello Azure 儲存體 SDK for Node.js，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="11b07-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="11b07-114">使用節點封裝管理員 (NPM) tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="11b07-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="11b07-115">使用命令列介面，例如**PowerShell** (Windows，)**終端機**(Mac，) 或**撞**(Unix)，瀏覽 toohello 資料夾建立範例應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="11b07-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="11b07-116">型別**npm 安裝 azure 儲存體**hello 命令視窗中。</span><span class="sxs-lookup"><span data-stu-id="11b07-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="11b07-117">Hello 命令的輸出會類似下列範例的 toohello。</span><span class="sxs-lookup"><span data-stu-id="11b07-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="11b07-118">您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="11b07-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="11b07-119">在該資料夾中，您會發現 hello **azure 儲存體**套件，其中包含您需要存取儲存體的 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="11b07-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="11b07-120">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="11b07-120">Import hello package</span></span>
<span data-ttu-id="11b07-121">使用 [記事本] 或其他文字編輯器，新增下列 toohello 頂端的 hello**立即轉譯 server.js** hello 應用程式檔案，但您想 toouse 儲存體：</span><span class="sxs-lookup"><span data-stu-id="11b07-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="11b07-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="11b07-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="11b07-123">hello azure 模組會讀取 hello 環境變數 AZURE\_儲存體\_帳戶和 AZURE\_儲存體\_存取\_索引鍵或 AZURE\_儲存體\_連線\_所需的資訊 tooconnect tooyour Azure 儲存體帳戶的字串。</span><span class="sxs-lookup"><span data-stu-id="11b07-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="11b07-124">如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊**createQueueService**。</span><span class="sxs-lookup"><span data-stu-id="11b07-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="11b07-125">如需設定 hello hello 環境變數的範例[Azure 入口網站](https://portal.azure.com)Azure 網站，請參閱[Node.js web 應用程式使用 hello Azure 資料表服務]。</span><span class="sxs-lookup"><span data-stu-id="11b07-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="11b07-126">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="11b07-126">How To: Create a Queue</span></span>
<span data-ttu-id="11b07-127">hello 下列程式碼會建立**QueueService**物件，可讓您與佇列搭配 toowork。</span><span class="sxs-lookup"><span data-stu-id="11b07-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="11b07-128">使用 hello **createQueueIfNotExists**方法，傳回 hello 指定的佇列是否已經存在，或建立新的佇列與 hello 指定名稱，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="11b07-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="11b07-129">建立 hello 佇列時，如果`result.created`為 true。</span><span class="sxs-lookup"><span data-stu-id="11b07-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="11b07-130">如果 hello 佇列存在，`result.created`為 false。</span><span class="sxs-lookup"><span data-stu-id="11b07-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="11b07-131">篩選器</span><span class="sxs-lookup"><span data-stu-id="11b07-131">Filters</span></span>
<span data-ttu-id="11b07-132">選擇性的篩選作業可能會使用執行套用的 toooperations **QueueService**。</span><span class="sxs-lookup"><span data-stu-id="11b07-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="11b07-133">篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：</span><span class="sxs-lookup"><span data-stu-id="11b07-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="11b07-134">在執行其前置處理 hello 要求選項之後, hello 方法需要 toocall 「 下一步 以下列簽章的 hello 傳遞回呼：</span><span class="sxs-lookup"><span data-stu-id="11b07-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="11b07-135">Hello 回呼此回呼中,，在處理 hello returnObject （hello 回應 hello 要求 toohello 伺服器） 之後時，需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或是只會叫用 finalCallback 否則 tooend 向上 hello叫用服務。</span><span class="sxs-lookup"><span data-stu-id="11b07-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="11b07-136">實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="11b07-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="11b07-137">hello 下列範例會建立**QueueService**物件，使用 hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="11b07-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="11b07-138">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="11b07-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="11b07-139">將訊息插入佇列中，使用 hello tooinsert **createMessage**方法來建立新的訊息，並將它加入 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="11b07-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="11b07-140">如何： 檢視 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="11b07-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="11b07-141">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **peekMessages**方法。</span><span class="sxs-lookup"><span data-stu-id="11b07-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="11b07-142">**peekMessages** 預設會查看單一訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="11b07-143">hello`result`包含 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="11b07-144">使用**peekMessages** hello 佇列中不有任何訊息時將不會傳回錯誤，但是會不傳回任何訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="11b07-145">如何： 清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="11b07-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="11b07-146">處理訊息是兩階段的過程：</span><span class="sxs-lookup"><span data-stu-id="11b07-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="11b07-147">清除佇列 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="11b07-148">刪除 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-148">Delete hello message.</span></span>

<span data-ttu-id="11b07-149">toodequeue 訊息時，使用**getMessages**。</span><span class="sxs-lookup"><span data-stu-id="11b07-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="11b07-150">這會 hello 訊息在 hello 佇列中不可見以便讓其他用戶端可以處理它們。</span><span class="sxs-lookup"><span data-stu-id="11b07-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="11b07-151">一旦您的應用程式已處理訊息，呼叫**deleteMessage** toodelete 從 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="11b07-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="11b07-152">下列範例中的 hello 取得訊息時，則會將它刪除：</span><span class="sxs-lookup"><span data-stu-id="11b07-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="11b07-153">根據預設，只是 30 秒之後，它便可見 tooother 用戶端隱藏訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="11b07-154">您可以使用具有 **getMessages** 的 `options.visibilityTimeout` 指定其他值。</span><span class="sxs-lookup"><span data-stu-id="11b07-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="11b07-155">使用**getMessages** hello 佇列中不有任何訊息時將不會傳回錯誤，但是會不傳回任何訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="11b07-156">如何： 變更 hello 排入佇列的訊息內容</span><span class="sxs-lookup"><span data-stu-id="11b07-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="11b07-157">您可以變更的訊息中就地 hello 佇列使用的 hello 內容**updateMessage**。</span><span class="sxs-lookup"><span data-stu-id="11b07-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="11b07-158">下列範例中的 hello 更新訊息的 hello 文字：</span><span class="sxs-lookup"><span data-stu-id="11b07-158">hello following example updates hello text of a message:</span></span>

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="11b07-159">作法：清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="11b07-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="11b07-160">自訂從佇列中擷取訊息的方法有兩種：</span><span class="sxs-lookup"><span data-stu-id="11b07-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="11b07-161">`options.numOfMessages`-擷取一批訊息 （向上 too32。)</span><span class="sxs-lookup"><span data-stu-id="11b07-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="11b07-162">`options.visibilityTimeout` - 設定較長或較短的隱藏逾時。</span><span class="sxs-lookup"><span data-stu-id="11b07-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="11b07-163">hello 下列範例會使用 hello **getMessages**方法 tooget 15 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="11b07-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="11b07-164">接著它會使用 for 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="11b07-165">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的這個方法所傳回的所有訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="11b07-166">如何： 取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="11b07-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="11b07-167">hello **getQueueMetadata**傳回 hello 佇列，包括 hello 大約的訊息 hello 佇列中等候的數目的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="11b07-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="11b07-168">作法：列出佇列</span><span class="sxs-lookup"><span data-stu-id="11b07-168">How To: List Queues</span></span>
<span data-ttu-id="11b07-169">tooretrieve 的佇列，使用清單**listQueuesSegmented**。</span><span class="sxs-lookup"><span data-stu-id="11b07-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="11b07-170">tooretrieve 特定的前置詞來篩選清單，請使用**listQueuesSegmentedWithPrefix**。</span><span class="sxs-lookup"><span data-stu-id="11b07-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="11b07-171">如果無法傳回所有佇列，`result.continuationToken`可以做為第一個參數的 hello **listQueuesSegmented** hello 第二個參數或**listQueuesSegmentedWithPrefix** tooretrieve 取得更多結果。</span><span class="sxs-lookup"><span data-stu-id="11b07-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="11b07-172">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="11b07-172">How To: Delete a Queue</span></span>
<span data-ttu-id="11b07-173">toodelete 佇列和所有 hello 訊息包含在它，請呼叫**deletequeue 等**hello 佇列物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="11b07-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="11b07-174">tooclear 所有訊息從佇列中而不刪除它，會都使用**clearMessages**。</span><span class="sxs-lookup"><span data-stu-id="11b07-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="11b07-175">作法：使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="11b07-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="11b07-176">共用存取簽章 (SAS) 是安全的方式 tooprovide 細微的存取權 tooqueues，但未提供您的儲存體帳戶名稱或索引鍵。</span><span class="sxs-lookup"><span data-stu-id="11b07-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="11b07-177">SAS 通常是使用的 tooprovide 有限存取 tooyour 佇列，例如 toosubmit 訊息允許行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="11b07-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="11b07-178">信任的應用程式，例如雲端服務會產生 SAS 使用 hello **generateSharedAccessSignature**的 hello **QueueService**，然後將其提供 tooan 不受信任或非完全信任的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11b07-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="11b07-179">例如行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="11b07-179">For example, a mobile app.</span></span> <span data-ttu-id="11b07-180">hello SAS 會產生使用原則描述 hello 開始和結束日期的 hello 期間 SAS 有效，以及 hello 存取層級授與的 toohello SAS 持有者。</span><span class="sxs-lookup"><span data-stu-id="11b07-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="11b07-181">hello 下列範例會產生新的共用的存取原則，可讓 hello SAS 持有者 tooadd 訊息 toohello 佇列，並到期之後建立的 hello 時 100 分鐘。</span><span class="sxs-lookup"><span data-stu-id="11b07-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="11b07-182">請注意 hello 主機資訊必須提供此外，視需要當 hello SAS 持有者嘗試 tooaccess hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="11b07-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="11b07-183">hello 用戶端應用程式，然後使用 hello 與 SAS **QueueServiceWithSAS** tooperform hello 佇列作業。</span><span class="sxs-lookup"><span data-stu-id="11b07-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="11b07-184">下列範例中的 hello 連接 toohello 佇列，並且建立訊息。</span><span class="sxs-lookup"><span data-stu-id="11b07-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="11b07-185">Hello SAS 產生後新增存取與嘗試進行 tooread 更新或刪除訊息，則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="11b07-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="11b07-186">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="11b07-186">Access control lists</span></span>
<span data-ttu-id="11b07-187">您也可以使用存取控制清單 (ACL) tooset hello 存取原則 SAS 的。</span><span class="sxs-lookup"><span data-stu-id="11b07-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="11b07-188">如果您想 tooallow 多個用戶端 tooaccess hello 佇列，但每個用戶端提供不同的存取原則，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="11b07-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="11b07-189">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="11b07-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="11b07-190">下列範例中的 hello 定義兩個原則。其中一個 'user1' 和 'user2' 其中一個值：</span><span class="sxs-lookup"><span data-stu-id="11b07-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="11b07-191">下列範例取得 hello hello 目前 ACL **myqueue**，然後將 hello 新原則使用**setQueueAcl**。</span><span class="sxs-lookup"><span data-stu-id="11b07-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="11b07-192">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="11b07-192">This approach allows:</span></span>

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

<span data-ttu-id="11b07-193">一次 hello 已設定 ACL，然後您可以建立根據 hello 識別碼原則 SAS。</span><span class="sxs-lookup"><span data-stu-id="11b07-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="11b07-194">hello 下列範例會建立新的 SAS 'user2':</span><span class="sxs-lookup"><span data-stu-id="11b07-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="11b07-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11b07-195">Next Steps</span></span>
<span data-ttu-id="11b07-196">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。</span><span class="sxs-lookup"><span data-stu-id="11b07-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="11b07-197">請瀏覽 hello [Azure 儲存體團隊部落格][Azure Storage Team Blog]。</span><span class="sxs-lookup"><span data-stu-id="11b07-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="11b07-198">請瀏覽 hello[節點的 Azure 儲存體 SDK] [ Azure Storage SDK for Node] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="11b07-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Node.js web 應用程式建立 Azure App Service 中]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web 應用程式使用 hello Azure 資料表服務]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[建置和部署 Azure 雲端服務的 Node.js 應用程式 tooan]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[建置和部署使用 Web Matrix Node.js web 應用程式 tooAzure]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
