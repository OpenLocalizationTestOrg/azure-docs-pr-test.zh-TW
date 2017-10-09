---
title: "aaaiOS 推播通知的通知中樞的 Xamarin 應用程式 |Microsoft 文件"
description: "在本教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooa Xamarin iOS 應用程式。"
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
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>適用於 Xamarin 應用程式的 iOS 推播通知和通知中樞
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!IMPORTANT]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)。
> 
> 

本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooan iOS 應用程式。
您將建立空白的 Xamarin.iOS 應用程式透過使用 hello 接收推播通知[Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)。 完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。 hello 完成會提供程式碼 hello[通知中樞應用程式][ GitHub]範例。

本教學課程示範了通知中心的 hello 簡單的推播訊息廣播的案例。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* [Xcode 6.0][Install Xcode]
* iOS 7.0 (或更新版本) 相容的裝置
* iOS Developer Program 成員資格
* [Xamarin Studio]
  
  > [!NOTE]
  > IOS 推播通知的設定需求，因為您必須部署，並在 hello 模擬器 中，而不是測試 hello 實體 iOS 裝置 （iPhone 或 iPad） 上的範例應用程式。
  > 
  > 

完成本教學課程是 Xamarin.iOS 應用程式的所有其他通知中樞教學課程的先決條件。

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>設定您的通知中樞
本節將引導您建立新的通知中樞及與使用 hello APNS 設定驗證**.p12**您所建立的推播憑證。 如果您想 toouse 您已經建立通知中樞，您可以略過 toostep 5。

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>我們想要 tooconfigure hello APNS 連線，請在 hello Azure 入口網站中，開啟您通知中樞的設定，ande 按一下<b>Notification Services</b>，然後按一下hello <b>Apple (APNS)</b> hello 清單中的項目。 一旦完成，請按一下<b>上傳憑證</b>和選取 hello <b>.p12</b> hello hello 憑證密碼以及更早版本，匯出的憑證。</p>

<p>請確定 tooselect<b>沙箱</b>模式，因為您將會傳送推播訊息在開發環境中。 只使用 hello<b>生產</b>設定，如果您想 toosend 推播通知 toousers 已經購買您的應用程式從 hello 存放區。</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

您的通知中樞現在是設定的 toowork 使用 APNS，而且您擁有 hello 連接字串 tooregister 您的應用程式，並傳送推播通知。

## <a name="connect-your-app-toohello-notification-hub"></a>連接您的應用程式 toohello 通知中樞
#### <a name="create-a-new-project"></a>建立新專案
1. 在 Xamarin Studio，請在建立新的 iOS 專案，然後選取 hello**統一的 API** > **單一檢視應用程式**範本。
   
     ![Xamarin Studio - 選取應用程式類型][31]
2. 新增參考 toohello Azure 傳訊元件。 在 hello 方案檢視，以滑鼠右鍵按一下 hello**元件**專案的資料夾，然後選擇 **取得多元件**。 搜尋 hello **Azure 訊息**元件並加入 hello 元件 tooyour 專案。
3. 在**d**，新增 hello 下列 using 陳述式：
   
        using WindowsAzure.Messaging;
4. 宣告 **SBNotificationHub**的執行個體：
   
        private SBNotificationHub Hub { get; set; }
5. 建立**Constants.cs**類別以 hello 下列變數：
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. 在**d**，更新**FinishedLaunching()** toomatch hello 下列：
   
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
7. 覆寫 hello **RegisteredForRemoteNotifications()**方法中的**d**:
   
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
8. 覆寫 hello **ReceivedRemoteNotification()**方法中的**d**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. 建立 hello 遵循**ProcessNotification()**方法中的**d**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
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
   > 您可以選擇 toooverride **FailedToRegisterForRemoteNotifications()** toohandle 情況下，例如，沒有網路連線。 其中 hello 使用者可能會在離線模式 （例如飛機） 中啟動您的應用程式，而且您想 toohandle 發送傳訊案例特定 tooyour 應用程式，這是特別重要。
   > 
   > 
10. 在您的裝置上執行 hello 應用程式。

## <a name="sending-push-notifications"></a>傳送推播通知
您可以測試應用程式中接收推播通知傳送通知給 hello 以[Azure 入口網站]透過 hello**測試傳送**功能 hello**疑難排解**工具組，直接在 hello 通知中樞頁面上，囉 」 畫面下方所示。

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

通常是使用相容的程式庫，透過行動服務或 ASP.NET 之類的後端服務來傳送推播通知。 直接 toosend 發送訊息，如果媒體櫃無法使用您的案例中，您也可以使用 hello REST API。 

