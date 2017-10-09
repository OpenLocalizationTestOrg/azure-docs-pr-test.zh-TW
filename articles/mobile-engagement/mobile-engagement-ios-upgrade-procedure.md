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
# <a name="upgrade-procedures"></a><span data-ttu-id="95a4b-103">升級程序</span><span class="sxs-lookup"><span data-stu-id="95a4b-103">Upgrade procedures</span></span>
<span data-ttu-id="95a4b-104">如果您已經有整合至您的應用程式較舊版本的參與，則必須升級 hello SDK 時，下列點 tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="95a4b-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="95a4b-105">為每個新的 hello SDK 版本，您必須先取代 （移除並重新匯入在 xcode 中） hello EngagementSDK 和 EngagementReach 資料夾。</span><span class="sxs-lookup"><span data-stu-id="95a4b-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="95a4b-106">從 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="95a4b-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="95a4b-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="95a4b-107">XCode 8</span></span>
<span data-ttu-id="95a4b-108">XCode 8 開始就必須從 hello SDK 4.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="95a4b-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="95a4b-109">如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="95a4b-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="95a4b-110">沒有已知的錯誤之前的版本中的 hello 觸達模組 10 的 iOS 裝置上執行時： 系統通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="95a4b-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="95a4b-111">toofix 就 tooimplement hello 這個已被取代 API`application:didReceiveRemoteNotification:`在您的應用程式委派，如下所示：</span><span class="sxs-lookup"><span data-stu-id="95a4b-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="95a4b-112">**我們不建議此因應措施** ，因為此 iOS API 已被取代，此行為在任何即將推出的 (甚至次要的) iOS 版本升級中會有所變更。</span><span class="sxs-lookup"><span data-stu-id="95a4b-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="95a4b-113">您應儘速切換 tooXCode 8。</span><span class="sxs-lookup"><span data-stu-id="95a4b-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="95a4b-114">UserNotifications 架構</span><span class="sxs-lookup"><span data-stu-id="95a4b-114">UserNotifications framework</span></span>
<span data-ttu-id="95a4b-115">您需要 tooadd hello`UserNotifications`您建置階段中的架構。</span><span class="sxs-lookup"><span data-stu-id="95a4b-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="95a4b-116">hello 專案總管 中開啟您專案窗格並選取 hello 正確的目標。</span><span class="sxs-lookup"><span data-stu-id="95a4b-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="95a4b-117">然後，開啟 hello **建置階段** 索引標籤在 hello **< 連結二進位與媒體櫃**功能表上，加入架構`UserNotifications.framework`-設定 hello 連結做為`Optional`</span><span class="sxs-lookup"><span data-stu-id="95a4b-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="95a4b-118">應用程式推播功能</span><span class="sxs-lookup"><span data-stu-id="95a4b-118">Application push capability</span></span>
<span data-ttu-id="95a4b-119">XCode 8 可能會重設您的應用程式發送功能，請再檢查一次在 hello`capability`您選取的目標 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="95a4b-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="95a4b-120">加入 hello 新 iOS 10 通知註冊程式碼</span><span class="sxs-lookup"><span data-stu-id="95a4b-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="95a4b-121">hello 較舊的程式碼片段 tooregister hello 應用程式 toonotifications 仍然運作，但使用的 iOS 10 上執行時，被取代 Api。</span><span class="sxs-lookup"><span data-stu-id="95a4b-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="95a4b-122">匯入 hello`User Notification`架構：</span><span class="sxs-lookup"><span data-stu-id="95a4b-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="95a4b-123">在您的應用程式中委派 `application:didFinishLaunchingWithOptions` 方法取代︰</span><span class="sxs-lookup"><span data-stu-id="95a4b-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="95a4b-124">依︰</span><span class="sxs-lookup"><span data-stu-id="95a4b-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="95a4b-125">解決 UNUserNotificationCenter 委派衝突</span><span class="sxs-lookup"><span data-stu-id="95a4b-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="95a4b-126">如果您的應用程式或其中一個協力廠商程式庫都未實作 `UNUserNotificationCenterDelegate`，則可以略過這個部分。</span><span class="sxs-lookup"><span data-stu-id="95a4b-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="95a4b-127">A`UNUserNotificationCenter`委派由 hello SDK toomonitor hello 生命週期的 Engagement 大於或等於 10 在 iOS 上執行的裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="95a4b-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="95a4b-128">hello SDK 有它自己實作 hello`UNUserNotificationCenterDelegate`通訊協定，但可以是只有一個`UNUserNotificationCenter`委派每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="95a4b-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="95a4b-129">任何其他的委派加入 toohello`UNUserNotificationCenter`物件會與 hello Engagement 其中一個衝突。</span><span class="sxs-lookup"><span data-stu-id="95a4b-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="95a4b-130">如果 hello SDK 偵測到您或任何其他協力廠商的委派，則不會使用它自己的實作 toogive 您機會 tooresolve hello 衝突。</span><span class="sxs-lookup"><span data-stu-id="95a4b-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="95a4b-131">您必須擁有在順序中的委派 tooresolve hello 衝突 tooadd hello Engagement 邏輯 tooyour。</span><span class="sxs-lookup"><span data-stu-id="95a4b-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="95a4b-132">有兩種方式 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="95a4b-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="95a4b-133">提案 1，只要轉送您的委派呼叫 toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="95a4b-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="95a4b-134">或透過繼承自 hello 提案 2，`AEUserNotificationHandler`類別</span><span class="sxs-lookup"><span data-stu-id="95a4b-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="95a4b-135">您可以判斷通知來自 Engagement 或不是藉由傳遞其`userInfo`字典 toohello 代理程式`isEngagementPushPayload:`類別方法。</span><span class="sxs-lookup"><span data-stu-id="95a4b-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="95a4b-136">請確定該 hello`UNUserNotificationCenter`物件的委派設定中任一 hello tooyour 委派`application:willFinishLaunchingWithOptions:`或 hello`application:didFinishLaunchingWithOptions:`應用程式委派的方法。</span><span class="sxs-lookup"><span data-stu-id="95a4b-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="95a4b-137">比方說，如果您已實作提案 1 以上的 hello:</span><span class="sxs-lookup"><span data-stu-id="95a4b-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="95a4b-138">從 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="95a4b-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="95a4b-139">停止支援 iOS 4.X。</span><span class="sxs-lookup"><span data-stu-id="95a4b-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="95a4b-140">從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 6。</span><span class="sxs-lookup"><span data-stu-id="95a4b-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="95a4b-141">如果您使用觸達應用程式中，您必須新增`remote-notification`值 toohello`UIBackgroundModes`順序 tooreceive 遠端通知 Info.plist 檔案中的陣列。</span><span class="sxs-lookup"><span data-stu-id="95a4b-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="95a4b-142">hello 方法`application:didReceiveRemoteNotification:`需要取代 toobe`application:didReceiveRemoteNotification:fetchCompletionHandler:`在應用程式委派。</span><span class="sxs-lookup"><span data-stu-id="95a4b-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="95a4b-143">已被取代"AEPushDelegate.h 」 介面，且需要 tooremove 所有參考。</span><span class="sxs-lookup"><span data-stu-id="95a4b-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="95a4b-144">這包括移除`[[EngagementAgent shared] setPushDelegate:self]`和 hello 委派方法，從您的應用程式委派：</span><span class="sxs-lookup"><span data-stu-id="95a4b-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="95a4b-145">從 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="95a4b-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="95a4b-146">hello 下列程式碼說明如何 toomigrate hello Capptain 服務從 SDK 整合提供 Capptain SAS 到由 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95a4b-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="95a4b-147">如果您從舊版移轉，請先參閱 hello Capptain 網站 toomigrate too1.16，然後套用 hello 遵循程序。</span><span class="sxs-lookup"><span data-stu-id="95a4b-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a4b-148">Capptain 和 Mobile Engagement 不是 hello 相同的服務和 hello 下列程序只會反白顯示 toomigrate hello 用戶端應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="95a4b-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="95a4b-149">移轉 hello SDK hello 應用程式中的不會移轉您的資料從 hello Capptain 伺服器 toohello Mobile Engagement 伺服器</span><span class="sxs-lookup"><span data-stu-id="95a4b-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="95a4b-150">代理程式</span><span class="sxs-lookup"><span data-stu-id="95a4b-150">Agent</span></span>
<span data-ttu-id="95a4b-151">hello 方法`registerApp:`已由 hello 新方法取代`init:`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="95a4b-152">您的應用程式委派必須隨之更新，並使用連接字串：</span><span class="sxs-lookup"><span data-stu-id="95a4b-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="95a4b-153">您只需要 tooremove 的所有執行個體的 SDK 中已移除 SmartAd 追蹤`AETrackModule`類別</span><span class="sxs-lookup"><span data-stu-id="95a4b-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="95a4b-154">類別名稱變更</span><span class="sxs-lookup"><span data-stu-id="95a4b-154">Class Name Changes</span></span>
<span data-ttu-id="95a4b-155">Hello rebranding 的一部分，有幾個需要 toobe 變更的類別/檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="95a4b-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="95a4b-156">所有首碼為 "CP" 的類別，都使用 "AE" 首碼重新命名。</span><span class="sxs-lookup"><span data-stu-id="95a4b-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="95a4b-157">範例：</span><span class="sxs-lookup"><span data-stu-id="95a4b-157">Example:</span></span>

* <span data-ttu-id="95a4b-158">`CPModule.h`重新命名過`AEModule.h`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="95a4b-159">所有首碼為 "Capptain" 的類別，都已使用 "Engagement" 首碼重新命名。</span><span class="sxs-lookup"><span data-stu-id="95a4b-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="95a4b-160">範例：</span><span class="sxs-lookup"><span data-stu-id="95a4b-160">Examples:</span></span>

* <span data-ttu-id="95a4b-161">hello 類別`CapptainAgent`重新命名過`EngagementAgent`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="95a4b-162">hello 類別`CapptainTableViewController`重新命名過`EngagementTableViewController`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="95a4b-163">hello 類別`CapptainUtils`重新命名過`EngagementUtils`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="95a4b-164">hello 類別`CapptainViewController`重新命名過`EngagementViewController`。</span><span class="sxs-lookup"><span data-stu-id="95a4b-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

