---
title: "aaaGet Kindle 應用程式啟動了 Azure 通知中心 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooa Kindle 應用程式。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>開始使用適用於 Kindle 應用程式的通知中樞
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa Kindle 應用程式。
您將使用 Amazon 裝置傳訊 (ADM)，建立可接收推播通知的空白 Kindle app。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* 收到 hello hello （我們假設您將使用 Eclipse） 的 Android SDK <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 的站台</a>。
* 中的 hello 步驟<a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">工作開發環境上設定</a>tooset 適用於 Kindle 開發環境。

## <a name="add-a-new-app-toohello-developer-portal"></a>加入新的應用程式 toohello 開發人員入口網站
1. 首先，建立應用程式在 hello [Amazon 開發人員入口網站]。
   
    ![][0]
2. 複製 hello**應用程式金鑰**。
   
    ![][1]
3. 在 hello 入口網站按一下 [hello 應用程式的名稱，然後按一下hello**裝置傳訊**] 索引標籤。
   
    ![][2]
4. 按一下 [建立新的安全性設定檔]，然後建立新的安全性設定檔 (例如 **TestAdm 安全性設定檔**)。 然後按一下 [儲存] 。
   
    ![][3]
5. 按一下**安全性設定檔**tooview hello 安全性您剛建立設定檔。 複製 hello**用戶端識別碼**和**用戶端密碼**值供日後使用。
   
    ![][4]

## <a name="create-an-api-key"></a>建立 API 金鑰
1. 以系統管理員權限開啟命令提示字元。
2. 瀏覽 toohello Android SDK 資料夾。
3. 輸入下列命令的 hello:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Hello **keystore**密碼、 型別**android**。
5. 複製 hello **MD5**指紋。
6. 在 hello 開發人員入口網站，在 hello**傳訊**索引標籤上，按一下  **Android/Kindle**並輸入您的應用程式的 hello 套件 hello 名稱 (比方說， **com.sample.notificationhubtest**)和 hello **MD5**值，然後按一下**產生 API 金鑰**。

## <a name="add-credentials-toohello-hub"></a>新增認證 toohello 中樞
在 [hello 入口網站中，新增 hello 用戶端密碼和用戶端識別碼 toohello**設定**通知中樞] 索引標籤。

## <a name="set-up-your-application"></a>設定您的應用程式
> [!NOTE]
> 建立應用程式時，至少應使用 API 層級 17。
> 
> 

加入 hello ADM 文件庫 tooyour Eclipse 專案：

1. tooobtain hello ADM 程式庫[下載 hello SDK]。 Hello SDK zip 檔案解壓縮。
2. 在 Eclipse 中，以滑鼠右鍵按一下您的專案，然後按一下屬性 。 選取**Java 組建路徑**hello 左、，然後選取 hello 上 * * 程式庫 * * 在 hello 最上方的索引標籤。 按一下**新增外部 Jar**，和選取 hello 檔案`\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar`從 hello 目錄，您可以在其中解壓縮 hello Amazon SDK。
3. 下載 hello 通知中樞 Android SDK （連結）。
4. 解壓縮 hello 封裝，然後將拖曳 hello 檔案`notification-hubs-sdk.jar`到 hello`libs`在 Eclipse 中的資料夾。

編輯您的應用程式資訊清單 toosupport ADM:

1. 新增 hello 根資訊清單項目中的 hello Amazon 命名空間：

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. 將權限新增為 hello hello 資訊清單項目下的第一個項目。 替代**[您的封裝名稱]**與 hello 封裝，您使用 toocreate 您的應用程式。
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. 插入 hello hello hello 應用程式項目的第一個子系為下列項目。 請記住 toosubstitute **[您的服務名稱]** hello 名稱，為您建立 hello 下一節 （包括 hello 封裝），並取代您 ADM 訊息處理常式**[您的封裝名稱]**以 hello您用來建立您的應用程式封裝名稱。
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>建立您的 ADM 訊息處理常式
1. 建立新的類別繼承自`com.amazon.device.messaging.ADMMessageHandlerBase`並將其命名`MyADMMessageHandler`hello 遵循圖所示：
   
    ![][6]
2. 新增下列 hello`import`陳述式：
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. 新增下列程式碼，您所建立的 hello 類別中的 hello。 請記住 toosubstitute hello 中樞名稱和連接字串 （待命）：
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. 新增下列程式碼 toohello hello`OnMessage()`方法：
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. 新增下列程式碼 toohello hello`OnRegistered`方法：
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. 新增下列程式碼 toohello hello`OnUnregistered`方法：
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. 在 hello`MainActivity`方法，加入下列 import 陳述式的 hello:
   
        import com.amazon.device.messaging.ADM;
8. 新增下列程式碼結尾 hello hello hello`OnCreate`方法：
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>加入您的 API 金鑰 tooyour 應用程式
1. 在 Eclipse 中，建立新的檔案命名為**api_key.txt** hello 目錄資產，您的專案中。
2. 開啟 hello 檔案，並複製 hello API 金鑰，您在 hello Amazon 開發人員入口網站中產生。

## <a name="run-hello-app"></a>執行 hello 應用程式
1. 啟動 hello 模擬器。
2. 從 hello 頂端向撥動 hello 模擬器中，按一下 **設定**，然後按一下**我的帳戶**並使用有效的 Amazon 帳戶註冊。
3. 在 Eclipse 中，執行 hello 應用程式。

> [!NOTE]
> 如果發生問題，請檢查 hello 時間 hello 模擬器 （或裝置）。 hello 時間值必須是正確的。 toochange hello hello Kindle 模擬器時，您可以執行下列命令，從您的 Android SDK 平台工具目錄 hello:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>傳送訊息
toosend 使用.NET 訊息：

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon 開發人員入口網站]: https://developer.amazon.com/home.html
[下載 hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
