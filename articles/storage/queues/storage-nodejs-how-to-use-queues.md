---
title: "如何使用 Node.js 中的佇列儲存體 | Microsoft Docs"
description: "了解如何使用 Azure 佇列服務來建立和刪除佇列，以及插入、取得和刪除訊息。 範例以 Node.js 撰寫。"
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
ms.openlocfilehash: 15c1d3cb6eac8fc14837277c4a4275dea91701cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="b72e3-104">如何使用 Node.js 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b72e3-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="b72e3-105">概觀</span><span class="sxs-lookup"><span data-stu-id="b72e3-105">Overview</span></span>
<span data-ttu-id="b72e3-106">本指南示範如何使用 Microsoft Azure 佇列服務執行常見案例。</span><span class="sxs-lookup"><span data-stu-id="b72e3-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="b72e3-107">這些範例使用 Node.js API 撰寫。</span><span class="sxs-lookup"><span data-stu-id="b72e3-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="b72e3-108">所涵蓋的案例包括「插入」、「查看」、「取得」和「刪除」佇列訊息，以及「建立和刪除佇列」。</span><span class="sxs-lookup"><span data-stu-id="b72e3-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="b72e3-109">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="b72e3-109">Create a Node.js Application</span></span>
<span data-ttu-id="b72e3-110">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b72e3-110">Create a blank Node.js application.</span></span> <span data-ttu-id="b72e3-111">如需建立 Node.js 應用程式的相關指示，請參閱[在 Azure App Service 中建立 Node.js Web 應用程式](../../app-service-web/app-service-web-get-started-nodejs.md)、[使用 Windows PowerShell 建立 Node.js 應用程式並部署至 Azure 雲端服務](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)，或[使用 Web Matrix 建立 Node.js Web 應用程式並部署至 Azure](https://www.microsoft.com/web/webmatrix/)。</span><span class="sxs-lookup"><span data-stu-id="b72e3-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="b72e3-112">設定您的應用程式以存取儲存體</span><span class="sxs-lookup"><span data-stu-id="b72e3-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="b72e3-113">若要使用 Azure 儲存體，您需要 Azure Storage SDK for Node.js，這包含一組便利程式庫，能與儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="b72e3-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="b72e3-114">使用 Node Package Manager (NPM) 取得套件</span><span class="sxs-lookup"><span data-stu-id="b72e3-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="b72e3-115">使用命令列介面，例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Unix)，瀏覽到您建立範例應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b72e3-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="b72e3-116">在命令視窗中輸入 **npm install azure-storage** 。</span><span class="sxs-lookup"><span data-stu-id="b72e3-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="b72e3-117">此命令的輸出類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="b72e3-117">Output from the command is similar to the following example.</span></span>
 
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

3. <span data-ttu-id="b72e3-118">您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b72e3-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="b72e3-119">該資料夾中有 **azure-storage** 封裝，當中包含存取儲存體所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="b72e3-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="b72e3-120">匯入套件</span><span class="sxs-lookup"><span data-stu-id="b72e3-120">Import the package</span></span>
<span data-ttu-id="b72e3-121">使用記事本或其他文字編輯器，將以下內容新增至您要使用儲存體之應用程式的 **server.js** 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="b72e3-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="b72e3-122">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="b72e3-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="b72e3-123">azure 模組會讀取環境變數 AZURE\_STORAGE\_ACCOUNT 和 AZURE\_STORAGE\_ACCESS\_KEY，或 AZURE\_STORAGE\_CONNECTION\_STRING，以取得連接 Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="b72e3-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="b72e3-124">如果未設定這些環境變數，則在呼叫 **createQueueService**時必須指定帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b72e3-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="b72e3-125">如需針對 Azure 網站在 [Azure 入口網站](https://portal.azure.com)中設定環境變數的範例，請參閱 [使用 Azure 表格服務的 Node.js Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b72e3-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="b72e3-126">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="b72e3-126">How To: Create a Queue</span></span>
<span data-ttu-id="b72e3-127">下列程式碼會建立一個 **QueueService** 物件，其讓您能夠使用佇列。</span><span class="sxs-lookup"><span data-stu-id="b72e3-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="b72e3-128">請使用 **createQueueIfNotExists** 方法，此方法會傳回指定的佇列 (如果佇列已經存在)，或以指定的名稱建立新佇列 (如果佇列不存在)。</span><span class="sxs-lookup"><span data-stu-id="b72e3-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="b72e3-129">如果建立佇列，則 `result.created` 為 true。</span><span class="sxs-lookup"><span data-stu-id="b72e3-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="b72e3-130">如果佇列已存在，則 `result.created` 為 false。</span><span class="sxs-lookup"><span data-stu-id="b72e3-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="b72e3-131">篩選器</span><span class="sxs-lookup"><span data-stu-id="b72e3-131">Filters</span></span>
<span data-ttu-id="b72e3-132">可以將選用性的篩選操作套用到使用 **QueueService** 執行的操作。</span><span class="sxs-lookup"><span data-stu-id="b72e3-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="b72e3-133">篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：</span><span class="sxs-lookup"><span data-stu-id="b72e3-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="b72e3-134">在對要求選項進行前處理之後，方法需要呼叫 "next" 並傳遞具有下列簽章的回呼：</span><span class="sxs-lookup"><span data-stu-id="b72e3-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="b72e3-135">在此回呼中，以及處理 returnObject (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是就改為叫用 finalCallback 結束服務叫用。</span><span class="sxs-lookup"><span data-stu-id="b72e3-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="b72e3-136">Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="b72e3-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="b72e3-137">以下會建立使用 **ExponentialRetryPolicyFilter** 的 **QueueService** 物件：</span><span class="sxs-lookup"><span data-stu-id="b72e3-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="b72e3-138">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="b72e3-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="b72e3-139">若要將訊息插入佇列，請使用 **createMessage** 方法建立新訊息，然後將該訊息加到佇列中。</span><span class="sxs-lookup"><span data-stu-id="b72e3-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="b72e3-140">作法：預覽下一個訊息</span><span class="sxs-lookup"><span data-stu-id="b72e3-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="b72e3-141">透過呼叫 **peekMessages** 方法，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="b72e3-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="b72e3-142">**peekMessages** 預設會查看單一訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="b72e3-143">`result` 包含訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="b72e3-144">當佇列中沒有任何訊息時，使用 **peekMessages** 並不會傳回錯誤，不過也不會傳回任何訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="b72e3-145">作法：清除下一個佇列訊息</span><span class="sxs-lookup"><span data-stu-id="b72e3-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="b72e3-146">處理訊息是兩階段的過程：</span><span class="sxs-lookup"><span data-stu-id="b72e3-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="b72e3-147">從佇列中清除訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-147">Dequeue the message.</span></span>
2. <span data-ttu-id="b72e3-148">刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-148">Delete the message.</span></span>

