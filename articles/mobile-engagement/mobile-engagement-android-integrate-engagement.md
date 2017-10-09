---
title: "aaaAzure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>如何在 Android 上 Engagement tooIntegrate
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

此程序描述 hello 最簡單方式 tooactivate Engagement 分析及監視您的 Android 應用程式中的函式。

> [!IMPORTANT]
> 最低 Android SDK API 層級必須是 10 或更高版本 (Android 2.3.3 或更高版本)。
> 
> 

hello 步驟所記錄的足夠 tooactivates hello 報表所需 toocompute 關於使用者、 工作階段、 活動、 當機和 Technicals 的所有統計資料。 hello 報表的記錄檔所需 toocompute 其他統計資料像是事件、 錯誤和作業必須完成手動使用 hello Engagement 應用程式開發介面 (請參閱[toouse hello 如何進階標記您的 Android 應用程式開發介面的 Mobile Engagement](mobile-engagement-android-use-engagement-api.md)自這些統計資料是應用程式相依。

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>嵌入您的 Android 專案中的 hello Engagement SDK 和服務
下載 hello 從 Android SDK[這裡](https://aka.ms/vq9mfn)取得`mobile-engagement-VERSION.jar`並將它們放入 hello `libs` Android 專案的資料夾 （如果它尚未存在，請建立 hello 程式庫資料夾）。

> [!IMPORTANT]
> 如果您建立使用 ProGuard 應用程式套件，您需要 tookeep 某些類別。 您可以使用下列組態程式碼片段的 hello:
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

指定依照 hello 啟動器活動的方法呼叫 hello Engagement 連接字串：

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

您的應用程式的 hello 連接字串會顯示在 Azure 入口網站。

* 如果遺失，新增下列 Android 的權限的 hello (之前 hello`<application>`標記):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* 新增下列區段的 hello (之間 hello`<application>`和`</application>`標記):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* 變更`<Your application name>`hello 應用程式的名稱。

> [!TIP]
> hello`android:label`屬性可讓您 toochoose hello hello Engagement 服務名稱將顯示 toohello 使用者在他們的電話號碼的 hello 」 執行的服務 」 畫面。 它會建議 tooset 這個屬性太`"<Your application name>Service"`(例如`"AcmeFunGameService"`)。
> 
> 

指定 hello`android:process`屬性可確保該 hello Engagement 服務會在自己的處理序 （在相同的處理序因為您的應用程式會使得您的主要/UI 執行緒可能較不回應 hello 執行 Engagement） 中執行。

> [!NOTE]
> 您將放置在任何程式碼`Application.onCreate()`並將所有應用程式的處理程序，包括 hello Engagement 服務執行其他應用程式回呼。 它有不必要的副作用 （如不需要的記憶體配置和 hello Engagement 的程序、 重複廣播的接收者或服務中的執行緒）。
> 
> 

如果您覆寫`Application.onCreate()`，它為下列程式碼片段在 hello 開頭的建議的 tooadd hello 您`Application.onCreate()`函式：

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

您可以 hello 相同的動作，如`Application.onTerminate()`，`Application.onLowMemory()`和`Application.onConfigurationChanged(...)`。

您也可以擴充`EngagementApplication`而不是擴充`Application`: hello 回呼`Application.onCreate()`程序的核取並呼叫沒有 hello`Application.onApplicationProcessCreate()`僅 hello 目前處理序是否不 hello 一個裝載 hello Engagement 服務，hello 適用相同的規則hello 其他回呼。

## <a name="basic-reporting"></a>基本報告
### <a name="recommended-method-overload-your-activity-classes"></a>建議使用的方法：多載您的 `Activity` 類別
在訂單 tooactivate hello Engagement toocompute 使用者、 工作階段、 活動、 當機和技術的統計資料所需的所有 hello 記錄檔的報表，您只需要 toomake 所有您`*Activity`子類別是繼承自 hello 對應`Engagement*Activity`類別 (例如： 如果您的舊版活動延伸`ListActivity`，讓它會擴充`EngagementListActivity`)。

**沒有 Engagement：**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**有 Engagement：**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> 當使用`EngagementListActivity`或`EngagementExpandableListActivity`，請確定任何呼叫太`requestWindowFeature(...);`太進行 hello 呼叫之前`super.onCreate(...);`，否則會發生損毀。
> 
> 

您可以在 hello 找到這些類別`src`資料夾，並可以將其複製到您的專案。 hello 類別中也會有 hello **JavaDoc**。

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>替代方法：手動呼叫 `startActivity()` 和 `endActivity()`
如果您無法或不想 toooverload 您`Activity`類別，您可以改為啟動及結束您的活動藉由呼叫`EngagementAgent`的直接的方法。

> [!IMPORTANT]
> hello Android SDK 從未呼叫 hello`endActivity()`方法，即使關閉 hello 應用程式 （在 Android 上，已關閉應用程式實際上永遠不會）。 因此，它是*高*建議 toocall hello `startActivity()` hello 中的方法`onResume`回呼的*所有*程式活動與 hello `endActivity()` hello 中的方法`onPause()`回呼的*所有*程式活動。 這是 hello 唯一方式 toobe 確定不會遺漏工作階段。 如果工作階段外洩，hello Engagement 服務將永遠不會中斷 hello Engagement 後端 （因為 hello 服務仍會保持連接，只要工作階段已暫止）。
> 
> 

下列是一個範例：

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

此範例非常類似 toohello`EngagementActivity`類別與變種，提供其原始程式碼中 hello`src`資料夾。

## <a name="test"></a>測試
現在請確認您的整合，方法是執行中模擬器或裝置的行動應用程式，然後確認它註冊 hello 監視 索引標籤上的工作階段。

hello 下一個區段是選擇性的。

## <a name="location-reporting"></a>位置報告
如果您想位置 toobe 報告，您需要 tooadd 幾行程式的組態 (之間 hello`<application>`和`</application>`標記)。

### <a name="lazy-area-location-reporting"></a>簡易區域位置報告
延遲區域位置回報允許 tooreport hello 國家/地區、 區域和位置相關聯 toodevices。 這類位置報告只會使用網路位置 (根據基地台識別碼或 WIFI)。 裝置 hello 區域會報告每個工作階段最多一次。 hello GPS 從未使用過，，因此這種類型的報表位置會有很少 (不 toosay 沒有) hello 電池的影響。

報告的區域是使用的 toocompute 有關使用者、 工作階段、 事件和錯誤地理統計資料。 它們也可用來做為觸達活動的準則。

tooenable 延遲區域位置回報，您可以使用此程序中先前所述的 hello 組態來進行：

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

您還需要下列權限，如果遺漏 tooadd hello:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。

### <a name="real-time-location-reporting"></a>即時位置報告
即時位置回報允許 tooreport hello 緯度和經度相關聯 toodevices。 根據預設，這類位置報告只會使用網路位置 （根據資料格識別碼或 WIFI），而且 hello reporting 僅 active hello 應用程式在前景中執行 （也就是在工作階段） 時。

即時位置*不*用 toocompute 統計資料。 其唯一用途就是即時地理圍欄 tooallow hello 使用\<觸達觀眾-地理圍欄\>觸達活動中的準則。

tooenable 即時位置回報，您可以使用此程序中先前所述的 hello 組態來進行：

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

您還需要下列權限，如果遺漏 tooadd hello:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

或者如果您已經在應用程式中使用 ``ACCESS_FINE_LOCATION`` ，則可以繼續使用。

#### <a name="gps-based-reporting"></a>GPS 式報告
根據預設，即時位置報告只會使用網路位置。 GPS tooenable hello 使用基礎 （也就是更精確） 的位置，請使用 hello 組態物件：

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

您還需要下列權限，如果遺漏 tooadd hello:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>背景報告
根據預設，即時位置回報作用中時才 hello 應用程式在前景中執行 （也就是在工作階段）。 tooenable hello reporting 也在背景中，使用 hello 組態物件：

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> 當背景中執行 hello 應用程式時，會報告只有基礎的網路位置，即使您啟用 hello GPS。
> 
> 

若 hello 使用者重新開機裝置，將會停止 hello 背景位置的報表，您可以加入這個 toomake 自動重新啟動在開機時：

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

您還需要下列權限，如果遺漏 tooadd hello:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Android M 權限
從 Android M 開始，某些權限會在執行階段管理，而且需要使用者核准。

如果您的目標 Android API 層級 23 hello 執行階段權限將會根據預設，新安裝的應用程式關閉。 否則預設將會開啟。

hello 使用者可以啟用/停用 hello 裝置設定 功能表中的這些權限。 關閉 權限，從系統功能表刪除 hello 應用程式的背景處理程序，這是系統行為，而且在能力 tooreceive 推送背景中沒有任何影響。

在 Mobile Engagement 的 hello 內容中，還需要在執行階段的核准的 hello 權限：

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (只有在針對 Android API 層級 23 的這個權限時)

hello 外部儲存體只能用於觸達整體功能。 如果您發現要求此權限 toobe 干擾性的使用者，您可以將它移除您用 Mobile Engagement 只但停用大圖片功能 hello 成本。

Hello 位置功能，您應要求權限 toouser 使用標準的系統對話方塊。 如果 hello 使用者核准，您需要 tootell ``EngagementAgent`` tootake 以 （否則 hello 變更將會處理的 hello 下一個時間 hello 使用者啟動 hello 應用程式） 的即時變更納入考量。

以下是在您的應用程式 toorequest 權限和轉寄的 hello 結果的活動中的程式碼範例 toouse，如果正太``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>進階報告
（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您需要透過 hello 方法的 hello toouse hello Engagement API`EngagementAgent`類別。 這個類別的物件可以透過呼叫 hello 互動式`EngagementAgent.getInstance()`靜態方法。

hello Engagement API 允許 toouse 所有參與的進階功能，並會詳細說明 hello 如何 tooUse 在 Android 上的行動應用程式開發介面 (以及在 hello hello 的技術文件中`EngagementAgent`類別)。

## <a name="advanced-configuration-in-androidmanifestxml"></a>進階組態 (在 AndroidManifest.xml 中)
### <a name="wake-locks"></a>線上醒機的鎖定
如果您想 toobe 確定統計資料會傳送即時使用 Wifi 時，或關閉囉 」 畫面時，，加入下列選擇性權限的 hello:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>當機報告
如果您想要 toodisable 損毀報表，加入 (之間 hello`<application>`和`</application>`標記):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>高載閾值
根據預設，hello Engagement 服務報表會即時記錄。 如果您的應用程式會報告記錄檔頻率很高，是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 hello 「 高載模式 」）。 toodo，加入 (之間 hello`<application>`和`</application>`標記):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

hello 高載模式稍微增加 hello 電池壽命但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間將會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。 它會建議 toouse 高載臨界值不會再於 30000 （30 秒）。

### <a name="session-timeout"></a>工作階段逾時
根據預設，工作階段是以結束的 10s hello 其最後一個活動 （這通常是按 hello 首頁所致，或透過閒置的 設定 hello 電話或跳到其他應用程式，備份金鑰，） 的結尾之後。 這是 tooavoid 工作階段分隔每個階段 hello 使用者結束，並非常快速地返回 toohello 應用程式 （這可以發生時他挑選一個映像，請檢查通知等。）。 您可能想 toomodify 這個參數。 toodo，加入 (之間 hello`<application>`和`</application>`標記):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>停用記錄報告
### <a name="using-a-method-call"></a>使用方法呼叫
如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：

            EngagementAgent.getInstance(context).setEnabled(false);

這個呼叫是持續性的：它使用共用的喜好設定檔案。

如果參與作用中時呼叫此函式，可能需要 hello 服務 toostop 1 分鐘。 不過，它將不會啟動所有 hello hello 服務下次您啟動 hello 應用程式。

您可以啟用記錄 reporting 再次呼叫相同函式與 hello `true`。

### <a name="integration-in-your-own-preferenceactivity"></a>在您自己的 `PreferenceActivity`
如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。

您可以設定您的喜好設定檔案 （由 hello 所需的模式） 的 Engagement toouse hello`AndroidManifest.xml`檔案搭配`application meta-data`:

* hello`engagement:agent:settings:name`金鑰是使用的 toodefine hello hello 共用的喜好設定檔案名稱。
* hello`engagement:agent:settings:mode`金鑰是使用的 toodefine hello 模式 hello 共用的喜好設定檔案，您應該使用 hello 相同的模式，在您`PreferenceActivity`。 必須傳遞 hello 模式，表示為數字： 如果您在程式碼中使用常數旗標的組合，請檢查 hello 總計值。

Engagement 一律使用 hello`engagement:key`內 hello 喜好設定檔案，以便管理這項設定，則為 true 的索引鍵。

下列範例中的 hello`AndroidManifest.xml`顯示 hello 預設值：

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

接著您可以將新增`CheckBoxPreference`中您的喜好設定配置，例如 hello 下列其中一個：

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
