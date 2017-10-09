---
title: "aaaAzure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>如何在 Android 上的 tooIntegrate Engagement 連接
> [!IMPORTANT]
> 您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。
> 
> 

## <a name="standard-integration"></a>標準整合

複製觸達資源檔從您的專案中的 hello SDK:

* Hello 檔案複製 hello`res/layout`資料夾傳遞以 hello SDK 到 hello`res/layout`應用程式資料夾。
* Hello 檔案複製 hello`res/drawable`資料夾傳遞以 hello SDK 到 hello`res/drawable`應用程式資料夾。

編輯 `AndroidManifest.xml` 檔案：

* 新增下列區段的 hello (之間 hello`<application>`和`</application>`標記):
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* 您必須開機所未按下此權限 tooreplay 系統通知 （否則它們將會保留在磁碟上，但不會再顯示，您只需要 tooinclude 這）。
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* 指定用於複製和編輯 hello 下列區段 （在應用程式及系統的兩者） 的通知圖示 (之間 hello`<application>`和`</application>`標記):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> 如果您打算在建立 Reach 活動時使用系統通知，則「務必」使用此區段。 Android 禁止顯示沒有圖示的系統通知。 因此，如果您省略這個區段，您的使用者將都能 tooreceive 它們。
> 
> 

* 如果您建立使用大圖片的系統通知的活動時，您需要下列權限的 tooadd hello (hello 之後`</application>`標記) 如果遺失：
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * 在 Android M 上，若您的應用程式目標為 Android API 層級 23 或更高層級， ``WRITE_EXTERNAL_STORAGE`` 權限需要使用者核准。 請閱讀 [本節](mobile-engagement-android-integrate-engagement.md#android-m-permissions)。
* 您也可以指定在 hello 系統通知到達活動 hello 裝置應該環和/或震動。 它 toowork，您必須確定宣告下列權限的 hello toomake (hello 之後`</application>`標記):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  沒有這個權限，Android 可防止系統通知，使其不要顯示當您核取 hello 信號或 hello 震動 hello 到達活動管理員中的選項。

## <a name="native-push"></a>原生推送
現在您已設定觸達模組，您需要 tooconfigure 原生推送 toobe 無法 tooreceive hello 活動 hello 裝置上。

我們在 Android 上支援兩種服務：

* Google Play 的裝置： 使用[Google Cloud Messaging]由下列 hello [tooIntegrate 與 Engagement GCM 如何引導](mobile-engagement-android-gcm-integrate.md)指南。
* Amazon 裝置： 使用[Amazon 裝置傳訊]由下列 hello [tooIntegrate 與 Engagement ADM 如何引導](mobile-engagement-android-adm-integrate.md)指南。

如果您想 tootarget Amazon 和 Google Play 的裝置，其可能 toohave 開發 1 AndroidManifest.xml/APK 內的所有項目。 但是，如果他們找到 GCM 程式碼時送出 tooAmazon，它們可能會拒絕您的應用程式。

您應該在此情況下使用多個 APK。

**現在準備 tooreceive 和顯示達到行銷活動，就會是您的應用程式 ！**

## <a name="how-toohandle-data-push"></a>Toohandle 資料的推播
### <a name="integration"></a>整合
如果您想要應用程式 toobe 無法 tooreceive 觸達資料推播通知、 的子類別有 toocreate `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` hello 中參考它`AndroidManifest.xml`檔案 (之間 hello`<application>`及/或`</application>`標記):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

然後您可以覆寫 hello`onDataPushStringReceived`和`onDataPushBase64Received`回呼。 下列是一個範例：

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>類別
hello 分類參數是選擇性的當您建立將資料推送活動時，可讓您 toofilter 資料推播通知。 這是適用於有數個廣播的接收者處理不同類型的資料推播通知，或如果您想 toopush 不同種類的`Base64`資料而且想 tooidentify 其類型，再剖析它們。

### <a name="callbacks-return-parameter"></a>回呼的傳回參數
以下是一些指導方針 tooproperly 處理 hello 傳回參數的`onDataPushStringReceived`和`onDataPushBase64Received`:

* 廣播的接收者應該傳回`null`如果不知道如何 toohandle 資料推送的 hello 回呼中。 您應該使用 hello 類別 toodetermine 是否您廣播的接收者應該要或不處理 hello 資料推送。
* 其中一個 hello 廣播接收者應該傳回`true`如果它接受 hello 資料推送的 hello 回呼中。
* 其中一個 hello 廣播接收者應該傳回`false`hello 回呼會辨識 hello 資料推入，但因故捨棄它。 例如，傳回`false`hello 收到資料時無效。
* 如果其中一個廣播接收者傳回`true`而另一個會傳回`false`hello 相同資料推入，hello 行為是未定義，您應該永遠不會這麼做。

hello 傳回型別只適用於 hello 觸達統計資料：

* `Replied`如果是傳回 hello 廣播接收者其中之一，就會遞增`true`或`false`。
* `Actioned`其中一個 hello 廣播接收者傳回時，才會遞增`true`。

## <a name="how-toocustomize-campaigns"></a>如何 toocustomize 活動
toocustomize 活動時，您可以修改 hello hello Reach SDK 中提供的配置。

您應該在 hello 版面配置中所使用的所有 hello 識別碼保留，以及使用識別項，特別是針對檢視文字和影像檢視的 hello 檢視 hello 類型。 部分檢視只使用的 toohide 或顯示區域，所以可能會變更其類型。 請如果您想檢視的 toochange hello 類型提供的 hello 版面配置中，檢查 hello 原始程式碼。

### <a name="notifications"></a>通知
有兩種類型的通知：系統和應用程式內通知，它們使用不同的配置檔。

#### <a name="system-notifications"></a>系統通知
您需要 toouse hello toocustomize 系統通知**類別**。 您可以再跳過[類別](#categories)。

#### <a name="in-app-notifications"></a>應用程式內通知
根據預設，應用程式內通知是以動態方式加入的 toohello 目前活動的使用者介面感謝您 toohello Android 方法的檢視`addContentView()`。 這稱為通知重疊。 通知的影像覆疊非常適合在快速地整合在一起，因為它們不需要您 toomodify 應用程式中的任何配置。

toomodify hello 查詢通知重疊的您可以只修改 hello 檔案`engagement_notification_area.xml`tooyour 需要。

> [!NOTE]
> hello 檔案`engagement_notification_overlay.xml`是 hello 是使用的 toocreate 通知重疊，它包含 hello 檔案`engagement_notification_area.xml`。 您也可以自訂它 toosuit 您的需求 （例如定位 hello 通知區域內 hello 重疊）。
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>包含通知配置做為活動配置的一部分
覆疊非常適合快速整合，但可能在特殊情況下造成不便或有副作用。 您可以自訂 hello 重疊系統在活動層級，讓您輕鬆 tooprevent 副作用的特殊活動。

您可以決定 tooinclude 通知配置在您現有的版面配置感謝您 toohello Android**包含**陳述式。 hello 的範例如下的已修改`ListActivity`配置只包含`ListView`。

**Engagement 整合之前：**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Engagement 整合之後：**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

在此範例中我們會加入父容器，因為 hello 原始配置的清單檢視做為 hello 上層項目。 我們也加入`android:layout_weight="1"`toobe 無法 tooadd 下方的清單檢視的檢視設定`android:layout_height="fill_parent"`。

hello Engagement 觸達 SDK 會自動偵測 hello 通知版面配置包含在此活動，且不會加入這項活動的重疊。

> [!TIP]
> 如果您在應用程式中使用 ListActivity，可見的觸達覆疊會防止您對回應 hello 清單檢視中的 tooclicked 項目不再。 這是已知的問題。 toowork 解決這個問題我們建議您在自己清單活動的配置，例如 hello 前一個範例中的 tooembed hello 通知版面配置。
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>停用關於活動的應用程式通知
如果您不想 hello 重疊 toobe 加入 tooyour 活動，而且如果您不想加入 hello 通知配置自己版面配置中，您可以停用這項活動在 hello hello 重疊`AndroidManifest.xml`加`meta-data`區段如同在 hello 下列範例：

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> 類別
當您修改提供的版面配置的 hello 時，您會修改您的通知 hello 外觀。 類別可讓您 toodefine 各種目標會尋找通知 （可能是行為）。 當您建立觸達活動時可以指定類別。 請記住，類別也可讓您自訂宣告與輪詢，本文件稍後將會說明。

tooregister 您的通知的類別處理常式，您需要 tooadd 呼叫，hello 應用程式初始化時。

> [!IMPORTANT]
> 請閱讀警告 hello android： 處理序屬性的 hello \<android sdk-engagement 處理\>hello 中如何 tooIntegrate Engagement Android 主題後再繼續。
> 
> 

hello 下列範例假設您認可 hello 先前的警告，且使用的子類別`EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

hello`MyNotifier`物件是 hello hello 通知類別處理常式實作。 其中一個是實作的 hello`EngagementNotifier`介面或子類別的 hello 預設實作： `EngagementDefaultNotifier`。

請注意，hello 相同通知程式可以處理數種類別，就能註冊它們像這樣：

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello 預設類別實作中，您可以在下列範例中的 hello 註冊您的實作，例如：

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

使用處理常式中的 hello 目前類別會傳遞做為參數，您可以覆寫中的大部分方法中`EngagementDefaultNotifier`。

這能以 `String` 參數的形式傳遞，或是間接在 `EngagementReachContent` 物件中傳遞 (使用 `getCategory()` 方法)。

您可以重新定義上的方法來變更大部分的 hello 通知建立程序`EngagementDefaultNotifier`，針對更進階的自訂覺得可用 tootake 在 hello 技術文件，而 hello 原始程式碼在一起來看看。

##### <a name="in-app-notifications"></a>應用程式內通知
如果您只想 toouse 替代配置特定分類，您可以實作此如 hello 下列範例所示：

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**`my_notification_overlay.xml` 的範例：**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

如您所見，hello 重疊檢視識別項是比 hello 標準一個不同的。 很重要的是，每個配置要針對覆疊使用唯一識別碼。

**`my_notification_area.xml` 的範例：**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

如您所見，hello 通知區域中檢視識別項是比 hello 標準一個不同的。 很重要的是，每個配置要針對通知區域使用唯一識別碼。

類別目錄的這個簡單的範例可讓應用程式 （或在應用程式） 顯示在 hello 囉 」 畫面最上方的通知。 我們不會變更 hello 本身 hello 通知區域中所使用的標準識別碼。

如果您想要您有 tooredefine hello toochange`EngagementDefaultNotifier.prepareInAppArea`方法。 建議在 hello 技術文件和 hello 原始程式碼 toolook`EngagementNotifier`和`EngagementDefaultNotifier`如果您要的進階自訂層級。

##### <a name="system-notifications"></a>系統通知
藉由擴充`EngagementDefaultNotifier`，您可以覆寫`onNotificationPrepared`tooalter hello 通知已準備好 hello 預設實作。

例如：

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

這個範例會顯示為 進行中的事件時 hello 「 進行中 」 類別使用內容的系統通知。

如果您想 toobuild hello`Notification`物件從頭情況下，您可以傳回`false`toohello 方法，並呼叫`notify`自行在 hello `NotificationManager`。 在此情況下很重要，保留`contentIntent`、 `deleteIntent` hello 所使用的通知識別碼和`EngagementReachReceiver`。

以下是這類實作的正確範例：

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>僅通知的公告
hello 管理 hello 按一下通知，可以藉由覆寫自訂唯一公告`EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared`toomodify hello 備妥`Intent`。 使用此方法可讓您 tootune hello 旗標輕鬆。

例如 tooadd hello`SINGLE_TOP`旗標：

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

針對舊版 Engagement 使用者，請注意，而不進行動作的系統通知 URL 現在會啟動 hello 應用程式是否它是在背景中，因此可以與通知動作 URL 沒有呼叫這個方法。 自訂 hello 意圖時，您應該考慮的。

您也可以從頭實作 `EngagementNotifier.executeNotifAnnouncementAction` 。

##### <a name="notification-life-cycle"></a>通知生命週期
使用 hello 預設分類，某些存留週期方法會呼叫在 hello`EngagementReachInteractiveContent`物件 tooreport 統計資料和更新 hello 活動狀態：

* 當 hello 通知會顯示在應用程式，或將放在 hello 狀態列時，hello`displayNotification`方法呼叫 （它會報告統計資料） 所`EngagementReachAgent`如果`handleNotification`傳回`true`。
* 如果關閉 hello 通知，hello`exitNotification`呼叫方法時，統計資料會報告，並可立即處理下一個活動。
* 如果按一下 hello 通知，`actionNotification`是呼叫，統計資料會報告與相關聯的 hello 意圖會啟動。

如果您實作`EngagementNotifier`略過 hello 預設行為，您自己有 toocall 這些生命週期的方法。 hello 遵循範例將說明某些情況下，會在略過 hello 預設行為：

* 您不延伸 `EngagementDefaultNotifier`，例如從頭開始實作類別處理。
* 系統通知您已覆寫 hello`onNotificationPrepared`您修改`contentIntent`或`deleteIntent`在 hello`Notification`物件。
* 應用程式內通知您已覆寫`prepareInAppArea`，至少是確定 toomap `actionNotification` tooone U.I 控制項。

> [!NOTE]
> 如果`handleNotification`擲回例外狀況，hello 內容會刪除與`dropContent`呼叫。 這報告在統計資料中，並且立即可以處理接下來的活動。
> 
> 

### <a name="announcements-and-polls"></a>宣告和輪詢
#### <a name="layouts"></a>版面配置
您可以修改 hello `engagement_text_announcement.xml`，`engagement_web_announcement.xml`和`engagement_poll.xml`toocustomize 文字公告、 web 宣告與輪詢檔案。

這些檔案共用 hello 標題區域與 hello 按鈕區域的兩個一般配置。 hello 標題 hello 配置有`engagement_content_title.xml`和使用 hello 得名 drawable hello 背景檔案。 hello hello 動作和 [結束] 按鈕的配置是`engagement_button_bar.xml`和使用 hello 得名 drawable hello 背景檔案。

在投票，hello 問題版面配置和其選項動態膨脹使用多次 hello `engagement_question.xml` hello 問題與 hello 的版面配置檔`engagement_choice.xml`hello 選擇的檔案。

#### <a name="categories"></a>類別
##### <a name="alternate-layouts"></a>替代版面配置
通知，如同 hello 活動的類別可以是您的宣告與輪詢使用的 toohave 替代配置。

例如，toocreate 文字公告的類別，您可以擴充`EngagementTextAnnouncementActivity`參照該 hello`AndroidManifest.xml`檔案：

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

請注意在 hello 意圖該 hello 類別目錄會使用篩選器與 hello 預設公告活動 toomake hello 差異。

hello Reach SDK 使用 hello 意圖系統 tooresolve hello 正確的活動特定分類，則會回到上 hello 預設分類如果 hello 解析失敗。

就會有 tooimplement `MyCustomTextAnnouncementActivity`，如果您只想 toochange hello 配置 （但保留 hello 相同檢視識別項），您只在 toodefine hello 類別，例如下列範例中的 hello:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

只要取代文字公告 tooreplace hello 預設分類`android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"`由您的實作。

可以以類似的方式自訂 web 公告與輪詢。

Web 公告，您可以擴充`EngagementWebAnnouncementActivity`並宣告您的活動 hello`AndroidManifest.xml`如 hello 下列範例所示：

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

針對輪詢您可以延伸`EngagementPollActivity`並宣告您在 hello`AndroidManifest.xml`如 hello 下列範例所示：

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>從頭實作
您可以通知 （與輪詢） 活動的實作類別，而不用擴充一個 hello`Engagement*Activity`類別所提供 hello Reach SDK。 這非常有用，例如是否要讓 toodefine 未使用相同檢視的 hello hello 標準配置的配置。

類似的進階的通知自訂建議 toolook 在 hello 標準實作 hello 原始程式碼。

以下是一些事情 tookeep 記住： 觸達將會啟動 hello 活動特定的意圖 （對應 toohello 意圖篩選），再加上額外的參數也就是 hello 內容識別項。

tooretrieve hello 內容物件會包含您指定當建立 hello 活動 hello 網站上您的 hello 欄位可以執行下列動作：

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

統計資料，則應該報告 hello 內容會顯示在 hello`onResume`事件：

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

然後，請不要忘記 toocall`actionContent(this)`或`exitContent(this)`hello 內容物件之前先發掘背景的 hello 活動上。

如果您不可以呼叫`actionContent`或`exitContent`、 統計資料將不會傳送 （也就是在 hello 活動上的任何分析） 和多個重要的是，hello hello 應用程式處理序重新啟動之前，不會通知下一個活動。

方向或其他組態變更可以讓 hello 程式碼很難解釋 toodetermine 是否 hello 活動便會進入背景，或不、 hello 標準實作可確定 hello 內容報告為離開如果 hello 使用者離開 hello 活動 （無論是由按下`HOME`或`BACK`) 但不是如果 hello 方向變更。

以下是 hello 值得注意的 hello 實作：

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

如您所見，如果您呼叫`actionContent(this)`然後完成 hello 活動`exitContent(this)`影響的情況下可以安全地呼叫。

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon 裝置傳訊]:https://developer.amazon.com/sdk/adm.html
