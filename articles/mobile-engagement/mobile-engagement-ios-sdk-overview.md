---
title: "aaaAzure Mobile Engagement iOS SDK 概觀 |Microsoft 文件"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>Azure Mobile Engagement iOS SDK
從這裡開始 tooget hello 的所有詳細資料如何 toointegrate Azure Mobile Engagement 中 iOS 應用程式。 如果您想要 toogive 它再試一次第一次，請確定您我們[15 分鐘教學課程](mobile-engagement-ios-get-started.md)。

按一下 toosee hello [SDK 內容](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>整合程序
1. 從這裡開始：[如何 toointegrate Mobile Engagement 中 iOS 應用程式](mobile-engagement-ios-integrate-engagement.md)
2. 通知：[如何在您的 iOS 應用程式中的 toointegrate 觸達 （通知）](mobile-engagement-ios-integrate-engagement-reach.md)
3. 標記計劃實作： [toouse hello 進階 Mobile Engagement 應用程式開發介面中 iOS 應用程式所標記的方式](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>版本資訊
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* 修正在背景清除徽章。
* 修正在 XCode 9 上關於 API 未在主要佇列呼叫的警告。
* 修正觸達輪詢中的記憶體流失。
* 停止支援 iOS 6.X。 從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 7。

針對較早版本，請參閱 hello[完成版本資訊](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>升級程序
如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。

如果可能會發生 toofollow 數個程序錯過數個版本的 SDK 請的 hello hello 完成[升級程序](mobile-engagement-ios-upgrade-procedure.md)。

為每個新的 hello SDK 版本，您必須先取代 （移除並重新匯入在 xcode 中） hello EngagementSDK 和 EngagementReach 資料夾。

### <a name="from-300-too400"></a>從 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 開始就必須從 hello SDK 4.0.0 版。

> [!NOTE]
> 如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。 沒有已知的錯誤之前的版本中的 hello 觸達模組 10 的 iOS 裝置上執行時： 系統通知不會採取動作。 toofix 就 tooimplement hello 這個已被取代 API`application:didReceiveRemoteNotification:`在您的應用程式委派，如下所示：
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。 您應儘速切換 tooXCode 8。
>
>

#### <a name="usernotifications-framework"></a>UserNotifications 架構
您需要 tooadd hello`UserNotifications`您建置階段中的架構。

hello 專案總管 中開啟您專案窗格並選取 hello 正確的目標。 然後，開啟 hello **建置階段** 索引標籤在 hello **< 連結二進位與媒體櫃**功能表上，加入架構`UserNotifications.framework`-設定 hello 連結做為`Optional`

#### <a name="application-push-capability"></a>應用程式推播功能
XCode 8 可能會重設您的應用程式發送功能，請再檢查一次在 hello`capability`您選取的目標 索引標籤。

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>加入 hello 新 iOS 10 通知註冊程式碼
hello 較舊的程式碼片段 tooregister hello 應用程式 toonotifications 仍然運作，但使用的 iOS 10 上執行時，被取代 Api。

匯入 hello`User Notification`架構：

        #import <UserNotifications/UserNotifications.h>

在您的應用程式中委派 `application:didFinishLaunchingWithOptions` 方法取代︰

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

依︰

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>解決 UNUserNotificationCenter 委派衝突

如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。

A`UNUserNotificationCenter`委派由 hello SDK toomonitor hello 生命週期的 Engagement 大於或等於 10 在 iOS 上執行的裝置上的通知。 hello SDK 有它自己實作 hello`UNUserNotificationCenterDelegate`通訊協定，但可以是只有一個`UNUserNotificationCenter`委派每個應用程式。 任何其他的委派加入 toohello`UNUserNotificationCenter`物件會與 hello Engagement 其中一個衝突。 如果 hello SDK 偵測到您或任何其他協力廠商的委派，則不會使用它自己的實作 toogive 您機會 tooresolve hello 衝突。 您必須擁有在順序中的委派 tooresolve hello 衝突 tooadd hello Engagement 邏輯 tooyour。

有兩種方式 tooachieve 這。

提案 1，只要轉送您的委派呼叫 toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

或透過繼承自 hello 提案 2，`AEUserNotificationHandler`類別

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> 您可以判斷通知來自 Engagement 或不是藉由傳遞其`userInfo`字典 toohello 代理程式`isEngagementPushPayload:`類別方法。

請確定該 hello`UNUserNotificationCenter`物件的委派設定中任一 hello tooyour 委派`application:willFinishLaunchingWithOptions:`或 hello`application:didFinishLaunchingWithOptions:`應用程式委派的方法。
比方說，如果您已實作提案 1 以上的 hello:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
