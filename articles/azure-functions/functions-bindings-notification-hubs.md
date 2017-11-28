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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="28570-104">Azure Functions 通知中樞輸出繫結</span><span class="sxs-lookup"><span data-stu-id="28570-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="28570-105">這篇文章說明如何在 Azure 函式的 tooconfigure 和程式碼 Azure 通知中樞繫結。</span><span class="sxs-lookup"><span data-stu-id="28570-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="28570-106">您的函式可使用已設定的「Azure 通知中樞」搭配幾行程式碼來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="28570-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="28570-107">不過，平台通知服務 (PNS) 想 toouse hello 必須設定 hello Azure 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="28570-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="28570-108">如需有關設定 Azure 通知中樞及開發註冊 tooreceive 通知用戶端應用程式的詳細資訊，請參閱[開始使用通知中心](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)按一下目標用戶端在 hello 平台top。</span><span class="sxs-lookup"><span data-stu-id="28570-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="28570-109">您傳送嗨通知可以是原生通知或範本的通知。</span><span class="sxs-lookup"><span data-stu-id="28570-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="28570-110">原生通知特定通知平台設為目標來設定在 hello`platform`屬性 hello 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="28570-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="28570-111">範本通知可使用的 tootarget 多個平台。</span><span class="sxs-lookup"><span data-stu-id="28570-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="28570-112">通知中樞輸出繫結屬性</span><span class="sxs-lookup"><span data-stu-id="28570-112">Notification hub output binding properties</span></span>
<span data-ttu-id="28570-113">hello function.json 檔案提供 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="28570-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="28570-114">`name`： 用於 hello 通知中樞訊息函式程式碼變數的名稱。</span><span class="sxs-lookup"><span data-stu-id="28570-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="28570-115">`type`： 必須設定得*"notificationHub"*。</span><span class="sxs-lookup"><span data-stu-id="28570-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="28570-116">`tagExpression`： 標記運算式可讓您 toospecify，傳遞通知 tooa 整組裝置已註冊與 hello 標記運算式相符的 tooreceive 通知使用者。</span><span class="sxs-lookup"><span data-stu-id="28570-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="28570-117">如需詳細資訊，請參閱 [路由與標籤運算式](../notification-hubs/notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="28570-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="28570-118">`hubName`: Hello Azure 入口網站中的 hello 通知中樞資源名稱。</span><span class="sxs-lookup"><span data-stu-id="28570-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="28570-119">`connection`： 這個連接字串必須是**應用程式設定**連接字串設定 toohello *DefaultFullSharedAccessSignature*通知中樞的值。</span><span class="sxs-lookup"><span data-stu-id="28570-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="28570-120">`direction`： 必須設定得*"out"*。</span><span class="sxs-lookup"><span data-stu-id="28570-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="28570-121">`platform`: hello 平台屬性表示 hello 通知平台通知目標。</span><span class="sxs-lookup"><span data-stu-id="28570-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="28570-122">必須是 hello 的下列值的其中一個：</span><span class="sxs-lookup"><span data-stu-id="28570-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="28570-123">根據預設，如果 hello 平台屬性繫結的 hello 輸出中會省略範本通知可以使用的 tootarget hello Azure 通知中樞的任何平台設定。</span><span class="sxs-lookup"><span data-stu-id="28570-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="28570-124">如需有關一般使用範本 toosend 跨平台通知與 Azure 通知中樞，請參閱[範本](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="28570-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="28570-125">`apns`：Apple Push Notification Service。</span><span class="sxs-lookup"><span data-stu-id="28570-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="28570-126">如需有關設定適用於 APNS 的 hello 通知中樞和用戶端應用程式中收到 hello 通知的詳細資訊，請參閱[傳送推播通知 tooiOS 與 Azure 通知中心](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="28570-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="28570-127">`adm`：[Amazon 裝置傳訊](https://developer.amazon.com/device-messaging)。</span><span class="sxs-lookup"><span data-stu-id="28570-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="28570-128">如需有關設定 ADM hello 通知中樞，並用於 Kindle 應用程式中收到 hello 通知的詳細資訊，請參閱[入門 Kindle 應用程式的通知中樞](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="28570-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="28570-129">`gcm`：[Google 雲端通訊](https://developers.google.com/cloud-messaging/)。</span><span class="sxs-lookup"><span data-stu-id="28570-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="28570-130">也支援 firebase Cloud Messaging，也就是 GCM hello 新版本。</span><span class="sxs-lookup"><span data-stu-id="28570-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="28570-131">如需有關設定 GCM/FCM hello 通知中樞及 Android 用戶端應用程式中收到 hello 通知的詳細資訊，請參閱[傳送推播通知 tooAndroid 與 Azure 通知中心](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="28570-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="28570-132">`wns`：以 Windows 平台為目標的 [Windows 推播通知服務](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)。</span><span class="sxs-lookup"><span data-stu-id="28570-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="28570-133">WNS 也支援 Windows Phone 8.1 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="28570-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="28570-134">如需有關設定適用於 WNS hello 通知中樞和通用 Windows 平台 (UWP) 應用程式中收到 hello 通知的詳細資訊，請參閱[開始使用通知中樞為 Windows 通用平台應用程式](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="28570-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="28570-135">`mpns`：[Microsoft 推播通知服務](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28570-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="28570-136">此平台支援 Windows Phone 8 和舊版 Windows Phone 平台。</span><span class="sxs-lookup"><span data-stu-id="28570-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="28570-137">如需有關設定 MPNS 的 hello 通知中樞與 Windows Phone 應用程式中收到 hello 通知的詳細資訊，請參閱[與 Windows Phone 上的 Azure 通知中樞傳送推播通知](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="28570-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="28570-138">function.json 範例：</span><span class="sxs-lookup"><span data-stu-id="28570-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="28570-139">通知中樞連接字串設定</span><span class="sxs-lookup"><span data-stu-id="28570-139">Notification hub connection string setup</span></span>
<span data-ttu-id="28570-140">通知中樞 toouse 輸出繫結，您必須設定 hello hello 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="28570-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="28570-141">這可以在 hello*整合*藉由選取您的通知中樞，或建立新的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="28570-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="28570-142">您可以手動加入將加入現有中樞的連接字串 hello 的連接字串*DefaultFullSharedAccessSignature* tooyour 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="28570-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="28570-143">這個連接字串提供您函式的存取權限 toosend 通知訊息。</span><span class="sxs-lookup"><span data-stu-id="28570-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="28570-144">hello *DefaultFullSharedAccessSignature*可以存取連接字串值，從 hello**金鑰**hello 通知中樞資源 hello Azure 入口網站中的 [主要] 刀鋒視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="28570-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="28570-145">toomanually 加入您的中樞，下列步驟使用 hello 的連接字串：</span><span class="sxs-lookup"><span data-stu-id="28570-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="28570-146">在 hello**函式應用程式**刀鋒視窗中的 hello Azure 入口網站中，按一下**函式應用程式的設定 > 移 tooApp 服務設定**。</span><span class="sxs-lookup"><span data-stu-id="28570-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="28570-147">在 hello**設定**刀鋒視窗中，按一下 **應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="28570-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="28570-148">捲動 toohello**應用程式設定**區段，然後新增的具名項目*DefaultFullSharedAccessSignature*通知中樞的值。</span><span class="sxs-lookup"><span data-stu-id="28570-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="28570-149">請參考您的應用程式設定中 hello 輸出繫結的字串名稱。</span><span class="sxs-lookup"><span data-stu-id="28570-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="28570-150">類似太**MyHubConnectionString** hello 上述範例中使用。</span><span class="sxs-lookup"><span data-stu-id="28570-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="28570-151">含 C# 佇列觸發程序的 APNS 原生通知</span><span class="sxs-lookup"><span data-stu-id="28570-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="28570-152">此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 APNS 通知。</span><span class="sxs-lookup"><span data-stu-id="28570-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="28570-153">含 C# 佇列觸發程序的 GCM 原生通知</span><span class="sxs-lookup"><span data-stu-id="28570-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="28570-154">此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 GCM 通知。</span><span class="sxs-lookup"><span data-stu-id="28570-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="28570-155">含 C# 佇列觸發程序的 WNS 原生通知</span><span class="sxs-lookup"><span data-stu-id="28570-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="28570-156">此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)toosend 原生 WNS 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="28570-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="28570-157">Node.js 計時器觸發程序的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="28570-158">這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="28570-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="28570-159">F# 計時器觸發程序的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="28570-160">這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="28570-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="28570-161">使用 out 參數的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-161">Template example using an out parameter</span></span>
<span data-ttu-id="28570-162">這個範例會將通知傳送[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)包含`message`hello 範本中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="28570-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="28570-163">含非同步函式的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-163">Template example with asynchronous function</span></span>
<span data-ttu-id="28570-164">如果您使用非同步程式碼，則不允許使用 out 參數。</span><span class="sxs-lookup"><span data-stu-id="28570-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="28570-165">在此情況下使用`IAsyncCollector`tooreturn 範本通知。</span><span class="sxs-lookup"><span data-stu-id="28570-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="28570-166">hello 下列程式碼是非同步的 hello 上述的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="28570-166">hello following code is an asynchronous example of hello code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="28570-167">使用 JSON 的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-167">Template example using JSON</span></span>
<span data-ttu-id="28570-168">這個範例會將通知傳送[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)包含`message`hello 範本使用有效的 JSON 字串中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="28570-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="28570-169">使用通知中樞程式庫類型的範本範例</span><span class="sxs-lookup"><span data-stu-id="28570-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="28570-170">此範例示範如何 toouse 類型定義中 hello [Microsoft Azure 通知中心程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="28570-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="28570-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28570-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

