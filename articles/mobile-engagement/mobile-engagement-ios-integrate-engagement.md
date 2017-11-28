---
title: "Mobile Engagement iOS SDK 整合 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="9b898-103">如何在 iOS 上的 tooIntegrate Engagement</span><span class="sxs-lookup"><span data-stu-id="9b898-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b898-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="9b898-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="9b898-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="9b898-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="9b898-106">iOS</span><span class="sxs-lookup"><span data-stu-id="9b898-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="9b898-107">Android</span><span class="sxs-lookup"><span data-stu-id="9b898-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="9b898-108">此程序描述 hello 最簡單方式 tooactivate Engagement 分析及監視您的 iOS 應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="9b898-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="9b898-109">hello Engagement SDK 需要 iOS7 + 和 Xcode 8 +: hello 部署目標的應用程式至少必須為 iOS 7。</span><span class="sxs-lookup"><span data-stu-id="9b898-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="9b898-110">如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。</span><span class="sxs-lookup"><span data-stu-id="9b898-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="9b898-111">沒有已知的錯誤之前的版本中的 hello 觸達模組，請參閱 iOS 10 裝置上執行時[hello 觸達模組整合](mobile-engagement-ios-integrate-engagement-reach.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9b898-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="9b898-112">若您選擇 toouse hello SDK v3.2.4 則直接略過 hello `UserNotifications.framework` hello 下一個步驟中匯入。</span><span class="sxs-lookup"><span data-stu-id="9b898-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="9b898-113">hello 步驟所記錄的足夠 tooactivate hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="9b898-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="9b898-114">hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 進階 Mobile Engagement 應用程式開發介面中 iOS 應用程式所標記的方式](mobile-engagement-ios-use-engagement-api.md)自這些統計資料所相依的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b898-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="9b898-115">內嵌至 iOS 專案中的 hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="9b898-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="9b898-116">下載 hello iOS SDK 從[這裡](http://aka.ms/qk2rnj)。</span><span class="sxs-lookup"><span data-stu-id="9b898-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="9b898-117">新增 hello Engagement SDK tooyour iOS 專案： 在 Xcode 中，以滑鼠右鍵按一下您的專案並選取**」 太新增檔案..."**選擇 hello`EngagementSDK`資料夾。</span><span class="sxs-lookup"><span data-stu-id="9b898-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="9b898-118">Engagement 會需要額外的架構 toowork: hello 專案總管 中開啟您專案的窗格，然後選取 hello 正確的目標。</span><span class="sxs-lookup"><span data-stu-id="9b898-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="9b898-119">然後，開啟 hello **建置階段** 索引標籤和 hello **< 連結二進位與媒體櫃**功能表上，新增這些架構：</span><span class="sxs-lookup"><span data-stu-id="9b898-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="9b898-120">`UserNotifications.framework`-為設定 hello 連結`Optional`</span><span class="sxs-lookup"><span data-stu-id="9b898-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="9b898-121">`AdSupport.framework`-為設定 hello 連結`Optional`</span><span class="sxs-lookup"><span data-stu-id="9b898-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="9b898-122">您可以移除 hello AdSupport 架構。</span><span class="sxs-lookup"><span data-stu-id="9b898-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="9b898-123">Engagement 會需要這個 framework toocollect hello IDFA。</span><span class="sxs-lookup"><span data-stu-id="9b898-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="9b898-124">不過，您可以停用 IDFA 收集\<ios sdk-engagement idfa\> toocomply hello 新 Apple 原則有關此識別碼。</span><span class="sxs-lookup"><span data-stu-id="9b898-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="9b898-125">初始化 hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="9b898-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="9b898-126">您需要 toomodify 您應用程式的委派：</span><span class="sxs-lookup"><span data-stu-id="9b898-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="9b898-127">在實作檔 hello 頂端，匯入 hello Engagement 代理程式：</span><span class="sxs-lookup"><span data-stu-id="9b898-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="9b898-128">初始化 Engagement hello 方法內 '**applicationDidFinishLaunching:**'**: Didfinishlaunchingwithoptions<:**':</span><span class="sxs-lookup"><span data-stu-id="9b898-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="9b898-129">基本報告</span><span class="sxs-lookup"><span data-stu-id="9b898-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="9b898-130">建議使用的方法：多載您的 `UIViewController` 類別</span><span class="sxs-lookup"><span data-stu-id="9b898-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="9b898-131">訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您可以只在所有您`UIViewController`子類別是繼承自 hello`EngagementViewController`類別 （相同的規則如`UITableViewController`  - \> `EngagementTableViewController`)。</span><span class="sxs-lookup"><span data-stu-id="9b898-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="9b898-132">**沒有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="9b898-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="9b898-133">**有 Engagement：**</span><span class="sxs-lookup"><span data-stu-id="9b898-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="9b898-134">替代方法：手動呼叫 `startActivity()`</span><span class="sxs-lookup"><span data-stu-id="9b898-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="9b898-135">如果您無法或不想 toooverload 您`UIViewController`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`的直接的方法。</span><span class="sxs-lookup"><span data-stu-id="9b898-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b898-136">hello iOS SDK 會自動呼叫 hello `endActivity()` hello 應用程式關閉時的方法。</span><span class="sxs-lookup"><span data-stu-id="9b898-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="9b898-137">因此，它是*高*建議 toocall hello`startActivity`每當 hello 使用者的 hello 活動變更時，方法和太*永不*呼叫 hello`endActivity`方法，因為呼叫這個方法會強制hello 目前工作階段 toobe 結束。</span><span class="sxs-lookup"><span data-stu-id="9b898-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="9b898-138">位置報告</span><span class="sxs-lookup"><span data-stu-id="9b898-138">Location reporting</span></span>
<span data-ttu-id="9b898-139">Apple 服務條款不允許應用程式統計資料的目的只追蹤 toouse 位置。</span><span class="sxs-lookup"><span data-stu-id="9b898-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="9b898-140">因此，建議 tooenable 位置報告只有當您的應用程式也會使用 hello 位置追蹤，因為其他原因。</span><span class="sxs-lookup"><span data-stu-id="9b898-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="9b898-141">從 iOS 8 開始，您必須提供您的應用程式藉由設定 hello 索引鍵的字串所使用的位置服務的描述[NSLocationWhenInUseUsageDescription]或[NSLocationAlwaysUsageDescription]您的應用程式 Info.plist 檔案中。</span><span class="sxs-lookup"><span data-stu-id="9b898-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="9b898-142">如果您想在 hello 背景與 Engagement tooreport 位置，請新增 hello 金鑰 NSLocationAlwaysUsageDescription。</span><span class="sxs-lookup"><span data-stu-id="9b898-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="9b898-143">在其他情況下，加入 hello 機碼 NSLocationWhenInUseUsageDescription。</span><span class="sxs-lookup"><span data-stu-id="9b898-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="9b898-144">請注意，您需要在 iOS 11 NSLocationAlwaysAndWhenInUseUsageDescription 和 NSLocationWhenInUseUsageDescription tooreport 背景位置。</span><span class="sxs-lookup"><span data-stu-id="9b898-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="9b898-145">簡易區域位置報告</span><span class="sxs-lookup"><span data-stu-id="9b898-145">Lazy area location reporting</span></span>
<span data-ttu-id="9b898-146">延遲區域位置回報允許 tooreport hello 國家/地區、 區域和位置相關聯 toodevices。</span><span class="sxs-lookup"><span data-stu-id="9b898-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="9b898-147">這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。</span><span class="sxs-lookup"><span data-stu-id="9b898-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="9b898-148">裝置 hello 區域會報告每個工作階段最多一次。</span><span class="sxs-lookup"><span data-stu-id="9b898-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="9b898-149">hello GPS 從未使用過，，因此這種類型的報表位置會有很少 (不 toosay 沒有) hello 電池的影響。</span><span class="sxs-lookup"><span data-stu-id="9b898-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="9b898-150">報告的區域是使用的 toocompute 有關使用者、 工作階段、 事件和錯誤地理統計資料。</span><span class="sxs-lookup"><span data-stu-id="9b898-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="9b898-151">它們也可用來做為觸達活動的準則。</span><span class="sxs-lookup"><span data-stu-id="9b898-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="9b898-152">最後一個已知區域所報告的裝置可以擷取感謝您 toohello hello[裝置 API]。</span><span class="sxs-lookup"><span data-stu-id="9b898-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="9b898-153">tooenable 延遲區域位置回報，加入下列一行之後初始化 hello Engagement 代理程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="9b898-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="9b898-154">即時位置報告</span><span class="sxs-lookup"><span data-stu-id="9b898-154">Real time location reporting</span></span>
<span data-ttu-id="9b898-155">即時位置回報允許 tooreport hello 緯度和經度相關聯 toodevices。</span><span class="sxs-lookup"><span data-stu-id="9b898-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="9b898-156">根據預設，這類位置報告只會使用網路位置 （根據資料格識別碼或 WIFI），而且 hello reporting 僅 active hello 應用程式在前景中執行 （也就是在工作階段） 時。</span><span class="sxs-lookup"><span data-stu-id="9b898-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="9b898-157">即時位置*不*用 toocompute 統計資料。</span><span class="sxs-lookup"><span data-stu-id="9b898-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="9b898-158">其唯一用途就是即時地理圍欄 tooallow hello 使用\<觸達觀眾-地理圍欄\>觸達活動中的準則。</span><span class="sxs-lookup"><span data-stu-id="9b898-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="9b898-159">tooenable 即時位置回報，加入下列一行之後初始化 hello Engagement 代理程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="9b898-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="9b898-160">GPS 的報告</span><span class="sxs-lookup"><span data-stu-id="9b898-160">GPS based reporting</span></span>
<span data-ttu-id="9b898-161">根據預設，即時位置報告只會使用網路位置。</span><span class="sxs-lookup"><span data-stu-id="9b898-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="9b898-162">GPS tooenable hello 使用基礎 （也就是更精確） 的位置，加入：</span><span class="sxs-lookup"><span data-stu-id="9b898-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="9b898-163">背景報告</span><span class="sxs-lookup"><span data-stu-id="9b898-163">Background reporting</span></span>
<span data-ttu-id="9b898-164">根據預設，即時位置回報作用中時才 hello 應用程式在前景中執行 （也就是在工作階段）。</span><span class="sxs-lookup"><span data-stu-id="9b898-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="9b898-165">tooenable hello reporting 也在背景中，加入：</span><span class="sxs-lookup"><span data-stu-id="9b898-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="9b898-166">當背景中執行 hello 應用程式時，會報告只有基礎的網路位置，即使您啟用 hello GPS。</span><span class="sxs-lookup"><span data-stu-id="9b898-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="9b898-167">此函式實作會呼叫[startMonitoringSignificantLocationChanges]應用程式進入 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="9b898-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="9b898-168">請注意，它會自動重新啟動應用程式分成 hello 背景如果新的位置事件抵達。</span><span class="sxs-lookup"><span data-stu-id="9b898-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="9b898-169">進階報告</span><span class="sxs-lookup"><span data-stu-id="9b898-169">Advanced reporting</span></span>
<span data-ttu-id="9b898-170">（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您需要透過 hello 方法的 hello toouse hello Engagement API`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="9b898-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="9b898-171">這個類別的物件可以擷取由呼叫 hello`[EngagementAgent shared]`靜態方法。</span><span class="sxs-lookup"><span data-stu-id="9b898-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="9b898-172">hello Engagement API 允許 toouse 所有參與的進階功能，並會詳細說明 hello 如何 tooUse 在 iOS 上的行動應用程式開發介面 (以及在 hello hello 的技術文件中`EngagementAgent`類別)。</span><span class="sxs-lookup"><span data-stu-id="9b898-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="9b898-173">停用 IDFA 集合</span><span class="sxs-lookup"><span data-stu-id="9b898-173">Disable IDFA collection</span></span>
<span data-ttu-id="9b898-174">根據預設，部署將會使用 hello [IDFA] toouniquely 識別使用者。</span><span class="sxs-lookup"><span data-stu-id="9b898-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="9b898-175">但是，如果您不使用廣告 hello 應用程式中的其他位置，您可能會拒絕的 hello App Store 檢閱程序。</span><span class="sxs-lookup"><span data-stu-id="9b898-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="9b898-176">藉由新增 hello 前置處理器巨集可以停用 IDFA 收集`ENGAGEMENT_DISABLE_IDFA`pch 檔案中 (或在 hello`Build Settings`應用程式)。</span><span class="sxs-lookup"><span data-stu-id="9b898-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="9b898-177">這可確保沒有任何參考太`ASIdentifierManager`，`advertisingIdentifier`或`isAdvertisingTrackingEnabled`hello 應用程式組建中。</span><span class="sxs-lookup"><span data-stu-id="9b898-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="9b898-178">Hello 中的整合**prefix.pch**檔案：</span><span class="sxs-lookup"><span data-stu-id="9b898-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="9b898-179">您可以確認 hello IDFA 收集已正確地停用應用程式中藉由檢查 hello Engagement 測試記錄。</span><span class="sxs-lookup"><span data-stu-id="9b898-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="9b898-180">請參閱整合測試的 hello\<ios-sdk-部署-測試-idfa\>文件的進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="9b898-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="9b898-181">停用記錄報告</span><span class="sxs-lookup"><span data-stu-id="9b898-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="9b898-182">使用方法呼叫</span><span class="sxs-lookup"><span data-stu-id="9b898-182">Using a method call</span></span>
<span data-ttu-id="9b898-183">如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：</span><span class="sxs-lookup"><span data-stu-id="9b898-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="9b898-184">這個呼叫是持續性： 它會使用`NSUserDefaults`toostore hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="9b898-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="9b898-185">您可以啟用記錄 reporting 再次呼叫相同函式與 hello `YES`。</span><span class="sxs-lookup"><span data-stu-id="9b898-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="9b898-186">設定組合中的整合</span><span class="sxs-lookup"><span data-stu-id="9b898-186">Integration in your settings bundle</span></span>
<span data-ttu-id="9b898-187">如不呼叫此函數，您也可以直接在現有的 `Settings.bundle` 檔案中整合此設定。</span><span class="sxs-lookup"><span data-stu-id="9b898-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="9b898-188">hello 字串`engagement_agent_enabled`必須使用為 hello 喜好設定識別項，且必須關聯的 tooa 切換參數 (`PSToggleSwitchSpecifier`)。</span><span class="sxs-lookup"><span data-stu-id="9b898-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="9b898-189">下列範例中的 hello`Settings.bundle`示範如何 tooimplement 它：</span><span class="sxs-lookup"><span data-stu-id="9b898-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
[裝置 API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
