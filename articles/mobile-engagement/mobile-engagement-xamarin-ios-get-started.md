---
title: "aaaGet Started with Xamarin.iOS 的 Azure Mobile Engagement"
description: "深入了解如何使用分析及推播通知 Xamarin.iOS 應用程式的 Azure Mobile Engagement toouse。"
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
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="8ac3c-103">開始使用適用於 Xamarin.iOS 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8ac3c-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8ac3c-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 Xamarin.iOS 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="8ac3c-105">在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 Xamarin.iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="8ac3c-106">hello Azure Mobile Engagement 服務將會遭到淘汰年 3 月 2018年，目前只使用 tooexisting 客戶。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="8ac3c-107">如需詳細資訊，請參閱 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="8ac3c-108">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="8ac3c-109">[Xamarin Studio](http://xamarin.com/studio)。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="8ac3c-110">您也可以使用 Visual Studio 搭配 Xamarin，但本教學課程會使用 Xamarin Studio。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="8ac3c-111">如需安裝指示，請參閱[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="8ac3c-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="8ac3c-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="8ac3c-113">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8ac3c-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8ac3c-115">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="8ac3c-116"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8ac3c-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="8ac3c-117"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="8ac3c-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="8ac3c-118">此教學課程提供 < 基本整合 > hello 最小設定必要的 toocollect 資料及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="8ac3c-119">我們將使用 Xamarin toodemonstrate hello 整合，以建立基本應用程式：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="8ac3c-120">建立新的 Xamarin.iOS 專案</span><span class="sxs-lookup"><span data-stu-id="8ac3c-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="8ac3c-121">啟動 Xamarin Studio。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="8ac3c-122">跳過**檔案** -> **新增** -> **方案**</span><span class="sxs-lookup"><span data-stu-id="8ac3c-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="8ac3c-123">選取**單一檢視應用程式**，請確定選取的 hello 語言是**C#** ，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="8ac3c-124">填寫 hello**應用程式名稱**和 hello**組織識別碼**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="8ac3c-125">請確定該 hello 發行設定檔，您最終會使用的 toodeploy iOS 應用程式使用與您在這裡有的配套識別碼 hello 完全符合應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="8ac3c-126">更新 hello**專案名稱**，**方案名稱**和**位置**如果需要，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="8ac3c-127">Xamarin Studio 將會建立在其中，我們將會整合 Mobile Engagement hello 示範應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="8ac3c-128">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="8ac3c-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="8ac3c-129">以滑鼠右鍵按一下 hello**封裝**hello 方案 windows 和選取資料夾**新增套件...**</span><span class="sxs-lookup"><span data-stu-id="8ac3c-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="8ac3c-130">搜尋 hello **Microsoft Azure Mobile Engagement Xamarin SDK**並將它加入 tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="8ac3c-131">開啟**d**並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="8ac3c-132">在 hello **FinishedLaunching**方法中，新增下列 tooinitialize hello 連線與 Mobile Engagement 後端的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="8ac3c-133">請確定 tooadd 您**ConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="8ac3c-134">此程式碼也會使用假**NotificationIcon** hello Mobile Engagement SDK，您可能想要新增的 tooreplace。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="8ac3c-135"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="8ac3c-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="8ac3c-136">在訂單 toostart 傳送資料，並確保 hello 的使用者，您必須傳送至少一個螢幕 toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="8ac3c-137">開啟**ViewController.cs**並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="8ac3c-138">取代 hello 類別`ViewController`繼承自`UIViewController`太`EngagementViewController`。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="8ac3c-139"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="8ac3c-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="8ac3c-140"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="8ac3c-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="8ac3c-141">Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="8ac3c-142">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="8ac3c-143">hello 下列各節將設定您的應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="8ac3c-144">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="8ac3c-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="8ac3c-145">開啟 hello **d**並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="8ac3c-146">現在內 hello`FinishedLaunching`方法，加入下列 tooregister 推播訊息之後的 hello`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="8ac3c-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
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
3. <span data-ttu-id="8ac3c-147">最後的更新，或新增 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="8ac3c-147">Finally - update or add hello following methods:</span></span>
   
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
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="8ac3c-148">在您**Info.plist** hello 方案中的檔案，請確認該 hello**配套識別碼**符合以 hello**應用程式識別碼**hello Apple 開發人員在您佈建設定檔中有置中。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="8ac3c-149">在 hello 相同**Info.plist**檔案，請確定您已核取 hello**啟用背景模式**和**遠端通知**。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="8ac3c-150">在您已經與此發行設定檔關聯的 hello 裝置上執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ac3c-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

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
