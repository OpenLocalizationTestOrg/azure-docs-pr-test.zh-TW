---
title: "從任何裝置存取您的應用程式 | Microsoft Docs"
description: "了解 Azure RemoteApp 支援哪些用戶端以及如何存取您的應用程式。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="ecf56-103">在 Azure RemoteApp 存取您的應用程式</span><span class="sxs-lookup"><span data-stu-id="ecf56-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ecf56-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ecf56-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ecf56-106">Azure RemoteApp 的優點之一，就是您可以從任何裝置存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecf56-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="ecf56-107">更棒的是，您能在一台裝置上運作，然後順暢地轉換至第二台裝置，並從您先前停止的地方繼續進行。</span><span class="sxs-lookup"><span data-stu-id="ecf56-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="ecf56-108">若要開始進行，您必須為裝置下載適當的用戶端，然後登入該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="ecf56-109">在本主題中，我們將檢閱目前支援的用戶端，以及向您示範如何下載它們，接著示範如何從各個用戶端登入 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="ecf56-110">支持的用戶端</span><span class="sxs-lookup"><span data-stu-id="ecf56-110">Supported clients</span></span>
<span data-ttu-id="ecf56-111">如果您的裝置正在執行下列其中一個作業系統，就能夠使用下列步驟來存取 RemoteApp：</span><span class="sxs-lookup"><span data-stu-id="ecf56-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="ecf56-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ecf56-112">Windows 10</span></span> 
* <span data-ttu-id="ecf56-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ecf56-113">Windows 8.1</span></span>
* <span data-ttu-id="ecf56-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ecf56-114">Windows 8</span></span>
* <span data-ttu-id="ecf56-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="ecf56-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="ecf56-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ecf56-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="ecf56-117">iOS</span><span class="sxs-lookup"><span data-stu-id="ecf56-117">iOS</span></span>
* <span data-ttu-id="ecf56-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ecf56-118">Mac OS X</span></span>
* <span data-ttu-id="ecf56-119">Android</span><span class="sxs-lookup"><span data-stu-id="ecf56-119">Android</span></span>

 <span data-ttu-id="ecf56-120">精簡型用戶端呢？</span><span class="sxs-lookup"><span data-stu-id="ecf56-120">What about thin clients?</span></span> <span data-ttu-id="ecf56-121">支援下列 Windows Embedded 精簡型用戶端：</span><span class="sxs-lookup"><span data-stu-id="ecf56-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="ecf56-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="ecf56-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="ecf56-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="ecf56-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="ecf56-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="ecf56-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="ecf56-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="ecf56-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="ecf56-126">下載用戶端</span><span class="sxs-lookup"><span data-stu-id="ecf56-126">Downloading the client</span></span>
