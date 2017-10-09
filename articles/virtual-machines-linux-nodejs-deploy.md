---
title: "aaaDeploy Node.js 應用程式 tooLinux 在 Azure 虛擬機器"
description: "深入了解如何 toodeploy Node.js 應用程式 tooLinux 在 Azure 虛擬機器。"
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="28ee8-103">部署 Node.js 應用程式 tooLinux 在 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="28ee8-104">本教學課程示範如何 tootake Node.js 應用程式並將它部署在 Azure 中執行的 tooLinux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="28ee8-105">在能夠執行 Node.js 任何作業系統上可依照本教學課程中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="28ee8-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="28ee8-106">您將學習如何：</span><span class="sxs-lookup"><span data-stu-id="28ee8-106">You'll learn how to:</span></span>

* <span data-ttu-id="28ee8-107">分叉和複製含有簡易待辦事項應用程式的 GitHub 儲存機制；</span><span class="sxs-lookup"><span data-stu-id="28ee8-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="28ee8-108">在建立和設定兩部 Linux 虛擬機器 Azure toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28ee8-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="28ee8-109">逐一查看 hello 應用程式上推送更新 toohello web 前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="28ee8-110">toocomplete 本教學課程中，您需要的 GitHub 帳戶與 Microsoft Azure 帳戶，並 hello 能力 toouse Git 從開發電腦。</span><span class="sxs-lookup"><span data-stu-id="28ee8-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="28ee8-111">如果您沒有 GitHub 帳戶，您可以在 [這裡](https://github.com/join)註冊。</span><span class="sxs-lookup"><span data-stu-id="28ee8-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="28ee8-112">如果您沒有 [Microsoft Azure](https://azure.microsoft.com/) 帳戶，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)註冊免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28ee8-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="28ee8-113">這也將引導您完成註冊程序的 hello [Microsoft 帳戶](http://account.microsoft.com)如果您還沒有其中一個。</span><span class="sxs-lookup"><span data-stu-id="28ee8-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="28ee8-114">或者，如果您是 Visual Studio 訂閱者，您可以 [啟用 MSDN 權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="28ee8-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="28ee8-115">如果您的開發電腦上沒有 git，當您使用 Macintosh 或 Windows 機器時，請從 [這裡](http://www.git-scm.com)安裝 git。</span><span class="sxs-lookup"><span data-stu-id="28ee8-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="28ee8-116">如果您使用 Linux，安裝 git 使用最適合您，hello 機制，例如`sudo apt-get install git`。</span><span class="sxs-lookup"><span data-stu-id="28ee8-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="28ee8-117">分支和複製 hello 待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="28ee8-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="28ee8-118">hello 本教學課程所使用的待辦事項應用程式會透過 MongoDB 執行個體，可追蹤的 TODO 清單實作簡單的 web 前端。</span><span class="sxs-lookup"><span data-stu-id="28ee8-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="28ee8-119">登入 tooGitHub 之後，請移[這裡](https://github.com/stepro/node-todo)toofind hello 應用程式和分岔會使用在 hello 右上方的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="28ee8-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="28ee8-120">這應該會在您的帳戶中建立名為 *accountname*/node-todo 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="28ee8-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="28ee8-121">現在，在您的開發電腦上複製這個儲存機制：</span><span class="sxs-lookup"><span data-stu-id="28ee8-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="28ee8-122">我們稍後會使用此本機複本 hello 儲存機制的有點 toohello 原始程式碼進行變更時。</span><span class="sxs-lookup"><span data-stu-id="28ee8-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="28ee8-123">建立及設定 hello Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="28ee8-124">Azure 充分支援使用 Linux 虛擬機器執行原始計算。</span><span class="sxs-lookup"><span data-stu-id="28ee8-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="28ee8-125">Hello 教學課程示範如何輕鬆地加速兩部 Linux 虛擬機器和部署 hello TODO 應用程式 toothem 執行的這個部分 hello web 前端上其中一個，並 hello MongoDB hello 其他執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="28ee8-126">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-126">Creating Virtual Machines</span></span>
<span data-ttu-id="28ee8-127">最簡單方式 toocreate hello Azure 中的新虛擬機器為 toouse hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="28ee8-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="28ee8-128">按一下[這裡](https://portal.azure.com)toosign 中的並啟動 hello Azure 入口網站 web 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="28ee8-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="28ee8-129">Hello Azure 入口網站已載入之後，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="28ee8-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="28ee8-130">按一下 hello [+ 新增] 連結。</span><span class="sxs-lookup"><span data-stu-id="28ee8-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="28ee8-131">挑選 hello 「 計算 」 類別目錄，然後選擇 「 Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="28ee8-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="28ee8-132">選取 hello 「 資源管理員 」 部署模型，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="28ee8-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="28ee8-133">填寫下列指導方針的 hello 基本概念：</span><span class="sxs-lookup"><span data-stu-id="28ee8-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="28ee8-134">指定您稍後可以輕鬆識別的名稱；</span><span class="sxs-lookup"><span data-stu-id="28ee8-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="28ee8-135">針對本教學課程，請選擇 [密碼] 驗證；</span><span class="sxs-lookup"><span data-stu-id="28ee8-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="28ee8-136">使用可識別的名稱建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="28ee8-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="28ee8-137">Hello 虛擬機器大小，「 A1 標準 」 是合理的選擇在此教學課程。</span><span class="sxs-lookup"><span data-stu-id="28ee8-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="28ee8-138">如需其他設定，確保 hello 磁碟類型為 「 標準 」，並接受所有 hello 其餘的預設值。</span><span class="sxs-lookup"><span data-stu-id="28ee8-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="28ee8-139">開始進行的 hello 建立 hello 摘要 頁面上。</span><span class="sxs-lookup"><span data-stu-id="28ee8-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="28ee8-140">執行上述的 hello 處理兩次 toocreate 兩個 Linux 虛擬機器，一個用於 hello web 前端，另一個 hello MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="28ee8-141">建立 hello 虛擬機器將需要大約 5-10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="28ee8-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="28ee8-142">指派虛擬機器的 DNS 項目</span><span class="sxs-lookup"><span data-stu-id="28ee8-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="28ee8-143">根據預設，只有透過公用 IP 位址 (例如 1.2.3.4) 才能存取 Azure 中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="28ee8-144">藉由指派這些 DNS 項目請 hello 機器更容易識別。</span><span class="sxs-lookup"><span data-stu-id="28ee8-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="28ee8-145">一旦 hello 入口網站會指出 hello 虛擬機器已建立，請按一下 hello hello 左導覽列中的 「 虛擬機器 」 連結，然後找出您的電腦。</span><span class="sxs-lookup"><span data-stu-id="28ee8-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="28ee8-146">針對每一部機器：</span><span class="sxs-lookup"><span data-stu-id="28ee8-146">For each machine:</span></span>

* <span data-ttu-id="28ee8-147">找出 hello Essentials 索引標籤並按一下 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="28ee8-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="28ee8-148">在 hello 公用 IP 位址組態，指定 DNS 名稱標籤並儲存。</span><span class="sxs-lookup"><span data-stu-id="28ee8-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="28ee8-149">hello 入口網站可確保您指定該 hello 名稱可用。</span><span class="sxs-lookup"><span data-stu-id="28ee8-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="28ee8-150">在儲存 hello 組態之後, 您的虛擬機器會有類似的主機名稱太`machinename.region.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="28ee8-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="28ee8-151">連接 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="28ee8-152">您的虛擬機器已佈建時，他們會透過 SSH 是預先設定的 tooallow 遠端連線。</span><span class="sxs-lookup"><span data-stu-id="28ee8-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="28ee8-153">這是我們將使用 tooconfigure hello 虛擬機器的 hello 機制。</span><span class="sxs-lookup"><span data-stu-id="28ee8-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="28ee8-154">如果您使用 Windows 的程式開發，您必須 tooget 將 SSH 用戶端如果您還沒有其中一個。</span><span class="sxs-lookup"><span data-stu-id="28ee8-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="28ee8-155">常見的選擇是 PuTTy，您可以從 [這裡](http://www.chiark.greenend.org.uk/~sgtatham/putty/)下載。</span><span class="sxs-lookup"><span data-stu-id="28ee8-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="28ee8-156">Macintosh 與 Linux 作業系統會預先安裝一個 SSH 版本。</span><span class="sxs-lookup"><span data-stu-id="28ee8-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="28ee8-157">設定 hello Web 前端的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="28ee8-158">您所建立的 SSH toohello web 前端電腦使用 PuTTY，ssh 命令列或其他最愛 SSH 工具。</span><span class="sxs-lookup"><span data-stu-id="28ee8-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="28ee8-159">您應該會看到歡迎使用訊息，後面接著命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="28ee8-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="28ee8-160">首先，讓我們確定 git 和節點都已安裝：</span><span class="sxs-lookup"><span data-stu-id="28ee8-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="28ee8-161">由於 hello 應用程式的 web 前端依賴某些原生的 Node.js 模組，我們還需要 tooinstall hello 組基本的建置工具：</span><span class="sxs-lookup"><span data-stu-id="28ee8-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="28ee8-162">最後，讓我們來安裝 Node.js 應用程式呼叫*永遠*，進而協助 toorun Node.js 伺服器應用程式：</span><span class="sxs-lookup"><span data-stu-id="28ee8-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="28ee8-163">這些是此虛擬機器 toobe 無法 toorun hello 應用程式的 web 前端上所需的所有 hello 相依性，所以請將該執行。</span><span class="sxs-lookup"><span data-stu-id="28ee8-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="28ee8-164">toodo，我們會先建立裸機先前分叉，使您可以輕鬆地發行更新 toohello 的虛擬機器 （我們稍後將說明此更新案例中），然後複製 hello 裸機複製 tooprovide hello GitHub 儲存機制的複製品 hello 的版本實際執行的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="28ee8-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="28ee8-165">從開始 hello home （~） 目錄中，執行下列命令的 hello (取代*accountname*使用 GitHub 使用者帳戶名稱):</span><span class="sxs-lookup"><span data-stu-id="28ee8-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="28ee8-166">現在，請輸入 hello 節點 todo 目錄，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="28ee8-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="28ee8-167">hello 應用程式的 web 前端正在執行，但是還有一個步驟之前，您可以從網頁瀏覽器存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28ee8-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="28ee8-168">hello 您建立虛擬機器受到 Azure 資源呼叫*網路安全性群組*，這為您您佈建時 hello 虛擬機器建立。</span><span class="sxs-lookup"><span data-stu-id="28ee8-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="28ee8-169">目前，此資源只允許外部要求 tooport 22 toobe 路由 toohello 虛擬機器，可讓與 hello 機器，但沒有其他的 SSH 通訊。</span><span class="sxs-lookup"><span data-stu-id="28ee8-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="28ee8-170">因此在順序 tooview hello 待辦事項應用程式，也就是連接埠 8080 上的設定的 toorun，此連接埠也需要 toobe 開啟。</span><span class="sxs-lookup"><span data-stu-id="28ee8-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="28ee8-171">傳回 toohello Azure 入口網站，並完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="28ee8-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="28ee8-172">按一下左側導覽列 hello; 中的 「 資源群組 」</span><span class="sxs-lookup"><span data-stu-id="28ee8-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="28ee8-173">選取包含您的虛擬機器; hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="28ee8-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="28ee8-174">在 hello 產生資源的清單，選取 hello 網路安全性群組 (hello 其中一個以保護盾圖示);</span><span class="sxs-lookup"><span data-stu-id="28ee8-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="28ee8-175">在 hello 屬性中，選擇 [連入的安全性規則]。</span><span class="sxs-lookup"><span data-stu-id="28ee8-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="28ee8-176">在 hello 工具列中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="28ee8-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="28ee8-177">提供名稱，例如 "default-allow-todo"；</span><span class="sxs-lookup"><span data-stu-id="28ee8-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="28ee8-178">Hello 通訊協定設定太"TCP";</span><span class="sxs-lookup"><span data-stu-id="28ee8-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="28ee8-179">設定 hello 目的地連接埠範圍太"8080";</span><span class="sxs-lookup"><span data-stu-id="28ee8-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="28ee8-180">按一下 [確定]，並等候建立 hello 安全性規則 toobe。</span><span class="sxs-lookup"><span data-stu-id="28ee8-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="28ee8-181">建立這個安全性規則之後, hello 待辦事項應用程式公開上會顯示 hello 網際網路，您可以瀏覽 tooit，執行個體使用的 URL，例如：</span><span class="sxs-lookup"><span data-stu-id="28ee8-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="28ee8-182">您會發現，即使我們尚未設定 hello MongoDB 虛擬機器，hello 待辦事項應用程式會出現 toobe 相當的功能。</span><span class="sxs-lookup"><span data-stu-id="28ee8-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="28ee8-183">這是因為 hello 來源儲存機制是硬式編碼 toouse 預先部署的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="28ee8-184">一旦我們已經設定 hello MongoDB 虛擬機器，我們將會返回，並改為變更 hello 來源的程式碼 tooutilize 我們私用 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="28ee8-185">設定 hello MongoDB 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="28ee8-186">您所建立的 SSH toohello 第二部電腦使用 PuTTY，ssh 命令列或其他最愛 SSH 工具。</span><span class="sxs-lookup"><span data-stu-id="28ee8-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="28ee8-187">之後看到 hello 歡迎訊息和命令提示字元，安裝 MongoDB (這些指示取自[這裡](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="28ee8-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="28ee8-188">根據預設，MongoDB 會設定為只供本機存取。</span><span class="sxs-lookup"><span data-stu-id="28ee8-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="28ee8-189">此教學課程中，我們會設定 MongoDB，以便從 hello 應用程式的虛擬機器存取。</span><span class="sxs-lookup"><span data-stu-id="28ee8-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="28ee8-190">在 sudo 內容中，開啟 hello /etc/mongod.conf 檔案，並找出 hello `# network interfaces` > 一節。</span><span class="sxs-lookup"><span data-stu-id="28ee8-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="28ee8-191">變更 hello`net.bindIp`組態值太`0.0.0.0`。</span><span class="sxs-lookup"><span data-stu-id="28ee8-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="28ee8-192">這項設定適用於 hello 只在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="28ee8-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="28ee8-193">**不是** 建議的安全性作法，不應該用於實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="28ee8-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="28ee8-194">現在請 hello MongoDB 服務已啟動：</span><span class="sxs-lookup"><span data-stu-id="28ee8-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="28ee8-195">根據預設，MongoDB 會透過連接埠 27017 運作。</span><span class="sxs-lookup"><span data-stu-id="28ee8-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="28ee8-196">因此 hello 中相同的方式，我們需要 tooopen 連接埠 8080 上 hello web 前端的虛擬機器，我們需要 tooopen 連接埠 27017 hello MongoDB 虛擬機器上的。</span><span class="sxs-lookup"><span data-stu-id="28ee8-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="28ee8-197">傳回 toohello Azure 入口網站，並完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="28ee8-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="28ee8-198">按一下左側導覽列 hello; 中的 「 資源群組 」</span><span class="sxs-lookup"><span data-stu-id="28ee8-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="28ee8-199">選取 hello 資源群組含有 hello MongoDB 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="28ee8-200">在 hello 產生資源的清單，選取 hello 網路安全性群組 (hello 其中一個以保護盾圖示) 以相同的名稱，您提供給 toohello MongoDB 虛擬機器; hello</span><span class="sxs-lookup"><span data-stu-id="28ee8-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="28ee8-201">在 hello 屬性中，選擇 [連入的安全性規則]。</span><span class="sxs-lookup"><span data-stu-id="28ee8-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="28ee8-202">在 hello 工具列中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="28ee8-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="28ee8-203">提供名稱，例如 "default-allow-mongo"；</span><span class="sxs-lookup"><span data-stu-id="28ee8-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="28ee8-204">Hello 通訊協定設定太"TCP";</span><span class="sxs-lookup"><span data-stu-id="28ee8-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="28ee8-205">設定 hello 目的地連接埠範圍太"27017";</span><span class="sxs-lookup"><span data-stu-id="28ee8-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="28ee8-206">按一下 [確定]，並等候建立 hello 安全性規則 toobe。</span><span class="sxs-lookup"><span data-stu-id="28ee8-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="28ee8-207">反覆運算 hello 待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="28ee8-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="28ee8-208">目前為止，我們已佈建兩個的 Linux 虛擬機器： 其中一個執行中的 hello 應用程式的 web 前端，另一個執行 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="28ee8-209">但有問題-hello web 前端不實際會尚未佈建的 hello MongoDB 執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="28ee8-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="28ee8-210">我們會修正藉由更新 hello web 前端的程式碼 toouse 環境變數，而不是硬式編碼的執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="28ee8-211">變更 hello 待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="28ee8-211">Changing hello TODO application</span></span>
<span data-ttu-id="28ee8-212">在您第一次複製 hello 節點 todo 儲存機制的開發電腦，開啟 hello`node-todo/config/database.js`檔案在您最愛的編輯器中，並變更 hello url hello 硬式編碼值類似`mongodb://...`太`process.env.MONGODB`。</span><span class="sxs-lookup"><span data-stu-id="28ee8-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="28ee8-213">認可您的變更，並推送 toohello GitHub master:</span><span class="sxs-lookup"><span data-stu-id="28ee8-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="28ee8-214">不幸的是，這不會發行 hello 變更 toohello web 前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="28ee8-215">讓我們進行一些詳細變更 toothat 虛擬機器 tooenable 簡單但有效率的機制來發佈更新，因此您可以快速觀察 hello 變更的影響 hello hello 實際環境中。</span><span class="sxs-lookup"><span data-stu-id="28ee8-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="28ee8-216">設定 hello Web 前端的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28ee8-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="28ee8-217">還記得我們先前 hello web 前端的虛擬機器上建立裸機 hello 節點 todo 儲存機制的複製品。</span><span class="sxs-lookup"><span data-stu-id="28ee8-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="28ee8-218">事實上，此動作會建立新的 Git 遠端 toowhich 變更可推入。</span><span class="sxs-lookup"><span data-stu-id="28ee8-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="28ee8-219">不過，只要推送 toothis 遠端相當不讓開發人員使用他們的程式碼時所需的 hello 快速反覆項目模型。</span><span class="sxs-lookup"><span data-stu-id="28ee8-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="28ee8-220">什麼我們想要 toobe 無法 toodo 是確保發送 toohello 遠端儲存機制 hello 虛擬機器上的時，hello 執行待辦事項應用程式會自動更新。</span><span class="sxs-lookup"><span data-stu-id="28ee8-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="28ee8-221">幸運的是，這是含 git 的簡單 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="28ee8-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="28ee8-222">Git 會公開攔截程序呼叫在特定時間 tooreact tooactions 採取 hello 儲存機制上的數的字。</span><span class="sxs-lookup"><span data-stu-id="28ee8-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="28ee8-223">這些使用指定的殼層指令碼儲存機制 hello 中`hooks`資料夾。</span><span class="sxs-lookup"><span data-stu-id="28ee8-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="28ee8-224">hello 攔截最適用 hello 自動更新案例中為 hello`post-update`事件。</span><span class="sxs-lookup"><span data-stu-id="28ee8-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="28ee8-225">SSH 工作階段 toohello web 前端虛擬機器中，變更 toohello`~/node-todo.git/hooks`目錄並加入下列內容 tooa 檔名為 hello `post-update` (取代`machinename`和`region`使用 MongoDB 虛擬機器資訊):</span><span class="sxs-lookup"><span data-stu-id="28ee8-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="28ee8-226">請確定這個檔案是藉由執行下列命令的 hello 可執行檔：</span><span class="sxs-lookup"><span data-stu-id="28ee8-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="28ee8-227">此指令碼確保 hello 目前伺服器應用程式已停止、 hello hello 複製儲存機制中的程式碼是更新的 toohello 最新版本，符合任何更新的相依性，且 hello 伺服器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="28ee8-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="28ee8-228">它也可確保該 hello 環境已設定在準備從環境變數接收我們第一個應用程式更新 tooget hello MongoDB 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="28ee8-229">設定您的開發電腦</span><span class="sxs-lookup"><span data-stu-id="28ee8-229">Configuring your Development Machine</span></span>
<span data-ttu-id="28ee8-230">現在讓我們協助您在開發電腦接到 toohello web 前端的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="28ee8-231">這很簡單，只新增 hello 裸機儲存機制 hello 與遠端的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="28ee8-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="28ee8-232">執行下列命令 toodo hello (取代*使用者*與 web 前端的虛擬機器登入名稱和*machinename*和*區域*依適當情況):</span><span class="sxs-lookup"><span data-stu-id="28ee8-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="28ee8-233">這是所有需要的 tooenable 推入，或作用中發行時，變更 toohello web 前端的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="28ee8-234">發佈更新</span><span class="sxs-lookup"><span data-stu-id="28ee8-234">Publishing Updates</span></span>
<span data-ttu-id="28ee8-235">讓我們發行 hello 發出到目前為止，使 hello 應用程式使用我們自己 MongoDB 執行個體的一項變更：</span><span class="sxs-lookup"><span data-stu-id="28ee8-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="28ee8-236">您應該會看到輸出類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="28ee8-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="28ee8-237">此命令完成之後，請嘗試重新整理網頁瀏覽器中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28ee8-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="28ee8-238">您應該能夠 toosee 這裡所呈現的 hello TODO 清單為空白，且不會再繫結的 toohello 共用部署 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28ee8-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="28ee8-239">toocomplete hello 教學課程中，讓我們來變更另一個、 更明顯可見。</span><span class="sxs-lookup"><span data-stu-id="28ee8-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="28ee8-240">在您的開發電腦上開啟 hello node-todo/public/index.html 檔案使用您最愛的編輯器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="28ee8-241">找出 hello jumbotron 標頭，並將變更從 「 我 Todo aholic 」 太的 我在 Azure 上 Todo aholic ！"的 hello 標題。</span><span class="sxs-lookup"><span data-stu-id="28ee8-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="28ee8-242">現在讓我們確認：</span><span class="sxs-lookup"><span data-stu-id="28ee8-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="28ee8-243">這個時間，讓我們發行 hello 變更 tooAzure 之前將它推送 tooback toohello GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="28ee8-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="28ee8-244">此命令完成之後，請重新整理 hello 網頁，您會看到 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="28ee8-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="28ee8-245">它們能呈現最佳效果，因為發送 hello 變更後 toohello 原始遠端：</span><span class="sxs-lookup"><span data-stu-id="28ee8-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="28ee8-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28ee8-246">Next Steps</span></span>
<span data-ttu-id="28ee8-247">本文示範過 tootake Node.js 應用程式並將它部署在 Azure 中執行的 tooLinux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28ee8-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="28ee8-248">toolearn 有關在 Azure 中 Linux 虛擬機器的詳細資訊請參閱[在 Azure 上的簡介 tooLinux](/documentation/articles/virtual-machines-linux-introduction/)。</span><span class="sxs-lookup"><span data-stu-id="28ee8-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="28ee8-249">如需有關如何在 Azure 上、 toodevelop Node.js 應用程式，請參閱 「 hello [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="28ee8-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

