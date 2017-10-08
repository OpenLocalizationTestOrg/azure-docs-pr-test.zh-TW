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
# <a name="how-toointegrate-engagement-on-ios"></a>如何在 iOS 上的 tooIntegrate Engagement
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

此程序描述 hello 最簡單方式 tooactivate Engagement 分析及監視您的 iOS 應用程式中的函式。

hello Engagement SDK 需要 iOS7 + 和 Xcode 8 +: hello 部署目標的應用程式至少必須為 iOS 7。

> [!NOTE]
> 如果您真的依賴 XCode 7，則您可能使用 hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)。 沒有已知的錯誤之前的版本中的 hello 觸達模組，請參閱 iOS 10 裝置上執行時[hello 觸達模組整合](mobile-engagement-ios-integrate-engagement-reach.md)如需詳細資訊。 若您選擇 toouse hello SDK v3.2.4 則直接略過 hello `UserNotifications.framework` hello 下一個步驟中匯入。
>
>

hello 步驟所記錄的足夠 tooactivate hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。 hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 進階 Mobile Engagement 應用程式開發介面中 iOS 應用程式所標記的方式](mobile-engagement-ios-use-engagement-api.md)自這些統計資料所相依的應用程式。

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>內嵌至 iOS 專案中的 hello Engagement SDK
* 下載 hello iOS SDK 從[這裡](http://aka.ms/qk2rnj)。
* 新增 hello Engagement SDK tooyour iOS 專案： 在 Xcode 中，以滑鼠右鍵按一下您的專案並選取**」 太新增檔案..."**選擇 hello`EngagementSDK`資料夾。
* Engagement 會需要額外的架構 toowork: hello 專案總管 中開啟您專案的窗格，然後選取 hello 正確的目標。 然後，開啟 hello **建置階段** 索引標籤和 hello **< 連結二進位與媒體櫃**功能表上，新增這些架構：

  * `UserNotifications.framework`-為設定 hello 連結`Optional`
  * `AdSupport.framework`-為設定 hello 連結`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> 您可以移除 hello AdSupport 架構。 Engagement 會需要這個 framework toocollect hello IDFA。 不過，您可以停用 IDFA 收集\<ios sdk-engagement idfa\> toocomply hello 新 Apple 原則有關此識別碼。
>
>

## <a name="initialize-hello-engagement-sdk"></a>初始化 hello Engagement SDK
您需要 toomodify 您應用程式的委派：

* 在實作檔 hello 頂端，匯入 hello Engagement 代理程式：

      [...]
      #import "EngagementAgent.h"
* 初始化 Engagement hello 方法內 '**applicationDidFinishLaunching:**'**: Didfinishlaunchingwithoptions<:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>基本報告
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>建議使用的方法：多載您的 `UIViewController` 類別
訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您可以只在所有您`UIViewController`子類別是繼承自 hello`EngagementViewController`類別 （相同的規則如`UITableViewController`  - \> `EngagementTableViewController`)。

**沒有 Engagement：**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**有 Engagement：**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>替代方法：手動呼叫 `startActivity()`
如果您無法或不想 toooverload 您`UIViewController`類別，您可以改為啟動您的活動藉由呼叫`EngagementAgent`的直接的方法。

> [!IMPORTANT]
> hello iOS SDK 會自動呼叫 hello `endActivity()` hello 應用程式關閉時的方法。 因此，它是*高*建議 toocall hello`startActivity`每當 hello 使用者的 hello 活動變更時，方法和太*永不*呼叫 hello`endActivity`方法，因為呼叫這個方法會強制hello 目前工作階段 toobe 結束。
>
>

## <a name="location-reporting"></a>位置報告
Apple 服務條款不允許應用程式統計資料的目的只追蹤 toouse 位置。 因此，建議 tooenable 位置報告只有當您的應用程式也會使用 hello 位置追蹤，因為其他原因。

從 iOS 8 開始，您必須提供您的應用程式藉由設定 hello 索引鍵的字串所使用的位置服務的描述[NSLocationWhenInUseUsageDescription]或[NSLocationAlwaysUsageDescription]您的應用程式 Info.plist 檔案中。 如果您想在 hello 背景與 Engagement tooreport 位置，請新增 hello 金鑰 NSLocationAlwaysUsageDescription。 在其他情況下，加入 hello 機碼 NSLocationWhenInUseUsageDescription。 請注意，您需要在 iOS 11 NSLocationAlwaysAndWhenInUseUsageDescription 和 NSLocationWhenInUseUsageDescription tooreport 背景位置。

### <a name="lazy-area-location-reporting"></a>簡易區域位置報告
延遲區域位置回報允許 tooreport hello 國家/地區、 區域和位置相關聯 toodevices。 這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。 裝置 hello 區域會報告每個工作階段最多一次。 hello GPS 從未使用過，，因此這種類型的報表位置會有很少 (不 toosay 沒有) hello 電池的影響。

報告的區域是使用的 toocompute 有關使用者、 工作階段、 事件和錯誤地理統計資料。 它們也可用來做為觸達活動的準則。 最後一個已知區域所報告的裝置可以擷取感謝您 toohello hello[裝置 API]。

tooenable 延遲區域位置回報，加入下列一行之後初始化 hello Engagement 代理程式的 hello:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>即時位置報告
即時位置回報允許 tooreport hello 緯度和經度相關聯 toodevices。 根據預設，這類位置報告只會使用網路位置 （根據資料格識別碼或 WIFI），而且 hello reporting 僅 active hello 應用程式在前景中執行 （也就是在工作階段） 時。

即時位置*不*用 toocompute 統計資料。 其唯一用途就是即時地理圍欄 tooallow hello 使用\<觸達觀眾-地理圍欄\>觸達活動中的準則。

tooenable 即時位置回報，加入下列一行之後初始化 hello Engagement 代理程式的 hello:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>GPS 的報告
根據預設，即時位置報告只會使用網路位置。 GPS tooenable hello 使用基礎 （也就是更精確） 的位置，加入：

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>背景報告
根據預設，即時位置回報作用中時才 hello 應用程式在前景中執行 （也就是在工作階段）。 tooenable hello reporting 也在背景中，加入：

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> 當背景中執行 hello 應用程式時，會報告只有基礎的網路位置，即使您啟用 hello GPS。
>
>

此函式實作會呼叫[startMonitoringSignificantLocationChanges]應用程式進入 hello 背景。 請注意，它會自動重新啟動應用程式分成 hello 背景如果新的位置事件抵達。

## <a name="advanced-reporting"></a>進階報告
（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您需要透過 hello 方法的 hello toouse hello Engagement API`EngagementAgent`類別。 這個類別的物件可以擷取由呼叫 hello`[EngagementAgent shared]`靜態方法。

hello Engagement API 允許 toouse 所有參與的進階功能，並會詳細說明 hello 如何 tooUse 在 iOS 上的行動應用程式開發介面 (以及在 hello hello 的技術文件中`EngagementAgent`類別)。

## <a name="disable-idfa-collection"></a>停用 IDFA 集合
根據預設，部署將會使用 hello [IDFA] toouniquely 識別使用者。 但是，如果您不使用廣告 hello 應用程式中的其他位置，您可能會拒絕的 hello App Store 檢閱程序。 藉由新增 hello 前置處理器巨集可以停用 IDFA 收集`ENGAGEMENT_DISABLE_IDFA`pch 檔案中 (或在 hello`Build Settings`應用程式)。 這可確保沒有任何參考太`ASIdentifierManager`，`advertisingIdentifier`或`isAdvertisingTrackingEnabled`hello 應用程式組建中。

Hello 中的整合**prefix.pch**檔案：

    #define ENGAGEMENT_DISABLE_IDFA
    ...

您可以確認 hello IDFA 收集已正確地停用應用程式中藉由檢查 hello Engagement 測試記錄。 請參閱整合測試的 hello\<ios-sdk-部署-測試-idfa\>文件的進一步資訊。

## <a name="disable-log-reporting"></a>停用記錄報告
### <a name="using-a-method-call"></a>使用方法呼叫
如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：

    [[EngagementAgent shared] setEnabled:NO];

這個呼叫是持續性： 它會使用`NSUserDefaults`toostore hello 資訊。

您可以啟用記錄 reporting 再次呼叫相同函式與 hello `YES`。

### <a name="integration-in-your-settings-bundle"></a>設定組合中的整合
如不呼叫此函數，您也可以直接在現有的 `Settings.bundle` 檔案中整合此設定。 hello 字串`engagement_agent_enabled`必須使用為 hello 喜好設定識別項，且必須關聯的 tooa 切換參數 (`PSToggleSwitchSpecifier`)。

下列範例中的 hello`Settings.bundle`示範如何 tooimplement 它：

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
