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
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="4d972-103">新增推播通知 tooyour Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d972-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="4d972-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4d972-104">Overview</span></span>
<span data-ttu-id="4d972-105">在本教學課程中，您將加入推播通知 toohello [Windows 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="4d972-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="4d972-106">如果您不要使用 hello 下載快速入門的伺服器專案，您將需要 hello 推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="4d972-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="4d972-107">請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4d972-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="4d972-108"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="4d972-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="4d972-109">針對推播通知註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="4d972-109">Register your app for push notifications</span></span>
<span data-ttu-id="4d972-110">您需要 toosubmit 您應用程式 toohello Windows 市集、，然後設定您的伺服器專案 toointegrate 與 Windows 通知服務 (WNS) toosend 推入。</span><span class="sxs-lookup"><span data-stu-id="4d972-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="4d972-111">在 Visual Studio 方案總管 中，以滑鼠右鍵按一下 hello UWP 應用程式專案，按一下**存放區** > **將應用程式建立關聯以 hello 存放區...**.</span><span class="sxs-lookup"><span data-stu-id="4d972-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="4d972-113">在 hello 精靈中，按一下 **下一步**，使用您的 Microsoft 帳戶登入，輸入您的應用程式中的名稱**新的應用程式名稱保留**，然後按一下 **保留**。</span><span class="sxs-lookup"><span data-stu-id="4d972-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="4d972-114">Hello 應用程式註冊已成功建立，請選取 hello 新應用程式名稱後，請按一下**下一步**，然後按一下**關聯**。</span><span class="sxs-lookup"><span data-stu-id="4d972-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="4d972-115">這會將所需的 hello Windows 市集註冊資訊 toohello 應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="4d972-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="4d972-116">瀏覽 toohello [Windows 開發人員中心](https://dev.windows.com/en-us/overview)，使用您的 Microsoft 帳戶登入，按一下 hello 新應用程式註冊在**我的應用程式**，然後展開**服務** > **推播通知**。</span><span class="sxs-lookup"><span data-stu-id="4d972-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="4d972-117">在 hello**推播通知**頁面上，按一下**Live 服務 」 站台**下**Microsoft Azure 行動服務**。</span><span class="sxs-lookup"><span data-stu-id="4d972-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="4d972-118">在 hello 註冊頁面中，記下 hello 值**應用程式密碼**和 hello**封裝 SID**，而您接著可以將 tooconfigure 您的行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="4d972-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4d972-120">hello 用戶端密碼和封裝 SID 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="4d972-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="4d972-121">請勿與任何人共用這些值，或與您的應用程式一起散發密碼。</span><span class="sxs-lookup"><span data-stu-id="4d972-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="4d972-122">hello**應用程式識別碼**hello 秘密 tooconfigure Microsoft 帳戶驗證搭配使用。</span><span class="sxs-lookup"><span data-stu-id="4d972-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="4d972-123">設定 hello 後端 toosend 推播通知</span><span class="sxs-lookup"><span data-stu-id="4d972-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="4d972-124"><a id="update-service"></a>更新 hello 伺服器 toosend 推播通知</span><span class="sxs-lookup"><span data-stu-id="4d972-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="4d972-125">使用 hello 面的程序符合您的後端專案類型&mdash;任一[.NET 後端](#dotnet)或[Node.js 後端](#nodejs)。</span><span class="sxs-lookup"><span data-stu-id="4d972-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="4d972-126"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="4d972-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="4d972-127">在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**、 搜尋 Microsoft.Azure.NotificationHubs，然後按一下 **安裝**。</span><span class="sxs-lookup"><span data-stu-id="4d972-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="4d972-128">這會安裝 hello 通知中樞的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4d972-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="4d972-129">展開**控制器**，開啟 TodoItemController.cs，並加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="4d972-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="4d972-130">在 hello **PostTodoItem**方法，新增下列程式碼 hello 呼叫之後，太 hello**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="4d972-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

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

    <span data-ttu-id="4d972-131">此程式碼插入新項目之後，告知 hello 通知中樞 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="4d972-132">重新發佈 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="4d972-132">Republish hello server project.</span></span>

### <span data-ttu-id="4d972-133"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="4d972-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="4d972-134">如果您沒有這樣做，[下載 hello 快速入門專案](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)或其他使用 hello [hello Azure 入口網站中的線上編輯器](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="4d972-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="4d972-135">取代 hello 下列 hello hello todoitem.js 檔案中的現有程式碼：</span><span class="sxs-lookup"><span data-stu-id="4d972-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

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

    <span data-ttu-id="4d972-136">這會傳送新的 todo 項目插入時，包含 hello item.text WNS 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="4d972-137">編輯本機電腦上的 hello 檔案時，重新發行 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="4d972-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="4d972-138"><a id="update-app"></a>新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d972-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="4d972-139">接下來，您的應用程式必須在啟動時註冊推播通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="4d972-140">當您已啟用驗證時，請確定該 hello 使用者登入時才會嘗試 tooregister 推播通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="4d972-141">開啟 hello **App.xaml.cs**專案檔案，並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4d972-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="4d972-142">在 hello 同一個檔案中新增 hello 下列**InitNotificationsAsync**方法定義 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="4d972-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="4d972-143">此程式碼會從 WNS，擷取 hello ChannelURI hello 應用程式，並使用 App Service 行動應用程式，然後註冊該 ChannelURI。</span><span class="sxs-lookup"><span data-stu-id="4d972-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="4d972-144">頂端的 hello hello **OnLaunched**中的事件處理常式**App.xaml.cs**，新增 hello**非同步**修飾詞 toohello 方法定義並加入 hello 下列呼叫 toohello 新**InitNotificationsAsync**方法，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="4d972-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="4d972-145">這可確保每次啟動 hello 應用程式註冊存留較短的 ChannelURI 該 hello。</span><span class="sxs-lookup"><span data-stu-id="4d972-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="4d972-146">重建 UWP 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="4d972-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="4d972-147">您的應用程式現在已準備好 tooreceive 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="4d972-148"><a id="test"></a>在應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="4d972-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="4d972-149"><a id="more"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="4d972-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="4d972-150">進一步了解推播通知︰</span><span class="sxs-lookup"><span data-stu-id="4d972-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="4d972-151">Toouse hello 如何管理 Azure 行動應用程式的用戶端</span><span class="sxs-lookup"><span data-stu-id="4d972-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="4d972-152">範本可讓您彈性 toosend 跨平台的推送和當地語系化的推播通知。</span><span class="sxs-lookup"><span data-stu-id="4d972-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="4d972-153">深入了解如何 tooregister 範本。</span><span class="sxs-lookup"><span data-stu-id="4d972-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="4d972-154">診斷推播通知問題</span><span class="sxs-lookup"><span data-stu-id="4d972-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="4d972-155">通知遭到捨棄或未抵達裝置有各種原因。</span><span class="sxs-lookup"><span data-stu-id="4d972-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="4d972-156">本主題說明如何 tooanalyze 並找出 hello 根原因的推送通知失敗。</span><span class="sxs-lookup"><span data-stu-id="4d972-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="4d972-157">請考慮 tooone hello 遵循教學課程的上繼續進行：</span><span class="sxs-lookup"><span data-stu-id="4d972-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="4d972-158">新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d972-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="4d972-159">深入了解如何 tooauthenticate 使用者身分識別提供者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d972-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="4d972-160">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="4d972-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="4d972-161">了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d972-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="4d972-162">離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="4d972-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
