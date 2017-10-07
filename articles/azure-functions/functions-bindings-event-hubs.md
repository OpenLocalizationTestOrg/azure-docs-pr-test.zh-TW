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
# <a name="azure-functions-event-hubs-bindings"></a>Azure Functions 事件中樞繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何 tooconfigure 並用[Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)Azure 函式繫結。
Azure Functions 支援事件中樞的觸發程序和輸出繫結。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

如果您是新 tooAzure 事件中心時，請參閱 hello[事件中心概觀](../event-hubs/event-hubs-what-is-event-hubs.md)。

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>事件中樞觸發程序
使用 hello 事件中心觸發 toorespond tooan 事件傳送 tooan 事件中樞事件資料流。 您必須擁有讀取權限 toohello 事件中樞 tooset hello 觸發程序。

hello 事件中心函式觸發程序會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

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

`consumerGroup`為使用的選擇性屬性 tooset hello[取用者群組](../event-hubs/event-hubs-features.md#event-consumers)toosubscribe tooevents 用於 hello 中樞。 如果省略，hello`$Default`使用取用者群組。  
`connection`必須是 hello 包含 hello 連接字串 toohello 事件中心的命名空間的應用程式設定名稱。
複製這個連接字串，請按一下 hello**連接資訊**按鈕 hello*命名空間*，不 hello 事件中心本身。 這個連接字串必須至少具有讀取權限 tooactivate hello 觸發程序。

[其他設定](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)可以用來在 host.json 檔案 toofurther 正常微調事件中心觸發程序。  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>觸發程序使用方式
觸發的事件中心的觸發程序函式時，它會觸發的 hello 訊息傳入 hello 函式做為字串。

<a name="triggersample"></a>

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列事件中心觸發 hello 中的 hello `bindings` function.json 的陣列：

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

請參閱 hello 記錄 hello 訊息本文的 hello 事件中樞觸發程序的特定語言的範例。

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>C# 中的觸發程序範例 #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

您也可以收到 hello 事件做[EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata)物件，可讓您存取 toohello 事件中繼資料。

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

tooreceive 批次中的事件變更 hello 方法簽章太`string[]`或`EventData[]`。

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

### <a name="trigger-sample-in-f"></a>F# 中的觸發程序範例 #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js 中的觸發程序範例

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>事件中樞輸出繫結
使用 hello 事件中心輸出繫結 toowrite 事件 tooan 事件中樞事件資料流。 您必須擁有傳送權限 tooan 事件中樞 toowrite 事件 tooit。

hello 輸出繫結會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`必須是 hello 包含 hello 連接字串 toohello 事件中心的命名空間的應用程式設定名稱。
複製這個連接字串，請按一下 hello**連接資訊**按鈕 hello*命名空間*，不 hello 事件中心本身。 這個連接字串必須傳送權限 toosend hello 訊息 toohello 事件資料流。

## <a name="output-usage"></a>輸出使用方式
本節說明如何 toouse 事件中心輸出繫結函式程式碼中。

您可以使用下列參數類型的 hello 輸出訊息 toohello 設定事件中心：

* `out string`
* `ICollector<string>`(toooutput 多個訊息)
* `IAsyncCollector<string>` (`ICollector<T>` 的非同步版本)

<a name="outputsample"></a>

## <a name="output-sample"></a>輸出範例
假設您有 hello 下列事件中心輸出繫結中 hello `bindings` function.json 的陣列：

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

請參閱 hello 寫入事件 toohello 甚至是資料流的特定語言的範例。

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# 中的輸出範例 #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

或者，toocreate 多則訊息：

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

### <a name="output-sample-in-f"></a>F# 中的輸出範例 #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Node.js 的輸出範例

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

或者，toosend 多則訊息，

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

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
