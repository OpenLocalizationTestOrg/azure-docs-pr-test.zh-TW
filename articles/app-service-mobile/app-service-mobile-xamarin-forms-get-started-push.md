---
title: "aaaAdd 推播通知 tooyour Xamarin.Forms 應用程式 |Microsoft 文件"
description: "了解如何 toouse Azure 服務 toosend 多平台推送通知 tooyour Xamarin.Forms 應用程式。"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>新增推播通知 tooyour Xamarin.Forms 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將推播通知 tooall hello 專案所產生 hello [Xamarin.Forms 快速入門](app-service-mobile-xamarin-forms-get-started.md)。 這表示每次將記錄插入推播通知會傳送 tooall 跨平台的用戶端。

如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。 如需詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

## <a name="prerequisites"></a>必要條件
若為 iOS，您需要 [Apple Developer Program 成員資格](https://developer.apple.com/programs/ios/)和實體 iOS 裝置。 hello [iOS 模擬器不支援推播通知](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)。

## <a name="configure-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>更新 hello 伺服器專案 toosend 推播通知
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>設定及執行 hello Android 專案 （選擇性）
完成這個區段 tooenable 的推播通知 hello Xamarin.Forms Droid 專案 for Android。

### <a name="enable-firebase-cloud-messaging-fcm"></a>啟用 Firebase 雲端傳訊 (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>使用 FCM 設定 hello 行動應用程式後端 toosend 推播要求
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>加入推播通知 toohello Android 專案
設有 FCM hello 的後端，您可以新增傳回碼的元件和 toohello 用戶端 tooregister FCM 與。 您也可以透過回行動應用程式結束，並且接收通知的 hello 與 Azure 通知中心的推播通知登錄。

1. 在 hello **Droid**專案中，以滑鼠右鍵按一下 hello**元件**資料夾，然後按一下**取得多元件...**.然後搜尋 hello **Google 雲端訊息用戶端**元件並將它加入 toohello 專案。 此元件支援 Xamarin Android 專案的推播通知。
2. 開啟 hello Weatherapp 專案檔，並加入下列陳述式在 hello hello 檔案最上方的 hello:

        using Gcm.Client;
3. 新增下列程式碼 toohello hello **OnCreate**太呼叫方法之後 hello**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. 加入新的 **CreateAndShowDialog** 協助程式方法，如下所示︰

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. 新增下列程式碼 toohello hello **MainActivity**類別：

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    這樣會公開 hello 目前**MainActivity**執行個體，因此我們可以在 hello 主要 UI 執行緒上執行。
6. 初始化 hello`instance`變數在 hello hello 開頭**OnCreate**方法，如下所示。

        // Set hello current instance of MainActivity.
        instance = this;
7. 加入新的類別檔案 toohello **Droid**專案名為`GcmService.cs`，並請確定 hello 下列**使用**陳述式都出現在 hello hello 檔案的頂端：

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. 新增下列在 hello hello 檔案最上方的權限要求之後 hello hello**使用**陳述式之前 hello**命名空間**宣告。

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. 新增下列類別定義 toohello 命名空間的 hello。

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > 以您先前記下的專案號碼取代 **<PROJECT_NUMBER>**。    
   >
   >
10. 取代空白 hello **GcmService**類別以下列程式碼，使用 hello 新廣播的接收者 hello:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. 新增下列程式碼 toohello hello **GcmService**類別。 這會覆寫 hello **OnRegistered**事件處理常式，而且會實作**註冊**方法。

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    請注意這段程式碼會使用 hello `messageParam` hello 範本註冊中的參數。
12. 新增下列程式碼會實作 hello **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    這會處理內送通知，並將它們傳送 toohello 通知管理員 toobe 顯示。
13. **GcmServiceBase**也需要 tooimplement hello **OnUnRegistered**和**OnError**處理常式方法，您可以完成這件事，如下所示：

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

現在，您要準備測試 hello Android 裝置上執行的應用程式中的推播通知，或 hello 模擬器。

### <a name="test-push-notifications-in-your-android-app"></a>在 Android 應用程式中測試推播通知
只有在您要在模擬器上測試時，才需要 hello 前兩個步驟。

1. 請確定您要部署 tooor 偵錯包含 Google Api 將設為 hello 目標，如下所示在 hello Android 虛擬裝置管理員 中的虛擬裝置上。
2. 按一下 新增 Google 帳戶 toohello Android 裝置**應用程式** > **設定** > **將帳戶加入**。 然後，遵循 hello 提示 tooadd 現有的 Google 帳戶 toohello 裝置或 toocreate 新建一個。
3. 在 Visual Studio 或 Xamarin Studio，以滑鼠右鍵按一下 hello **Droid**專案，然後按一下**設定為啟始專案**。
4. 按一下**執行**toobuild hello 專案，並啟動您的 Android 裝置或模擬器上的 hello 應用程式。
5. 在 hello 應用程式，請在類型的工作，，，然後按一下加號 hello (**+**) 圖示。
6. 確認在加入項目時收到通知。

## <a name="configure-and-run-hello-ios-project-optional"></a>設定及執行 hello iOS 專案 （選擇性）
這個區段可讓您執行使用適用於 iOS 裝置 hello Xamarin iOS 專案。 如果未使用 iOS 裝置，可以略過這一節。

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>APNS 設定 hello 通知中樞
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

接下來，您將在 Visual Studio 或 Xamarin Studio 來設定 hello iOS 的專案設定。

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>加入推播通知 tooyour iOS 應用程式
1. 在 hello **iOS**專案中，開啟 d 並新增下列陳述式 toohello hello 程式碼檔案最上方的 hello。

        using Newtonsoft.Json.Linq;
2. 在 hello **AppDelegate**類別中，加入 hello 的覆寫**RegisteredForRemoteNotifications**事件 tooregister 通知：

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. 在**AppDelegate**，也新增下列 hello 覆寫的 hello **DidReceiveRemoteNotification**事件處理常式：

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Hello 應用程式執行時，這個方法會處理內送通知。
4. 在 hello **AppDelegate**類別中，加入下列程式碼 toohello hello **FinishedLaunching**方法：

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    這能夠支援遠端通知，並要求推播註冊。

您的應用程式已更新的 toosupport 推播通知。

#### <a name="test-push-notifications-in-your-ios-app"></a>在 iOS 應用程式中測試推播通知
1. 以滑鼠右鍵按一下 hello iOS 專案，然後按一下**設定為啟始專案**。
2. 按 hello**執行**按鈕或**F5** toobuild hello 專案和啟動 hello 應用程式在 iOS 裝置中，Visual Studio 中。 然後按一下 **確定**tooaccept 推播通知。

   > [!NOTE]
   > 您必須明確地接受來自應用程式的推播通知。 此要求才會發生 hello hello 應用程式執行的第一次。
   >
   >
3. 在 hello 應用程式，請在類型的工作，，，然後按一下加號 hello (**+**) 圖示。
4. 確認通知接收，然後按一下**確定**toodismiss hello 通知。

## <a name="configure-and-run-windows-projects-optional"></a>設定和執行 Windows 專案 (選擇性)
這個區段可讓您執行 hello，Xamarin.Forms WinApp 和 WinPhone81 的專案，適用於 Windows 裝置。 這些步驟也支援通用 Windows 平台 (UWP) 專案。 如果未使用 Windows 裝置，可以略過這一節。

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>為 Windows 應用程式向 Windows 通知服務 (WNS) 註冊推播通知
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>WNS 設定 hello 通知中樞
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>新增推播通知 tooyour Windows 應用程式
1. 在 Visual Studio 中開啟**App.xaml.cs** windows 專案，然後新增下列陳述式的 hello。

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    取代`<your_TodoItemManager_portable_class_namespace>`hello 命名空間，而包含 hello 可攜式專案`TodoItemManager`類別。
2. 在 App.xaml.cs，加入 hello 下列**InitNotificationsAsync**方法：

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    這個方法可以取得 hello 推播通知通道，並註冊您的通知中樞範本 tooreceive 範本通知。 支援的範本通知*messageParam*傳遞 toothis 用戶端。
3. 在 App.xaml.cs，更新 hello **OnLaunched**事件處理常式方法定義，藉由新增 hello`async`修飾詞。 然後加入下列一行程式碼在 hello hello 方法結尾處的 hello:

        await InitNotificationsAsync();

    這可確保 hello 推播通知登錄建立或重新整理每次啟動 hello 應用程式。 請務必 toodo hello WNS 發送通道此 tooguarantee 一律是使用中。  
4. 適用於 Visual Studio 方案總管 中開啟 hello **Package.appxmanifest**檔案，並設定**快顯能夠**太**是**下**通知**.
5. 建置 hello 應用程式並確認您有任何錯誤。 您的用戶端應用程式應該立即註冊 hello 範本通知從 hello 回行動應用程式結束。 針對方案中每個 Windows 專案重複操作這一節。

#### <a name="test-push-notifications-in-your-windows-app"></a>在 Windows 應用程式中測試推播通知
1. 在 Visual Studio 中，以滑鼠右鍵按一下 Windows 專案，然後按一下 [設定為啟始專案]。
2. 按 hello**執行**按鈕 toobuild hello 專案，然後啟動 hello 應用程式。
3. 在 hello 應用程式中輸入新的 todoitem，名稱，然後按一下hello 加號 (**+**) 圖示 tooadd 它。
4. 確認新增 hello 項目時，收到通知。

## <a name="next-steps"></a>後續步驟
您可以深入了解推播通知︰

* [診斷推播通知問題](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  通知遭到捨棄或未抵達裝置有各種原因。 本主題說明如何 tooanalyze 並找出 hello 根原因的推送通知失敗。

您也可以繼續 tooone 的 hello 遵循教學課程：

* [新增驗證 tooyour 應用程式](app-service-mobile-xamarin-forms-get-started-users.md)  
  深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。
* [啟用應用程式的離線同步處理](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  深入了解如何使用行動應用程式的應用程式的 tooadd 離線支援後端。 使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
