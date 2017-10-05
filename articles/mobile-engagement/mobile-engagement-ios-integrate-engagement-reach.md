---
title: "Azure Mobile Engagement iOS SDK Reach 整合 | Microsoft Docs"
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
ms.openlocfilehash: ba74e0c442ac10f096d465f989e03d2ceae8cd88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="cb41a-103">如何在 iOS 上整合 Engagement Reach</span><span class="sxs-lookup"><span data-stu-id="cb41a-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="cb41a-104">在遵循此指南之前，您必須先遵循 [如何在 iOS 上整合 Engagement](mobile-engagement-ios-integrate-engagement.md) 文件中所說明的整合程序。</span><span class="sxs-lookup"><span data-stu-id="cb41a-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="cb41a-105">這份文件需要 XCode 8。</span><span class="sxs-lookup"><span data-stu-id="cb41a-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="cb41a-106">如果您實際上是仰賴 XCode 7，則可以使用 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="cb41a-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="cb41a-107">這個舊版本在 iOS 10 裝置上執行時有已知錯誤︰系統通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="cb41a-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="cb41a-108">若要修正此錯誤，您必須在應用程式委派中實作已被取代的 API `application:didReceiveRemoteNotification:` ，方式如下︰</span><span class="sxs-lookup"><span data-stu-id="cb41a-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="cb41a-109">**我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。</span><span class="sxs-lookup"><span data-stu-id="cb41a-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="cb41a-110">您應盡快改用 XCode 8。</span><span class="sxs-lookup"><span data-stu-id="cb41a-110">You should switch to XCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="cb41a-111">啟用應用程式接收無聲推播通知</span><span class="sxs-lookup"><span data-stu-id="cb41a-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="cb41a-112">整合步驟</span><span class="sxs-lookup"><span data-stu-id="cb41a-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="cb41a-113">將 Engagement Reach SDK 嵌入您的 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="cb41a-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="cb41a-114">在您的 Xcode 專案中加入 Reach SDK。</span><span class="sxs-lookup"><span data-stu-id="cb41a-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="cb41a-115">在 Xcode 中，移至 [專案] \> [新增至專案]，然後選擇 `EngagementReach` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cb41a-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="cb41a-116">修改您的應用程式代理人</span><span class="sxs-lookup"><span data-stu-id="cb41a-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="cb41a-117">在您的實作檔案頂端，匯入 Engagement Reach 模組：</span><span class="sxs-lookup"><span data-stu-id="cb41a-117">At the top of your implementation file, import the Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="cb41a-118">在 `applicationDidFinishLaunching:` 或 `application:didFinishLaunchingWithOptions:` 方法內建立觸達模組，並將它傳遞到您現有的 Engagement 初始化行：</span><span class="sxs-lookup"><span data-stu-id="cb41a-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="cb41a-119">使用您想做為通知圖示的影像名稱修改 **'icon.png'** 字串。</span><span class="sxs-lookup"><span data-stu-id="cb41a-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="cb41a-120">如果您想在觸達活動中使用 [更新徽章值] 選項，或想使用原生推送 \</SaaS/Reach API/Campaign format/Native Push\> 活動，必須讓觸達模組自行管理徽章圖示 (它會自動清除應用程式徽章，也會重設每一次應用程式啟動或於前景執行時，由 Engagement 所儲存的值)。</span><span class="sxs-lookup"><span data-stu-id="cb41a-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="cb41a-121">做法是在觸達模組初始化之後加入以下這一行：</span><span class="sxs-lookup"><span data-stu-id="cb41a-121">This is done by adding the following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="cb41a-122">如果您想要處理觸達資料推送，必須讓您的應用程式委派符合 `AEReachDataPushDelegate` 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cb41a-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="cb41a-123">觸達模組初始化之後請加入以下這一行：</span><span class="sxs-lookup"><span data-stu-id="cb41a-123">Add the following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="cb41a-124">然後您就可以在應用程式委派中實作 `onDataPushStringReceived:` 與 `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` 方法：</span><span class="sxs-lookup"><span data-stu-id="cb41a-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="cb41a-125">類別</span><span class="sxs-lookup"><span data-stu-id="cb41a-125">Category</span></span>
<span data-ttu-id="cb41a-126">當您建立「資料推送」活動時，類別參數是選用的，且可讓您篩選資料推送。</span><span class="sxs-lookup"><span data-stu-id="cb41a-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="cb41a-127">如果您想要推送不同種類的 `Base64` 資料，且想要在剖析這些資料之前識別其類型，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="cb41a-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="cb41a-128">**您的應用程式現在已準備好接收及顯示觸達內容！**</span><span class="sxs-lookup"><span data-stu-id="cb41a-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="cb41a-129">如何隨時接收宣告和輪詢</span><span class="sxs-lookup"><span data-stu-id="cb41a-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="cb41a-130">透過使用 Apple Push Notification Service，Engagement 就可以隨時傳送觸達通知給您的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb41a-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="cb41a-131">若要啟用這項功能，必須準備好您的應用程式以使用 Apple 推送通知，並修改您的應用程式委派。</span><span class="sxs-lookup"><span data-stu-id="cb41a-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="cb41a-132">準備好您的應用程式以使用 Apple 推送通知</span><span class="sxs-lookup"><span data-stu-id="cb41a-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="cb41a-133">請依照本指南進行： [如何準備您的應用程式以使用 Apple 推播通知](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="cb41a-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="cb41a-134">加入必要的用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="cb41a-134">Add the necessary client code</span></span>
<span data-ttu-id="cb41a-135">*目前您的應用程式應該在 Engagement 前端具備已註冊的 Apple 推送憑證。*</span><span class="sxs-lookup"><span data-stu-id="cb41a-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="cb41a-136">如果尚未這麼做，必須註冊應用程式以接收推送通知。</span><span class="sxs-lookup"><span data-stu-id="cb41a-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="cb41a-137">匯入 `User Notification` 架構：</span><span class="sxs-lookup"><span data-stu-id="cb41a-137">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="cb41a-138">啟動您的應用程式時，請新增以下這一行 (通常在 `application:didFinishLaunchingWithOptions:`中)：</span><span class="sxs-lookup"><span data-stu-id="cb41a-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="cb41a-139">然後，您需要將 Apple 伺服器傳回的裝置權杖提供給 Engagement。</span><span class="sxs-lookup"><span data-stu-id="cb41a-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="cb41a-140">這會在您應用程式委派的 `application:didRegisterForRemoteNotificationsWithDeviceToken:` 方法中完成：</span><span class="sxs-lookup"><span data-stu-id="cb41a-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="cb41a-141">最後，當您的應用程式接收到遠端通知時，必須告知 Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="cb41a-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="cb41a-142">若要這麼做，請呼叫您應用程式委派中的 `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` 方法：</span><span class="sxs-lookup"><span data-stu-id="cb41a-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="cb41a-143">根據預設，Engagement Reach 控制 completionHandler。</span><span class="sxs-lookup"><span data-stu-id="cb41a-143">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="cb41a-144">如果您想以手動方式回應您程式碼中的 `handler` 區塊，可以針對 `handler` 引數傳遞 nil並自行控制 completion 區塊。</span><span class="sxs-lookup"><span data-stu-id="cb41a-144">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="cb41a-145">請參閱 `UIBackgroundFetchResult` 類型，查看可能值清單。</span><span class="sxs-lookup"><span data-stu-id="cb41a-145">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="cb41a-146">完整範例</span><span class="sxs-lookup"><span data-stu-id="cb41a-146">Full example</span></span>
<span data-ttu-id="cb41a-147">以下是整合的完整範例：</span><span class="sxs-lookup"><span data-stu-id="cb41a-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="cb41a-148">解決 UNUserNotificationCenter 委派衝突</span><span class="sxs-lookup"><span data-stu-id="cb41a-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="cb41a-149">如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。</span><span class="sxs-lookup"><span data-stu-id="cb41a-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="cb41a-150">SDK 會用 `UNUserNotificationCenter` 委派來監視在 iOS 10 或更新版本上執行的裝置中的 Engagement 通知生命週期。</span><span class="sxs-lookup"><span data-stu-id="cb41a-150">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="cb41a-151">SDK 會實作自己的 `UNUserNotificationCenterDelegate` 通訊協定，但每個應用程式只能有一個 `UNUserNotificationCenter` 委派。</span><span class="sxs-lookup"><span data-stu-id="cb41a-151">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="cb41a-152">新增至 `UNUserNotificationCenter` 物件的任何其他委派會與 Engagement one 發生衝突。</span><span class="sxs-lookup"><span data-stu-id="cb41a-152">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="cb41a-153">如果 SDK 偵測到您的委派或任何其他協力廠商的委派，則不會使用它自己的實作來讓您有機會解決衝突。</span><span class="sxs-lookup"><span data-stu-id="cb41a-153">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="cb41a-154">您必須將 Engagement 邏輯新增至您自己的委派，以便解決衝突。</span><span class="sxs-lookup"><span data-stu-id="cb41a-154">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="cb41a-155">有兩種方式可以達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="cb41a-155">There are two ways to achieve this.</span></span>

<span data-ttu-id="cb41a-156">提案 1，直接將委派呼叫轉送給 SDK：</span><span class="sxs-lookup"><span data-stu-id="cb41a-156">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="cb41a-157">或提案 2，繼承自 `AEUserNotificationHandler` 類別</span><span class="sxs-lookup"><span data-stu-id="cb41a-157">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="cb41a-158">您可以藉由將通知的 `userInfo` 字典傳遞給代理程式的 `isEngagementPushPayload:` 類別方法，來決定通知是否來自 Engagement。</span><span class="sxs-lookup"><span data-stu-id="cb41a-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="cb41a-159">請確定 `UNUserNotificationCenter` 物件的委派已設為您在 `application:willFinishLaunchingWithOptions:` 內的委派或應用程式委派的 `application:didFinishLaunchingWithOptions:` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb41a-159">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="cb41a-160">例如，如果您實作了上述提案 1：</span><span class="sxs-lookup"><span data-stu-id="cb41a-160">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="cb41a-161">如何自訂活動</span><span class="sxs-lookup"><span data-stu-id="cb41a-161">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="cb41a-162">通知</span><span class="sxs-lookup"><span data-stu-id="cb41a-162">Notifications</span></span>
<span data-ttu-id="cb41a-163">有兩種通知類型： 系統通知和應用程式內通知。</span><span class="sxs-lookup"><span data-stu-id="cb41a-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="cb41a-164">系統通知都是由 iOS 處理，且無法自訂。</span><span class="sxs-lookup"><span data-stu-id="cb41a-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="cb41a-165">應用程式內通知，是由以動態方式加入到目前應用程式視窗中的檢視所組成。</span><span class="sxs-lookup"><span data-stu-id="cb41a-165">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="cb41a-166">這稱為通知重疊。</span><span class="sxs-lookup"><span data-stu-id="cb41a-166">This is called a notification overlay.</span></span> <span data-ttu-id="cb41a-167">通知重疊非常適合用於快速整合，因為它們不需要您修改應用程式中的任何檢視。</span><span class="sxs-lookup"><span data-stu-id="cb41a-167">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="cb41a-168">版面配置</span><span class="sxs-lookup"><span data-stu-id="cb41a-168">Layout</span></span>
<span data-ttu-id="cb41a-169">若要修改應用程式內通知的外觀，您可以依需求直接修改 `AENotificationView.xib` 檔案，只要保留標記值與現有子檢視的類型即可。</span><span class="sxs-lookup"><span data-stu-id="cb41a-169">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="cb41a-170">根據預設，應用程式內通知會出現在畫面底部。</span><span class="sxs-lookup"><span data-stu-id="cb41a-170">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="cb41a-171">如果您偏好將通知顯示在畫面頂端，請編輯所提供的 `AENotificationView.xib` 並變更主要檢視的 `AutoSizing` 屬性，讓通知可以保留在其 superview 的頂端。</span><span class="sxs-lookup"><span data-stu-id="cb41a-171">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="cb41a-172">類別</span><span class="sxs-lookup"><span data-stu-id="cb41a-172">Categories</span></span>
<span data-ttu-id="cb41a-173">當您修改提供的版面配置時，會修改您所有通知的外觀。</span><span class="sxs-lookup"><span data-stu-id="cb41a-173">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="cb41a-174">類別可讓您定義通知的各種目標外觀 (也可能是行為)。</span><span class="sxs-lookup"><span data-stu-id="cb41a-174">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="cb41a-175">當您建立觸達活動時可以指定類別。</span><span class="sxs-lookup"><span data-stu-id="cb41a-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="cb41a-176">請記住，類別也可讓您自訂宣告與輪詢，本文件稍後將會說明。</span><span class="sxs-lookup"><span data-stu-id="cb41a-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="cb41a-177">若要為您的通知註冊類別處理常式，必須在觸達模組完成初始化後加入呼叫。</span><span class="sxs-lookup"><span data-stu-id="cb41a-177">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="cb41a-178">`myNotifier` 必須是符合 `AENotifier` 通訊協定之物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cb41a-178">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="cb41a-179">您可以自己實作通訊協定方法，或選擇重新實作已經執行大部分工作的現有 `AEDefaultNotifier` 類別。</span><span class="sxs-lookup"><span data-stu-id="cb41a-179">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="cb41a-180">例如，如果您想要重新定義特定類別的通知檢視，可以遵循此範例：</span><span class="sxs-lookup"><span data-stu-id="cb41a-180">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="cb41a-181">這個簡單的類別範例假設您已在主要的應用程式套件組合中有一個名為 `MyNotificationView.xib` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb41a-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="cb41a-182">如果方法無法找到相對應的 `.xib`，將不會顯示通知且 Engagement 會在主控台中輸出一則訊息。</span><span class="sxs-lookup"><span data-stu-id="cb41a-182">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="cb41a-183">提供的 nib 檔案應該遵守以下規則：</span><span class="sxs-lookup"><span data-stu-id="cb41a-183">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="cb41a-184">它應該只包含一個檢視。</span><span class="sxs-lookup"><span data-stu-id="cb41a-184">It should only contain one view.</span></span>
* <span data-ttu-id="cb41a-185">子檢視的類型應該與提供的 nib 檔案 (名稱為 `AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="cb41a-185">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="cb41a-186">子檢視應該具有與提供的 nib 檔案 (名稱為 `AENotificationView.xib`) 內標記相同的標記</span><span class="sxs-lookup"><span data-stu-id="cb41a-186">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="cb41a-187">複製提供的 nib 檔案 (名稱為 `AENotificationView.xib`)，並從該處開始工作。</span><span class="sxs-lookup"><span data-stu-id="cb41a-187">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="cb41a-188">但請小心，此 nib 檔案內的檢視與 `AENotificationView`類別相關聯。</span><span class="sxs-lookup"><span data-stu-id="cb41a-188">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="cb41a-189">這個類別重新定義了 `layoutSubViews` 方法，藉此根據內容來移動並重新調整其子檢視的大小。</span><span class="sxs-lookup"><span data-stu-id="cb41a-189">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="cb41a-190">您可以用 `UIView` 取代它，或是自訂檢視類別。</span><span class="sxs-lookup"><span data-stu-id="cb41a-190">You may want to replace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="cb41a-191">如果您需要更深入地自訂通知 (如果要讓執行個體直接從程式碼載入檢視)，建議您查看所提供之 `Protocol ReferencesDefaultNotifier` 與 `AENotifier` 的原始程式碼與類別文件。</span><span class="sxs-lookup"><span data-stu-id="cb41a-191">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="cb41a-192">請注意，您可以針對多個類別使用相同的通知程式。</span><span class="sxs-lookup"><span data-stu-id="cb41a-192">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="cb41a-193">您也可以重新定義預設通知程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cb41a-193">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="cb41a-194">通知處理</span><span class="sxs-lookup"><span data-stu-id="cb41a-194">Notification handling</span></span>
<span data-ttu-id="cb41a-195">使用預設類別時，會在 `AEReachContent` 物件上呼叫部分生命週期方法，來報告統計資料並更新活動狀態：</span><span class="sxs-lookup"><span data-stu-id="cb41a-195">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="cb41a-196">在應用程式中顯示通知時，如果 `handleNotification:` 傳回 `YES`，則 `AEReachModule` 會呼叫 `displayNotification` 方法 (它會報告統計資料)。</span><span class="sxs-lookup"><span data-stu-id="cb41a-196">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="cb41a-197">如果關閉通知，則會呼叫 `exitNotification` 方法、報告統計資料，且可以立即處理下一個活動。</span><span class="sxs-lookup"><span data-stu-id="cb41a-197">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="cb41a-198">如果按一下通知，則會呼叫 `actionNotification` 、報告統計資料，並執行相關聯的動作。</span><span class="sxs-lookup"><span data-stu-id="cb41a-198">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="cb41a-199">如果 `AENotifier` 的實作略過預設行為，您必須自行呼叫這些生命週期方法。</span><span class="sxs-lookup"><span data-stu-id="cb41a-199">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="cb41a-200">以下範例說明一些會略過預設行為的情況：</span><span class="sxs-lookup"><span data-stu-id="cb41a-200">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="cb41a-201">您不延伸 `AEDefaultNotifier`，例如從頭開始實作類別處理。</span><span class="sxs-lookup"><span data-stu-id="cb41a-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="cb41a-202">您已覆寫 `prepareNotificationView:forContent:`，請務必至少將 `onNotificationActioned` 或 `onNotificationExited` 對應到其中一個 U.I 控制項。</span><span class="sxs-lookup"><span data-stu-id="cb41a-202">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="cb41a-203">如果 `handleNotification:` 擲回例外狀況，則會刪除內容且會呼叫 `drop`，這會在統計資料中報告，且可以立即處理下一個活動。</span><span class="sxs-lookup"><span data-stu-id="cb41a-203">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="cb41a-204">將通知併入現有的檢視</span><span class="sxs-lookup"><span data-stu-id="cb41a-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="cb41a-205">重疊最適合用於快速整合，但有些時候不太方便，或是造成不想要的副作用。</span><span class="sxs-lookup"><span data-stu-id="cb41a-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="cb41a-206">如果您不滿意您部分檢視中的重疊系統，可以對這些檢視加以自訂。</span><span class="sxs-lookup"><span data-stu-id="cb41a-206">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="cb41a-207">您可以決定在現有的檢視中包含我們的通知版面配置。</span><span class="sxs-lookup"><span data-stu-id="cb41a-207">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="cb41a-208">若要這樣做，有兩種實作樣式可用：</span><span class="sxs-lookup"><span data-stu-id="cb41a-208">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="cb41a-209">使用介面產生器加入通知檢視</span><span class="sxs-lookup"><span data-stu-id="cb41a-209">Add the notification view using interface builder</span></span>

   * <span data-ttu-id="cb41a-210">開啟 [介面產生器] </span><span class="sxs-lookup"><span data-stu-id="cb41a-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="cb41a-211">放置您想要在其中顯示通知的 `UIView` (大小為 320x60，如果在 iPad 上則為 768x60)</span><span class="sxs-lookup"><span data-stu-id="cb41a-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="cb41a-212">將此檢視的標記值設定為： **36822491**</span><span class="sxs-lookup"><span data-stu-id="cb41a-212">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="cb41a-213">以程式設計方式新增通知檢視。</span><span class="sxs-lookup"><span data-stu-id="cb41a-213">Add the notification view programmatically.</span></span> <span data-ttu-id="cb41a-214">在您已經將檢視初始化時加入以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="cb41a-214">Just add the following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="cb41a-215">您可以在 `AEDefaultNotifier.h` 中找到 `NOTIFICATION_AREA_VIEW_TAG` 巨集。</span><span class="sxs-lookup"><span data-stu-id="cb41a-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="cb41a-216">預設通知程式會自動偵測此檢視中是否已包含通知版面配置，而且不會為它新增重疊。</span><span class="sxs-lookup"><span data-stu-id="cb41a-216">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="cb41a-217">宣告和輪詢</span><span class="sxs-lookup"><span data-stu-id="cb41a-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="cb41a-218">版面配置</span><span class="sxs-lookup"><span data-stu-id="cb41a-218">Layouts</span></span>
<span data-ttu-id="cb41a-219">您可以修改 `AEDefaultAnnouncementView.xib` 與 `AEDefaultPollView.xib` 檔案，只要保留標記值與現有子檢視的類型即可。</span><span class="sxs-lookup"><span data-stu-id="cb41a-219">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="cb41a-220">類別</span><span class="sxs-lookup"><span data-stu-id="cb41a-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="cb41a-221">替代版面配置</span><span class="sxs-lookup"><span data-stu-id="cb41a-221">Alternate layouts</span></span>
<span data-ttu-id="cb41a-222">類似通知，活動類別可以用來做為宣告和輪詢的替代版片配置。</span><span class="sxs-lookup"><span data-stu-id="cb41a-222">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="cb41a-223">若要建立宣告的類別，您必須在初始化觸達模組後延伸 **AEAnnouncementViewController** 並將它註冊：</span><span class="sxs-lookup"><span data-stu-id="cb41a-223">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="cb41a-224">每次使用者按一下通知以取得 "my\_category" 類別的宣告時，會將您已經註冊的檢視控制器 (在此情況下為 `initWithAnnouncement:`) 透過呼叫 `MyCustomAnnouncementViewController` 方法來初始化，而且會將檢視新增到目前的應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="cb41a-224">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
>
>

<span data-ttu-id="cb41a-225">在 `AEAnnouncementViewController` 類別的實作中，您必須讀取 `announcement` 屬性來初始化您的子檢視。</span><span class="sxs-lookup"><span data-stu-id="cb41a-225">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="cb41a-226">請考量以下範例，其中的兩個標籤會使用屬於 `AEReachAnnouncement` 類別的 `title` 和 `body` 屬性來初始化：</span><span class="sxs-lookup"><span data-stu-id="cb41a-226">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="cb41a-227">如果您不想要自行載入您的檢視，但是想要重複使用預設的宣告檢視配置，可以讓自訂檢視控制器延伸提供的 `AEDefaultAnnouncementViewController`類別。</span><span class="sxs-lookup"><span data-stu-id="cb41a-227">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="cb41a-228">在此情況下，請複製 nib 檔案 `AEDefaultAnnouncementView.xib` 並將它重新命名，讓您的自訂檢視控制器可以載入它 (若是名稱為 `CustomAnnouncementViewController` 的控制器，您應該呼叫您的 nib 檔案 `CustomAnnouncementView.xib`) 。</span><span class="sxs-lookup"><span data-stu-id="cb41a-228">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="cb41a-229">若要取代預設的宣告類別，只要針對 `kAEReachDefaultCategory`中定義的類別註冊您的自訂檢視控制器即可：</span><span class="sxs-lookup"><span data-stu-id="cb41a-229">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="cb41a-230">可利用相同的方式自訂輪詢：</span><span class="sxs-lookup"><span data-stu-id="cb41a-230">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="cb41a-231">這一次，提供的 `MyCustomPollViewController` 必須延伸 `AEPollViewController`。</span><span class="sxs-lookup"><span data-stu-id="cb41a-231">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="cb41a-232">或者您可以選擇從預設控制器 `AEDefaultPollViewController`延伸。</span><span class="sxs-lookup"><span data-stu-id="cb41a-232">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb41a-233">請記得在關閉檢視控制器之前呼叫 `action` (若是自訂輪詢檢視控制器，則為 `submitAnswers:`)，或是呼叫 `exit` 方法。</span><span class="sxs-lookup"><span data-stu-id="cb41a-233">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="cb41a-234">否則，將不會傳送統計資料 (亦即無法分析活動)，更重要的是將不會通知下一個活動，直到應用程式處理程序重新啟動為止。</span><span class="sxs-lookup"><span data-stu-id="cb41a-234">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="cb41a-235">實作範例</span><span class="sxs-lookup"><span data-stu-id="cb41a-235">Implementation example</span></span>
<span data-ttu-id="cb41a-236">在此實作中，是從外部 xib 檔案載入自訂宣告檢視。</span><span class="sxs-lookup"><span data-stu-id="cb41a-236">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="cb41a-237">就像進階通知的自訂一樣，也建議您查看標準實作的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="cb41a-237">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

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
