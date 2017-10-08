---
title: "aaaAzure 函式佇列儲存體繫結 |Microsoft 文件"
description: "了解觸發 toouse Azure 儲存體的方式，在 Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="40513-104">Azure Functions 佇列儲存體繫結</span><span class="sxs-lookup"><span data-stu-id="40513-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="40513-105">本文說明如何 tooconfigure 和程式碼 Azure 佇列儲存體中的繫結 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="40513-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="40513-106">Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="40513-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="40513-107">如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="40513-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="40513-108">佇列儲存體觸發程序</span><span class="sxs-lookup"><span data-stu-id="40513-108">Queue storage trigger</span></span>
<span data-ttu-id="40513-109">hello Azure 佇列儲存體觸發程序可讓 toomonitor 新郵件佇列儲存體，並反應 toothem。</span><span class="sxs-lookup"><span data-stu-id="40513-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="40513-110">定義佇列觸發程序使用 hello**整合**hello 函式的入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="40513-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="40513-111">hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:</span><span class="sxs-lookup"><span data-stu-id="40513-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="40513-112">hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="40513-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="40513-113">Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="40513-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="40513-114">其他設定可以提供在[host.json 檔案](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)toofurther 微調佇列儲存體觸發程序。</span><span class="sxs-lookup"><span data-stu-id="40513-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="40513-115">例如，您可以變更 host.json hello 佇列輪詢間隔。</span><span class="sxs-lookup"><span data-stu-id="40513-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="40513-116">使用佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="40513-116">Using a queue trigger</span></span>
<span data-ttu-id="40513-117">在 Node.js 函式，存取 hello 佇列資料使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="40513-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="40513-118">在.NET 函式，存取 使用下列方法參數的 hello 佇列裝載`CloudQueueMessage paramName`。</span><span class="sxs-lookup"><span data-stu-id="40513-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="40513-119">在這裡，`paramName`是您在 hello 中指定的 hello 值[觸發程序組態](#trigger)。</span><span class="sxs-lookup"><span data-stu-id="40513-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="40513-120">hello 佇列訊息可以是 hello 的下列類型的已還原序列化的 tooany:</span><span class="sxs-lookup"><span data-stu-id="40513-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="40513-121">POCO 物件。</span><span class="sxs-lookup"><span data-stu-id="40513-121">POCO object.</span></span> <span data-ttu-id="40513-122">如果 hello 佇列裝載為 JSON 物件，使用。</span><span class="sxs-lookup"><span data-stu-id="40513-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="40513-123">hello 函式執行階段會還原序列化成 hello POCO 物件 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="40513-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="40513-124">佇列觸發程序中繼資料</span><span class="sxs-lookup"><span data-stu-id="40513-124">Queue trigger metadata</span></span>
<span data-ttu-id="40513-125">hello 佇列觸發程序會提供數個中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="40513-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="40513-126">這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。</span><span class="sxs-lookup"><span data-stu-id="40513-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="40513-127">hello 值有 hello 相同的語意[ `CloudQueueMessage` ]。</span><span class="sxs-lookup"><span data-stu-id="40513-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="40513-128">**QueueTrigger** - 佇列承載 (如果為有效字串)</span><span class="sxs-lookup"><span data-stu-id="40513-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="40513-129">**DequeueCount** - 鍵入 `int`。</span><span class="sxs-lookup"><span data-stu-id="40513-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="40513-130">hello 的此訊息清除佇列的次數。</span><span class="sxs-lookup"><span data-stu-id="40513-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="40513-131">**ExpirationTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="40513-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="40513-132">hello 時間該 hello 訊息過期。</span><span class="sxs-lookup"><span data-stu-id="40513-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="40513-133">**Id** - 鍵入 `string`。</span><span class="sxs-lookup"><span data-stu-id="40513-133">**Id** - Type `string`.</span></span> <span data-ttu-id="40513-134">佇列訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="40513-134">Queue message ID.</span></span>
* <span data-ttu-id="40513-135">**InsertionTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="40513-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="40513-136">hello 時間 hello 訊息已加入 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="40513-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="40513-137">**NextVisibleTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="40513-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="40513-138">hello 時間 hello 訊息接著會顯示。</span><span class="sxs-lookup"><span data-stu-id="40513-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="40513-139">**PopReceipt** - 鍵入 `string`。</span><span class="sxs-lookup"><span data-stu-id="40513-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="40513-140">hello 訊息的 pop receipt。</span><span class="sxs-lookup"><span data-stu-id="40513-140">hello message's pop receipt.</span></span>

<span data-ttu-id="40513-141">請參閱如何 toouse hello 佇列中繼資料中的[觸發程序範例](#triggersample)。</span><span class="sxs-lookup"><span data-stu-id="40513-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="40513-142">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="40513-142">Trigger sample</span></span>
<span data-ttu-id="40513-143">假設您有下列定義佇列的觸發程序的 function.json hello:</span><span class="sxs-lookup"><span data-stu-id="40513-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

<span data-ttu-id="40513-144">請參閱 hello 特定語言的範例會擷取和記錄佇列中繼資料。</span><span class="sxs-lookup"><span data-stu-id="40513-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="40513-145">C#</span><span class="sxs-lookup"><span data-stu-id="40513-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="40513-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="40513-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="40513-147">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="40513-147">Trigger sample in C#</span></span> #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="40513-148">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="40513-148">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="40513-149">處理有害的佇列訊息</span><span class="sxs-lookup"><span data-stu-id="40513-149">Handling poison queue messages</span></span>
<span data-ttu-id="40513-150">佇列觸發程序函數失敗時，Azure 函式會重試總 toofive 對於給定的佇列訊息，包括 hello 第一次的時間再試一次該函式。</span><span class="sxs-lookup"><span data-stu-id="40513-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="40513-151">如果所有五個嘗試都失敗，hello 函式執行階段會將名為訊息 tooa 佇列儲存體 *&lt;originalqueuename >-有害*。</span><span class="sxs-lookup"><span data-stu-id="40513-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="40513-152">您可以撰寫函式 tooprocess 訊息從 hello 有害佇列記錄或傳送通知，需要進行手動處理。</span><span class="sxs-lookup"><span data-stu-id="40513-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="40513-153">toohandle 有害訊息，手動檢查 hello `dequeueCount` hello 佇列訊息的 (請參閱[佇列觸發程序的中繼資料](#meta))。</span><span class="sxs-lookup"><span data-stu-id="40513-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="40513-154">佇列儲存體輸出繫結</span><span class="sxs-lookup"><span data-stu-id="40513-154">Queue storage output binding</span></span>
<span data-ttu-id="40513-155">hello Azure 佇列儲存體輸出繫結可讓您 toowrite 訊息 tooa 佇列。</span><span class="sxs-lookup"><span data-stu-id="40513-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="40513-156">定義佇列輸出繫結使用 hello**整合**hello 函式的入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="40513-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="40513-157">hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:</span><span class="sxs-lookup"><span data-stu-id="40513-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="40513-158">hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="40513-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="40513-159">Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="40513-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="40513-160">使用佇列輸出繫結</span><span class="sxs-lookup"><span data-stu-id="40513-160">Using a queue output binding</span></span>
<span data-ttu-id="40513-161">Node.js 函式，在您存取 hello 輸出佇列使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="40513-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="40513-162">在.NET 函數中，您可以將輸出 tooany hello 下列類型。</span><span class="sxs-lookup"><span data-stu-id="40513-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="40513-163">型別參數時`T`，`T`必須是其中一個支援的 hello 輸出類型，例如`string`或 POCO。</span><span class="sxs-lookup"><span data-stu-id="40513-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="40513-164">`out T` (序列化為 JSON)</span><span class="sxs-lookup"><span data-stu-id="40513-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="40513-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="40513-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="40513-166">您也可以使用 hello 方法的傳回型別為 hello 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="40513-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="40513-167">佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="40513-167">Queue output sample</span></span>
<span data-ttu-id="40513-168">hello 下列*function.json*定義與佇列 HTTP 觸發程序輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="40513-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

<span data-ttu-id="40513-169">請參閱輸出 hello 連入 HTTP 裝載的佇列訊息的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="40513-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="40513-170">C#</span><span class="sxs-lookup"><span data-stu-id="40513-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="40513-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="40513-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="40513-172">C# 中的佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="40513-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

<span data-ttu-id="40513-173">toosend 多則訊息，使用`ICollector`:</span><span class="sxs-lookup"><span data-stu-id="40513-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="40513-174">Node.js 中的佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="40513-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="40513-175">或者，toosend 多則訊息，</span><span class="sxs-lookup"><span data-stu-id="40513-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="40513-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40513-176">Next steps</span></span>

<span data-ttu-id="40513-177">如需使用佇列儲存體觸發程序和繫結的函式的範例，請參閱[建立 Azure 服務的連線的 Azure 函式 tooan](functions-create-an-azure-connected-function.md)。</span><span class="sxs-lookup"><span data-stu-id="40513-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
