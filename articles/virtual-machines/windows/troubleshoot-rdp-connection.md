---
title: "與 RDP tooa 在 Azure 中的 Windows VM 連接 aaaCannot |Microsoft 文件"
description: "當您無法連接 tooyour Windows 虛擬機器使用遠端桌面在 Azure 中疑難排解問題"
keywords: "遠端桌面的錯誤，遠端桌面連線錯誤，無法連接 tooVM，遠端桌面的疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a><span data-ttu-id="4b5ad-104">疑難排解遠端桌面連線 tooan Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4b5ad-104">Troubleshoot Remote Desktop connections tooan Azure virtual machine</span></span>
<span data-ttu-id="4b5ad-105">您的 VM 時，可以基於各種原因，讓您無法 tooaccess 失敗 hello 遠端桌面通訊協定 (RDP) 連線 tooyour windows Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-105">hello Remote Desktop Protocol (RDP) connection tooyour Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable tooaccess your VM.</span></span> <span data-ttu-id="4b5ad-106">hello 問題可能是以 hello hello VM、 hello 網路連線或 hello 主機電腦上的遠端桌面用戶端上的遠端桌面服務。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-106">hello issue can be with hello Remote Desktop service on hello VM, hello network connection, or hello Remote Desktop client on your host computer.</span></span> <span data-ttu-id="4b5ad-107">這篇文章會引導您完成 hello 最常見的方法 tooresolve RDP 連線問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-107">This article guides you through some of hello most common methods tooresolve RDP connection issues.</span></span> 

<span data-ttu-id="4b5ad-108">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="4b5ad-109">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="4b5ad-110">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-110">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="4b5ad-111">快速疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="4b5ad-111">Quick troubleshooting steps</span></span>
<span data-ttu-id="4b5ad-112">每個疑難排解的步驟之後，嘗試重新連接 toohello VM:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-112">After each troubleshooting step, try reconnecting toohello VM:</span></span>

1. <span data-ttu-id="4b5ad-113">重設遠端桌面組態。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-113">Reset Remote Desktop configuration.</span></span>
2. <span data-ttu-id="4b5ad-114">檢查網路安全性群組規則 / 雲端服務端點。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-114">Check Network Security Group rules / Cloud Services endpoints.</span></span>
3. <span data-ttu-id="4b5ad-115">檢閱 VM 主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-115">Review VM console logs.</span></span>
4. <span data-ttu-id="4b5ad-116">重設 hello NIC hello VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-116">Reset hello NIC for hello VM.</span></span>
5. <span data-ttu-id="4b5ad-117">請檢查 hello VM 資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-117">Check hello VM Resource Health.</span></span>
6. <span data-ttu-id="4b5ad-118">重設您的 VM 密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-118">Reset your VM password.</span></span>
7. <span data-ttu-id="4b5ad-119">重新啟動您的 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-119">Restart your VM.</span></span>
8. <span data-ttu-id="4b5ad-120">重新部署您的 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-120">Redeploy your VM.</span></span>

<span data-ttu-id="4b5ad-121">如果您需要更詳細的步驟與說明，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-121">Continue reading if you need more detailed steps and explanations.</span></span> <span data-ttu-id="4b5ad-122">請確認區域網路設備 (例如路由器和防火牆) 沒有封鎖輸出 TCP 連接埠 3389，如[詳細的 RDP 疑難排解案例](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中所述。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-122">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="4b5ad-123">如果 hello**連接**按鈕 hello 入口網站中的 「 您的 VM 會變成灰色外，您不是透過連接的 tooAzure [Express Route](../../expressroute/expressroute-introduction.md)或[站對站 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)連線，您需要toocreate 及指派您 VM 的公用 IP 位址之前，您可以使用 RDP。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-123">If hello **Connect** button for your VM is grayed out in hello portal and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="4b5ad-124">您可以深入了解 [Azure 中的公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-124">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>


## <a name="ways-tootroubleshoot-rdp-issues"></a><span data-ttu-id="4b5ad-125">方式 tootroubleshoot RDP 問題</span><span class="sxs-lookup"><span data-stu-id="4b5ad-125">Ways tootroubleshoot RDP issues</span></span>
<span data-ttu-id="4b5ad-126">您可以疑難排解使用 hello Resource Manager 部署模型，使用其中一種 hello 下列方法建立的 Vm:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-126">You can troubleshoot VMs created using hello Resource Manager deployment model by using one of hello following methods:</span></span>

