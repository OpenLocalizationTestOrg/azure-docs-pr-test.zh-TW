---
title: "aaaAzure Twilio 函式繫結 |Microsoft 文件"
description: "了解如何搭配 Azure 函式 toouse Twilio 繫結。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="b537b-104">傳送 SMS 訊息從 Azure 函式使用 hello Twilio 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b537b-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b537b-105">這篇文章說明如何搭配 Azure 函式的 tooconfigure 和使用 Twilio 繫結。</span><span class="sxs-lookup"><span data-stu-id="b537b-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="b537b-106">Azure 的函式支援 Twilio 輸出繫結 tooenable 幾行程式碼的函式 toosend SMS 文字訊息和[Twilio](https://www.twilio.com/)帳戶。</span><span class="sxs-lookup"><span data-stu-id="b537b-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="b537b-107">hello function.json Twilio 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b537b-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="b537b-108">hello function.json 檔案提供 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b537b-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="b537b-109">`name`： 函式程式碼中使用 hello Twilio SMS 文字訊息為變數的名稱。</span><span class="sxs-lookup"><span data-stu-id="b537b-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="b537b-110">`type`： 必須設定得*"twilioSms"*。</span><span class="sxs-lookup"><span data-stu-id="b537b-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="b537b-111">`accountSid`： 這個值必須設定應用程式設定會保存您 Twilio 帳戶 Sid toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b537b-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="b537b-112">`authToken`： 這個值必須設定 toohello 保存您的 Twilio 驗證權杖的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="b537b-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="b537b-113">`to`： 這個值會設定 toohello hello 簡訊傳送到的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="b537b-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="b537b-114">`from`： 這個值會設定從傳送嗨 SMS 文字 toohello 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="b537b-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="b537b-115">`direction`： 必須設定得*"out"*。</span><span class="sxs-lookup"><span data-stu-id="b537b-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="b537b-116">`body`： 這個值可以是使用的 toohard 代碼 hello SMS 文字訊息，如果您不需要以動態方式在 hello 程式碼的 tooset 那麼函式。</span><span class="sxs-lookup"><span data-stu-id="b537b-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="b537b-117">function.json 範例：</span><span class="sxs-lookup"><span data-stu-id="b537b-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="b537b-118">具有 Twilio 輸出繫結的範例 C# 佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="b537b-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="b537b-119">同步</span><span class="sxs-lookup"><span data-stu-id="b537b-119">Synchronous</span></span>
<span data-ttu-id="b537b-120">此同步的範例程式碼的 Azure 儲存體佇列觸發程序會使用 out 參數 toosend 的文字訊息 tooa 客戶下訂單。</span><span class="sxs-lookup"><span data-stu-id="b537b-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="b537b-121">非同步</span><span class="sxs-lookup"><span data-stu-id="b537b-121">Asynchronous</span></span>
<span data-ttu-id="b537b-122">Azure 儲存體佇列的觸發程序的這個非同步的範例程式碼會將傳送的文字訊息 tooa 客戶下訂單。</span><span class="sxs-lookup"><span data-stu-id="b537b-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="b537b-123">具有 Twilio 輸出繫結的範例 Node.js 佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="b537b-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="b537b-124">Node.js 本例傳送的文字訊息 tooa 客戶下訂單。</span><span class="sxs-lookup"><span data-stu-id="b537b-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b537b-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b537b-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

