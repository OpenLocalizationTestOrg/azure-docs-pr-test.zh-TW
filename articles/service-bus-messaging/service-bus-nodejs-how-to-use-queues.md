---
title: "aaaHow toouse Service Bus 佇列在 Node.js |Microsoft 文件"
description: "了解如何 toouse Service Bus 排入佇列，在 Azure 中從 Node.js 應用程式。"
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="fe14e-103">服務匯流排 toouse 排入佇列以 Node.js</span><span class="sxs-lookup"><span data-stu-id="fe14e-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="fe14e-104">本文說明如何 toouse Service Bus 佇列含有 Node.js。</span><span class="sxs-lookup"><span data-stu-id="fe14e-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="fe14e-105">hello 範例以 JavaScript 撰寫，並使用 hello Node.js 的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="fe14e-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="fe14e-106">hello 涵蓋案例包括**建立佇列**，**傳送和接收訊息**，和**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="fe14e-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="fe14e-107">如需有關佇列的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="fe14e-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="fe14e-108">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="fe14e-108">Create a Node.js application</span></span>
<span data-ttu-id="fe14e-109">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe14e-109">Create a blank Node.js application.</span></span> <span data-ttu-id="fe14e-110">如需有關指示 toocreate Node.js 應用程式，請參閱[建立和部署 Azure 網站 Node.js 應用程式 tooan][Create and deploy a Node.js application tooan Azure Website]，或[Node.js 雲端服務][Node.js Cloud Service]使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="fe14e-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="fe14e-111">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="fe14e-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="fe14e-112">toouse Azure 服務匯流排，下載並使用 Node.js 的 Azure 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="fe14e-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="fe14e-113">此套件包含一組與 hello 服務匯流排 REST 服務通訊的程式庫。</span><span class="sxs-lookup"><span data-stu-id="fe14e-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="fe14e-114">使用節點封裝管理員 (NPM) tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="fe14e-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="fe14e-115">使用 hello **Windows PowerShell for Node.js**命令視窗 toonavigate toohello **c:\\節點\\sbqueues\\WebRole1**資料夾在其中建立程式範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe14e-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="fe14e-116">型別**npm 安裝 azure**在 hello 命令視窗中，這應該會導致類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="fe14e-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="fe14e-117">您可以手動執行 hello **ls**命令 tooverify， **node_modules**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe14e-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="fe14e-118">在該資料夾尋找 hello **azure**套件，其中包含需要 tooaccess 服務匯流排佇列的 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="fe14e-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="fe14e-119">匯入 hello 模組</span><span class="sxs-lookup"><span data-stu-id="fe14e-119">Import hello module</span></span>
<span data-ttu-id="fe14e-120">使用 [記事本] 或其他文字編輯器，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案：</span><span class="sxs-lookup"><span data-stu-id="fe14e-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="fe14e-121">設定 Azure 服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="fe14e-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="fe14e-122">hello Azure 模組讀取 hello 環境變數`AZURE_SERVICEBUS_CONNECTION_STRING`需要 tooconnect tooService 匯流排 tooobtain 資訊。</span><span class="sxs-lookup"><span data-stu-id="fe14e-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="fe14e-123">如果未設定這個環境變數，呼叫時，您必須指定 hello 帳戶資訊`createServiceBusService`。</span><span class="sxs-lookup"><span data-stu-id="fe14e-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="fe14e-124">如需設定 Azure 雲端服務組態檔中 hello 環境變數的範例，請參閱[Node.js 雲端服務與儲存體][Node.js Cloud Service with Storage]。</span><span class="sxs-lookup"><span data-stu-id="fe14e-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="fe14e-125">如需設定 hello hello 環境變數的範例[Azure 入口網站][ Azure portal] Azure 網站，請參閱[Node.js Web 應用程式，與儲存體][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="fe14e-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="fe14e-126">建立佇列</span><span class="sxs-lookup"><span data-stu-id="fe14e-126">Create a queue</span></span>
<span data-ttu-id="fe14e-127">hello **ServiceBusService**物件可讓您使用服務匯流排佇列 toowork。</span><span class="sxs-lookup"><span data-stu-id="fe14e-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="fe14e-128">hello 下列程式碼會建立**ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fe14e-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="fe14e-129">新增 hello hello 頂端附近**立即轉譯 server.js** hello 陳述式 tooimport hello Azure 模組之後的檔案：</span><span class="sxs-lookup"><span data-stu-id="fe14e-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="fe14e-130">藉由呼叫`createQueueIfNotExists`上 hello **ServiceBusService**物件、 hello 可讓您指定 （是否有的話），則會傳回佇列，或建立新佇列 hello 指定名稱。</span><span class="sxs-lookup"><span data-stu-id="fe14e-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="fe14e-131">hello 下列程式碼使用`createQueueIfNotExists`toocreate 或連接名為 toohello 佇列`myqueue`:</span><span class="sxs-lookup"><span data-stu-id="fe14e-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="fe14e-132">hello`createServiceBusService`方法也支援其他選項，可讓您 toooverride 預設佇列設定，例如訊息時間 toolive 或最大佇列大小。</span><span class="sxs-lookup"><span data-stu-id="fe14e-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="fe14e-133">hello 下列範例會設定 hello 最大佇列大小 too5 GB 和 1 分鐘的時間 toolive (TTL) 值：</span><span class="sxs-lookup"><span data-stu-id="fe14e-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="fe14e-134">篩選器</span><span class="sxs-lookup"><span data-stu-id="fe14e-134">Filters</span></span>
<span data-ttu-id="fe14e-135">選擇性的篩選作業可能會使用執行套用的 toooperations **ServiceBusService**。</span><span class="sxs-lookup"><span data-stu-id="fe14e-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="fe14e-136">篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：</span><span class="sxs-lookup"><span data-stu-id="fe14e-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="fe14e-137">在執行前的處理 hello 要求選項之後, 必須呼叫 hello 方法`next`，傳遞以下列簽章的 hello 回呼：</span><span class="sxs-lookup"><span data-stu-id="fe14e-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="fe14e-138">在此回呼，然後之後處理 hello `returnObject` (hello 回應 hello 要求 toohello 伺服器)，或是必須叫用回呼 hello`next`如果它存在 toocontinue 處理其他篩選器，或只會叫用`finalCallback`，結束hello 服務引動過程。</span><span class="sxs-lookup"><span data-stu-id="fe14e-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="fe14e-139">實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello`ExponentialRetryPolicyFilter`和`LinearRetryPolicyFilter`。</span><span class="sxs-lookup"><span data-stu-id="fe14e-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="fe14e-140">hello 下列程式碼會建立`ServiceBusService`物件，使用 hello `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="fe14e-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="fe14e-141">傳送訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="fe14e-141">Send messages tooa queue</span></span>
<span data-ttu-id="fe14e-142">toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`sendQueueMessage`方法上 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fe14e-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="fe14e-143">訊息太傳送 （與從接收的資料） 的服務匯流排佇列是**BrokeredMessage**物件，並有一組標準屬性 (例如**標籤**和**TimeToLive**)、字典，其中會使用的 toohold 自訂應用程式特定的屬性和任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="fe14e-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="fe14e-144">應用程式可以設定為 hello 訊息傳遞字串 hello hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="fe14e-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="fe14e-145">任何必要的標準屬性都會填入預設值。</span><span class="sxs-lookup"><span data-stu-id="fe14e-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="fe14e-146">hello 下列範例會示範如何 toosend 測試訊息 toohello 佇列名為`myqueue`使用`sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="fe14e-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="fe14e-147">服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="fe14e-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="fe14e-148">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="fe14e-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="fe14e-149">訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="fe14e-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="fe14e-150">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="fe14e-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="fe14e-151">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="fe14e-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="fe14e-152">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="fe14e-152">Receive messages from a queue</span></span>
<span data-ttu-id="fe14e-153">訊息會使用從佇列接收 hello`receiveQueueMessage`方法上 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fe14e-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="fe14e-154">根據預設，訊息會從佇列中刪除 hello 讀取。不過，您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它的設定 hello 選擇性參數 hello 佇列`isPeekLock`太**true**。</span><span class="sxs-lookup"><span data-stu-id="fe14e-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="fe14e-155">hello 讀取預設行為，而且刪除 hello 訊息，因為 hello 的一部分接收作業在 hello 最簡單的模型，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。</span><span class="sxs-lookup"><span data-stu-id="fe14e-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="fe14e-156">toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="fe14e-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="fe14e-157">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="fe14e-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="fe14e-158">如果 hello`isPeekLock`參數設定太**true**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe14e-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="fe14e-159">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe14e-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="fe14e-160">Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`deleteMessage`方法並提供 hello 訊息 toobe 刪除做為參數。</span><span class="sxs-lookup"><span data-stu-id="fe14e-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="fe14e-161">hello`deleteMessage`方法標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。</span><span class="sxs-lookup"><span data-stu-id="fe14e-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="fe14e-162">hello 下列範例會示範如何 tooreceive 和處理序訊息使用`receiveQueueMessage`。</span><span class="sxs-lookup"><span data-stu-id="fe14e-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="fe14e-163">hello 範例第一次收到和刪除的訊息，然後接收訊息，使用`isPeekLock`設定得**true**，然後刪除 hello 訊息使用`deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="fe14e-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="fe14e-164">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="fe14e-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="fe14e-165">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="fe14e-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="fe14e-166">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`方法上 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="fe14e-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="fe14e-167">這將導致服務匯流排 toounlock hello 佇列內的訊息，並讓它再次接收可用 toobe，是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="fe14e-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="fe14e-168">另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello tooprocess hello 訊息之前的應用程式失敗 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），服務匯流排會自動解除鎖定 hello 訊息，然後並將其可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="fe14e-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="fe14e-169">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="fe14e-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="fe14e-170">這通常稱為*至少一旦處理*，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="fe14e-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="fe14e-171">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="fe14e-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="fe14e-172">這通常用來達成 hello **MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。</span><span class="sxs-lookup"><span data-stu-id="fe14e-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe14e-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe14e-173">Next steps</span></span>
<span data-ttu-id="fe14e-174">toolearn 有關佇列的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="fe14e-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="fe14e-175">[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="fe14e-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="fe14e-176">GitHub 上的 [Azure SDK for Node][Azure SDK for Node] 儲存機制</span><span class="sxs-lookup"><span data-stu-id="fe14e-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="fe14e-177">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="fe14e-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
