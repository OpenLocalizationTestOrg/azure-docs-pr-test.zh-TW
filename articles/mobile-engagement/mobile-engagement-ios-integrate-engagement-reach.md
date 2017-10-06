---
title: "Mobile Engagement iOS SDK 到達整合 aaaAzure |Microsoft 文件"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>如何 tooIntegrate Engagement 觸達在 iOS 上
您必須遵循 hello 整合程序所述 hello[如何 tooIntegrate Engagement iOS 文件上的](mobile-engagement-ios-integrate-engagement.md)之前依照本指南。

這份文件需要 XCode 8。 如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。 這個舊版本在 iOS 10 裝置上執行時有已知錯誤︰系統通知不會採取動作。 toofix 就 tooimplement hello 這個已被取代 API`application:didReceiveRemoteNotification:`在您的應用程式委派，如下所示：

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。 您應儘速切換 tooXCode 8。
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>啟用您的應用程式 tooreceive 無訊息的推播通知
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>整合步驟
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>內嵌至 iOS 專案中的 hello Engagement 觸達 SDK
* 在您的 Xcode 專案中加入 hello 觸達 sdk。 在 Xcode 中，跳過**專案\>新增 tooproject**選擇 hello`EngagementReach`資料夾。

### <a name="modify-your-application-delegate"></a>修改您的應用程式代理人
* 在實作檔 hello 頂端，匯入 hello Engagement 觸達模組：

      [...]
      #import "AEReachModule.h"
* 在方法內`applicationDidFinishLaunching:`或`application:didFinishLaunchingWithOptions:`、 建立觸達模組並將它傳遞 tooyour 現有 Engagement 初始化行：

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* 修改**'icon.png'** hello 要作為通知圖示的影像名稱的字串。
* 如果您想要 toouse hello 選項*更新徽章值*觸達活動，或如果您想 toouse 原生推送\<SaaS/觸達 API/活動格式/原生推送\>活動時，您必須讓 hello 觸達模組管理hello 徽章圖示本身 （它會自動清除 hello 應用程式徽章和也重設儲存 Engagement 每當 hello 應用程式未啟動或 foregrounded 的 hello 值）。 這是加入以下各觸達模組初始化之後 hello:

      [reach setAutoBadgeEnabled:YES];
* 如果您想 toohandle 觸達資料推送，您必須讓您的應用程式委派符合 toohello`AEReachDataPushDelegate`通訊協定。 加入以下各觸達模組初始化之後 hello:

      [reach setDataPushDelegate:self];
* 然後，您可以實作 hello 方法`onDataPushStringReceived:`和`onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:`在應用程式委派：

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>類別
hello 分類參數是選擇性的當您建立將資料推送活動時，可讓您 toofilter 資料推播通知。 這非常有用，如果您想 toopush 不同種類的`Base64`資料而且想 tooidentify 其類型，再剖析它們。

**您的應用程式是現在準備好 tooreceive 和顯示達到內容 ！**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>如何 tooreceive 宣告與輪詢隨時
Engagement 可以傳送觸達通知 tooyour 使用者隨時利用 hello Apple Push Notification Service。

tooenable 這項功能，您將有 tooprepare Apple 推播通知的應用程式，並修改您應用程式的委派。

