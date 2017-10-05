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
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="75e2a-103">如何透過 Node.js 使用服務匯流排主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75e2a-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="75e2a-104">本指南說明如何從 Node.js 應用程式使用服務匯流排主題和訂閱。</span><span class="sxs-lookup"><span data-stu-id="75e2a-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="75e2a-105">涵蓋的案例包括**建立主題和訂用帳戶**、**建立訂用帳戶篩選器**、**傳送訊息至主題**、**接收訂用帳戶的訊息**，以及**刪除主題和訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="75e2a-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="75e2a-106">如需主題和訂用帳戶的詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="75e2a-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="75e2a-107">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="75e2a-107">Create a Node.js application</span></span>
<span data-ttu-id="75e2a-108">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75e2a-108">Create a blank Node.js application.</span></span> <span data-ttu-id="75e2a-109">如需有關建立 Node.js 應用程式的指示，請參閱[建立 Node.js 應用程式並將其部署到 Azure 網站]、[Node.js 雲端服務][Node.js Cloud Service] (使用 Windows PowerShell) 或使用 WebMatrix 的網站。</span><span class="sxs-lookup"><span data-stu-id="75e2a-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="75e2a-110">設定應用程式以使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="75e2a-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="75e2a-111">若要使用服務匯流排，請下載 Node.js Azure 封裝。</span><span class="sxs-lookup"><span data-stu-id="75e2a-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="75e2a-112">此封裝含有一組能與服務匯流排 REST 服務通訊的便利程式庫。</span><span class="sxs-lookup"><span data-stu-id="75e2a-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="75e2a-113">使用 Node Package Manager (NPM) 取得封裝</span><span class="sxs-lookup"><span data-stu-id="75e2a-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="75e2a-114">使用命令列介面，例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Unix)，瀏覽到您建立範例應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="75e2a-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="75e2a-115">在命令視窗中輸入 **npm install azure**，這應該會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="75e2a-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

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
3. <span data-ttu-id="75e2a-116">您可以手動執行 **ls** 命令，確認已建立 **node\_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="75e2a-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="75e2a-117">在該資料夾內找出 **azure** 封裝，其中含有存取服務匯流排主題所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="75e2a-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="75e2a-118">匯入模組</span><span class="sxs-lookup"><span data-stu-id="75e2a-118">Import the module</span></span>
<span data-ttu-id="75e2a-119">使用記事本或其他文字編輯器將以下內容新增至應用程式 **server.js** 檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="75e2a-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="75e2a-120">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="75e2a-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="75e2a-121">Azure 模組會讀取環境變數 `AZURE_SERVICEBUS_NAMESPACE` 和 `AZURE_SERVICEBUS_ACCESS_KEY`，以取得連接服務匯流排所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="75e2a-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="75e2a-122">如果未設定這些環境變數，則呼叫 `createServiceBusService` 時必須指定帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="75e2a-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="75e2a-123">如需在 Azure 雲端服務的環境變數設定範例，請參閱[使用儲存體的 Node.js 雲端服務][Node.js Cloud Service with Storage]。</span><span class="sxs-lookup"><span data-stu-id="75e2a-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="75e2a-124">如需 Azure 網站的環境變數設定範例，請參閱[使用儲存體的 Node.js Web 應用程式][Node.js Web Application with Storage]。</span><span class="sxs-lookup"><span data-stu-id="75e2a-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="75e2a-125">建立主題</span><span class="sxs-lookup"><span data-stu-id="75e2a-125">Create a topic</span></span>
<span data-ttu-id="75e2a-126">**ServiceBusService** 物件可讓您使用主題。</span><span class="sxs-lookup"><span data-stu-id="75e2a-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="75e2a-127">下列程式碼將建立 **ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="75e2a-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="75e2a-128">請將程式碼新增至 **server.js** 檔案的頂端附近，放置在匯入 azure 模型的陳述式後方：</span><span class="sxs-lookup"><span data-stu-id="75e2a-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="75e2a-129">藉由在 **ServiceBusService** 物件上呼叫 `createTopicIfNotExists`，系統將傳回指定的主題 (若有的話) 或建立具有指定名稱的新主題。</span><span class="sxs-lookup"><span data-stu-id="75e2a-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="75e2a-130">下列程式碼使用 `createTopicIfNotExists` 建立或連接至名稱為 `MyTopic` 的主題：</span><span class="sxs-lookup"><span data-stu-id="75e2a-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="75e2a-131">`createServiceBusService` 方法也支援其他選項，而可讓您覆寫訊息存留時間或主題大小上限等預設主題設定。</span><span class="sxs-lookup"><span data-stu-id="75e2a-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="75e2a-132">下列範例會將主題大小上限設為 5GB，並將存留時間設為 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="75e2a-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="75e2a-133">篩選器</span><span class="sxs-lookup"><span data-stu-id="75e2a-133">Filters</span></span>
<span data-ttu-id="75e2a-134">您可以將選用的篩選作業套用至使用 **ServiceBusService** 執行的作業。</span><span class="sxs-lookup"><span data-stu-id="75e2a-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="75e2a-135">篩選作業可包括記錄、自動重試等等。篩選器是使用簽章實作方法的物件：</span><span class="sxs-lookup"><span data-stu-id="75e2a-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="75e2a-136">對要求選項執行前置處理之後，方法會呼叫 `next`，並傳遞具有下列簽章的回呼：</span><span class="sxs-lookup"><span data-stu-id="75e2a-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="75e2a-137">在此回呼中，以及處理 `returnObject` (來自對伺服器之要求的回應) 之後，回呼需要叫用 next (如果存在) 以繼續處理其他篩選，或是改為叫用 `finalCallback` 結束服務叫用。</span><span class="sxs-lookup"><span data-stu-id="75e2a-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="75e2a-138">Azure SDK for Node.js 包含了實作重試邏輯的兩個篩選器：**ExponentialRetryPolicyFilter** 和 **LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="75e2a-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="75e2a-139">下列程式碼將建立使用 **ExponentialRetryPolicyFilter** 的 **ServiceBusService** 物件：</span><span class="sxs-lookup"><span data-stu-id="75e2a-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="75e2a-140">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75e2a-140">Create subscriptions</span></span>
<span data-ttu-id="75e2a-141">**ServiceBusService** 物件也能用來建立主題訂閱。</span><span class="sxs-lookup"><span data-stu-id="75e2a-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="75e2a-142">訂閱是具名的，它們能擁有選用的篩選器，以限制傳遞至訂閱之虛擬佇列的訊息集合。</span><span class="sxs-lookup"><span data-stu-id="75e2a-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="75e2a-143">訂用帳戶是持續性的，它們會持續存在，直到本身或相關的主題遭到刪除為止。</span><span class="sxs-lookup"><span data-stu-id="75e2a-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="75e2a-144">如果應用程式含有建立訂用帳戶的邏輯，它應該會先使用 `getSubscription` 方法檢查訂用帳戶是否存在。</span><span class="sxs-lookup"><span data-stu-id="75e2a-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="75e2a-145">使用預設 (MatchAll) 篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75e2a-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="75e2a-146">如果在建立新的訂用帳戶時沒有指定篩選器，**MatchAll** 篩選器就會是預設使用的篩選器。</span><span class="sxs-lookup"><span data-stu-id="75e2a-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="75e2a-147">使用 **MatchAll** 篩選器時，所有發佈至主題的訊息都會被置於訂用帳戶的虛擬佇列中。</span><span class="sxs-lookup"><span data-stu-id="75e2a-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="75e2a-148">下列範例將建立名為「AllMessages」的訂用帳戶，並使用預設的 **MatchAll** 篩選器。</span><span class="sxs-lookup"><span data-stu-id="75e2a-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="75e2a-149">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75e2a-149">Create subscriptions with filters</span></span>
<span data-ttu-id="75e2a-150">您也可以建立篩選器，讓您界定傳送至主題的哪些訊息應出現在特定主題訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="75e2a-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="75e2a-151">訂用帳戶所支援的最具彈性篩選器類型是實作 SQL92 子集的 **SqlFilter**。</span><span class="sxs-lookup"><span data-stu-id="75e2a-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="75e2a-152">SQL 篩選器會對發佈至主題之訊息的屬性運作。</span><span class="sxs-lookup"><span data-stu-id="75e2a-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="75e2a-153">如需有關可與 SQL 篩選器搭配使用的運算式詳細資料，請檢閱 [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 語法。</span><span class="sxs-lookup"><span data-stu-id="75e2a-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="75e2a-154">您可以使用 **ServiceBusService** 物件的 `createRule` 方法將篩選器新增至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="75e2a-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="75e2a-155">此方法可讓您將篩選器新增至現有的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="75e2a-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="75e2a-156">由於預設篩選器會自動套用至所有新的訂用帳戶，因此您必須先移除預設篩選器，否則 **MatchAll** 將會覆寫您指定的任何其他篩選器。</span><span class="sxs-lookup"><span data-stu-id="75e2a-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="75e2a-157">您可以使用 **ServiceBusService** 物件的 `deleteRule` 方法移除預設規則。</span><span class="sxs-lookup"><span data-stu-id="75e2a-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="75e2a-158">以下範例將建立名為 `HighMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取自訂 `messagenumber` 屬性大於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="75e2a-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="75e2a-159">同樣地，下列範例將建立名為 `LowMessages` 的訂用帳戶，而且所含的 **SqlFilter** 只會選取 `messagenumber` 屬性小於或等於 3 的訊息：</span><span class="sxs-lookup"><span data-stu-id="75e2a-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

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

<span data-ttu-id="75e2a-160">當訊息傳送至 `MyTopic` 時，一律會將該訊息傳遞至已訂閱 `AllMessages` 主題訂用帳戶的接收者，並選擇性地傳遞至已訂閱 `HighMessages` 和 `LowMessages` 主題訂用帳戶的接收者 (視訊息內容而定)。</span><span class="sxs-lookup"><span data-stu-id="75e2a-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="75e2a-161">如何將訊息傳送至主題</span><span class="sxs-lookup"><span data-stu-id="75e2a-161">How to send messages to a topic</span></span>
<span data-ttu-id="75e2a-162">若要將訊息傳送至服務匯流排主題，應用程式必須使用 **ServiceBusService** 物件的 `sendTopicMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="75e2a-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="75e2a-163">傳送至服務匯流排主題的訊息是 **BrokeredMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="75e2a-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="75e2a-164">**BrokeredMessage** 物件具有一組標準屬性 (例如 `Label` 和 `TimeToLive`)、一個用來保存自訂應用程式特定屬性的字典，以及一堆字串資料。</span><span class="sxs-lookup"><span data-stu-id="75e2a-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="75e2a-165">應用程式能將字串值傳遞至 `sendTopicMessage` 以設定訊息本文，系統會將預設值填入任何需要的標準屬性中。</span><span class="sxs-lookup"><span data-stu-id="75e2a-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="75e2a-166">下列範例說明如何將五個測試訊息傳送至 `MyTopic`。</span><span class="sxs-lookup"><span data-stu-id="75e2a-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="75e2a-167">請注意，迴圈反覆運算上每個訊息的`messagenumber` 屬性值會有變化 (這可判斷接收訊息的訂用帳戶為何)：</span><span class="sxs-lookup"><span data-stu-id="75e2a-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="75e2a-168">服務匯流排主題支援的訊息大小上限：在[標準層](service-bus-premium-messaging.md)中為 256 KB 以及在[進階層](service-bus-premium-messaging.md)中為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="75e2a-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="75e2a-169">標頭 (包含標準和自訂應用程式屬性) 可以容納 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="75e2a-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="75e2a-170">主題中所保存的訊息數目沒有限制，但主題所保存的訊息大小總計會有最高限制。</span><span class="sxs-lookup"><span data-stu-id="75e2a-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="75e2a-171">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="75e2a-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="75e2a-172">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="75e2a-172">Receive messages from a subscription</span></span>
<span data-ttu-id="75e2a-173">對於 **ServiceBusService** 物件使用 `receiveSubscriptionMessage` 方法即可從訂用帳戶接收訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="75e2a-174">依預設，當您讀取訊息後，系統便會從訂用帳戶刪除訊息，不過您可以將選用參數 `isPeekLock` 設定為 **true**，藉此讀取 (查看) 並鎖定訊息，避免從訂用帳戶中刪除訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="75e2a-175">隨著接收作業讀取及刪除訊息之預設行為是最簡單的模型，且最適合可容許在發生失敗時不處理訊息的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="75e2a-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="75e2a-176">若要了解這一點，請考慮取用者發出接收要求，接著系統在處理此要求之前當機的案例。</span><span class="sxs-lookup"><span data-stu-id="75e2a-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="75e2a-177">因為服務匯流排會將訊息標示為已取用，當應用程式重新啟動並開始重新取用訊息時，它將會遺漏當機前已取用的訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="75e2a-178">如果您將 `isPeekLock` 參數設為 **true**，接收會變成兩階段作業，因此可以支援無法容許遺漏訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="75e2a-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="75e2a-179">當服務匯流排收到要求時，它會尋找要取用的下一個訊息、將其鎖定以防止其他取用者接收此訊息，然後將它傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="75e2a-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="75e2a-180">在應用程式完成處理訊息 (或可靠地儲存此訊息以供未來處理) 之後，它可透過呼叫 **deleteMessage** 方法和以參數形式提供要刪除的訊息，完成接收程序的第二個階段。</span><span class="sxs-lookup"><span data-stu-id="75e2a-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="75e2a-181">**deleteMessage** 方法會將訊息標示為已取用，並將其自訂用帳戶移除。</span><span class="sxs-lookup"><span data-stu-id="75e2a-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="75e2a-182">以下範例將示範如何使用預設的 `receiveSubscriptionMessage` 模式來接收與處理訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="75e2a-183">此範例會先接收來自 'LowMessages' 訂閱的訊息並加以刪除，然後再使用設定為 true 的 `isPeekLock` 接收來自 'HighMessages' 訂用帳戶的訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="75e2a-184">接著再使用 `deleteMessage` 刪除訊息：</span><span class="sxs-lookup"><span data-stu-id="75e2a-184">It then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="75e2a-185">如何處理應用程式當機與無法讀取的訊息</span><span class="sxs-lookup"><span data-stu-id="75e2a-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="75e2a-186">服務匯流排提供一種功能，可協助您從應用程式的錯誤或處理訊息的問題中順利復原。</span><span class="sxs-lookup"><span data-stu-id="75e2a-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="75e2a-187">如果接收者應用程式因為某些原因無法處理訊息，它可以呼叫 **ServiceBusService** 物件上的 `unlockMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="75e2a-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="75e2a-188">這將導致服務匯流排將訂用帳戶中的訊息解除鎖定，讓此訊息可以被相同取用應用程式或其他取用應用程式重新接收。</span><span class="sxs-lookup"><span data-stu-id="75e2a-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="75e2a-189">與在訂閱內鎖定訊息相關的還有逾時，如果應用程式無法在鎖定逾時到期之前處理訊息 (例如，如果應用程式當機)，則服務匯流排會自動解除鎖定訊息，並讓訊息可以被重新接收。</span><span class="sxs-lookup"><span data-stu-id="75e2a-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="75e2a-190">如果應用程式在處理訊息之後，尚未呼叫 `deleteMessage` 方法時當機，則會在應用程式重新啟動時將訊息重新傳遞給該應用程式。</span><span class="sxs-lookup"><span data-stu-id="75e2a-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="75e2a-191">這通常稱為*至少處理一次*，也就是說，每個訊息至少會被處理一次，但在特定狀況下，可能會重新傳遞相同訊息。</span><span class="sxs-lookup"><span data-stu-id="75e2a-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="75e2a-192">如果案例無法容許重複處理，則應用程式開發人員應在其應用程式中加入其他邏輯，以處理重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="75e2a-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="75e2a-193">通常您可使用訊息的 **MessageId** 屬性來達到此目的，該屬性將在各個傳遞嘗試中會保持不變。</span><span class="sxs-lookup"><span data-stu-id="75e2a-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="75e2a-194">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75e2a-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="75e2a-195">主題和訂用帳戶是持續性的，您必須透過 [Azure 入口網站][Azure portal]或以程式設計方式明確地刪除它們。</span><span class="sxs-lookup"><span data-stu-id="75e2a-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="75e2a-196">下列範例示範如何刪除名為 `MyTopic` 的主題：</span><span class="sxs-lookup"><span data-stu-id="75e2a-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="75e2a-197">刪除主題也將會刪除對主題註冊的任何訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="75e2a-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="75e2a-198">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="75e2a-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="75e2a-199">下列範例示範如何從 `MyTopic` 主題刪除名為 `HighMessages` 的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="75e2a-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="75e2a-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75e2a-200">Next Steps</span></span>
<span data-ttu-id="75e2a-201">了解基本的服務匯流排主題之後，請參考下列連結以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="75e2a-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="75e2a-202">請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。</span><span class="sxs-lookup"><span data-stu-id="75e2a-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="75e2a-203">[SqlFilter][SqlFilter] 的 API 參考資料。</span><span class="sxs-lookup"><span data-stu-id="75e2a-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="75e2a-204">瀏覽 GitHub 上的 [Azure SDK for Node][Azure SDK for Node] 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="75e2a-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[建立 Node.js 應用程式並將其部署到 Azure 網站]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
