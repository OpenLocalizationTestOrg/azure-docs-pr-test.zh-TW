---
title: "第一個 Windows VM 上的 IIS aaaInstall |Microsoft 文件"
description: "試驗您第一次安裝 IIS，並開啟連接埠 80 使用的 Windows 虛擬機器 hello Azure 入口網站。"
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
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="a9030-103">試驗在 Windows VM 上安裝角色</span><span class="sxs-lookup"><span data-stu-id="a9030-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="a9030-104">一旦第一個虛擬機器 (VM) 設定和執行，您可以移動 tooinstalling 的軟體和服務。</span><span class="sxs-lookup"><span data-stu-id="a9030-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="a9030-105">此教學課程中，我們 toouse 伺服器管理員在 hello Windows Server VM tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="a9030-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="a9030-106">然後，我們會建立網路安全性群組 (NSG) 使用 hello Azure 入口網站 tooopen 連接埠 80 tooIIS 流量。</span><span class="sxs-lookup"><span data-stu-id="a9030-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="a9030-107">如果您尚未建立您的第一個 VM，您應該移回太[hello Azure 入口網站中建立第一個 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)再繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="a9030-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="a9030-108">請確認 VM 正在執行中的 hello</span><span class="sxs-lookup"><span data-stu-id="a9030-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="a9030-109">開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a9030-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9030-110">在 hello 中樞功能表中，按一下 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="a9030-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="a9030-111">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a9030-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="a9030-112">如果 hello 狀態是**已停止 （取消配置）**，按一下 hello**啟動**按鈕 hello **Essentials**刀鋒視窗中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a9030-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="a9030-113">如果 hello 狀態是**執行**，您可以移 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a9030-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="a9030-114">連接 toohello 虛擬機器並登入</span><span class="sxs-lookup"><span data-stu-id="a9030-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="a9030-115">在 hello 中樞功能表中，按一下 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="a9030-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="a9030-116">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a9030-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="a9030-117">在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="a9030-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="a9030-118">這會建立並下載遠端桌面通訊協定檔案 （.rdp 檔案），就像是快顯 tooconnect tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="a9030-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="a9030-119">您可能想 toosave hello 檔案 tooyour 桌面，以方便存取。</span><span class="sxs-lookup"><span data-stu-id="a9030-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="a9030-120">**開啟**此檔案 tooconnect tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="a9030-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![螢幕擷取畫面的 hello Azure 入口網站的顯示方式 tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="a9030-122">您會收到警告該 hello.rdp 取自未知的發行者。</span><span class="sxs-lookup"><span data-stu-id="a9030-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="a9030-123">這是正常現象。</span><span class="sxs-lookup"><span data-stu-id="a9030-123">This is normal.</span></span> <span data-ttu-id="a9030-124">在 hello 遠端桌面視窗中，按一下 **連接**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a9030-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![未知發行者相關警告的螢幕擷取畫面](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="a9030-126">在 [hello Windows 安全性] 視窗中，型別 hello 使用者名稱和密碼 hello 建立時，您所建立的本機帳戶的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a9030-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="a9030-127">hello 使用者名稱輸入為*vmname*&#92;*使用者名稱*，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a9030-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![輸入 hello VM 名稱、 使用者名稱和密碼的螢幕擷取畫面](./media/hero-role/credentials.png)
5. <span data-ttu-id="a9030-129">您會收到警告無法驗證該 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="a9030-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="a9030-130">這是正常現象。</span><span class="sxs-lookup"><span data-stu-id="a9030-130">This is normal.</span></span> <span data-ttu-id="a9030-131">按一下**是**tooverify hello hello 虛擬機器的身分識別，並完成登入。</span><span class="sxs-lookup"><span data-stu-id="a9030-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![螢幕擷取畫面顯示一則訊息 trap 驗證 hello 識別 hello VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="a9030-133">如果您在執行 tootrouble tooconnect 再試一次時，請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a9030-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="a9030-134">在您的 VM 上安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="a9030-134">Install IIS on your VM</span></span>
<span data-ttu-id="a9030-135">既然您已登入 toohello VM，我們會安裝伺服器角色，以便您可以試驗更多。</span><span class="sxs-lookup"><span data-stu-id="a9030-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="a9030-136">開啟 [伺服器管理員]  \(如果尚未開啟)。</span><span class="sxs-lookup"><span data-stu-id="a9030-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="a9030-137">按一下 hello**啟動**功能表，然後再按一下**伺服器管理員**。</span><span class="sxs-lookup"><span data-stu-id="a9030-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="a9030-138">在**伺服器管理員**，選取**本機伺服器**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="a9030-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="a9030-139">在 hello 功能表中，選取 **管理** > **新增角色及功能**。</span><span class="sxs-lookup"><span data-stu-id="a9030-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="a9030-140">在 [hello 新增角色及功能精靈] 的 hello**安裝類型**頁面上，選擇**角色型或功能型安裝**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9030-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![螢幕擷取畫面顯示 hello 新增角色及功能精靈] 索引標籤的 [安裝類型](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="a9030-142">選取 hello VM 從 hello 伺服器集區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9030-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="a9030-143">在 hello**伺服器角色**頁面上，選取**網頁伺服器 (IIS)**。</span><span class="sxs-lookup"><span data-stu-id="a9030-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![螢幕擷取畫面顯示 hello 新增角色及功能精靈] 索引標籤的 [伺服器角色](./media/hero-role/add-iis.png)
7. <span data-ttu-id="a9030-145">在 新增所需的 IIS 功能的相關快顯 hello，請確定**包含管理工具**已選取，然後按一下**新增功能**。</span><span class="sxs-lookup"><span data-stu-id="a9030-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="a9030-146">當快顯 hello 關閉時，按一下**下一步**hello 精靈中。</span><span class="sxs-lookup"><span data-stu-id="a9030-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![顯示快顯 tooconfirm 新增 hello IIS 角色螢幕擷取畫面](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="a9030-148">在 hello 功能頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9030-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="a9030-149">在 hello**網頁伺服器 (IIS)**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9030-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="a9030-150">在 hello**角色服務**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a9030-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="a9030-151">在 hello**確認**頁面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="a9030-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="a9030-152">Hello 安裝完成時，按一下**關閉**hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="a9030-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="a9030-153">開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="a9030-153">Open port 80</span></span>
<span data-ttu-id="a9030-154">為了讓 VM tooaccept 輸入流量透過連接埠 80，您需要 tooadd 輸入的規則 toohello 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="a9030-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="a9030-155">開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a9030-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a9030-156">在**虛擬機器**選取 hello 您所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="a9030-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="a9030-157">在 hello 虛擬機器設定中，選取**網路介面**，然後選取 hello 現有網路介面。</span><span class="sxs-lookup"><span data-stu-id="a9030-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![顯示 hello 的 hello 虛擬機器設定網路介面螢幕擷取畫面](./media/hero-role/network-interface.png)
4. <span data-ttu-id="a9030-159">在**Essentials** hello 網路介面，按一下 hello**網路安全性群組**。</span><span class="sxs-lookup"><span data-stu-id="a9030-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![顯示 hello Essentials > 一節 hello 網路介面的螢幕擷取畫面](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="a9030-161">在 hello **Essentials** hello NSG 刀鋒視窗中的，您應該有一個現有的預設輸入規則**預設允許 rdp**它可讓您 toolog toohello VM 中。</span><span class="sxs-lookup"><span data-stu-id="a9030-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="a9030-162">您會加入另一個輸入的規則 tooallow IIS 流量。</span><span class="sxs-lookup"><span data-stu-id="a9030-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="a9030-163">按一下 [輸入安全性規則] 。</span><span class="sxs-lookup"><span data-stu-id="a9030-163">Click **Inbound security rule**.</span></span>
   
    ![顯示 hello hello NSG 的 Essentials > 一節螢幕擷取畫面](./media/hero-role/inbound.png)
6. <span data-ttu-id="a9030-165">在 [輸入安全性規則] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a9030-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![安全性規則顯示 hello 按鈕 tooadd 螢幕擷取畫面](./media/hero-role/add-rule.png)
7. <span data-ttu-id="a9030-167">在 [輸入安全性規則] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a9030-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="a9030-168">型別**80**在 hello 連接埠範圍，並確定**允許**已選取。</span><span class="sxs-lookup"><span data-stu-id="a9030-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="a9030-169">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a9030-169">When you are done, click **OK**.</span></span>
   
    ![安全性規則顯示 hello 按鈕 tooadd 螢幕擷取畫面](./media/hero-role/port-80.png)

<span data-ttu-id="a9030-171">如需有關 Nsg，輸入和輸出規則，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a9030-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="a9030-172">連接 toohello 預設 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="a9030-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="a9030-173">在 hello Azure 入口網站，按一下 **虛擬機器**，然後選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="a9030-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="a9030-174">在 hello **Essentials**刀鋒視窗，複製您**公用 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="a9030-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![螢幕擷取畫面顯示其中 toofind hello VM 的公用 IP 位址](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="a9030-176">開啟瀏覽器，並在 hello 網址列中輸入公用 IP 位址如下： http://<publicIPaddress>按一下**Enter** toogo toothat 位址。</span><span class="sxs-lookup"><span data-stu-id="a9030-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="a9030-177">您的瀏覽器應該開啟 hello 預設 IIS web 網頁。</span><span class="sxs-lookup"><span data-stu-id="a9030-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="a9030-178">它看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="a9030-178">It looks something like this:</span></span>
   
    ![在瀏覽器中顯示哪些 hello 預設 IIS 頁面螢幕擷取畫面看起來像](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="a9030-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9030-180">Next steps</span></span>
* <span data-ttu-id="a9030-181">您也可以試驗[連接資料磁碟](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a9030-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="a9030-182">資料磁碟可為虛擬機器提供更多的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="a9030-182">Data disks provide more storage for your virtual machine.</span></span>

