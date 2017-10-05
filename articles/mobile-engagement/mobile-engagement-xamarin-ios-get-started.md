---
title: "開始使用適用於 Xamarin.iOS 的 Azure Mobile Engagement"
description: "了解如何使用 Xamarin.iOS 應用程式的 Azure Mobile Engagement 與分析和推播通知。"
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9938c3e994acf31244825b1afb347f8c9f90ebe3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="a019d-103">開始使用適用於 Xamarin.iOS 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a019d-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a019d-104">本主題說明如何使用 Azure Mobile Engagement 來了解您的應用程式使用量，並傳送推播通知給 Xamarin.iOS 應用程式的區隔使用者。</span><span class="sxs-lookup"><span data-stu-id="a019d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="a019d-105">在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 Xamarin.iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a019d-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="a019d-106">Azure Mobile Engagement 服務將於 2018 年 3 月淘汰，目前僅供現有客戶使用。</span><span class="sxs-lookup"><span data-stu-id="a019d-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="a019d-107">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="a019d-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="a019d-108">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="a019d-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="a019d-109">[Xamarin Studio](http://xamarin.com/studio)。</span><span class="sxs-lookup"><span data-stu-id="a019d-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="a019d-110">您也可以使用 Visual Studio 搭配 Xamarin，但本教學課程會使用 Xamarin Studio。</span><span class="sxs-lookup"><span data-stu-id="a019d-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="a019d-111">如需安裝指示，請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a019d-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="a019d-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="a019d-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="a019d-113">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a019d-113">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a019d-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a019d-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a019d-115">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="a019d-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="a019d-116"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a019d-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a019d-117"><a id="connecting-app"></a>將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="a019d-117"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="a019d-118">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知時必要的最低設定。</span><span class="sxs-lookup"><span data-stu-id="a019d-118">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span>

<span data-ttu-id="a019d-119">我們將會使用 Xamarin 建立基本應用程式來示範整合：</span><span class="sxs-lookup"><span data-stu-id="a019d-119">We will create a basic app with Xamarin to demonstrate the integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="a019d-120">建立新的 Xamarin.iOS 專案</span><span class="sxs-lookup"><span data-stu-id="a019d-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="a019d-121">啟動 Xamarin Studio。</span><span class="sxs-lookup"><span data-stu-id="a019d-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="a019d-122">移至 檔案 ->  -> 方案</span><span class="sxs-lookup"><span data-stu-id="a019d-122">Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="a019d-123">選取 [單一檢視應用程式]，確定選取的語言是 **C#**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a019d-123">Select **Single View App**, make sure the selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="a019d-124">填入 [應用程式名稱] 和 [組織識別碼]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a019d-124">Fill in the **App Name** and the **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="a019d-125">請確定您最後用來部署您的 iOS 應用程式的發行設定檔使用的應用程式識別碼完全符合這裡顯示的 [套件組合識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a019d-125">Make sure that the publishing profile you eventually use to deploy your iOS app is using an App ID which matches exactly with the Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="a019d-126">如有必要，請更新 [專案名稱]、[方案名稱] 和 [位置]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a019d-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="a019d-127">Xamarin Studio 會建立示範應用程式，我們將在其中整合 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a019d-127">Xamarin Studio will create the demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="a019d-128">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="a019d-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="a019d-129">以滑鼠右鍵按一下 [方案] 視窗中的 [套件] 資料夾，然後選取 [新增套件...]</span><span class="sxs-lookup"><span data-stu-id="a019d-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="a019d-130">搜尋 **Microsoft Azure Mobile Engagement Xamarin SDK** 並將它新增至您的方案。</span><span class="sxs-lookup"><span data-stu-id="a019d-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="a019d-131">開啟 **AppDelegate.cs** 並新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="a019d-131">Open **AppDelegate.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="a019d-132">在 **FinishedLaunching** 方法中，加入下列程式碼來初始化與 Mobile Engagement 後端的連接。</span><span class="sxs-lookup"><span data-stu-id="a019d-132">In the **FinishedLaunching** method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="a019d-133">請務必新增您的 **ConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="a019d-133">Make sure to add your **ConnectionString**.</span></span> <span data-ttu-id="a019d-134">此程式碼也會使用由 Mobile Engagement SDK 加入的虛擬 **NotificationIcon** ，建議您加以取代。</span><span class="sxs-lookup"><span data-stu-id="a019d-134">This code also uses a dummy **NotificationIcon** which is added by the Mobile Engagement SDK which you may want to replace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="a019d-135"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="a019d-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="a019d-136">若要開始傳送資料並確定使用者正在使用，您必須至少傳送一個螢幕到 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="a019d-136">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="a019d-137">開啟 **ViewController.cs** 並新增以下 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="a019d-137">Open **ViewController.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="a019d-138">取代 `ViewController` 從 `UIViewController` 繼承到 `EngagementViewController` 的類別。</span><span class="sxs-lookup"><span data-stu-id="a019d-138">Replace the class from which `ViewController` inherits from `UIViewController` to `EngagementViewController`.</span></span> 

## <span data-ttu-id="a019d-139"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="a019d-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a019d-140"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="a019d-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a019d-141">Mobile Engagement 可讓您透過「推播通知」和「應用程式內傳訊」，於活動進行時與使用者互動和觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="a019d-141">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="a019d-142">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="a019d-142">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="a019d-143">以下各節將設定您的用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="a019d-143">The following sections set up your app to receive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="a019d-144">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="a019d-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="a019d-145">開啟 **AppDelegate.cs** 並新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="a019d-145">Open the **AppDelegate.cs** and add the following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="a019d-146">現在在 `FinishedLaunching` 方法中，加入下列程式碼以註冊 `EngagementAgent.init(...)` 之後的推播訊息</span><span class="sxs-lookup"><span data-stu-id="a019d-146">Now inside the `FinishedLaunching` method, add the following to register for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="a019d-147">最後，更新或新增下列方法︰</span><span class="sxs-lookup"><span data-stu-id="a019d-147">Finally - update or add the following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed to register for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="a019d-148">在方案的 **Info.plist** 檔案中，確認 [套件組合識別碼] 符合 Apple Dev Center 中您的佈建設定檔中的 [應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a019d-148">In your **Info.plist** file in the solution, confirm that the **Bundle Identifier** matches with the **App ID** you have in your provisioning profile in the Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="a019d-149">在同一個 **Info.plist** 檔案中，確定您已核取 [啟用背景模式] 和 [遠端通知]。</span><span class="sxs-lookup"><span data-stu-id="a019d-149">In the same **Info.plist** file, make sure that you have checked the **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="a019d-150">在與此發行設定檔相關聯的裝置上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="a019d-150">Run the app on the device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
