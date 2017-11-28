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
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="05bb1-103">開始使用適用於 Windows 通用平台應用程式的通知中樞</span><span class="sxs-lookup"><span data-stu-id="05bb1-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="05bb1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="05bb1-104">Overview</span></span>
<span data-ttu-id="05bb1-105">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 通用 Windows 平台 (UWP) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="05bb1-106">在本教學課程中，您可以建立空白的 Windows 市集應用程式透過使用 Windows 推播通知服務 (WNS) hello 接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="05bb1-107">完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05bb1-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="05bb1-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="05bb1-109">hello 完成本教學課程中的程式碼可以在 GitHub 上找到[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05bb1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="05bb1-110">Prerequisites</span></span>
<span data-ttu-id="05bb1-111">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="05bb1-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="05bb1-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="05bb1-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="05bb1-113">已安裝通用 Windows 應用程式開發工具</span><span class="sxs-lookup"><span data-stu-id="05bb1-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="05bb1-114">作用中的 Azure 帳戶 </span><span class="sxs-lookup"><span data-stu-id="05bb1-114">An active Azure account</span></span> <br/><span data-ttu-id="05bb1-115">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05bb1-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="05bb1-116">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="05bb1-117">有效的 Windows 市集帳戶</span><span class="sxs-lookup"><span data-stu-id="05bb1-117">An active Windows Store account</span></span>

