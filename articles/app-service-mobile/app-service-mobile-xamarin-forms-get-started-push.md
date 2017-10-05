---
title: "將推播通知新增至 Xamarin.Forms 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure 服務將多平台推播通知傳送至 Xamarin.Forms 應用程式。"
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="f4fd1-103">將推播通知新增至 Xamarin.Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fd1-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f4fd1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f4fd1-104">Overview</span></span>
<span data-ttu-id="f4fd1-105">在本教學課程中，您會將推播通知新增至 [Xamarin.Forms 快速入門](app-service-mobile-xamarin-forms-get-started.md)所產生的所有專案。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="f4fd1-106">這表示每次插入記錄時，就會將推播通知傳送到所有跨平台用戶端。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="f4fd1-107">如果您不要使用下載的快速入門伺服器專案，將需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="f4fd1-108">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4fd1-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="f4fd1-109">Prerequisites</span></span>
<span data-ttu-id="f4fd1-110">若為 iOS，您需要 [Apple Developer Program 成員資格](https://developer.apple.com/programs/ios/)和實體 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="f4fd1-111">[iOS 模擬器不支援推播通知](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="f4fd1-112"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="f4fd1-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="f4fd1-113">更新伺服器專案以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="f4fd1-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="f4fd1-114">設定和執行 Android 專案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="f4fd1-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="f4fd1-115">完成本節可以為適用於 Android 的 Xamarin.Forms Droid 專案啟用推播通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="f4fd1-116">啟用 Firebase 雲端傳訊 (FCM)</span><span class="sxs-lookup"><span data-stu-id="f4fd1-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="f4fd1-117">設定 Mobile Apps 後端以使用 FCM 傳送推送要求</span><span class="sxs-lookup"><span data-stu-id="f4fd1-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="f4fd1-118">將推播通知新增至 Android 專案</span><span class="sxs-lookup"><span data-stu-id="f4fd1-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="f4fd1-119">為後端設定了 FCM 後，您就可以在用戶端中新增元件和程式碼，以向 FCM 註冊。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="f4fd1-120">您也可以透過 Mobile Apps 後端向 Azure 通知中樞註冊推播通知，並接收通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="f4fd1-121">在 **Droid** 專案中，以滑鼠右鍵按一下 [元件] 資料夾，然後按一下 [取得更多元件...]。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="f4fd1-122">然後搜尋 **Google 雲端通訊用戶端**元件，並將該元件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="f4fd1-123">此元件支援 Xamarin Android 專案的推播通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="f4fd1-124">開啟 MainActivity.cs 專案檔案，然後將下列陳述式加入至檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="f4fd1-125">在 **OnCreate** 方法中，在呼叫 **LoadApplication** 之後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="f4fd1-126">加入新的 **CreateAndShowDialog** 協助程式方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f4fd1-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="f4fd1-127">將下列程式碼加入至 **MainActivity** 類別：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="f4fd1-128">這會公開目前的 **MainActivity** 執行個體，讓我們可以在主要 UI 執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="f4fd1-129">初始化 `instance`OnCreate **方法開頭的**  變數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="f4fd1-130">將新的類別檔案新增至名為 `GcmService.cs` 的 **Droid** 專案，並確定下列 **using** 陳述式出現在檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="f4fd1-131">在檔案頂端的 **using** 陳述式之後和 **namespace** 宣告之前，新增下列權限要求。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="f4fd1-132">將下列類別定義加入至命名空間。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="f4fd1-133">以您先前記下的專案號碼取代 **<PROJECT_NUMBER>**。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="f4fd1-134">使用下列程式碼取代空的 **GcmService** 類別，以使用新的廣播接收器︰</span><span class="sxs-lookup"><span data-stu-id="f4fd1-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="f4fd1-135">將下列程式碼新增至 **GcmService** 類別。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="f4fd1-136">這會覆寫 **OnRegistered** 事件處理常式，並實作 **Register** 方法。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="f4fd1-137">請注意，此程式碼使用範本註冊中的 `messageParam` 參數。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="f4fd1-138">加入下列程式碼以實作 **OnMessage**：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="f4fd1-139">這會處理內送通知，並將它們傳送至通知管理員來顯示。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="f4fd1-140">**GcmServiceBase** 也會要求您實作 **OnUnRegistered** 和 **OnError** 處理常式方法，您的做法如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="f4fd1-141">現在，您已經準備好在 Android 裝置或模擬器上執行的應用程式中測試推播通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="f4fd1-142">在 Android 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f4fd1-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="f4fd1-143">只有要在模擬器上測試時，才需要前兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="f4fd1-144">針對您要部署的目的地虛擬裝置或偵錯的所在虛擬裝置，請確認該裝置具有已設定為目標的 Google API，如以下 Android 虛擬裝置管理員所示。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="f4fd1-145">按一下 [應用程式] > [設定] > [新增帳戶] 將 Google 帳戶加入 Android 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="f4fd1-146">然後遵循提示在裝置中新增現有 Google 帳戶，或是建立一個新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="f4fd1-147">在 Visual Studio 或 Xamarin Studio 中，以滑鼠右鍵按一下 **Droid** 專案，然後按一下 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="f4fd1-148">按一下 [執行] 以建置專案，並在 Android 裝置或模擬器上啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="f4fd1-149">在應用程式中輸入一項工作，然後按一下加號 (**+**) 圖示。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="f4fd1-150">確認在加入項目時收到通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="f4fd1-151">設定和執行 iOS 專案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="f4fd1-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="f4fd1-152">這一節適用於對 iOS 裝置執行 Xamarin iOS 專案。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="f4fd1-153">如果未使用 iOS 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="f4fd1-154">設定 APNS 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="f4fd1-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="f4fd1-155">接下來，您將在 Xamarin Studio 或 Visual Studio 中設定 iOS 專案設定。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="f4fd1-156">將推播通知加入至 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fd1-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="f4fd1-157">在 **iOS** 專案中開啟 AppDelegate.cs，並將下列陳述式新增到程式碼檔案頂端。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="f4fd1-158">在 **AppDelegate** 類別中，新增 **RegisteredForRemoteNotifications** 事件的覆寫以註冊通知：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="f4fd1-159">此外，也在 **AppDelegate** 中新增 **DidReceiveRemoteNotification** 事件處理常式的下列覆寫：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="f4fd1-160">當應用程式執行時，此方法會處理傳入的通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="f4fd1-161">在 **AppDelegate** 類別中，將下列程式碼新增到 **FinishedLaunching** 方法：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="f4fd1-162">這能夠支援遠端通知，並要求推播註冊。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="f4fd1-163">您的應用程式現在已更新為支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="f4fd1-164">在 iOS 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f4fd1-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="f4fd1-165">以滑鼠右鍵按一下 iOS 專案，然後按一下 [設為起始專案]。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="f4fd1-166">在 Visual Studio 中按下 [執行] 按鈕或 **F5** 以建置專案，並在 iOS 裝置上啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="f4fd1-167">然後，按一下 [確定] 以接收推撥通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f4fd1-168">您必須明確地接受來自應用程式的推播通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="f4fd1-169">只有在應用程式第一次執行時，才會發生此要求。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="f4fd1-170">在應用程式中輸入一項工作，然後按一下加號 (**+**) 圖示。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="f4fd1-171">確認您已接收到通知，然後按一下 [確定] 以關閉通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="f4fd1-172">設定和執行 Windows 專案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="f4fd1-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="f4fd1-173">本節說明執行適用於 Windows 裝置的 Xamarin.Forms WinApp 和 WinPhone81 專案。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="f4fd1-174">這些步驟也支援通用 Windows 平台 (UWP) 專案。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="f4fd1-175">如果未使用 Windows 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="f4fd1-176">為 Windows 應用程式向 Windows 通知服務 (WNS) 註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="f4fd1-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="f4fd1-177">設定 WNS 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="f4fd1-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="f4fd1-178">將推播通知加入至 Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fd1-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="f4fd1-179">在 Visual Studio 中，開啟 Windows 專案中的 **App.xaml.cs**，並新增下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="f4fd1-180">使用包含 `TodoItemManager` 類別的可攜式專案命名空間來取代 `<your_TodoItemManager_portable_class_namespace>`。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="f4fd1-181">在 App.xaml.cs 中，新增下列 **InitNotificationsAsync** 方法：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="f4fd1-182">這個方法會取得推播通知通道，並註冊範本以接收來自通知中樞的範本通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="f4fd1-183">支援 messageParam  的範本通知會傳送到此用戶端。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="f4fd1-184">在 App.xaml.cs 中，新增 `async` 修飾詞以更新 **OnLaunched** 事件處理常式方法定義。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="f4fd1-185">然後，在方法的結尾新增下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="f4fd1-186">如此可確保每次啟動應用程式時都會建立或重新整理推播通知註冊。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="f4fd1-187">必須如此以保證 WNS 推送通道永遠在作用中。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="f4fd1-188">在 Visual Studio 的 [方案總管] 中，開啟 **Package.appxmanifest** 檔案，然後把 [通知] 下方的 [支援快顯通知] 設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="f4fd1-189">建置應用程式並確認沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="f4fd1-190">您用戶端應用程式現在應該註冊 Mobile Apps 後端的範本通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="f4fd1-191">針對方案中每個 Windows 專案重複操作這一節。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="f4fd1-192">在 Windows 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f4fd1-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="f4fd1-193">在 Visual Studio 中，以滑鼠右鍵按一下 Windows 專案，然後按一下 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="f4fd1-194">按 [執行] 按鈕，以建立專案並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="f4fd1-195">在應用程式中輸入新 todoitem 的名稱，然後按一下加號 (**+**) 圖示來加入它。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="f4fd1-196">確認在加入項目時收到通知。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4fd1-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4fd1-197">Next steps</span></span>
<span data-ttu-id="f4fd1-198">您可以深入了解推播通知︰</span><span class="sxs-lookup"><span data-stu-id="f4fd1-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="f4fd1-199">診斷推播通知問題</span><span class="sxs-lookup"><span data-stu-id="f4fd1-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="f4fd1-200">通知遭到捨棄或未抵達裝置有各種原因。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="f4fd1-201">本主題說明如何分析及找出推播通知失敗的根本原因。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="f4fd1-202">您也可以繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="f4fd1-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="f4fd1-203">在您的應用程式中新增驗證</span><span class="sxs-lookup"><span data-stu-id="f4fd1-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="f4fd1-204">了解如何使用身分識別提供者驗證應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="f4fd1-205">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="f4fd1-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="f4fd1-206">了解如何使用 Mobile Apps 後端，為應用程式新增離線支援。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="f4fd1-207">使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="f4fd1-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
