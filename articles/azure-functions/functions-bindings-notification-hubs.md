---
title: "aaaAzure 函式的通知中樞繫結 |Microsoft 文件"
description: "了解如何在 Azure 函式 toouse Azure 通知中樞繫結。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Azure Functions 通知中樞輸出繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何在 Azure 函式的 tooconfigure 和程式碼 Azure 通知中樞繫結。 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

您的函式可使用已設定的「Azure 通知中樞」搭配幾行程式碼來傳送推播通知。 不過，平台通知服務 (PNS) 想 toouse hello 必須設定 hello Azure 通知中樞。 如需有關設定 Azure 通知中樞及開發註冊 tooreceive 通知用戶端應用程式的詳細資訊，請參閱[開始使用通知中心](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)按一下目標用戶端在 hello 平台top。

您傳送嗨通知可以是原生通知或範本的通知。 原生通知特定通知平台設為目標來設定在 hello`platform`屬性 hello 輸出繫結。 範本通知可使用的 tootarget 多個平台。   

## <a name="notification-hub-output-binding-properties"></a>通知中樞輸出繫結屬性
hello function.json 檔案提供 hello 下列屬性：

* `name`： 用於 hello 通知中樞訊息函式程式碼變數的名稱。
* `type`： 必須設定得*"notificationHub"*。
* `tagExpression`： 標記運算式可讓您 toospecify，傳遞通知 tooa 整組裝置已註冊與 hello 標記運算式相符的 tooreceive 通知使用者。  如需詳細資訊，請參閱 [路由與標籤運算式](../notification-hubs/notification-hubs-tags-segment-push-message.md)。
* `hubName`: Hello Azure 入口網站中的 hello 通知中樞資源名稱。
* `connection`： 這個連接字串必須是**應用程式設定**連接字串設定 toohello *DefaultFullSharedAccessSignature*通知中樞的值。
* `direction`： 必須設定得*"out"*。 
* `platform`: hello 平台屬性表示 hello 通知平台通知目標。 必須是 hello 的下列值的其中一個：
  * 根據預設，如果 hello 平台屬性繫結的 hello 輸出中會省略範本通知可以使用的 tootarget hello Azure 通知中樞的任何平台設定。 如需有關一般使用範本 toosend 跨平台通知與 Azure 通知中樞，請參閱[範本](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)。
  * `apns`：Apple Push Notification Service。 如需有關設定適用於 APNS 的 hello 通知中樞和用戶端應用程式中收到 hello 通知的詳細資訊，請參閱[傳送推播通知 tooiOS 與 Azure 通知中心](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`：[Amazon 裝置傳訊](https://developer.amazon.com/device-messaging)。 如需有關設定 ADM hello 通知中樞，並用於 Kindle 應用程式中收到 hello 通知的詳細資訊，請參閱[入門 Kindle 應用程式的通知中樞](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`：[Google 雲端通訊](https://developers.google.com/cloud-messaging/)。 也支援 firebase Cloud Messaging，也就是 GCM hello 新版本。 如需有關設定 GCM/FCM hello 通知中樞及 Android 用戶端應用程式中收到 hello 通知的詳細資訊，請參閱[傳送推播通知 tooAndroid 與 Azure 通知中心](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`：以 Windows 平台為目標的 [Windows 推播通知服務](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)。 WNS 也支援 Windows Phone 8.1 和更新版本。 如需有關設定適用於 WNS hello 通知中樞和通用 Windows 平台 (UWP) 應用程式中收到 hello 通知的詳細資訊，請參閱[開始使用通知中樞為 Windows 通用平台應用程式](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`：[Microsoft 推播通知服務](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx)。 此平台支援 Windows Phone 8 和舊版 Windows Phone 平台。 如需有關設定 MPNS 的 hello 通知中樞與 Windows Phone 應用程式中收到 hello 通知的詳細資訊，請參閱[與 Windows Phone 上的 Azure 通知中樞傳送推播通知](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

function.json 範例：

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>通知中樞連接字串設定
通知中樞 toouse 輸出繫結，您必須設定 hello hello 中樞連接字串。 這可以在 hello*整合*藉由選取您的通知中樞，或建立新的索引標籤。 

您可以手動加入將加入現有中樞的連接字串 hello 的連接字串*DefaultFullSharedAccessSignature* tooyour 通知中樞。 這個連接字串提供您函式的存取權限 toosend 通知訊息。 hello *DefaultFullSharedAccessSignature*可以存取連接字串值，從 hello**金鑰**hello 通知中樞資源 hello Azure 入口網站中的 [主要] 刀鋒視窗中的按鈕。 toomanually 加入您的中樞，下列步驟使用 hello 的連接字串： 

1. 在 hello**函式應用程式**刀鋒視窗中的 hello Azure 入口網站中，按一下**函式應用程式的設定 > 移 tooApp 服務設定**。
2. 在 hello**設定**刀鋒視窗中，按一下 **應用程式設定**。
3. 捲動 toohello**應用程式設定**區段，然後新增的具名項目*DefaultFullSharedAccessSignature*通知中樞的值。
4. 請參考您的應用程式設定中 hello 輸出繫結的字串名稱。 類似太**MyHubConnectionString** hello 上述範例中使用。

## <a name="apns-native-notifications-with-c-queue-triggers"></a>含 C# 佇列觸發程序的 APNS 原生通知
此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 APNS 通知。 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>含 C# 佇列觸發程序的 GCM 原生通知
此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 GCM 通知。 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>含 C# 佇列觸發程序的 WNS 原生通知
此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 WNS 快顯通知。 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Node.js 計時器觸發程序的範本範例
這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>F# 計時器觸發程序的範本範例
這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>使用 out 參數的範本範例
這個範例會將通知傳送[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)包含`message`hello 範本中的預留位置。

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>含非同步函式的範本範例
如果您使用非同步程式碼，則不允許使用 out 參數。 在此情況下使用`IAsyncCollector`tooreturn 範本通知。 hello 下列程式碼是非同步的 hello 上述的程式碼範例。 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>使用 JSON 的範本範例
這個範例會將通知傳送[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)包含`message`hello 範本使用有效的 JSON 字串中的預留位置。

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>使用通知中樞程式庫類型的範本範例
此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

