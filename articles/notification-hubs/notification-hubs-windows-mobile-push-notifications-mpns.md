---
title: "與 Windows Phone 上的 Azure 通知中心 aaaSending 推播通知 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooa Windows Phone 8 或 Windows Phone 8.1 Silverlight 應用程式。"
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
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>在 Windows Phone 上使用 Azure 通知中樞傳送推播通知
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F)。
> 
> 

本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa Windows Phone 8 或 Windows Phone 8.1 Silverlight 應用程式。 如果您的目標 Windows Phone 8.1 (非 Silverlight)，則參考 toohello [Windows 通用](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)版本。
在本教學課程中，您可以建立空白的 Windows Phone 8 應用程式透過使用 Microsoft 推播通知服務 (MPNS) hello 接收推播通知。 完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。

> [!NOTE]
> hello 通知中樞 Windows Phone SDK 不支援使用 Windows Phone 8.1 Silverlight 應用程式中的 hello Windows 推播通知服務 (WNS)。 toouse WNS （而不是 MPNS) 與 Windows Phone 8.1 Silverlight 應用程式，請遵循 hello[通知中樞-Windows Phone Silverlight 教學課程]，它會使用 REST Api。
> 
> 

hello 教學課程示範 hello 簡單廣播的案例中使用通知中樞。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* [Visual Studio 2012 Express for Windows Phone]或更新版本。

完成本教學課程是 Windows Phone 8 應用程式所有其他通知中樞教學課程的先決條件。

## <a name="create-your-notification-hub"></a>建立您的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>按一下 hello <b>Notification Services</b> > 一節 (內<i>設定</i>)，按一下<b>Windows Phone (MPNS)</b>然後按一下hello<b>啟用未經驗證的推送</b>核取方塊。</p>
</li>
</ol>

&emsp;&emsp;![Azure 入口網站 - 啟用未經驗證的推播通知](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

您的中樞現在是適用於 Windows Phone 的已建立並設定 toosend 未經驗證的通知。

> [!NOTE]
> 本教學課程使用處於未通過驗證模式的 MPNS。 MPNS 驗證的模式會隨附您可以將 tooeach 通道傳送通知的限制。 通知中心支援[MPNS 驗證模式](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx)可讓您 tooupload 您的憑證。
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>連接您的應用程式 toohello 通知中樞
1. 在 Visual Studio 中建立新的 Windows Phone 8 應用程式。
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    在 Visual Studio 2013 Update 2 或更新版本中，您必須改為建立 Windows Phone Silverlight 應用程式。
   
    ![Visual Studio - 新增專案 - 空白應用程式 - Windows Phone Silverlight][11]
2. 在 Visual Studio 中，hello 方案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。
   
    這會顯示 hello**管理 NuGet 封裝** 對話方塊。
3. 搜尋`WindowsAzure.Messaging.Managed`按一下**安裝**，並接受使用規定 hello。
   
    ![Visual Studio - NuGet 封裝管理員][20]
   
    這會下載、 安裝，並將適用於 Windows 的參考 toohello Azure 訊息文件庫，使用 hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>。
4. 開啟 hello 檔案 App.xaml.cs 並加入下列 hello`using`陳述式：
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. 新增下列程式碼頂端的 hello hello **Application_Launching** App.xaml.cs 中的方法：
   
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
   > hello 值**MyPushChannel**索引所使用的 toolookup 現有通道在 hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx)集合。 如果集合中沒有任何項目，請以該名稱建立新的項目。
   > 
   > 
   
    請確定 tooinsert hello 中樞和 hello 連接字串名稱呼叫**DefaultListenSharedAccessSignature** hello 上一節中取得。
    這個程式碼 hello 應用程式的 hello 通道 URI 擷取 MPNS，並使用通知中樞，然後註冊該通道 URI。 它也可保證該 hello 通道，在您每次 hello 應用程式啟動的通知中樞已註冊的 URI。
   
   > [!NOTE]
   > 本教學課程傳送快顯通知 toohello 裝置。 當您傳送磚通知時，您必須改為呼叫 hello **BindToShellTile** hello 通道上的方法。 toosupport 快顯通知和磚通知，請呼叫兩者**BindToShellTile**和**BindToShellToast**。
   > 
   > 