<span data-ttu-id="b72e3-149">若要從佇列中清除訊息，請使用 **getMessages**。</span><span class="sxs-lookup"><span data-stu-id="b72e3-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="b72e3-150">這樣會使訊息從佇列中隱藏起來，而不讓其他用戶端處理它。</span><span class="sxs-lookup"><span data-stu-id="b72e3-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="b72e3-151">當應用程式處理訊息之後，請呼叫 **deleteMessage** 從佇列中刪除它。</span><span class="sxs-lookup"><span data-stu-id="b72e3-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="b72e3-152">下列範例會取得訊息，接著刪除訊息：</span><span class="sxs-lookup"><span data-stu-id="b72e3-152">The following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="b72e3-153">依預設，訊息只會隱藏 30 秒，之後又會被其他用戶端看見。</span><span class="sxs-lookup"><span data-stu-id="b72e3-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="b72e3-154">您可以使用具有 **getMessages** 的 `options.visibilityTimeout` 指定其他值。</span><span class="sxs-lookup"><span data-stu-id="b72e3-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b72e3-155">當佇列中沒有任何訊息時，使用 **getMessages** 並不會傳回錯誤，不過也不會傳回任何訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="b72e3-156">作法：變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="b72e3-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="b72e3-157">您可以使用 **updateMessage**在佇列中就地變更訊息內容。</span><span class="sxs-lookup"><span data-stu-id="b72e3-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="b72e3-158">下列範例會更新訊息的文字：</span><span class="sxs-lookup"><span data-stu-id="b72e3-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="b72e3-159">作法：清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="b72e3-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="b72e3-160">自訂從佇列中擷取訊息的方法有兩種：</span><span class="sxs-lookup"><span data-stu-id="b72e3-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="b72e3-161">`options.numOfMessages` - 擷取一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="b72e3-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="b72e3-162">`options.visibilityTimeout` - 設定較長或較短的隱藏逾時。</span><span class="sxs-lookup"><span data-stu-id="b72e3-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="b72e3-163">下列範例使用 **getMessages** 方法，在一次呼叫中取得 15 個訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="b72e3-164">接著它會使用 for 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="b72e3-165">另外，對此方法傳回的所有訊息，將隱藏逾時設為五分鐘。</span><span class="sxs-lookup"><span data-stu-id="b72e3-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="b72e3-166">作法：取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="b72e3-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="b72e3-167">**getQueueMetadata** 會傳回佇列的中繼資料，包括在佇列中等待的大約訊息數目。</span><span class="sxs-lookup"><span data-stu-id="b72e3-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="b72e3-168">作法：列出佇列</span><span class="sxs-lookup"><span data-stu-id="b72e3-168">How To: List Queues</span></span>
<span data-ttu-id="b72e3-169">若要擷取佇列清單，請使用 **listQueuesSegmented**。</span><span class="sxs-lookup"><span data-stu-id="b72e3-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="b72e3-170">若要擷取依特定首碼篩選的清單，請使用 **listQueuesSegmentedWithPrefix**。</span><span class="sxs-lookup"><span data-stu-id="b72e3-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="b72e3-171">若無法傳回所有佇列，`result.continuationToken` 可做為 **listQueuesSegmented** 的第一個參數，或 **listQueuesSegmentedWithPrefix** 的第二個參數，以擷取更多結果。</span><span class="sxs-lookup"><span data-stu-id="b72e3-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="b72e3-172">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="b72e3-172">How To: Delete a Queue</span></span>
<span data-ttu-id="b72e3-173">若要刪除佇列及其內含的所有訊息，請在佇列物件上呼叫 **deleteQueue** 方法。</span><span class="sxs-lookup"><span data-stu-id="b72e3-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="b72e3-174">若要從佇列中清除所有訊息但不要刪除，請使用 **clearMessages**。</span><span class="sxs-lookup"><span data-stu-id="b72e3-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="b72e3-175">作法：使用共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="b72e3-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="b72e3-176">共用存取簽章 (SAS) 可安全地提供對佇列的精確存取，而不必提供您的儲存體帳戶名稱或金鑰。</span><span class="sxs-lookup"><span data-stu-id="b72e3-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="b72e3-177">SAS 通常用來提供對佇列的有限存取，例如允許行動應用程式提交訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="b72e3-178">信任的應用程式 (例如雲端型服務) 會使用 **QueueService** 的 **generateSharedAccessSignature** 來產生 SAS，並提供它給不信任或不完全信任的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b72e3-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="b72e3-179">例如行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="b72e3-179">For example, a mobile app.</span></span> <span data-ttu-id="b72e3-180">SAS 是使用原則來產生，該原則描述 SAS 有效期間的開始和結束日期，以及授與 SAS 持有者的存取等級。</span><span class="sxs-lookup"><span data-stu-id="b72e3-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="b72e3-181">下列範例會產生新的共用存取原則，讓 SAS 持有者將訊息新增至佇列，並於建立它之後的 100 分鐘過期。</span><span class="sxs-lookup"><span data-stu-id="b72e3-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="b72e3-182">請注意，也必須提供主機資訊，因為 SAS 持有者嘗試存取佇列時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="b72e3-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="b72e3-183">用戶端應用程式接著以 **QueueServiceWithSAS** 來使用 SAS，對佇列執行操作。</span><span class="sxs-lookup"><span data-stu-id="b72e3-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="b72e3-184">下列範例會連線到佇列並建立訊息。</span><span class="sxs-lookup"><span data-stu-id="b72e3-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="b72e3-185">因為產生的 SAS 具有新增權限，若嘗試讀取、更新或刪除訊息，則會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="b72e3-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="b72e3-186">存取控制清單</span><span class="sxs-lookup"><span data-stu-id="b72e3-186">Access control lists</span></span>
<span data-ttu-id="b72e3-187">您也可以使用存取控制清單 (ACL) 來設定 SAS 的存取原則。</span><span class="sxs-lookup"><span data-stu-id="b72e3-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="b72e3-188">若您要允許用戶端存取佇列，但對每個用戶端提供不同的存取原則，則這會很有用。</span><span class="sxs-lookup"><span data-stu-id="b72e3-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="b72e3-189">ACL 是使用存取原則陣列來實作，每個原則有相關聯的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b72e3-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="b72e3-190">下列範例定義兩個原則，其中一個用於 'user1'，另一個用於 'user2'：</span><span class="sxs-lookup"><span data-stu-id="b72e3-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="b72e3-191">下列範例會取得 **myqueue** 的目前 ACL，然後使用 **setQueueAcl** 來新增新的原則。</span><span class="sxs-lookup"><span data-stu-id="b72e3-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="b72e3-192">此方法允許：</span><span class="sxs-lookup"><span data-stu-id="b72e3-192">This approach allows:</span></span>

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

