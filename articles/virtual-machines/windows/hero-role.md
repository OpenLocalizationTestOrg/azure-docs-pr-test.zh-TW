---
title: "在第一個 Windows VM 上安裝 IIS | Microsoft Docs"
description: "藉由安裝 IIS 並使用 Azure 入口網站來開啟連接埠 80，試驗您的第一個 Windows 虛擬機器。"
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="2ce42-103">試驗在 Windows VM 上安裝角色</span><span class="sxs-lookup"><span data-stu-id="2ce42-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="2ce42-104">在讓您的第一部虛擬機器 (VM) 啟動並正常執行之後，您可以接著安裝軟體和服務。</span><span class="sxs-lookup"><span data-stu-id="2ce42-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="2ce42-105">針對本教學課程，我們將使用 Windows Server VM 上的「伺服器管理員」來安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="2ce42-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="2ce42-106">接著，我們將使用 Azure 入口網站對 IIS 流量開啟連接埠 80 來建立「網路安全性群組」(NSG)。</span><span class="sxs-lookup"><span data-stu-id="2ce42-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="2ce42-107">如果您尚未建立第一個 VM，您應該先返回 [在 Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，然後再繼續此教學課程。</span><span class="sxs-lookup"><span data-stu-id="2ce42-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="2ce42-108">確認 VM 正在執行</span><span class="sxs-lookup"><span data-stu-id="2ce42-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="2ce42-109">開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ce42-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ce42-110">在 [中樞] 功能表上，按一下 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="2ce42-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="2ce42-111">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ce42-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="2ce42-112">如果狀態為 [已停止 (已解除配置)]，請按一下 VM [基本資訊] 刀鋒視窗上的 [啟動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2ce42-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="2ce42-113">如果狀態為 [正在執行] ，則您可以移至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="2ce42-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="2ce42-114">連線至虛擬機器並登入</span><span class="sxs-lookup"><span data-stu-id="2ce42-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="2ce42-115">在 [中樞] 功能表上，按一下 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="2ce42-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="2ce42-116">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ce42-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="2ce42-117">在虛擬機器的刀鋒視窗中，按一下 [ **連線**]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="2ce42-118">這會建立並下載遠端桌面通訊協定檔案 (.rdp 檔案)，該檔案就像是用來連接到您的電腦的捷徑。</span><span class="sxs-lookup"><span data-stu-id="2ce42-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="2ce42-119">您可能想要將此檔案儲存至桌面，以便存取。</span><span class="sxs-lookup"><span data-stu-id="2ce42-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="2ce42-120">**開啟** 此檔案以連接到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="2ce42-120">**Open** this file to connect to your VM.</span></span>
   
    ![顯示如何連接至 VM 的 Azure 入口網站螢幕擷取畫面](./media/hero-role/connect.png)
3. <span data-ttu-id="2ce42-122">您會收到警告，表示 .rdp 來自未知的發行者。</span><span class="sxs-lookup"><span data-stu-id="2ce42-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="2ce42-123">這是正常現象。</span><span class="sxs-lookup"><span data-stu-id="2ce42-123">This is normal.</span></span> <span data-ttu-id="2ce42-124">在 [遠端桌面] 視窗中按一下 [連接]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="2ce42-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![未知發行者相關警告的螢幕擷取畫面](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="2ce42-126">在 [Windows 安全性] 視窗中，針對您建立 VM 時所建立的本機帳戶，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2ce42-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="2ce42-127">使用者名稱會輸入為 vmname&#92;username，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![輸入 VM 名稱、使用者名稱及密碼時的螢幕擷取畫面](./media/hero-role/credentials.png)
5. <span data-ttu-id="2ce42-129">您會收到一個指出無法驗證憑證的警告。</span><span class="sxs-lookup"><span data-stu-id="2ce42-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="2ce42-130">這是正常現象。</span><span class="sxs-lookup"><span data-stu-id="2ce42-130">This is normal.</span></span> <span data-ttu-id="2ce42-131">按一下 [是]  來確認虛擬機器的身分識別，並完成登入。</span><span class="sxs-lookup"><span data-stu-id="2ce42-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![顯示驗證 VM 身分識別相關訊息的螢幕擷取畫面](./media/hero-role/cert-warning.png)

<span data-ttu-id="2ce42-133">如果嘗試連線時遇到問題，請參閱 [針對執行 Windows 之 Azure 虛擬機器的遠端桌面連線進行疑難排解](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2ce42-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="2ce42-134">在您的 VM 上安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="2ce42-134">Install IIS on your VM</span></span>
<span data-ttu-id="2ce42-135">您現在已登入 VM，我們將安裝一個伺服器角色，以便您進行更多試驗。</span><span class="sxs-lookup"><span data-stu-id="2ce42-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="2ce42-136">開啟 [伺服器管理員]  \(如果尚未開啟)。</span><span class="sxs-lookup"><span data-stu-id="2ce42-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="2ce42-137">按一下 [啟動] 功能表，然後按一下 [伺服器管理員]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="2ce42-138">在 [伺服器管理員] 中，選取左窗格中的 [本機伺服器]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="2ce42-139">在功能表中，選取 [管理] > [新增角色及功能]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="2ce42-140">在「新增角色及功能精靈」的 [安裝類型] 頁面上，選擇 [角色型或功能型安裝]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![顯示 [安裝類型] 的 [新增角色及功能精靈] 索引標籤的螢幕擷取畫面](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="2ce42-142">從伺服器集區中選取 VM，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2ce42-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="2ce42-143">在 [伺服器角色] 頁面上，選取 [Web 伺服器 (IIS)]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![顯示 [伺服器角色] 的 [新增角色及功能精靈] 索引標籤的螢幕擷取畫面](./media/hero-role/add-iis.png)
7. <span data-ttu-id="2ce42-145">在新增 IIS 所需功能的相關快顯視窗中，確定已選取 [包含管理工具]，然後按一下 [新增功能]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="2ce42-146">當快顯視窗關閉時，請在精靈中按 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="2ce42-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![顯示用以確認新增 IIS 角色之快顯視窗的螢幕擷取畫面](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="2ce42-148">在功能頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2ce42-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="2ce42-149">在 [Web 伺服器角色 (IIS)] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="2ce42-150">在 [角色服務] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="2ce42-151">在 [確認] 頁面中上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="2ce42-152">安裝完成時，按一下精靈上的 [關閉]  。</span><span class="sxs-lookup"><span data-stu-id="2ce42-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="2ce42-153">開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="2ce42-153">Open port 80</span></span>
<span data-ttu-id="2ce42-154">為了讓您的 VM 透過連接埠 80 接收輸入流量，您必須將輸入規則新增至網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="2ce42-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="2ce42-155">開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2ce42-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ce42-156">在 [虛擬機器]  中，選取您所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="2ce42-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="2ce42-157">在虛擬機器設定中，選取 [網路介面]  ，然後選取現有的網路介面。</span><span class="sxs-lookup"><span data-stu-id="2ce42-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![顯示網路介面的虛擬機器設定的螢幕擷取畫面](./media/hero-role/network-interface.png)
4. <span data-ttu-id="2ce42-159">在網路介面的 [基本資訊] 中，按一下 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![顯示網路介面的 [基本資訊] 區段的螢幕擷取畫面](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="2ce42-161">在 NSG 的 [基本資訊] 刀鋒視窗中，您應該會有一個 **default-allow-rdp** 的現有預設輸入規則可讓您登入 VM。</span><span class="sxs-lookup"><span data-stu-id="2ce42-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="2ce42-162">您將加入另一個允許 IIS 流量的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="2ce42-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="2ce42-163">按一下 [輸入安全性規則] 。</span><span class="sxs-lookup"><span data-stu-id="2ce42-163">Click **Inbound security rule**.</span></span>
   
    ![顯示 NSG 的 [基本資訊] 區段的螢幕擷取畫面](./media/hero-role/inbound.png)
6. <span data-ttu-id="2ce42-165">在 [輸入安全性規則] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![顯示用以新增安全性規則之按鈕的螢幕擷取畫面](./media/hero-role/add-rule.png)
7. <span data-ttu-id="2ce42-167">在 [輸入安全性規則] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="2ce42-168">在連接埠範圍中輸入 **80**，請確定已選取 [允許]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="2ce42-169">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-169">When you are done, click **OK**.</span></span>
   
    ![顯示用以新增安全性規則之按鈕的螢幕擷取畫面](./media/hero-role/port-80.png)

<span data-ttu-id="2ce42-171">如需 NSG、輸入和輸出規則的詳細資訊，請參閱 [允許使用 Azure 入口網站從外部存取您的 VM](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2ce42-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="2ce42-172">連接到預設 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="2ce42-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="2ce42-173">在 Azure 入口網站中，按一下 [虛擬機器]  ，然後選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="2ce42-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="2ce42-174">在 [基本資訊] 刀鋒視窗中，複製您的 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="2ce42-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![顯示何處尋找 VM 公用 IP 位址的螢幕擷取畫面](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="2ce42-176">開啟瀏覽器並在網址列中，輸入您的公用 IP 位址︰http://<publicIPaddress>，然後按一下 **Enter** 前往該位址。</span><span class="sxs-lookup"><span data-stu-id="2ce42-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="2ce42-177">您的瀏覽器應該會開啟預設的 IIS 網頁。</span><span class="sxs-lookup"><span data-stu-id="2ce42-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="2ce42-178">它看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="2ce42-178">It looks something like this:</span></span>
   
    ![顯示預設 IIS 頁面在瀏覽器中樣貌的螢幕擷取畫面](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="2ce42-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ce42-180">Next steps</span></span>
* <span data-ttu-id="2ce42-181">您也可以體驗 [附加資料磁碟](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ce42-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="2ce42-182">資料磁碟可為虛擬機器提供更多的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="2ce42-182">Data disks provide more storage for your virtual machine.</span></span>

