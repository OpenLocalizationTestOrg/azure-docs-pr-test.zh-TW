---
title: "開始使用適用於 Android 應用程式的 Azure 通知中樞和 Firebase 雲端通訊 | Microsoft Docs"
description: "在本教學課程中，您會了解如何使用 Azure 通知中樞和 Firebase 雲端通訊，將通知推播到 Android 裝置。"
services: notification-hubs
documentationcenter: android
keywords: "推播通知,推播通知,android 推播通知,fcm,firebase 雲端通訊"
author: jwhitedev
manager: kpiteira
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 12/22/2017
ms.author: jawh
ms.openlocfilehash: 2cac554be145c3bb9ec2c71ef893bba947104a2d
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="get-started-with-azure-notification-hubs-for-android-apps-and-firebase-cloud-messaging"></a>開始使用適用於 Android 應用程式的 Azure 通知中樞和 Firebase 雲端通訊
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!IMPORTANT]
> 本文示範使用 Google Firebase 雲端通訊 (FCM) 的推播通知。 如果您仍然使用 Google 雲端通訊 (GCM)，請參閱 [使用 Azure 通知中樞和 GCM 將推播通知傳送至 Android](notification-hubs-android-push-notification-google-gcm-get-started.md)。
> 
> 

本教學課程說明如何使用 Azure 通知中樞和 Firebase 雲端通訊，將推播通知傳送到 Android 應用程式。 在本教學課程中，您會建立空白的 Android 應用程式，其可使用 Firebase 雲端通訊 (FCM) 接收推播通知。

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

您可以從 [此處](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase)的 GitHub 下載本教學課程的完整程式碼。

## <a name="prerequisites"></a>先決條件
> [!IMPORTANT]
> 若要完成此教學課程，您必須具備有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)。
> 
> 

* 除了上述的作用中 Azure 帳戶，本教學課程需要最新版的 [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)。
* 適用於 Firebase 雲端通訊的 Android 2.3 或更新版本。
* 適用於 Firebase 雲端通訊的 Google Repository 修訂版本 27 或更新版本。
* 適用於 Firebase 雲端通訊的 Google Play Services 9.0.2 或更新版本。
* 完成本教學課程是 Android app 所有其他通知中樞教學課程的先決條件。

