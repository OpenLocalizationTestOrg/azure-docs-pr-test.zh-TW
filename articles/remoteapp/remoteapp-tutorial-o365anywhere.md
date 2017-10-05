---
title: "在任何具有 Azure RemoteApp 的裝置上取得相同的 Office 365 體驗 | Microsoft Docs"
description: "了解如何使用 Azure RemoteApp 與使用者共用任何 Office 365 應用程式。"
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="2d9b4-103">在任何具有 Azure RemoteApp 的裝置上取得相同的 Office 365 體驗</span><span class="sxs-lookup"><span data-stu-id="2d9b4-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2d9b4-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2d9b4-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2d9b4-106">本文涵蓋如何在公司的任何裝置上部署 Office 365。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="2d9b4-107">您的使用者可以在 Android、Apple 和 Windows 上取得相同的功能和 UI 體驗。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="2d9b4-108">在 Azure 中使用者可連接的可調整虛擬機器上裝載 Office 365，即可使用 Azure RemoteApp 完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="2d9b4-109">這組虛擬機器稱為「雲端收藏」。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="2d9b4-110">建立雲端收藏</span><span class="sxs-lookup"><span data-stu-id="2d9b4-110">Create a cloud collection</span></span>
<span data-ttu-id="2d9b4-111">首先，建立 Azure 帳戶之後，請按一下左側的連結，以瀏覽至 **RemoteApp** 。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="2d9b4-112">![在 Azure 入口網站上顯示 Azure RemoteApp](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="2d9b4-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="2d9b4-113">然後，按一下底部的 [ **新增** ] 並「快速建立」收藏，以繼續進行。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="2d9b4-114">提供所提供的名稱、區域、訂用帳戶、計畫和映像 "Office Proffesional 2013"。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="2d9b4-115">![建立對話方塊](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="2d9b4-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="2d9b4-116">完成表單之後，應該會啟動集合建立程序。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="2d9b4-117">這可能需要一個小時左右。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-117">This may take up to an hour or so.</span></span>

![等候](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="2d9b4-119">完成程序之後，結果會與以下範例類似。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="2d9b4-120">如果按一下 [發佈]  ，可以看到已發佈大部分的 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="2d9b4-121">![已建立集合](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="2d9b4-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![已發佈的應用程式](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="2d9b4-123">此時，按一下 [使用者存取] ，也可以加入可存取此收藏的更多使用者。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="2d9b4-124">![設定使用者存取](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="2d9b4-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="2d9b4-125">現在讓我們嘗試連接至 Office 365！</span><span class="sxs-lookup"><span data-stu-id="2d9b4-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="2d9b4-126">連接至 Office 365</span><span class="sxs-lookup"><span data-stu-id="2d9b4-126">Connect to Office 365</span></span>
<span data-ttu-id="2d9b4-127">我們將會前往 [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/)，向下捲動並按一下 [下載用戶端]，以在您所在的裝置上安裝 Azure RemoteApp 用戶端。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="2d9b4-128">下面的螢幕擷取畫面適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="2d9b4-129">啟動應用程式之後，系統會要求您使用 Microsoft 帳戶 (先前稱為 Live ID) 登入，請現在使用相同的 Live ID 做為您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="2d9b4-130">登入時，您應該會看到有關新邀請的通知，而按一下該處，您應該會看到與下面類似的清單。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="2d9b4-131">請接受符合您 Azure 帳戶擁有者電子郵件的邀請。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-131">Accept the invitation that matches your Azure account owner email.</span></span>

![新的邀請](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="2d9b4-133">它看起來就像有新的邀請。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-133">What it looks like when there are new invitations.</span></span>

![接受應用程式](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="2d9b4-135">接受邀請之後，應該會看到 Azure RemoteApp 用戶端中的所有 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d9b4-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![應用程式清單](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="2d9b4-137">按一下其中任何一項時，應該會在 Azure 虛擬機器上啟動應用程式，而您應該已完成所有設定！</span><span class="sxs-lookup"><span data-stu-id="2d9b4-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="2d9b4-138">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="2d9b4-138">Enjoy!</span></span>

![啟動](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

