---
title: "Azure Mobile Engagement iOS SDK 升級程序 | Microsoft Docs"
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="c2908-103">升級程序</span><span class="sxs-lookup"><span data-stu-id="c2908-103">Upgrade procedures</span></span>
<span data-ttu-id="c2908-104">如果您已經整合舊版 Engagement 到您的應用程式，在升級 SDK 時您必須考慮以下幾點。</span><span class="sxs-lookup"><span data-stu-id="c2908-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="c2908-105">針對每個新版 SDK，您必須先取代 (在 xcode 中移除並重新匯入) EngagementSDK 與 EngagementReach 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c2908-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="c2908-106">從 3.0.0 到 4.0.0</span><span class="sxs-lookup"><span data-stu-id="c2908-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="c2908-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="c2908-107">XCode 8</span></span>
<span data-ttu-id="c2908-108">從 SDK 4.0.0 版開始就必須要有 XCode 8。</span><span class="sxs-lookup"><span data-stu-id="c2908-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="c2908-109">如果您實際上是仰賴 XCode 7，則可以使用 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="c2908-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="c2908-110">這個舊版本的觸達模組在 iOS 10 裝置上執行時有已知錯誤︰系統通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="c2908-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="c2908-111">若要修正此錯誤，您必須在應用程式委派中實作已被取代的 API `application:didReceiveRemoteNotification:` ，方式如下︰</span><span class="sxs-lookup"><span data-stu-id="c2908-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="c2908-112">**我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。</span><span class="sxs-lookup"><span data-stu-id="c2908-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="c2908-113">您應盡快改用 XCode 8。</span><span class="sxs-lookup"><span data-stu-id="c2908-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="c2908-114">UserNotifications 架構</span><span class="sxs-lookup"><span data-stu-id="c2908-114">UserNotifications framework</span></span>
<span data-ttu-id="c2908-115">您需要在建置階段新增 `UserNotifications` 架構。</span><span class="sxs-lookup"><span data-stu-id="c2908-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="c2908-116">在專案總管中，開啟專案窗格並選取正確的目標。</span><span class="sxs-lookup"><span data-stu-id="c2908-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="c2908-117">然後，開啟 [建置階段] 索引標籤，並在 [連結二進位檔與程式庫] 功能表中新增架構 `UserNotifications.framework``Optional`</span><span class="sxs-lookup"><span data-stu-id="c2908-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="c2908-118">應用程式推播功能</span><span class="sxs-lookup"><span data-stu-id="c2908-118">Application push capability</span></span>
<span data-ttu-id="c2908-119">XCode 8 可能會重設您的應用程式推播功能，請在您選取的目標的 `capability` 索引標籤中再檢查一次。</span><span class="sxs-lookup"><span data-stu-id="c2908-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="c2908-120">新增 iOS 10 通知註冊程式碼</span><span class="sxs-lookup"><span data-stu-id="c2908-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="c2908-121">要將應用程式註冊通知的較舊程式碼片段仍會運作，但在 iOS 10 上執行時會使用已被取代的 API。</span><span class="sxs-lookup"><span data-stu-id="c2908-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="c2908-122">匯入 `User Notification` 架構：</span><span class="sxs-lookup"><span data-stu-id="c2908-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="c2908-123">在您的應用程式中委派 `application:didFinishLaunchingWithOptions` 方法取代︰</span><span class="sxs-lookup"><span data-stu-id="c2908-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="c2908-124">依︰</span><span class="sxs-lookup"><span data-stu-id="c2908-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="c2908-125">解決 UNUserNotificationCenter 委派衝突</span><span class="sxs-lookup"><span data-stu-id="c2908-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="c2908-126">如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。</span><span class="sxs-lookup"><span data-stu-id="c2908-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="c2908-127">SDK 會用 `UNUserNotificationCenter` 委派來監視在 iOS 10 或更新版本上執行的裝置中的 Engagement 通知生命週期。</span><span class="sxs-lookup"><span data-stu-id="c2908-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="c2908-128">SDK 會實作自己的 `UNUserNotificationCenterDelegate` 通訊協定，但每個應用程式只能有一個 `UNUserNotificationCenter` 委派。</span><span class="sxs-lookup"><span data-stu-id="c2908-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="c2908-129">新增至 `UNUserNotificationCenter` 物件的任何其他委派會與 Engagement one 發生衝突。</span><span class="sxs-lookup"><span data-stu-id="c2908-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="c2908-130">如果 SDK 偵測到您的委派或任何其他協力廠商的委派，則不會使用它自己的實作來讓您有機會解決衝突。</span><span class="sxs-lookup"><span data-stu-id="c2908-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="c2908-131">您必須將 Engagement 邏輯新增至您自己的委派，以便解決衝突。</span><span class="sxs-lookup"><span data-stu-id="c2908-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="c2908-132">有兩種方式可以達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="c2908-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="c2908-133">提案 1，直接將委派呼叫轉送給 SDK：</span><span class="sxs-lookup"><span data-stu-id="c2908-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="c2908-134">或提案 2，繼承自 `AEUserNotificationHandler` 類別</span><span class="sxs-lookup"><span data-stu-id="c2908-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="c2908-135">您可以藉由將通知的 `userInfo` 字典傳遞給代理程式的 `isEngagementPushPayload:` 類別方法，來決定通知是否來自 Engagement。</span><span class="sxs-lookup"><span data-stu-id="c2908-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="c2908-136">請確定 `UNUserNotificationCenter` 物件的委派已設為您在 `application:willFinishLaunchingWithOptions:` 內的委派或應用程式委派的 `application:didFinishLaunchingWithOptions:` 方法。</span><span class="sxs-lookup"><span data-stu-id="c2908-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="c2908-137">例如，如果您實作了上述提案 1：</span><span class="sxs-lookup"><span data-stu-id="c2908-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="c2908-138">從 2.0.0 到 3.0.0</span><span class="sxs-lookup"><span data-stu-id="c2908-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="c2908-139">停止支援 iOS 4.X。</span><span class="sxs-lookup"><span data-stu-id="c2908-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="c2908-140">從此版本開始，您的應用程式部署目標必須至少為 iOS 6。</span><span class="sxs-lookup"><span data-stu-id="c2908-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="c2908-141">如果您在應用程式中使用 Reach，必須將`remote-notification` 值新增至 Info.plist 檔案中的 `UIBackgroundModes` 陣列，以接收遠端通知。</span><span class="sxs-lookup"><span data-stu-id="c2908-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="c2908-142">在您的應用程式委派中，方法 `application:didReceiveRemoteNotification:` 需由 `application:didReceiveRemoteNotification:fetchCompletionHandler:` 取代。</span><span class="sxs-lookup"><span data-stu-id="c2908-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="c2908-143">"AEPushDelegate.h" 是已被取代的介面，且您必須移除所有參考。</span><span class="sxs-lookup"><span data-stu-id="c2908-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="c2908-144">這包括從您的應用程式委派移除 `[[EngagementAgent shared] setPushDelegate:self]` 以及委派方法：</span><span class="sxs-lookup"><span data-stu-id="c2908-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="c2908-145">從 1.16.0 到 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c2908-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="c2908-146">以下說明如何將 SDK 整合從 Capptain SAS 提供的 Capptain 服務，移轉到由 Azure Mobile Engagement 提供的應用程式內。</span><span class="sxs-lookup"><span data-stu-id="c2908-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="c2908-147">如果您是從較早版本移轉，請參閱 Capptain 網站，先移轉到 1.16 後再套用以下程序。</span><span class="sxs-lookup"><span data-stu-id="c2908-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2908-148">Capptain 和 Mobile Engagement 是不同的服務，而以下程序只適用於移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2908-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="c2908-149">移轉應用程式中的 SDK「不會」將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="c2908-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="c2908-150">代理程式</span><span class="sxs-lookup"><span data-stu-id="c2908-150">Agent</span></span>
<span data-ttu-id="c2908-151">`registerApp:` 方法已被新方法 `init:` 取代。</span><span class="sxs-lookup"><span data-stu-id="c2908-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="c2908-152">您的應用程式委派必須隨之更新，並使用連接字串：</span><span class="sxs-lookup"><span data-stu-id="c2908-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="c2908-153">SmartAd 追蹤已從 SDK 移除，因此您必須移除 `AETrackModule` 類別的所有執行個體</span><span class="sxs-lookup"><span data-stu-id="c2908-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="c2908-154">類別名稱變更</span><span class="sxs-lookup"><span data-stu-id="c2908-154">Class Name Changes</span></span>
<span data-ttu-id="c2908-155">執行品牌再造時，有幾個類別/檔案名稱需要變更。</span><span class="sxs-lookup"><span data-stu-id="c2908-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="c2908-156">所有首碼為 "CP" 的類別，都使用 "AE" 首碼重新命名。</span><span class="sxs-lookup"><span data-stu-id="c2908-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="c2908-157">範例：</span><span class="sxs-lookup"><span data-stu-id="c2908-157">Example:</span></span>

* <span data-ttu-id="c2908-158">`CPModule.h` 已重新命名為 `AEModule.h`。</span><span class="sxs-lookup"><span data-stu-id="c2908-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="c2908-159">所有首碼為 "Capptain" 的類別，都已使用 "Engagement" 首碼重新命名。</span><span class="sxs-lookup"><span data-stu-id="c2908-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="c2908-160">範例：</span><span class="sxs-lookup"><span data-stu-id="c2908-160">Examples:</span></span>

* <span data-ttu-id="c2908-161">`CapptainAgent` 類別已重新命名為 `EngagementAgent`。</span><span class="sxs-lookup"><span data-stu-id="c2908-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="c2908-162">`CapptainTableViewController` 類別已重新命名為 `EngagementTableViewController`。</span><span class="sxs-lookup"><span data-stu-id="c2908-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="c2908-163">`CapptainUtils` 類別已重新命名為 `EngagementUtils`。</span><span class="sxs-lookup"><span data-stu-id="c2908-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="c2908-164">`CapptainViewController` 類別已重新命名為 `EngagementViewController`。</span><span class="sxs-lookup"><span data-stu-id="c2908-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

