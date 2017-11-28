---
title: "適用於 Xamarin 應用程式的 iOS 推播通知和通知中樞 | Microsoft Docs"
description: "在本教學課程中，您會了解如何使用 Azure 通知中樞將推播通知傳送至 Xamarin iOS 應用程式。"
services: notification-hubs
keywords: "ios 推播通知,推播訊息,推播通知"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="cd67a-104">適用於 Xamarin 應用程式的 iOS 推播通知和通知中樞</span><span class="sxs-lookup"><span data-stu-id="cd67a-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="cd67a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="cd67a-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cd67a-106">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cd67a-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cd67a-107">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cd67a-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cd67a-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="cd67a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="cd67a-109">本教學課程示範如何使用 Azure 通知中樞將推播通知傳送至 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd67a-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="cd67a-110">您將使用 [Apple Push Notification Service (APN)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)，建立可接收推播通知的空白 Xamarin.iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd67a-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="cd67a-111">完成時，您便能夠使用通知中樞，將推播通知廣播到所有執行您應用程式的裝置。</span><span class="sxs-lookup"><span data-stu-id="cd67a-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="cd67a-112">[NotificationHubs 應用程式][GitHub]範例中提供完成的程式碼。</span><span class="sxs-lookup"><span data-stu-id="cd67a-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="cd67a-113">本教學課程示範使用通知中樞的簡單推播訊息廣播案例。</span><span class="sxs-lookup"><span data-stu-id="cd67a-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd67a-114">先決條件</span><span class="sxs-lookup"><span data-stu-id="cd67a-114">Prerequisites</span></span>
<span data-ttu-id="cd67a-115">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="cd67a-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="cd67a-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="cd67a-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="cd67a-117">iOS 7.0 (或更新版本) 相容的裝置</span><span class="sxs-lookup"><span data-stu-id="cd67a-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="cd67a-118">iOS Developer Program 成員資格</span><span class="sxs-lookup"><span data-stu-id="cd67a-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="cd67a-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="cd67a-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cd67a-120">基於 iOS 推播通知的組態需求，您必須在實體 iOS 裝置 (iPhone 或 iPad) 上部署和測試範例應用程式，而不是在模擬器中。</span><span class="sxs-lookup"><span data-stu-id="cd67a-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="cd67a-121">完成本教學課程是 Xamarin.iOS 應用程式的所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="cd67a-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="cd67a-122">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="cd67a-122">Configure your notification hub</span></span>
<span data-ttu-id="cd67a-123">本節將引導您利用所建立的 **.p12** 推播憑證，建立新的通知中樞，並設定搭配 APNS 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cd67a-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="cd67a-124">如果您想要使用已經建立的通知中樞，可以跳至步驟 5。</span><span class="sxs-lookup"><span data-stu-id="cd67a-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="cd67a-125">因為我們想要設定 APNS 連線，請在 Azure 入口網站開啟您的通知中樞設定，按一下 [通知服務]<b></b>，然後按一下清單中的 [Apple (APNS)]<b></b> 項目。</span><span class="sxs-lookup"><span data-stu-id="cd67a-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="cd67a-126">完成後，按一下 [上傳憑證]<b></b>，選取您稍早匯出的 <b>.p12</b> 憑證，以及憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="cd67a-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="cd67a-127">請務必選取 [沙箱]<b></b> 模式，因為您將在開發環境中傳送推播訊息。</span><span class="sxs-lookup"><span data-stu-id="cd67a-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="cd67a-128">只有在您想傳送推播通知給已從市集購買應用程式的使用者時，才使用 [生產]<b></b> 設定。</span><span class="sxs-lookup"><span data-stu-id="cd67a-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="cd67a-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="cd67a-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="cd67a-130">現在已將您的通知中心設定成使用 APNS，而且您有可用來註冊應用程式和傳送推播通知的連接字串。</span><span class="sxs-lookup"><span data-stu-id="cd67a-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="cd67a-131">將您的應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="cd67a-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="cd67a-132">建立新專案</span><span class="sxs-lookup"><span data-stu-id="cd67a-132">Create a new project</span></span>
1. <span data-ttu-id="cd67a-133">在 Xamarin Studio 中，建立新的 iOS 專案，並選取 [統一 API] > [單一檢視應用程式] 範本。</span><span class="sxs-lookup"><span data-stu-id="cd67a-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - 選取應用程式類型][31]
2. <span data-ttu-id="cd67a-135">新增 Azure 訊息元件的參考。</span><span class="sxs-lookup"><span data-stu-id="cd67a-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="cd67a-136">在 [方案] 檢視中，以滑鼠右鍵按一下專案的 [元件] 資料夾，並選擇 [取得其他元件]。</span><span class="sxs-lookup"><span data-stu-id="cd67a-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="cd67a-137">搜尋 **Azure 傳訊**元件，並將該元件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="cd67a-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="cd67a-138">在 **AppDelegate.cs**中，新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="cd67a-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="cd67a-139">宣告 **SBNotificationHub**的執行個體：</span><span class="sxs-lookup"><span data-stu-id="cd67a-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="cd67a-140">建立含有下列變數的 **Constants.cs** 類別：</span><span class="sxs-lookup"><span data-stu-id="cd67a-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="cd67a-141">在 **AppDelegate.cs** 中，更新 **FinishedLaunching()** 以符合下列內容：</span><span class="sxs-lookup"><span data-stu-id="cd67a-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="cd67a-142">覆寫 **AppDelegate.cs** 中的 **RegisteredForRemoteNotifications()** 方法：</span><span class="sxs-lookup"><span data-stu-id="cd67a-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="cd67a-143">覆寫 **AppDelegate.cs** 中的 **ReceivedRemoteNotification()** 方法：</span><span class="sxs-lookup"><span data-stu-id="cd67a-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="cd67a-144">在 **AppDelegate.cs** 中建立下列 **ProcessNotification()** 方法：</span><span class="sxs-lookup"><span data-stu-id="cd67a-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="cd67a-145">您可以選擇覆寫 **FailedToRegisterForRemoteNotifications()** 以處理沒有網路連線等的情況。</span><span class="sxs-lookup"><span data-stu-id="cd67a-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="cd67a-146">這點特別重要，因為使用者可能在離線模式下 (例如飛機) 啟動您的應用程式，而您希望針對您的應用程式來處理推播傳訊案例。</span><span class="sxs-lookup"><span data-stu-id="cd67a-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="cd67a-147">在您的裝置上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd67a-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="cd67a-148">傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="cd67a-148">Sending Push Notifications</span></span>
<span data-ttu-id="cd67a-149">您可以在 [Azure 入口網站]中透過**疑難排解**工具集的**測試傳送**功能 (就在通知中樞裡，如下圖所示)，在您的應用程式中測試接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="cd67a-150">通常是使用相容的程式庫，透過行動服務或 ASP.NET 之類的後端服務來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="cd67a-151">如果您的案例中沒有可用的程式庫，您也可以直接使用 REST API 來傳送推播訊息。</span><span class="sxs-lookup"><span data-stu-id="cd67a-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="cd67a-152">在本教學課程中，為了簡單起見，我們只會在主控台應用程式 (而非後端服務) 中使用適用於通知中樞的 .NET SDK 傳送通知，示範如何測試您的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd67a-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="cd67a-153">我們建議以 [使用通知中樞將通知推播給使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 教學課程做為下一個步驟，以便從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="cd67a-154">不過，下列方法可用來傳送通知：</span><span class="sxs-lookup"><span data-stu-id="cd67a-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="cd67a-155">**REST 介面**：您可以在任何後端平台上使用 [REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)來支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="cd67a-156">**Microsoft Azure 通知中樞 .NET SDK**︰在適用於 Visual Studio 的 NuGet 套件管理員中，執行 [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="cd67a-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="cd67a-157">**Node.js** ： [如何從 Node.js 使用通知中樞](notification-hubs-nodejs-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="cd67a-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="cd67a-158">**Mobile Apps**：如需如何從已與通知中樞整合的 Azure App Service Mobile Apps 傳送通知的範例，請參閱[將推播通知新增至行動應用程式](../app-service-mobile/app-service-mobile-ios-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="cd67a-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="cd67a-159">**Java / PHP**︰如需使用 REST API 傳送推播通知的範例，請參閱＜如何從 Java/PHP 使用通知中樞＞([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。</span><span class="sxs-lookup"><span data-stu-id="cd67a-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="cd67a-160">(選用) 從 .NET 主控台應用程式傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="cd67a-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="cd67a-161">在本節中，您將使用簡單的 .NET 主控台應用程式來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="cd67a-162">就此範例而言，我們將切換到已安裝 Visual Studio 的 Windows 開發環境。</span><span class="sxs-lookup"><span data-stu-id="cd67a-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="cd67a-163">在 Visual Studio 中，建立新的 Visual C# 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="cd67a-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="cd67a-164">在 Visual Studio 中，依序按一下 [工具]、[NuGet 套件管理員] 和 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="cd67a-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="cd67a-165">套件管理員主控台應該會停駐於 Visual Studio 工作區的底端。</span><span class="sxs-lookup"><span data-stu-id="cd67a-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="cd67a-166">在 [套件管理員主控台] 視窗中，將 [預設專案]  設為新的主控台應用程式專案，然後在主控台視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cd67a-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="cd67a-167">這會使用 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 套件</a>加入對 Azure 通知中樞 SDK 的參考。</span><span class="sxs-lookup"><span data-stu-id="cd67a-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="cd67a-168">開啟 `Program.cs` 檔案，並新增下列 `using` 陳述式，確保我們可以在您的主要類別中使用 Azure 類別和函式：</span><span class="sxs-lookup"><span data-stu-id="cd67a-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="cd67a-169">在 `Program` 類別中，新增下列方法 (別忘了更換**連接字串**和**中樞名稱**)：</span><span class="sxs-lookup"><span data-stu-id="cd67a-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="cd67a-170">在您的 `Main` 方法中新增下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="cd67a-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="cd67a-171">按 F5 鍵以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd67a-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="cd67a-172">在幾秒之內就可以看到推播通知出現在裝置上。</span><span class="sxs-lookup"><span data-stu-id="cd67a-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="cd67a-173">無論是使用 Wi-Fi 或行動資料網路，請確定裝置上有作用中的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="cd67a-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="cd67a-174">您可以在 Apple [本機和推播通知程式設計指南](英文) 中找到所有可能的裝載。</span><span class="sxs-lookup"><span data-stu-id="cd67a-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="cd67a-175">(選用) 從行動服務傳送通知</span><span class="sxs-lookup"><span data-stu-id="cd67a-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="cd67a-176">在本節中，我們將使用行動服務透過節點指令碼傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="cd67a-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="cd67a-177">若要使用行動服務傳送通知，請依照 [開始使用行動服務]中的步驟進行，然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="cd67a-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="cd67a-178">登入 [Azure 傳統入口網站]，然後選取您的行動服務。</span><span class="sxs-lookup"><span data-stu-id="cd67a-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="cd67a-179">選取頂端的 [排程器]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cd67a-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="cd67a-180">建立新的排定工作、插入名稱，然後選取 [隨選] 。</span><span class="sxs-lookup"><span data-stu-id="cd67a-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="cd67a-181">在工作建立之後，按一下此工作名稱。</span><span class="sxs-lookup"><span data-stu-id="cd67a-181">When the job is created, click the job name.</span></span> <span data-ttu-id="cd67a-182">然後按一下頂端列中的 [指令碼]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cd67a-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="cd67a-183">將下列指令碼插入您的排程器函式內。</span><span class="sxs-lookup"><span data-stu-id="cd67a-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="cd67a-184">請確定使用您的通知中心名稱和稍早取得的 *DefaultFullSharedAccessSignature* 連接字串，來取代預留位置。</span><span class="sxs-lookup"><span data-stu-id="cd67a-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="cd67a-185">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cd67a-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="cd67a-186">按一下底列上的 [執行一次]  。</span><span class="sxs-lookup"><span data-stu-id="cd67a-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="cd67a-187">您應該會在裝置上收到警示。</span><span class="sxs-lookup"><span data-stu-id="cd67a-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd67a-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd67a-188">Next steps</span></span>
<span data-ttu-id="cd67a-189">在此簡單範例中，您將推播通知廣播通知到您的所有 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="cd67a-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="cd67a-190">為了鎖定特定使用者，請參閱教學課程 [使用通知中樞將通知推播給使用者]。</span><span class="sxs-lookup"><span data-stu-id="cd67a-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="cd67a-191">如果您想要按興趣群組分隔使用者，您可以參閱 [使用通知中心傳送即時新聞]。</span><span class="sxs-lookup"><span data-stu-id="cd67a-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="cd67a-192">若要深入了解如何使用通知中樞，請參閱[通知中樞指引]和 [iOS 的通知中樞作法]。</span><span class="sxs-lookup"><span data-stu-id="cd67a-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

<span data-ttu-id="cd67a-193">[開始使用行動服務]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="cd67a-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="cd67a-194">[Azure 傳統入口網站]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="cd67a-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="cd67a-195">[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="cd67a-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="cd67a-196">[iOS 的通知中樞作法]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="cd67a-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="cd67a-197">[使用通知中樞將通知推播給使用者]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="cd67a-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="cd67a-198">[使用通知中心傳送即時新聞]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="cd67a-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="cd67a-199">[本機和推播通知程式設計指南]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="cd67a-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="cd67a-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="cd67a-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="cd67a-201">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cd67a-201">[Azure Portal]: https://portal.azure.com</span></span>
