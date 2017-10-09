---
title: "aaaGet 開始使用 Azure 通知中心使用百度 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooAndroid 裝置使用百度。"
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>透過百度開始使用通知中樞
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
百度雲端推播是中文的雲端服務，您可以使用 toosend 推播通知 toomobile 裝置。 這個服務是用於中國，其中傳遞 tooAndroid 很複雜，因為 hello 出現不同的應用程式存放區與推入的推播通知服務，除了 toohello 可用性的不是通常連接的 tooGCM (Google Android 裝置雲端傳訊）。

## <a name="prerequisites"></a>必要條件
本教學課程需要：

* Android SDK （我們假設您使用 Eclipse），您可以下載從 hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 的站台</a>
* [行動服務 Android SDK]
* [百度發送的 Android SDK]

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F)。
> 
> 

## <a name="create-a-baidu-account"></a>建立百度帳戶
toouse 百度，您必須在百度帳戶。 如果您已經有一個，登入 toohello[百度入口網站]並略過 toohello 下一個步驟。 否則，請參閱如何在下列指示的 hello toocreate 百度帳戶。  

1. 移 toohello[百度入口網站]按一下 hello**登录**(**登入**) 連結。 按一下**立即注册**toostart hello 帳戶註冊程序。
   
   ![][1]
2. 輸入所需的 hello 詳細資料 — 電話/電子郵件地址、 密碼和驗證程式碼，按一下 **註冊**。
   
   ![][2]
3. 您將會收到電子郵件 toohello 電子郵件地址，您輸入連結 tooactivate 百度帳戶。
   
   ![][3]
4. 登入 tooyour 電子郵件帳戶，開啟 hello 百度啟用郵件，然後按一下 hello 啟用連結 tooactivate 百度帳戶。
   
   ![][4]

一旦您擁有已啟用的百度帳戶，登入 toohello[百度入口網站]。

## <a name="register-as-a-baidu-developer"></a>註冊為百度開發人員
1. 一旦您登入 toohello[百度入口網站]，按一下 **更多 >>** (**詳細**)。
   
      ![][5]
2. Hello 中向下捲動**站长与开发者服务 （網站管理員和開發人員服務）**區段，然後按一下**百度开放云平台**(**百度開放雲平台**)。
   
      ![][6]
3. 在 hello 下一個頁面上，按一下 **开发者服务**(**開發人員服務**) hello 右上角。
   
      ![][7]
4. 在 hello 下一個頁面上，按一下 **注册开发者**(**註冊開發人員**) 從 hello hello 右上角的功能表。
   
      ![][8]
5. 輸入您的名稱、描述和可收到驗證簡訊的行動電話號碼，然後按一下送验证码 \(**傳送驗證碼**)。 國際電話號碼，您需要括號括住 tooenclose hello 國家/地區碼。 例如，如果是美國的電話號碼，則為 **(1)1234567890**。
   
      ![][9]
6. 您接著應該會收到一則簡訊驗證數 hello 下列範例所示：
   
      ![][10]
7. 輸入 hello 驗證數字中的 hello 訊息**验证码**(**確認碼**)。
8. 最後，完成 接受 hello 百度協議，然後按一下 hello 開發人員註冊**提交**(**送出**)。 您會看到下列頁面上成功完成註冊的 hello:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>建立百度雲端推播專案
建立百度雲端推播專案時，您會收到應用程式識別碼、API 金鑰和秘密金鑰。

1. 一旦您登入 toohello[百度入口網站]，按一下 **更多 >>** (**詳細**)。
   
      ![][5]
2. Hello 中向下捲動**站长与开发者服务**(**網站管理員和開發人員服務**) 區段，然後按一下**百度开放云平台**(**百度開放雲平台**)。
   
      ![][6]
3. 在 hello 下一個頁面上，按一下 **开发者服务**(**開發人員服務**) hello 右上角。
   
      ![][7]
4. 在 hello 下一個頁面上，按一下 **云推送**(**雲端推播**) 從 hello**云服务**(**雲端服務**) 一節。
   
      ![][12]
5. 一旦您已註冊的開發人員，您會看到**管理控制台**(**管理主控台**) 在 hello 上方的功能表。 按一下 [开发者服务管理] \(**開發人員服務管理**)。
   
      ![][13]
