---
title: "開始使用適用於 iOS (Swift) 的 Azure Mobile Engagement | Microsoft Docs"
description: "了解如何使用 iOS 應用程式的 Azure Mobile Engagement 與分析和推播通知。"
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
ms.openlocfilehash: 1011b9823333e79a52cd2d187df4f8d063b1f799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="75006-103">開始使用適用於 iOS 應用程式 (Swift) 的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="75006-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="75006-104">本主題說明如何使用 Azure Mobile Engagement 了解您的應用程式使用情形，並將推送通知傳送至 iOS 應用程式的區隔使用者。</span><span class="sxs-lookup"><span data-stu-id="75006-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="75006-105">在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75006-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="75006-106">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="75006-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="75006-107">Xcode 8，可以從您的 MAC App Store 安裝</span><span class="sxs-lookup"><span data-stu-id="75006-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="75006-108">[Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="75006-108">the [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="75006-109">推播通知憑證 (.p12)，您可以在 Apple Dev Center 取得</span><span class="sxs-lookup"><span data-stu-id="75006-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="75006-110">本教學課程使用 Swift 3.0 版。</span><span class="sxs-lookup"><span data-stu-id="75006-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="75006-111">完成本教學課程是所有其他 iOS 應用程式 Mobile Engagement 教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="75006-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="75006-112">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75006-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="75006-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="75006-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75006-114">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)。</span><span class="sxs-lookup"><span data-stu-id="75006-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="75006-115"><a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="75006-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="75006-116"><a id="connecting-app"></a>將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="75006-116"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="75006-117">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知時必要的最低設定。</span><span class="sxs-lookup"><span data-stu-id="75006-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="75006-118">完整的整合文件位於 [Mobile Engagement iOS SDK 整合](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="75006-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="75006-119">我們將會使用 XCode 建立基本應用程式來示範整合：</span><span class="sxs-lookup"><span data-stu-id="75006-119">We will create a basic app with XCode to demonstrate the integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="75006-120">建立新的 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="75006-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="75006-121">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="75006-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="75006-122">下載 [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="75006-122">Download the [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="75006-123">將 .tar.gz 檔案解壓縮到電腦中的資料夾</span><span class="sxs-lookup"><span data-stu-id="75006-123">Extract the .tar.gz file to a folder in your computer</span></span>
3. <span data-ttu-id="75006-124">以滑鼠右鍵按一下專案，然後選取 [Add files to ...]</span><span class="sxs-lookup"><span data-stu-id="75006-124">Right click the project and select "Add files to ..."</span></span>
   
    ![][1]
4. <span data-ttu-id="75006-125">瀏覽至您解壓縮 SDK 的資料夾，選取 `EngagementSDK` 資料夾，然後按 [OK]。</span><span class="sxs-lookup"><span data-stu-id="75006-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="75006-126">開啟 `Build Phases` 索引標籤，並在 `Link Binary With Libraries` 功能表中新增框架，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75006-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="75006-127">選擇 [File] > [New] > [File] > [iOS] > [Source] > [Header File] 來建立「橋接」標頭，以使用 SDK 的 Objective C API。</span><span class="sxs-lookup"><span data-stu-id="75006-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="75006-128">編輯橋接標頭檔案來將 Mobile Engagement Objective-C 程式碼公開至 Swift 程式碼，並新增以下匯入：</span><span class="sxs-lookup"><span data-stu-id="75006-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="75006-129">在 [Build Settings]，請確定在 [Swift Compiler - Code Generation] 下的 [Objective-C Bridging Header] 組件設定有指向此標頭的路徑。</span><span class="sxs-lookup"><span data-stu-id="75006-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span></span> <span data-ttu-id="75006-130">路徑的範例： **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (依路徑而定)**</span><span class="sxs-lookup"><span data-stu-id="75006-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="75006-131">回到 Azure 入口網站中您應用程式的 [連線資訊]  頁面，並複製 [連線字串]。</span><span class="sxs-lookup"><span data-stu-id="75006-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="75006-132">現在 `didFinishLaunchingWithOptions` 代理人中貼上連接字串。</span><span class="sxs-lookup"><span data-stu-id="75006-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="75006-133"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="75006-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="75006-134">若要開始傳送資料並確定使用者正在使用，您必須至少傳送一個畫面 (活動) 到 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="75006-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="75006-135">開啟 **ViewController.swift** 檔案，將 **ViewController** 的基底類別取代為 **EngagementViewController**：</span><span class="sxs-lookup"><span data-stu-id="75006-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="75006-136"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="75006-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="75006-137"><a id="integrate-push"></a>啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="75006-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="75006-138">Mobile Engagement 可讓您透過「推播通知」和「應用程式內傳訊」，於活動進行時與使用者互動和觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="75006-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="75006-139">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="75006-139">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="75006-140">以下各節將設定您的應用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="75006-140">The following sections will setup your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="75006-141">啟用應用程式接收無聲推播通知</span><span class="sxs-lookup"><span data-stu-id="75006-141">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="75006-142">將觸達程式庫加入至專案</span><span class="sxs-lookup"><span data-stu-id="75006-142">Add the Reach library to your project</span></span>
1. <span data-ttu-id="75006-143">以滑鼠右鍵按一下您的專案</span><span class="sxs-lookup"><span data-stu-id="75006-143">Right click your project</span></span>
2. <span data-ttu-id="75006-144">選取 `Add file to ...`</span><span class="sxs-lookup"><span data-stu-id="75006-144">Select `Add file to ...`</span></span>
3. <span data-ttu-id="75006-145">瀏覽至您解壓縮 SDK 所在的資料夾</span><span class="sxs-lookup"><span data-stu-id="75006-145">Navigate to the folder where you extracted the SDK</span></span>
4. <span data-ttu-id="75006-146">選取 `EngagementReach` 資料夾</span><span class="sxs-lookup"><span data-stu-id="75006-146">Select the `EngagementReach` folder</span></span>
5. <span data-ttu-id="75006-147">按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="75006-147">Click Add</span></span>
6. <span data-ttu-id="75006-148">編輯橋接標頭檔案來將 Mobile Engagement Objective-C 觸達標頭公開，並新增以下匯入：</span><span class="sxs-lookup"><span data-stu-id="75006-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span></span>
   
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

### <a name="modify-your-application-delegate"></a><span data-ttu-id="75006-149">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="75006-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="75006-150">在 `didFinishLaunchingWithOptions` 內 - 建立觸達模組並將它傳遞到您現有的 Engagement 初始化行：</span><span class="sxs-lookup"><span data-stu-id="75006-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="75006-151">讓您的應用程式能接收 APNS 推播通知</span><span class="sxs-lookup"><span data-stu-id="75006-151">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="75006-152">將下行新增至 `didFinishLaunchingWithOptions` 方法：</span><span class="sxs-lookup"><span data-stu-id="75006-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span></span>
   
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
2. <span data-ttu-id="75006-153">新增 `didRegisterForRemoteNotificationsWithDeviceToken` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75006-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="75006-154">新增 `didReceiveRemoteNotification:fetchCompletionHandler:` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75006-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="75006-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="75006-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
