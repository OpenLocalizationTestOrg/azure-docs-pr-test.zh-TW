---
title: "如何使用 Node.js 中的服務匯流排佇列 | Microsoft Docs"
description: "了解如何從 Node.js 應用程式，在 Azure 中使用服務匯流排佇列。"
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
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="ce3f2-103">如何將服務匯流排佇列搭配 Node.js 使用</span><span class="sxs-lookup"><span data-stu-id="ce3f2-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="ce3f2-104">本文說明如何將服務匯流排佇列搭配 Node.js 使用。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="ce3f2-105">這些範例均以 JavaScript 撰寫並使用 Node.js Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="ce3f2-106">本文說明的案例包括**建立佇列**、**傳送並接收訊息**，以及**刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="ce3f2-107">如需佇列的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="ce3f2-108">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="ce3f2-108">Create a Node.js application</span></span>
<span data-ttu-id="ce3f2-109">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-109">Create a blank Node.js application.</span></span> <span data-ttu-id="ce3f2-110">如需有關建立 Node.js 應用程式的指示，請參閱[建立 Node.js 應用程式並將其部署到 Azure 網站][Create and deploy a Node.js application to an Azure Website]或 [Node.js 雲端服務][Node.js Cloud Service] (使用 Windows PowerShell)。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="ce3f2-111">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="ce3f2-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="ce3f2-112">若要使用 Azure 服務匯流排，請下載及使用 Node.js Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="ce3f2-113">此封裝含有一組能與服務匯流排 REST 服務通訊的便利程式庫。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="ce3f2-114">使用 Node Package Manager (NPM) 取得封裝</span><span class="sxs-lookup"><span data-stu-id="ce3f2-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="ce3f2-115">使用 **Windows PowerShell for Node.js** 命令視窗巡覽至已建立範例應用程式的 **c:\\node\\sbqueues\\WebRole1** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="ce3f2-116">在命令視窗中輸入 **npm install azure**，這應該會產生類似下列內容的輸出：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

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
3. <span data-ttu-id="ce3f2-117">您可以手動執行 **ls** 命令，確認已建立 **node_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="ce3f2-118">在該資料夾內找到 **azure** 封裝，其中包含您存取服務匯流排佇列所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="ce3f2-119">匯入模組</span><span class="sxs-lookup"><span data-stu-id="ce3f2-119">Import the module</span></span>
<span data-ttu-id="ce3f2-120">使用記事本或其他文字編輯器將以下內容新增至應用程式 **server.js** 檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="ce3f2-121">設定 Azure 服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="ce3f2-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="ce3f2-122">Azure 模組會讀取環境變數 `AZURE_SERVICEBUS_CONNECTION_STRING`，以取得連接服務匯流排所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="ce3f2-123">如未設定此環境變數，必須在呼叫 `createServiceBusService` 時指定帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="ce3f2-124">如需在「Azure 雲端服務」組態檔中設定環境變數的範例，請參閱[使用儲存體的 Node.js 雲端服務][Node.js Cloud Service with Storage]。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="ce3f2-125">如需在 [Azure 入口網站][Azure portal]中設定 Azure 網站環境變數的範例，請參閱[使用儲存體的 Node.js Web 應用程式][Node.js Web Application with Storage]。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="ce3f2-126">建立佇列</span><span class="sxs-lookup"><span data-stu-id="ce3f2-126">Create a queue</span></span>
<span data-ttu-id="ce3f2-127">**ServiceBusService** 物件可讓您使用服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="ce3f2-128">下列程式碼將建立 **ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="ce3f2-129">請將程式碼新增至 **server.js** 檔案的頂端附近，放置在匯入 Azure 模型的陳述式後方：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="ce3f2-130">呼叫 **ServiceBusService** 物件上的 `createQueueIfNotExists` 之後，會傳回指定的佇列 (如果存在)，或以指定的名稱建立新的佇列。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="ce3f2-131">下列程式碼使用 `createQueueIfNotExists` 建立或連接至名稱為 `myqueue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="ce3f2-132">`createServiceBusService` 方法也支援其他選項，而可讓您覆寫訊息存留時間或佇列大小上限等預設佇列設定。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="ce3f2-133">下列範例會將佇列大小上限設為 5 GB，並將存留時間 (TTL) 值設為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="ce3f2-134">篩選器</span><span class="sxs-lookup"><span data-stu-id="ce3f2-134">Filters</span></span>
<span data-ttu-id="ce3f2-135">您可以將選用的篩選作業套用至使用 **ServiceBusService** 執行的作業。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="ce3f2-136">篩選作業可包括記錄、自動重試等等。篩選器是以簽章實作方法的物件：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="ce3f2-137">在對要求選項進行前處理之後，方法必須呼叫 `next`，並傳遞具有下列簽章的回呼：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="ce3f2-138">在此回呼中，以及處理 `returnObject` (來自對伺服器之要求的回應) 之後，回呼必須叫用 `next` (如果存在) 以繼續處理其他篩選器，或是直接叫用 `finalCallback` 結束服務叫用。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="ce3f2-139">Azure SDK for Node.js 包含了兩個實作重試邏輯的篩選器： `ExponentialRetryPolicyFilter` 與 `LinearRetryPolicyFilter`。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="ce3f2-140">下列程式碼會建立使用 `ExponentialRetryPolicyFilter` 的 `ServiceBusService` 物件：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="ce3f2-141">傳送訊息至佇列</span><span class="sxs-lookup"><span data-stu-id="ce3f2-141">Send messages to a queue</span></span>
<span data-ttu-id="ce3f2-142">若要傳送訊息至服務匯流排佇列，應用程式將呼叫 **ServiceBusService** 物件上的 `sendQueueMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="ce3f2-143">傳送至服務匯排流 (以及服務匯流排接收) 的佇列是 **BrokeredMessage** 物件，而且具有一組標準屬性 (例如 **Label** 和 **TimeToLive**)、一個用來保存自訂應用程式特定屬性的字典，以及任意應用程式資料的主體。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="ce3f2-144">應用程式可將字串做為訊息傳遞來設定訊息的內文。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="ce3f2-145">任何必要的標準屬性都會填入預設值。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="ce3f2-146">下列範例示範如何使用 `sendQueueMessage` 將測試訊息傳送至名為 `myqueue` 的佇列：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="ce3f2-147">服務匯流排佇列支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ce3f2-148">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ce3f2-149">佇列中所保存的訊息數目沒有限制，但佇列所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="ce3f2-150">此佇列大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="ce3f2-151">如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="ce3f2-152">從佇列接收訊息</span><span class="sxs-lookup"><span data-stu-id="ce3f2-152">Receive messages from a queue</span></span>
<span data-ttu-id="ce3f2-153">對於 **ServiceBusService** 物件使用 `receiveQueueMessage` 方法即可從佇列接收訊息。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="ce3f2-154">預設會從佇列刪除唯讀的訊息，不過，您可以將 `isPeekLock` 設定為 **true**，不需要從佇列刪除訊息，即可讀取 (查看) 並鎖定訊息。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="ce3f2-155">隨著接收作業讀取及刪除訊息之預設行為是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="ce3f2-156">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="ce3f2-157">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="ce3f2-158">如果您將 `isPeekLock` 參數設為 **true**，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ce3f2-159">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="ce3f2-160">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫 `deleteMessage` 方法和以參數形式提供要刪除的訊息，完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="ce3f2-161">`deleteMessage` 方法會將訊息標示為已取用，並將其從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="ce3f2-162">下列範例示範如何使用 `receiveQueueMessage` 來接收和處理訊息。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="ce3f2-163">範例首先會接收並刪除訊息，然後使用設定為 **true** 的 `isPeekLock` 接收訊息，接著使用 `deleteMessage` 刪除訊息：</span><span class="sxs-lookup"><span data-stu-id="ce3f2-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ce3f2-164">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="ce3f2-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ce3f2-165">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ce3f2-166">如果接收者應用程式因為某些原因無法處理訊息，它可以呼叫 **ServiceBusService** 物件上的 `unlockMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="ce3f2-167">這將導致服務匯流排將佇列中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ce3f2-168">與在佇列內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排將自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="ce3f2-169">如果應用程式在處理訊息之後，尚未呼叫 `deleteMessage` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="ce3f2-170">這通常稱為*至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="ce3f2-171">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="ce3f2-172">通常您可使用訊息的 **MessageId** 屬性來達到此目的，該屬性將在各個傳遞嘗試中會保持不變。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce3f2-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce3f2-173">Next steps</span></span>
<span data-ttu-id="ce3f2-174">若要深入了解佇列，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="ce3f2-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="ce3f2-175">[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="ce3f2-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="ce3f2-176">GitHub 上的 [Azure SDK for Node][Azure SDK for Node] 儲存機制</span><span class="sxs-lookup"><span data-stu-id="ce3f2-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="ce3f2-177">Node.js 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="ce3f2-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
