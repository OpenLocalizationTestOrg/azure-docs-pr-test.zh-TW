---
title: "Azure Functions 服務匯流排觸發程序和繫結 | Microsoft Docs"
description: "瞭解如何在 Azure Functions 中使用「Azure 服務匯流排」觸發程序和繫結。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="e6405-104">Azure Functions 服務匯流排繫結</span><span class="sxs-lookup"><span data-stu-id="e6405-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e6405-105">此文章說明如何在 Azure Functions 中設定及使用 Azure 服務匯流排繫結。</span><span class="sxs-lookup"><span data-stu-id="e6405-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="e6405-106">Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e6405-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="e6405-107">服務匯流排觸發程序</span><span class="sxs-lookup"><span data-stu-id="e6405-107">Service Bus trigger</span></span>
<span data-ttu-id="e6405-108">使用服務匯流排觸發程序來回應來自服務匯流排佇列或主題的訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="e6405-109">服務匯流排佇列和主題觸發程序是由 function.json 之 `bindings` 陣列中的 JSON 物件定義的:</span><span class="sxs-lookup"><span data-stu-id="e6405-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="e6405-110">*佇列*觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="e6405-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="e6405-111">*主題*觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="e6405-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="e6405-112">請注意：</span><span class="sxs-lookup"><span data-stu-id="e6405-112">Note the following:</span></span>

