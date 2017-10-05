---
title: "使用 Azure App Service 將推播通知新增至 Xamarin.iOS 應用程式"
description: "了解如何使用 Azure App Service 將推播通知傳送至 Xamarin.iOS 應用程式。"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="6c0ea-103">將推播通知新增至 Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="6c0ea-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="6c0ea-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6c0ea-104">Overview</span></span>
<span data-ttu-id="6c0ea-105">在本教學課程中，您會將推播通知新增至 [Xamarin.iOS 快速入門](app-service-mobile-xamarin-ios-get-started.md)專案，以便在每次插入一筆記錄時傳送推播通知至裝置。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="6c0ea-106">如果您不要使用下載的快速入門伺服器專案，將需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="6c0ea-107">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c0ea-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c0ea-108">Prerequisites</span></span>
* <span data-ttu-id="6c0ea-109">完成 [建立 Xamarin.iOS 應用程式](app-service-mobile-xamarin-ios-get-started.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="6c0ea-110">實體的 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-110">A physical iOS device.</span></span> <span data-ttu-id="6c0ea-111">iOS 模擬器不支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="6c0ea-112">在 Apple 的開發人員入口網站註冊應用程式以取得推播通知</span><span class="sxs-lookup"><span data-stu-id="6c0ea-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="6c0ea-113">設定您的行動應用程式以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="6c0ea-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="6c0ea-114">更新伺服器專案以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="6c0ea-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="6c0ea-115">設定您的 Xamarin.iOS 專案</span><span class="sxs-lookup"><span data-stu-id="6c0ea-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="6c0ea-116">將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="6c0ea-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="6c0ea-117">在 **QSTodoService** 中新增下列屬性，以便讓 **AppDelegate** 能夠取得行動用戶端：</span><span class="sxs-lookup"><span data-stu-id="6c0ea-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="6c0ea-118">將下列 `using` 陳述式加入至 **AppDelegate.cs** 檔案頂端。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="6c0ea-119">在 **AppDelegate** 中，覆寫 **FinishedLaunching** 事件：</span><span class="sxs-lookup"><span data-stu-id="6c0ea-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="6c0ea-120">在相同的檔案中，覆寫 **RegisteredForRemoteNotifications** 事件。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="6c0ea-121">透過此程式碼，您將註冊能夠在伺服器所支援的所有平台間傳送的簡單範本通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="6c0ea-122">如需有關通知中樞範本的詳細資訊，請參閱 [範本](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="6c0ea-123">然後，覆寫 **DidReceivedRemoteNotification** 事件：</span><span class="sxs-lookup"><span data-stu-id="6c0ea-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="6c0ea-124">您的應用程式現在已更新為支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="6c0ea-125"><a name="test"></a>在應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="6c0ea-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="6c0ea-126">按 [執行] 按鈕以建置專案並在可執行 iOS 的裝置上啟動應用程式，然後按一下 [確定] 以接受推播通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c0ea-127">您必須明確地接受來自應用程式的推播通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="6c0ea-128">只有在應用程式第一次執行時，才會發生此要求。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="6c0ea-129">在應用程式中輸入一項工作，然後按一下加號 (**+**) 圖示。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="6c0ea-130">確認您已接收到通知，然後按一下 [確定]  以關閉通知。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="6c0ea-131">重複執行步驟 2 並立即關閉應用程式，接著確認通知已顯示。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="6c0ea-132">您已成功完成此教學課程。</span><span class="sxs-lookup"><span data-stu-id="6c0ea-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



