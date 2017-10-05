---
title: "Azure Functions 計時器觸發程序 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用計時器觸發程序。"
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="bdfd6-104">Azure Functions 計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="bdfd6-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="bdfd6-105">這篇文章說明如何在 Azure Functions 中設定及撰寫計時器觸發程序。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="bdfd6-106">Azure Functions 具有計時器觸發程序繫結，可讓您根據所定義的排程執行函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="bdfd6-107">計時器觸發程序支援多個執行個體向外延展。特定計時器函式的單一執行個體會對所有執行個體執行。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="bdfd6-108">計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="bdfd6-108">Timer trigger</span></span>
<span data-ttu-id="bdfd6-109">函式的計時器觸發程序會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="bdfd6-110">`schedule` 的值是包含以下 6 個欄位的 [CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="bdfd6-111">您會在線上找到的許多 cron 運算式會省略 `{second}` 欄位。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="bdfd6-112">如果您從中複製一個，您需要對 `{second}` 欄位進行額外調整。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="bdfd6-113">如需特定範例，請參閱以下的[排程範例](#examples)。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="bdfd6-114">CRON 運算式使用的預設時區是國際標準時間 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="bdfd6-115">若要讓 CRON 運算式以另一個時區為基礎，請為名為 `WEBSITE_TIME_ZONE` 的函式應用程式建立新的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="bdfd6-116">將值設定為所需的時區名稱，如 [Microsoft 時區索引](https://msdn.microsoft.com/library/ms912391.aspx)中所示。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="bdfd6-117">例如，*美加東部標準時間*是 UTC-05:00。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="bdfd6-118">若要讓計時器觸發程序在每天上午 10:00 (美加東部標準時間) 觸發，您可以使用說明 UTC 時區的下列 CRON 運算式︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="bdfd6-119">或者，您可以為名為 `WEBSITE_TIME_ZONE` 的函式應用程式新增新的應用程式設定，並將值設為**美加東部標準時間**。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="bdfd6-120">那麼，下列 CRON 運算式即可用於 EST 上午 10:00：</span><span class="sxs-lookup"><span data-stu-id="bdfd6-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="bdfd6-121">排程範例</span><span class="sxs-lookup"><span data-stu-id="bdfd6-121">Schedule examples</span></span>
<span data-ttu-id="bdfd6-122">以下是您可以用於 `schedule` 屬性的 CRON 運算式的一些範例。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="bdfd6-123">若要每隔 5 分鐘觸發一次︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="bdfd6-124">若要在每小時開始時觸發一次︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="bdfd6-125">若要每隔 2 小時觸發一次：</span><span class="sxs-lookup"><span data-stu-id="bdfd6-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="bdfd6-126">若要在上午 9 點到下午 5 點之間每隔一小時觸發一次：</span><span class="sxs-lookup"><span data-stu-id="bdfd6-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="bdfd6-127">若要在每天上午 9:30 觸發一次：</span><span class="sxs-lookup"><span data-stu-id="bdfd6-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="bdfd6-128">若要在每個工作天上午 9:30 觸發一次：</span><span class="sxs-lookup"><span data-stu-id="bdfd6-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="bdfd6-129">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="bdfd6-129">Trigger usage</span></span>
<span data-ttu-id="bdfd6-130">叫用計時器觸發程序函式時，[計時器物件](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs)會傳遞至函式。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="bdfd6-131">下列 JSON 是計時器物件的範例表示法。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="bdfd6-132">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="bdfd6-132">Trigger sample</span></span>
<span data-ttu-id="bdfd6-133">假設您的 function.json `bindings` 陣列中有下列計時器觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="bdfd6-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="bdfd6-134">請參閱可讀取計時器物件，以查看是否晚執行的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="bdfd6-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="bdfd6-135">C#</span><span class="sxs-lookup"><span data-stu-id="bdfd6-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="bdfd6-136">F#</span><span class="sxs-lookup"><span data-stu-id="bdfd6-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="bdfd6-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="bdfd6-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="bdfd6-138">C# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="bdfd6-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="bdfd6-139">F# 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="bdfd6-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="bdfd6-140">Node.js 中的觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="bdfd6-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="bdfd6-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bdfd6-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