* <span data-ttu-id="e6405-113">針對 `connection`，請[在您的函數應用程式中建立應用程式設定](functions-how-to-use-azure-function-app-settings.md)，其中包含您「服務匯流排」命名空間的連接字串，然後在觸發程序的 `connection` 屬性中指定應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6405-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="e6405-114">您會遵循[取得管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)中顯示的步驟來取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="e6405-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="e6405-115">連接字串必須是用於服務匯流排命名空間，而不限於特定佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="e6405-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="e6405-116">如果您將 `connection` 保留空白，觸發程序會假設預設的服務匯流排連接字串已在名為 `AzureWebJobsServiceBus` 的應用程式設定中指定。</span><span class="sxs-lookup"><span data-stu-id="e6405-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="e6405-117">針對 `accessRights`，可用值為 `manage` 和 `listen`。</span><span class="sxs-lookup"><span data-stu-id="e6405-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="e6405-118">預設值是 `manage`，這表示 `connection` 已具備**管理**權限。</span><span class="sxs-lookup"><span data-stu-id="e6405-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="e6405-119">如果您使用沒有**管理**權限的連接字串，請將 `accessRights` 設定為 `listen`。</span><span class="sxs-lookup"><span data-stu-id="e6405-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="e6405-120">否則，Functions 執行階段在嘗試執行需要管理權限的作業時可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e6405-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="e6405-121">觸發程序行為</span><span class="sxs-lookup"><span data-stu-id="e6405-121">Trigger behavior</span></span>
* <span data-ttu-id="e6405-122">**單一執行緒** - Functions 執行階段預設會並行處理多個訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="e6405-123">若要指示執行階段一次只處理一個佇列或主題訊息，請在 *host.json* 檔案中將 `serviceBus.maxConcurrentCalls` 設定為 1。</span><span class="sxs-lookup"><span data-stu-id="e6405-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="e6405-124">如需有關 *host.json* 的資訊，請參閱[資料夾結構](functions-reference.md#folder-structure)和 [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e6405-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="e6405-125">**有害訊息處理** - 服務匯流排會自行處理無法在 Azure Functions 組態或程式碼中控制或設定的有害訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="e6405-126">**PeekLock behavior** - Functions 執行階段會在 [`PeekLock` 模式](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode)下接收訊息，並在函式順利完成時，於訊息上呼叫 `Complete`，或是在函式失敗時呼叫 `Abandon`。</span><span class="sxs-lookup"><span data-stu-id="e6405-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="e6405-127">如果函數執行時間較 `PeekLock` 逾時還長，即會自動更新鎖定。</span><span class="sxs-lookup"><span data-stu-id="e6405-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e6405-128">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="e6405-128">Trigger usage</span></span>
<span data-ttu-id="e6405-129">本節說明如何在您的函數程式碼中使用「服務匯流排」觸發程序。</span><span class="sxs-lookup"><span data-stu-id="e6405-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="e6405-130">在 C# 和 F# 中，服務匯流排觸發程序訊息可以還原序列化為下列任何一種輸入類型︰</span><span class="sxs-lookup"><span data-stu-id="e6405-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="e6405-131">`string` - 適用於字串訊息</span><span class="sxs-lookup"><span data-stu-id="e6405-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="e6405-132">`byte[]` - 適用於二進位資料</span><span class="sxs-lookup"><span data-stu-id="e6405-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="e6405-133">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的資料。</span><span class="sxs-lookup"><span data-stu-id="e6405-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="e6405-134">如果您宣告自訂輸入類型 (例如 `CustomType`)，Azure Functions 會嘗試將 JSON 資料還原序列化為您指定的類型。</span><span class="sxs-lookup"><span data-stu-id="e6405-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="e6405-135">`BrokeredMessage` - 利用 [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) 方法提供您還原序列化的訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="e6405-136">在 Node.js 中，服務匯流排觸發程序訊息會以字串或 JSON 物件的形式傳遞至函式。</span><span class="sxs-lookup"><span data-stu-id="e6405-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="e6405-137">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e6405-137">Trigger sample</span></span>
<span data-ttu-id="e6405-138">假設您有下列 function.json︰</span><span class="sxs-lookup"><span data-stu-id="e6405-138">Suppose you have the following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="e6405-139">請參閱可處理服務匯流排佇列訊息的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="e6405-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="e6405-140">C#</span><span class="sxs-lookup"><span data-stu-id="e6405-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e6405-141">F#</span><span class="sxs-lookup"><span data-stu-id="e6405-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="e6405-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="e6405-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e6405-143">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e6405-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="e6405-144">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e6405-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e6405-145">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e6405-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="e6405-146">服務匯流排輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e6405-146">Service Bus output binding</span></span>
<span data-ttu-id="e6405-147">函式的服務匯流排佇列和主題輸出會使用 function.json 之 `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="e6405-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="e6405-148">*佇列*輸出︰</span><span class="sxs-lookup"><span data-stu-id="e6405-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="e6405-149">*主題*輸出︰</span><span class="sxs-lookup"><span data-stu-id="e6405-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="e6405-150">請注意：</span><span class="sxs-lookup"><span data-stu-id="e6405-150">Note the following:</span></span>

* <span data-ttu-id="e6405-151">針對 `connection`，請[在您的函數應用程式中建立應用程式設定](functions-how-to-use-azure-function-app-settings.md)，其中包含您「服務匯流排」命名空間的連接字串，然後在輸出繫結的 `connection` 屬性中指定應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="e6405-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="e6405-152">您會遵循[取得管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)中顯示的步驟來取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="e6405-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="e6405-153">連接字串必須是用於服務匯流排命名空間，而不限於特定佇列或主題。</span><span class="sxs-lookup"><span data-stu-id="e6405-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="e6405-154">如果您將 `connection` 保留空白，輸出繫結會假設預設的服務匯流排連接字串已在名為 `AzureWebJobsServiceBus` 的應用程式設定中指定。</span><span class="sxs-lookup"><span data-stu-id="e6405-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="e6405-155">針對 `accessRights`，可用值為 `manage` 和 `listen`。</span><span class="sxs-lookup"><span data-stu-id="e6405-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="e6405-156">預設值是 `manage`，這表示 `connection` 已具備**管理**權限。</span><span class="sxs-lookup"><span data-stu-id="e6405-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="e6405-157">如果您使用沒有**管理**權限的連接字串，請將 `accessRights` 設定為 `listen`。</span><span class="sxs-lookup"><span data-stu-id="e6405-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="e6405-158">否則，Functions 執行階段在嘗試執行需要管理權限的作業時可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e6405-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="e6405-159">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="e6405-159">Output usage</span></span>
<span data-ttu-id="e6405-160">在 C# 和 F# 中，Azure Functions 可以從下列任何類型建立服務匯流排佇列訊息：</span><span class="sxs-lookup"><span data-stu-id="e6405-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="e6405-161">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 參數定義看起來像 `out T paramName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="e6405-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="e6405-162">Functions 會將物件還原序列化為 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="e6405-163">當函式結束時，如果輸出值是 null，Functions 會使用 Null 物件建立訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="e6405-164">`string` - 參數定義看起來像 `out string paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="e6405-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="e6405-165">如果參數值為非 Null，則函式結束時，Functions 會建立一則訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="e6405-166">`byte[]` - 參數定義看起來像 `out byte[] paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="e6405-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="e6405-167">如果參數值為非 Null，則函式結束時，Functions 會建立一則訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="e6405-168">`BrokeredMessage` - 參數定義看起來像 `out BrokeredMessage paraName` (C#)。</span><span class="sxs-lookup"><span data-stu-id="e6405-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="e6405-169">如果參數值為非 Null，則函式結束時，Functions 會建立一則訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="e6405-170">若要在 C# 函式中建立多個訊息，您可以使用 `ICollector<T>` 或 `IAsyncCollector<T>`。</span><span class="sxs-lookup"><span data-stu-id="e6405-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="e6405-171">當您呼叫 `Add` 方法時，就會建立一則訊息。</span><span class="sxs-lookup"><span data-stu-id="e6405-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="e6405-172">在 Node.js 中，您可以指派字串、位元組陣列或 Javascript 物件 (還原序列化為 JSON) 給 `context.binding.<paramName>`。</span><span class="sxs-lookup"><span data-stu-id="e6405-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="e6405-173">輸出範例</span><span class="sxs-lookup"><span data-stu-id="e6405-173">Output sample</span></span>
<span data-ttu-id="e6405-174">假設您有下列 function.json，則會定義服務匯流排佇列輸出︰</span><span class="sxs-lookup"><span data-stu-id="e6405-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="e6405-175">請參閱可傳送訊息至服務匯流排佇列的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="e6405-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="e6405-176">C#</span><span class="sxs-lookup"><span data-stu-id="e6405-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e6405-177">F#</span><span class="sxs-lookup"><span data-stu-id="e6405-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e6405-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="e6405-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e6405-179">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e6405-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="e6405-180">或者，若要建立多個訊息：</span><span class="sxs-lookup"><span data-stu-id="e6405-180">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="e6405-181">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e6405-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="e6405-182">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e6405-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="e6405-183">或者，若要建立多個訊息：</span><span class="sxs-lookup"><span data-stu-id="e6405-183">Or, to create multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e6405-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6405-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

