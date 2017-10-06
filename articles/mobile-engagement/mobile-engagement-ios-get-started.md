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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>開始使用適用於 iOS 應用程式 (Objective C) 的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 您的應用程式使用量和傳送推播通知 toosegmented 使用者 tooan iOS 應用程式。
在本教學課程中，您將使用 Apple 推播通知服務 (APNS)，建立可收集基本資料，並接收推播通知的空白 iOS 應用程式。

本教學課程必須 hello 下列需求：

* Xcode 8，可以從您的 MAC App Store 安裝
* hello [Mobile Engagement iOS SDK]

完成本教學課程是所有其他 iOS 應用程式 Mobile Engagement 教學課程的先決條件。

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started)。
>
>

## <a id="setup-azme"></a>為您的 iOS 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。 hello 完整的整合文件可以在 hello [Mobile Engagement iOS SDK 整合](mobile-engagement-ios-sdk-overview.md)

我們將使用 XCode toodemonstrate hello 整合來建立基本應用程式。

### <a name="create-a-new-ios-project"></a>建立新的 iOS 專案
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>連接您的應用程式 toohello Mobile Engagement 後端
1. 下載 hello [Mobile Engagement iOS SDK]。
2. 擷取 hello。.tar.gz 檔案 tooa 資料夾中您的電腦。
3. Hello 專案上按一下滑鼠右鍵，然後選取**新增檔案至**。

    ![][1]
4. 瀏覽 toohello hello SDK 的解壓縮所在的資料夾，選取 hello`EngagementSDK`資料夾中，按一下 **選項**在 hello 左下的角，並確定該 hello 核取方塊**複製的項目，視**和 hello會檢查您的目標核取方塊，然後按**確定**。

    ![][2]
5. 開啟 hello**建置階段** 索引標籤，並在 hello**連結二進位的程式庫**功能表上，將 hello 架構，如下所示：

    ![][3]
6. 請返回 Azure 入口網站應用程式中 toohello**連接資訊**頁面，並複製 hello 連接字串。

    ![][4]
7. 新增下列一行程式碼中的 hello 您**d**檔案。

        #import "EngagementAgent.h"
8. 現在將 hello 連接字串貼在 hello`didFinishLaunchingWithOptions`委派。

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`是選擇性的陳述式可讓您 tooidentify 問題 SDK 記錄檔。

## <a id="monitor"></a>啟用即時監視
在順序 toostart 傳送資料，並確保 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。

1. 開啟 hello **ViewController.h**檔案和匯入**EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. 現在取代 hello 超級類別的 hello **ViewController**介面由`EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與 App 內傳訊
Mobile Engagement 可讓您與您的使用者 toointeract 和觸達推播通知與應用程式內訊息的活動 hello 內容中。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將設定您的應用程式 tooreceive 它們。

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>啟用您的應用程式 tooreceive 無訊息的推播通知
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>加入 hello 觸達庫 tooyour 專案
1. 以滑鼠右鍵按一下您的專案。
2. 選取 [新增檔案至] 。
3. 瀏覽 toohello 資料夾解壓縮 hello SDK 的位置。
4. 選取 hello`EngagementReach`資料夾。
5. 按一下 [新增] 。

### <a name="modify-your-application-delegate"></a>修改您的應用程式代理人
1. 回到**AppDeletegate.m**檔案中，匯入 hello Engagement 觸達模組。

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. 內部 hello`application:didFinishLaunchingWithOptions`方法，建立觸達模組，並將它傳遞 tooyour 現有 Engagement 初始化行：

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>啟用您的應用程式 tooreceive APNS 的推播通知
1. 加入下列行 toohello hello`application:didFinishLaunchingWithOptions`方法：

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
2. 新增 hello`application:didRegisterForRemoteNotificationsWithDeviceToken`方法，如下所示：

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. 新增 hello`didFailToRegisterForRemoteNotificationsWithError`方法，如下所示：

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. 新增 hello`didReceiveRemoteNotification:fetchCompletionHandler`方法，如下所示：

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
