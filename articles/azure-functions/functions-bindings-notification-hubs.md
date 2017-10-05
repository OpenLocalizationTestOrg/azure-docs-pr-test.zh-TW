---
title: "Azure Functions 通知中樞繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用「Azure 通知中樞」繫結。"
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="335c3-104">Azure Functions 通知中樞輸出繫結</span><span class="sxs-lookup"><span data-stu-id="335c3-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="335c3-105">這篇文章說明如何在 Azure Functions 中為「Azure 通知中樞」繫結進行設定及撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="335c3-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="335c3-106">您的函式可使用已設定的「Azure 通知中樞」搭配幾行程式碼來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="335c3-107">不過，「Azure 通知中樞」必須針對您要使用的「平台通知服務」(PNS) 做設定。</span><span class="sxs-lookup"><span data-stu-id="335c3-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="335c3-108">如需設定 Azure 通知中樞以及開發註冊來接收通知之用戶端應用程式的詳細資訊，請參閱 [開始使用通知中樞](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 並按一下頂端的目標用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="335c3-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="335c3-109">您傳送的通知可以是原生通知或範本通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="335c3-110">原生通知是以輸出繫結的 `platform` 屬性中所設定的特定通知平台為目標。</span><span class="sxs-lookup"><span data-stu-id="335c3-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="335c3-111">範本通知可用來以多個平台為目標。</span><span class="sxs-lookup"><span data-stu-id="335c3-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="335c3-112">通知中樞輸出繫結屬性</span><span class="sxs-lookup"><span data-stu-id="335c3-112">Notification hub output binding properties</span></span>
<span data-ttu-id="335c3-113">function.json 檔案提供下列屬性：</span><span class="sxs-lookup"><span data-stu-id="335c3-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="335c3-114">`name` ︰函式程式碼中用於通知中樞訊息的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="335c3-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="335c3-115">`type`：必須設定為 *"notificationHub"*。</span><span class="sxs-lookup"><span data-stu-id="335c3-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="335c3-116">`tagExpression` ︰標籤運算式可讓您指定將通知傳遞到一組裝置，這些裝置已註冊要接收與標籤運算式相符的通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="335c3-117">如需詳細資訊，請參閱 [路由與標籤運算式](../notification-hubs/notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="335c3-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="335c3-118">`hubName` ︰Azure 入口網站中通知中樞資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="335c3-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="335c3-119">`connection`︰此連接字串必須是設定為您通知中樞之 *DefaultFullSharedAccessSignature* 值的「應用程式設定」連接字串。</span><span class="sxs-lookup"><span data-stu-id="335c3-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="335c3-120">`direction`：必須設定為 *"out"*。</span><span class="sxs-lookup"><span data-stu-id="335c3-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="335c3-121">`platform`：此平台屬性指出作為您通知目標的通知平台。</span><span class="sxs-lookup"><span data-stu-id="335c3-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="335c3-122">必須為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="335c3-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="335c3-123">依照預設，如果輸出繫結中省略平台屬性，範本通知可用來以「Azure 通知中樞」上所設定的任何平台為目標。</span><span class="sxs-lookup"><span data-stu-id="335c3-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="335c3-124">如需有關一般使用範本搭配「Azure 通知中樞」來傳送跨平台通知的詳細資訊，請參閱[範本](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="335c3-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="335c3-125">`apns`：Apple Push Notification Service。</span><span class="sxs-lookup"><span data-stu-id="335c3-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="335c3-126">如果有關設定適用於 APNS 的通知中樞及在用戶端 App 中接收通知的詳細資訊，請參閱[使用 Azure 通知中樞將推播通知傳送至 iOS](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="335c3-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="335c3-127">`adm`：[Amazon 裝置傳訊](https://developer.amazon.com/device-messaging)。</span><span class="sxs-lookup"><span data-stu-id="335c3-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="335c3-128">如果有關設定適用於 ADM 的通知中樞及在 Kindle App 中接收通知的詳細資訊，請參閱[開始使用適用於 Kindle 應用程式的通知中樞](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="335c3-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="335c3-129">`gcm`：[Google 雲端通訊](https://developers.google.com/cloud-messaging/)。</span><span class="sxs-lookup"><span data-stu-id="335c3-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="335c3-130">也支援 Firebase Cloud Messaging (新版 GCM)。</span><span class="sxs-lookup"><span data-stu-id="335c3-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="335c3-131">如果有關設定適用於 GCM/FCM 的通知中樞及在 Android 用戶端 App 中接收通知的詳細資訊，請參閱[使用 Azure 通知中樞將推播通知傳送至 Android](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="335c3-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="335c3-132">`wns`：以 Windows 平台為目標的 [Windows 推播通知服務](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)。</span><span class="sxs-lookup"><span data-stu-id="335c3-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="335c3-133">WNS 也支援 Windows Phone 8.1 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="335c3-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="335c3-134">如果有關設定適用於 WNS 的通知中樞及在「通用 Windows 平台」(UWP) app 中接收通知的詳細資訊，請參閱[開始使用適用於 Windows 通用平台應用程式的通知中樞](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="335c3-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="335c3-135">`mpns`：[Microsoft 推播通知服務](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="335c3-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="335c3-136">此平台支援 Windows Phone 8 和舊版 Windows Phone 平台。</span><span class="sxs-lookup"><span data-stu-id="335c3-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="335c3-137">如果有關設定適用於 MPNS 的通知中樞及在 Windows Phone App 中接收通知的詳細資訊，請參閱[在 Windows Phone 上使用 Azure 通知中樞傳送推播通知](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="335c3-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="335c3-138">function.json 範例：</span><span class="sxs-lookup"><span data-stu-id="335c3-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="335c3-139">通知中樞連接字串設定</span><span class="sxs-lookup"><span data-stu-id="335c3-139">Notification hub connection string setup</span></span>
<span data-ttu-id="335c3-140">若要使用通知中樞輸出繫結，必須設定中樞的連接字串。</span><span class="sxs-lookup"><span data-stu-id="335c3-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="335c3-141">若要這麼做，只要在 [整合] 索引標籤上選取您的通知中樞或建立一個新通知中樞即可。</span><span class="sxs-lookup"><span data-stu-id="335c3-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="335c3-142">您也可以將「DefaultFullSharedAccessSignature」  新增至通知中樞，手動新增現有中樞的連接字串。</span><span class="sxs-lookup"><span data-stu-id="335c3-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="335c3-143">此連接字串提供您的函式存取權限來傳送通知訊息。</span><span class="sxs-lookup"><span data-stu-id="335c3-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="335c3-144">您可以在 Azure 入口網站中，從通知中樞資源之主要刀鋒視窗中的 [金鑰] 按鈕存取 *DefaultFullSharedAccessSignature* 連接字串值。</span><span class="sxs-lookup"><span data-stu-id="335c3-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="335c3-145">若要手動新增中樞的連接字串，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="335c3-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="335c3-146">在 Azure 入口網站的 [函數應用程式] 刀鋒視窗上，按一下 [函數應用程式設定] > [前往 App Service 設定]。</span><span class="sxs-lookup"><span data-stu-id="335c3-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="335c3-147">在 [設定] 刀鋒視窗中，按一下 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="335c3-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="335c3-148">向下捲動至 [應用程式設定] 區段，為通知中樞的 *DefaultFullSharedAccessSignature* 值新增具名項目。</span><span class="sxs-lookup"><span data-stu-id="335c3-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="335c3-149">參考輸出繫結中的應用程式設定字串名稱。</span><span class="sxs-lookup"><span data-stu-id="335c3-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="335c3-150">與上述範例中使用的 **MyHubConnectionString** 類似。</span><span class="sxs-lookup"><span data-stu-id="335c3-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="335c3-151">含 C# 佇列觸發程序的 APNS 原生通知</span><span class="sxs-lookup"><span data-stu-id="335c3-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="335c3-152">這個範例示範如何使用 [Microsoft Azure 通知中樞程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)中定義的類型來傳送原生 APNS 通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="335c3-153">含 C# 佇列觸發程序的 GCM 原生通知</span><span class="sxs-lookup"><span data-stu-id="335c3-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="335c3-154">這個範例示範如何使用 [Microsoft Azure 通知中樞程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)中定義的類型來傳送原生 GCM 通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="335c3-155">含 C# 佇列觸發程序的 WNS 原生通知</span><span class="sxs-lookup"><span data-stu-id="335c3-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="335c3-156">這個範例示範如何使用 [Microsoft Azure 通知中樞程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)中定義的類型來傳送原生 WNS 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="335c3-157">Node.js 計時器觸發程序的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="335c3-158">這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="335c3-159">F# 計時器觸發程序的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="335c3-160">這個範例會傳送包含 `location` 和 `message` 的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="335c3-161">使用 out 參數的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-161">Template example using an out parameter</span></span>
<span data-ttu-id="335c3-162">這個範例會傳送在範本中包含 `message` 預留位置的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="335c3-163">含非同步函式的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-163">Template example with asynchronous function</span></span>
<span data-ttu-id="335c3-164">如果您使用非同步程式碼，則不允許使用 out 參數。</span><span class="sxs-lookup"><span data-stu-id="335c3-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="335c3-165">在此情況下，請使用 `IAsyncCollector` 來傳回您的範本通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="335c3-166">下列程式碼是上述程式碼的非同步範例。</span><span class="sxs-lookup"><span data-stu-id="335c3-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="335c3-167">使用 JSON 的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-167">Template example using JSON</span></span>
<span data-ttu-id="335c3-168">這個範例會使用有效的 JSON 字串來傳送在範本中包含 `message` 預留位置的[範本註冊](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="335c3-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="335c3-169">使用通知中樞程式庫類型的範本範例</span><span class="sxs-lookup"><span data-stu-id="335c3-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="335c3-170">這個範例示範如何使用 [Microsoft Azure 通知中樞程式庫](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)中定義的類型。</span><span class="sxs-lookup"><span data-stu-id="335c3-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="335c3-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="335c3-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