<span data-ttu-id="ecf56-127">不論您使用的平台為何，都能在 [遠端桌面用戶端下載](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) 頁面找到您需要存取 RemoteApp 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ecf56-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="ecf56-128">按一下不同的連結，將直接開始下載用戶端，或將您送到應用程式市集中該平台的用戶端下載頁面。</span><span class="sxs-lookup"><span data-stu-id="ecf56-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="ecf56-129">依照畫面上的指定來安裝用戶端。</span><span class="sxs-lookup"><span data-stu-id="ecf56-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="ecf56-130">當您在裝置上安裝用戶端並加以啟動後，請到下面對應的小節，了解如何從該用戶端登入 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="ecf56-131">Android</span><span class="sxs-lookup"><span data-stu-id="ecf56-131">Android</span></span>
<span data-ttu-id="ecf56-132">當您從 Google Play 商店安裝  Microsoft 遠端桌面之後，就可以在 [遠端桌面] 下找到您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ecf56-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ecf56-133">除非您已經開始使用應用程式，否則啟動應用程式將帶您前往空白的「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ecf56-134">若要開始使用 Azure RemoteApp，請點選加號按鈕 **""+""**，然後再點選 [Azure RemoteApp]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![空白連線中心](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="ecf56-136">您必須使用電子郵件地址登入以存取服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="ecf56-137">點選 [開始使用] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-137">Tap **Get started**.</span></span>
   
    ![提示時登入](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="ecf56-139">在下個頁面上，輸入您的 [電子郵件地址]，然後點選 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ecf56-140">這樣就會使用 Azure Active Directory 開始登入程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![第一個 Azure Active Directory 頁面](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="ecf56-142">依照畫面上的指示執行，以使用您的 Microsoft 帳戶 (先前稱為 "LiveID") 或組織識別碼登入。</span><span class="sxs-lookup"><span data-stu-id="ecf56-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="ecf56-143">登入之後，就會以頁面清單呈現您接收到的所有邀請。</span><span class="sxs-lookup"><span data-stu-id="ecf56-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ecf56-144">若是如此，請選取您信任的邀請，然後點選 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![邀請頁面](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="ecf56-146">接受您的邀請之後，就會將您擁有存取權的應用程式清單下載到您的裝置，並提供在「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ecf56-147">點選其中一個應用程式以開始使用它。</span><span class="sxs-lookup"><span data-stu-id="ecf56-147">Tap one of the apps to start using it.</span></span>
   
    ![包含摘要的連線中心](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="ecf56-149">如果您尚未收到邀請，還是能夠試用該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ecf56-150">若要這樣做，請在出現提示時，點選 [前往免費試用]  。</span><span class="sxs-lookup"><span data-stu-id="ecf56-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![示範摘要提示](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="ecf56-152">這將提供您存取一組基本應用程式的權限，讓您開始使用 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp 的示範摘要](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="ecf56-154">iOS</span><span class="sxs-lookup"><span data-stu-id="ecf56-154">iOS</span></span>
<span data-ttu-id="ecf56-155">當您從 App Store 安裝 Microsoft 遠端桌面應用程式之後，就可以在 [RD 用戶端] 下找到您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ecf56-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="ecf56-156">除非您已經開始使用應用程式，否則啟動應用程式將帶您前往空白的「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ecf56-157">若要開始使用 Azure RemoteApp，請點選加號按鈕 **""+""**，然後再點選 [新增 Azure RemoteApp]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![空白連線中心](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="ecf56-159">您必須使用自己的電子郵件地址登入才能存取服務，輸入您的 [電子郵件地址]，然後點選 [繼續] 以開始該程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![提示時登入](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="ecf56-161">依照畫面上的指示執行，以使用您的 Microsoft 帳戶 (LiveID) 或組織識別碼登入。</span><span class="sxs-lookup"><span data-stu-id="ecf56-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ecf56-162">登入之後，就會以頁面清單呈現您接收到的所有邀請。</span><span class="sxs-lookup"><span data-stu-id="ecf56-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ecf56-163">若是如此，請選取您信任的邀請，然後點選 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![邀請頁面](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="ecf56-165">接受您的邀請之後，就會將您擁有存取權的應用程式清單下載到您的裝置，並提供在「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ecf56-166">點選其中一個應用程式，即可加以啟動並開始使用。</span><span class="sxs-lookup"><span data-stu-id="ecf56-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![包含摘要的連線中心](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="ecf56-168">如果您尚未收到邀請，還是能夠試用該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ecf56-169">若要這樣做，請在出現提示時，點選 [前往免費試用]  。</span><span class="sxs-lookup"><span data-stu-id="ecf56-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![示範摘要提示](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="ecf56-171">這將提供您存取一組基本應用程式的權限，讓您開始使用 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp 的示範摘要](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="ecf56-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ecf56-173">Mac OS X</span></span>
<span data-ttu-id="ecf56-174">當您從 App Store 安裝  Microsoft 遠端桌面應用程式之後，就可以在 [Microsoft 遠端桌面] 下找到您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ecf56-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="ecf56-175">除非您已經開始使用應用程式，否則啟動應用程式將帶您前往空白的「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ecf56-176">若要開始使用 Azure RemoteApp，請按一下 [Azure RemoteApp]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ecf56-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![空白連線中心](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="ecf56-178">您必須使用自己的電子郵件地址登入才能存取服務，點選 [開始使用] 可開始該程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![提示時登入](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="ecf56-180">在下個頁面上，輸入您的 [電子郵件地址]，然後點選 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ecf56-181">這樣就會使用 Azure Active Directory 開始登入程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![第一個 Azure Active Directory 頁面](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="ecf56-183">依照畫面上的指示執行，以使用您的 Microsoft 帳戶 (LiveID) 或組織識別碼登入。</span><span class="sxs-lookup"><span data-stu-id="ecf56-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ecf56-184">登入之後，就會以頁面清單呈現您接收到的所有邀請。</span><span class="sxs-lookup"><span data-stu-id="ecf56-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ecf56-185">若是如此，請選取您信任的邀請，然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ecf56-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![邀請頁面](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="ecf56-187">接受您的邀請之後，就會將您擁有存取權的應用程式清單下載到您的裝置，並提供在「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ecf56-188">按兩下其中一個應用程式，即可加以啟動並開始使用。</span><span class="sxs-lookup"><span data-stu-id="ecf56-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![包含摘要的連線中心](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="ecf56-190">如果您尚未收到邀請，還是能夠試用該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ecf56-191">若要這樣做，請在出現提示時，按一下 [前往免費試用]  。</span><span class="sxs-lookup"><span data-stu-id="ecf56-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![示範摘要提示](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="ecf56-193">這將提供您存取一組基本應用程式的權限，讓您開始使用 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp 的示範摘要](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="ecf56-195">Windows (所有支援的版本，Windows Phone 除外)</span><span class="sxs-lookup"><span data-stu-id="ecf56-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="ecf56-196">用戶端會在完成安裝後自動啟動，不過之後若需要再次存取時，您可以在 [Azure RemoteApp] 這個名稱下找到您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ecf56-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="ecf56-197">啟動用戶端之後，您看到的第一個頁面會歡迎您使用 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="ecf56-198">若要繼續，請按一下 [開始使用] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-198">To proceed, click on **Get Started**.</span></span>
   
    ![Azure RemoteApp 用戶端的歡迎使用頁面](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="ecf56-200">下一個頁面會使用 Azure Active Directory，開始進行 Azure RemoteApp 登入程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="ecf56-201">這項程序看起來應該類似於您過去使用的 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="ecf56-202">請從輸入 [電子郵件地址] 開始，然後按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![第一個 Azure Active Directory 提示](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="ecf56-204">依照畫面上的指示執行，以使用您的 Microsoft 帳戶 (LiveID) 或組織識別碼登入。</span><span class="sxs-lookup"><span data-stu-id="ecf56-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ecf56-205">登入之後，就會以頁面清單呈現您接收到的所有邀請。</span><span class="sxs-lookup"><span data-stu-id="ecf56-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ecf56-206">若是如此，請選取您信任的邀請，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Azure RemoteApp 用戶端的邀請頁面](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="ecf56-208">接受您的邀請之後，就會將您擁有存取權的應用程式清單下載到您的裝置，並提供在「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ecf56-209">按兩下其中一個應用程式，即可加以啟動並開始使用。</span><span class="sxs-lookup"><span data-stu-id="ecf56-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Azure RemoteApp 用戶端的連線中心](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="ecf56-211">如果尚無任何人傳送邀請給您，請別擔心，我們會助您一臂之力！</span><span class="sxs-lookup"><span data-stu-id="ecf56-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="ecf56-212">您仍將擁有示範集合的存取權，讓您測試該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Azure RemoteApp 的示範摘要](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="ecf56-214">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ecf56-214">Windows Phone 8.1</span></span>
<span data-ttu-id="ecf56-215">當您從 Windows Phone 8.1 市集安裝  Microsoft 遠端桌面之後，就可以在 [遠端桌面] 下找到您的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ecf56-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="ecf56-216">除非您已經開始使用應用程式，否則啟動應用程式將直接帶您前往空白的「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="ecf56-217">若要開始使用 Azure RemoteApp，請點選畫面底部的加號按鈕 ""+""  。</span><span class="sxs-lookup"><span data-stu-id="ecf56-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![空白連線中心](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="ecf56-219">接下來，點選 [Azure RemoteApp] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![新增項目頁面](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="ecf56-221">您必須使用自己的電子郵件地址登入才能存取服務，點選 [連線] 可開始該程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![提示時登入](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="ecf56-223">在下個頁面上，輸入您的 [電子郵件地址]，然後點選 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="ecf56-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="ecf56-224">這樣就會使用 Azure Active Directory 開始登入程序。</span><span class="sxs-lookup"><span data-stu-id="ecf56-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![第一個 Azure Active Directory 頁面](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="ecf56-226">依照畫面上的指示執行，以使用您的 Microsoft 帳戶 (LiveID) 或組織識別碼登入。</span><span class="sxs-lookup"><span data-stu-id="ecf56-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="ecf56-227">登入之後，就會以頁面清單呈現您接收到的所有邀請。</span><span class="sxs-lookup"><span data-stu-id="ecf56-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="ecf56-228">若是如此，請選取您信任的邀請，然後點選 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ecf56-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![邀請頁面](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="ecf56-230">接受您的邀請之後，就會將您擁有存取權的應用程式清單下載到您的裝置，並提供在「連線中心」。</span><span class="sxs-lookup"><span data-stu-id="ecf56-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="ecf56-231">點選其中一個應用程式，即可加以啟動並開始使用。</span><span class="sxs-lookup"><span data-stu-id="ecf56-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![包含摘要的連線中心](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="ecf56-233">如果您尚未收到邀請，還是能夠試用該服務。</span><span class="sxs-lookup"><span data-stu-id="ecf56-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="ecf56-234">若要這樣做，請在出現提示時，點選 [是]  。</span><span class="sxs-lookup"><span data-stu-id="ecf56-234">To do so, tap **yes** when prompted.</span></span>
   
    ![示範摘要提示](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="ecf56-236">這將提供您存取一組基本應用程式的權限，讓您開始使用 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ecf56-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Azure RemoteApp 的示範摘要](./media/remoteapp-clients/WinPhone8.png)

