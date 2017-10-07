---
title: "開始使用 Azure 通知中樞為 Windows 通用平台應用程式的 aaaGet |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooa Windows 通用平台應用程式。"
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>開始使用適用於 Windows 通用平台應用程式的通知中樞
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 通用 Windows 平台 (UWP) 應用程式。

在本教學課程中，您可以建立空白的 Windows 市集應用程式透過使用 Windows 推播通知服務 (WNS) hello 接收推播通知。 完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。

## <a name="before-you-begin"></a>開始之前
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

hello 完成本教學課程中的程式碼可以在 GitHub 上找到[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)。

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 或更新版本
* [已安裝通用 Windows 應用程式開發工具](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* 作用中的 Azure 帳戶  <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)。
* 有效的 Windows 市集帳戶

完成本教學課程是 Windows 通用平台應用程式所有其他通知中樞教學課程的先決條件。

## <a name="register-your-app-for-hello-windows-store"></a>註冊 hello Windows 市集應用程式
toosend 推播通知 tooUWP 應用程式，您必須使您的應用程式 toohello Windows 市集。 接著，您必須設定您的通知中樞 toointegrate 搭配 WNS。

1. 如果您沒有註冊您的應用程式，請瀏覽 toohello [Windows 開發人員中心](https://dev.windows.com/overview)，使用您的 Microsoft 帳戶登入，然後按一下**建立新的應用程式**。

2. 輸入您的 App 名稱，然後按一下 [保留應用程式名稱] 。 這會為您的應用程式建立新的 Windows 市集註冊。

3. 在 Visual Studio 中，建立新的 Visual C# 市集應用程式專案使用 Windows 通用 hello**空白應用程式**範本，然後按一下**確定**。

4. 接受 hello hello 目標與最低平台版本的預設值。

5. 在 [方案總管] 中，以滑鼠右鍵按一下 hello Windows 市集應用程式專案中，按一下 [**存放區**，然後按一下**將應用程式建立關聯以 hello 存放區...**。 hello**您應用程式建立關聯以 hello Windows 市集**精靈] 隨即出現。

6. 在 hello 精靈中，使用登入您的 Microsoft 帳戶。

7. 按一下 註冊，讓您在步驟 2 中的 hello 應用程式中，按一下**下一步**，然後按一下**關聯**。 這會將所需的 hello Windows 市集註冊資訊 toohello 應用程式資訊清單。

8. 在 hello [Windows 開發人員中心](http://dev.windows.com/overview)新應用程式頁面上，按一下**服務**，按一下 **推播通知**，然後按一下**WNS/MPNS**。

9. 按一下 [新增通知]。

10. 按一下 空白 (快顯) 範本，然後按一下確定。

11. 輸入通知 [名稱] 和視覺化 [內容] 訊息。 然後按一下 [儲存為草稿]。

12. 瀏覽 toohello[應用程式註冊入口網站](http://apps.dev.microsoft.com)並登入。

13. 按一下您的應用程式名稱。 請記下 hello**應用程式密碼**密碼和 hello**封裝安全性識別碼 (SID)**位於 hello **Windows 市集**平台設定。

     > [AZURE.WARNING]
    hello 應用程式密碼和封裝 SID 是重要的安全性認證。 請勿與任何人共用這些值，或與您的應用程式一起散發密碼。

## <a name="configure-your-notification-hub"></a>設定您的通知中樞
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>選取 hello <b>Notification Services</b>選項和 hello <b>Windows (WNS)</b>選項。 然後輸入 hello<b>應用程式密碼</b>密碼 hello<b>安全性金鑰</b>欄位。 輸入您<b>封裝 SID</b>值取自 WNS hello 前一節中，然後再按一下<b>儲存</b>。</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

您的通知中樞現在是設定的 toowork 搭配 WNS，而且您擁有 hello 連接字串 tooregister 您的應用程式，並將傳送通知。

## <a name="connect-your-app-toohello-notification-hub"></a>連接您的應用程式 toohello 通知中樞
1. 在 Visual Studio 中，hello 方案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。
   
    這會顯示 hello**管理 NuGet 封裝** 對話方塊。
2. 搜尋`WindowsAzure.Messaging.Managed`按一下**安裝**，並接受使用規定 hello。
   
    ![][20]
   
    這會下載、 安裝，並將適用於 Windows 的參考 toohello Azure 訊息文件庫，使用 hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>。
3. 開啟 hello App.xaml.cs 專案檔，然後加入下列 hello`using`陳述式。 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. 也在 App.xaml.cs，加入 hello 下列**InitNotificationsAsync**方法定義 toohello**應用程式**類別：
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    這個程式碼 hello 應用程式的 hello 通道 URI 擷取 WNS，並使用通知中樞，然後註冊該通道 URI。
   
   > [!NOTE]
   > 請確定 tooreplace hello hello 名稱出現在 hello Azure 入口網站中的 hello 通知中樞的 「 中樞名稱 」 預留位置。 也將 hello 連接字串預留位置取代 hello **DefaultListenSharedAccessSignature**連接字串，您取得的 hello**存取原則**通知中樞 頁面上一節。
   > 
   > 
5. 頂端的 hello hello **OnLaunched** App.xaml.cs，事件處理常式新增下列新的呼叫 toohello hello **InitNotificationsAsync**方法：
   
        InitNotificationsAsync();
   
    這可確保該 hello 通道，在您每次 hello 應用程式啟動的通知中樞已註冊的 URI。
6. 按 hello **F5**金鑰 toorun hello 應用程式。 會顯示快顯的對話方塊，其中包含 hello 登錄機碼。

您的應用程式現在已準備好 tooreceive 快顯通知。

## <a name="send-notifications"></a>傳送通知
您可以快速測試您的應用程式中接收通知，傳送通知給 hello 以[Azure 入口網站](https://portal.azure.com/)使用 hello**測試傳送**按鈕在 hello 通知中樞內，囉 」 畫面下方所示。

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

推播通知通常會以後端服務傳送，例如行動服務或使用相容程式庫的 ASP.NET。 您也可以使用 hello REST API 直接 toosend 通知訊息，如果文件庫不適用於您的後端。 

在本教學課程中，我們將保持簡單，並只示範測試用戶端應用程式透過傳送 hello.NET SDK 使用通知中心，而不是後端服務的主控台應用程式的通知。 我們建議 hello[使用通知中樞 toopush 通知 toousers]教學課程為 hello 下一個步驟，從 ASP.NET 後端傳送通知。 不過，hello 下列方法可用來傳送通知：

* **REST 介面**： 您可以使用 hello 任何後端平台上支援通知[REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)。
* **Microsoft Azure 通知中樞.NET SDK**: hello for Visual Studio 的 Nuget 封裝管理員，在執行[Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。
* **Node.js** :[如何 toouse 通知中樞，從 Node.js](notification-hubs-nodejs-push-notification-tutorial.md)。
* **Azure 行動應用程式**： 如需如何 toosend 通知從 Azure 行動應用程式與通知中樞整合，請參閱[行動應用程式的新增推播通知](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)。
* **Java / PHP**： 如需如何使用 toosend 通知 hello REST Api 的範例，請參閱 「 如何 toouse 來自 Java/PHP 的通知中心 」 ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。

## <a name="optional-send-notifications-from-a-console-app"></a>(選擇性) 從主控台應用程式傳送通知
使用.NET 主控台應用程式的 toosend 通知，請遵循下列步驟。 

1. 以滑鼠右鍵按一下 hello 方案中，選取**新增**和**新的專案...**，，然後在**Visual C#**，按一下  **Windows**和**主控台應用程式**，然後按一下**確定**。
   
    這會將新 Visual C# 主控台應用程式 toohello 方案。 您也可以在個別方案中進行此項作業。

2. 在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。
   
    這是 Visual Studio 中顯示 hello Package Manager Console。
3. 在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. 開啟 hello Program.cs 檔案並加入下列 hello`using`陳述式：
   
        using Microsoft.Azure.NotificationHubs;
5. 在 hello**程式**類別中，新增下列方法 hello:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > 請確定您使用 hello 連接字串具有**完整**不存取**接聽**存取。 hello 接聽存取字串不具有權限 toosend 通知。
   > 
   > 
6. 加入下列行 hello hello **Main**方法：
   
         SendNotificationAsync();
         Console.ReadLine();
7. 在 Visual Studio 中的 hello 主控台應用程式專案上按一下滑鼠右鍵，然後按一下**設定為啟始專案**tooset 它為 hello 啟始專案。 然後按 hello **F5**金鑰 toorun hello 應用程式。
   
    您將會在所有註冊裝置上收到快顯通知。 按一下或點選 hello 快顯通知橫幅載入 hello 應用程式。

您可以在 hello 找到所有支援的 hello 裝載[快顯通知目錄]，[磚目錄]，和[徽章概觀]MSDN 上的主題。

## <a name="next-steps"></a>後續步驟
在這個簡單的範例中，您傳送廣播的通知 tooall hello 入口網站或主控台應用程式使用 Windows 裝置。 我們建議 hello[使用通知中樞 toopush 通知 toousers] hello 下一個步驟的教學課程。 它會顯示如何從 ASP.NET 後端使用 toosend 通知標記 tootarget 特定使用者。

如果您希望 toosegment 使用者感興趣的群組，請參閱[使用通知中樞 toosend 最新消息]。 

toolearn 通知中樞的相關詳細資訊，請參閱[通知中樞指引](notification-hubs-push-notification-overview.md)。

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[使用通知中樞 toopush 通知 toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[快顯通知目錄]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[磚目錄]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[徽章概觀]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
