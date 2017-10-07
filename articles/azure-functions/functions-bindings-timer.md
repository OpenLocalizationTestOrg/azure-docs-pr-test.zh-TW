---
title: "aaaAzure 函式計時器觸發程序 |Microsoft 文件"
description: "了解 toouse 計時器觸發程序在 Azure 函式。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a>Azure Functions 計時器觸發程序

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

本文說明 tooconfigure 和程式碼的計時器觸發程序在 Azure 函式。 Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。 

hello 計時器觸發程序支援向外延展多重執行個體。特定計時器函式的單一執行個體會對所有執行個體執行。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>計時器觸發程序
hello 計時器觸發程序 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

hello 值`schedule`是[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)包含下列六個欄位： 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>許多線上找到 hello cron 運算式省略 hello`{second}`欄位。 如果您複製的其中一個，您需要額外的 hello tooadjust`{second}`欄位。 如需特定範例，請參閱以下的[排程範例](#examples)。

hello 與 hello CRON 運算式一起使用的預設時間區域是國際標準時間 (UTC)。 toohave CRON 運算式會根據另一個時區，建立名為函式應用程式的新應用程式設定`WEBSITE_TIME_ZONE`。 需要時區組 hello 值 toohello 名稱的 hello hello 中所示[Microsoft 時區索引](https://msdn.microsoft.com/library/ms912391.aspx)。 

例如，*美加東部標準時間*是 UTC-05:00。 toohave 計時器觸發引發在 10:00 AM EST 每一天，下列帳戶 UTC 時區為準的 CRON 運算式使用 hello:

```json
"schedule": "0 0 15 * * *",
``` 

或者，您可以加入新的應用程式設定名為應用程式函式`WEBSITE_TIME_ZONE`並將 hello 值設定為太**美加東部標準時間**。  然後 hello 下列 CRON 運算式無法用於 10:00 AM EST: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>排程範例
以下是一些您可以使用 hello CRON 運算式的範例`schedule`屬性。 

tootrigger 一次每隔五分鐘：

```json
"schedule": "0 */5 * * * *"
```

在 hello 頂端每小時執行一次 tootrigger:

```json
"schedule": "0 0 * * * *",
```

tootrigger 一次每隔兩小時：

```json
"schedule": "0 0 */2 * * *",
```

每小時從上午 9 點 too5 tootrigger PM:

```json
"schedule": "0 0 9-17 * * *",
```

在每一天的上午 9:30 tootrigger:

```json
"schedule": "0 30 9 * * *",
```

在每個工作天的上午 9:30 tootrigger:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>觸發程序使用方式
當計時器觸發程序函式會叫用時，hello[計時器物件](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs)傳入 hello 函式。 hello 下列 JSON 是 hello 計時器物件的範例表示法。 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列計時器觸發程序在 hello hello `bindings` function.json 的陣列：

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

查看可讀取 hello 計時器物件 toosee 是否正在執行晚期 hello 特定語言的範例。

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>C# 中的觸發程序範例 #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>F# 中的觸發程序範例 #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js 中的觸發程序範例
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

