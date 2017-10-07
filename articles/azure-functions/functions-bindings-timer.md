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
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="e5750-104">Azure Functions 計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="e5750-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e5750-105">本文說明 tooconfigure 和程式碼的計時器觸發程序在 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="e5750-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="e5750-106">Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="e5750-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="e5750-107">hello 計時器觸發程序支援向外延展多重執行個體。特定計時器函式的單一執行個體會對所有執行個體執行。</span><span class="sxs-lookup"><span data-stu-id="e5750-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="e5750-108">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="e5750-108">Timer trigger</span></span>
<span data-ttu-id="e5750-109">hello 計時器觸發程序 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="e5750-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e5750-110">hello 值`schedule`是[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)包含下列六個欄位：</span><span class="sxs-lookup"><span data-stu-id="e5750-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="e5750-111">許多線上找到 hello cron 運算式省略 hello`{second}`欄位。</span><span class="sxs-lookup"><span data-stu-id="e5750-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="e5750-112">如果您複製的其中一個，您需要額外的 hello tooadjust`{second}`欄位。</span><span class="sxs-lookup"><span data-stu-id="e5750-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="e5750-113">如需特定範例，請參閱以下的[排程範例](#examples)。</span><span class="sxs-lookup"><span data-stu-id="e5750-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="e5750-114">hello 與 hello CRON 運算式一起使用的預設時間區域是國際標準時間 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="e5750-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="e5750-115">toohave CRON 運算式會根據另一個時區，建立名為函式應用程式的新應用程式設定`WEBSITE_TIME_ZONE`。</span><span class="sxs-lookup"><span data-stu-id="e5750-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="e5750-116">需要時區組 hello 值 toohello 名稱的 hello hello 中所示[Microsoft 時區索引](https://msdn.microsoft.com/library/ms912391.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5750-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="e5750-117">例如，*美加東部標準時間*是 UTC-05:00。</span><span class="sxs-lookup"><span data-stu-id="e5750-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="e5750-118">toohave 計時器觸發引發在 10:00 AM EST 每一天，下列帳戶 UTC 時區為準的 CRON 運算式使用 hello:</span><span class="sxs-lookup"><span data-stu-id="e5750-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="e5750-119">或者，您可以加入新的應用程式設定名為應用程式函式`WEBSITE_TIME_ZONE`並將 hello 值設定為太**美加東部標準時間**。</span><span class="sxs-lookup"><span data-stu-id="e5750-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="e5750-120">然後 hello 下列 CRON 運算式無法用於 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="e5750-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="e5750-121">排程範例</span><span class="sxs-lookup"><span data-stu-id="e5750-121">Schedule examples</span></span>
<span data-ttu-id="e5750-122">以下是一些您可以使用 hello CRON 運算式的範例`schedule`屬性。</span><span class="sxs-lookup"><span data-stu-id="e5750-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="e5750-123">tootrigger 一次每隔五分鐘：</span><span class="sxs-lookup"><span data-stu-id="e5750-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="e5750-124">在 hello 頂端每小時執行一次 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="e5750-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="e5750-125">tootrigger 一次每隔兩小時：</span><span class="sxs-lookup"><span data-stu-id="e5750-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="e5750-126">每小時從上午 9 點 too5 tootrigger PM:</span><span class="sxs-lookup"><span data-stu-id="e5750-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="e5750-127">在每一天的上午 9:30 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="e5750-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="e5750-128">在每個工作天的上午 9:30 tootrigger:</span><span class="sxs-lookup"><span data-stu-id="e5750-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e5750-129">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="e5750-129">Trigger usage</span></span>
<span data-ttu-id="e5750-130">當計時器觸發程序函式會叫用時，hello[計時器物件](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs)傳入 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="e5750-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="e5750-131">hello 下列 JSON 是 hello 計時器物件的範例表示法。</span><span class="sxs-lookup"><span data-stu-id="e5750-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="e5750-132">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e5750-132">Trigger sample</span></span>
<span data-ttu-id="e5750-133">假設您有下列計時器觸發程序在 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="e5750-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e5750-134">查看可讀取 hello 計時器物件 toosee 是否正在執行晚期 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="e5750-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="e5750-135">C#</span><span class="sxs-lookup"><span data-stu-id="e5750-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e5750-136">F#</span><span class="sxs-lookup"><span data-stu-id="e5750-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="e5750-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="e5750-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e5750-138">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e5750-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="e5750-139">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e5750-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e5750-140">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="e5750-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="e5750-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5750-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

