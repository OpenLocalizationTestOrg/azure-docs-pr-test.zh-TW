---
title: "aaaAzure 函式服務匯流排觸發程序和繫結 |Microsoft 文件"
description: "了解觸發 toouse Azure 服務匯流排的方式，在 Azure 函式中的繫結。"
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
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Azure Functions 服務匯流排繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何 tooconfigure 地使用 Azure 功能中的 Azure 服務匯流排繫結。 

Azure Functions 支援服務匯流排佇列和主題的觸發程序和輸出繫結。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>服務匯流排觸發程序
使用 hello Service Bus 觸發程序 toorespond toomessages 從服務匯流排佇列或主題。 

hello Service Bus 佇列和主題觸發程序會由下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

* *佇列*觸發程序︰

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* *主題*觸發程序︰

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

請注意 hello 下列：

* 如`connection`，[函式應用程式中建立的應用程式設定](functions-how-to-use-azure-function-app-settings.md)包含 hello 連接字串 tooyour 服務匯流排命名空間，然後指定 hello hello 應用程式設定名稱在 hello`connection`觸發程序中的屬性。 您取得 hello 連接字串顯示 hello 步驟[取得 hello 管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)。
  hello 連接字串必須是服務匯流排命名空間、 不限的 tooa 特定佇列或主題。
  如果您離開`connection`空的 hello 觸發程序會假設預設服務匯流排連接字串會指定在應用程式中設定，稱為`AzureWebJobsServiceBus`。
* 針對 `accessRights`，可用值為 `manage` 和 `listen`。 hello 預設值是`manage`，表示該 hello`connection`具有 hello**管理**權限。 如果您使用的連接字串，但是沒有 hello**管理**權限，設定`accessRights`太`listen`。 否則，hello 函式執行階段可能會失敗，嘗試 toodo 作業需要管理權限。

## <a name="trigger-behavior"></a>觸發程序行為
* **單一執行緒**-根據預設，多個訊息同時的 hello 函式執行階段處理序。 toodirect hello 執行階段 tooprocess 只有單一佇列或主題訊息一次設定`serviceBus.maxConcurrentCalls`中的 too1 *host.json*。 
  如需有關 *host.json* 的資訊，請參閱[資料夾結構](functions-reference.md#folder-structure)和 [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json) \(英文\)。
* **有害訊息處理** - 服務匯流排會自行處理無法在 Azure Functions 組態或程式碼中控制或設定的有害訊息。 
* **PeekLock 行為**-hello 函式執行階段接收的訊息中[`PeekLock`模式](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode)和呼叫`Complete`hello 訊息，如果成功，完成 hello 函式或呼叫`Abandon`如果 hello函式會失敗。 
  如果 hello 函式執行時間長於 hello `PeekLock` hello 鎖定逾時，會自動更新。

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>觸發程序使用方式
本節說明如何 toouse Service Bus 觸發函式程式碼中。 

在 C# 和 F # hello Service Bus 觸發程序訊息可以是 hello 的下列輸入的類型的已還原序列化的 tooany:

* `string` - 適用於字串訊息
* `byte[]` - 適用於二進位資料
* 任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的資料。
  如果您宣告自訂的輸入的類型，例如`CustomType`，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。
* `BrokeredMessage`-可讓您 hello 還原序列化訊息以 hello [BrokeredMessage.GetBody<T>（)](https://msdn.microsoft.com/library/hh144211.aspx)方法。

在 Node.js hello Service Bus 觸發程序訊息傳遞到做為字串或 JSON 物件的 hello 函式。

<a name="triggersample"></a>

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列 function.json hello:

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

請參閱 hello 處理服務匯流排佇列訊息的特定語言的範例。

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>C# 中的觸發程序範例 #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>F# 中的觸發程序範例 #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js 中的觸發程序範例

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>服務匯流排輸出繫結
hello 函式的服務匯流排佇列和主題輸出使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

* *佇列*輸出︰

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* *主題*輸出︰

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

請注意 hello 下列：

* 如`connection`，[函式應用程式中建立的應用程式設定](functions-how-to-use-azure-function-app-settings.md)包含 hello 連接字串 tooyour 服務匯流排命名空間，然後指定 hello hello 應用程式設定名稱在 hello`connection`在輸出中的屬性繫結。 您取得 hello 連接字串顯示 hello 步驟[取得 hello 管理認證](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials)。
  hello 連接字串必須是服務匯流排命名空間、 不限的 tooa 特定佇列或主題。
  如果您離開`connection`空的 hello 輸出繫結假設預設服務匯流排連接字串會指定在應用程式中設定，稱為`AzureWebJobsServiceBus`。
* 針對 `accessRights`，可用值為 `manage` 和 `listen`。 hello 預設值是`manage`，表示該 hello`connection`具有 hello**管理**權限。 如果您使用的連接字串，但是沒有 hello**管理**權限，設定`accessRights`太`listen`。 否則，hello 函式執行階段可能會失敗，嘗試 toodo 作業需要管理權限。

<a name="outputusage"></a>

## <a name="output-usage"></a>輸出使用方式
在 C# 和 F #，Azure 函式可以從任何下列類型的 hello 建立服務匯流排佇列訊息：

* 任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 參數定義看起來像 `out T paramName` (C#)。
  函式會將 hello 物件還原序列化成 JSON 訊息。 如果 hello 函式結束時，hello 輸出值是 null，函式會建立 hello 訊息與 null 的物件。
* `string` - 參數定義看起來像 `out string paraName` (C#)。 Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。
* `byte[]` - 參數定義看起來像 `out byte[] paraName` (C#)。 Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。
* `BrokeredMessage` - 參數定義看起來像 `out BrokeredMessage paraName` (C#)。 Hello 參數值為非 null hello 函式結束時，如果函式會建立訊息。

若要在 C# 函式中建立多個訊息，您可以使用 `ICollector<T>` 或 `IAsyncCollector<T>`。 當您呼叫 hello 時，會建立訊息`Add`方法。

在 Node.js，您可以指定字串、 位元組陣列或 Javascript 物件 （還原序列化為 JSON） 太`context.binding.<paramName>`。

<a name="outputsample"></a>

## <a name="output-sample"></a>輸出範例
假設您有下列 function.json 定義服務匯流排佇列輸出 hello:

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

請參閱 hello 傳送訊息 toohello 服務匯流排佇列的特定語言的範例。

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# 中的輸出範例 #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

或者，toocreate 多則訊息：

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

### <a name="output-sample-in-f"></a>F# 中的輸出範例 #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Node.js 中的輸出範例

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

或者，toocreate 多則訊息：

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

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