6. 在 hello 下一個頁面上，按一下 **创建工程**(**建立專案**)。
   
      ![][14]
7. 輸入應用程式名稱，然後按一下 [创建] \(**建立**)。
   
      ![][15]
8. 成功建立百度雲推送專案後，您會看到包含 **AppID**、**API 金鑰**與**祕密金鑰**的頁面。 記下的 hello API 金鑰與秘密金鑰，我們將在稍後使用。
   
      ![][16]
9. 按一下 設定推播通知的 hello 專案**云推送**(**雲端推播**) 在 hello 的左窗格。
   
      ![][31]
10. 在 hello 下一個頁面上，按一下 hello**推送设置**(**設定推送**) 按鈕。
    
    ![][32]  
11. 在 hello 組態頁面上，加入您將使用在 hello Android 專案中的 hello 封裝名稱**应用包名**(**應用程式封裝**) 欄位，，然後按一下**保存设置**(**儲存**)。  
    
    ![][33]

您會看到 hello**保存成功 ！** (**儲存成功！**\) 的訊息。

## <a name="configure-your-notification-hub"></a>設定您的通知中樞
1. 登入 toohello [Azure 傳統入口網站]，然後按一下 **+ 新增**在 hello 囉 」 畫面底部。
2. 依序按一下 應用程式服務、服務匯流排、通知中樞，然後按一下快速建立。
3. 提供名稱給您**通知中樞**，選取 hello**區域**和 hello**命名空間**此通知中樞將會建立，然後按一下 **建立新的通知中樞**。  
   
      ![][17]
4. 按一下您要在其中建立您的通知中樞的 hello 命名空間，然後按一下**通知中樞**hello 頂端。
   
      ![][18]
5. 選取 hello 通知中樞，您建立，然後按一下**設定**從 hello 上方的功能表。
   
      ![][19]
6. 捲動 toohello**百度通知設定**區段，然後輸入 hello API 金鑰及祕密金鑰，您先前取得的 hello 百度主控台百度雲端推入專案。 按一下 [儲存] 。
   
      ![][20]
7. 按一下 hello**儀表板**hello 通知中樞，hello 頂端索引標籤，然後按一下**檢視連接字串**。
   
      ![][21]
8. 請記下 hello **DefaultListenSharedAccessSignature**和**DefaultFullSharedAccessSignature**從 hello**存取連線資訊**視窗。
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>連接您的應用程式 toohello 通知中樞
1. 在 Eclipse ADT 中建立新的 Android 專案 ([檔案] > [新增] > [Android 應用程式專案])。
   
    ![][23]
2. 輸入**應用程式名稱**，並確保該 hello**最低所需的 SDK**版本設定得**API 16: Android 4.1**。
   
    ![][24]
3. 按一下**下一步**並繼續遵循 hello 精靈直到 hello**建立活動** 視窗隨即出現。 請確定**空白活動**已選取，最後選取**完成**toocreate 新的 Android 應用程式。
   
    ![][25]
4. 請確定該 hello**專案建置目標**已正確設定。
   
    ![][26]
5. 從 hello 下載 hello 通知-中樞-0.4.jar 檔案**檔案** 索引標籤的 hello[通知-中樞-Android-SDK 上 Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4)。 新增 hello 檔案 toohello**程式庫**資料夾您 Eclipse 專案，並重新整理 hello*程式庫*資料夾。
6. 下載並解壓縮 hello[百度發送的 Android SDK]，開啟 hello**程式庫**資料夾，然後再複製 hello **pushservice x.y.z** jar 檔案和 hello **armeabi** &  **mips**資料夾中 hello**程式庫**Android 應用程式資料夾。
7. 開啟 hello **AndroidManifest.xml**檔案的 Android 專案，並加入 hello hello 百度 SDK 所需的權限。
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. 新增 hello **android: name**屬性 tooyour**應用程式**中的項目**AndroidManifest.xml**，並將*yourprojectname* （適用於範例中， **com.example.BaiduTest**)。 請確定此專案名稱符合 hello 一個 hello 百度主控台中設定。
   
        <application android:name="yourprojectname.DemoApplication"
