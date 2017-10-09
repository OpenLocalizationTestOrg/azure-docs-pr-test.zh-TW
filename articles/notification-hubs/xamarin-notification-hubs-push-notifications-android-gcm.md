---
title: "aaaGet Xamarin.Android 應用程式入門通知中心 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooa Xamarin Android 應用程式。"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>開始使用適用於 Android 應用程式的通知中樞
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa Xamarin.Android 應用程式。
您將建立可使用 Google Cloud Messaging (GCM) 接收推播通知的空白 Xamarin.Android app。 完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。 hello 完成會提供程式碼 hello[通知中樞應用程式][ GitHub]範例。

本教學課程示範 hello 簡單廣播的案例中使用通知中樞。

## <a name="before-you-begin"></a>開始之前
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

hello 完成本教學課程中的程式碼可以在 GitHub 上找到[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid)。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* Windows 的 Visual Studio 與 Xamarin 或 Mac OS X 的 Xamarin Studio。完整的安裝指示位於[設定和安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx)。
* 有效的 Google 帳戶
* [Azure 訊息元件]
* [Google Cloud Messaging 用戶端元件]

完成本教學課程是 Xamarin.Android 應用程式所有其他通知中樞教學課程的先決條件。

> [!IMPORTANT]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F)。
> 
> 

## <a name="enable-google-cloud-messaging"></a>啟用 Google 雲端通訊
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>設定您的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>按一下 hello<b>設定</b>hello 頂端索引標籤上，輸入 hello <b>API 金鑰</b>hello 上一節，取得值，然後按一下<b>儲存</b>。</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 連接字串 tooboth 註冊您的應用程式 tooreceive 通知和 toosend 推播通知。

## <a name="connect-your-app-toohello-notification-hub"></a>連接您的應用程式 toohello 通知中樞
### <a name="create-a-new-project"></a>建立新專案
1. 在 Xamarin Studio 中，依序按一下 [新增方案]、[Android 應用程式] 和 [下一步]。
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. 輸入您的**應用程式名稱**和**識別碼**。 按一下 hello**目標平台**toosupport 然後再按一下**下一步**和**建立**。
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    這會建立新的 Android 專案。

1. Hello 方案檢視中新的專案上按一下滑鼠右鍵，然後選擇開啟 hello 專案屬性**選項**。 選取 hello **Android 應用程式**hello 中的項目**建置**> 一節。
   
    請確定該 hello 第一個字母您**封裝名稱**是小寫。
   
   > [!IMPORTANT]
   > hello 的 hello 封裝名稱的第一個字母必須是小寫。 否則，當您在下文為推播通知註冊 **BroadcastReceiver** 和 **IntentFilter** 時，將收到應用程式資訊清單錯誤。
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. （選擇性） 組 hello **Android 最小版本**tooanother API 層級。
3. （選擇性） 組 hello**目標 Android 版本**toohello 想的 tootarget （必須是應用程式開發介面層級 8 或更新版本） 的另一個應用程式開發介面版本。

按一下**確定**和關閉 hello 專案選項 對話方塊。

### <a name="add-hello-required-components-tooyour-project"></a>加入 hello 必要的元件 tooyour 專案
hello Google 雲端訊息用戶端 hello Xamarin 元件存放區提供簡化 Xamarin.Android 支援推播通知的 hello 程序。

1. Xamarin.Android 應用程式中的 hello Components 資料夾上按一下滑鼠右鍵，然後選擇 **取得多元件**。
2. 搜尋 hello **Azure 訊息**元件並將它加入 toohello 專案。
3. 搜尋 hello **Google 雲端訊息用戶端**元件並將它加入 toohello 專案。

### <a name="set-up-notification-hubs-in-your-project"></a>在專案中設定通知中樞
1. 收集下列資訊 Android 應用程式與通知中樞的 hello:
   
   * **GoogleProjectNumber**： 取得此專案數字值從 hello hello Google 開發人員入口網站上的應用程式的概觀。 記下這個值前面的 hello 入口網站上建立 hello 應用程式時。
   * **接聽的連接字串**: hello 儀表板中 hello [Azure 傳統入口網站]，按一下 **檢視連接字串**。 複製 hello *DefaultListenSharedAccessSignature*連接字串，這個值。
   * **中樞名稱**： 這是您的中樞，從 hello hello 名稱[Azure 傳統入口網站]。 例如， *mynotificationhub2*。
     
     建立**Constants.cs** Xamarin 專案的類別，並定義下列 hello 類別中的常數值的 hello。 Hello 預留位置取代為您的值。
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. 新增 hello 下列 using 陳述式太**Weatherapp**:
   
        using Android.Util;
        using Gcm.Client;
