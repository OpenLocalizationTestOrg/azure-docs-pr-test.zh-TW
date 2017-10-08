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
# <a name="azure-functions-queue-storage-bindings"></a>Azure Functions 佇列儲存體繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

本文說明如何 tooconfigure 和程式碼 Azure 佇列儲存體中的繫結 Azure 函式。 Azure Functions 支援適用於 Azure 佇列的觸發程序和輸出繫結。 如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>佇列儲存體觸發程序
hello Azure 佇列儲存體觸發程序可讓 toomonitor 新郵件佇列儲存體，並反應 toothem。 

定義佇列觸發程序使用 hello**整合**hello 函式的入口網站中的索引標籤。 hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。 Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。

其他設定可以提供在[host.json 檔案](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)toofurther 微調佇列儲存體觸發程序。 例如，您可以變更 host.json hello 佇列輪詢間隔。

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>使用佇列觸發程序
在 Node.js 函式，存取 hello 佇列資料使用`context.bindings.<name>`。


在.NET 函式，存取 使用下列方法參數的 hello 佇列裝載`CloudQueueMessage paramName`。 在這裡，`paramName`是您在 hello 中指定的 hello 值[觸發程序組態](#trigger)。 hello 佇列訊息可以是 hello 的下列類型的已還原序列化的 tooany:

* POCO 物件。 如果 hello 佇列裝載為 JSON 物件，使用。 hello 函式執行階段會還原序列化成 hello POCO 物件 hello 裝載。 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>佇列觸發程序中繼資料
hello 佇列觸發程序會提供數個中繼資料屬性。 這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。 hello 值有 hello 相同的語意[ `CloudQueueMessage` ]。

* **QueueTrigger** - 佇列承載 (如果為有效字串)
* **DequeueCount** - 鍵入 `int`。 hello 的此訊息清除佇列的次數。
* **ExpirationTime** - 鍵入 `DateTimeOffset?`。 hello 時間該 hello 訊息過期。
* **Id** - 鍵入 `string`。 佇列訊息識別碼。
* **InsertionTime** - 鍵入 `DateTimeOffset?`。 hello 時間 hello 訊息已加入 toohello 佇列。
* **NextVisibleTime** - 鍵入 `DateTimeOffset?`。 hello 時間 hello 訊息接著會顯示。
* **PopReceipt** - 鍵入 `string`。 hello 訊息的 pop receipt。

請參閱如何 toouse hello 佇列中繼資料中的[觸發程序範例](#triggersample)。

<a name="triggersample"></a>

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列定義佇列的觸發程序的 function.json hello:

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

請參閱 hello 特定語言的範例會擷取和記錄佇列中繼資料。

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>C# 中的觸發程序範例 #
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

### <a name="trigger-sample-in-nodejs"></a>Node.js 中的觸發程序範例

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

### <a name="handling-poison-queue-messages"></a>處理有害的佇列訊息
佇列觸發程序函數失敗時，Azure 函式會重試總 toofive 對於給定的佇列訊息，包括 hello 第一次的時間再試一次該函式。 如果所有五個嘗試都失敗，hello 函式執行階段會將名為訊息 tooa 佇列儲存體 *&lt;originalqueuename >-有害*。 您可以撰寫函式 tooprocess 訊息從 hello 有害佇列記錄或傳送通知，需要進行手動處理。 

toohandle 有害訊息，手動檢查 hello `dequeueCount` hello 佇列訊息的 (請參閱[佇列觸發程序的中繼資料](#meta))。

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>佇列儲存體輸出繫結
hello Azure 佇列儲存體輸出繫結可讓您 toowrite 訊息 tooa 佇列。 

定義佇列輸出繫結使用 hello**整合**hello 函式的入口網站中的索引標籤。 hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。 Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>使用佇列輸出繫結
Node.js 函式，在您存取 hello 輸出佇列使用`context.bindings.<name>`。

在.NET 函數中，您可以將輸出 tooany hello 下列類型。 型別參數時`T`，`T`必須是其中一個支援的 hello 輸出類型，例如`string`或 POCO。

* `out T` (序列化為 JSON)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

您也可以使用 hello 方法的傳回型別為 hello 輸出繫結。

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>佇列輸出範例
hello 下列*function.json*定義與佇列 HTTP 觸發程序輸出繫結：

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

請參閱輸出 hello 連入 HTTP 裝載的佇列訊息的 hello 特定語言的範例。

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>C# 中的佇列輸出範例 #

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

toosend 多則訊息，使用`ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Node.js 中的佇列輸出範例

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

或者，toosend 多則訊息，

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>後續步驟

如需使用佇列儲存體觸發程序和繫結的函式的範例，請參閱[建立 Azure 服務的連線的 Azure 函式 tooan](functions-create-an-azure-connected-function.md)。

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