<span data-ttu-id="05bb1-118">完成本教學課程是 Windows 通用平台應用程式所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="05bb1-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="05bb1-119">註冊 hello Windows 市集應用程式</span><span class="sxs-lookup"><span data-stu-id="05bb1-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="05bb1-120">toosend 推播通知 tooUWP 應用程式，您必須使您的應用程式 toohello Windows 市集。</span><span class="sxs-lookup"><span data-stu-id="05bb1-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="05bb1-121">接著，您必須設定您的通知中樞 toointegrate 搭配 WNS。</span><span class="sxs-lookup"><span data-stu-id="05bb1-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="05bb1-122">如果您沒有註冊您的應用程式，請瀏覽 toohello [Windows 開發人員中心](https://dev.windows.com/overview)，使用您的 Microsoft 帳戶登入，然後按一下**建立新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="05bb1-123">輸入您的 App 名稱，然後按一下 [保留應用程式名稱] 。</span><span class="sxs-lookup"><span data-stu-id="05bb1-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="05bb1-124">這會為您的應用程式建立新的 Windows 市集註冊。</span><span class="sxs-lookup"><span data-stu-id="05bb1-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="05bb1-125">在 Visual Studio 中，建立新的 Visual C# 市集應用程式專案使用 Windows 通用 hello**空白應用程式**範本，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="05bb1-126">接受 hello hello 目標與最低平台版本的預設值。</span><span class="sxs-lookup"><span data-stu-id="05bb1-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="05bb1-127">在 [方案總管] 中，以滑鼠右鍵按一下 hello Windows 市集應用程式專案中，按一下 [**存放區**，然後按一下**將應用程式建立關聯以 hello 存放區...**。 hello**您應用程式建立關聯以 hello Windows 市集**精靈] 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="05bb1-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="05bb1-128">在 hello 精靈中，使用登入您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="05bb1-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="05bb1-129">按一下 註冊，讓您在步驟 2 中的 hello 應用程式中，按一下**下一步**，然後按一下**關聯**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="05bb1-130">這會將所需的 hello Windows 市集註冊資訊 toohello 應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="05bb1-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="05bb1-131">在 hello [Windows 開發人員中心](http://dev.windows.com/overview)新應用程式頁面上，按一下**服務**，按一下 **推播通知**，然後按一下**WNS/MPNS**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="05bb1-132">按一下 [新增通知]。</span><span class="sxs-lookup"><span data-stu-id="05bb1-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="05bb1-133">按一下 空白 (快顯) 範本，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="05bb1-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="05bb1-134">輸入通知 [名稱] 和視覺化 [內容] 訊息。</span><span class="sxs-lookup"><span data-stu-id="05bb1-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="05bb1-135">然後按一下 [儲存為草稿]。</span><span class="sxs-lookup"><span data-stu-id="05bb1-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="05bb1-136">瀏覽 toohello[應用程式註冊入口網站](http://apps.dev.microsoft.com)並登入。</span><span class="sxs-lookup"><span data-stu-id="05bb1-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="05bb1-137">按一下您的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="05bb1-137">Click on your application name.</span></span> <span data-ttu-id="05bb1-138">請記下 hello**應用程式密碼**密碼和 hello**封裝安全性識別碼 (SID)**位於 hello **Windows 市集**平台設定。</span><span class="sxs-lookup"><span data-stu-id="05bb1-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="05bb1-139">hello 應用程式密碼和封裝 SID 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="05bb1-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="05bb1-140">請勿與任何人共用這些值，或與您的應用程式一起散發密碼。</span><span class="sxs-lookup"><span data-stu-id="05bb1-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="05bb1-141">設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="05bb1-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="05bb1-142">選取 hello <b>Notification Services</b>選項和 hello <b>Windows (WNS)</b>選項。</span><span class="sxs-lookup"><span data-stu-id="05bb1-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="05bb1-143">然後輸入 hello<b>應用程式密碼</b>密碼 hello<b>安全性金鑰</b>欄位。</span><span class="sxs-lookup"><span data-stu-id="05bb1-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="05bb1-144">輸入您<b>封裝 SID</b>值取自 WNS hello 前一節中，然後再按一下<b>儲存</b>。</span><span class="sxs-lookup"><span data-stu-id="05bb1-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="05bb1-145">您的通知中樞現在是設定的 toowork 搭配 WNS，而且您擁有 hello 連接字串 tooregister 您的應用程式，並將傳送通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="05bb1-146">連接您的應用程式 toohello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="05bb1-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="05bb1-147">在 Visual Studio 中，hello 方案上按一下滑鼠右鍵，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="05bb1-148">這會顯示 hello**管理 NuGet 封裝** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="05bb1-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="05bb1-149">搜尋`WindowsAzure.Messaging.Managed`按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="05bb1-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="05bb1-150">這會下載、 安裝，並將適用於 Windows 的參考 toohello Azure 訊息文件庫，使用 hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 封裝</a>。</span><span class="sxs-lookup"><span data-stu-id="05bb1-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="05bb1-151">開啟 hello App.xaml.cs 專案檔，然後加入下列 hello`using`陳述式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="05bb1-152">也在 App.xaml.cs，加入 hello 下列**InitNotificationsAsync**方法定義 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="05bb1-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
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
   
    <span data-ttu-id="05bb1-153">這個程式碼 hello 應用程式的 hello 通道 URI 擷取 WNS，並使用通知中樞，然後註冊該通道 URI。</span><span class="sxs-lookup"><span data-stu-id="05bb1-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05bb1-154">請確定 tooreplace hello hello 名稱出現在 hello Azure 入口網站中的 hello 通知中樞的 「 中樞名稱 」 預留位置。</span><span class="sxs-lookup"><span data-stu-id="05bb1-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="05bb1-155">也將 hello 連接字串預留位置取代 hello **DefaultListenSharedAccessSignature**連接字串，您取得的 hello**存取原則**通知中樞 頁面上一節。</span><span class="sxs-lookup"><span data-stu-id="05bb1-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="05bb1-156">頂端的 hello hello **OnLaunched** App.xaml.cs，事件處理常式新增下列新的呼叫 toohello hello **InitNotificationsAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="05bb1-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="05bb1-157">這可確保該 hello 通道，在您每次 hello 應用程式啟動的通知中樞已註冊的 URI。</span><span class="sxs-lookup"><span data-stu-id="05bb1-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="05bb1-158">按 hello **F5**金鑰 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="05bb1-159">會顯示快顯的對話方塊，其中包含 hello 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="05bb1-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="05bb1-160">您的應用程式現在已準備好 tooreceive 快顯通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="05bb1-161">傳送通知</span><span class="sxs-lookup"><span data-stu-id="05bb1-161">Send notifications</span></span>
<span data-ttu-id="05bb1-162">您可以快速測試您的應用程式中接收通知，傳送通知給 hello 以[Azure 入口網站](https://portal.azure.com/)使用 hello**測試傳送**按鈕在 hello 通知中樞內，囉 」 畫面下方所示。</span><span class="sxs-lookup"><span data-stu-id="05bb1-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="05bb1-163">推播通知通常會以後端服務傳送，例如行動服務或使用相容程式庫的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="05bb1-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="05bb1-164">您也可以使用 hello REST API 直接 toosend 通知訊息，如果文件庫不適用於您的後端。</span><span class="sxs-lookup"><span data-stu-id="05bb1-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="05bb1-165">在本教學課程中，我們將保持簡單，並只示範測試用戶端應用程式透過傳送 hello.NET SDK 使用通知中心，而不是後端服務的主控台應用程式的通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="05bb1-166">我們建議 hello[使用通知中樞 toopush 通知 toousers]教學課程為 hello 下一個步驟，從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="05bb1-167">不過，hello 下列方法可用來傳送通知：</span><span class="sxs-lookup"><span data-stu-id="05bb1-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="05bb1-168">**REST 介面**： 您可以使用 hello 任何後端平台上支援通知[REST 介面](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="05bb1-169">**Microsoft Azure 通知中樞.NET SDK**: hello for Visual Studio 的 Nuget 封裝管理員，在執行[Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="05bb1-170">**Node.js** :[如何 toouse 通知中樞，從 Node.js](notification-hubs-nodejs-push-notification-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="05bb1-171">**Azure 行動應用程式**： 如需如何 toosend 通知從 Azure 行動應用程式與通知中樞整合，請參閱[行動應用程式的新增推播通知](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="05bb1-172">**Java / PHP**： 如需如何使用 toosend 通知 hello REST Api 的範例，請參閱 「 如何 toouse 來自 Java/PHP 的通知中心 」 ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))。</span><span class="sxs-lookup"><span data-stu-id="05bb1-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="05bb1-173">(選擇性) 從主控台應用程式傳送通知</span><span class="sxs-lookup"><span data-stu-id="05bb1-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="05bb1-174">使用.NET 主控台應用程式的 toosend 通知，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="05bb1-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="05bb1-175">以滑鼠右鍵按一下 hello 方案中，選取**新增**和**新的專案...**，，然後在**Visual C#**，按一下  **Windows**和**主控台應用程式**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="05bb1-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="05bb1-176">這會將新 Visual C# 主控台應用程式 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="05bb1-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="05bb1-177">您也可以在個別方案中進行此項作業。</span><span class="sxs-lookup"><span data-stu-id="05bb1-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="05bb1-178">在 Visual Studio 中，依序按一下 [工具]、[NuGet 封裝管理員] 和 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="05bb1-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="05bb1-179">這是 Visual Studio 中顯示 hello Package Manager Console。</span><span class="sxs-lookup"><span data-stu-id="05bb1-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="05bb1-180">在 [hello 封裝管理員主控台] 視窗中，設定 hello**預設專案**tooyour 新主控台應用程式專案，然後在 hello 主控台視窗中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="05bb1-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="05bb1-181">這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。</span><span class="sxs-lookup"><span data-stu-id="05bb1-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="05bb1-182">開啟 hello Program.cs 檔案並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="05bb1-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="05bb1-183">在 hello**程式**類別中，新增下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="05bb1-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="05bb1-184">請確定您使用 hello 連接字串具有**完整**不存取**接聽**存取。</span><span class="sxs-lookup"><span data-stu-id="05bb1-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="05bb1-185">hello 接聽存取字串不具有權限 toosend 通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="05bb1-186">加入下列行 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="05bb1-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="05bb1-187">在 Visual Studio 中的 hello 主控台應用程式專案上按一下滑鼠右鍵，然後按一下**設定為啟始專案**tooset 它為 hello 啟始專案。</span><span class="sxs-lookup"><span data-stu-id="05bb1-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="05bb1-188">然後按 hello **F5**金鑰 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="05bb1-189">您將會在所有註冊裝置上收到快顯通知。</span><span class="sxs-lookup"><span data-stu-id="05bb1-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="05bb1-190">按一下或點選 hello 快顯通知橫幅載入 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05bb1-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="05bb1-191">您可以在 hello 找到所有支援的 hello 裝載[快顯通知目錄]，[磚目錄]，和[徽章概觀]MSDN 上的主題。</span><span class="sxs-lookup"><span data-stu-id="05bb1-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05bb1-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05bb1-192">Next steps</span></span>
<span data-ttu-id="05bb1-193">在這個簡單的範例中，您傳送廣播的通知 tooall hello 入口網站或主控台應用程式使用 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="05bb1-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="05bb1-194">我們建議 hello[使用通知中樞 toopush 通知 toousers] hello 下一個步驟的教學課程。</span><span class="sxs-lookup"><span data-stu-id="05bb1-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="05bb1-195">它會顯示如何從 ASP.NET 後端使用 toosend 通知標記 tootarget 特定使用者。</span><span class="sxs-lookup"><span data-stu-id="05bb1-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="05bb1-196">如果您希望 toosegment 使用者感興趣的群組，請參閱[使用通知中樞 toosend 最新消息]。</span><span class="sxs-lookup"><span data-stu-id="05bb1-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="05bb1-197">toolearn 通知中樞的相關詳細資訊，請參閱[通知中樞指引](notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="05bb1-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

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
