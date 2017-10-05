---
title: "無法透過 RDP 連接到 Azure 中的 Windows VM | Microsoft Docs"
description: "針對無法在 Azure 中使用遠端桌面連接到 Windows 虛擬機器時的問題進行疑難排解"
keywords: "遠端桌面錯誤、遠端桌面連線錯誤、無法連接到 VM、遠端桌面疑難排解"
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
ms.openlocfilehash: 87b6c99c28a95c9be37486717e689baa22804882
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-remote-desktop-connections-to-an-azure-virtual-machine"></a><span data-ttu-id="daf88-104">針對 Azure 虛擬機器的遠端桌面連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="daf88-104">Troubleshoot Remote Desktop connections to an Azure virtual machine</span></span>
<span data-ttu-id="daf88-105">有各式各樣的原因可能導致 Windows 型 Azure 虛擬機器 (VM) 的遠端桌面通訊協定 (RDP) 連線失敗，讓您無法存取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-105">The Remote Desktop Protocol (RDP) connection to your Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable to access your VM.</span></span> <span data-ttu-id="daf88-106">問題可能與 VM 上的遠端桌面服務、網路連線或主機電腦上的遠端桌面用戶端有關。</span><span class="sxs-lookup"><span data-stu-id="daf88-106">The issue can be with the Remote Desktop service on the VM, the network connection, or the Remote Desktop client on your host computer.</span></span> <span data-ttu-id="daf88-107">本文將引導您完成一些可解決 RDP 連線問題的最常見方法。</span><span class="sxs-lookup"><span data-stu-id="daf88-107">This article guides you through some of the most common methods to resolve RDP connection issues.</span></span> 

<span data-ttu-id="daf88-108">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="daf88-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="daf88-109">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="daf88-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="daf88-110">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="daf88-110">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="daf88-111">快速疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="daf88-111">Quick troubleshooting steps</span></span>
<span data-ttu-id="daf88-112">在完成每個疑難排解步驟之後，請嘗試重新連接到 VM：</span><span class="sxs-lookup"><span data-stu-id="daf88-112">After each troubleshooting step, try reconnecting to the VM:</span></span>

1. <span data-ttu-id="daf88-113">重設遠端桌面組態。</span><span class="sxs-lookup"><span data-stu-id="daf88-113">Reset Remote Desktop configuration.</span></span>
2. <span data-ttu-id="daf88-114">檢查網路安全性群組規則 / 雲端服務端點。</span><span class="sxs-lookup"><span data-stu-id="daf88-114">Check Network Security Group rules / Cloud Services endpoints.</span></span>
3. <span data-ttu-id="daf88-115">檢閱 VM 主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="daf88-115">Review VM console logs.</span></span>
4. <span data-ttu-id="daf88-116">重設 VM 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="daf88-116">Reset the NIC for the VM.</span></span>
5. <span data-ttu-id="daf88-117">檢查 VM 資源健康狀態。</span><span class="sxs-lookup"><span data-stu-id="daf88-117">Check the VM Resource Health.</span></span>
6. <span data-ttu-id="daf88-118">重設您的 VM 密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-118">Reset your VM password.</span></span>
7. <span data-ttu-id="daf88-119">重新啟動您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-119">Restart your VM.</span></span>
8. <span data-ttu-id="daf88-120">重新部署您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-120">Redeploy your VM.</span></span>

