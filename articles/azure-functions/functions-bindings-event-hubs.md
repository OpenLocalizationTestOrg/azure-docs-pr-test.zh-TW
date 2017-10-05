---
title: "Azure Functions 事件中樞繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用 Azure 事件中樞繫結。"
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
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="c6a1d-104">Azure Functions 事件中樞繫結</span><span class="sxs-lookup"><span data-stu-id="c6a1d-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="c6a1d-105">本文說明如何針對 Azure Functions 設定及使用 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)繫結。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="c6a1d-106">Azure Functions 支援事件中樞的觸發程序和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="c6a1d-107">如果您對 Azure 事件中樞並不熟悉，請參閱[事件中樞概述](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="c6a1d-108">事件中樞觸發程序</span><span class="sxs-lookup"><span data-stu-id="c6a1d-108">Event hub trigger</span></span>
<span data-ttu-id="c6a1d-109">使用事件中樞觸發程序將回應傳送至事件中樞事件資料流。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="c6a1d-110">您必須具有事件中樞的讀取存取權，才能設定觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="c6a1d-111">事件中樞函式觸發程序會使用 function.json 之 `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="c6a1d-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="c6a1d-112">`consumerGroup` 是選擇性屬性，可設定用來訂閱中樞內事件的[取用者群組](../event-hubs/event-hubs-features.md#event-consumers)。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="c6a1d-113">如果省略，則會使用 `$Default` 取用者群組。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="c6a1d-114">`connection` 必須是應用程式設定的名稱，包含事件中樞命名空間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="c6a1d-115">按一下*命名空間*的 [連接資訊] 按鈕 (而不是事件中樞本身)，來複製此連接字串。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="c6a1d-116">此連接字串至少必須具備讀取權限，才能啟動觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="c6a1d-117">可以在 host.json 檔案中提供[其他設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)來進一步微調事件中樞觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="c6a1d-118">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="c6a1d-118">Trigger usage</span></span>
<span data-ttu-id="c6a1d-119">事件中樞觸發程序函式觸發時，觸發它的訊息會以字串形式傳遞至函式。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="c6a1d-120">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-120">Trigger sample</span></span>
<span data-ttu-id="c6a1d-121">假設您的 function.json 之 `bindings` 陣列中有下列事件中樞觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="c6a1d-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="c6a1d-122">請參閱記錄事件中樞的觸發程序的訊息本文的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="c6a1d-123">C#</span><span class="sxs-lookup"><span data-stu-id="c6a1d-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="c6a1d-124">F#</span><span class="sxs-lookup"><span data-stu-id="c6a1d-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="c6a1d-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6a1d-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="c6a1d-126">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="c6a1d-127">您也能以 [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) 物件的形式接收事件，該物件能為您提供事件中繼資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="c6a1d-128">若要以批次接收事件，請將方法簽章變更為 `string[]` 或 `EventData[]`。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="c6a1d-129">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="c6a1d-130">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="c6a1d-131">事件中樞輸出繫結</span><span class="sxs-lookup"><span data-stu-id="c6a1d-131">Event Hubs output binding</span></span>
<span data-ttu-id="c6a1d-132">使用事件中樞輸出繫結將事件寫入事件中樞事件資料流。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="c6a1d-133">您必須具備事件中樞的傳送權限，才能將事件寫入其中。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="c6a1d-134">輸出繫結會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="c6a1d-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="c6a1d-135">`connection` 必須是應用程式設定的名稱，包含事件中樞命名空間的連接字串。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="c6a1d-136">按一下*命名空間*的 [連接資訊] 按鈕 (而不是事件中樞本身)，來複製此連接字串。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="c6a1d-137">此連接字串必須具有傳送權限，才能將訊息傳送至事件資料流。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="c6a1d-138">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="c6a1d-138">Output usage</span></span>
<span data-ttu-id="c6a1d-139">本節說明如何在您的函式程式碼中使用「事件中樞」輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="c6a1d-140">您可以使用下列參數類型，將訊息輸出至已設定的事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="c6a1d-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="c6a1d-141">`ICollector<string>` (輸出多個訊息)</span><span class="sxs-lookup"><span data-stu-id="c6a1d-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="c6a1d-142">`IAsyncCollector<string>` (`ICollector<T>` 的非同步版本)</span><span class="sxs-lookup"><span data-stu-id="c6a1d-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="c6a1d-143">輸出範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-143">Output sample</span></span>
<span data-ttu-id="c6a1d-144">假設您的 function.json 之 `bindings` 陣列中有下列事件中樞輸出繫結︰</span><span class="sxs-lookup"><span data-stu-id="c6a1d-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="c6a1d-145">請參閱會將事件寫入事件資料流的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="c6a1d-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="c6a1d-146">C#</span><span class="sxs-lookup"><span data-stu-id="c6a1d-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="c6a1d-147">F#</span><span class="sxs-lookup"><span data-stu-id="c6a1d-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="c6a1d-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6a1d-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="c6a1d-149">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="c6a1d-150">或者，若要建立多個訊息：</span><span class="sxs-lookup"><span data-stu-id="c6a1d-150">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="c6a1d-151">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="c6a1d-152">Node.js 的輸出範例</span><span class="sxs-lookup"><span data-stu-id="c6a1d-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="c6a1d-153">或者，若要傳送多個訊息，</span><span class="sxs-lookup"><span data-stu-id="c6a1d-153">Or, to send multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c6a1d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6a1d-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
