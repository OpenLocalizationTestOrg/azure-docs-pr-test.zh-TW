---
title: "Azure Functions Twilio 繫結 | Microsoft Docs"
description: "了解如何搭配使用 Twilio 繫結與 Azure Functions。"
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
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="e0606-104">使用 Twilio 輸出繫結從 Azure Functions 傳送手機訊息</span><span class="sxs-lookup"><span data-stu-id="e0606-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e0606-105">本文說明如何設定 Twilio 繫結，以及其如何與 Azure Functions 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e0606-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="e0606-106">Azure Functions 支援 Twilio 輸出繫結，讓函式傳送具有數行程式碼和一個 [Twilio](https://www.twilio.com/) 帳戶的 SMS 文字訊息。</span><span class="sxs-lookup"><span data-stu-id="e0606-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="e0606-107">適用於 Twilio 輸出繫結的 function.json</span><span class="sxs-lookup"><span data-stu-id="e0606-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="e0606-108">function.json 檔案提供下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e0606-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="e0606-109">`name`︰用於 Twilio 簡訊文字訊息之函式程式碼中的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="e0606-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="e0606-110">`type`：必須設定為 *"twilioSms"*。</span><span class="sxs-lookup"><span data-stu-id="e0606-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="e0606-111">`accountSid`︰此值必須設定為保留您 Twilio 帳戶 Sid 的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="e0606-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="e0606-112">`authToken`︰此值必須設定為保留您 Twilio 驗證權杖的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="e0606-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="e0606-113">`to`︰此值設定為簡訊文字傳送至的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="e0606-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="e0606-114">`from`︰此值設定為從中傳送簡訊文字的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="e0606-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="e0606-115">`direction`：必須設為 *"out"*。</span><span class="sxs-lookup"><span data-stu-id="e0606-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="e0606-116">`body`︰如果您不需要在函式程式碼中動態設定 SMS 文字訊息，則此值可以用來硬式編碼 SMS 文字訊息。</span><span class="sxs-lookup"><span data-stu-id="e0606-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="e0606-117">function.json 範例：</span><span class="sxs-lookup"><span data-stu-id="e0606-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="e0606-118">具有 Twilio 輸出繫結的範例 C# 佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="e0606-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="e0606-119">同步</span><span class="sxs-lookup"><span data-stu-id="e0606-119">Synchronous</span></span>
<span data-ttu-id="e0606-120">Azure 儲存體佇列觸發程序的這個同步範例程式碼會使用 out 參數，將文字訊息傳送給下單的客戶。</span><span class="sxs-lookup"><span data-stu-id="e0606-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="e0606-121">非同步</span><span class="sxs-lookup"><span data-stu-id="e0606-121">Asynchronous</span></span>
<span data-ttu-id="e0606-122">Azure 儲存體佇列觸發程序的這個非同步範例程式碼會將文字訊息傳送給下單的客戶。</span><span class="sxs-lookup"><span data-stu-id="e0606-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="e0606-123">具有 Twilio 輸出繫結的範例 Node.js 佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="e0606-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="e0606-124">這個 Node.js 範例會將文字訊息傳送給下單的客戶。</span><span class="sxs-lookup"><span data-stu-id="e0606-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e0606-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0606-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

