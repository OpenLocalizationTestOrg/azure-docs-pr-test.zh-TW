---
title: "aaaGet hello 與 Azure RemoteApp 的任何裝置上的相同 Office 365 體驗 |Microsoft 文件"
description: "深入了解如何 tooshare 與您的使用者使用 Azure RemoteApp 任何 Office 365 應用程式。"
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
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="d593d-103">Get hello 相同 Azure RemoteApp 使用任何裝置上的 Office 365 體驗</span><span class="sxs-lookup"><span data-stu-id="d593d-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d593d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="d593d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d593d-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d593d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d593d-106">本文將討論如何 toodeploy Office 365 公司中的任何裝置上。</span><span class="sxs-lookup"><span data-stu-id="d593d-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="d593d-107">您的使用者可以取得相同功能 hello，Android、 Apple 和 Windows 上的 UI 體驗。</span><span class="sxs-lookup"><span data-stu-id="d593d-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="d593d-108">在 Azure 中使用者可連接的可調整虛擬機器上裝載 Office 365，即可使用 Azure RemoteApp 完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="d593d-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="d593d-109">這組虛擬機器稱為「雲端收藏」。</span><span class="sxs-lookup"><span data-stu-id="d593d-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="d593d-110">建立雲端收藏</span><span class="sxs-lookup"><span data-stu-id="d593d-110">Create a cloud collection</span></span>
<span data-ttu-id="d593d-111">先建立 Azure 帳戶之後，瀏覽過**RemoteApp**中的 hello hello 左側連結，即可。</span><span class="sxs-lookup"><span data-stu-id="d593d-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="d593d-112">![顯示 hello Azure 入口網站上的 Azure RemoteApp](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="d593d-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="d593d-113">然後即可繼續**新**hello 底部和 「 快速建立 」 集合。</span><span class="sxs-lookup"><span data-stu-id="d593d-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="d593d-114">提供名稱、 hello 區域、 hello 訂用帳戶、 hello 計劃以及我們所提供的 hello 影像"Office Proffesional 2013"。</span><span class="sxs-lookup"><span data-stu-id="d593d-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="d593d-115">![建立對話方塊](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="d593d-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="d593d-116">完成之後應該啟動 hello 表單 hello 集合建立程序。</span><span class="sxs-lookup"><span data-stu-id="d593d-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="d593d-117">這可能需要 tooan 小時左右。</span><span class="sxs-lookup"><span data-stu-id="d593d-117">This may take up tooan hour or so.</span></span>

![等候](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="d593d-119">一旦 hello 程序完成時，它看起來會像這樣。</span><span class="sxs-lookup"><span data-stu-id="d593d-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="d593d-120">如果按一下 [發佈]  ，可以看到已發佈大部分的 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d593d-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="d593d-121">![已建立集合](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="d593d-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![已發佈的應用程式](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="d593d-123">此時您也可以加入更多的使用者具有存取 toothis 集合，依序按一下**使用者存取**。</span><span class="sxs-lookup"><span data-stu-id="d593d-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="d593d-124">![設定使用者存取](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="d593d-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="d593d-125">現在讓我們來試試看連接 tooOffice 365 ！</span><span class="sxs-lookup"><span data-stu-id="d593d-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="d593d-126">連接 tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="d593d-126">Connect tooOffice 365</span></span>
<span data-ttu-id="d593d-127">我們將會太前端透過[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/)、 向下捲動並按一下**下載用戶端**tooinstall hello Azure RemoteApp 用戶端 hello 您所在的裝置上。</span><span class="sxs-lookup"><span data-stu-id="d593d-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="d593d-128">是 Windows hello 以下螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d593d-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="d593d-129">Hello 應用程式啟動會詢問 toosign 使用 Microsoft 帳戶 （先前稱為"Live ID 」），使用同一個為您的 Azure 帳戶現在 hello。</span><span class="sxs-lookup"><span data-stu-id="d593d-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="d593d-130">登入時，您應該會看到有關新邀請的通知，而按一下該處，您應該會看到與下面類似的清單。</span><span class="sxs-lookup"><span data-stu-id="d593d-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="d593d-131">接受 hello 邀請符合您的 Azure 帳戶擁有者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="d593d-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![新的邀請](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="d593d-133">它看起來就像有新的邀請。</span><span class="sxs-lookup"><span data-stu-id="d593d-133">What it looks like when there are new invitations.</span></span>

![接受應用程式](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="d593d-135">一旦您接受 hello 邀請您應該會看到所有 hello Azure RemoteApp 用戶端中的 hello Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d593d-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![應用程式清單](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="d593d-137">當您按一下任何這些 hello 應用程式應該啟動上 hello Azure 虛擬機器，而且您應該設 ！</span><span class="sxs-lookup"><span data-stu-id="d593d-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="d593d-138">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="d593d-138">Enjoy!</span></span>

![啟動](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

