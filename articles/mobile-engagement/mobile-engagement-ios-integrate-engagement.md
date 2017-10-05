---
title: "Azure Mobile Engagement iOS SDK 整合 | Microsoft Docs"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="f3f57-103">如何在 iOS 上整合 Engagement</span><span class="sxs-lookup"><span data-stu-id="f3f57-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3f57-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f3f57-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="f3f57-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="f3f57-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="f3f57-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f3f57-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="f3f57-107">Android</span><span class="sxs-lookup"><span data-stu-id="f3f57-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="f3f57-108">此程序描述在您的 iOS 應用程式中，啟動 Engagement 的分析和監視功能時，最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="f3f57-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="f3f57-109">Engagement SDK 需要 iOS 7 以上和 Xcode 8 以上版本：應用程式的部署目標必須至少為 iOS 7。</span><span class="sxs-lookup"><span data-stu-id="f3f57-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="f3f57-110">如果您實際上是仰賴 XCode 7，則可以使用 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="f3f57-111">這個舊版本的觸達模組在 iOS 10 裝置上執行時有已知錯誤，請參閱 [觸達模組整合](mobile-engagement-ios-integrate-engagement-reach.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f3f57-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="f3f57-112">如果您選擇使用 SDK v3.2.4，請直接跳過下一個步驟中的 `UserNotifications.framework` 匯入。</span><span class="sxs-lookup"><span data-stu-id="f3f57-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="f3f57-113">下列步驟便足以啟用計算使用者、工作階段、活動、當機和技術等所有統計資料時需要的記錄檔報告。</span><span class="sxs-lookup"><span data-stu-id="f3f57-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="f3f57-114">用來計算事件、錯誤及工作等其他統計資料所需的記錄檔報告必須使用 Engagement API 手動完成 (請參閱[如何在 iOS 應用程式中使用進階的 Mobile Engagement 標記 API](mobile-engagement-ios-use-engagement-api.md))，因為這些是與應用程式相依的統計資料。</span><span class="sxs-lookup"><span data-stu-id="f3f57-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="f3f57-115">將 Engagement SDK 嵌入您的 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="f3f57-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="f3f57-116">從 [這裡](http://aka.ms/qk2rnj)下載 iOS SDK。</span><span class="sxs-lookup"><span data-stu-id="f3f57-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="f3f57-117">將 Engagement SDK 加入您的 iOS 專案：在 Xcode 中，以滑鼠右鍵按一下專案，然後選取 [新增檔案至]，再選擇 `EngagementSDK` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3f57-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="f3f57-118">Engagement 需要額外的架構才能運作：在專案總管中，開啟專案窗格並選取正確的目標。</span><span class="sxs-lookup"><span data-stu-id="f3f57-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="f3f57-119">然後，開啟 [建置階段] 索引標籤，在 [連結二進位檔與程式庫] 功能表中加入下列架構：</span><span class="sxs-lookup"><span data-stu-id="f3f57-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="f3f57-120">`UserNotifications.framework`：將連結設為`Optional`</span><span class="sxs-lookup"><span data-stu-id="f3f57-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="f3f57-121">`AdSupport.framework`：將連結設為`Optional`</span><span class="sxs-lookup"><span data-stu-id="f3f57-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="f3f57-122">AdSupport 架構可以移除。</span><span class="sxs-lookup"><span data-stu-id="f3f57-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="f3f57-123">Engagement 需要此架構來收集 IDFA。</span><span class="sxs-lookup"><span data-stu-id="f3f57-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="f3f57-124">但您可以停用 IDFA 集合 \<ios-sdk-engagement-idfa\>，以符合關於此識別碼的新 Apple 原則。</span><span class="sxs-lookup"><span data-stu-id="f3f57-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="f3f57-125">初始化 Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="f3f57-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="f3f57-126">您需要修改應用程式委派：</span><span class="sxs-lookup"><span data-stu-id="f3f57-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="f3f57-127">在實作檔案頂端匯入 Engagement 代理程式：</span><span class="sxs-lookup"><span data-stu-id="f3f57-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="f3f57-128">在 '**applicationDidFinishLaunching:**' 或 '**application:didFinishLaunchingWithOptions:**' 方法內初始化 Engagement：</span><span class="sxs-lookup"><span data-stu-id="f3f57-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="f3f57-129">基本報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="f3f57-130">建議使用的方法：多載您的 `UIViewController` 類別</span><span class="sxs-lookup"><span data-stu-id="f3f57-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="f3f57-131">若要啟動 Engagement 需要的所有記錄檔報告，來計算使用者、工作階段、活動、當機和技術統計資料，您只需要讓所有 `UIViewController` 子類別繼承自 `EngagementViewController` 類別 (`UITableViewController` -\>`EngagementTableViewController` 也是相同的規則)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="f3f57-132">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3f57-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="f3f57-133">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="f3f57-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="f3f57-134">替代方法：手動呼叫 `startActivity()`</span><span class="sxs-lookup"><span data-stu-id="f3f57-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="f3f57-135">如果您無法或不想要多載 `UIViewController` 類別，可以改用直接呼叫 `EngagementAgent` 的方法來開始活動。</span><span class="sxs-lookup"><span data-stu-id="f3f57-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3f57-136">iOS SDK 會在應用程式關閉時自動呼叫 `endActivity()` 方法。</span><span class="sxs-lookup"><span data-stu-id="f3f57-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="f3f57-137">因此，「強烈」建議每當使用者的活動變更時便呼叫 `startActivity` 方法，並且「絕對不要」呼叫 `endActivity` 方法，因為呼叫此方法會強制結束目前的工作階段。</span><span class="sxs-lookup"><span data-stu-id="f3f57-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="f3f57-138">位置報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-138">Location reporting</span></span>
<span data-ttu-id="f3f57-139">Apple 服務條款不允許應用程式只為了統計資料的目的而使用位置追蹤。</span><span class="sxs-lookup"><span data-stu-id="f3f57-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="f3f57-140">因此，建議您只有當應用程式也會因為另一個原因而使用位置追蹤時，才啟用位置報告。</span><span class="sxs-lookup"><span data-stu-id="f3f57-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="f3f57-141">從 iOS 8 開始，您必須提供應用程式如何使用位置服務的描述，方法是在應用程式的 Info.plist 檔案中設定索引鍵 [NSLocationWhenInUseUsageDescription] 或 [NSLocationAlwaysUsageDescription] 的字串。</span><span class="sxs-lookup"><span data-stu-id="f3f57-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="f3f57-142">如果您想要在背景以 Engagement 報告位置，請加入 NSLocationAlwaysUsageDescription 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f3f57-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="f3f57-143">在其他情況下，請加入 NSLocationWhenInUseUsageDescription 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f3f57-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="f3f57-144">請注意，在 iOS 11 上，您同時需要 NSLocationAlwaysAndWhenInUseUsageDescription 和 NSLocationWhenInUseUsageDescription 來報告背景位置。</span><span class="sxs-lookup"><span data-stu-id="f3f57-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="f3f57-145">簡易區域位置報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-145">Lazy area location reporting</span></span>
<span data-ttu-id="f3f57-146">延遲區域位置報告允許報告國家、地區以及與裝置相關聯的位置。</span><span class="sxs-lookup"><span data-stu-id="f3f57-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="f3f57-147">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="f3f57-148">每個工作階段最多報告一次裝置區域。</span><span class="sxs-lookup"><span data-stu-id="f3f57-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="f3f57-149">絕不會使用 GPS，因此這類位置報告對於電池的影響很小 (但不是沒有)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="f3f57-150">報告的區域用來計算關於使用者、工作階段、事件與錯誤的地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="f3f57-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="f3f57-151">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="f3f57-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="f3f57-152">針對裝置報告的最後已知區域可以藉由 [裝置 API]來擷取。</span><span class="sxs-lookup"><span data-stu-id="f3f57-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="f3f57-153">若要啟用延遲區域位置報告，請在初始化 Engagement 代理程式之後加入下面這一行：</span><span class="sxs-lookup"><span data-stu-id="f3f57-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="f3f57-154">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-154">Real time location reporting</span></span>
<span data-ttu-id="f3f57-155">即時位置報告允許報告與裝置相關聯的緯度和經度。</span><span class="sxs-lookup"><span data-stu-id="f3f57-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="f3f57-156">根據預設，這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)，且只會在應用程式於前景中執行 (也就是在工作階段) 時，報告才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="f3f57-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="f3f57-157">即時位置「不會」  用來計算統計資料。</span><span class="sxs-lookup"><span data-stu-id="f3f57-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="f3f57-158">其唯一用途，是允許在觸達活動中使用即時地理圍欄 \<Reach-Audience-geofencing\> 準則。</span><span class="sxs-lookup"><span data-stu-id="f3f57-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="f3f57-159">若要啟用即時位置報告，請在初始化 Engagement 代理程式之後加入下面這一行：</span><span class="sxs-lookup"><span data-stu-id="f3f57-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="f3f57-160">GPS 的報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-160">GPS based reporting</span></span>
<span data-ttu-id="f3f57-161">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="f3f57-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="f3f57-162">若要啟用 GPS 位置 (精準度大為提高)，請加入：</span><span class="sxs-lookup"><span data-stu-id="f3f57-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="f3f57-163">背景報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-163">Background reporting</span></span>
<span data-ttu-id="f3f57-164">根據預設，即時位置報告只在應用程式在前景中執行 (也就是在工作階段) 時才會為作用中。</span><span class="sxs-lookup"><span data-stu-id="f3f57-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="f3f57-165">若要也在背景中啟用報告，請加入：</span><span class="sxs-lookup"><span data-stu-id="f3f57-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="f3f57-166">當應用程式在背景中執行，即使啟用 GPS，也只會報告網路位置。</span><span class="sxs-lookup"><span data-stu-id="f3f57-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="f3f57-167">實作此函數會在應用程式進入背景時呼叫 [startMonitoringSignificantLocationChanges] 。</span><span class="sxs-lookup"><span data-stu-id="f3f57-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="f3f57-168">請注意，如果新的位置事件抵達，它會自動重新啟動您的應用程式到背景中。</span><span class="sxs-lookup"><span data-stu-id="f3f57-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="f3f57-169">進階報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-169">Advanced reporting</span></span>
<span data-ttu-id="f3f57-170">此外，如果您想要報告應用程式的特定事件、錯誤和工作，必須透過 `EngagementAgent` 類別的方法使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="f3f57-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="f3f57-171">此類別的物件可以透過呼叫 `[EngagementAgent shared]` 靜態方法來擷取。</span><span class="sxs-lookup"><span data-stu-id="f3f57-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="f3f57-172">Engagement API 可允許使用所有 Engagement 的進階功能，詳情請見＜如何在 iOS 上使用 Engagement API＞(以及 `EngagementAgent` 類別的技術文件)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="f3f57-173">停用 IDFA 集合</span><span class="sxs-lookup"><span data-stu-id="f3f57-173">Disable IDFA collection</span></span>
<span data-ttu-id="f3f57-174">根據預設，Engagement 會使用 [IDFA] 來唯一識別使用者。</span><span class="sxs-lookup"><span data-stu-id="f3f57-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="f3f57-175">但是，如果您未在應用程式中的其他地方使用廣告，您可能會遭到應用程式市集審查程序拒絕。</span><span class="sxs-lookup"><span data-stu-id="f3f57-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="f3f57-176">您可以在 pch 檔案 (或是在應用程式的 `Build Settings` 中) 加入前置處理器巨集 `ENGAGEMENT_DISABLE_IDFA`，藉此停用 IDFA 集合。</span><span class="sxs-lookup"><span data-stu-id="f3f57-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="f3f57-177">如此可確保應用程式組建中沒有任何對 `ASIdentifierManager`、`advertisingIdentifier` 或 `isAdvertisingTrackingEnabled` 的參考。</span><span class="sxs-lookup"><span data-stu-id="f3f57-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="f3f57-178">**prefix.pch** 檔案中的整合：</span><span class="sxs-lookup"><span data-stu-id="f3f57-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="f3f57-179">您可以藉由檢查 Engagement 測試記錄檔，確認 IDFA 集合已在應用程式中正確停用。</span><span class="sxs-lookup"><span data-stu-id="f3f57-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="f3f57-180">請參閱 Integration Test\<ios-sdk-engagement-test-idfa\> 文件以取得進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="f3f57-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="f3f57-181">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="f3f57-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="f3f57-182">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="f3f57-182">Using a method call</span></span>
<span data-ttu-id="f3f57-183">如果您想要 Engagement 停止傳送記錄檔，可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="f3f57-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="f3f57-184">這個呼叫是持續性的：它會使用 `NSUserDefaults` 來存放資訊。</span><span class="sxs-lookup"><span data-stu-id="f3f57-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="f3f57-185">您可以使用 `YES`呼叫相同函數，即可再次啟用記錄報告。</span><span class="sxs-lookup"><span data-stu-id="f3f57-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="f3f57-186">設定組合中的整合</span><span class="sxs-lookup"><span data-stu-id="f3f57-186">Integration in your settings bundle</span></span>
<span data-ttu-id="f3f57-187">如不呼叫此函數，您也可以直接在現有的 `Settings.bundle` 檔案中整合此設定。</span><span class="sxs-lookup"><span data-stu-id="f3f57-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="f3f57-188">字串 `engagement_agent_enabled` 必須當做喜好設定識別碼，而且必須與切換開關相關聯 (`PSToggleSwitchSpecifier`)。</span><span class="sxs-lookup"><span data-stu-id="f3f57-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="f3f57-189">以下 `Settings.bundle` 範例說明如何實作：</span><span class="sxs-lookup"><span data-stu-id="f3f57-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
<span data-ttu-id="f3f57-190">[裝置 API]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="f3f57-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="f3f57-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="f3f57-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="f3f57-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="f3f57-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="f3f57-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="f3f57-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="f3f57-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="f3f57-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
