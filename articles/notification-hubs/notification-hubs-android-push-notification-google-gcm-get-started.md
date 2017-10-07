---
title: "與 Azure 通知中心 aaaSending 推播通知 tooAndroid |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooAndroid 裝置。"
services: notification-hubs
documentationcenter: android
keywords: "推播通知,推播通知,android 推播通知"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>使用 Azure 通知中樞傳送推播通知 tooAndroid
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!IMPORTANT]
> 本主題示範使用 Google 雲端通訊 (GCM) 的推播通知。 如果您使用 Google Firebase 雲端傳訊 (FCM)，請參閱[FCM 與 Azure 通知中樞傳送推播通知 tooAndroid](notification-hubs-android-push-notification-google-fcm-get-started.md)。
> 
> 

本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooan Android 應用程式。
您將建立可使用 Google Cloud Messaging (GCM) 接收推播通知的空白 Android app。

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

此教學課程中的 hello 完成程式碼可以從 GitHub 下載[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted)。

## <a name="prerequisites"></a>必要條件
> [!IMPORTANT]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)。
> 
> 

此外 tooan 有效的 Azure 帳戶先前所述，本教學課程只需要 hello 最新版本的[Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)。

完成本教學課程是 Android app 所有其他通知中樞教學課程的先決條件。

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>建立支援 Google 雲端通訊的專案
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>設定新的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   在 hello**設定**刀鋒視窗中，選取**Notification Services**然後**Google (GCM)**。 輸入 hello API 金鑰，然後按一下 **儲存**。

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

您的通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 的連接字串 tooboth 註冊您的應用程式 tooreceive 及傳送推播通知。

## <a id="connecting-app"></a>連接您的應用程式 toohello 通知中樞
### <a name="create-a-new-android-project"></a>建立新的 Android 專案
1. 在 Android Studio 中，啟動新的 Android Studio 專案。
   
   ![Android Studio - 新增專案][13]
2. 選擇 hello**電話和平板電腦**構成要素和 hello**最低 SDK**想 toosupport。 然後按 [下一步] 。
   
   ![Android Studio - 專案建立工作流程][14]
3. 選擇**空的活動**hello 主要活動，請按一下**下一步**，然後按一下**完成**。