在本教學課程中，我們將保持簡單，並只示範測試用戶端應用程式透過傳送 hello.NET SDK 使用通知中心，而不是後端服務的主控台應用程式的通知。 我們建議 hello[使用通知中樞 toopush 通知 toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程為 hello 下一個步驟，從 ASP.NET 後端傳送通知。 不過，hello 下列方法可用來傳送通知：

* **REST 介面**： 您可以使用 hello 任何後端平台上支援推播通知[REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)。
* **Microsoft Azure 通知中樞.NET SDK**: hello for Visual Studio 的 Nuget 封裝管理員，在執行[Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。
* **Node.js** :[如何 toouse 通知中樞，從 Node.js](notification-hubs-nodejs-push-notification-tutorial.md)。

**行動應用程式**： 如需如何 toosend 通知從 Azure App Service 行動應用程式後端整合通知中心，請參閱[新增推播通知 tooyour 行動裝置應用程式](../app-service-mobile/app-service-mobile-ios-get-started-push.md)。

* **Java / PHP**： 如需如何使用 toosend 推播通知 hello REST Api 的範例，請參閱 「 如何 toouse 來自 Java/PHP 的通知中心 」 ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(選用) 從 .NET 主控台應用程式傳送推播通知
在本節中，您將使用簡單的 .NET 主控台應用程式來傳送推播通知。 基於 hello 此範例中，我們將會切換 tooa Windows 開發環境中擁有已經安裝 Visual Studio。

1. 在 Visual Studio 中，建立新的 Visual C# 主控台應用程式：
   
       ![Visual Studio - Create a new console application][213]
2. 在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。
   
    hello 封裝管理員主控台應該會出現您的 Visual Studio 工作區的停駐的 toohello 底部。
3. 在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. 開啟 hello`Program.cs`檔案，然後加入下列 hello`using`陳述式，確保我們可以使用 Azure 的類別和您的主要類別內的函式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在您`Program`類別中，新增下列方法 hello (不要忘記 tooreplace hello**連接字串**和**中樞名稱**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. 新增下列幾行中的 hello 您`Main`方法：
   
         SendNotificationAsync();
         Console.ReadLine();
7. 按 F5 鍵 toorun hello 應用程式 hello。 在幾秒之內就可以看到推播通知出現在裝置上。 不論您使用 Wi-fi 或行動數據網路，請確定您有網際網路連線，hello 裝置上。

您可以在 hello Apple 找到所有 hello 可能裝載[本機和推播通知程式設計指南]。

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(選用) 從行動服務傳送通知
在本節中，我們將使用行動服務透過節點指令碼傳送推播通知。

toosend 通知使用行動服務中，請遵循[開始使用 Mobile Services]，然後：

1. 登入 toohello [Azure 傳統入口網站]，然後選取您的行動服務。
2. 選取 hello**排程器**hello 最上層顯示 索引標籤。
   
       ![Azure Classic Portal - Scheduler][215]
3. 建立新的排定工作、插入名稱，然後選取 [隨選] 。
   
       ![Azure Classic Portal - Create new job][216]
4. 建立 hello 作業時，按一下 hello 作業名稱。 然後按一下 [hello**指令碼**hello 頂端列] 索引標籤。
5. 插入 hello 遵循您的排程器函式內的指令碼。 請確定 tooreplace hello 預留位置取代通知中樞名稱和 hello 的連接字串*DefaultFullSharedAccessSignature*您稍早取得。 按一下 [儲存] 。
   
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
6. 按一下**執行一次**hello 下方列上。 您應該會在裝置上收到警示。

## <a name="next-steps"></a>後續步驟
在這個簡單的範例中，您傳播推播通知 tooall iOS 裝置。 在排序 tootarget 特定使用者，請參閱 toohello 教學課程[使用通知中樞 toopush 通知 toousers]。 如果您想 toosegment 您感興趣群組的使用者，您可以閱讀[使用通知中樞 toosend 最新消息]。 深入了解如何 toouse 中的通知中樞[通知中樞指引]在 hello[通知中心如何 toofor iOS]。

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

[開始使用 Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[通知中心如何 toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[使用通知中樞 toopush 通知 toousers]: /manage/services/notification-hubs/notify-users-aspnet
[使用通知中樞 toosend 最新消息]: /manage/services/notification-hubs/breaking-news-dotnet

[本機和推播通知程式設計指南]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure 入口網站]: https://portal.azure.com