<span data-ttu-id="daf88-121">如果您需要更詳細的步驟與說明，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="daf88-121">Continue reading if you need more detailed steps and explanations.</span></span> <span data-ttu-id="daf88-122">請確認區域網路設備 (例如路由器和防火牆) 沒有封鎖輸出 TCP 連接埠 3389，如[詳細的 RDP 疑難排解案例](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中所述。</span><span class="sxs-lookup"><span data-stu-id="daf88-122">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="daf88-123">如果 VM 的 [連接] 按鈕呈現灰色，而且您未透過 [Express Route](../../expressroute/expressroute-introduction.md) 或 [網站間 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 連線來連接 Azure，您就必須先建立 VM 並為其指派公用 IP 位址，才能使用 RDP。</span><span class="sxs-lookup"><span data-stu-id="daf88-123">If the **Connect** button for your VM is grayed out in the portal and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="daf88-124">您可以深入了解 [Azure 中的公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="daf88-124">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>


## <a name="ways-to-troubleshoot-rdp-issues"></a><span data-ttu-id="daf88-125">針對 RDP 問題進行疑難排解的方法</span><span class="sxs-lookup"><span data-stu-id="daf88-125">Ways to troubleshoot RDP issues</span></span>
<span data-ttu-id="daf88-126">您可以使用下列其中一種方法，針對使用 Resource Manager 部署模型建立的 VM 進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="daf88-126">You can troubleshoot VMs created using the Resource Manager deployment model by using one of the following methods:</span></span>

* <span data-ttu-id="daf88-127">[Azure 入口網站](#using-the-azure-portal) - 適用於您需要快速重設 RDP 組態或使用者認證，而且未安裝 Azure 工具時。</span><span class="sxs-lookup"><span data-stu-id="daf88-127">[Azure portal](#using-the-azure-portal) - great if you need to quickly reset the RDP configuration or user credentials and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="daf88-128">[Azure PowerShell](#using-azure-powershell) - 如果您已熟悉 PowerShell 提示字元，請使用 Azure PowerShell Cmdlet 快速重設 RDP 組態或使用者認證。</span><span class="sxs-lookup"><span data-stu-id="daf88-128">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset the RDP configuration or user credentials using the Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="daf88-129">您也可以找到有關針對使用[傳統部署模型](#troubleshoot-vms-created-using-the-classic-deployment-model)建立的 VM 進行疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="daf88-129">You can also find steps on troubleshooting VMs created using the [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span></span>

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-the-azure-portal"></a><span data-ttu-id="daf88-130">使用 Azure 入口網站進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="daf88-130">Troubleshoot using the Azure portal</span></span>
<span data-ttu-id="daf88-131">在每個疑難排解步驟完成之後，請再次嘗試連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="daf88-132">如果仍然無法連線，請嘗試下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="daf88-132">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="daf88-133">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="daf88-133">**Reset your RDP connection**.</span></span> <span data-ttu-id="daf88-134">當遠端連線已停用或 Windows 防火牆規則封鎖 RDP 時，此疑難排解步驟可重設 RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="daf88-134">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="daf88-135">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-136">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-136">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-137">按一下 [重設密碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daf88-137">Click the **Reset password** button.</span></span> <span data-ttu-id="daf88-138">將 [模式] 設定為 [只重設組態]，然後按一下 [更新] 按鈕︰</span><span class="sxs-lookup"><span data-stu-id="daf88-138">Set the **Mode** to **Reset configuration only** and then click the **Update** button:</span></span>
   
    ![在 Azure 入口網站中重設 RDP 組態](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. <span data-ttu-id="daf88-140">**確認網路安全性群組規則**。</span><span class="sxs-lookup"><span data-stu-id="daf88-140">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="daf88-141">使用 [IP 流量驗證](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)來確認網路安全性群組中的規則是否會封鎖虛擬機器的輸入或輸出流量。</span><span class="sxs-lookup"><span data-stu-id="daf88-141">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a Network Security Group is blocking traffic to or from a virtual machine.</span></span> <span data-ttu-id="daf88-142">您也可以檢閱有效的安全性群組規則，以確保輸入「允許」NSG 規則存在並已針對 RDP 連接埠 (預設值 3389) 設定優先順序。</span><span class="sxs-lookup"><span data-stu-id="daf88-142">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="daf88-143">如需詳細資訊，請參閱[使用有效安全性規則對 VM 流量流程進行疑難排解](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。</span><span class="sxs-lookup"><span data-stu-id="daf88-143">For more information, see [Using Effective Security Rules to troubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

3. <span data-ttu-id="daf88-144">**檢閱 VM 開機診斷**。</span><span class="sxs-lookup"><span data-stu-id="daf88-144">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="daf88-145">此疑難排解步驟可檢閱 VM 主控台記錄檔，以判斷 VM 是否報告問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-145">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="daf88-146">並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="daf88-146">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="daf88-147">特定疑難排解步驟已超出本文的範圍，但可能指出會影響 RDP 連線的更廣問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-147">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="daf88-148">如需有關檢閱主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱 [VM 的開機診斷](boot-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="daf88-148">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](boot-diagnostics.md).</span></span>

4. <span data-ttu-id="daf88-149">**重設 VM 的 NIC**。</span><span class="sxs-lookup"><span data-stu-id="daf88-149">**Reset the NIC for the VM**.</span></span> <span data-ttu-id="daf88-150">如需詳細資訊，請參閱[如何重設 Azure Windows VM 的 NIC](reset-network-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="daf88-150">For more information, see [how to reset NIC for Azure Windows VM](reset-network-interface.md).</span></span>
5. <span data-ttu-id="daf88-151">**檢查 VM 資源健康狀態**。</span><span class="sxs-lookup"><span data-stu-id="daf88-151">**Check the VM Resource Health**.</span></span> <span data-ttu-id="daf88-152">此疑難排解步驟可確認 Azure 平台沒有任何可能影響 VM 連線的已知問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-152">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="daf88-153">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-153">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-154">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-154">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-155">按一下 [資源健康狀態] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daf88-155">Click the **Resource health** button.</span></span> <span data-ttu-id="daf88-156">狀況良好的 VM 會報告為 [可用]：</span><span class="sxs-lookup"><span data-stu-id="daf88-156">A healthy VM reports as being **Available**:</span></span>
   
    ![在 Azure 入口網站中檢查 VM 資源健康狀態](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. <span data-ttu-id="daf88-158">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="daf88-158">**Reset user credentials**.</span></span> <span data-ttu-id="daf88-159">當您不確定或忘了認證時，此疑難排解步驟可重設本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-159">This troubleshooting step resets the password on a local administrator account when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="daf88-160">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-160">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-161">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-161">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-162">按一下 [重設密碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daf88-162">Click the **Reset password** button.</span></span> <span data-ttu-id="daf88-163">確定 [模式] 已設為 [重設密碼]，然後輸入您的使用者名稱和新密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-163">Make sure the **Mode** is set to **Reset password** and then enter your username and a new password.</span></span> <span data-ttu-id="daf88-164">最後，按一下 [更新] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="daf88-164">Finally, click the **Update** button:</span></span>
   
    ![在 Azure 入口網站中重設使用者認證](./media/troubleshoot-rdp-connection/reset-password.png)
7. <span data-ttu-id="daf88-166">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="daf88-166">**Restart your VM**.</span></span> <span data-ttu-id="daf88-167">此疑難排解步驟可以修正 VM 本身具有的任何基礎問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-167">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="daf88-168">在 Azure 入口網站中選取您的 VM，按一下 [概觀] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="daf88-168">Select your VM in the Azure portal and click the **Overview** tab.</span></span> <span data-ttu-id="daf88-169">按一下 [重新啟動] 按鈕︰</span><span class="sxs-lookup"><span data-stu-id="daf88-169">Click the **Restart** button:</span></span>
   
    ![在 Azure 入口網站中重新啟動 VM](./media/troubleshoot-rdp-connection/restart-vm.png)
8. <span data-ttu-id="daf88-171">**重新部署您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="daf88-171">**Redeploy your VM**.</span></span> <span data-ttu-id="daf88-172">此疑難排解步驟可將您的 VM 重新部署至 Azure 內的另一部主機，以更正任何基礎平台或網路問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-172">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="daf88-173">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-173">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-174">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-174">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-175">按一下 [重新部署] 按鈕，然後再按一下 [重新部署]：</span><span class="sxs-lookup"><span data-stu-id="daf88-175">Click the **Redeploy** button, and then click **Redeploy**:</span></span>
   
    ![在 Azure 入口網站中重新部署 VM](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    <span data-ttu-id="daf88-177">此作業完成之後，會遺失暫時磁碟資料，並且會更新與 VM 相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="daf88-177">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with the VM are updated.</span></span>

<span data-ttu-id="daf88-178">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-178">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-using-azure-powershell"></a><span data-ttu-id="daf88-179">使用 Azure PowerShell 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="daf88-179">Troubleshoot using Azure PowerShell</span></span>
<span data-ttu-id="daf88-180">如果您尚未這樣做，請參閱 [安裝並設定最新的 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="daf88-180">If you haven't already, [install and configure the latest Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="daf88-181">下列範例使用 `myResourceGroup``myVM` 和 `myVMAccessExtension` 等變數。</span><span class="sxs-lookup"><span data-stu-id="daf88-181">The following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span></span> <span data-ttu-id="daf88-182">以您自己的值取代這些變數名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="daf88-182">Replace these variable names and locations with your own values.</span></span>

> [!NOTE]
> <span data-ttu-id="daf88-183">您可使用 [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell Cmdlet 重設使用者認證和 RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="daf88-183">You reset the user credentials and the RDP configuration by using the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="daf88-184">在下列範例中，`myVMAccessExtension` 是您指定為程序一部分的名稱。</span><span class="sxs-lookup"><span data-stu-id="daf88-184">In the following examples, `myVMAccessExtension` is a name that you specify as part of the process.</span></span> <span data-ttu-id="daf88-185">如果您先前使用了 VMAccessAgent，則可以使用 `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` 來檢查 VM 的屬性，以取得現有擴充功能的名稱。</span><span class="sxs-lookup"><span data-stu-id="daf88-185">If you have previously worked with the VMAccessAgent, you can get the name of the existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` to check the properties of the VM.</span></span> <span data-ttu-id="daf88-186">請查看輸出的 'Extensions' 區段底下來檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="daf88-186">To view the name, look under the 'Extensions' section of the output.</span></span>

<span data-ttu-id="daf88-187">在每個疑難排解步驟完成之後，請再次嘗試連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-187">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="daf88-188">如果仍然無法連線，請嘗試下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="daf88-188">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="daf88-189">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="daf88-189">**Reset your RDP connection**.</span></span> <span data-ttu-id="daf88-190">當遠端連線已停用或 Windows 防火牆規則封鎖 RDP 時，此疑難排解步驟可重設 RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="daf88-190">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="daf88-191">下列範例會在位於 `WestUS` 且名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM 上重設 RDP 連線：</span><span class="sxs-lookup"><span data-stu-id="daf88-191">The follow example resets the RDP connection on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. <span data-ttu-id="daf88-192">**確認網路安全性群組規則**。</span><span class="sxs-lookup"><span data-stu-id="daf88-192">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="daf88-193">此疑難排解步驟可確認您有可允許 RDP 流量的網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="daf88-193">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span></span> <span data-ttu-id="daf88-194">RDP 的預設連接埠是 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="daf88-194">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="daf88-195">當您建立您的 VM 時，可能不會自動建立可允許 RDP 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="daf88-195">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="daf88-196">首先，將網路安全性群組的所有組態資料指派給 `$rules` 變數。</span><span class="sxs-lookup"><span data-stu-id="daf88-196">First, assign all the configuration data for your Network Security Group to the `$rules` variable.</span></span> <span data-ttu-id="daf88-197">下列範例會在名為 `myResourceGroup` 的資源群組中取得名為 `myNetworkSecurityGroup` 的網路安全性群組相關資訊：</span><span class="sxs-lookup"><span data-stu-id="daf88-197">The following example obtains information about the Network Security Group named `myNetworkSecurityGroup` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    <span data-ttu-id="daf88-198">現在，檢視針對此網路安全性群組設定的規則。</span><span class="sxs-lookup"><span data-stu-id="daf88-198">Now, view the rules that are configured for this Network Security Group.</span></span> <span data-ttu-id="daf88-199">確認存在一個規則可允許 TCP 連接埠 3389 進行輸入連線，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="daf88-199">Verify that a rule exists to allow TCP port 3389 for inbound connections as follows:</span></span>
   
    ```powershell
    $rules.SecurityRules
    ```
   
    <span data-ttu-id="daf88-200">下列範例顯示可允許 RDP 流量的有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="daf88-200">The following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="daf88-201">您可以看到 `Protocol`、`DestinationPortRange`、`Access` 和 `Direction` 已正確設定︰</span><span class="sxs-lookup"><span data-stu-id="daf88-201">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span></span>
   
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
   
    <span data-ttu-id="daf88-202">如果您沒有可允許 RDP 流量的規則，請[建立網路安全性群組規則](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-202">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="daf88-203">允許 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="daf88-203">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="daf88-204">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="daf88-204">**Reset user credentials**.</span></span> <span data-ttu-id="daf88-205">當您不確定或忘了認證時，此疑難排解步驟可重設您指定之本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-205">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure of, or have forgotten, the credentials.</span></span>
   
    <span data-ttu-id="daf88-206">首先，藉由將認證指派給 `$cred` 變數，以指定使用者名稱和新密碼，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="daf88-206">First, specify the username and a new password by assigning credentials to the `$cred` variable as follows:</span></span>
   
    ```powershell
    $cred=Get-Credential
    ```
   
    <span data-ttu-id="daf88-207">現在，更新 VM 上的認證。</span><span class="sxs-lookup"><span data-stu-id="daf88-207">Now, update the credentials on your VM.</span></span> <span data-ttu-id="daf88-208">下列範例會在位於 `WestUS` 且名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM 上更新認證：</span><span class="sxs-lookup"><span data-stu-id="daf88-208">The following example updates the credentials on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. <span data-ttu-id="daf88-209">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="daf88-209">**Restart your VM**.</span></span> <span data-ttu-id="daf88-210">此疑難排解步驟可以修正 VM 本身具有的任何基礎問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-210">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="daf88-211">下列範例會重新啟動名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="daf88-211">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. <span data-ttu-id="daf88-212">**重新部署您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="daf88-212">**Redeploy your VM**.</span></span> <span data-ttu-id="daf88-213">此疑難排解步驟可將您的 VM 重新部署至 Azure 內的另一部主機，以更正任何基礎平台或網路問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-213">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="daf88-214">下列範例會重新部署位於 `WestUS` 且名為 `myResourceGroup` 的資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="daf88-214">The following example redeploys the VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

<span data-ttu-id="daf88-215">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-215">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-vms-created-using-the-classic-deployment-model"></a><span data-ttu-id="daf88-216">針對使用傳統部署模型建立的 VM 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="daf88-216">Troubleshoot VMs created using the Classic deployment model</span></span>
<span data-ttu-id="daf88-217">在每個疑難排解步驟完成之後，請嘗試重新連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-217">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="daf88-218">**重設您的 RDP 連線**。</span><span class="sxs-lookup"><span data-stu-id="daf88-218">**Reset your RDP connection**.</span></span> <span data-ttu-id="daf88-219">當遠端連線已停用或 Windows 防火牆規則封鎖 RDP 時，此疑難排解步驟可重設 RDP 組態。</span><span class="sxs-lookup"><span data-stu-id="daf88-219">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="daf88-220">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-220">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-221">按一下 [...更多] 按鈕，然後按一下 [重設遠端存取]：</span><span class="sxs-lookup"><span data-stu-id="daf88-221">Click the **...More** button, then click **Reset Remote Access**:</span></span>
   
    ![在 Azure 入口網站中重設 RDP 組態](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. <span data-ttu-id="daf88-223">**確認雲端服務端點**。</span><span class="sxs-lookup"><span data-stu-id="daf88-223">**Verify Cloud Services endpoints**.</span></span> <span data-ttu-id="daf88-224">此疑難排解步驟可確認您的雲端服務中有可允許 RDP 流量的端點。</span><span class="sxs-lookup"><span data-stu-id="daf88-224">This troubleshooting step verifies that you have endpoints in your Cloud Services to permit RDP traffic.</span></span> <span data-ttu-id="daf88-225">RDP 的預設連接埠是 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="daf88-225">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="daf88-226">當您建立您的 VM 時，可能不會自動建立可允許 RDP 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="daf88-226">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
   <span data-ttu-id="daf88-227">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-227">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-228">按一下 [端點] 按鈕，以檢視目前為您的 VM 設定的端點。</span><span class="sxs-lookup"><span data-stu-id="daf88-228">Click the **Endpoints** button to view the endpoints currently configured for your VM.</span></span> <span data-ttu-id="daf88-229">確認存在可允許 TCP 連接埠 3389 上 RDP 流量的端點。</span><span class="sxs-lookup"><span data-stu-id="daf88-229">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span></span>
   
   <span data-ttu-id="daf88-230">下列範例顯示可允許 RDP 流量的有效端點：</span><span class="sxs-lookup"><span data-stu-id="daf88-230">The following example shows valid endpoints that permit RDP traffic:</span></span>
   
   ![在 Azure 入口網站中確認雲端服務端點](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   <span data-ttu-id="daf88-232">如果您沒有可允許 RDP 流量的端點，請[建立雲端服務端點](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-232">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="daf88-233">允許使用 TCP 連接至私人連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="daf88-233">Allow TCP to private port 3389.</span></span>
3. <span data-ttu-id="daf88-234">**檢閱 VM 開機診斷**。</span><span class="sxs-lookup"><span data-stu-id="daf88-234">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="daf88-235">此疑難排解步驟可檢閱 VM 主控台記錄檔，以判斷 VM 是否報告問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-235">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="daf88-236">並非所有 VM 都已啟用開機診斷，所以此疑難排解步驟可能是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="daf88-236">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="daf88-237">特定疑難排解步驟已超出本文的範圍，但可能指出會影響 RDP 連線的更廣問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-237">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="daf88-238">如需有關檢閱主控台記錄檔和 VM 螢幕擷取畫面的詳細資訊，請參閱 [VM 的開機診斷](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="daf88-238">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="daf88-239">**檢查 VM 資源健康狀態**。</span><span class="sxs-lookup"><span data-stu-id="daf88-239">**Check the VM Resource Health**.</span></span> <span data-ttu-id="daf88-240">此疑難排解步驟可確認 Azure 平台沒有任何可能影響 VM 連線的已知問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-240">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="daf88-241">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-241">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-242">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-242">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-243">按一下 [資源健康狀態] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daf88-243">Click the **Resource Health** button.</span></span> <span data-ttu-id="daf88-244">狀況良好的 VM 會報告為 [可用]：</span><span class="sxs-lookup"><span data-stu-id="daf88-244">A healthy VM reports as being **Available**:</span></span>
   
    ![在 Azure 入口網站中檢查 VM 資源健康狀態](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. <span data-ttu-id="daf88-246">**重設使用者認證**。</span><span class="sxs-lookup"><span data-stu-id="daf88-246">**Reset user credentials**.</span></span> <span data-ttu-id="daf88-247">當您不確定或忘了認證時，此疑難排解步驟可重設您指定之本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-247">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="daf88-248">在 Azure 入口網站中選取您的 VM。</span><span class="sxs-lookup"><span data-stu-id="daf88-248">Select your VM in the Azure portal.</span></span> <span data-ttu-id="daf88-249">向下捲動至 [設定] 窗格中接近清單底部的 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="daf88-249">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="daf88-250">按一下 [重設密碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="daf88-250">Click the **Reset password** button.</span></span> <span data-ttu-id="daf88-251">輸入您的使用者名稱和新密碼。</span><span class="sxs-lookup"><span data-stu-id="daf88-251">Enter your username and a new password.</span></span> <span data-ttu-id="daf88-252">最後，按一下 [儲存] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="daf88-252">Finally, click the **Save** button:</span></span>
   
    ![在 Azure 入口網站中重設使用者認證](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. <span data-ttu-id="daf88-254">**重新啟動您的 VM**。</span><span class="sxs-lookup"><span data-stu-id="daf88-254">**Restart your VM**.</span></span> <span data-ttu-id="daf88-255">此疑難排解步驟可以修正 VM 本身具有的任何基礎問題。</span><span class="sxs-lookup"><span data-stu-id="daf88-255">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="daf88-256">在 Azure 入口網站中選取您的 VM，按一下 [概觀] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="daf88-256">Select your VM in the Azure portal and click the **Overview** tab.</span></span> <span data-ttu-id="daf88-257">按一下 [重新啟動] 按鈕︰</span><span class="sxs-lookup"><span data-stu-id="daf88-257">Click the **Restart** button:</span></span>
   
    ![在 Azure 入口網站中重新啟動 VM](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

<span data-ttu-id="daf88-259">如果您仍然遇到 RDP 問題，可以[開啟支援要求](https://azure.microsoft.com/support/options/)或閱讀[更詳細的 RDP 疑難排解概念和步驟](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-259">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-specific-rdp-errors"></a><span data-ttu-id="daf88-260">針對特定 RDP 錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="daf88-260">Troubleshoot specific RDP errors</span></span>
<span data-ttu-id="daf88-261">嘗試透過 RDP 連接到您的 VM 時，您可能會遇到特定的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="daf88-261">You may encounter a specific error message when trying to connect to your VM via RDP.</span></span> <span data-ttu-id="daf88-262">以下是最常見的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="daf88-262">The following are the most common error messages:</span></span>

* <span data-ttu-id="daf88-263">[遠端工作階段中斷，因為沒有提供授權的遠端桌面授權伺服器可以使用](troubleshoot-specific-rdp-errors.md#rdplicense)。</span><span class="sxs-lookup"><span data-stu-id="daf88-263">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span></span>
* <span data-ttu-id="daf88-264">[遠端桌面找不到電腦「名稱」](troubleshoot-specific-rdp-errors.md#rdpname)。</span><span class="sxs-lookup"><span data-stu-id="daf88-264">[Remote Desktop can't find the computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span></span>
* <span data-ttu-id="daf88-265">[發生驗證錯誤。無法連絡本機安全性授權](troubleshoot-specific-rdp-errors.md#rdpauth)。</span><span class="sxs-lookup"><span data-stu-id="daf88-265">[An authentication error has occurred. The Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span></span>
* <span data-ttu-id="daf88-266">[Windows 安全性錯誤：您的認證無法運作](troubleshoot-specific-rdp-errors.md#wincred)。</span><span class="sxs-lookup"><span data-stu-id="daf88-266">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span></span>
* <span data-ttu-id="daf88-267">[這部電腦無法連線到遠端電腦](troubleshoot-specific-rdp-errors.md#rdpconnect)。</span><span class="sxs-lookup"><span data-stu-id="daf88-267">[This computer can't connect to the remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="daf88-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="daf88-268">Additional resources</span></span>
<span data-ttu-id="daf88-269">如果這些錯誤皆未發生，而您仍然無法透過「遠端桌面」連接到 VM，請閱讀詳細的 [遠端桌面疑難排解指南](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-269">If none of these errors occurred and you still can't connect to the VM via Remote Desktop, read the detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="daf88-270">如需存取在 VM 上執行之應用程式的疑難排解步驟，請參閱[針對在 Azure VM 上執行之應用程式的存取進行疑難排解](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-270">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="daf88-271">如果您在 Azure 中使用安全殼層 (SSH) 連線到 Linux VM 時遇到問題，請參閱[針對 Azure 中對 Linux VM 的 SSH 連線進行疑難排解](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="daf88-271">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

