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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>傳送 SMS 訊息從 Azure 函式使用 hello Twilio 輸出繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何搭配 Azure 函式的 tooconfigure 和使用 Twilio 繫結。 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Azure 的函式支援 Twilio 輸出繫結 tooenable 幾行程式碼的函式 toosend SMS 文字訊息和[Twilio](https://www.twilio.com/)帳戶。 

## <a name="functionjson-for-hello-twilio-output-binding"></a>hello function.json Twilio 輸出繫結
hello function.json 檔案提供 hello 下列屬性：

* `name`： 函式程式碼中使用 hello Twilio SMS 文字訊息為變數的名稱。
* `type`： 必須設定得*"twilioSms"*。
* `accountSid`： 這個值必須設定應用程式設定會保存您 Twilio 帳戶 Sid toohello 名稱。
* `authToken`： 這個值必須設定 toohello 保存您的 Twilio 驗證權杖的應用程式設定名稱。
* `to`： 這個值會設定 toohello hello 簡訊傳送到的電話號碼。
* `from`： 這個值會設定從傳送嗨 SMS 文字 toohello 電話號碼。
* `direction`： 必須設定得*"out"*。
* `body`： 這個值可以是使用的 toohard 代碼 hello SMS 文字訊息，如果您不需要以動態方式在 hello 程式碼的 tooset 那麼函式。 

function.json 範例：

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>具有 Twilio 輸出繫結的範例 C# 佇列觸發程序
#### <a name="synchronous"></a>同步
此同步的範例程式碼的 Azure 儲存體佇列觸發程序會使用 out 參數 toosend 的文字訊息 tooa 客戶下訂單。

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

#### <a name="asynchronous"></a>非同步
Azure 儲存體佇列的觸發程序的這個非同步的範例程式碼會將傳送的文字訊息 tooa 客戶下訂單。

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>具有 Twilio 輸出繫結的範例 Node.js 佇列觸發程序
Node.js 本例傳送的文字訊息 tooa 客戶下訂單。

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

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