* <span data-ttu-id="4b5ad-127">[Azure 入口網站](#using-the-azure-portal)-太好了，如果您需要 tooquickly 重設 hello RDP 設定] 或 [使用者認證並不 hello Azure tools 安裝。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-127">[Azure portal](#using-the-azure-portal) - great if you need tooquickly reset hello RDP configuration or user credentials and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="4b5ad-128">[Azure PowerShell](#using-azure-powershell) -如果您想要使用 PowerShell 提示時，快速重設 hello RDP 設定] 或 [使用者認證使用 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-128">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset hello RDP configuration or user credentials using hello Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="4b5ad-129">您也可以找到疑難排解使用 hello 所建立的 Vm 上的步驟[傳統部署模型](#troubleshoot-vms-created-using-the-classic-deployment-model)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-129">You can also find steps on troubleshooting VMs created using hello [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span></span>

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a><span data-ttu-id="4b5ad-130">使用 hello Azure 入口網站的疑難排解</span><span class="sxs-lookup"><span data-stu-id="4b5ad-130">Troubleshoot using hello Azure portal</span></span>
<span data-ttu-id="4b5ad-131">每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="4b5ad-132">如果仍然無法連線，請嘗試 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-132">If you still cannot connect, try hello next step.</span></span>

1. <span data-ttu-id="4b5ad-133">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-133">**Reset your RDP connection**.</span></span> <span data-ttu-id="4b5ad-134">遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-134">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="4b5ad-135">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-136">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-136">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-137">按一下 hello**重設密碼** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-137">Click hello **Reset password** button.</span></span> <span data-ttu-id="4b5ad-138">設定 hello**模式**太**只能重設組態**然後按一下hello**更新**按鈕：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-138">Set hello **Mode** too**Reset configuration only** and then click hello **Update** button:</span></span>
   
    ![重設 hello Azure 入口網站中的 hello RDP 設定](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. <span data-ttu-id="4b5ad-140">**確認網路安全性群組規則**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-140">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="4b5ad-141">使用[IP 流量確認](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)tooconfirm 如果網路安全性群組中的規則會封鎖從虛擬機器的流量 tooor。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-141">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm if a rule in a Network Security Group is blocking traffic tooor from a virtual machine.</span></span> <span data-ttu-id="4b5ad-142">您也可以檢閱有效安全性群組規則 tooensure 輸入 「 允許 」 NSG 規則存在，而且已設定優先權的 RDP 連接埠 （預設值為 3389）。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-142">You can also review effective security group rules tooensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="4b5ad-143">如需詳細資訊，請參閱[使用有效的安全性規則 tootroubleshoot VM 流量流程](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-143">For more information, see [Using Effective Security Rules tootroubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

3. <span data-ttu-id="4b5ad-144">**檢閱 VM 開機診斷**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-144">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="4b5ad-145">此步驟中疑難排解檢閱 hello VM 主控台記錄檔 toodetermine 如果 hello VM 所報告的問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-145">This troubleshooting step reviews hello VM console logs toodetermine if hello VM is reporting an issue.</span></span> <span data-ttu-id="4b5ad-146">並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-146">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="4b5ad-147">特定的疑難排解步驟已超出本文的 hello 範圍，但可能會影響 RDP 連線更多問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-147">Specific troubleshooting steps are beyond hello scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="4b5ad-148">如需有關如何檢閱 hello 主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱[Vm 的開機診斷](boot-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-148">For more information on reviewing hello console logs and VM screenshot, see [Boot Diagnostics for VMs](boot-diagnostics.md).</span></span>

4. <span data-ttu-id="4b5ad-149">**重設 hello NIC VM hello**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-149">**Reset hello NIC for hello VM**.</span></span> <span data-ttu-id="4b5ad-150">如需詳細資訊，請參閱[如何 tooreset Azure Windows vm NIC](reset-network-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-150">For more information, see [how tooreset NIC for Azure Windows VM](reset-network-interface.md).</span></span>
5. <span data-ttu-id="4b5ad-151">**請檢查 VM 資源健全狀況 hello**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-151">**Check hello VM Resource Health**.</span></span> <span data-ttu-id="4b5ad-152">此疑難排解步驟會確認沒有任何已知的問題與 hello 可能會影響連線 toohello VM 的 Azure 平台。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-152">This troubleshooting step verifies there are no known issues with hello Azure platform that may impact connectivity toohello VM.</span></span>
   
    <span data-ttu-id="4b5ad-153">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-153">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-154">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-154">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-155">按一下 hello**資源健全狀況** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-155">Click hello **Resource health** button.</span></span> <span data-ttu-id="4b5ad-156">狀況良好的 VM 會報告為 [可用]：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-156">A healthy VM reports as being **Available**:</span></span>
   
    ![檢查 VM hello Azure 入口網站中的資源健全狀況](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. <span data-ttu-id="4b5ad-158">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-158">**Reset user credentials**.</span></span> <span data-ttu-id="4b5ad-159">當您不確定或忘記 hello 認證時，此疑難排解步驟會重設 hello 上本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-159">This troubleshooting step resets hello password on a local administrator account when you are unsure or have forgotten hello credentials.</span></span>
   
    <span data-ttu-id="4b5ad-160">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-160">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-161">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-161">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-162">按一下 hello**重設密碼** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-162">Click hello **Reset password** button.</span></span> <span data-ttu-id="4b5ad-163">請確定 hello**模式**設定得**重設密碼**，然後輸入您的使用者名稱和新的密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-163">Make sure hello **Mode** is set too**Reset password** and then enter your username and a new password.</span></span> <span data-ttu-id="4b5ad-164">最後，按一下 hello**更新**按鈕：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-164">Finally, click hello **Update** button:</span></span>
   
    ![重設 hello hello Azure 入口網站中的使用者認證](./media/troubleshoot-rdp-connection/reset-password.png)
7. <span data-ttu-id="4b5ad-166">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-166">**Restart your VM**.</span></span> <span data-ttu-id="4b5ad-167">此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-167">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="4b5ad-168">Hello Azure 入口網站中選取您的 VM，然後按一下 hello**概觀** 索引標籤。按一下 hello**重新啟動**按鈕：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-168">Select your VM in hello Azure portal and click hello **Overview** tab. Click hello **Restart** button:</span></span>
   
    ![在 hello Azure 入口網站中重新啟動 VM hello](./media/troubleshoot-rdp-connection/restart-vm.png)
8. <span data-ttu-id="4b5ad-170">**重新部署您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-170">**Redeploy your VM**.</span></span> <span data-ttu-id="4b5ad-171">此步驟中疑難排解重新部署 VM tooanother 主應用程式，Azure toocorrect 內任何基礎的平台或網路問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-171">This troubleshooting step redeploys your VM tooanother host within Azure toocorrect any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="4b5ad-172">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-172">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-173">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-173">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-174">按一下 hello**重新部署**按鈕，然後再按一下**重新部署**:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-174">Click hello **Redeploy** button, and then click **Redeploy**:</span></span>
   
    ![重新部署 hello Azure 入口網站中的 hello VM](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    <span data-ttu-id="4b5ad-176">這項作業完成之後，暫時磁碟資料是遺失和動態 hello VM 會更新相關聯的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-176">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with hello VM are updated.</span></span>

<span data-ttu-id="4b5ad-177">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-177">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-using-azure-powershell"></a><span data-ttu-id="4b5ad-178">使用 Azure PowerShell 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4b5ad-178">Troubleshoot using Azure PowerShell</span></span>
<span data-ttu-id="4b5ad-179">如果您還沒有這麼做，[安裝及設定 hello 最新 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-179">If you haven't already, [install and configure hello latest Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="4b5ad-180">hello 下列範例會使用變數例如`myResourceGroup`， `myVM`，和`myVMAccessExtension`。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-180">hello following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span></span> <span data-ttu-id="4b5ad-181">以您自己的值取代這些變數名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-181">Replace these variable names and locations with your own values.</span></span>

> [!NOTE]
> <span data-ttu-id="4b5ad-182">您使用重設 hello 使用者認證及 hello RDP 組態 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-182">You reset hello user credentials and hello RDP configuration by using hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="4b5ad-183">在下列範例中，hello`myVMAccessExtension`是您指定 hello 程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-183">In hello following examples, `myVMAccessExtension` is a name that you specify as part of hello process.</span></span> <span data-ttu-id="4b5ad-184">如果您先前已使用 hello VMAccessAgent，您可以使用來取得 hello hello 現有擴充功能名稱`Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"`hello VM toocheck hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-184">If you have previously worked with hello VMAccessAgent, you can get hello name of hello existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck hello properties of hello VM.</span></span> <span data-ttu-id="4b5ad-185">hello 輸出 hello 'Extensions' 區段下的外觀 tooview hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-185">tooview hello name, look under hello 'Extensions' section of hello output.</span></span>

<span data-ttu-id="4b5ad-186">每個疑難排解的步驟之後，請再次嘗試連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-186">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="4b5ad-187">如果仍然無法連線，請嘗試 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-187">If you still cannot connect, try hello next step.</span></span>

1. <span data-ttu-id="4b5ad-188">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-188">**Reset your RDP connection**.</span></span> <span data-ttu-id="4b5ad-189">遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-189">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="4b5ad-190">hello 下列範例會重設名為的 VM 上的 hello RDP 連線`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-190">hello follow example resets hello RDP connection on a VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. <span data-ttu-id="4b5ad-191">**確認網路安全性群組規則**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-191">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="4b5ad-192">此疑難排解步驟會確認您的網路安全性群組 toopermit RDP 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-192">This troubleshooting step verifies that you have a rule in your Network Security Group toopermit RDP traffic.</span></span> <span data-ttu-id="4b5ad-193">RDP 的 hello 預設連接埠是 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-193">hello default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="4b5ad-194">規則 toopermit RDP 流量可能不會自動建立時建立您的 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-194">A rule toopermit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="4b5ad-195">首先，指派所有 hello 組態資料的網路安全性群組 toohello`$rules`變數。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-195">First, assign all hello configuration data for your Network Security Group toohello `$rules` variable.</span></span> <span data-ttu-id="4b5ad-196">hello 下列範例會取得 hello 名為的網路安全性群組的相關資訊`myNetworkSecurityGroup`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-196">hello following example obtains information about hello Network Security Group named `myNetworkSecurityGroup` in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    <span data-ttu-id="4b5ad-197">現在，檢視已針對此網路安全性群組的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-197">Now, view hello rules that are configured for this Network Security Group.</span></span> <span data-ttu-id="4b5ad-198">請確認的規則存在 tooallow TCP 連接埠 3389 的傳入連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-198">Verify that a rule exists tooallow TCP port 3389 for inbound connections as follows:</span></span>
   
    ```powershell
    $rules.SecurityRules
    ```
   
    <span data-ttu-id="4b5ad-199">hello 下列範例示範有效的安全性規則，允許 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-199">hello following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="4b5ad-200">您可以看到 `Protocol`、`DestinationPortRange`、`Access` 和 `Direction` 已正確設定︰</span><span class="sxs-lookup"><span data-stu-id="4b5ad-200">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span></span>
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    <span data-ttu-id="4b5ad-201">如果您沒有可允許 RDP 流量的規則，請[建立網路安全性群組規則](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-201">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="4b5ad-202">允許 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-202">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="4b5ad-203">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-203">**Reset user credentials**.</span></span> <span data-ttu-id="4b5ad-204">此疑難排解的步驟會重設 hello hello 您指定當您不確定，或已忘記 hello 認證的本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-204">This troubleshooting step resets hello password on hello local administrator account that you specify when you are unsure of, or have forgotten, hello credentials.</span></span>
   
    <span data-ttu-id="4b5ad-205">首先，指定 hello 使用者名稱和指派新的密碼認證 toohello`$cred`變數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-205">First, specify hello username and a new password by assigning credentials toohello `$cred` variable as follows:</span></span>
   
    ```powershell
    $cred=Get-Credential
    ```
   
    <span data-ttu-id="4b5ad-206">現在，更新您的 VM 上的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-206">Now, update hello credentials on your VM.</span></span> <span data-ttu-id="4b5ad-207">hello 下列範例會更新名為的 VM 上的 hello 認證`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-207">hello following example updates hello credentials on a VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. <span data-ttu-id="4b5ad-208">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-208">**Restart your VM**.</span></span> <span data-ttu-id="4b5ad-209">此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-209">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="4b5ad-210">下列範例會重新啟動的 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-210">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. <span data-ttu-id="4b5ad-211">**重新部署您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-211">**Redeploy your VM**.</span></span> <span data-ttu-id="4b5ad-212">此步驟中疑難排解重新部署 VM tooanother 主應用程式，Azure toocorrect 內任何基礎的平台或網路問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-212">This troubleshooting step redeploys your VM tooanother host within Azure toocorrect any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="4b5ad-213">下列範例重新部署的 hello hello 名為 VM`myVM`在 hello`WestUS`位置並在 hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-213">hello following example redeploys hello VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

<span data-ttu-id="4b5ad-214">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-214">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a><span data-ttu-id="4b5ad-215">疑難排解使用 hello 傳統部署模型所建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="4b5ad-215">Troubleshoot VMs created using hello Classic deployment model</span></span>
<span data-ttu-id="4b5ad-216">每個疑難排解的步驟之後，嘗試重新連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-216">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="4b5ad-217">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-217">**Reset your RDP connection**.</span></span> <span data-ttu-id="4b5ad-218">遠端連接已停用或 Windows 防火牆規則，例如封鎖 RDP 時，此疑難排解的步驟會重設 hello RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-218">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="4b5ad-219">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-219">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-220">按一下 hello **...多個**按鈕，然後按一下**重設遠端存取**:</span><span class="sxs-lookup"><span data-stu-id="4b5ad-220">Click hello **...More** button, then click **Reset Remote Access**:</span></span>
   
    ![重設 hello Azure 入口網站中的 hello RDP 設定](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. <span data-ttu-id="4b5ad-222">**確認雲端服務端點**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-222">**Verify Cloud Services endpoints**.</span></span> <span data-ttu-id="4b5ad-223">此疑難排解步驟會確認您的雲端服務 toopermit RDP 流量的端點。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-223">This troubleshooting step verifies that you have endpoints in your Cloud Services toopermit RDP traffic.</span></span> <span data-ttu-id="4b5ad-224">RDP 的 hello 預設連接埠是 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-224">hello default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="4b5ad-225">規則 toopermit RDP 流量可能不會自動建立時建立您的 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-225">A rule toopermit RDP traffic may not be created automatically when you create your VM.</span></span>
   
   <span data-ttu-id="4b5ad-226">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-226">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-227">按一下 hello**端點**按鈕 tooview hello 端點目前設定為您的 VM。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-227">Click hello **Endpoints** button tooview hello endpoints currently configured for your VM.</span></span> <span data-ttu-id="4b5ad-228">確認存在可允許 TCP 連接埠 3389 上 RDP 流量的端點。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-228">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span></span>
   
   <span data-ttu-id="4b5ad-229">hello 下列範例示範有效的端點，允許 RDP 流量：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-229">hello following example shows valid endpoints that permit RDP traffic:</span></span>
   
   ![確認 hello Azure 入口網站中的雲端服務端點](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   <span data-ttu-id="4b5ad-231">如果您沒有可允許 RDP 流量的端點，請[建立雲端服務端點](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-231">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="4b5ad-232">允許 TCP tooprivate 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-232">Allow TCP tooprivate port 3389.</span></span>
3. <span data-ttu-id="4b5ad-233">**檢閱 VM 開機診斷**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-233">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="4b5ad-234">此步驟中疑難排解檢閱 hello VM 主控台記錄檔 toodetermine 如果 hello VM 所報告的問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-234">This troubleshooting step reviews hello VM console logs toodetermine if hello VM is reporting an issue.</span></span> <span data-ttu-id="4b5ad-235">並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-235">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="4b5ad-236">特定的疑難排解步驟已超出本文的 hello 範圍，但可能會影響 RDP 連線更多問題。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-236">Specific troubleshooting steps are beyond hello scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="4b5ad-237">如需有關如何檢閱 hello 主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱[Vm 的開機診斷](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-237">For more information on reviewing hello console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="4b5ad-238">**請檢查 VM 資源健全狀況 hello**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-238">**Check hello VM Resource Health**.</span></span> <span data-ttu-id="4b5ad-239">此疑難排解步驟會確認沒有任何已知的問題與 hello 可能會影響連線 toohello VM 的 Azure 平台。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-239">This troubleshooting step verifies there are no known issues with hello Azure platform that may impact connectivity toohello VM.</span></span>
   
    <span data-ttu-id="4b5ad-240">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-240">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-241">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-241">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-242">按一下 hello**資源健全狀況** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-242">Click hello **Resource Health** button.</span></span> <span data-ttu-id="4b5ad-243">狀況良好的 VM 會報告為 [可用]：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-243">A healthy VM reports as being **Available**:</span></span>
   
    ![檢查 VM hello Azure 入口網站中的資源健全狀況](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. <span data-ttu-id="4b5ad-245">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-245">**Reset user credentials**.</span></span> <span data-ttu-id="4b5ad-246">此疑難排解的步驟會重設 hello hello 您指定當您不確定或忘記 hello 認證的本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-246">This troubleshooting step resets hello password on hello local administrator account that you specify when you are unsure or have forgotten hello credentials.</span></span>
   
    <span data-ttu-id="4b5ad-247">選取您的 VM 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-247">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="4b5ad-248">捲動 hello 設定窗格 toohello**支援 + 疑難排解**hello 清單的底部附近一節。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-248">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="4b5ad-249">按一下 hello**重設密碼** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-249">Click hello **Reset password** button.</span></span> <span data-ttu-id="4b5ad-250">輸入您的使用者名稱和新密碼。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-250">Enter your username and a new password.</span></span> <span data-ttu-id="4b5ad-251">最後，按一下 hello**儲存**按鈕：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-251">Finally, click hello **Save** button:</span></span>
   
    ![重設 hello hello Azure 入口網站中的使用者認證](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. <span data-ttu-id="4b5ad-253">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-253">**Restart your VM**.</span></span> <span data-ttu-id="4b5ad-254">此疑難排解的步驟可以更正任何基礎的問題已擁有 hello VM 本身。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-254">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="4b5ad-255">Hello Azure 入口網站中選取您的 VM，然後按一下 hello**概觀** 索引標籤。按一下 hello**重新啟動**按鈕：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-255">Select your VM in hello Azure portal and click hello **Overview** tab. Click hello **Restart** button:</span></span>
   
    ![在 hello Azure 入口網站中重新啟動 VM hello](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

<span data-ttu-id="4b5ad-257">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-257">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-specific-rdp-errors"></a><span data-ttu-id="4b5ad-258">針對特定 RDP 錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4b5ad-258">Troubleshoot specific RDP errors</span></span>
<span data-ttu-id="4b5ad-259">嘗試 tooconnect tooyour 透過 RDP 的 VM 時，可能會遇到的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-259">You may encounter a specific error message when trying tooconnect tooyour VM via RDP.</span></span> <span data-ttu-id="4b5ad-260">hello 下面是 hello 最常見的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="4b5ad-260">hello following are hello most common error messages:</span></span>

* <span data-ttu-id="4b5ad-261">[hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器的可用 tooprovide 授權](troubleshoot-specific-rdp-errors.md#rdplicense)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-261">[hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span></span>
* <span data-ttu-id="4b5ad-262">[遠端桌面找不到 hello 電腦 「 名稱 」](troubleshoot-specific-rdp-errors.md#rdpname)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-262">[Remote Desktop can't find hello computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span></span>
* <span data-ttu-id="4b5ad-263">[發生驗證錯誤。hello 本機安全性授權無法連絡](troubleshoot-specific-rdp-errors.md#rdpauth)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-263">[An authentication error has occurred. hello Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span></span>
* <span data-ttu-id="4b5ad-264">[Windows 安全性錯誤：您的認證無法運作](troubleshoot-specific-rdp-errors.md#wincred)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-264">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span></span>
* <span data-ttu-id="4b5ad-265">[這部電腦無法連線遠端電腦的 toohello](troubleshoot-specific-rdp-errors.md#rdpconnect)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-265">[This computer can't connect toohello remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b5ad-266">其他資源</span><span class="sxs-lookup"><span data-stu-id="4b5ad-266">Additional resources</span></span>
<span data-ttu-id="4b5ad-267">如果沒有任何這些錯誤發生，您仍然無法連線 toohello 透過遠端桌面的 VM 讀取詳細的 hello[疑難排解指南針對遠端桌面](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-267">If none of these errors occurred and you still can't connect toohello VM via Remote Desktop, read hello detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4b5ad-268">如需疑難排解存取 VM 上執行的應用程式的步驟，請參閱[疑難排解存取 tooan 應用程式在 Azure VM 上執行](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-268">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access tooan application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="4b5ad-269">如果您有使用安全殼層 (SSH) tooconnect tooa Linux VM 在 Azure 中的問題，請參閱[疑難排解 SSH 連線 tooa 在 Azure 中的 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4b5ad-269">If you are having issues using Secure Shell (SSH) tooconnect tooa Linux VM in Azure, see [Troubleshoot SSH connections tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

