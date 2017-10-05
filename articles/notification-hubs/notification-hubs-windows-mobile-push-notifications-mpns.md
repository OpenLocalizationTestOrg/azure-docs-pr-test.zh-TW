---
title: "在 Windows Phone 上使用 Azure 通知中樞傳送推播通知 | Microsoft Docs"
description: "在本教學課程中，您會了解如何使用 Azure 通知中樞，將推播通知傳送到 Windows Phone 8 或 Windows Phone 8.1 Silverlight 應用程式。"
services: notification-hubs
documentationcenter: windows
keywords: "推播通知,推播通知,windows phone 推播"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>在 Windows Phone 上使用 Azure 通知中樞傳送推播通知
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!NOTE]
> 若要完成此教學課程，您必須具備有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F)。
> 
> 

本教學課程將示範如何使用 Azure 通知中樞，將推播通知傳送到 Windows Phone 8 或 Windows Phone 8.1 Silverlight 應用程式。 如果您的目標是 Windows Phone 8.1 (非 Silverlight)，請參閱 [Windows 通用](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 版本。
在本教學課程中，您將使用 Microsoft 推播通知服務 (MPNS)，建立可接收推播通知的空白 Windows Phone 8 應用程式。 完成時，您便能夠使用通知中樞，將推播通知廣播到所有執行您 app 的裝置。

> [!NOTE]
> 通知中樞 Windows Phone SDK 不支援將 Windows 推播通知服務 (WNS) 與 Windows Phone 8.1 Silverlight app 搭配使用。 若要將 WNS (而非 MPNS) 與 Windows Phone 8.1 Silverlight app 搭配使用，請遵循使用 REST API 的 [通知中樞 - Windows Phone Silverlight 教學課程]。
> 
> 

本教學課程示範使用通知中樞的簡單廣播案例。

## <a name="prerequisites"></a>先決條件
本教學課程需要下列各項：

* [Visual Studio 2012 Express for Windows Phone]或更新版本。

完成本教學課程是 Windows Phone 8 應用程式所有其他通知中樞教學課程的先決條件。

## <a name="create-your-notification-hub"></a>建立您的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>按一下 [通知服務]<b></b> 區段 (在 [設定]<i></i> 中)，按一下 [Windows Phone (MPNS)]<b></b>，然後按一下 [啟用未經驗證的推送]<b></b> 核取方塊。</p>
</li>
</ol>

&emsp;&emsp;![Azure 入口網站 - 啟用未經驗證的推播通知](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

現在已建立並設定您的中樞，以傳送未經驗證的 Windows Phone 通知。

> [!NOTE]
> 本教學課程使用處於未通過驗證模式的 MPNS。 MPNS 未通過驗證模式內含您可傳送至每個通道的通知限制。 通知中樞可讓您上傳憑證，以支援 [MPNS 驗證模式](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) 。
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a>將您的應用程式連接到通知中樞
1. 在 Visual Studio 中建立新的 Windows Phone 8 應用程式。
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    在 Visual Studio 2013 Update 2 或更新版本中，您必須改為建立 Windows Phone Silverlight 應用程式。
   
    ![Visual Studio - 新增專案 - 空白應用程式 - Windows Phone Silverlight][11]
2. 在 Visual Studio 中，以滑鼠右鍵按一下方案，然後按一下 [管理 NuGet 封裝] 。
   
    此時會顯示 [管理 NuGet 封裝]  對話方塊。
3. 搜尋 `WindowsAzure.Messaging.Managed`，然後按一下 [安裝] 並接受使用條款。
   
    ![Visual Studio - NuGet 封裝管理員][20]
   
    這會使用 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>來下載、安裝並新增適用於 Windows 的 Azure 傳訊程式庫參考。
4. 開啟 App.xaml.cs 檔案，並新增下列 `using` 陳述式：
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. 在 App.xaml.cs 中 **Application_Launching** 方法的頂端新增下列程式碼：
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > **MyPushChannel** 值是一個索引，用來查閱 [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) 集合中的現有通道。 如果集合中沒有任何項目，請以該名稱建立新的項目。
   > 
   > 
   
    請確定插入您的中心名稱，及您在上一節中取得、名為 **DefaultListenSharedAccessSignature** 的連接字串。
    此程式碼會從 MPNS 中擷取 app 的通道 URI，然後向您的通知中樞註冊該通道 URI。 它也保證每次啟動應用程式時，便會在通知中樞中註冊通道 URI。
   
   > [!NOTE]
   > 本教學課程將傳送快顯通知給裝置。 傳送磚通知時，您必須在通道上改為呼叫 **BindToShellTile** 方法。 若要同時支援快顯和圖格通知，請呼叫 **BindToShellTile** 和 **BindToShellToast**。
   > 
   > 
6. 在 [方案總管] 中，展開 [屬性]、開啟 `WMAppManifest.xml` 檔案、按一下 [功能] 索引標籤，然後確定已核取 [ID_CAP_PUSH_NOTIFICATION] 功能。
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. 按 `F5` 鍵以執行應用程式。
   
    註冊訊息會顯示在應用程式中。
8. 關閉應用程式。  
   
   > [!NOTE]
   > 若要接收快顯推播通知，應用程式不得在前景執行。
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>從後端傳送推播通知
您可以透過公用 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>，使用通知中樞從任何後端傳送推播通知。 在本教學課程中，您將使用 .NET 主控台應用程式來傳送推播通知。 

如需從已與通知中樞整合的 ASP.NET WebAPI 後端傳送推播通知的範例，請參閱 [Azure 通知中樞透過 .NET 後端通知使用者](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)。  

如需使用 [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx) 傳送推播通知的範例，請查看[如何從 Java 使用通知中樞](notification-hubs-java-push-notification-tutorial.md)和[如何從 PHP 使用通知中樞](notification-hubs-php-push-notification-tutorial.md)。

1. 以滑鼠右鍵按一下方案，並選取 [新增] 和 [新增專案...]，然後按一下 [Visual C#] 底下的 [Windows] 和 [主控台應用程式]，再按一下 [確定]。
   
       ![Visual Studio - New Project - Console Application][6]
   
    即會將新的 Visual C# 主控台應用程式新增到方案中。 您也可以在個別方案中進行此項作業。
2. 依序按一下 [工具]、[程式庫套件管理員] 和 [套件管理器主控台]。
   
    這會顯示 [Package Manager Console]。
3. 在 [套件管理員主控台] 視窗中，將 [預設專案] 設為新的主控台應用程式專案，然後在主控台視窗中執行下列命令：
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   這會使用 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 封裝</a>加入對 Azure 通知中樞 SDK 的參考。
4. 開啟 `Program.cs` 檔案，並加入下列 `using` 陳述式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在 `Program` 類別中，新增下列方法：
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    請務必使用出現在入口網站中的通知中樞名稱，來取代 `<hub name>` 預留位置。 此外，請將連接字串預留位置取代為您在＜設定通知中樞＞一節中取得，且名為 **DefaultFullSharedAccessSignature** 的連接字串。
   
   > [!NOTE]
   > 請確定您使用的連接字串具有 [完整] 存取權，而非 [接聽] 存取權。 接聽存取權的字串沒有傳送推播通知的權限。
   > 
   > 
6. 在 `Main` 方法中加入以下這行：
   
         SendNotificationAsync();
         Console.ReadLine();
7. 當您的 Windows Phone 模擬器正在執行且您的應用程式已關閉時，將主控台應用程式專案設為預設啟動專案，然後按 `F5` 鍵來執行應用程式。
   
    您將會收到快顯推播通知。 點選快顯通知即可載入 app。

您可以在 MSDN 上的[快顯目錄]和[圖格目錄]主題中找到所有可能的裝載。

## <a name="next-steps"></a>後續步驟
在此簡單範例中，您會將推播通知廣播到所有 Windows Phone 8 裝置。 

為了鎖定特定使用者，請參閱 [使用通知中樞來推播通知給使用者] 教學課程。 

如果您想要按興趣群組分隔使用者，您可以參閱 [使用通知中心傳送即時新聞]。 

在 [通知中心指引]中深入了解如何使用通知中心。

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[通知中心指引]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[使用通知中樞來推播通知給使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[使用通知中心傳送即時新聞]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[快顯目錄]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[圖格目錄]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[通知中樞 - Windows Phone Silverlight 教學課程]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