9. 新增下列 hello 應用程式項目內的組態之後 hello hello **。MainActivity**活動項目，取代*yourprojectname* (例如， **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. 加入新的類別稱為**ConfigurationSettings.java** toohello 專案。
    
     ![][28]
    
     ![][29]
11. 加入下列程式碼 tooit hello:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    設定 hello 值**API_KEY**什麼您擷取 hello 百度雲端專案從較舊版本，與**NotificationHubName**以您的通知中樞名稱，從 Azure 傳統入口網站的 hello 和**NotificationHubConnectionString** DefaultListenSharedAccessSignature hello Azure 傳統入口網站中使用。
12. 加入新的類別稱為**DemoApplication.java**，並加入下列程式碼 tooit hello:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. 加入另一個新的類別稱為 「 **MyPushMessageReceiver.java**，並加入下列程式碼 tooit hello。 它是控制代碼 hello hello 百度推入 server 從接收推播通知的 hello 類別。
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. 開啟**MainActivity.java**，並加入下列 toohello hello **onCreate**方法：
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. 開啟 hello 下列匯入在 hello 最上方的陳述式：
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>傳送通知 tooyour 應用程式
您可以快速測試您的應用程式中接收通知，傳送通知給 hello 以[Azure 入口網站](https://portal.azure.com/)使用 hello**傳送**按鈕在 hello 通知中樞內，hello 遵循畫面所示：

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

推播通知通常會以後端服務傳送，例如行動服務或使用相容程式庫的 ASP.NET。 如果文件庫不適用於您的後端中，您可以使用 hello REST API 直接 toosend 通知訊息。

在本教學課程中，我們會保持簡單，只示範測試用戶端應用程式透過傳送 hello.NET SDK 使用通知中心，而不是後端服務的主控台應用程式的通知。 我們建議 hello[使用通知中樞 toopush 通知 toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)教學課程為 hello 下一個步驟，從 ASP.NET 後端傳送通知。 不過，hello 下列方法可用來傳送通知：

* **REST 介面**： 您可以使用 hello 任何後端平台上支援通知[REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)。
* **Microsoft Azure 通知中樞.NET SDK**: hello for Visual Studio 的 Nuget 封裝管理員，在執行[Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。
* **Node.js**:[如何 toouse 通知中樞，從 Node.js](notification-hubs-nodejs-push-notification-tutorial.md)。
* **行動應用程式**： 如需如何 toosend 通知從 Azure App Service 行動應用程式後端整合通知中心，請參閱[新增推播通知 tooyour 行動裝置應用程式](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)。
* **Java / PHP**： 如需如何使用 toosend 通知 hello REST Api 的範例，請參閱 「 如何 toouse 來自 Java/PHP 的通知中心 」 ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。

## <a name="optional-send-notifications-from-a-net-console-app"></a>(選擇性) 從 .NET 主控台應用程式傳送通知。
在本節中，我們會說明如何使用.NET 主控台應用程式傳送通知。

1. 建立新的 Visual C# 主控台應用程式：
   
    ![][30]
2. 在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    這個指令會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. 開啟 hello 檔案**Program.cs**並加入 hello 下列 using 陳述式：
   
        using Microsoft.Azure.NotificationHubs;
4. 在您`Program`類別，加入下列方法 hello 並取代*DefaultFullSharedAccessSignatureSASConnectionString*和*NotificationHubName*您擁有 hello 值。
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. 新增下列幾行中的 hello 您**Main**方法：
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>測試應用程式
實際電話，只與此應用程式連接的 tootest hello 電話 tooyour 電腦使用 USB 纜線。 這個動作會載入到附加的 hello 電話應用程式。

此應用程式與 hello 模擬器，hello Eclipse 頂端工具列上，按一下 tootest**執行**，然後選取您的應用程式： hello 模擬器中，負載、 啟動和執行 hello 應用程式。

hello 應用程式會從 hello 百度推播通知服務擷取 hello 'userId' 和 'channelId'，並註冊與 hello 通知中樞。

toosend 測試通知，您可以使用 hello hello Azure 傳統入口網站的 [偵錯] 索引標籤。 如果您建立 hello for Visual Studio.NET 主控台應用程式，請按 hello F5 鍵在 Visual Studio toorun hello 應用程式中。 hello 應用程式傳送通知出現在您的裝置或模擬器 hello 上方的通知區域中。

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[行動服務 Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[百度發送的 Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[百度入口網站]: http://www.baidu.com/
