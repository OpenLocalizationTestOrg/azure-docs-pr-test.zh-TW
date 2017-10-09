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
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="67e96-103">Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="67e96-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="67e96-104">從這裡開始 tooget hello 的所有詳細資料如何 toointegrate Azure Mobile Engagement 中 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67e96-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="67e96-105">如果您想要 toogive 它再試一次第一次，請確定您我們[15 分鐘教學課程](mobile-engagement-ios-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="67e96-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="67e96-106">按一下 toosee hello [SDK 內容](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="67e96-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="67e96-107">整合程序</span><span class="sxs-lookup"><span data-stu-id="67e96-107">Integration procedures</span></span>
1. <span data-ttu-id="67e96-108">從這裡開始：[如何 toointegrate Mobile Engagement 中 iOS 應用程式](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="67e96-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="67e96-109">通知：[如何在您的 iOS 應用程式中的 toointegrate 觸達 （通知）](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="67e96-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="67e96-110">標記計劃實作： [toouse hello 進階 Mobile Engagement 應用程式開發介面中 iOS 應用程式所標記的方式](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="67e96-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="67e96-111">版本資訊</span><span class="sxs-lookup"><span data-stu-id="67e96-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="67e96-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="67e96-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="67e96-113">修正在背景清除徽章。</span><span class="sxs-lookup"><span data-stu-id="67e96-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="67e96-114">修正在 XCode 9 上關於 API 未在主要佇列呼叫的警告。</span><span class="sxs-lookup"><span data-stu-id="67e96-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="67e96-115">修正觸達輪詢中的記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="67e96-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="67e96-116">停止支援 iOS 6.X。</span><span class="sxs-lookup"><span data-stu-id="67e96-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="67e96-117">從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 7。</span><span class="sxs-lookup"><span data-stu-id="67e96-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="67e96-118">針對較早版本，請參閱 hello[完成版本資訊](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="67e96-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="67e96-119">升級程序</span><span class="sxs-lookup"><span data-stu-id="67e96-119">Upgrade procedures</span></span>
<span data-ttu-id="67e96-120">如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="67e96-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="67e96-121">如果可能會發生 toofollow 數個程序錯過數個版本的 SDK 請的 hello hello 完成[升級程序](mobile-engagement-ios-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="67e96-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="67e96-122">為每個新的 hello SDK 版本，您必須先取代 （移除並重新匯入在 xcode 中） hello EngagementSDK 和 EngagementReach 資料夾。</span><span class="sxs-lookup"><span data-stu-id="67e96-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="67e96-123">從 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="67e96-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="67e96-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="67e96-124">XCode 8</span></span>
<span data-ttu-id="67e96-125">XCode 8 開始就必須從 hello SDK 4.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="67e96-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="67e96-126">如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="67e96-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="67e96-127">沒有已知的錯誤之前的版本中的 hello 觸達模組 10 的 iOS 裝置上執行時： 系統通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="67e96-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="67e96-128">toofix 就 tooimplement hello 這個已被取代 API`application:didReceiveRemoteNotification:`在您的應用程式委派，如下所示：</span><span class="sxs-lookup"><span data-stu-id="67e96-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="67e96-129">**我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。</span><span class="sxs-lookup"><span data-stu-id="67e96-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="67e96-130">您應儘速切換 tooXCode 8。</span><span class="sxs-lookup"><span data-stu-id="67e96-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="67e96-131">UserNotifications 架構</span><span class="sxs-lookup"><span data-stu-id="67e96-131">UserNotifications framework</span></span>
<span data-ttu-id="67e96-132">您需要 tooadd hello`UserNotifications`您建置階段中的架構。</span><span class="sxs-lookup"><span data-stu-id="67e96-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="67e96-133">hello 專案總管 中開啟您專案窗格並選取 hello 正確的目標。</span><span class="sxs-lookup"><span data-stu-id="67e96-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="67e96-134">然後，開啟 hello **建置階段** 索引標籤在 hello **< 連結二進位與媒體櫃**功能表上，加入架構`UserNotifications.framework`-設定 hello 連結做為`Optional`</span><span class="sxs-lookup"><span data-stu-id="67e96-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="67e96-135">應用程式推播功能</span><span class="sxs-lookup"><span data-stu-id="67e96-135">Application push capability</span></span>
<span data-ttu-id="67e96-136">XCode 8 可能會重設您的應用程式發送功能，請再檢查一次在 hello`capability`您選取的目標 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="67e96-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="67e96-137">加入 hello 新 iOS 10 通知註冊程式碼</span><span class="sxs-lookup"><span data-stu-id="67e96-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="67e96-138">hello 較舊的程式碼片段 tooregister hello 應用程式 toonotifications 仍然運作，但使用的 iOS 10 上執行時，被取代 Api。</span><span class="sxs-lookup"><span data-stu-id="67e96-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="67e96-139">匯入 hello`User Notification`架構：</span><span class="sxs-lookup"><span data-stu-id="67e96-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="67e96-140">在您的應用程式中委派 `application:didFinishLaunchingWithOptions` 方法取代︰</span><span class="sxs-lookup"><span data-stu-id="67e96-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="67e96-141">依︰</span><span class="sxs-lookup"><span data-stu-id="67e96-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="67e96-142">解決 UNUserNotificationCenter 委派衝突</span><span class="sxs-lookup"><span data-stu-id="67e96-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="67e96-143">如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。</span><span class="sxs-lookup"><span data-stu-id="67e96-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="67e96-144">A`UNUserNotificationCenter`委派由 hello SDK toomonitor hello 生命週期的 Engagement 大於或等於 10 在 iOS 上執行的裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="67e96-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="67e96-145">hello SDK 有它自己實作 hello`UNUserNotificationCenterDelegate`通訊協定，但可以是只有一個`UNUserNotificationCenter`委派每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="67e96-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="67e96-146">任何其他的委派加入 toohello`UNUserNotificationCenter`物件會與 hello Engagement 其中一個衝突。</span><span class="sxs-lookup"><span data-stu-id="67e96-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="67e96-147">如果 hello SDK 偵測到您或任何其他協力廠商的委派，則不會使用它自己的實作 toogive 您機會 tooresolve hello 衝突。</span><span class="sxs-lookup"><span data-stu-id="67e96-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="67e96-148">您必須擁有在順序中的委派 tooresolve hello 衝突 tooadd hello Engagement 邏輯 tooyour。</span><span class="sxs-lookup"><span data-stu-id="67e96-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="67e96-149">有兩種方式 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="67e96-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="67e96-150">提案 1，只要轉送您的委派呼叫 toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="67e96-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="67e96-151">或透過繼承自 hello 提案 2，`AEUserNotificationHandler`類別</span><span class="sxs-lookup"><span data-stu-id="67e96-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="67e96-152">您可以判斷通知來自 Engagement 或不是藉由傳遞其`userInfo`字典 toohello 代理程式`isEngagementPushPayload:`類別方法。</span><span class="sxs-lookup"><span data-stu-id="67e96-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="67e96-153">請確定該 hello`UNUserNotificationCenter`物件的委派設定中任一 hello tooyour 委派`application:willFinishLaunchingWithOptions:`或 hello`application:didFinishLaunchingWithOptions:`應用程式委派的方法。</span><span class="sxs-lookup"><span data-stu-id="67e96-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="67e96-154">比方說，如果您已實作提案 1 以上的 hello:</span><span class="sxs-lookup"><span data-stu-id="67e96-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