6. 在 [方案總管] 中，展開**屬性**，開啟 hello`WMAppManifest.xml`檔案，請按一下 hello**功能**索引標籤，並確定該 hello **ID_CAP_PUSH_NOTIFICATION**會檢查功能。
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. 按 hello`F5`金鑰 toorun hello 應用程式。
   
    登錄訊息會顯示在 hello 應用程式。
8. 關閉 hello 應用程式。  
   
   > [!NOTE]
   > tooreceive 快顯通知推播通知，不可在 hello 前景執行 hello 應用程式。
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>從後端傳送推播通知
您可以從任何後端 hello 公用透過使用通知中樞傳送推播通知<a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>。 在本教學課程中，您將使用 .NET 主控台應用程式來傳送推播通知。 

如需如何 toosend 推播通知從 ASP.NET WebAPI 後端與通知中樞整合，請參閱[Azure 通知中樞通知使用者與.NET 後端](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)。  

如需如何使用 toosend 推播通知 hello [REST Api](https://msdn.microsoft.com/library/azure/dn223264.aspx)，簽出[如何 toouse 通知中樞，從 Java](notification-hubs-java-push-notification-tutorial.md)和[如何 toouse 通知中樞，從 PHP](notification-hubs-php-push-notification-tutorial.md).

1. 以滑鼠右鍵按一下 hello 方案中，選取**新增**和**新的專案...**，，然後在**Visual C#**，按一下  **Windows**和**主控台應用程式**，然後按一下**確定**。
   
       ![Visual Studio - New Project - Console Application][6]
   
    這會將新 Visual C# 主控台應用程式 toohello 方案。 您也可以在個別方案中進行此項作業。
2. 依序按一下 [工具]、[程式庫套件管理員] 和 [套件管理器主控台]。
   
    這會顯示 hello Package Manager Console。
3. 在 hello **Package Manager Console**視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
4. 開啟 hello`Program.cs`檔案，然後加入下列 hello`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在 hello`Program`類別中，新增下列方法 hello:
   
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
   
    請確定 tooreplace hello `<hub name>` hello hello hello 入口網站中顯示的通知中樞名稱的預留位置。 此外，取代呼叫 hello 連接字串中的 hello 連接字串預留位置**DefaultFullSharedAccessSignature**您取得的 hello > 一節中的 < 設定您的通知中樞。 」
   
   > [!NOTE]
   > 請確定您使用連接字串 hello**完整**不存取**接聽**存取。 hello 接聽存取字串不具有權限 toosend 推播通知。
   > 
   > 
6. 加入下列行中的 hello 您`Main`方法：
   
         SendNotificationAsync();
         Console.ReadLine();
7. Windows Phone 模擬器執行和應用程式已關閉，請設定 hello 主控台應用程式專案為 hello 預設啟始專案，再按 hello`F5`金鑰 toorun hello 應用程式。
   
    您將會收到快顯推播通知。 點選 hello 快顯通知橫幅載入 hello 應用程式。

您可以在 hello 找到所有 hello 可能裝載[快顯通知目錄]和[磚目錄]MSDN 上的主題。

## <a name="next-steps"></a>後續步驟
在這個簡單的範例中，您傳播推播通知 tooall Windows Phone 8 裝置。 

在排序 tootarget 特定使用者，請參閱 toohello[使用通知中樞 toopush 通知 toousers]教學課程。 

如果您想 toosegment 您感興趣群組的使用者，您可以閱讀[使用通知中樞 toosend 最新消息]。 

深入了解如何在 toouse 通知中樞[通知中樞指引]。

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
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[使用通知中樞 toopush 通知 toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[快顯通知目錄]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[磚目錄]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[通知中樞-Windows Phone Silverlight 教學課程]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

