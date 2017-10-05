---
title: "Azure Functions 佇列儲存體繫結 | Microsoft Docs"
description: "瞭解如何在 Azure Functions 中使用「Azure 儲存體」觸發程序和繫結。"
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
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="4a300-104">Azure Functions 佇列儲存體繫結</span><span class="sxs-lookup"><span data-stu-id="4a300-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="4a300-105">本文說明如何在 Azure Functions 中為 Azure 佇列儲存體繫結進行設定及撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a300-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="4a300-106">Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="4a300-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="4a300-107">如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="4a300-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="4a300-108">佇列儲存體觸發程序</span><span class="sxs-lookup"><span data-stu-id="4a300-108">Queue storage trigger</span></span>
<span data-ttu-id="4a300-109">Azure 佇列儲存體觸發程序可讓您監視佇列儲存體的新訊息，並對它們做出回應。</span><span class="sxs-lookup"><span data-stu-id="4a300-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="4a300-110">使用 Functions 入口網站中的 [整合] 索引標籤定義佇列觸發程序。</span><span class="sxs-lookup"><span data-stu-id="4a300-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="4a300-111">該入口網站會在 *function.json* 的 **bindings** 區段中建立下列定義：</span><span class="sxs-lookup"><span data-stu-id="4a300-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="4a300-112">`connection` 屬性必須包含應用程式設定的名稱，其中包含儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="4a300-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="4a300-113">在 Azure 入口網站中，當您選取儲存體帳戶時，[整合] 索引標籤中的標準編輯器可設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="4a300-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="4a300-114">您可以在 [host.json 檔案](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)中提供其他設定，進一步微調佇列儲存體觸發程序。</span><span class="sxs-lookup"><span data-stu-id="4a300-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="4a300-115">例如，您可以變更 host.json 中的佇列輪詢間隔。</span><span class="sxs-lookup"><span data-stu-id="4a300-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="4a300-116">使用佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="4a300-116">Using a queue trigger</span></span>
<span data-ttu-id="4a300-117">在 Node.js 函式中，使用 `context.bindings.<name>` 存取佇列資料。</span><span class="sxs-lookup"><span data-stu-id="4a300-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="4a300-118">在 .NET 函式中，使用方法參數 (例如`CloudQueueMessage paramName`) 存取佇列承載。</span><span class="sxs-lookup"><span data-stu-id="4a300-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="4a300-119">其中，`paramName` 是您在[觸發程序設定](#trigger)中指定的值。</span><span class="sxs-lookup"><span data-stu-id="4a300-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="4a300-120">佇列訊息可以還原序列化為下列任何一種類型︰</span><span class="sxs-lookup"><span data-stu-id="4a300-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="4a300-121">POCO 物件。</span><span class="sxs-lookup"><span data-stu-id="4a300-121">POCO object.</span></span> <span data-ttu-id="4a300-122">佇列承載為 JSON 物件時使用。</span><span class="sxs-lookup"><span data-stu-id="4a300-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="4a300-123">Functions 執行階段會將承載還原序列化為 POCO 物件。</span><span class="sxs-lookup"><span data-stu-id="4a300-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="4a300-124">佇列觸發程序中繼資料</span><span class="sxs-lookup"><span data-stu-id="4a300-124">Queue trigger metadata</span></span>
<span data-ttu-id="4a300-125">佇列觸發程序提供數個中繼資料屬性。</span><span class="sxs-lookup"><span data-stu-id="4a300-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="4a300-126">這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。</span><span class="sxs-lookup"><span data-stu-id="4a300-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="4a300-127">這些值的語意與 [`CloudQueueMessage`] 相同。</span><span class="sxs-lookup"><span data-stu-id="4a300-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="4a300-128">**QueueTrigger** - 佇列承載 (如果為有效字串)</span><span class="sxs-lookup"><span data-stu-id="4a300-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="4a300-129">**DequeueCount** - 鍵入 `int`。</span><span class="sxs-lookup"><span data-stu-id="4a300-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="4a300-130">此訊息已從佇列清除的次數。</span><span class="sxs-lookup"><span data-stu-id="4a300-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="4a300-131">**ExpirationTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="4a300-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="4a300-132">訊息到期時間。</span><span class="sxs-lookup"><span data-stu-id="4a300-132">The time that the message expires.</span></span>
* <span data-ttu-id="4a300-133">**Id** - 鍵入 `string`。</span><span class="sxs-lookup"><span data-stu-id="4a300-133">**Id** - Type `string`.</span></span> <span data-ttu-id="4a300-134">佇列訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="4a300-134">Queue message ID.</span></span>
* <span data-ttu-id="4a300-135">**InsertionTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="4a300-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="4a300-136">訊息新增至佇列的時間。</span><span class="sxs-lookup"><span data-stu-id="4a300-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="4a300-137">**NextVisibleTime** - 鍵入 `DateTimeOffset?`。</span><span class="sxs-lookup"><span data-stu-id="4a300-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="4a300-138">下次顯示訊息的時間。</span><span class="sxs-lookup"><span data-stu-id="4a300-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="4a300-139">**PopReceipt** - 鍵入 `string`。</span><span class="sxs-lookup"><span data-stu-id="4a300-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="4a300-140">訊息的離開通知。</span><span class="sxs-lookup"><span data-stu-id="4a300-140">The message's pop receipt.</span></span>

<span data-ttu-id="4a300-141">請參閱[觸發程序範例](#triggersample)以了解如何使用佇列中繼資料。</span><span class="sxs-lookup"><span data-stu-id="4a300-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="4a300-142">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="4a300-142">Trigger sample</span></span>
<span data-ttu-id="4a300-143">假設您有下列 function.json，定義了佇列觸發程序：</span><span class="sxs-lookup"><span data-stu-id="4a300-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="4a300-144">請參閱可擷取及記錄佇列中繼資料的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="4a300-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="4a300-145">C#</span><span class="sxs-lookup"><span data-stu-id="4a300-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="4a300-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="4a300-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="4a300-147">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="4a300-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="4a300-148">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="4a300-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="4a300-149">處理有害的佇列訊息</span><span class="sxs-lookup"><span data-stu-id="4a300-149">Handling poison queue messages</span></span>
<span data-ttu-id="4a300-150">當佇列觸發程序函數失敗時，Azure Functions 會針對指定的佇列訊息重試該函數最多五次，包括第一次嘗試。</span><span class="sxs-lookup"><span data-stu-id="4a300-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="4a300-151">如果五次嘗試全都失敗，Functions 執行階段會將訊息新增至名為 &lt;原始佇列名稱>-poison 的佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="4a300-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="4a300-152">您可以撰寫函數，透過記錄或傳送通知表示需要手動處理，來處理有害佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="4a300-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="4a300-153">若要手動處理有害訊息，請檢查佇列訊息的 `dequeueCount` (請參閱[佇列觸發程序中繼資料](#meta))。</span><span class="sxs-lookup"><span data-stu-id="4a300-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="4a300-154">佇列儲存體輸出繫結</span><span class="sxs-lookup"><span data-stu-id="4a300-154">Queue storage output binding</span></span>
<span data-ttu-id="4a300-155">Azure 佇列儲存體輸出繫結可讓您將訊息寫入佇列。</span><span class="sxs-lookup"><span data-stu-id="4a300-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="4a300-156">使用 Functions 入口網站中的 [整合] 索引標籤定義佇列輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="4a300-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="4a300-157">該入口網站會在 *function.json* 的 **bindings** 區段中建立下列定義：</span><span class="sxs-lookup"><span data-stu-id="4a300-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="4a300-158">`connection` 屬性必須包含應用程式設定的名稱，其中包含儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="4a300-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="4a300-159">在 Azure 入口網站中，當您選取儲存體帳戶時，[整合] 索引標籤中的標準編輯器可設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="4a300-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="4a300-160">使用佇列輸出繫結</span><span class="sxs-lookup"><span data-stu-id="4a300-160">Using a queue output binding</span></span>
<span data-ttu-id="4a300-161">在 Node.js 函數中，您會使用 `context.bindings.<name>` 存取輸出佇列。</span><span class="sxs-lookup"><span data-stu-id="4a300-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="4a300-162">在 .NET 函式中，您可以輸出至下列任何類型。</span><span class="sxs-lookup"><span data-stu-id="4a300-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="4a300-163">如果有型別參數 `T`，`T` 必須是其中一個支援的輸出類型，例如 `string` 或 POCO。</span><span class="sxs-lookup"><span data-stu-id="4a300-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="4a300-164">`out T` (序列化為 JSON)</span><span class="sxs-lookup"><span data-stu-id="4a300-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="4a300-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="4a300-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="4a300-166">您也可以使用方法傳回型別作為輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="4a300-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="4a300-167">佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="4a300-167">Queue output sample</span></span>
<span data-ttu-id="4a300-168">下列 *function.json* 定義 HTTP 觸發程序與佇列輸出的繫結：</span><span class="sxs-lookup"><span data-stu-id="4a300-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="4a300-169">請參閱透過傳入 HTTP 承載輸出佇列訊息的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="4a300-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="4a300-170">C#</span><span class="sxs-lookup"><span data-stu-id="4a300-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="4a300-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="4a300-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="4a300-172">C# 中的佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="4a300-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
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

<span data-ttu-id="4a300-173">若要傳送多個訊息，請使用 `ICollector`：</span><span class="sxs-lookup"><span data-stu-id="4a300-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="4a300-174">Node.js 中的佇列輸出範例</span><span class="sxs-lookup"><span data-stu-id="4a300-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="4a300-175">或者，若要傳送多個訊息，</span><span class="sxs-lookup"><span data-stu-id="4a300-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="4a300-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a300-176">Next steps</span></span>

<span data-ttu-id="4a300-177">如需使用佇列儲存體觸發程序和繫結的函式範例，請參閱[建立連線至 Azure 服務的 Azure 函式](functions-create-an-azure-connected-function.md)。</span><span class="sxs-lookup"><span data-stu-id="4a300-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
