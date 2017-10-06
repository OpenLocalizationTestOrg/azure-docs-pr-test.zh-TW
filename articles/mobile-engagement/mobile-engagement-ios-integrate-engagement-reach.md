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
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="63cbd-103">如何 tooIntegrate Engagement 觸達在 iOS 上</span><span class="sxs-lookup"><span data-stu-id="63cbd-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="63cbd-104">您必須遵循 hello 整合程序所述 hello[如何 tooIntegrate Engagement iOS 文件上的](mobile-engagement-ios-integrate-engagement.md)之前依照本指南。</span><span class="sxs-lookup"><span data-stu-id="63cbd-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="63cbd-105">這份文件需要 XCode 8。</span><span class="sxs-lookup"><span data-stu-id="63cbd-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="63cbd-106">如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="63cbd-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="63cbd-107">這個舊版本在 iOS 10 裝置上執行時有已知錯誤︰系統通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="63cbd-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="63cbd-108">toofix 就 tooimplement hello 這個已被取代 API`application:didReceiveRemoteNotification:`在您的應用程式委派，如下所示：</span><span class="sxs-lookup"><span data-stu-id="63cbd-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="63cbd-109">**我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。</span><span class="sxs-lookup"><span data-stu-id="63cbd-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="63cbd-110">您應儘速切換 tooXCode 8。</span><span class="sxs-lookup"><span data-stu-id="63cbd-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="63cbd-111">啟用您的應用程式 tooreceive 無訊息的推播通知</span><span class="sxs-lookup"><span data-stu-id="63cbd-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="63cbd-112">整合步驟</span><span class="sxs-lookup"><span data-stu-id="63cbd-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="63cbd-113">內嵌至 iOS 專案中的 hello Engagement 觸達 SDK</span><span class="sxs-lookup"><span data-stu-id="63cbd-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="63cbd-114">在您的 Xcode 專案中加入 hello 觸達 sdk。</span><span class="sxs-lookup"><span data-stu-id="63cbd-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="63cbd-115">在 Xcode 中，跳過**專案\>新增 tooproject**選擇 hello`EngagementReach`資料夾。</span><span class="sxs-lookup"><span data-stu-id="63cbd-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="63cbd-116">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="63cbd-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="63cbd-117">在實作檔 hello 頂端，匯入 hello Engagement 觸達模組：</span><span class="sxs-lookup"><span data-stu-id="63cbd-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="63cbd-118">在方法內`applicationDidFinishLaunching:`或`application:didFinishLaunchingWithOptions:`、 建立觸達模組並將它傳遞 tooyour 現有 Engagement 初始化行：</span><span class="sxs-lookup"><span data-stu-id="63cbd-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="63cbd-119">修改**'icon.png'** hello 要作為通知圖示的影像名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="63cbd-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="63cbd-120">如果您想要 toouse hello 選項*更新徽章值*觸達活動，或如果您想 toouse 原生推送\<SaaS/觸達 API/活動格式/原生推送\>活動時，您必須讓 hello 觸達模組管理hello 徽章圖示本身 （它會自動清除 hello 應用程式徽章和也重設儲存 Engagement 每當 hello 應用程式未啟動或 foregrounded 的 hello 值）。</span><span class="sxs-lookup"><span data-stu-id="63cbd-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="63cbd-121">這是加入以下各觸達模組初始化之後 hello:</span><span class="sxs-lookup"><span data-stu-id="63cbd-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="63cbd-122">如果您想 toohandle 觸達資料推送，您必須讓您的應用程式委派符合 toohello`AEReachDataPushDelegate`通訊協定。</span><span class="sxs-lookup"><span data-stu-id="63cbd-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="63cbd-123">加入以下各觸達模組初始化之後 hello:</span><span class="sxs-lookup"><span data-stu-id="63cbd-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="63cbd-124">然後，您可以實作 hello 方法`onDataPushStringReceived:`和`onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:`在應用程式委派：</span><span class="sxs-lookup"><span data-stu-id="63cbd-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="63cbd-125">類別</span><span class="sxs-lookup"><span data-stu-id="63cbd-125">Category</span></span>
<span data-ttu-id="63cbd-126">hello 分類參數是選擇性的當您建立將資料推送活動時，可讓您 toofilter 資料推播通知。</span><span class="sxs-lookup"><span data-stu-id="63cbd-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="63cbd-127">這非常有用，如果您想 toopush 不同種類的`Base64`資料而且想 tooidentify 其類型，再剖析它們。</span><span class="sxs-lookup"><span data-stu-id="63cbd-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="63cbd-128">**您的應用程式是現在準備好 tooreceive 和顯示達到內容 ！**</span><span class="sxs-lookup"><span data-stu-id="63cbd-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="63cbd-129">如何 tooreceive 宣告與輪詢隨時</span><span class="sxs-lookup"><span data-stu-id="63cbd-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="63cbd-130">Engagement 可以傳送觸達通知 tooyour 使用者隨時利用 hello Apple Push Notification Service。</span><span class="sxs-lookup"><span data-stu-id="63cbd-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="63cbd-131">tooenable 這項功能，您將有 tooprepare Apple 推播通知的應用程式，並修改您應用程式的委派。</span><span class="sxs-lookup"><span data-stu-id="63cbd-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="63cbd-132">準備好您的應用程式以使用 Apple 推送通知</span><span class="sxs-lookup"><span data-stu-id="63cbd-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="63cbd-133">請遵循 hello 指南：[如何 tooPrepare Apple 推播通知您的應用程式](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="63cbd-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="63cbd-134">加入 hello 必要的用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="63cbd-134">Add hello necessary client code</span></span>
<span data-ttu-id="63cbd-135">*此時您的應用程式應該在 hello Engagement 前端有已註冊的 Apple 推播憑證。*</span><span class="sxs-lookup"><span data-stu-id="63cbd-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="63cbd-136">如果它尚未完成，您需要 tooregister 應用程式 tooreceive 推播通知。</span><span class="sxs-lookup"><span data-stu-id="63cbd-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="63cbd-137">匯入 hello`User Notification`架構：</span><span class="sxs-lookup"><span data-stu-id="63cbd-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="63cbd-138">新增 hello 行下，應用程式啟動時 (通常在`application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="63cbd-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="63cbd-139">然後，您需要 Apple 伺服器傳回的 tooprovide tooEngagement hello 裝置權杖。</span><span class="sxs-lookup"><span data-stu-id="63cbd-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="63cbd-140">這是名為 「 hello 方法`application:didRegisterForRemoteNotificationsWithDeviceToken:`在應用程式委派：</span><span class="sxs-lookup"><span data-stu-id="63cbd-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="63cbd-141">最後，當您的應用程式收到遠端通知擁有 tooinform hello Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="63cbd-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="63cbd-142">會呼叫 toodo hello 方法`applicationDidReceiveRemoteNotification:fetchCompletionHandler:`在應用程式委派：</span><span class="sxs-lookup"><span data-stu-id="63cbd-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="63cbd-143">根據預設，Engagement 觸達控制 hello completionHandler。</span><span class="sxs-lookup"><span data-stu-id="63cbd-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="63cbd-144">如果您想 toomanually 回應 toohello`handler`封鎖您的程式碼中，您可以傳遞 hello nil`handler`引數和控制 hello 完成封鎖自己。</span><span class="sxs-lookup"><span data-stu-id="63cbd-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="63cbd-145">請參閱 hello`UIBackgroundFetchResult`種可能的值清單。</span><span class="sxs-lookup"><span data-stu-id="63cbd-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="63cbd-146">完整範例</span><span class="sxs-lookup"><span data-stu-id="63cbd-146">Full example</span></span>
<span data-ttu-id="63cbd-147">以下是整合的完整範例：</span><span class="sxs-lookup"><span data-stu-id="63cbd-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="63cbd-148">解決 UNUserNotificationCenter 委派衝突</span><span class="sxs-lookup"><span data-stu-id="63cbd-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="63cbd-149">如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。</span><span class="sxs-lookup"><span data-stu-id="63cbd-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="63cbd-150">A`UNUserNotificationCenter`委派由 hello SDK toomonitor hello 生命週期的 Engagement 大於或等於 10 在 iOS 上執行的裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="63cbd-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="63cbd-151">hello SDK 有它自己實作 hello`UNUserNotificationCenterDelegate`通訊協定，但可以是只有一個`UNUserNotificationCenter`委派每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="63cbd-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="63cbd-152">任何其他的委派加入 toohello`UNUserNotificationCenter`物件會與 hello Engagement 其中一個衝突。</span><span class="sxs-lookup"><span data-stu-id="63cbd-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="63cbd-153">如果 hello SDK 偵測到您或任何其他協力廠商的委派，則不會使用它自己的實作 toogive 您機會 tooresolve hello 衝突。</span><span class="sxs-lookup"><span data-stu-id="63cbd-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="63cbd-154">您必須擁有在順序中的委派 tooresolve hello 衝突 tooadd hello Engagement 邏輯 tooyour。</span><span class="sxs-lookup"><span data-stu-id="63cbd-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="63cbd-155">有兩種方式 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="63cbd-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="63cbd-156">提案 1，只要轉送您的委派呼叫 toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="63cbd-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="63cbd-157">或透過繼承自 hello 提案 2，`AEUserNotificationHandler`類別</span><span class="sxs-lookup"><span data-stu-id="63cbd-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="63cbd-158">您可以判斷通知來自 Engagement 或不是藉由傳遞其`userInfo`字典 toohello 代理程式`isEngagementPushPayload:`類別方法。</span><span class="sxs-lookup"><span data-stu-id="63cbd-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="63cbd-159">請確定該 hello`UNUserNotificationCenter`物件的委派設定中任一 hello tooyour 委派`application:willFinishLaunchingWithOptions:`或 hello`application:didFinishLaunchingWithOptions:`應用程式委派的方法。</span><span class="sxs-lookup"><span data-stu-id="63cbd-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="63cbd-160">比方說，如果您已實作提案 1 以上的 hello:</span><span class="sxs-lookup"><span data-stu-id="63cbd-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="63cbd-161">如何 toocustomize 活動</span><span class="sxs-lookup"><span data-stu-id="63cbd-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="63cbd-162">通知</span><span class="sxs-lookup"><span data-stu-id="63cbd-162">Notifications</span></span>
<span data-ttu-id="63cbd-163">有兩種通知類型： 系統通知和應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="63cbd-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="63cbd-164">系統通知都是由 iOS 處理，且無法自訂。</span><span class="sxs-lookup"><span data-stu-id="63cbd-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="63cbd-165">應用程式內通知是由以動態方式加入 toohello 目前應用程式視窗的檢視。</span><span class="sxs-lookup"><span data-stu-id="63cbd-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="63cbd-166">這稱為通知重疊。</span><span class="sxs-lookup"><span data-stu-id="63cbd-166">This is called a notification overlay.</span></span> <span data-ttu-id="63cbd-167">通知的影像覆疊非常適合在快速地整合在一起，因為它們不需要您 toomodify 應用程式中的任何檢視。</span><span class="sxs-lookup"><span data-stu-id="63cbd-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="63cbd-168">版面配置</span><span class="sxs-lookup"><span data-stu-id="63cbd-168">Layout</span></span>
<span data-ttu-id="63cbd-169">您的應用程式內通知 toomodify hello 外觀，您可以只修改 hello 檔案`AENotificationView.xib`tooyour 需要只要您保留 hello 標記值和類型的 hello 現有 subviews。</span><span class="sxs-lookup"><span data-stu-id="63cbd-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="63cbd-170">根據預設，應用程式內通知會顯示在 hello 囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="63cbd-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="63cbd-171">如果您偏好 toodisplay 它們在畫面上，編輯 hello hello 頂端提供`AENotificationView.xib`並變更 hello `AutoSizing` hello 主要檢視，也可以保持在最上方 hello 其超級檢視表的屬性。</span><span class="sxs-lookup"><span data-stu-id="63cbd-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="63cbd-172">類別</span><span class="sxs-lookup"><span data-stu-id="63cbd-172">Categories</span></span>
<span data-ttu-id="63cbd-173">當您修改 hello 提供版面配置時，您修改您的通知 hello 外觀。</span><span class="sxs-lookup"><span data-stu-id="63cbd-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="63cbd-174">類別可讓您 toodefine 各種目標會尋找通知 （可能是行為）。</span><span class="sxs-lookup"><span data-stu-id="63cbd-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="63cbd-175">當您建立觸達活動時可以指定類別。</span><span class="sxs-lookup"><span data-stu-id="63cbd-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="63cbd-176">請記住，類別也可讓您自訂宣告與輪詢，本文件稍後將會說明。</span><span class="sxs-lookup"><span data-stu-id="63cbd-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="63cbd-177">tooregister 您的通知的類別處理常式，您需要的 tooadd 當 hello 達到模組的呼叫已初始化。</span><span class="sxs-lookup"><span data-stu-id="63cbd-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="63cbd-178">`myNotifier`必須是符合 toohello 通訊協定的物件執行個體`AENotifier`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="63cbd-179">您可以實作自己的 hello 通訊協定方法，或者您可以選擇 tooreimplement hello 現有類別`AEDefaultNotifier`它已經執行 hello 工作的絕大部分。</span><span class="sxs-lookup"><span data-stu-id="63cbd-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="63cbd-180">例如，如果您想 tooredefine hello 通知檢視特定分類，您可以依照此範例中：</span><span class="sxs-lookup"><span data-stu-id="63cbd-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="63cbd-181">這個簡單的類別範例假設您已在主要的應用程式套件組合中有一個名為 `MyNotificationView.xib` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="63cbd-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="63cbd-182">如果 hello 方法不能 toofind 對應`.xib`、 將不會顯示 hello 通知和 Engagement 會輸出 hello 主控台中的訊息。</span><span class="sxs-lookup"><span data-stu-id="63cbd-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="63cbd-183">提供的 hello nib 檔案應該遵守下列規則的 hello:</span><span class="sxs-lookup"><span data-stu-id="63cbd-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="63cbd-184">它應該只包含一個檢視。</span><span class="sxs-lookup"><span data-stu-id="63cbd-184">It should only contain one view.</span></span>
* <span data-ttu-id="63cbd-185">Subviews 應該是相同類型作為 hello 是名為提供的 hello nib 檔案內的 hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="63cbd-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="63cbd-186">Subviews 應該具有相同標記為 hello 是名為提供的 hello nib 檔案內的 hello`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="63cbd-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="63cbd-187">只複製提供的 hello nib 檔，名稱為`AENotificationView.xib`，並開始從該處工作。</span><span class="sxs-lookup"><span data-stu-id="63cbd-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="63cbd-188">但請小心，hello 的內這個 nib 檔案相關聯 toohello 類別檢視`AENotificationView`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="63cbd-189">這個類別已重新定義 hello 方法`layoutSubViews`toomove 和調整大小，根據 toocontext 其 subviews。</span><span class="sxs-lookup"><span data-stu-id="63cbd-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="63cbd-190">您可能會想 tooreplace 它與`UIView`或自訂的檢視類別。</span><span class="sxs-lookup"><span data-stu-id="63cbd-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="63cbd-191">如果您需要更深入自訂您的通知 （如果您想執行個體 tooload 直接從 hello 程式碼檢視），則建議的 tootake hello 查看所提供的來源的程式碼和類別文件`Protocol ReferencesDefaultNotifier`和`AENotifier`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="63cbd-192">請注意，您可以使用 hello 的多個類別相同的通知。</span><span class="sxs-lookup"><span data-stu-id="63cbd-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="63cbd-193">您可以也重新定義的 hello 預設通知，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="63cbd-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="63cbd-194">通知處理</span><span class="sxs-lookup"><span data-stu-id="63cbd-194">Notification handling</span></span>
<span data-ttu-id="63cbd-195">使用 hello 預設分類，某些存留週期方法會呼叫在 hello`AEReachContent`物件 tooreport 統計資料和更新 hello 活動狀態：</span><span class="sxs-lookup"><span data-stu-id="63cbd-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="63cbd-196">當應用程式中會顯示 hello 通知時，hello`displayNotification`方法呼叫 （它會報告統計資料） 所`AEReachModule`如果`handleNotification:`傳回`YES`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="63cbd-197">如果關閉 hello 通知，hello`exitNotification`呼叫方法時，統計資料會報告，並可立即處理下一個活動。</span><span class="sxs-lookup"><span data-stu-id="63cbd-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="63cbd-198">如果按一下 hello 通知，`actionNotification`是呼叫，統計資料會報告並不會執行相關聯的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="63cbd-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="63cbd-199">如果您實作`AENotifier`略過 hello 預設行為，您自己有 toocall 這些生命週期的方法。</span><span class="sxs-lookup"><span data-stu-id="63cbd-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="63cbd-200">hello 遵循範例將說明某些情況下，會在略過 hello 預設行為：</span><span class="sxs-lookup"><span data-stu-id="63cbd-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="63cbd-201">您不延伸 `AEDefaultNotifier`，例如從頭開始實作類別處理。</span><span class="sxs-lookup"><span data-stu-id="63cbd-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="63cbd-202">您已覆寫`prepareNotificationView:forContent:`，至少是確定 toomap`onNotificationActioned`或`onNotificationExited`tooone U.I 控制項。</span><span class="sxs-lookup"><span data-stu-id="63cbd-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="63cbd-203">如果`handleNotification:`擲回例外狀況，hello 內容會刪除與`drop`是呼叫，這報告的統計資料，而現在可處理下一個活動。</span><span class="sxs-lookup"><span data-stu-id="63cbd-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="63cbd-204">將通知併入現有的檢視</span><span class="sxs-lookup"><span data-stu-id="63cbd-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="63cbd-205">重疊最適合用於快速整合，但有些時候不太方便，或是造成不想要的副作用。</span><span class="sxs-lookup"><span data-stu-id="63cbd-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="63cbd-206">如果您不滿意 hello 重疊系統的某些資料檢視，您可以針對這些檢視來進行自訂。</span><span class="sxs-lookup"><span data-stu-id="63cbd-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="63cbd-207">您可以在現有的檢視決定 tooinclude 我們通知版面配置。</span><span class="sxs-lookup"><span data-stu-id="63cbd-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="63cbd-208">toodo，還有兩種實作樣式：</span><span class="sxs-lookup"><span data-stu-id="63cbd-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="63cbd-209">新增使用介面產生器的 hello 通知檢視</span><span class="sxs-lookup"><span data-stu-id="63cbd-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="63cbd-210">開啟 [介面產生器] </span><span class="sxs-lookup"><span data-stu-id="63cbd-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="63cbd-211">放置 320 x 60 （或 768 x 60，如果您在 iPad 上）`UIView`想 hello 通知 tooappear</span><span class="sxs-lookup"><span data-stu-id="63cbd-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="63cbd-212">設定此檢視的 hello 標記值太： **36822491**</span><span class="sxs-lookup"><span data-stu-id="63cbd-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="63cbd-213">以程式設計方式加入 hello 通知檢視。</span><span class="sxs-lookup"><span data-stu-id="63cbd-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="63cbd-214">只要加入您的檢視已初始化時，下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="63cbd-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="63cbd-215">您可以在 `AEDefaultNotifier.h` 中找到 `NOTIFICATION_AREA_VIEW_TAG` 巨集。</span><span class="sxs-lookup"><span data-stu-id="63cbd-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="63cbd-216">hello 預設通知程式會自動偵測該 hello 通知版面配置包含在此檢視，就不會為其新增覆疊。</span><span class="sxs-lookup"><span data-stu-id="63cbd-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="63cbd-217">宣告和輪詢</span><span class="sxs-lookup"><span data-stu-id="63cbd-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="63cbd-218">版面配置</span><span class="sxs-lookup"><span data-stu-id="63cbd-218">Layouts</span></span>
<span data-ttu-id="63cbd-219">您可以修改 hello 檔`AEDefaultAnnouncementView.xib`和`AEDefaultPollView.xib`，只要您保留 hello 標記值和類型的 hello 現有 subviews。</span><span class="sxs-lookup"><span data-stu-id="63cbd-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="63cbd-220">類別</span><span class="sxs-lookup"><span data-stu-id="63cbd-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="63cbd-221">替代版面配置</span><span class="sxs-lookup"><span data-stu-id="63cbd-221">Alternate layouts</span></span>
<span data-ttu-id="63cbd-222">通知，如同 hello 活動的類別可以是您的宣告與輪詢使用的 toohave 替代配置。</span><span class="sxs-lookup"><span data-stu-id="63cbd-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="63cbd-223">toocreate 通知的類別，您必須擴充**AEAnnouncementViewController**並將其註冊之後尚未初始化 hello 觸達模組：</span><span class="sxs-lookup"><span data-stu-id="63cbd-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="63cbd-224">每當使用者將按一下通知，以與 hello 類別宣告"我\_類別目錄 」，您已註冊的檢視控制器 (在此情況下`MyCustomAnnouncementViewController`) 會藉由呼叫 hello 方法初始化`initWithAnnouncement:`hello 檢視將會加入的 toohello 目前的應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="63cbd-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="63cbd-225">在您實作中的 hello`AEAnnouncementViewController`類別就 tooread hello 屬性`announcement`tooinitialize 您 subviews。</span><span class="sxs-lookup"><span data-stu-id="63cbd-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="63cbd-226">請考慮 hello 範例所示，兩個標籤會使用初始化`title`和`body`屬性 hello`AEReachAnnouncement`類別：</span><span class="sxs-lookup"><span data-stu-id="63cbd-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="63cbd-227">如果您不想 tooload 檢視自己，但您只想 tooreuse hello 預設公告檢視版面配置，您只可以讓您自訂檢視的控制器延伸所提供的 hello 類別`AEDefaultAnnouncementViewController`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="63cbd-228">在此情況下，重複的 hello nib 檔案`AEDefaultAnnouncementView.xib`並將它重新命名，所以它可以載入由您的自訂檢視控制器 (控制器，名為`CustomAnnouncementViewController`，您應該呼叫 nib 檔案`CustomAnnouncementView.xib`)。</span><span class="sxs-lookup"><span data-stu-id="63cbd-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="63cbd-229">tooreplace hello 預設分類的宣告，只是註冊 hello 類別中定義的自訂檢視控制器`kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="63cbd-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="63cbd-230">輪詢可以是自訂的 hello 相同的方式：</span><span class="sxs-lookup"><span data-stu-id="63cbd-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="63cbd-231">這個時間，提供 hello`MyCustomPollViewController`必須擴充`AEPollViewController`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="63cbd-232">您可以選擇 tooextend hello 預設控制器或者： `AEDefaultPollViewController`。</span><span class="sxs-lookup"><span data-stu-id="63cbd-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63cbd-233">請不要忘記 toocall `action` (`submitAnswers:`自訂輪詢檢視控制站) 或`exit`方法之前關閉 hello 檢視控制器。</span><span class="sxs-lookup"><span data-stu-id="63cbd-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="63cbd-234">否則，統計資料將不會傳送 （也就是在 hello 活動上的任何分析），而且 hello 應用程式處理序重新啟動之前，不會通知多個重要的是下一個活動。</span><span class="sxs-lookup"><span data-stu-id="63cbd-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="63cbd-235">實作範例</span><span class="sxs-lookup"><span data-stu-id="63cbd-235">Implementation example</span></span>
<span data-ttu-id="63cbd-236">在此實作中從外部 xib 檔案載入 hello 公告自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="63cbd-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="63cbd-237">類似的進階的通知自訂建議 toolook 在 hello 標準實作 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="63cbd-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

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
