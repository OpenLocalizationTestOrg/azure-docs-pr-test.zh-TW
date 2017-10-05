---
title: "開始使用適用於 Windows 通用平台應用程式的 Azure 通知中樞 | Microsoft Docs"
description: "在本教學課程中，您將了解如何使用 Azure 通知中樞，將通知推播至 Windows 通用平台應用程式。"
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
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="be598-103">開始使用適用於 Windows 通用平台應用程式的通知中樞</span><span class="sxs-lookup"><span data-stu-id="be598-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="be598-104">概觀</span><span class="sxs-lookup"><span data-stu-id="be598-104">Overview</span></span>
<span data-ttu-id="be598-105">本教學課程將說明如何使用 Azure 通知中樞將推播通知傳送至 Windows 通用平台 (UWP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="be598-106">在本教學課程中，您將使用 Windows 推播通知服務 (WNS)，建立可接收推播通知的空白 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="be598-107">完成時，您便能夠使用通知中樞，將推播通知廣播到所有執行您 app 的裝置。</span><span class="sxs-lookup"><span data-stu-id="be598-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="be598-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="be598-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="be598-109">您可以在 [此處](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)的 GitHub 上找到本教學課程的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="be598-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be598-110">先決條件</span><span class="sxs-lookup"><span data-stu-id="be598-110">Prerequisites</span></span>
<span data-ttu-id="be598-111">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="be598-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="be598-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="be598-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="be598-113">已安裝通用 Windows 應用程式開發工具</span><span class="sxs-lookup"><span data-stu-id="be598-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="be598-114">作用中的 Azure 帳戶 </span><span class="sxs-lookup"><span data-stu-id="be598-114">An active Azure account</span></span> <br/><span data-ttu-id="be598-115">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="be598-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="be598-116">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="be598-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="be598-117">有效的 Windows 市集帳戶</span><span class="sxs-lookup"><span data-stu-id="be598-117">An active Windows Store account</span></span>

<span data-ttu-id="be598-118">完成本教學課程是 Windows 通用平台應用程式所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="be598-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="be598-119">向 Windows 市集註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="be598-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="be598-120">若要傳送推播通知給 Windows UWP 應用程式，您必須將您的應用程式與 Windows 市集產生關聯。</span><span class="sxs-lookup"><span data-stu-id="be598-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="be598-121">接著您必須設定您的通知中心，以便與 WNS 進行整合。</span><span class="sxs-lookup"><span data-stu-id="be598-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="be598-122">如果您尚未註冊您的應用程式，請瀏覽至 [Windows 開發人員中心](https://dev.windows.com/overview)，並使用 Microsoft 帳戶登入，然後按一下 [建立新的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="be598-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="be598-123">輸入您的 App 名稱，然後按一下 [保留應用程式名稱] 。</span><span class="sxs-lookup"><span data-stu-id="be598-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="be598-124">這會為您的應用程式建立新的 Windows 市集註冊。</span><span class="sxs-lookup"><span data-stu-id="be598-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="be598-125">在 Visual Studio 中，使用 Windows 通用 [空白應用程式] 範本來建立新的 Visual C# 市集應用程式專案，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="be598-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="be598-126">接受目標和最小平台版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="be598-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="be598-127">在 [方案總管] 中，以滑鼠右鍵按一下 Windows 市集應用程式專案，然後依序按一下 [市集] 和 [將應用程式與市集建立關聯...]。</span><span class="sxs-lookup"><span data-stu-id="be598-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="be598-128">隨即顯示 [將您的應用程式與 Windows 市集建立關聯]  精靈。</span><span class="sxs-lookup"><span data-stu-id="be598-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="be598-129">在此精靈中，使用您的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="be598-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="be598-130">按一下您在步驟 2 中註冊的應用程式，並按 [下一步]，然後按一下 [關聯]。</span><span class="sxs-lookup"><span data-stu-id="be598-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="be598-131">這會將所需的 Windows 市集註冊資訊新增至應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="be598-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="be598-132">回到新應用程式的 [Windows 開發人員中心](http://dev.windows.com/overview)頁面，並依序按一下 [服務] 和 [推播通知]，然後按一下 [WNS/MPNS]。</span><span class="sxs-lookup"><span data-stu-id="be598-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="be598-133">按一下 [新增通知]。</span><span class="sxs-lookup"><span data-stu-id="be598-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="be598-134">按一下 [空白 (快顯)] 範本，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="be598-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="be598-135">輸入通知 [名稱] 和視覺化 [內容] 訊息。</span><span class="sxs-lookup"><span data-stu-id="be598-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="be598-136">然後按一下 [儲存為草稿]。</span><span class="sxs-lookup"><span data-stu-id="be598-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="be598-137">瀏覽至[應用程式註冊入口網站](http://apps.dev.microsoft.com)並登入。</span><span class="sxs-lookup"><span data-stu-id="be598-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="be598-138">按一下您的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="be598-138">Click on your application name.</span></span> <span data-ttu-id="be598-139">記下位於 [Windows 市集] 平台設定中的 [應用程式祕密] 和 [套件安全性識別碼 (SID)]。</span><span class="sxs-lookup"><span data-stu-id="be598-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="be598-140">應用程式密碼與封裝 SID 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="be598-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="be598-141">請勿與任何人共用這些值，或與您的應用程式一起散發密碼。</span><span class="sxs-lookup"><span data-stu-id="be598-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="be598-142">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="be598-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="be598-143">選取 [通知服務]<b></b> 選項和 [Windows (WNS)]<b></b> 選項。</span><span class="sxs-lookup"><span data-stu-id="be598-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="be598-144">然後在 [安全性金鑰]<b></b> 欄位中輸入<b>應用程式密碼</b>。</span><span class="sxs-lookup"><span data-stu-id="be598-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="be598-145">輸入您在上一節中從 WNS 取得的 [套件 SID]<b></b> 值，然後按一下 [儲存]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="be598-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="be598-146">現在已將您的通知中心設定成使用 WNS，而且您已擁有可用來註冊應用程式和傳送通知的連接字串。</span><span class="sxs-lookup"><span data-stu-id="be598-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="be598-147">將您的應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="be598-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="be598-148">在 Visual Studio 中，以滑鼠右鍵按一下方案，然後按一下 [管理 NuGet 封裝] 。</span><span class="sxs-lookup"><span data-stu-id="be598-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="be598-149">此時會顯示 [管理 NuGet 封裝]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="be598-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="be598-150">搜尋 `WindowsAzure.Messaging.Managed` ，然後按一下 [ **安裝**] 並接受使用條款。</span><span class="sxs-lookup"><span data-stu-id="be598-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="be598-151">這會使用 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>來下載、安裝並新增適用於 Windows 的 Azure 傳訊程式庫參考。</span><span class="sxs-lookup"><span data-stu-id="be598-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="be598-152">開啟 App.xaml.cs 專案檔案，並新增下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="be598-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="be598-153">接著，在 App.xaml.cs 中，將下列 **InitNotificationsAsync** 方法定義新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="be598-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="be598-154">此程式碼會從 WNS 中擷取應用程式的通道 URI，然後向您的通知中樞註冊該通道 URI。</span><span class="sxs-lookup"><span data-stu-id="be598-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="be598-155">請務必使用出現在 Azure 入口網站中的通知中樞名稱，取代 "your hub name" 預留位置。</span><span class="sxs-lookup"><span data-stu-id="be598-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="be598-156">此外，使用您在上一節中從通知中樞的 [存取原則] 頁面取得的 **DefaultListenSharedAccessSignature** 連接字串，取代連接字串預留位置。</span><span class="sxs-lookup"><span data-stu-id="be598-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="be598-157">在 App.xaml.cs 的 **OnLaunched** 事件處理常式頂端，將下列呼叫新增至新 **InitNotificationsAsync** 方法：</span><span class="sxs-lookup"><span data-stu-id="be598-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="be598-158">這會保證每次啟動應用程式時，通道 URI 便會在通知中樞中註冊。</span><span class="sxs-lookup"><span data-stu-id="be598-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="be598-159">按 **F5** 鍵以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="be598-160">包含註冊金鑰的快顯對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="be598-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="be598-161">您的應用程式現在已能夠接收快顯通知。</span><span class="sxs-lookup"><span data-stu-id="be598-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="be598-162">傳送通知</span><span class="sxs-lookup"><span data-stu-id="be598-162">Send notifications</span></span>
<span data-ttu-id="be598-163">在 [Azure 入口網站](https://portal.azure.com/)中使用通知中樞上的 [測試傳送] 案例 (如下列螢幕畫面所示) 來傳送通知，即可在應用程式中快速測試通知的接收。</span><span class="sxs-lookup"><span data-stu-id="be598-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="be598-164">推播通知通常會以後端服務傳送，例如行動服務或使用相容程式庫的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="be598-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="be598-165">如果程式庫不適用於您的後端，也可以直接使用 REST API 來傳送通知訊息。</span><span class="sxs-lookup"><span data-stu-id="be598-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="be598-166">在本教學課程中，為了簡單起見，我們只會在主控台應用程式 (而非後端服務) 中使用適用於通知中樞的 .NET SDK 傳送通知，示範如何測試您的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="be598-167">我們建議以 [使用通知中樞將通知推播給使用者] 教學課程做為下一個步驟，以便從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="be598-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="be598-168">不過，下列方法可用來傳送通知：</span><span class="sxs-lookup"><span data-stu-id="be598-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="be598-169">**REST 介面**：您可以在使用 [REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)的任何後端平台上支援通知。</span><span class="sxs-lookup"><span data-stu-id="be598-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="be598-170">**Microsoft Azure 通知中樞 .NET SDK**︰在適用於 Visual Studio 的 NuGet 封裝管理員中，執行 [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="be598-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="be598-171">**Node.js** ： [如何從 Node.js 使用通知中樞](notification-hubs-nodejs-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="be598-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="be598-172">**Azure Mobile Apps**：如需如何從已與通知中樞整合的 Azure Mobile App 傳送通知的範例，請參閱 [新增 Mobile Apps 的推播通知](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="be598-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="be598-173">**Java/PHP**︰如需使用 REST API 傳送通知的範例，請參閱＜如何從 Java/PHP 使用通知中樞＞([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。</span><span class="sxs-lookup"><span data-stu-id="be598-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="be598-174">(選擇性) 從主控台應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="be598-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="be598-175">若要使用 .NET 主控台應用程式來傳送通知，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="be598-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="be598-176">以滑鼠右鍵按一下方案，並選取 [新增] 和 [新增專案...]，然後按一下 [Visual C#] 底下的 [Windows] 和 [主控台應用程式]，再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="be598-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="be598-177">即會將新的 Visual C# 主控台應用程式新增到方案中。</span><span class="sxs-lookup"><span data-stu-id="be598-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="be598-178">您也可以在個別方案中進行此項作業。</span><span class="sxs-lookup"><span data-stu-id="be598-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="be598-179">在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="be598-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="be598-180">這會在 Visual Studio 中顯示 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="be598-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="be598-181">在 [封裝管理員主控台] 視窗中，將 [預設專案]  設為新的主控台應用程式專案，然後在主控台視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="be598-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="be598-182">這會使用 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 封裝</a>加入對 Azure 通知中樞 SDK 的參考。</span><span class="sxs-lookup"><span data-stu-id="be598-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="be598-183">開啟 Program.cs 檔案，並新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="be598-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="be598-184">在 **Program** 類別中，新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="be598-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="be598-185">請確定您使用的連接字串具有 [完整] 存取權，而非 [接聽] 存取權。</span><span class="sxs-lookup"><span data-stu-id="be598-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="be598-186">接聽存取權的字串沒有傳送通知的權限。</span><span class="sxs-lookup"><span data-stu-id="be598-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="be598-187">在 **[主要]** 方法中新增下列命令列。</span><span class="sxs-lookup"><span data-stu-id="be598-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="be598-188">在 Visual Studio 中，以滑鼠右鍵按一下主控台應用程式專案，然後按一下 [設定為啟始專案]，將它設為啟始專案。</span><span class="sxs-lookup"><span data-stu-id="be598-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="be598-189">然後按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="be598-190">您將會在所有註冊裝置上收到快顯通知。</span><span class="sxs-lookup"><span data-stu-id="be598-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="be598-191">按一下或點選快顯橫幅即會載入應用程式。</span><span class="sxs-lookup"><span data-stu-id="be598-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="be598-192">您可以在 MSDN 上的[快顯目錄]、[圖格目錄]和[徽章概觀]主題中找到所有支援的承載。</span><span class="sxs-lookup"><span data-stu-id="be598-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be598-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be598-193">Next steps</span></span>
<span data-ttu-id="be598-194">在此簡單範例中，您會使用入口網站或主控台應用程式，將廣播通知傳送到您的所有 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="be598-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="be598-195">我們建議以 [使用通知中樞將通知推播給使用者] 教學課程做為下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="be598-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="be598-196">它會示範如何使用標記以特定使用者為目標，從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="be598-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="be598-197">如果您想要按興趣群組分隔使用者，請參閱 [使用通知中心傳送即時新聞]。</span><span class="sxs-lookup"><span data-stu-id="be598-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="be598-198">若要深入了解通知中樞的一般資訊，請參閱 [通知中樞指引](notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="be598-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="be598-199">[使用通知中樞將通知推播給使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="be598-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="be598-200">[使用通知中心傳送即時新聞]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="be598-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="be598-201">[快顯目錄]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="be598-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="be598-202">[圖格目錄]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="be598-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="be598-203">[徽章概觀]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="be598-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