## <a name="create-a-new-android-studio-project"></a>建立新的 Android Studio 專案
1. 在 Android Studio 中，啟動新的 Android Studio 專案。
   
    ![Android Studio - 新增專案](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. 選擇 [電話和平板電腦] 板型規格和您要支援的 [Minimum SDK]。 然後按 [下一步] 。
   
    ![Android Studio - 專案建立工作流程](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. 為主要活動選擇 [空白活動]，並按 [下一步]，然後按一下 [完成]。

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>建立支援 Firebase 雲端通訊的專案
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>設定新的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. 在 [Notification Services] 下，選取 [Google (GCM)]。 輸入您先前從 [Firebase 主控台](https://firebase.google.com/console/)複製的 FCM 伺服器金鑰，然後按一下 [儲存]。

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

現在已將您的通知中樞設定成使用 Firebase 雲端通訊，而且您已擁有可用來註冊應用程式以接收和傳送推播通知的連接字串。

## <a id="connecting-app"></a>將您的應用程式連接到通知中樞
### <a name="add-google-play-services-to-the-project"></a>新增 Google Play 服務至專案
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>新增 Azure 通知中樞程式庫
1. 在 **app** 的 `Build.Gradle` 檔案中，於 **dependencies** 區段中新增下列數行。
   
    ```java
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

2. 加入下列儲存機制到 **dependencies** 一節之後。
   
    ```java
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }
    ```

### <a name="updating-the-androidmanifestxml"></a>更新 AndroidManifest.xml。
1. 若要支援 FCM，您必須在程式碼中實作執行個體識別碼接聽程式服務，以便使用 [Google 的 FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId) 來[取得註冊權杖](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register)。 在本教學課程中，類別名稱為 `MyInstanceIDService`。 
   
    將下列服務定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。 
   
    ```xml
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
    ```

2. 一旦從 FirebaseInstanceId API 收到 FCM 註冊權杖，您會用它來[向 Azure 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。 您會使用名為 `RegistrationIntentService` 的 `IntentService` 在背景支援此註冊。 此服務也會負責重新整理 FCM 註冊權杖。
   
    將下列服務定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。 
   
    ```xml
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
    ```

3. 您也必須定義要接收通知的接收者。 將下列接收者定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。 以 `AndroidManifest.xml` 檔案頂端顯示的實際套件名稱取代 `<your package>` 預留位置。

    ```xml
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
    ```

4. 在 `</application>` 標籤下面新增下列必要的 FCM 相關權限。 請務必以 `AndroidManifest.xml` 檔案頂端顯示的封裝名稱取代 `<your package>`。
   
    如需這些權限的詳細資訊，請參閱[設定適用於 Android 的 GCM 用戶端應用程式](https://developers.google.com/cloud-messaging/android/client#manifest)和[將適用於 Android 的 GCM 用戶端應用程式移轉至 Firebase 雲端通訊](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm)。
   
    ```xml
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    ```

### <a name="adding-code"></a>加入程式碼
1. 在 [專案檢視] 中，展開 [app] > [src] > [main] > [java]。 以滑鼠右鍵按一下 **java** 底下您的套件資料夾，並按一下 [新增]，然後按一下 [Java 類別]。 新增名為 `NotificationSettings` 的新類別。 
   
    ![Android Studio - 新增 Java 類別](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    請務必在 `NotificationSettings` 類別的下列程式碼中更新這三個預留位置：
   
   * **SenderId**︰您稍早在 [Firebase 主控台](https://firebase.google.com/console/)專案設定的 [雲端通訊] 索引標籤中取得的寄件者識別碼。
   * **HubListenConnectionString**：中樞的 **DefaultListenAccessSignature** 連接字串。 在 [Azure 入口網站]上的中樞內按一下 [存取原則]，即可複製該連接字串。
   * **HubName**︰使用出現在 [Azure 入口網站]中樞刀鋒視窗中的通知中樞名稱。
     
     `NotificationSettings` 程式碼︰
     
    ```java
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
    ```

2. 使用上述步驟，加入另一個名為 `MyInstanceIDService` 的新類別。 這是您的執行個體識別碼接聽程式服務實作。
   
    此類別的程式碼會呼叫 `IntentService` 以在背景[重新整理 FCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)。
   
    ```java
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };
    ```

1. 將另一個新類別新增至名為 `RegistrationIntentService`的專案。 這是您的 `IntentService` 實作，可處理[重新整理 FCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)和[向通知中樞註冊](notification-hubs-push-notification-registration-management.md)。
   
    針對此類別使用下列程式碼。
   
    ```java
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration ID that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
    ```

2. 在 `MainActivity` 類別中，在類別宣告上面新增下列 `import` 陳述式。
   
    ```java
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
    ```

3. 在類別頂端新增下列 Private 成員。 您會使用這些成員來[檢查 Google 所建議的 Google Play 服務可用性](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)。
   
    ```java
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
    ```

4. 在 `MainActivity` 類別中，將下列方法新增至 Google Play 服務的可用性。 
   
    ```java
        /**
        * Check the device to make sure it has the Google Play Services APK. If
        * it doesn't, display a dialog that allows users to download the APK from
        * the Google Play Store or enable it in the device's system settings.
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
    ```

5. 在 `MainActivity` 類別中加入下列程式碼，以在呼叫 `IntentService` 之前檢查 Google Play 服務，進而取得 FCM 註冊權杖並向通知中樞註冊。
   
    ```java
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
    ```

6. 在 `MainActivity` 類別的 `OnCreate` 方法中，加入下列程式碼以便在活動建立時開始註冊程序。
   
    ```java
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
    ```

7. 為了驗證應用程式狀態及報告您的應用程式狀態，請將上述其他方法新增至 `MainActivity`。
   
    ```java
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
    ```

8. `ToastNotify` 方法會使用 *"Hello World"* `TextView` 控制項持續在應用程式中報告狀態和通知。 在 activity_main.xml 配置中，為該控制項加入下列識別碼。
   
    ```java
       android:id="@+id/text_hello"
    ```

9. 接下來，您會為 AndroidManifest.xml 中所定義的接收者新增子類別。 將另一個新類別新增至名為 `MyHandler`的專案。
10. 在 `MyHandler.java` 頂端新增下列 import 陳述式：
    
    ```java
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
    ```

11. 在 `MyHandler` 類別中新增下列程式碼，使其成為 `com.microsoft.windowsazure.notifications.NotificationsHandler` 的子類別。
    
    此程式碼會覆寫 `OnReceive` 方法，以便讓處理常式報告所收到的通知。 處理常式也會使用 `sendNotification()` 方法，將推播通知傳送給 Android 通知管理員。 當應用程式不在執行中並收到通知時，應該執行 `sendNotification()` 方法。
    
    ```java
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
    ```

12. 在 Android Studio 的功能表列上，按一下 [建置] > [重新建置專案]，確保您的程式碼中未沒有任何錯誤。
13. 在您的裝置上執行應用程式，並確認該應用程式已向通知中心註冊成功。 
    
    > [!NOTE]
    > 註冊可能會在初始啟動時失敗，直到呼叫執行個體識別碼服務的 `onTokenRefresh()` 方法為止。 重新整理作業應該會起始向通知中樞註冊的作業並且會成功。
    > 
    > 

## <a name="sending-push-notifications"></a>傳送推播通知
透過 [Azure 入口網站]傳送推播通知，即可在您的應用程式中測試接收推播通知 - 尋找中樞中的 [疑難排解] 區段，如下所示。

![Azure 通知中樞 - 測試傳送](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]


## <a name="testing-your-app"></a>測試應用程式
#### <a name="push-notifications-in-the-emulator"></a>在模擬器中測試推播通知
如果您要在模擬器中測試推播通知，請確定您的模擬器映像支援您為應用程式選擇的 Google API 層級。 如果您的映像不支援原生 Google API，最後會發生 **SERVICE\_NOT\_AVAILABLE** 例外狀況。

除此之外，請確定已將 Google 帳戶新增至執行中模擬器的 [設定] > [帳戶] 之下。 否則，嘗試向 GCM 註冊可能會導致 **AUTHENTICATION\_FAILED** 例外狀況。

#### <a name="running-the-application"></a>執行應用程式
1. 執行 app，並注意已回報註冊成功的註冊識別碼。
   
    ![在 Android 上測試 - 通道註冊](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. 輸入通知訊息，以傳送給已向中心註冊的所有 Android 裝置。
   
    ![在 Android 上測試 - 傳送訊息](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. 按 [ **傳送通知**]。 任何執行應用程式的裝置都會顯示含推播通知訊息的 `AlertDialog` 執行個體。 未執行應用程式但先前已註冊推播通知的裝置，將會收到 Android 通知管理員的通知。 從左上角往下撥動，即可檢視通知。
   
    ![在 Android 上測試 - 通知](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>後續步驟
我們建議以 [使用通知中樞將通知推播給使用者] 教學課程做為下一個步驟。 它會示範如何使用標籤來鎖定特定使用者，以從 ASP.NET 後端傳送通知。


如果您想要依興趣群組分隔使用者，請查看 [使用通知中樞傳送即時新聞] 教學課程。

若要深入了解通知中樞的一般資訊，請參閱 [通知中樞指引]。

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[通知中樞指引]: notification-hubs-push-notification-overview.md
[使用通知中樞將通知推播給使用者]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[使用通知中樞傳送即時新聞]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure 入口網站]: https://portal.azure.com
