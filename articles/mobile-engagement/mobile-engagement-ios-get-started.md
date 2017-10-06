---
title: "適用於 iOS Objective C 中的開始使用 Azure Mobile Engagement aaaGet |Microsoft 文件"
description: "深入了解如何使用 iOS 應用程式分析及推播通知的 Azure Mobile Engagement toouse。"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="85eec-103">開始使用適用於 iOS 應用程式 (Objective C) 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="85eec-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="85eec-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 tooan iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="85eec-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="85eec-105">在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="85eec-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="85eec-106">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="85eec-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="85eec-107">Xcode 8，可以從您的 MAC App Store 安裝</span><span class="sxs-lookup"><span data-stu-id="85eec-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="85eec-108">hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="85eec-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="85eec-109">完成本教學課程是所有其他 iOS 應用程式 Mobile Engagement 教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="85eec-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="85eec-110">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="85eec-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="85eec-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="85eec-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="85eec-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="85eec-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="85eec-113"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="85eec-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="85eec-114"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="85eec-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="85eec-115">此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="85eec-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="85eec-116">hello 完整的整合文件可以在 hello [Mobile Engagement iOS SDK 整合](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="85eec-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="85eec-117">我們將使用 XCode toodemonstrate hello 整合來建立基本應用程式。</span><span class="sxs-lookup"><span data-stu-id="85eec-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="85eec-118">建立新的 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="85eec-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="85eec-119">連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="85eec-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="85eec-120">下載 hello [Mobile Engagement iOS SDK]。</span><span class="sxs-lookup"><span data-stu-id="85eec-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="85eec-121">擷取 hello。.tar.gz 檔案 tooa 資料夾中您的電腦。</span><span class="sxs-lookup"><span data-stu-id="85eec-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="85eec-122">Hello 專案上按一下滑鼠右鍵，然後選取**新增檔案至**。</span><span class="sxs-lookup"><span data-stu-id="85eec-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="85eec-123">瀏覽 toohello hello SDK 的解壓縮所在的資料夾，選取 hello`EngagementSDK`資料夾中，按一下 **選項**在 hello 左下的角，並確定該 hello 核取方塊**複製的項目，視**和 hello會檢查您的目標核取方塊，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="85eec-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="85eec-124">開啟 hello**建置階段** 索引標籤，並在 hello**連結二進位的程式庫**功能表上，將 hello 架構，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85eec-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="85eec-125">請返回 Azure 入口網站應用程式中 toohello**連接資訊**頁面，並複製 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="85eec-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="85eec-126">新增下列一行程式碼中的 hello 您**d**檔案。</span><span class="sxs-lookup"><span data-stu-id="85eec-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="85eec-127">現在將 hello 連接字串貼在 hello`didFinishLaunchingWithOptions`委派。</span><span class="sxs-lookup"><span data-stu-id="85eec-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="85eec-128">`setTestLogEnabled`是選擇性的陳述式可讓您 tooidentify 問題 SDK 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="85eec-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="85eec-129"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="85eec-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="85eec-130">在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="85eec-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="85eec-131">開啟 hello **ViewController.h**檔案和匯入**EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="85eec-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="85eec-132">現在取代 hello 超級類別的 hello **ViewController**介面由`EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="85eec-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="85eec-133"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="85eec-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="85eec-134"><a id="integrate-push"></a>啟用推播通知與 App 內傳訊</span><span class="sxs-lookup"><span data-stu-id="85eec-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="85eec-135">Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。</span><span class="sxs-lookup"><span data-stu-id="85eec-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="85eec-136">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="85eec-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="85eec-137">hello 下列各節將設定您的應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="85eec-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="85eec-138">啟用您的應用程式 tooreceive 無訊息的推播通知</span><span class="sxs-lookup"><span data-stu-id="85eec-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="85eec-139">加入 hello 觸達庫 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="85eec-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="85eec-140">以滑鼠右鍵按一下您的專案。</span><span class="sxs-lookup"><span data-stu-id="85eec-140">Right-click your project.</span></span>
2. <span data-ttu-id="85eec-141">選取 [新增檔案至] 。</span><span class="sxs-lookup"><span data-stu-id="85eec-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="85eec-142">瀏覽 toohello 資料夾解壓縮 hello SDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="85eec-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="85eec-143">選取 hello`EngagementReach`資料夾。</span><span class="sxs-lookup"><span data-stu-id="85eec-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="85eec-144">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="85eec-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="85eec-145">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="85eec-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="85eec-146">回到**AppDeletegate.m**檔案中，匯入 hello Engagement 觸達模組。</span><span class="sxs-lookup"><span data-stu-id="85eec-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="85eec-147">內部 hello`application:didFinishLaunchingWithOptions`方法，建立觸達模組，並將它傳遞 tooyour 現有 Engagement 初始化行：</span><span class="sxs-lookup"><span data-stu-id="85eec-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="85eec-148">啟用您的應用程式 tooreceive APNS 的推播通知</span><span class="sxs-lookup"><span data-stu-id="85eec-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="85eec-149">加入下列行 toohello hello`application:didFinishLaunchingWithOptions`方法：</span><span class="sxs-lookup"><span data-stu-id="85eec-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="85eec-150">新增 hello`application:didRegisterForRemoteNotificationsWithDeviceToken`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85eec-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="85eec-151">新增 hello`didFailToRegisterForRemoteNotificationsWithError`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85eec-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="85eec-152">新增 hello`didReceiveRemoteNotification:fetchCompletionHandler`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85eec-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