3. 新增執行個體變數 toohello `MainActivity` hello 應用程式執行時，將會使用的 tooshow 警示 對話方塊的類別：
   
        public static MainActivity instance;
4. 建立下列方法在 hello hello **MainActivity**類別：
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. 在 hello`OnCreate`方法**Weatherapp**，初始化 hello`instance`變數和太加入呼叫`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. 建立新類別 **MyBroadcastReceiver**。
   
   > [!NOTE]
   > 我們將在下文中從頭逐步建立 **BroadcastReceiver** 類別。 不過，快速替代 toomanually 建立**MyBroadcastReceiver.cs**是 toorefer toohello **GcmService.cs**隨附 hello hello範例Xamarin.Android專案中找到檔案[通知中樞範例][GitHub]。 複製**GcmService.cs**和變更類別名稱可以是很好 toostart 以及。
   > 
   > 
7. 新增 hello 下列 using 陳述式太**MyBroadcastReceiver.cs** （toohello 元件，並針對您先前加入的組件參考）：
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. 在**MyBroadcastReceiver.cs**，新增下列權限要求之間 hello hello**使用**陳述式和 hello**命名空間**宣告：
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. 在**MyBroadcastReceiver.cs**，變更 hello **MyBroadcastReceiver**類別 toomatch hello 下列：
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. 在 **MyBroadcastReceiver.cs** 中，新增另一個衍生自 **GcmServiceBase** 且名稱為 **PushHandlerService** 的類別。 請確定 tooapply hello**服務**屬性 toohello 類別：
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** 實作 **OnRegistered()**、**OnUnRegistered()**、**OnMessage()**、**OnRecoverableError()** 和 **OnError()** 等方法。 我們**PushHandlerService**實作類別必須覆寫這些方法，而且這些方法會引發在回應 toointeracting 與 hello 通知中樞。
12. 覆寫 hello **OnRegistered()**方法中的**PushHandlerService**使用下列程式碼的 hello:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > 在 hello **OnRegistered()**上述程式碼，您應該會注意到 hello 能力 toospecify 標記 tooregister 特定訊息的通道。
    > 
    > 
13. 覆寫 hello **OnMessage**方法中的**PushHandlerService**使用下列程式碼的 hello:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. 新增下列 hello **createNotification**和**dialogNotify**方法太**PushHandlerService**收到通知時，通知使用者。
    
    > [!NOTE]
    > Android 5.0 版與更新版本中的通知設計，與先前版本有極大的不同。 如果您測試 Android 5.0 或更新版本，hello 應用程式需要 toobe 執行 tooreceive hello 通知。 如需詳細資訊，請參閱 [Android 通知](http://go.microsoft.com/fwlink/?LinkId=615880)。
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. 覆寫抽象成員 **OnUnRegistered()**、**OnRecoverableError()** 和 **OnError()**，以便您的程式碼進行編譯：
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Hello 模擬器中執行您的應用程式
如果您在 hello 模擬器中執行此應用程式，請確定您使用 Android 虛擬裝置 (AVD) 支援 Google 應用程式開發介面。

> [!IMPORTANT]
> 在順序 tooreceive 推播通知，您必須設定 Android 虛擬裝置上的 Google 帳戶。 (在 hello 模擬器中，瀏覽過**設定**按一下**新增帳戶**。)此外，請確定該 hello 模擬器連接的 toohello 網際網路。
> 
> [!NOTE]
> Android 5.0 版與更新版本中的通知設計，與先前版本有極大的不同。 如需詳細資訊，請參閱 [Android 通知](http://go.microsoft.com/fwlink/?LinkId=615880)。
> 
> 

1. 從 工具 中，按一下 Open Android Emulator Manager，選取您的裝置，然後按一下Edit。
   
      ![][18]
2. 在 目標 中選取 Google API，然後按一下確定。
   
      ![][19]
3. Hello 頂端工具列上，按一下**執行**，然後選取您的應用程式。 這會啟動 hello 模擬器，並執行 hello 應用程式。
   
   hello 應用程式擷取 hello *registrationId*從 GCM 以及與 hello 通知中樞的暫存器。

## <a name="send-notifications-from-your-backend"></a>從後端傳送通知
您可以測試應用程式中接收通知，傳送通知給 hello 以[Azure 傳統入口網站]hello 透過偵錯索引標籤上 hello 通知中樞，囉 」 畫面下方所示。

![][30]

推播通知通常會在後端服務 (例如行動服務) 中或透過相容程式庫的 ASP.NET 傳送。 您也可以使用 hello REST API 直接 toosend 通知訊息，如果文件庫不適用於您的後端。

以下是一些您可能想要 tooreview 傳送通知的教學課程清單：

* ASP.NET: 請參閱 <<c0> [ 使用通知中樞 toopush 通知 toousers]。
* Azure 通知中樞 Java SDK： 請參閱[如何 toouse 通知中樞，從 Java](notification-hubs-java-push-notification-tutorial.md)從 Java 傳送通知。 這已在 Eclipse for Android Development 中測試。
* PHP： 請參閱[如何 toouse 通知中樞，從 PHP](notification-hubs-php-push-notification-tutorial.md)。

Hello hello 教學課程的下一個小節，您會傳送通知，藉由使用.NET 主控台應用程式和使用透過節點指令碼的行動服務。

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(選用) 使用 .NET 應用程式傳送通知
在本節中，您將使用 .NET 主控台應用程式來傳送通知。

1. 建立新的 Visual C# 主控台應用程式：
   
      ![][20]
2. 在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。
   
    這是 Visual Studio 中顯示 hello Package Manager Console。
3. 在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. 開啟 hello Program.cs 檔案並加入下列 hello`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在您`Program`類別中，新增下列方法 hello。 更新 hello 預留位置文字，與您*DefaultFullSharedAccessSignature*連接字串和中樞名稱，從 hello [Azure 傳統入口網站]。
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. 新增下列幾行中的 hello 您**Main**方法：
   
         SendNotificationAsync();
         Console.ReadLine();
