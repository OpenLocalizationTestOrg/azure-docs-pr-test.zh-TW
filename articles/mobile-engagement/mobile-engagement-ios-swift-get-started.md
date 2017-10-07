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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>開始使用適用於 iOS 應用程式 (Swift) 的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 tooan iOS 應用程式。
在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 iOS 應用程式。

本教學課程必須 hello 下列需求：

* Xcode 8，可以從您的 MAC App Store 安裝
* hello [Mobile Engagement iOS SDK]
* 推播通知憑證 (.p12)，您可以在 Apple Dev Center 取得

> [!NOTE]
> 本教學課程使用 Swift 3.0 版。 
> 
> 

完成本教學課程是所有其他 iOS 應用程式 Mobile Engagement 教學課程的先決條件。

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started)。
> 
> 

## <a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。 hello 完整的整合文件可以在 hello [Mobile Engagement iOS SDK 整合](mobile-engagement-ios-sdk-overview.md)

我們將使用 XCode toodemonstrate hello 整合，以建立基本應用程式：

### <a name="create-a-new-ios-project"></a>建立新的 iOS 專案
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 下載 hello [Mobile Engagement iOS SDK]
2. 擷取 hello。.tar.gz 檔案 tooa 資料夾中您的電腦
3. Hello 專案上按一下滑鼠右鍵，然後選取 「 太新增檔案...」
   
    ![][1]
4. 瀏覽解壓縮 hello SDK 和選取 hello toohello 資料夾`EngagementSDK`資料夾，然後按 [確定]。
   
    ![][2]
5. 開啟 hello `Build Phases`  索引標籤和 hello`Link Binary With Libraries`功能表將 hello 架構，如下所示：
   
    ![][3]
6. 選擇檔案以建立橋接標頭 toobe 無法 toouse hello SDK 的目標 C 應用程式開發介面 > 新增 > 檔案 > iOS > 來源 > 標頭檔。
   
    ![][4]
7. 編輯 hello 橋接標頭檔 tooexpose Mobile Engagement Objective C 程式碼 tooyour Swift 代碼，請新增下列 imports hello:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. 在建置設定，確定的 hello OBJECTIVE-C 橋接標頭組建 Swift 編譯器的程式碼產生的設定有一個路徑 toothis 標頭。 以下是路徑的範例： **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h （取決於 hello 路徑）**
   
   ![][6]
9. 請返回 Azure 入口網站應用程式中 toohello*連接資訊*頁面，並複製 hello 連接字串
   
   ![][5]
10. 現在將 hello 連接字串貼在 hello`didFinishLaunchingWithOptions`委派
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>啟用即時監視
在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。

1. 開啟 hello **ViewController.swift**檔案，並將 hello 基底類別**ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與應用程式內傳訊
Mobile Engagement 可讓您 toointeract 和與您的使用者使用推播通知及應用程式內訊息的觸達活動 hello 內容中。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將會安裝應用程式 tooreceive 它們。

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>啟用您的應用程式 tooreceive 無訊息的推播通知
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>加入 hello 觸達庫 tooyour 專案
1. 以滑鼠右鍵按一下您的專案
2. 選取 `Add file too...`
3. 瀏覽 toohello 資料夾解壓縮 hello SDK 的位置
4. 選取 hello`EngagementReach`資料夾
5. 按一下 [新增]
6. 編輯 hello 橋接標頭檔 tooexpose Mobile Engagement OBJECTIVE-C 觸達標頭，並新增下列 imports hello:
   
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

### <a name="modify-your-application-delegate"></a>修改您的應用程式代理人
1. 內部 hello `didFinishLaunchingWithOptions` -建立觸達模組並將它傳遞 tooyour 現有 Engagement 初始化行：
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>啟用您的應用程式 tooreceive APNS 的推播通知
1. 加入下列行 toohello hello`didFinishLaunchingWithOptions`方法：
   
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
2. 新增 hello`didRegisterForRemoteNotificationsWithDeviceToken`方法，如下所示：
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. 新增 hello`didReceiveRemoteNotification:fetchCompletionHandler:`方法，如下所示：
   
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