### <a name="add-google-play-services-toohello-project"></a>將 Google Play 服務 toohello 專案
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>新增 Azure 通知中樞程式庫
1. 在 hello`Build.Gradle`檔案 hello**應用程式**，加入下列行 hello hello**相依性**> 一節。
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. 新增下列儲存機制之後 hello hello**相依性**> 一節。
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>正在更新 hello AndroidManifest.xml。
1. toosupport GCM，我們必須在用過的程式碼中實作的執行個體識別碼的接聽程式服務[取得註冊權杖](https://developers.google.com/cloud-messaging/android/client#sample-register)使用[Google 的執行個體識別碼 API](https://developers.google.com/instance-id/)。 在本教學課程中，我們會命名 hello 類別`MyInstanceIDService`。 
   
    新增下列服務定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。 取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. 一旦我們有我們 GCM 註冊語彙基元收到 hello 執行個體識別碼的 API，將會使用此太[hello Azure 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。 我們將在背景中使用 hello 支援此註冊`IntentService`名為`RegistrationIntentService`。 此服務也會負責 [重新整理我們的 GCM 註冊權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)。
   
    新增下列服務定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。 取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. 我們也會定義接收者 tooreceive 通知。 新增下列收件者定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。 取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. 新增下列必要的 GCM hello 相關權限下 hello`</application>`標記。 請確定 tooreplace`<your package>`與 hello 套件名稱顯示在 hello hello 頂端`AndroidManifest.xml`檔案。
   
    如需這些權限的詳細資訊，請參閱 [設定適用於 Android 的 GCM 用戶端應用程式](https://developers.google.com/cloud-messaging/android/client#manifest)。
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>加入程式碼
1. 在 hello 專案檢視，展開**應用程式** > **src** > **主要** > **java**。 以滑鼠右鍵按一下 **java** 底下您的套件資料夾，並按一下 新增，然後按一下Java 類別。 新增名為 `NotificationSettings` 的新類別。 
   
    ![Android Studio - 新增 Java 類別][6]
   
    請確定 tooupdate hello 這些 hello 遵循 hello 的程式碼中的三個預留位置`NotificationSettings`類別：
   
   * **SenderId**: hello 您稍早在 hello 中取得的專案數目[Google 雲端主控台](http://cloud.google.com/console)。
   * **HubListenConnectionString**: hello **DefaultListenAccessSignature**中樞連接字串。 您可以將該連接字串複製按一下**存取原則**上 hello**設定**刀鋒視窗上 hello 中樞[Azure 入口網站]。
   * **HubName**: hello 的 hello 中樞 刀鋒視窗中會出現在通知中樞的使用 hello 名稱[Azure 入口網站]。
     
     `NotificationSettings` 程式碼︰
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. 使用上述的 hello 步驟，加入另一個名為的新類別`MyInstanceIDService`。 這會是我們的執行個體識別碼接聽程式服務實作。
   
    此類別的 hello 程式碼會呼叫我們`IntentService`太[重新整理 hello GCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)hello 背景。
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. 加入另一個新的類別 tooyour 專案命名， `RegistrationIntentService`。 這會是 hello 實作我們`IntentService`處理[重新整理 hello GCM 語彙基元](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)和[hello 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。
   
    使用下列程式碼，這個類別的 hello。
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. 在您`MainActivity`類別中，加入下列 hello `import` hello 上面的陳述式的類別宣告。
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. 加入下列私用成員在 hello hello 類別頂端的 hello。 我們會使用這些[Google 依照建議，請檢查 Google Play 服務的 hello 可用性](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)。
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. 在您`MainActivity`類別中，新增下列方法 toohello 可用性的 Google Play 服務的 hello。 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. 在您`MainActivity`類別中，加入下列程式碼會檢查之前先呼叫 Google Play 服務的 hello 您`IntentService`tooget 您 GCM 註冊語彙基元及與您的通知中樞的註冊。
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. 在 hello `OnCreate` hello 方法`MainActivity`類別中，新增 hello 建立活動時，下列程式碼 toostart hello 註冊程序。
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. 新增這些其他方法 toohello `MainActivity` tooverify prb： 應用程式中的發生應用程式狀態及報告狀態。
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. hello`ToastNotify`方法會使用 hello *"Hello World"* `TextView`控制 tooreport 狀態和持續中 hello 應用程式的通知。 在 activity_main.xml 配置中，加入下列控制項的識別碼 hello。
   
       android:id="@+id/text_hello"
9. 接下來，我們將我們我們 hello AndroidManifest.xml 中定義的收件者加入子類別。 加入另一個新的類別 tooyour 專案名為`MyHandler`。
10. 加入下列 import 陳述式在 hello 最上方的 hello `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. 新增下列程式碼 hello hello`MyHandler`讓它的子類別的類別`com.microsoft.windowsazure.notifications.NotificationsHandler`。
    
    此程式碼會覆寫 hello`OnReceive`方法，所以 hello 處理常式會報告所接收的通知。 hello 處理常式也會將傳送嗨推播通知 toohello Android 的通知管理員使用 hello`sendNotification()`方法。 hello`sendNotification()`方法應該在執行時收到通知，而且 hello 應用程式未執行。
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. 在 Android Studio 中 hello 功能表列上，按一下 **建置** > **重建專案**toomake 確定任何錯誤會出現在您的程式碼。

## <a name="sending-push-notifications"></a>傳送推播通知
您可以測試應用程式中接收推播通知傳送嗨透過[Azure 入口網站]-尋找 hello**疑難排解**區段在 hello 中樞刀鋒視窗中，如下所示。

![Azure 通知中樞 - 測試傳送](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>（選擇性）直接從 hello 應用程式中傳送推播通知
一般來說，您會使用後端伺服器傳送通知。 在某些情況下，您可能想直接從 hello 用戶端應用程式的 toobe 無法 toosend 推播通知。 本章節將說明如何 toosend 通知 hello 使用從用戶端 hello [Azure 通知中樞 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)。

1. 在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [layout]。 開啟 hello`activity_main.xml`配置檔案，然後按一下 hello**文字**hello 檔案 tooupdate hello 文字內容索引標籤上。 它與 hello 的下列程式碼將新的更新`Button`和`EditText`控制項傳送推播通知訊息 toohello 通知中樞。 之前加入這個程式碼在 hello 下方`</RelativeLayout>`。
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. 在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [values]。 開啟 hello`strings.xml`檔案，然後加入新的 hello 所參考的 hello 字串值`Button`和`EditText`控制項。 之前加入下列底部 hello hello 檔案`</resources>`。
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. 在您`NotificationSetting.java`檔案中，新增下列設定 toohello hello`NotificationSettings`類別。
   
    更新`HubFullAccess`以 hello **DefaultFullSharedAccessSignature**中樞連接字串。 這個連接字串可以從 hello 複製[Azure 入口網站]按一下**存取原則**上 hello**設定**通知中樞的刀鋒視窗。
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. 在您`MainActivity.java`file、 add hello 下列`import`hello 上面的陳述式`MainActivity`類別。
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. 在您`MainActivity.java`檔案中加入下列成員在 hello hello 最上方的 hello`MainActivity`類別。    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. 您必須建立軟體存取簽章 (SaS) 權杖的 tooauthenticate POST 要求 toosend 訊息 tooyour 通知中樞。 這是藉由剖析 hello hello 連接字串中的索引鍵資料和 hello 中所述，然後建立 hello SaS 權杖[Common 概念](http://msdn.microsoft.com/library/azure/dn495627.aspx)REST API 參考。 下列程式碼的 hello 是範例實作。
   
    在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 tooparse 連接字串。
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. 在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 toocreate SaS 驗證權杖。
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. 在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 toohandle hello**傳送通知**按鈕按一下，然後傳送 hello 訊息 toohello 集線器使用 hello 內建的 REST API 的推播通知。
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>測試應用程式
#### <a name="push-notifications-in-hello-emulator"></a>Hello 模擬器中的推播通知
如果您想在模擬器 tootest 推播通知，請確定模擬器映像支援您選擇您的應用程式的 hello Google API 層級。 如果您的映像不支援原生的 Google Api，您會得到 hello**服務\_不\_可用**例外狀況。

此外 toohello 上述項目，確定您已加入執行模擬器，在您 Google 帳戶 tooyour**設定** > **帳戶**。 否則，GCM 與您嘗試 tooregister 可能導致 hello**驗證\_失敗**例外狀況。

#### <a name="running-hello-application"></a>執行 hello 應用程式
1. 執行 hello 應用程式，並注意 hello 註冊 ID 會報告成功註冊。
   
      ![在 Android 上測試 - 通道註冊][18]
2. 輸入通知訊息 toobe 傳送 tooall hello 集線器與已註冊的 Android 裝置。
   
      ![在 Android 上測試 - 傳送訊息][19]

3. 按 [ **傳送通知**]。 任何具有 hello 應用程式執行的裝置將會顯示`AlertDialog`與 hello 推播通知訊息的執行個體。 沒有 hello 應用程式執行，但先前註冊推播通知將會收到通知 hello Android 通知管理員中的裝置。 可以檢視這些撥動往下從 hello 左上角。
   
      ![在 Android 上測試 - 通知][21]

## <a name="next-steps"></a>後續步驟
我們建議 hello[使用通知中樞 toopush 通知 toousers] hello 下一個步驟的教學課程。 它會顯示如何從 ASP.NET 後端使用 toosend 通知標記 tootarget 特定使用者。

如果您希望 toosegment 使用者感興趣的群組，請參閱 hello[使用通知中樞 toosend 最新消息]教學課程。

toolearn 通知中樞的相關詳細資訊，請參閱我們[通知中樞指引]。

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[使用通知中樞 toopush 通知 toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure 入口網站]: https://portal.azure.com