7. 按 F5 鍵 toorun hello 應用程式 hello。 您應該在 hello 應用程式會收到通知。
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(選用) 使用行動服務傳送通知
1. 依照 [開始使用行動服務]執行作業。
2. 登入 toohello [Azure 傳統入口網站]，然後選取您的行動服務。
3. 選取 hello**排程器**hello 最上層顯示 索引標籤。
   
      ![][22]
4. 建立新的排定工作、插入名稱，然後選取 [隨選] 。
   
      ![][23]
5. 建立 hello 作業時，按一下 hello 作業名稱。 然後按一下 [hello**指令碼**hello 頂端列] 索引標籤。
6. 插入 hello 遵循您的排程器函式內的指令碼。 請確定 tooreplace hello 預留位置取代通知中樞名稱和 hello 的連接字串*DefaultFullSharedAccessSignature*您稍早取得。 按一下 [儲存] 。
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. 按一下**執行一次**hello 下方列上。 您應會收到快顯通知。

## <a name="next-steps"></a>後續步驟
在這個簡單的範例中，您傳播通知 tooall 您的 Android 裝置。 在排序 tootarget 特定使用者，請參閱 toohello 教學課程[ 使用通知中樞 toopush 通知 toousers]。 如果您想 toosegment 您感興趣群組的使用者，您可以閱讀[使用通知中樞 toosend 最新消息]。 深入了解如何 toouse 中的通知中樞[通知中樞指引]在 hello[通知中心如何 toofor Android]。

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[開始使用行動服務]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Azure 傳統入口網站]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[通知中心如何 toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[ 使用通知中樞 toopush 通知 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[使用通知中樞 toosend 最新消息]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging 用戶端元件]: http://components.xamarin.com/view/GCMClient/
[Azure 訊息元件]: http://components.xamarin.com/view/azure-messaging
