---
title: "aaaAdd 推播通知 tooyour 通用 Windows 平台 (UWP) 應用程式 |Microsoft 文件"
description: "了解如何 toouse Azure App Service 行動應用程式與 Azure 通知中樞 toosend 推播通知 tooyour 通用 Windows 平台 (UWP) 應用程式。"
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>新增推播通知 tooyour Windows 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您將加入推播通知 toohello [Windows 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。 請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。

## <a name="configure-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>針對推播通知註冊應用程式
您需要 toosubmit 您應用程式 toohello Windows 市集、，然後設定您的伺服器專案 toointegrate 與 Windows 通知服務 (WNS) toosend 推入。

1. 在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello UWP 應用程式專案，按一下**存放區** > **將應用程式建立關聯以 hello 存放區...**.

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. 在 hello 精靈中，按一下 **下一步**，使用您的 Microsoft 帳戶登入，輸入您的應用程式中的名稱**新的應用程式名稱保留**，然後按一下 **保留**。
3. Hello 應用程式註冊已成功建立，請選取 hello 新應用程式名稱後，請按一下**下一步**，然後按一下**關聯**。 這會將所需的 hello Windows 市集註冊資訊 toohello 應用程式資訊清單。  
4. 瀏覽 toohello [Windows 開發人員中心](https://dev.windows.com/en-us/overview)，使用您的 Microsoft 帳戶登入，按一下 hello 新應用程式註冊在**我的應用程式**，然後展開**服務** > **推播通知**。
5. 在 hello**推播通知**頁面上，按一下**Live 服務 」 站台**下**Microsoft Azure 行動服務**。
6. 在 hello 註冊頁面中，記下 hello 值**應用程式密碼**和 hello**封裝 SID**，而您接著可以將 tooconfigure 您的行動裝置應用程式後端。

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > hello 用戶端密碼和封裝 SID 是重要的安全性認證。 請勿與任何人共用這些值，或與您的應用程式一起散發密碼。 hello**應用程式識別碼**hello 秘密 tooconfigure Microsoft 帳戶驗證搭配使用。
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>設定 hello 後端 toosend 推播通知
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>更新 hello 伺服器 toosend 推播通知
使用 hello 面的程序符合您的後端專案類型&mdash;任一[.NET 後端](#dotnet)或[Node.js 後端](#nodejs)。

### <a name="dotnet"></a>.NET 後端專案
1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**、 搜尋 Microsoft.Azure.NotificationHubs，然後按一下 **安裝**。 這會安裝 hello 通知中樞的用戶端程式庫。
2. 展開**控制器**，開啟 TodoItemController.cs，並加入 hello 下列 using 陳述式：

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. 在 hello **PostTodoItem**方法，新增下列程式碼 hello 呼叫之後，太 hello**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    此程式碼插入新項目之後，告知 hello 通知中樞 toosend 推播通知。
4. 重新發佈 hello 伺服器專案。

### <a name="nodejs"></a>Node.js 後端專案
1. 如果您沒有這樣做，[下載 hello 快速入門專案](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)或其他使用 hello [hello Azure 入口網站中的線上編輯器](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。
2. 取代 hello 下列 hello hello todoitem.js 檔案中的現有程式碼：

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    這會傳送新的 todo 項目插入時，包含 hello item.text WNS 快顯通知。
3. 編輯本機電腦上的 hello 檔案時，重新發行 hello 伺服器專案。

## <a id="update-app"></a>新增推播通知 tooyour 應用程式
接下來，您的應用程式必須在啟動時註冊推播通知。 當您已啟用驗證時，請確定該 hello 使用者登入時才會嘗試 tooregister 推播通知。

1. 開啟 hello **App.xaml.cs**專案檔案，並加入下列 hello`using`陳述式：

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. 在 hello 同一個檔案中新增 hello 下列**InitNotificationsAsync**方法定義 toohello**應用程式**類別：

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    此程式碼會從 WNS，擷取 hello ChannelURI hello 應用程式，並使用 App Service 行動應用程式，然後註冊該 ChannelURI。
3. 頂端的 hello hello **OnLaunched**中的事件處理常式**App.xaml.cs**，新增 hello**非同步**修飾詞 toohello 方法定義並加入 hello 下列呼叫 toohello 新**InitNotificationsAsync**方法，如 hello 下列範例所示：

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    這可確保每次啟動 hello 應用程式註冊存留較短的 ChannelURI 該 hello。
4. 重建 UWP 應用程式專案。 您的應用程式現在已準備好 tooreceive 快顯通知。

## <a id="test"></a>在應用程式中測試推播通知
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>接續步驟
進一步了解推播通知︰

* [Toouse hello 如何管理 Azure 行動應用程式的用戶端](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  範本可讓您彈性 toosend 跨平台的推送和當地語系化的推播通知。 深入了解如何 tooregister 範本。
* [診斷推播通知問題](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  通知遭到捨棄或未抵達裝置有各種原因。 本主題說明如何 tooanalyze 並找出 hello 根原因的推送通知失敗。

請考慮 tooone hello 遵循教學課程的上繼續進行：

* [新增驗證 tooyour 應用程式](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。
* [啟用應用程式的離線同步處理](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。 離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
