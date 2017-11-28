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
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="742b9-104">在 Windows Phone 上使用 Azure 通知中樞傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="742b9-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="742b9-105">概觀</span><span class="sxs-lookup"><span data-stu-id="742b9-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="742b9-106">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="742b9-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="742b9-107">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="742b9-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="742b9-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="742b9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="742b9-109">本教學課程將示範如何使用 Azure 通知中樞，將推播通知傳送到 Windows Phone 8 或 Windows Phone 8.1 Silverlight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="742b9-110">如果您的目標是 Windows Phone 8.1 (非 Silverlight)，請參閱 [Windows 通用](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 版本。</span><span class="sxs-lookup"><span data-stu-id="742b9-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="742b9-111">在本教學課程中，您將使用 Microsoft 推播通知服務 (MPNS)，建立可接收推播通知的空白 Windows Phone 8 應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="742b9-112">完成時，您便能夠使用通知中樞，將推播通知廣播到所有執行您 app 的裝置。</span><span class="sxs-lookup"><span data-stu-id="742b9-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="742b9-113">通知中樞 Windows Phone SDK 不支援將 Windows 推播通知服務 (WNS) 與 Windows Phone 8.1 Silverlight app 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="742b9-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="742b9-114">若要將 WNS (而非 MPNS) 與 Windows Phone 8.1 Silverlight app 搭配使用，請遵循使用 REST API 的 [通知中樞 - Windows Phone Silverlight 教學課程]。</span><span class="sxs-lookup"><span data-stu-id="742b9-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="742b9-115">本教學課程示範使用通知中樞的簡單廣播案例。</span><span class="sxs-lookup"><span data-stu-id="742b9-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="742b9-116">先決條件</span><span class="sxs-lookup"><span data-stu-id="742b9-116">Prerequisites</span></span>
<span data-ttu-id="742b9-117">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="742b9-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="742b9-118">[Visual Studio 2012 Express for Windows Phone]或更新版本。</span><span class="sxs-lookup"><span data-stu-id="742b9-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="742b9-119">完成本教學課程是 Windows Phone 8 應用程式所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="742b9-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="742b9-120">建立您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="742b9-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="742b9-121">按一下 [通知服務]<b></b> 區段 (在 [設定]<i></i> 中)，按一下 [Windows Phone (MPNS)]<b></b>，然後按一下 [啟用未經驗證的推送]<b></b> 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="742b9-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure 入口網站 - 啟用未經驗證的推播通知](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="742b9-123">現在已建立並設定您的中樞，以傳送未經驗證的 Windows Phone 通知。</span><span class="sxs-lookup"><span data-stu-id="742b9-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="742b9-124">本教學課程使用處於未通過驗證模式的 MPNS。</span><span class="sxs-lookup"><span data-stu-id="742b9-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="742b9-125">MPNS 未通過驗證模式內含您可傳送至每個通道的通知限制。</span><span class="sxs-lookup"><span data-stu-id="742b9-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="742b9-126">通知中樞可讓您上傳憑證，以支援 [MPNS 驗證模式](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="742b9-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="742b9-127">將您的應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="742b9-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="742b9-128">在 Visual Studio 中建立新的 Windows Phone 8 應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="742b9-129">在 Visual Studio 2013 Update 2 或更新版本中，您必須改為建立 Windows Phone Silverlight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - 新增專案 - 空白應用程式 - Windows Phone Silverlight][11]
2. <span data-ttu-id="742b9-131">在 Visual Studio 中，以滑鼠右鍵按一下方案，然後按一下 [管理 NuGet 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="742b9-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="742b9-132">此時會顯示 [管理 NuGet 封裝]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="742b9-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="742b9-133">搜尋 `WindowsAzure.Messaging.Managed`，然後按一下 [安裝] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="742b9-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio - NuGet 封裝管理員][20]
   
    <span data-ttu-id="742b9-135">這會使用 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>來下載、安裝並新增適用於 Windows 的 Azure 傳訊程式庫參考。</span><span class="sxs-lookup"><span data-stu-id="742b9-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="742b9-136">開啟 App.xaml.cs 檔案，並新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="742b9-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="742b9-137">在 App.xaml.cs 中 **Application_Launching** 方法的頂端新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="742b9-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="742b9-138">**MyPushChannel** 值是一個索引，用來查閱 [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) 集合中的現有通道。</span><span class="sxs-lookup"><span data-stu-id="742b9-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="742b9-139">如果集合中沒有任何項目，請以該名稱建立新的項目。</span><span class="sxs-lookup"><span data-stu-id="742b9-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="742b9-140">請確定插入您的中心名稱，及您在上一節中取得、名為 **DefaultListenSharedAccessSignature** 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="742b9-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="742b9-141">此程式碼會從 MPNS 中擷取 app 的通道 URI，然後向您的通知中樞註冊該通道 URI。</span><span class="sxs-lookup"><span data-stu-id="742b9-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="742b9-142">它也保證每次啟動應用程式時，便會在通知中樞中註冊通道 URI。</span><span class="sxs-lookup"><span data-stu-id="742b9-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="742b9-143">本教學課程將傳送快顯通知給裝置。</span><span class="sxs-lookup"><span data-stu-id="742b9-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="742b9-144">傳送磚通知時，您必須在通道上改為呼叫 **BindToShellTile** 方法。</span><span class="sxs-lookup"><span data-stu-id="742b9-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="742b9-145">若要同時支援快顯和圖格通知，請呼叫 **BindToShellTile** 和 **BindToShellToast**。</span><span class="sxs-lookup"><span data-stu-id="742b9-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="742b9-146">在 [方案總管] 中，展開 [屬性]、開啟 `WMAppManifest.xml` 檔案、按一下 [功能] 索引標籤，然後確定已核取 [ID_CAP_PUSH_NOTIFICATION] 功能。</span><span class="sxs-lookup"><span data-stu-id="742b9-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="742b9-147">按 `F5` 鍵以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="742b9-148">註冊訊息會顯示在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="742b9-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="742b9-149">關閉應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="742b9-150">若要接收快顯推播通知，應用程式不得在前景執行。</span><span class="sxs-lookup"><span data-stu-id="742b9-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="742b9-151">從後端傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="742b9-151">Send push notifications from your backend</span></span>
<span data-ttu-id="742b9-152">您可以透過公用 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 介面</a>，使用通知中樞從任何後端傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="742b9-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="742b9-153">在本教學課程中，您將使用 .NET 主控台應用程式來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="742b9-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="742b9-154">如需從已與通知中樞整合的 ASP.NET WebAPI 後端傳送推播通知的範例，請參閱 [Azure 通知中樞透過 .NET 後端通知使用者](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)。</span><span class="sxs-lookup"><span data-stu-id="742b9-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="742b9-155">如需使用 [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx) 傳送推播通知的範例，請查看[如何從 Java 使用通知中樞](notification-hubs-java-push-notification-tutorial.md)和[如何從 PHP 使用通知中樞](notification-hubs-php-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="742b9-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="742b9-156">以滑鼠右鍵按一下方案，並選取 [新增] 和 [新增專案...]，然後按一下 [Visual C#] 底下的 [Windows] 和 [主控台應用程式]，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="742b9-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="742b9-157">即會將新的 Visual C# 主控台應用程式新增到方案中。</span><span class="sxs-lookup"><span data-stu-id="742b9-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="742b9-158">您也可以在個別方案中進行此項作業。</span><span class="sxs-lookup"><span data-stu-id="742b9-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="742b9-159">依序按一下 [工具]、[程式庫套件管理員] 和 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="742b9-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="742b9-160">這會顯示 [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="742b9-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="742b9-161">在 [套件管理員主控台] 視窗中，將 [預設專案] 設為新的主控台應用程式專案，然後在主控台視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="742b9-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="742b9-162">這會使用 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 封裝</a>加入對 Azure 通知中樞 SDK 的參考。</span><span class="sxs-lookup"><span data-stu-id="742b9-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="742b9-163">開啟 `Program.cs` 檔案，並加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="742b9-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="742b9-164">在 `Program` 類別中，新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="742b9-164">In the `Program` class, add the following method:</span></span>
   
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
   
    <span data-ttu-id="742b9-165">請務必使用出現在入口網站中的通知中樞名稱，來取代 `<hub name>` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="742b9-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="742b9-166">此外，請將連接字串預留位置取代為您在＜設定通知中樞＞一節中取得，且名為 **DefaultFullSharedAccessSignature** 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="742b9-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="742b9-167">請確定您使用的連接字串具有 [完整] 存取權，而非 [接聽] 存取權。</span><span class="sxs-lookup"><span data-stu-id="742b9-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="742b9-168">接聽存取權的字串沒有傳送推播通知的權限。</span><span class="sxs-lookup"><span data-stu-id="742b9-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="742b9-169">在 `Main` 方法中加入以下這行：</span><span class="sxs-lookup"><span data-stu-id="742b9-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="742b9-170">當您的 Windows Phone 模擬器正在執行且您的應用程式已關閉時，將主控台應用程式專案設為預設啟動專案，然後按 `F5` 鍵來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="742b9-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="742b9-171">您將會收到快顯推播通知。</span><span class="sxs-lookup"><span data-stu-id="742b9-171">You will receive a toast push notification.</span></span> <span data-ttu-id="742b9-172">點選快顯通知即可載入 app。</span><span class="sxs-lookup"><span data-stu-id="742b9-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="742b9-173">您可以在 MSDN 上的[快顯目錄]和[圖格目錄]主題中找到所有可能的裝載。</span><span class="sxs-lookup"><span data-stu-id="742b9-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="742b9-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="742b9-174">Next steps</span></span>
<span data-ttu-id="742b9-175">在此簡單範例中，您會將推播通知廣播到所有 Windows Phone 8 裝置。</span><span class="sxs-lookup"><span data-stu-id="742b9-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="742b9-176">為了鎖定特定使用者，請參閱 [使用通知中樞來推播通知給使用者] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="742b9-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="742b9-177">如果您想要按興趣群組分隔使用者，您可以參閱 [使用通知中心傳送即時新聞]。</span><span class="sxs-lookup"><span data-stu-id="742b9-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="742b9-178">在 [通知中心指引]中深入了解如何使用通知中心。</span><span class="sxs-lookup"><span data-stu-id="742b9-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="742b9-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="742b9-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="742b9-180">[通知中心指引]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="742b9-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="742b9-181">[使用通知中樞來推播通知給使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="742b9-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="742b9-182">[使用通知中心傳送即時新聞]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="742b9-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="742b9-183">[快顯目錄]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="742b9-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="742b9-184">[圖格目錄]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="742b9-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="742b9-185">[通知中樞 - Windows Phone Silverlight 教學課程]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="742b9-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

