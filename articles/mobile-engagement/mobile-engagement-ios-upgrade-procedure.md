---
title: "Mobile Engagement iOS SDK 升級程序 aaaAzure |Microsoft 文件"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>升級程序
如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。

為每個新的 hello SDK 版本，您必須先取代 （移除並重新匯入在 xcode 中） hello EngagementSDK 和 EngagementReach 資料夾。

## <a name="from-300-too400"></a>從 3.0.0 too4.0.0
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

### <a name="usernotifications-framework"></a>UserNotifications 架構
您需要 tooadd hello`UserNotifications`您建置階段中的架構。

hello 專案總管 中開啟您專案窗格並選取 hello 正確的目標。 然後，開啟 hello **建置階段** 索引標籤在 hello **< 連結二進位與媒體櫃**功能表上，加入架構`UserNotifications.framework`-設定 hello 連結做為`Optional`

### <a name="application-push-capability"></a>應用程式推播功能
XCode 8 可能會重設您的應用程式發送功能，請再檢查一次在 hello`capability`您選取的目標 索引標籤。

### <a name="add-hello-new-ios-10-notification-registration-code"></a>加入 hello 新 iOS 10 通知註冊程式碼
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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>解決 UNUserNotificationCenter 委派衝突

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

## <a name="from-200-too300"></a>從 2.0.0 too3.0.0
停止支援 iOS 4.X。 從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 6。

如果您使用觸達應用程式中，您必須新增`remote-notification`值 toohello`UIBackgroundModes`順序 tooreceive 遠端通知 Info.plist 檔案中的陣列。

hello 方法`application:didReceiveRemoteNotification:`需要取代 toobe`application:didReceiveRemoteNotification:fetchCompletionHandler:`在應用程式委派。

已被取代"AEPushDelegate.h 」 介面，且需要 tooremove 所有參考。 這包括移除`[[EngagementAgent shared] setPushDelegate:self]`和 hello 委派方法，從您的應用程式委派：

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>從 1.16.0 too2.0.0
hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。
如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.16，然後套用 hello 遵循程序。

> [!IMPORTANT]
> Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。 移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器
> 
> 

### <a name="agent"></a>代理程式
hello 方法`registerApp:`已由 hello 新方法取代`init:`。 您的應用程式委派必須隨之更新，並使用連接字串：

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

您只需要 tooremove 的所有執行個體的 SDK 中已移除 SmartAd 追蹤`AETrackModule`類別

### <a name="class-name-changes"></a>類別名稱變更
Hello rebranding 的一部分，有幾個需要 toobe 變更的類別/檔案名稱。

所有首碼為 "CP" 的類別，都使用 "AE" 首碼重新命名。

範例：

* `CPModule.h`重新命名過`AEModule.h`。

所有首碼為 "Capptain" 的類別，都已使用 "Engagement" 首碼重新命名。

範例：

* hello 類別`CapptainAgent`重新命名過`EngagementAgent`。
* hello 類別`CapptainTableViewController`重新命名過`EngagementTableViewController`。
* hello 類別`CapptainUtils`重新命名過`EngagementUtils`。
* hello 類別`CapptainViewController`重新命名過`EngagementViewController`。