<span data-ttu-id="b72e3-193">設定 ACL 之後，您可以根據原則的識別碼來建立 SAS。</span><span class="sxs-lookup"><span data-stu-id="b72e3-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="b72e3-194">下列範例會建立 'user2' 的新 SAS：</span><span class="sxs-lookup"><span data-stu-id="b72e3-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="b72e3-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b72e3-195">Next Steps</span></span>
<span data-ttu-id="b72e3-196">了解佇列儲存體的基礎概念之後，請參考下列連結以了解有關更複雜的儲存工作。</span><span class="sxs-lookup"><span data-stu-id="b72e3-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="b72e3-197">造訪 [Azure 儲存體團隊部落格][Azure 儲存體團隊部落格]。</span><span class="sxs-lookup"><span data-stu-id="b72e3-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="b72e3-198">請造訪 GitHub 上的 [Azure Storage SDK for Node][Azure Storage SDK for Node] 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b72e3-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="b72e3-199">
[在 Azure App Service 中建立 Node.js Web 應用程式](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="b72e3-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="b72e3-200">[使用 Azure 表格服務的 Node.js Web 應用程式](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="b72e3-200">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="b72e3-201">[建立 Node.js 應用程式並部署到 Azure 雲端服務](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="b72e3-201">[Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="b72e3-202">[Azure 儲存體團隊部落格]：http://blogs.msdn.com/b/windowsazurestorage/ [使用 Web Matrix 建立 Node.js Web 應用程式並部署至 Azure]：https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="b72e3-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
