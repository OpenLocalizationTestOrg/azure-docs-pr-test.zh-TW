---
title: "ios 的 Swift aaaGet Started with Azure Mobile Engagement |Microsoft 文件"
description: "深入了解如何 toouse 與分析及推播通知的 Azure Mobile Engagement 適用於 iOS 的應用程式。"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="c62a0-103">開始使用適用於 iOS 應用程式 (Swift) 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c62a0-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="c62a0-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 tooan iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c62a0-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="c62a0-105">在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c62a0-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="c62a0-106">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="c62a0-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="c62a0-107">Xcode 8，可以從您的 MAC App Store 安裝</span><span class="sxs-lookup"><span data-stu-id="c62a0-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="c62a0-108">hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="c62a0-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="c62a0-109">推播通知憑證 (.p12)，您可以在 Apple Dev Center 取得</span><span class="sxs-lookup"><span data-stu-id="c62a0-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="c62a0-110">本教學課程使用 Swift 3.0 版。</span><span class="sxs-lookup"><span data-stu-id="c62a0-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="c62a0-111">完成本教學課程是所有其他 iOS 應用程式 Mobile Engagement 教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="c62a0-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="c62a0-112">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c62a0-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c62a0-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c62a0-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c62a0-114">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)。</span><span class="sxs-lookup"><span data-stu-id="c62a0-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="c62a0-115"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c62a0-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="c62a0-116"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="c62a0-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="c62a0-117">此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="c62a0-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="c62a0-118">hello 完整的整合文件可以在 hello [Mobile Engagement iOS SDK 整合](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c62a0-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="c62a0-119">我們將使用 XCode toodemonstrate hello 整合，以建立基本應用程式：</span><span class="sxs-lookup"><span data-stu-id="c62a0-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="c62a0-120">建立新的 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="c62a0-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="c62a0-121">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="c62a0-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="c62a0-122">下載 hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="c62a0-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="c62a0-123">擷取 hello。.tar.gz 檔案 tooa 資料夾中您的電腦</span><span class="sxs-lookup"><span data-stu-id="c62a0-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="c62a0-124">Hello 專案上按一下滑鼠右鍵，然後選取 「 太新增檔案...」</span><span class="sxs-lookup"><span data-stu-id="c62a0-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="c62a0-125">瀏覽解壓縮 hello SDK 和選取 hello toohello 資料夾`EngagementSDK`資料夾，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c62a0-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="c62a0-126">開啟 hello `Build Phases`  索引標籤和 hello`Link Binary With Libraries`功能表將 hello 架構，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c62a0-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="c62a0-127">選擇檔案以建立橋接標頭 toobe 無法 toouse hello SDK 的目標 C 應用程式開發介面 > 新增 > 檔案 > iOS > 來源 > 標頭檔。</span><span class="sxs-lookup"><span data-stu-id="c62a0-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="c62a0-128">編輯 hello 橋接標頭檔 tooexpose Mobile Engagement Objective C 程式碼 tooyour Swift 代碼，請新增下列 imports hello:</span><span class="sxs-lookup"><span data-stu-id="c62a0-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="c62a0-129">在建置設定，確定的 hello OBJECTIVE-C 橋接標頭組建 Swift 編譯器的程式碼產生的設定有一個路徑 toothis 標頭。</span><span class="sxs-lookup"><span data-stu-id="c62a0-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="c62a0-130">以下是路徑的範例： **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h （取決於 hello 路徑）**</span><span class="sxs-lookup"><span data-stu-id="c62a0-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="c62a0-131">請返回 Azure 入口網站應用程式中 toohello*連接資訊*頁面，並複製 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="c62a0-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="c62a0-132">現在將 hello 連接字串貼在 hello`didFinishLaunchingWithOptions`委派</span><span class="sxs-lookup"><span data-stu-id="c62a0-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="c62a0-133"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="c62a0-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="c62a0-134">在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="c62a0-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="c62a0-135">開啟 hello **ViewController.swift**檔案，並將 hello 基底類別**ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="c62a0-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="c62a0-136"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="c62a0-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="c62a0-137"><a id="integrate-push"></a>啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="c62a0-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="c62a0-138">Mobile Engagement 可讓您 toointeract 和與您的使用者使用推播通知及應用程式內訊息的觸達活動 hello 內容中。</span><span class="sxs-lookup"><span data-stu-id="c62a0-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="c62a0-139">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c62a0-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="c62a0-140">hello 下列各節將會安裝應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="c62a0-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="c62a0-141">啟用您的應用程式 tooreceive 無訊息的推播通知</span><span class="sxs-lookup"><span data-stu-id="c62a0-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="c62a0-142">加入 hello 觸達庫 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="c62a0-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="c62a0-143">以滑鼠右鍵按一下您的專案</span><span class="sxs-lookup"><span data-stu-id="c62a0-143">Right click your project</span></span>
2. <span data-ttu-id="c62a0-144">選取 `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="c62a0-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="c62a0-145">瀏覽 toohello 資料夾解壓縮 hello SDK 的位置</span><span class="sxs-lookup"><span data-stu-id="c62a0-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="c62a0-146">選取 hello`EngagementReach`資料夾</span><span class="sxs-lookup"><span data-stu-id="c62a0-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="c62a0-147">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="c62a0-147">Click Add</span></span>
6. <span data-ttu-id="c62a0-148">編輯 hello 橋接標頭檔 tooexpose Mobile Engagement OBJECTIVE-C 觸達標頭，並新增下列 imports hello:</span><span class="sxs-lookup"><span data-stu-id="c62a0-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="c62a0-149">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="c62a0-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="c62a0-150">內部 hello `didFinishLaunchingWithOptions` -建立觸達模組並將它傳遞 tooyour 現有 Engagement 初始化行：</span><span class="sxs-lookup"><span data-stu-id="c62a0-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="c62a0-151">啟用您的應用程式 tooreceive APNS 的推播通知</span><span class="sxs-lookup"><span data-stu-id="c62a0-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="c62a0-152">加入下列行 toohello hello`didFinishLaunchingWithOptions`方法：</span><span class="sxs-lookup"><span data-stu-id="c62a0-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="c62a0-153">新增 hello`didRegisterForRemoteNotificationsWithDeviceToken`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c62a0-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="c62a0-154">新增 hello`didReceiveRemoteNotification:fetchCompletionHandler:`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c62a0-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
