---
title: "快速入門-aaaAzure 建立 Windows VM 入口網站 |Microsoft 文件"
description: "Azure 快速入門 - 建立 Windows VM 入口網站"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="1d35f-103">建立 Windows 虛擬機器以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1d35f-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="1d35f-104">您可以透過 hello Azure 入口網站建立 azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1d35f-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="1d35f-105">此方法可提供以瀏覽器為基礎的使用者介面，以便建立和設定虛擬機器，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="1d35f-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="1d35f-106">此快速入門引導您逐步建立虛擬機器和 hello VM 上安裝 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d35f-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="1d35f-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="1d35f-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="1d35f-108">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d35f-108">Log in tooAzure</span></span>

<span data-ttu-id="1d35f-109">登入 toohello http://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1d35f-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="1d35f-110">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d35f-110">Create virtual machine</span></span>

1. <span data-ttu-id="1d35f-111">按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d35f-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="1d35f-112">選取 [計算]，然後選取 [Windows Server 2016 Datacenter]。</span><span class="sxs-lookup"><span data-stu-id="1d35f-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="1d35f-113">輸入 hello 虛擬機器資訊。</span><span class="sxs-lookup"><span data-stu-id="1d35f-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="1d35f-114">在此輸入 hello 使用者名稱和密碼是使用的 toolog toohello 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="1d35f-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="1d35f-115">完成時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d35f-115">When complete, click **OK**.</span></span>

    ![在 hello 入口網站的刀鋒視窗中輸入 VM 的基本資訊](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="1d35f-117">選取 hello VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="1d35f-117">Select a size for hello VM.</span></span> <span data-ttu-id="1d35f-118">多個的大小，選取 toosee**檢視所有**或變更 hello**支援磁碟類型**篩選器。</span><span class="sxs-lookup"><span data-stu-id="1d35f-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![顯示 VM 大小的螢幕擷取畫面](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="1d35f-120">Hello 設定 刀鋒視窗上保留 hello 預設值，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="1d35f-121">在 hello 摘要 頁面上，按一下 **確定**toostart hello 虛擬機器部署。</span><span class="sxs-lookup"><span data-stu-id="1d35f-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="1d35f-122">hello VM 將會是已釘選的 toohello Azure 入口網站的儀表板。</span><span class="sxs-lookup"><span data-stu-id="1d35f-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="1d35f-123">Hello 部署完成後，請 hello VM 摘要刀鋒視窗會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="1d35f-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="1d35f-124">Toovirtual 機器連線</span><span class="sxs-lookup"><span data-stu-id="1d35f-124">Connect toovirtual machine</span></span>

<span data-ttu-id="1d35f-125">建立遠端桌面連線 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1d35f-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="1d35f-126">按一下 hello**連接**hello 虛擬機器內容 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d35f-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="1d35f-127">隨即建立並下載遠端桌面通訊協定檔案 (.rdp 檔案)。</span><span class="sxs-lookup"><span data-stu-id="1d35f-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![入口網站 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="1d35f-129">tooconnect tooyour VM，開啟 hello 下載 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="1d35f-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="1d35f-130">出現提示時，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="1d35f-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="1d35f-131">在 Mac 上，您需要這類 RDP 用戶端[遠端桌面用戶端](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)從 hello Mac App Store。</span><span class="sxs-lookup"><span data-stu-id="1d35f-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="1d35f-132">Hello 使用者名稱和密碼建立 hello 的虛擬機器時所指定的輸入，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="1d35f-133">您可能會收到 hello 登入程序期間憑證警告。</span><span class="sxs-lookup"><span data-stu-id="1d35f-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="1d35f-134">按一下**是**或**繼續**tooproceed hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1d35f-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="1d35f-135">使用 PowerShell 安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="1d35f-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="1d35f-136">Hello 虛擬機器上，啟動 PowerShell 工作階段並執行下列命令 tooinstall IIS hello。</span><span class="sxs-lookup"><span data-stu-id="1d35f-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="1d35f-137">完成之後，結束 hello RDP 工作階段，傳回 hello Azure 入口網站中的 hello VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="1d35f-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="1d35f-138">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="1d35f-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="1d35f-139">網路安全性群組 (NSG) 可保護輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="1d35f-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="1d35f-140">從 hello Azure 入口網站建立 VM 時，連接埠 3389 RDP 連線就會建立輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="1d35f-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="1d35f-141">因為此 VM 裝載的網頁伺服器時，NSG 規則需要 toobe 建立的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="1d35f-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="1d35f-142">Hello 虛擬機器上，按一下 hello hello 名稱**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="1d35f-143">選取 hello**網路安全性群組**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-143">Select hello **network security group**.</span></span> <span data-ttu-id="1d35f-144">hello NSG 可以使用來識別 hello**類型**資料行。</span><span class="sxs-lookup"><span data-stu-id="1d35f-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="1d35f-145">在 hello 左側功能表中，在 設定 上按一下**輸入安全性規則**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="1d35f-146">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1d35f-146">Click on **Add**.</span></span>
5. <span data-ttu-id="1d35f-147">在 [名稱] 中輸入 **http**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-147">In **Name**, type **http**.</span></span> <span data-ttu-id="1d35f-148">請確定**連接埠範圍**設定 too80 和**動作**設定得**允許**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="1d35f-149">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d35f-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="1d35f-150">檢視 hello IIS [歡迎使用] 頁面</span><span class="sxs-lookup"><span data-stu-id="1d35f-150">View hello IIS welcome page</span></span>

<span data-ttu-id="1d35f-151">與 IIS 安裝，且連接埠 80 開啟 tooyour VM、 hello 網頁伺服器現在可以從 hello 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="1d35f-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="1d35f-152">開啟網頁瀏覽器，並輸入 hello VM 的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1d35f-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="1d35f-153">hello 公用 IP 位址可以找到 hello hello Azure 入口網站中的 VM 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d35f-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![IIS 預設網站](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="1d35f-155">清除資源</span><span class="sxs-lookup"><span data-stu-id="1d35f-155">Clean up resources</span></span>

<span data-ttu-id="1d35f-156">當不再需要請刪除 hello 資源群組、 虛擬機器和相關的所有資源。</span><span class="sxs-lookup"><span data-stu-id="1d35f-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1d35f-157">toodo 因此從 hello 虛擬機器刀鋒視窗中選取 hello 資源群組，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1d35f-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d35f-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d35f-158">Next steps</span></span>

<span data-ttu-id="1d35f-159">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d35f-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="1d35f-160">進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Windows Vm。</span><span class="sxs-lookup"><span data-stu-id="1d35f-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d35f-161">Azure Windows 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="1d35f-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
