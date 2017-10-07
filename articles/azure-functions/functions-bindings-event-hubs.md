---
title: "aaaAzure 函式的事件中心繫結 |Microsoft 文件"
description: "了解如何在 Azure 函式 toouse Azure 事件中心繫結。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="cc4b7-104">Azure Functions 事件中樞繫結</span><span class="sxs-lookup"><span data-stu-id="cc4b7-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="cc4b7-105">這篇文章說明如何 tooconfigure 並用[Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)Azure 函式繫結。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="cc4b7-106">Azure Functions 支援事件中樞的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="cc4b7-107">如果您是新 tooAzure 事件中心時，請參閱 hello[事件中心概觀](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="cc4b7-108">事件中樞觸發程序</span><span class="sxs-lookup"><span data-stu-id="cc4b7-108">Event hub trigger</span></span>
<span data-ttu-id="cc4b7-109">使用 hello 事件中心觸發 toorespond tooan 事件傳送 tooan 事件中樞事件資料流。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="cc4b7-110">您必須擁有讀取權限 toohello 事件中樞 tooset hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="cc4b7-111">hello 事件中心函式觸發程序會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="cc4b7-112">`consumerGroup`為使用的選擇性屬性 tooset hello[取用者群組](../event-hubs/event-hubs-features.md#event-consumers)toosubscribe tooevents 用於 hello 中樞。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="cc4b7-113">如果省略，hello`$Default`使用取用者群組。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="cc4b7-114">`connection`必須是 hello 包含 hello 連接字串 toohello 事件中心的命名空間的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="cc4b7-115">複製這個連接字串，請按一下 hello**連接資訊**按鈕 hello*命名空間*，不 hello 事件中心本身。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="cc4b7-116">這個連接字串必須至少具有讀取權限 tooactivate hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="cc4b7-117">[其他設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)可以用來在 host.json 檔案 toofurther 正常微調事件中心觸發程序。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="cc4b7-118">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="cc4b7-118">Trigger usage</span></span>
<span data-ttu-id="cc4b7-119">觸發的事件中心的觸發程序函式時，它會觸發的 hello 訊息傳入 hello 函式做為字串。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="cc4b7-120">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-120">Trigger sample</span></span>
<span data-ttu-id="cc4b7-121">假設您有下列事件中心觸發 hello 中的 hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="cc4b7-122">請參閱 hello 記錄 hello 訊息本文的 hello 事件中樞觸發程序的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="cc4b7-123">C#</span><span class="sxs-lookup"><span data-stu-id="cc4b7-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="cc4b7-124">F#</span><span class="sxs-lookup"><span data-stu-id="cc4b7-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="cc4b7-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="cc4b7-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="cc4b7-126">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="cc4b7-127">您也可以收到 hello 事件做[EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata)物件，可讓您存取 toohello 事件中繼資料。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="cc4b7-128">tooreceive 批次中的事件變更 hello 方法簽章太`string[]`或`EventData[]`。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="cc4b7-129">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="cc4b7-130">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="cc4b7-131">事件中樞輸出繫結</span><span class="sxs-lookup"><span data-stu-id="cc4b7-131">Event Hubs output binding</span></span>
<span data-ttu-id="cc4b7-132">使用 hello 事件中心輸出繫結 toowrite 事件 tooan 事件中樞事件資料流。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="cc4b7-133">您必須擁有傳送權限 tooan 事件中樞 toowrite 事件 tooit。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="cc4b7-134">hello 輸出繫結會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="cc4b7-135">`connection`必須是 hello 包含 hello 連接字串 toohello 事件中心的命名空間的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="cc4b7-136">複製這個連接字串，請按一下 hello**連接資訊**按鈕 hello*命名空間*，不 hello 事件中心本身。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="cc4b7-137">這個連接字串必須傳送權限 toosend hello 訊息 toohello 事件資料流。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="cc4b7-138">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="cc4b7-138">Output usage</span></span>
<span data-ttu-id="cc4b7-139">本節說明如何 toouse 事件中心輸出繫結函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="cc4b7-140">您可以使用下列參數類型的 hello 輸出訊息 toohello 設定事件中心：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="cc4b7-141">`ICollector<string>`(toooutput 多個訊息)</span><span class="sxs-lookup"><span data-stu-id="cc4b7-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="cc4b7-142">`IAsyncCollector<string>` (`ICollector<T>` 的非同步版本)</span><span class="sxs-lookup"><span data-stu-id="cc4b7-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="cc4b7-143">輸出範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-143">Output sample</span></span>
<span data-ttu-id="cc4b7-144">假設您有 hello 下列事件中心輸出繫結中 hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="cc4b7-145">請參閱 hello 寫入事件 toohello 甚至是資料流的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="cc4b7-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="cc4b7-146">C#</span><span class="sxs-lookup"><span data-stu-id="cc4b7-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="cc4b7-147">F#</span><span class="sxs-lookup"><span data-stu-id="cc4b7-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="cc4b7-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="cc4b7-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="cc4b7-149">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="cc4b7-150">或者，toocreate 多則訊息：</span><span class="sxs-lookup"><span data-stu-id="cc4b7-150">Or, toocreate multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="cc4b7-151">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="cc4b7-152">Node.js 的輸出範例</span><span class="sxs-lookup"><span data-stu-id="cc4b7-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="cc4b7-153">或者，toosend 多則訊息，</span><span class="sxs-lookup"><span data-stu-id="cc4b7-153">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="cc4b7-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc4b7-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
