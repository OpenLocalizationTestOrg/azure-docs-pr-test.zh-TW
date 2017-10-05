---
title: "將 Node.js 應用程式部署到 Azure 中的 Linux 虛擬機器"
description: "了解如何將 Node.js 應用程式部署到 Azure 中的 Linux 虛擬機器"
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
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="612fd-103">將 Node.js 應用程式部署到 Azure 中的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="612fd-104">本教學課程說明如何將 Node.js 應用程式部署到 Azure 中執行的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="612fd-105">本教學課程中的指示可運用在任何足以執行 Node.js 應用程式的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="612fd-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="612fd-106">您將學習如何：</span><span class="sxs-lookup"><span data-stu-id="612fd-106">You'll learn how to:</span></span>

* <span data-ttu-id="612fd-107">分叉和複製含有簡易待辦事項應用程式的 GitHub 儲存機制；</span><span class="sxs-lookup"><span data-stu-id="612fd-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="612fd-108">Azure 中建立和設定兩個 Linux 虛擬機器來執行應用程式；</span><span class="sxs-lookup"><span data-stu-id="612fd-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="612fd-109">將更新發送至 Web 前端虛擬機器來反覆測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="612fd-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="612fd-110">若要完成本教學課程，您需要有 GitHub 帳戶和 Microsoft Azure 帳戶，並且能夠從開發電腦上使用 Git。</span><span class="sxs-lookup"><span data-stu-id="612fd-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="612fd-111">如果您沒有 GitHub 帳戶，您可以在 [這裡](https://github.com/join)註冊。</span><span class="sxs-lookup"><span data-stu-id="612fd-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="612fd-112">如果您沒有 [Microsoft Azure](https://azure.microsoft.com/) 帳戶，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)註冊免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="612fd-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="612fd-113">如果您還沒有 Microsoft 帳戶，這也會引導您完成 [Microsoft 帳戶](http://account.microsoft.com) 的註冊程序。</span><span class="sxs-lookup"><span data-stu-id="612fd-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="612fd-114">或者，如果您是 Visual Studio 訂閱者，您可以 [啟用 MSDN 權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="612fd-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="612fd-115">如果您的開發電腦上沒有 git，當您使用 Macintosh 或 Windows 機器時，請從 [這裡](http://www.git-scm.com)安裝 git。</span><span class="sxs-lookup"><span data-stu-id="612fd-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="612fd-116">如果您使用 Linux，請使用最適合您的機制來安裝 git，例如 `sudo apt-get install git`。</span><span class="sxs-lookup"><span data-stu-id="612fd-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="612fd-117">分叉和複製待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="612fd-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="612fd-118">本教學課程所使用的待辦事項應用程式會透過 MongoDB 執行個體，實作簡單的 Web 前端來追蹤待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="612fd-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="612fd-119">登入 GitHub 之後，移至 [這裡](https://github.com/stepro/node-todo) 來尋找應用程式，並使用右上方的連結將它分叉。</span><span class="sxs-lookup"><span data-stu-id="612fd-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="612fd-120">這應該會在您的帳戶中建立名為 *accountname*/node-todo 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="612fd-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="612fd-121">現在，在您的開發電腦上複製這個儲存機制：</span><span class="sxs-lookup"><span data-stu-id="612fd-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="612fd-122">我們稍後會使用此儲存機制本機複製品來變更原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="612fd-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="612fd-123">建立和設定 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="612fd-124">Azure 充分支援使用 Linux 虛擬機器執行原始計算。</span><span class="sxs-lookup"><span data-stu-id="612fd-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="612fd-125">這部分的教學課程將說明如何輕鬆地讓兩個 Linux 虛擬機器運作，並在上面部署待辦事項應用程式，其中一個執行 Web 前端，另一個執行 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="612fd-126">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-126">Creating Virtual Machines</span></span>
<span data-ttu-id="612fd-127">在 Azure 中建立新的虛擬機器最簡單方式是使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="612fd-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="612fd-128">按一下 [這裡](https://portal.azure.com) 登入，並在網頁瀏覽器中啟動 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="612fd-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="612fd-129">載入 Azure 入口網站後，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="612fd-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="612fd-130">按一下 [+ 新增] 連結；</span><span class="sxs-lookup"><span data-stu-id="612fd-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="612fd-131">選取 [計算] 類別，然後選擇 [Ubuntu Server 14.04 LTS]；</span><span class="sxs-lookup"><span data-stu-id="612fd-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="612fd-132">選取 [資源管理員] 部署模型，然後按一下 [建立]；</span><span class="sxs-lookup"><span data-stu-id="612fd-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="612fd-133">依照下列指導方針填寫基本資料：</span><span class="sxs-lookup"><span data-stu-id="612fd-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="612fd-134">指定您稍後可以輕鬆識別的名稱；</span><span class="sxs-lookup"><span data-stu-id="612fd-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="612fd-135">針對本教學課程，請選擇 [密碼] 驗證；</span><span class="sxs-lookup"><span data-stu-id="612fd-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="612fd-136">使用可識別的名稱建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="612fd-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="612fd-137">在虛擬機器大小方面，[A1 標準] 是適合本教學課程的選擇。</span><span class="sxs-lookup"><span data-stu-id="612fd-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="612fd-138">關於其他設定，請確定磁碟類型為 [標準]，並接受其餘所有預設值。</span><span class="sxs-lookup"><span data-stu-id="612fd-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="612fd-139">在摘要頁面上開始建立。</span><span class="sxs-lookup"><span data-stu-id="612fd-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="612fd-140">執行上述程序兩次以建立兩個 Linux 虛擬機器，一個用於 Web 前端，另一個用於 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="612fd-141">建立虛擬機器需要大約 5-10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="612fd-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="612fd-142">指派虛擬機器的 DNS 項目</span><span class="sxs-lookup"><span data-stu-id="612fd-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="612fd-143">根據預設，只有透過公用 IP 位址 (例如 1.2.3.4) 才能存取 Azure 中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="612fd-144">我們指派 DNS 項目讓電腦更容易識別。</span><span class="sxs-lookup"><span data-stu-id="612fd-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="612fd-145">一旦入口網站指出已建立虛擬機器，請按一下左側導覽列中的 [虛擬機器] 連結，並找出您的機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="612fd-146">針對每一部機器：</span><span class="sxs-lookup"><span data-stu-id="612fd-146">For each machine:</span></span>

* <span data-ttu-id="612fd-147">找出 [基本資訊] 索引標籤，然後按一下 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="612fd-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="612fd-148">在公用 IP 位址設定中，指派 DNS 名稱標籤，然後儲存。</span><span class="sxs-lookup"><span data-stu-id="612fd-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="612fd-149">入口網站會確保您指定的名稱可用。</span><span class="sxs-lookup"><span data-stu-id="612fd-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="612fd-150">儲存組態之後，虛擬機器會有類似 `machinename.region.cloudapp.azure.com`的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="612fd-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="612fd-151">連線至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="612fd-152">當佈建虛擬機器時，它們已預先設定為允許透過 SSH 從遠端連接。</span><span class="sxs-lookup"><span data-stu-id="612fd-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="612fd-153">這是我們將用來設定虛擬機器的機制。</span><span class="sxs-lookup"><span data-stu-id="612fd-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="612fd-154">如果您使用 Windows 進行開發，您必須取得 SSH 用戶端 (如果還沒有的話)。</span><span class="sxs-lookup"><span data-stu-id="612fd-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="612fd-155">常見的選擇是 PuTTy，您可以從 [這裡](http://www.chiark.greenend.org.uk/~sgtatham/putty/)下載。</span><span class="sxs-lookup"><span data-stu-id="612fd-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="612fd-156">Macintosh 與 Linux 作業系統會預先安裝一個 SSH 版本。</span><span class="sxs-lookup"><span data-stu-id="612fd-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="612fd-157">設定 Web 前端虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="612fd-158">使用 PuTTY、ssh 命令列或您偏好的其他 SSH 工具，透過 SSH 連線到您建立的 Web 前端機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="612fd-159">您應該會看到歡迎使用訊息，後面接著命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="612fd-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="612fd-160">首先，讓我們確定 git 和節點都已安裝：</span><span class="sxs-lookup"><span data-stu-id="612fd-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="612fd-161">由於應用程式的 Web 前端依賴一些原生的 Node.js 模組，我們還需要安裝一套基本的建置工具：</span><span class="sxs-lookup"><span data-stu-id="612fd-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="612fd-162">最後，讓我們安裝一個稱為 *forever*的 Node.js 應用程式，以協助執行 Node.js 伺服器應用程式：</span><span class="sxs-lookup"><span data-stu-id="612fd-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="612fd-163">為了能夠執行應用程式的 Web 前端，這些是此虛擬機器上需要的所有相依項目，讓我們啟動它們。</span><span class="sxs-lookup"><span data-stu-id="612fd-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="612fd-164">若要這樣做，我們將先從您之前分叉的 GitHub 儲存機制建立裸機複製品，讓您可以輕鬆地將更新發佈至虛擬機器 (我們稍後會說明此更新案例)，然後再複製裸機複製品來提供可實際執行的儲存機制版本。</span><span class="sxs-lookup"><span data-stu-id="612fd-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="612fd-165">從起始 (~) 目錄開始，執行下列命令 (將 *accountname* 換成您的 GitHub 使用者帳戶名稱)：</span><span class="sxs-lookup"><span data-stu-id="612fd-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="612fd-166">現在，進入 node-todo 目錄並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="612fd-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="612fd-167">現在，應用程式的 Web 前端正在執行，但還需要完成一個步驟，您才能從網頁瀏覽器存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="612fd-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="612fd-168">您所建立的虛擬機器由一個稱為 *網路安全性群組*的 Azure 資源所保護，這是在您佈建虛擬機器時為您建立的群組。</span><span class="sxs-lookup"><span data-stu-id="612fd-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="612fd-169">目前，此資源只允許將到達連接埠 22 的外部要求路由傳送到虛擬機器，這樣可透過 SSH 與機器通訊，但也僅此而已。</span><span class="sxs-lookup"><span data-stu-id="612fd-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="612fd-170">因此，若要檢視設定在連接埠 8080 上執行的待辦事項應用程式，此連接埠也必須開啟。</span><span class="sxs-lookup"><span data-stu-id="612fd-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="612fd-171">返回 Azure 入口網站，並完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="612fd-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="612fd-172">按一下左側導覽列中的 [資源群組]；</span><span class="sxs-lookup"><span data-stu-id="612fd-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="612fd-173">選取包含您的虛擬機器的資源群組；</span><span class="sxs-lookup"><span data-stu-id="612fd-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="612fd-174">在產生的資源清單中，選取網路安全性小組 (有保護盾圖示)；</span><span class="sxs-lookup"><span data-stu-id="612fd-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="612fd-175">在屬性中，選擇 [輸入安全性規則]；</span><span class="sxs-lookup"><span data-stu-id="612fd-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="612fd-176">在工具列中，按一下 [新增]；</span><span class="sxs-lookup"><span data-stu-id="612fd-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="612fd-177">提供名稱，例如 "default-allow-todo"；</span><span class="sxs-lookup"><span data-stu-id="612fd-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="612fd-178">將通訊協定設為 [TCP]；</span><span class="sxs-lookup"><span data-stu-id="612fd-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="612fd-179">將目的地連接埠範圍設為 "8080"；</span><span class="sxs-lookup"><span data-stu-id="612fd-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="612fd-180">按一下 [確定]，並等候安全性規則建立。</span><span class="sxs-lookup"><span data-stu-id="612fd-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="612fd-181">建立這個安全性規則之後，待辦事項應用程式在網際網路上就公開可見，您可以使用如下的 URL 來瀏覽它：</span><span class="sxs-lookup"><span data-stu-id="612fd-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="612fd-182">您會發現，即使我們還沒有設定 MongoDB 虛擬機器，待辦事項應用程式也已頗具功能。</span><span class="sxs-lookup"><span data-stu-id="612fd-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="612fd-183">這是因為來源儲存機制已硬式編碼為使用預先部署的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="612fd-184">一旦我們設定 MongoDB 虛擬機器後，我們會返回並變更原始碼，以改用我們的私用 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="612fd-185">設定 MongoDB 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="612fd-186">使用 PuTTY、ssh 命令列或您偏好的其他 SSH 工具，透過 SSH 連線到您建立的第二部機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="612fd-187">看到歡迎訊息和命令提示字元之後，安裝 MongoDB (這些指示取自於 [這裡](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/))：</span><span class="sxs-lookup"><span data-stu-id="612fd-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="612fd-188">根據預設，MongoDB 會設定為只供本機存取。</span><span class="sxs-lookup"><span data-stu-id="612fd-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="612fd-189">本教學課程中，我們會將 MongoDB 設定為可從應用程式的虛擬機器存取。</span><span class="sxs-lookup"><span data-stu-id="612fd-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="612fd-190">在虛擬環境下，開啟 /etc/mongod.conf 檔案並尋找 `# network interfaces` 一節。</span><span class="sxs-lookup"><span data-stu-id="612fd-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="612fd-191">將 `net.bindIp` 組態值變更為 `0.0.0.0`。</span><span class="sxs-lookup"><span data-stu-id="612fd-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="612fd-192">此設定只用於本教學課程。</span><span class="sxs-lookup"><span data-stu-id="612fd-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="612fd-193">**不是** 建議的安全性作法，不應該用於實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="612fd-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="612fd-194">現在，請確定 MongoDB 服務已啟動：</span><span class="sxs-lookup"><span data-stu-id="612fd-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="612fd-195">根據預設，MongoDB 會透過連接埠 27017 運作。</span><span class="sxs-lookup"><span data-stu-id="612fd-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="612fd-196">因此，就像我們需要在 Web 前端虛擬機器上開啟連接埠 8080 一樣，我們也需要在 MongoDB 虛擬機器上開啟連接埠 27017。</span><span class="sxs-lookup"><span data-stu-id="612fd-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="612fd-197">返回 Azure 入口網站，並完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="612fd-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="612fd-198">按一下左側導覽列中的 [資源群組]；</span><span class="sxs-lookup"><span data-stu-id="612fd-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="612fd-199">選取包含 MongoDB 虛擬機器的資源群組；</span><span class="sxs-lookup"><span data-stu-id="612fd-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="612fd-200">在產生的資源清單中，選取與 MongoDB 虛擬機器同名的網路安全性小組 (有保護盾圖示)；</span><span class="sxs-lookup"><span data-stu-id="612fd-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="612fd-201">在屬性中，選擇 [輸入安全性規則]；</span><span class="sxs-lookup"><span data-stu-id="612fd-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="612fd-202">在工具列中，按一下 [新增]；</span><span class="sxs-lookup"><span data-stu-id="612fd-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="612fd-203">提供名稱，例如 "default-allow-mongo"；</span><span class="sxs-lookup"><span data-stu-id="612fd-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="612fd-204">將通訊協定設為 [TCP]；</span><span class="sxs-lookup"><span data-stu-id="612fd-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="612fd-205">將目的地連接埠範圍設為 "27017"；</span><span class="sxs-lookup"><span data-stu-id="612fd-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="612fd-206">按一下 [確定]，並等候安全性規則建立。</span><span class="sxs-lookup"><span data-stu-id="612fd-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="612fd-207">反覆測試待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="612fd-207">Iterating on the TODO application</span></span>
<span data-ttu-id="612fd-208">目前為止，我們已佈建兩個 Linux 虛擬機器：一個執行應用程式的 Web 前端，另一個執行 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="612fd-209">但有問題，Web 前端實際上還未使用已佈建的 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="612fd-210">讓我們更新 Web 前端程式碼來使用環境變數，而非硬式編碼的執行個體，以解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="612fd-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="612fd-211">變更待辦事項應用程式</span><span class="sxs-lookup"><span data-stu-id="612fd-211">Changing the TODO application</span></span>
<span data-ttu-id="612fd-212">在您最初複製 node-todo 存放庫的開發電腦上，使用您喜好的編輯器開啟 `node-todo/config/database.js` 檔案，將 url 值從硬式編碼值 (例如 `mongodb://...`) 變更為 `process.env.MONGODB`。</span><span class="sxs-lookup"><span data-stu-id="612fd-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="612fd-213">認可變更並推送至 GitHub master：</span><span class="sxs-lookup"><span data-stu-id="612fd-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="612fd-214">不幸的是，這不會將變更發佈至 Web 前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="612fd-215">讓我們稍微再變更該虛擬機器，以啟用一個簡單但很有效率的機制來發佈變更，讓您可以在實際環境中快速地觀察變更的效果。</span><span class="sxs-lookup"><span data-stu-id="612fd-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="612fd-216">設定 Web 前端虛擬機器</span><span class="sxs-lookup"><span data-stu-id="612fd-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="612fd-217">您應該記得，我們先前在 Web 前端虛擬機器上建立 node-todo 儲存機制的裸機複製品。</span><span class="sxs-lookup"><span data-stu-id="612fd-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="612fd-218">原來這個動作會建立新的 Git 遠端，讓變更推送到那裡。</span><span class="sxs-lookup"><span data-stu-id="612fd-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="612fd-219">不過，只是推送至此遠端無法提供開發人員處理程式碼時所尋找的快速反覆模型。</span><span class="sxs-lookup"><span data-stu-id="612fd-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="612fd-220">我們希望做的是確保推送至虛擬機器上的遠端儲存機制時，執行中的待辦事項應用程式會自動更新。</span><span class="sxs-lookup"><span data-stu-id="612fd-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="612fd-221">所幸，這使用 git 就能輕易達成。</span><span class="sxs-lookup"><span data-stu-id="612fd-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="612fd-222">Git 公開一些會在特定時間呼叫的勾點，可對儲存機制上採取的動作有所反應。</span><span class="sxs-lookup"><span data-stu-id="612fd-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="612fd-223">這些是使用儲存機制的 `hooks` 資料夾中的殼層指令碼來指定。</span><span class="sxs-lookup"><span data-stu-id="612fd-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="612fd-224">自動更新案例最適合的勾點是 `post-update` 事件。</span><span class="sxs-lookup"><span data-stu-id="612fd-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="612fd-225">在 Web 前端虛擬機器的 SSH 工作階段，切換至 `~/node-todo.git/hooks` 目錄，並將下列內容新增至名為 `post-update` 的檔案 (將 `machinename` 和 `region` 換成您的 MongoDB 虛擬機器資訊)：</span><span class="sxs-lookup"><span data-stu-id="612fd-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="612fd-226">請執行下列命令來確定這個檔案可執行：</span><span class="sxs-lookup"><span data-stu-id="612fd-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="612fd-227">此指令碼可確保目前的伺服器應用程式已停止、複製的儲存機制中的程式碼已更新為最新、滿足任何更新的相依性，以及已重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="612fd-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="612fd-228">它也可確保已設定環境來準備接收我們的第一個應用程式更新，從環境變數取得 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="612fd-229">設定您的開發電腦</span><span class="sxs-lookup"><span data-stu-id="612fd-229">Configuring your Development Machine</span></span>
<span data-ttu-id="612fd-230">現在讓我們將您的開發電腦連接到 Web 前端虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="612fd-231">這就像在虛擬機器上新增裸機儲存機制作為遠端那麼簡單。</span><span class="sxs-lookup"><span data-stu-id="612fd-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="612fd-232">執行下列命令來執行這項操作 (將 *user* 換成您的 Web 前端虛擬機器登入名稱，並視情況取代 *machinename* 和 *region*)：</span><span class="sxs-lookup"><span data-stu-id="612fd-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="612fd-233">這就是將變更推送 (事實上是發佈) 至 Web 前端虛擬機器所需的全部動作。</span><span class="sxs-lookup"><span data-stu-id="612fd-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="612fd-234">發佈更新</span><span class="sxs-lookup"><span data-stu-id="612fd-234">Publishing Updates</span></span>
<span data-ttu-id="612fd-235">讓我們發佈目前為止已完成的一項變更，使應用程式使用我們自己的 MongoDB 執行個體</span><span class="sxs-lookup"><span data-stu-id="612fd-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="612fd-236">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="612fd-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
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
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="612fd-237">此命令完成後，請嘗試在網頁瀏覽器中重新整理應用程式。</span><span class="sxs-lookup"><span data-stu-id="612fd-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="612fd-238">您應該可以看到此處顯示的待辦事項清單是空的，且不再繫結到已部署的共用 MongoDB 執行個體。</span><span class="sxs-lookup"><span data-stu-id="612fd-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="612fd-239">在本教學課程最後，讓我們再完成另一項更明顯的變更。</span><span class="sxs-lookup"><span data-stu-id="612fd-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="612fd-240">在您的開發電腦上，使用您喜好的編輯器開啟 node-todo/public/index.html 檔案。</span><span class="sxs-lookup"><span data-stu-id="612fd-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="612fd-241">找出 jumbotron 標頭，將標題 "I'm a Todo-aholic" 變更為 "I'm a Todo-aholic on Azure!"。</span><span class="sxs-lookup"><span data-stu-id="612fd-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="612fd-242">現在讓我們確認：</span><span class="sxs-lookup"><span data-stu-id="612fd-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="612fd-243">這一次，在將變更推回至 GitHub 儲存機制之前，讓我們先將變更發佈至 Azure：</span><span class="sxs-lookup"><span data-stu-id="612fd-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="612fd-244">此命令完成之後，重新整理網頁，您會看到所做的變更。</span><span class="sxs-lookup"><span data-stu-id="612fd-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="612fd-245">因為看起來沒問題，請將變更推回至原始遠端：</span><span class="sxs-lookup"><span data-stu-id="612fd-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="612fd-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="612fd-246">Next Steps</span></span>
<span data-ttu-id="612fd-247">這篇文章說明如何將 Node.js 應用程式部署到 Azure 中執行的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="612fd-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="612fd-248">若要深入了解 Azure 中的 Linux 虛擬機器，請參閱 [Azure 上的 Linux 簡介](/documentation/articles/virtual-machines-linux-introduction/)。</span><span class="sxs-lookup"><span data-stu-id="612fd-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="612fd-249">如需如何在 Azure 上開發 Node.js 應用程式的詳細資訊，請參閱 [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="612fd-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

