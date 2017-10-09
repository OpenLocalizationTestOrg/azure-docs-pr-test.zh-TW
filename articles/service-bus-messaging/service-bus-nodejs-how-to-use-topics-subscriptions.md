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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="10cdd-103">如何 tooUse Service Bus 主題和訂閱以 Node.js</span><span class="sxs-lookup"><span data-stu-id="10cdd-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="10cdd-104">本指南說明如何 toouse Service Bus 主題和訂閱從 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10cdd-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="10cdd-105">hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息**tooa 主題**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。</span><span class="sxs-lookup"><span data-stu-id="10cdd-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="10cdd-106">如需主題和訂閱的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="10cdd-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="10cdd-107">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="10cdd-107">Create a Node.js application</span></span>
<span data-ttu-id="10cdd-108">建立空白的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10cdd-108">Create a blank Node.js application.</span></span> <span data-ttu-id="10cdd-109">如需建立 Node.js 應用程式的指示，請參閱[建立和部署 Azure 網站 Node.js 應用程式 tooan]， [Node.js 雲端服務][ Node.js Cloud Service]使用 WindowsPowerShell 中或使用 WebMatrix 的網站。</span><span class="sxs-lookup"><span data-stu-id="10cdd-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="10cdd-110">設定您的應用程式 toouse 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="10cdd-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="10cdd-111">服務匯流排 toouse 下載 hello Node.js 的 Azure 套件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="10cdd-112">此套件包含一組與 hello 服務匯流排 REST 服務通訊的程式庫。</span><span class="sxs-lookup"><span data-stu-id="10cdd-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="10cdd-113">使用節點封裝管理員 (NPM) tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="10cdd-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="10cdd-114">使用命令列介面，例如**PowerShell** (Windows，)**終端機**(Mac，) 或**撞**(Unix)，瀏覽 toohello 資料夾建立範例應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="10cdd-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="10cdd-115">型別**npm 安裝 azure**在 hello 命令視窗中，這應該會導致 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="10cdd-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="10cdd-116">您可以手動執行 hello **ls**命令 tooverify，**節點\_模組**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="10cdd-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="10cdd-117">在該資料夾內尋找**azure**套件，其中包含需要 tooaccess Service Bus 主題 hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="10cdd-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="10cdd-118">匯入 hello 模組</span><span class="sxs-lookup"><span data-stu-id="10cdd-118">Import hello module</span></span>
<span data-ttu-id="10cdd-119">使用 [記事本] 或其他文字編輯器，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案：</span><span class="sxs-lookup"><span data-stu-id="10cdd-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="10cdd-120">設定服務匯流排連接</span><span class="sxs-lookup"><span data-stu-id="10cdd-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="10cdd-121">hello Azure 模組會讀取 hello 環境變數`AZURE_SERVICEBUS_NAMESPACE`和`AZURE_SERVICEBUS_ACCESS_KEY`資訊所需 tooconnect tooService 匯流排。</span><span class="sxs-lookup"><span data-stu-id="10cdd-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="10cdd-122">如果未設定這些環境變數，呼叫時，您必須指定 hello 帳戶資訊`createServiceBusService`。</span><span class="sxs-lookup"><span data-stu-id="10cdd-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="10cdd-123">如需設定 Azure 雲端服務的 hello 環境變數的範例，請參閱[Node.js 雲端服務與儲存體][Node.js Cloud Service with Storage]。</span><span class="sxs-lookup"><span data-stu-id="10cdd-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="10cdd-124">如需設定 Azure 網站的 hello 環境變數的範例，請參閱[Node.js Web 應用程式，與儲存體][Node.js Web Application with Storage]。</span><span class="sxs-lookup"><span data-stu-id="10cdd-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="10cdd-125">建立主題</span><span class="sxs-lookup"><span data-stu-id="10cdd-125">Create a topic</span></span>
<span data-ttu-id="10cdd-126">hello **ServiceBusService**物件可讓您 toowork 與主題。</span><span class="sxs-lookup"><span data-stu-id="10cdd-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="10cdd-127">下列程式碼將建立 **ServiceBusService** 物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="10cdd-128">將最上方的 hello**立即轉譯 server.js** hello 陳述式 tooimport hello azure 模組之後的檔案：</span><span class="sxs-lookup"><span data-stu-id="10cdd-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="10cdd-129">藉由呼叫`createTopicIfNotExists`上 hello **ServiceBusService**物件、 hello 指定 （是否存在的話，），就會傳回主題，或將會建立新主題與 hello 指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="10cdd-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="10cdd-130">hello 下列程式碼使用`createTopicIfNotExists`toocreate 或連接具名 toohello 主題`MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="10cdd-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="10cdd-131">hello`createServiceBusService`方法也支援其他選項，可讓您 toooverride 預設主題設定，例如訊息存留時間或主題大小上限。</span><span class="sxs-lookup"><span data-stu-id="10cdd-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="10cdd-132">hello 下列範例會設定具有時間 hello 最大主題大小 too5GB toolive 1 分鐘：</span><span class="sxs-lookup"><span data-stu-id="10cdd-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="10cdd-133">篩選器</span><span class="sxs-lookup"><span data-stu-id="10cdd-133">Filters</span></span>
<span data-ttu-id="10cdd-134">選擇性的篩選作業可能會使用執行套用的 toooperations **ServiceBusService**。</span><span class="sxs-lookup"><span data-stu-id="10cdd-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="10cdd-135">篩選作業可包括記錄、自動重試等等。篩選器是實作 hello 簽章的方法的物件：</span><span class="sxs-lookup"><span data-stu-id="10cdd-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="10cdd-136">執行前置處理 hello 要求選項之後, hello 方法呼叫`next`，將回呼傳遞具有下列簽章的 hello:</span><span class="sxs-lookup"><span data-stu-id="10cdd-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="10cdd-137">在此回呼，然後之後處理 hello `returnObject` (hello 回應 hello 要求 toohello 伺服器)，hello 回呼需要 tooeither 如果它存在 toocontinue 處理其他篩選器接著叫用，或叫用`finalCallback`否則 tooend hello叫用服務。</span><span class="sxs-lookup"><span data-stu-id="10cdd-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="10cdd-138">實作重試邏輯的兩個篩選器隨附於 Azure SDK for Node.js hello **ExponentialRetryPolicyFilter**和**LinearRetryPolicyFilter**。</span><span class="sxs-lookup"><span data-stu-id="10cdd-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="10cdd-139">hello 下列範例會建立**ServiceBusService**物件，使用 hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="10cdd-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="10cdd-140">建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10cdd-140">Create subscriptions</span></span>
<span data-ttu-id="10cdd-141">主題訂用帳戶也會建立以 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="10cdd-142">訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="10cdd-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="10cdd-143">訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題它們相關聯，則會被刪除。</span><span class="sxs-lookup"><span data-stu-id="10cdd-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="10cdd-144">如果您的應用程式包含邏輯 toocreate 訂用帳戶，它應該先查看 hello 訂用帳戶已經有使用`getSubscription`方法。</span><span class="sxs-lookup"><span data-stu-id="10cdd-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="10cdd-145">建立訂用帳戶與 hello 預設 (MatchAll) 篩選器</span><span class="sxs-lookup"><span data-stu-id="10cdd-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="10cdd-146">hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="10cdd-147">當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題會放在訂用帳戶的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="10cdd-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="10cdd-148">hello 下列範例會建立名為 'AllMessages' 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。</span><span class="sxs-lookup"><span data-stu-id="10cdd-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="10cdd-149">使用篩選器建立訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10cdd-149">Create subscriptions with filters</span></span>
<span data-ttu-id="10cdd-150">您也可以建立篩選器可讓您 tooscope tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="10cdd-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="10cdd-151">hello 最有彈性的訂用帳戶支援的篩選器的類型是**SqlFilter**，它會實作 SQL92 的子集。</span><span class="sxs-lookup"><span data-stu-id="10cdd-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="10cdd-152">SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="10cdd-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="10cdd-153">如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。</span><span class="sxs-lookup"><span data-stu-id="10cdd-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="10cdd-154">加入篩選條件可以 tooa 訂用帳戶使用 hello`createRule`方法 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="10cdd-155">這個方法可讓您將加入新篩選 tooan 現有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="10cdd-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="10cdd-156">因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器或**MatchAll**將會覆寫任何其他您可以指定的篩選器。</span><span class="sxs-lookup"><span data-stu-id="10cdd-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="10cdd-157">您可以藉由使用 hello 移除 hello 預設規則`deleteRule`方法**ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="10cdd-158">hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`messagenumber`大於 3 的屬性：</span><span class="sxs-lookup"><span data-stu-id="10cdd-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="10cdd-159">同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與**SqlFilter**只選取有訊息`messagenumber`屬性小於或等於 too3:</span><span class="sxs-lookup"><span data-stu-id="10cdd-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="10cdd-160">當訊息現在是否傳送太`MyTopic`，它會一律會將傳遞至訂閱的接收者 toohello`AllMessages`主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`主題訂用帳戶（視 hello 訊息內容）。</span><span class="sxs-lookup"><span data-stu-id="10cdd-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="10cdd-161">如何 toosend 訊息 tooa 主題</span><span class="sxs-lookup"><span data-stu-id="10cdd-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="10cdd-162">toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用`sendTopicMessage`方法 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="10cdd-163">訊息傳送 tooService 匯流排主題**BrokeredMessage**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="10cdd-164">**BrokeredMessage**物件具有一組標準屬性 (例如`Label`和`TimeToLive`) 的字典，其中使用的 toohold 自訂應用程式特定屬性，和字串資料的主體。</span><span class="sxs-lookup"><span data-stu-id="10cdd-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="10cdd-165">應用程式可以將字串值傳遞至 hello 設定 hello hello 訊息本文`sendTopicMessage`和任何所需的標準屬性將會填入預設值。</span><span class="sxs-lookup"><span data-stu-id="10cdd-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="10cdd-166">hello 下列範例會示範 toosend 如何在五個測試訊息至`MyTopic`。</span><span class="sxs-lookup"><span data-stu-id="10cdd-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="10cdd-167">請注意該 hello `messagenumber` hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：</span><span class="sxs-lookup"><span data-stu-id="10cdd-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="10cdd-168">服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="10cdd-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="10cdd-169">hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="10cdd-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="10cdd-170">訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。</span><span class="sxs-lookup"><span data-stu-id="10cdd-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="10cdd-171">此主題大小會在建立時定義，上限是 5 GB。</span><span class="sxs-lookup"><span data-stu-id="10cdd-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="10cdd-172">自訂用帳戶接收訊息</span><span class="sxs-lookup"><span data-stu-id="10cdd-172">Receive messages from a subscription</span></span>
<span data-ttu-id="10cdd-173">訊息會從訂用帳戶使用接收`receiveSubscriptionMessage`方法上 hello **ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="10cdd-174">根據預設，訊息會刪除 hello 訂用帳戶的讀取。不過，您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它從 hello 訂用帳戶所設定 hello 選擇性參數`isPeekLock`太**true**。</span><span class="sxs-lookup"><span data-stu-id="10cdd-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="10cdd-175">hello 讀取及刪除 hello 訊息，接收作業的一部分是 hello 簡單的模式，以及應用程式可以容許不處理中失敗的 hello 事件訊息的案例是最適合的預設行為。</span><span class="sxs-lookup"><span data-stu-id="10cdd-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="10cdd-176">toounderstand，假設取用者問題 hello 接收要求，而後再處理它。</span><span class="sxs-lookup"><span data-stu-id="10cdd-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="10cdd-177">服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。</span><span class="sxs-lookup"><span data-stu-id="10cdd-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="10cdd-178">如果 hello`isPeekLock`參數設定太**true**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10cdd-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="10cdd-179">服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10cdd-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="10cdd-180">藉由呼叫 hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理） 之後，完成接收程序 hello 第二個階段**deleteMessage**方法並提供訊息 toobe刪除做為參數。</span><span class="sxs-lookup"><span data-stu-id="10cdd-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="10cdd-181">hello **deleteMessage**方法會標示為正在使用的 hello 訊息，並移除從 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="10cdd-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="10cdd-182">hello 下列範例示範如何可以接收和處理使用`receiveSubscriptionMessage`。</span><span class="sxs-lookup"><span data-stu-id="10cdd-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="10cdd-183">hello 範例第一次收到並刪除 hello 'LowMessages' 訂用帳戶中的訊息，然後將訊息從接收 hello 'HighMessages' 訂用帳戶使用`isPeekLock`設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="10cdd-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="10cdd-184">然後刪除 hello 訊息使用`deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="10cdd-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="10cdd-185">Toohandle 應用程式的當機，而且無法讀取訊息</span><span class="sxs-lookup"><span data-stu-id="10cdd-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="10cdd-186">服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。</span><span class="sxs-lookup"><span data-stu-id="10cdd-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="10cdd-187">如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlockMessage`方法**ServiceBusService**物件。</span><span class="sxs-lookup"><span data-stu-id="10cdd-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="10cdd-188">這將導致服務匯流排 toounlock hello 訂用帳戶內的訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="10cdd-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="10cdd-189">也是在訂閱中，鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），則服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。</span><span class="sxs-lookup"><span data-stu-id="10cdd-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="10cdd-190">在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`deleteMessage`呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。</span><span class="sxs-lookup"><span data-stu-id="10cdd-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="10cdd-191">這通常稱為*至少一旦處理*，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="10cdd-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="10cdd-192">如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。</span><span class="sxs-lookup"><span data-stu-id="10cdd-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="10cdd-193">這通常用來達成**MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。</span><span class="sxs-lookup"><span data-stu-id="10cdd-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="10cdd-194">刪除主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10cdd-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="10cdd-195">主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="10cdd-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="10cdd-196">hello 下列範例會示範如何命名 toodelete hello 主題`MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="10cdd-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="10cdd-197">刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="10cdd-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="10cdd-198">您也可以個別刪除訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="10cdd-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="10cdd-199">下列範例示範如何 toodelete 訂用帳戶命名`HighMessages`從 hello`MyTopic`主題：</span><span class="sxs-lookup"><span data-stu-id="10cdd-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="10cdd-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10cdd-200">Next Steps</span></span>
<span data-ttu-id="10cdd-201">現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="10cdd-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="10cdd-202">請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。</span><span class="sxs-lookup"><span data-stu-id="10cdd-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="10cdd-203">[SqlFilter][SqlFilter] 的 API 參考資料。</span><span class="sxs-lookup"><span data-stu-id="10cdd-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="10cdd-204">請瀏覽 hello [Azure SDK for 節點][ Azure SDK for Node] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="10cdd-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[建立和部署 Azure 網站 Node.js 應用程式 tooan]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
