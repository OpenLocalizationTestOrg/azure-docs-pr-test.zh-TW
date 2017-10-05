---
title: "將推播通知新增至您的通用 Windows 平台 (UWP) 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure App Service Mobile Apps 與 Azure 通知中樞，將推播通知傳送至通用 Windows 平台 (UWP) 應用程式。"
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
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="1c8ce-103">將推播通知加入至 Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="1c8ce-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="1c8ce-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1c8ce-104">Overview</span></span>
<span data-ttu-id="1c8ce-105">在本教學課程中，您會將推播通知新增至 [Windows 快速入門](app-service-mobile-windows-store-dotnet-get-started.md)專案，以便在每次插入一筆記錄時傳送推播通知至裝置。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="1c8ce-106">如果您不要使用下載的快速入門伺服器專案，將需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="1c8ce-107">如需詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="1c8ce-108"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="1c8ce-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="1c8ce-109">針對推播通知註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="1c8ce-109">Register your app for push notifications</span></span>
<span data-ttu-id="1c8ce-110">您需要將應用程式提交至 Windows 市集，然後設定您的伺服器專案，以與 Windows 通知服務 (WNS) 整合來傳送推播。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="1c8ce-111">在 Visual Studio 方案總管中，以滑鼠右鍵按一下 UWP 應用程式專案，然後按一下 [市集]  >  [將應用程式與市集建立關聯...]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="1c8ce-113">在精靈中按 [下一步]，使用 Microsoft 帳戶登入，在 [保留新的應用程式名稱] 中輸入您應用程式的名稱，然後按一下 [保留]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="1c8ce-114">成功建立應用程式註冊之後，選取新的應用程式名稱，按 [下一步]，然後按一下 [關聯]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="1c8ce-115">這會將所需的 Windows 市集註冊資訊新增至應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="1c8ce-116">瀏覽至 [Windows 開發人員中心](https://dev.windows.com/en-us/overview)、使用您的 Microsoft 帳戶登入、在 [我的應用程式] 中按一下 [新增應用程式註冊]，然後展開 [服務]  >  [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="1c8ce-117">在 [推播通知] 頁面上，按一下 [Microsoft Azure 行動服務] 底下的 [線上服務網站]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="1c8ce-118">在註冊頁面中，記下 [應用程式祕密] 和 [套件 SID] 底下的值，以在接下來用來設定您的行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="1c8ce-120">用戶端密碼和封裝 SID 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="1c8ce-121">請勿與任何人共用這些值，或與您的應用程式一起散發密碼。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="1c8ce-122">**應用程式識別碼** 會與密碼搭配用來設定 Microsoft 帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="1c8ce-123">設定後端來傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="1c8ce-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="1c8ce-124"><a id="update-service"></a>更新伺服器以傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="1c8ce-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="1c8ce-125">使用下列符合您後端專案類型的程序 &mdash;[.NET 後端](#dotnet)或 [Node.js 後端](#nodejs)。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="1c8ce-126"><a name="dotnet"></a>.NET 後端專案</span><span class="sxs-lookup"><span data-stu-id="1c8ce-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="1c8ce-127">在 Visual Studio 中，以滑鼠右鍵按一下伺服器專案並按一下 [管理 NuGet 套件]，搜尋 Microsoft.Azure.NotificationHubs，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="1c8ce-128">這會安裝通知中樞用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="1c8ce-129">展開 [Controllers] ，開啟 [TodoItemController.cs]，然後新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="1c8ce-130">在 **PostTodoItem** 方法中，於呼叫 **InsertAsync** 之後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="1c8ce-131">此程式碼會告訴通知中樞在插入新項目之後傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="1c8ce-132">發佈伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-132">Republish the server project.</span></span>

### <span data-ttu-id="1c8ce-133"><a name="nodejs"></a>Node.js 後端專案</span><span class="sxs-lookup"><span data-stu-id="1c8ce-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="1c8ce-134">如果您還沒這麼做，請[下載快速入門專案](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)或使用 [Azure 入口網站中的線上編輯器](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="1c8ce-135">在 todoitem.js 檔案中，以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="1c8ce-136">插入新的 todo 項目時，這會傳送包含 item.text 的 WNS 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="1c8ce-137">當您在本機電腦上編輯檔案時，請重新發佈伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="1c8ce-138"><a id="update-app"></a>將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="1c8ce-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="1c8ce-139">接下來，您的應用程式必須在啟動時註冊推播通知。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="1c8ce-140">當您已啟用驗證時，請確定使用者在嘗試註冊推播通知之前已登入。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="1c8ce-141">開啟 **App.xaml.cs** 專案檔案，並新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="1c8ce-142">在相同檔案中，將下列 **InitNotificationsAsync** 方法定義新增至 [應用程式] 類別：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="1c8ce-143">此程式碼會從 WNS 中擷取應用程式的 ChannelURI，然後向您的應用程式服務行動應用程式註冊該 ChannelURI。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="1c8ce-144">在 **App.xaml.cs** 中 **OnLaunched** 事件處理常式的頂端，將 **async** 修飾詞新增到方法定義中，並將下列呼叫新增到新的 **InitNotificationsAsync** 方法中，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="1c8ce-145">這樣可保證在每次啟動應用程式時都會註冊存留期較短的 ChannelURI。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="1c8ce-146">重建 UWP 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="1c8ce-147">您的應用程式現在已能夠接收快顯通知。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="1c8ce-148"><a id="test"></a>在應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="1c8ce-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="1c8ce-149"><a id="more"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="1c8ce-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="1c8ce-150">進一步了解推播通知︰</span><span class="sxs-lookup"><span data-stu-id="1c8ce-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="1c8ce-151">如何針對 Azure Mobile Apps 使用受管理的用戶端</span><span class="sxs-lookup"><span data-stu-id="1c8ce-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="1c8ce-152">：範本可讓您彈性地傳送跨平台推播和當地語系化推播。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="1c8ce-153">了解如何註冊範本。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="1c8ce-154">診斷推播通知問題</span><span class="sxs-lookup"><span data-stu-id="1c8ce-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="1c8ce-155">通知遭到捨棄或未抵達裝置有各種原因。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="1c8ce-156">本主題說明如何分析及找出推播通知失敗的根本原因。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="1c8ce-157">請考慮繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="1c8ce-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="1c8ce-158">將驗證加入應用程式中</span><span class="sxs-lookup"><span data-stu-id="1c8ce-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="1c8ce-159">：了解如何使用識別提供者來驗證應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="1c8ce-160">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="1c8ce-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="1c8ce-161">了解如何使用行動應用程式後端，將離線支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="1c8ce-162">離線同步處理可讓使用者與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="1c8ce-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