### <a name="prepare-your-application-for-apple-push-notifications"></a>準備好您的應用程式以使用 Apple 推送通知
請遵循 hello 指南：[如何 tooPrepare Apple 推播通知您的應用程式](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>加入 hello 必要的用戶端程式碼
*此時您的應用程式應該在 hello Engagement 前端有已註冊的 Apple 推播憑證。*

如果它尚未完成，您需要 tooregister 應用程式 tooreceive 推播通知。

* 匯入 hello`User Notification`架構：

        #import <UserNotifications/UserNotifications.h>
* 新增 hello 行下，應用程式啟動時 (通常在`application:didFinishLaunchingWithOptions:`):

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

然後，您需要 Apple 伺服器傳回的 tooprovide tooEngagement hello 裝置權杖。 這是名為 「 hello 方法`application:didRegisterForRemoteNotificationsWithDeviceToken:`在應用程式委派：

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

最後，當您的應用程式收到遠端通知擁有 tooinform hello Engagement SDK。 會呼叫 toodo hello 方法`applicationDidReceiveRemoteNotification:fetchCompletionHandler:`在應用程式委派：

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> 根據預設，Engagement 觸達控制 hello completionHandler。 如果您想 toomanually 回應 toohello`handler`封鎖您的程式碼中，您可以傳遞 hello nil`handler`引數和控制 hello 完成封鎖自己。 請參閱 hello`UIBackgroundFetchResult`種可能的值清單。
>
>

### <a name="full-example"></a>完整範例
以下是整合的完整範例：

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
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

## <a name="how-toocustomize-campaigns"></a>如何 toocustomize 活動
### <a name="notifications"></a>通知
有兩種通知類型： 系統通知和應用程式內通知。

系統通知都是由 iOS 處理，且無法自訂。

應用程式內通知是由以動態方式加入 toohello 目前應用程式視窗的檢視。 這稱為通知重疊。 通知的影像覆疊非常適合在快速地整合在一起，因為它們不需要您 toomodify 應用程式中的任何檢視。

#### <a name="layout"></a>版面配置
您的應用程式內通知 toomodify hello 外觀，您可以只修改 hello 檔案`AENotificationView.xib`tooyour 需要只要您保留 hello 標記值和類型的 hello 現有 subviews。

根據預設，應用程式內通知會顯示在 hello 囉 」 畫面底部。 如果您偏好 toodisplay 它們在畫面上，編輯 hello hello 頂端提供`AENotificationView.xib`並變更 hello `AutoSizing` hello 主要檢視，也可以保持在最上方 hello 其超級檢視表的屬性。

#### <a name="categories"></a>類別
當您修改 hello 提供版面配置時，您修改您的通知 hello 外觀。 類別可讓您 toodefine 各種目標會尋找通知 （可能是行為）。 當您建立觸達活動時可以指定類別。 請記住，類別也可讓您自訂宣告與輪詢，本文件稍後將會說明。

tooregister 您的通知的類別處理常式，您需要的 tooadd 當 hello 達到模組的呼叫已初始化。

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`必須是符合 toohello 通訊協定的物件執行個體`AENotifier`。

您可以實作自己的 hello 通訊協定方法，或者您可以選擇 tooreimplement hello 現有類別`AEDefaultNotifier`它已經執行 hello 工作的絕大部分。

例如，如果您想 tooredefine hello 通知檢視特定分類，您可以依照此範例中：

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

這個簡單的類別範例假設您已在主要的應用程式套件組合中有一個名為 `MyNotificationView.xib` 的檔案。 如果 hello 方法不能 toofind 對應`.xib`、 將不會顯示 hello 通知和 Engagement 會輸出 hello 主控台中的訊息。

提供的 hello nib 檔案應該遵守下列規則的 hello:

* 它應該只包含一個檢視。
* Subviews 應該是相同類型作為 hello 是名為提供的 hello nib 檔案內的 hello`AENotificationView.xib`
* Subviews 應該具有相同標記為 hello 是名為提供的 hello nib 檔案內的 hello`AENotificationView.xib`

> [!TIP]
> 只複製提供的 hello nib 檔，名稱為`AENotificationView.xib`，並開始從該處工作。 但請小心，hello 的內這個 nib 檔案相關聯 toohello 類別檢視`AENotificationView`。 這個類別已重新定義 hello 方法`layoutSubViews`toomove 和調整大小，根據 toocontext 其 subviews。 您可能會想 tooreplace 它與`UIView`或自訂的檢視類別。
>
>

如果您需要更深入自訂您的通知 （如果您想執行個體 tooload 直接從 hello 程式碼檢視），則建議的 tootake hello 查看所提供的來源的程式碼和類別文件`Protocol ReferencesDefaultNotifier`和`AENotifier`。

請注意，您可以使用 hello 的多個類別相同的通知。

您可以也重新定義的 hello 預設通知，就像這樣：

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>通知處理
使用 hello 預設分類，某些存留週期方法會呼叫在 hello`AEReachContent`物件 tooreport 統計資料和更新 hello 活動狀態：

* 當應用程式中會顯示 hello 通知時，hello`displayNotification`方法呼叫 （它會報告統計資料） 所`AEReachModule`如果`handleNotification:`傳回`YES`。
* 如果關閉 hello 通知，hello`exitNotification`呼叫方法時，統計資料會報告，並可立即處理下一個活動。
* 如果按一下 hello 通知，`actionNotification`是呼叫，統計資料會報告並不會執行相關聯的 hello 動作。

如果您實作`AENotifier`略過 hello 預設行為，您自己有 toocall 這些生命週期的方法。 hello 遵循範例將說明某些情況下，會在略過 hello 預設行為：

* 您不延伸 `AEDefaultNotifier`，例如從頭開始實作類別處理。
* 您已覆寫`prepareNotificationView:forContent:`，至少是確定 toomap`onNotificationActioned`或`onNotificationExited`tooone U.I 控制項。

> [!WARNING]
> 如果`handleNotification:`擲回例外狀況，hello 內容會刪除與`drop`是呼叫，這報告的統計資料，而現在可處理下一個活動。
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>將通知併入現有的檢視
重疊最適合用於快速整合，但有些時候不太方便，或是造成不想要的副作用。

如果您不滿意 hello 重疊系統的某些資料檢視，您可以針對這些檢視來進行自訂。

您可以在現有的檢視決定 tooinclude 我們通知版面配置。 toodo，還有兩種實作樣式：

1. 新增使用介面產生器的 hello 通知檢視

   * 開啟 [介面產生器] 
   * 放置 320 x 60 （或 768 x 60，如果您在 iPad 上）`UIView`想 hello 通知 tooappear
   * 設定此檢視的 hello 標記值太： **36822491**
2. 以程式設計方式加入 hello 通知檢視。 只要加入您的檢視已初始化時，下列程式碼的 hello:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

您可以在 `AEDefaultNotifier.h` 中找到 `NOTIFICATION_AREA_VIEW_TAG` 巨集。

> [!NOTE]
> hello 預設通知程式會自動偵測該 hello 通知版面配置包含在此檢視，就不會為其新增覆疊。
>
>

### <a name="announcements-and-polls"></a>宣告和輪詢
#### <a name="layouts"></a>版面配置
您可以修改 hello 檔`AEDefaultAnnouncementView.xib`和`AEDefaultPollView.xib`，只要您保留 hello 標記值和類型的 hello 現有 subviews。

#### <a name="categories"></a>類別
##### <a name="alternate-layouts"></a>替代版面配置
通知，如同 hello 活動的類別可以是您的宣告與輪詢使用的 toohave 替代配置。

toocreate 通知的類別，您必須擴充**AEAnnouncementViewController**並將其註冊之後尚未初始化 hello 觸達模組：

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> 每當使用者將按一下通知，以與 hello 類別宣告"我\_類別目錄 」，您已註冊的檢視控制器 (在此情況下`MyCustomAnnouncementViewController`) 會藉由呼叫 hello 方法初始化`initWithAnnouncement:`hello 檢視將會加入的 toohello 目前的應用程式視窗。
>
>

在您實作中的 hello`AEAnnouncementViewController`類別就 tooread hello 屬性`announcement`tooinitialize 您 subviews。 請考慮 hello 範例所示，兩個標籤會使用初始化`title`和`body`屬性 hello`AEReachAnnouncement`類別：

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

如果您不想 tooload 檢視自己，但您只想 tooreuse hello 預設公告檢視版面配置，您只可以讓您自訂檢視的控制器延伸所提供的 hello 類別`AEDefaultAnnouncementViewController`。 在此情況下，重複的 hello nib 檔案`AEDefaultAnnouncementView.xib`並將它重新命名，所以它可以載入由您的自訂檢視控制器 (控制器，名為`CustomAnnouncementViewController`，您應該呼叫 nib 檔案`CustomAnnouncementView.xib`)。

tooreplace hello 預設分類的宣告，只是註冊 hello 類別中定義的自訂檢視控制器`kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

輪詢可以是自訂的 hello 相同的方式：

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

這個時間，提供 hello`MyCustomPollViewController`必須擴充`AEPollViewController`。 您可以選擇 tooextend hello 預設控制器或者： `AEDefaultPollViewController`。

> [!IMPORTANT]
> 請不要忘記 toocall `action` (`submitAnswers:`自訂輪詢檢視控制站) 或`exit`方法之前關閉 hello 檢視控制器。 否則，統計資料將不會傳送 （也就是在 hello 活動上的任何分析），而且 hello 應用程式處理序重新啟動之前，不會通知多個重要的是下一個活動。
>
>

##### <a name="implementation-example"></a>實作範例
在此實作中從外部 xib 檔案載入 hello 公告自訂檢視。

類似的進階的通知自訂建議 toolook 在 hello 標準實作 hello 原始程式碼。

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
