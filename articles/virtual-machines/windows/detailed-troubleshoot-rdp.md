---
title: "在 Azure 中疑難排解 aaaDetailed 遠端桌面 |Microsoft 文件"
description: "檢閱您不能在 Azure 中的 tooa Windows 虛擬機器的遠端桌面錯誤的詳細疑難排解步驟"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "無法連接 tooremote 桌面，疑難排解遠端桌面，遠端桌面無法連線，遠端桌面的錯誤、 遠端桌面疑難排解、 遠端桌面問題"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a><span data-ttu-id="efa62-104">遠端桌面連線的詳細疑難排解步驟發出 tooWindows Azure 中的 Vm</span><span class="sxs-lookup"><span data-stu-id="efa62-104">Detailed troubleshooting steps for remote desktop connection issues tooWindows VMs in Azure</span></span>
<span data-ttu-id="efa62-105">本文章提供詳細的疑難排解步驟 toodiagnose 及修正複雜的遠端桌面錯誤為 windows Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="efa62-105">This article provides detailed troubleshooting steps toodiagnose and fix complex Remote Desktop errors for Windows-based Azure virtual machines.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efa62-106">tooeliminate hello 更常見的遠端桌面錯誤，請確定 tooread [hello 基本的疑難排解文章遠端桌面](troubleshoot-rdp-connection.md)後再繼續。</span><span class="sxs-lookup"><span data-stu-id="efa62-106">tooeliminate hello more common Remote Desktop errors, make sure tooread [hello basic troubleshooting article for Remote Desktop](troubleshoot-rdp-connection.md) before proceeding.</span></span>

<span data-ttu-id="efa62-107">您可能會遇到不相似 hello 特定錯誤訊息的錯誤訊息中涵蓋的遠端桌面[hello 疑難排解指南的基本遠端桌面](troubleshoot-rdp-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="efa62-107">You may encounter a Remote Desktop error message that does not resemble any of hello specific error messages covered in [hello basic Remote Desktop troubleshooting guide](troubleshoot-rdp-connection.md).</span></span> <span data-ttu-id="efa62-108">請遵循這些步驟 toodetermine，hello 遠端桌面 (RDP) 用戶端為何無法 tooconnect toohello RDP 服務 hello Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="efa62-108">Follow these steps toodetermine why hello Remote Desktop (RDP) client is unable tooconnect toohello RDP service on hello Azure VM.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="efa62-109">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="efa62-109">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="efa62-110">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="efa62-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="efa62-111">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)按一下**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="efa62-111">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span> <span data-ttu-id="efa62-112">使用 Azure 支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="efa62-112">For information about using Azure Support, read hello [Microsoft Azure Support FAQ](https://azure.microsoft.com/support/faq/).</span></span>

## <a name="components-of-a-remote-desktop-connection"></a><span data-ttu-id="efa62-113">遠端桌面連線的元件</span><span class="sxs-lookup"><span data-stu-id="efa62-113">Components of a Remote Desktop connection</span></span>
<span data-ttu-id="efa62-114">RDP 連線涉及 hello 下列元件：</span><span class="sxs-lookup"><span data-stu-id="efa62-114">hello following components are involved in an RDP connection:</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

<span data-ttu-id="efa62-115">繼續之前，它可能有助於 toomentally 檢閱 hello 最後一個成功遠端桌面連線 toohello VM 以來的變更。</span><span class="sxs-lookup"><span data-stu-id="efa62-115">Before proceeding, it might help toomentally review what has changed since hello last successful Remote Desktop connection toohello VM.</span></span> <span data-ttu-id="efa62-116">例如：</span><span class="sxs-lookup"><span data-stu-id="efa62-116">For example:</span></span>

* <span data-ttu-id="efa62-117">hello hello VM 或 hello 雲端服務包含 hello VM 的公用 IP 位址 (也稱為虛擬 IP 位址 hello [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) 已變更。</span><span class="sxs-lookup"><span data-stu-id="efa62-117">hello public IP address of hello VM or hello cloud service containing hello VM (also called hello virtual IP address [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) has changed.</span></span> <span data-ttu-id="efa62-118">hello RDP 失敗可能是因為您的 DNS 用戶端快取仍然具有 hello*舊的 IP 位址*hello DNS 名稱登錄。</span><span class="sxs-lookup"><span data-stu-id="efa62-118">hello RDP failure could be because your DNS client cache still has hello *old IP address* registered for hello DNS name.</span></span> <span data-ttu-id="efa62-119">排清您的 DNS 用戶端快取，然後再試一次連接 hello VM。</span><span class="sxs-lookup"><span data-stu-id="efa62-119">Flush your DNS client cache and try connecting hello VM again.</span></span> <span data-ttu-id="efa62-120">或嘗試使用 hello 新 VIP 直接連接。</span><span class="sxs-lookup"><span data-stu-id="efa62-120">Or try connecting directly with hello new VIP.</span></span>
* <span data-ttu-id="efa62-121">您正在使用協力廠商應用程式 toomanage 遠端桌面連線，而不使用 hello hello Azure 入口網站所產生的連線。</span><span class="sxs-lookup"><span data-stu-id="efa62-121">You are using a third-party application toomanage your Remote Desktop connections instead of using hello connection generated by hello Azure portal.</span></span> <span data-ttu-id="efa62-122">請確認該 hello 應用程式組態包含 hello 正確 TCP 通訊埠 hello 遠端桌面流量。</span><span class="sxs-lookup"><span data-stu-id="efa62-122">Verify that hello application configuration includes hello correct TCP port for hello Remote Desktop traffic.</span></span> <span data-ttu-id="efa62-123">您可以檢查這個連接埠為傳統的虛擬機器在 hello [Azure 入口網站](https://portal.azure.com)，依序按一下 hello VM 的設定 > 端點。</span><span class="sxs-lookup"><span data-stu-id="efa62-123">You can check this port for a classic virtual machine in hello [Azure portal](https://portal.azure.com), by clicking hello VM's Settings > Endpoints.</span></span>

## <a name="preliminary-steps"></a><span data-ttu-id="efa62-124">預備步驟</span><span class="sxs-lookup"><span data-stu-id="efa62-124">Preliminary steps</span></span>
<span data-ttu-id="efa62-125">繼續之前 toohello 詳細的疑難排解，</span><span class="sxs-lookup"><span data-stu-id="efa62-125">Before proceeding toohello detailed troubleshooting,</span></span>

* <span data-ttu-id="efa62-126">檢查 hello hello hello Azure 入口網站有任何明顯的問題中的虛擬機器狀態。</span><span class="sxs-lookup"><span data-stu-id="efa62-126">Check hello status of hello virtual machine in hello Azure portal for any obvious issues.</span></span>
* <span data-ttu-id="efa62-127">請遵循 hello[快速修正常見 RDP 錯誤 hello 基本疑難排解步驟引導](troubleshoot-rdp-connection.md#quick-troubleshooting-steps)。</span><span class="sxs-lookup"><span data-stu-id="efa62-127">Follow hello [quick fix steps for common RDP errors in hello basic troubleshooting guide](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).</span></span>

<span data-ttu-id="efa62-128">嘗試完成這些步驟之後重新連接 toohello 透過遠端桌面的 VM。</span><span class="sxs-lookup"><span data-stu-id="efa62-128">Try reconnecting toohello VM via Remote Desktop after these steps.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="efa62-129">詳細的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="efa62-129">Detailed troubleshooting steps</span></span>
<span data-ttu-id="efa62-130">hello 遠端桌面用戶端可能無法 hello Azure VM 上的無法 tooreach hello 遠端桌面服務到期 tooissues 在 hello 下列來源：</span><span class="sxs-lookup"><span data-stu-id="efa62-130">hello Remote Desktop client may not be able tooreach hello Remote Desktop service on hello Azure VM due tooissues at hello following sources:</span></span>

* [<span data-ttu-id="efa62-131">遠端桌面用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="efa62-131">Remote Desktop client computer</span></span>](#source-1-remote-desktop-client-computer)
* [<span data-ttu-id="efa62-132">組織內部網路的邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="efa62-132">Organization intranet edge device</span></span>](#source-2-organization-intranet-edge-device)
* [<span data-ttu-id="efa62-133">雲端服務端點和存取控制清單 (ACL)</span><span class="sxs-lookup"><span data-stu-id="efa62-133">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="efa62-134">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="efa62-134">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="efa62-135">以 Windows 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="efa62-135">Windows-based Azure VM</span></span>](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a><span data-ttu-id="efa62-136">來源 1：遠端桌面用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="efa62-136">Source 1: Remote Desktop client computer</span></span>
<span data-ttu-id="efa62-137">請確認您的電腦，可以進行遠端桌面連線 tooanother 內部，Windows 型電腦。</span><span class="sxs-lookup"><span data-stu-id="efa62-137">Verify that your computer can make Remote Desktop connections tooanother on-premises, Windows-based computer.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

<span data-ttu-id="efa62-138">如果您無法檢查下列設定，在您的電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="efa62-138">If you cannot, check for hello following settings on your computer:</span></span>

* <span data-ttu-id="efa62-139">目前封鎖「遠端桌面」流量的本機防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="efa62-139">A local firewall setting that is blocking Remote Desktop traffic.</span></span>
* <span data-ttu-id="efa62-140">目前阻止「遠端桌面」連線的本機安裝用戶端 Proxy 軟體。</span><span class="sxs-lookup"><span data-stu-id="efa62-140">Locally installed client proxy software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="efa62-141">目前阻止「遠端桌面」連線的本機安裝網路監視軟體。</span><span class="sxs-lookup"><span data-stu-id="efa62-141">Locally installed network monitoring software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="efa62-142">目前阻止「遠端桌面」連線的其他類型安全性軟體，這些軟體會監視流量或允許/不允許特定類型的流量。</span><span class="sxs-lookup"><span data-stu-id="efa62-142">Other types of security software that either monitor traffic or allow/disallow specific types of traffic that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="efa62-143">在這些情況下，請暫時停用 hello 軟體，然後再試一次 tooconnect tooan 在內部部署電腦上透過遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="efa62-143">In all these cases, temporarily disable hello software and try tooconnect tooan on-premises computer via Remote Desktop.</span></span> <span data-ttu-id="efa62-144">如此一來，您可以找出 hello 實際原因中，如果使用您的網路系統管理員 toocorrect hello 軟體設定 tooallow 遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="efa62-144">If you can find out hello actual cause this way, work with your network administrator toocorrect hello software settings tooallow Remote Desktop connections.</span></span>

## <a name="source-2-organization-intranet-edge-device"></a><span data-ttu-id="efa62-145">來源 2：組織內部網路的邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="efa62-145">Source 2: Organization intranet edge device</span></span>
<span data-ttu-id="efa62-146">請確認電腦直接連線的 toohello 網際網路可讓遠端桌面連線 tooyour Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="efa62-146">Verify that a computer directly connected toohello Internet can make Remote Desktop connections tooyour Azure virtual machine.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

<span data-ttu-id="efa62-147">如果您沒有直接連接的 toohello 網際網路的電腦，建立並使用新的 Azure 虛擬機器資源群組或雲端服務中進行測試。</span><span class="sxs-lookup"><span data-stu-id="efa62-147">If you do not have a computer that is directly connected toohello Internet, create and test with a new Azure virtual machine in a resource group or cloud service.</span></span> <span data-ttu-id="efa62-148">如需詳細資訊，請參閱 [在 Azure 中建立執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="efa62-148">For more information, see [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="efa62-149">Hello 測試之後，您可以刪除 hello 虛擬機器和 hello 資源群組或 hello 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="efa62-149">You can delete hello virtual machine and hello resource group or hello cloud service, after hello test.</span></span>

<span data-ttu-id="efa62-150">如果您可以建立與電腦的遠端桌面連接直接連接 toohello 網際網路，請檢查您的組織內部網路的邊緣裝置進行：</span><span class="sxs-lookup"><span data-stu-id="efa62-150">If you can create a Remote Desktop connection with a computer directly attached toohello Internet, check your organization intranet edge device for:</span></span>

* <span data-ttu-id="efa62-151">內部防火牆封鎖 HTTPS 連線 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="efa62-151">An internal firewall blocking HTTPS connections toohello Internet.</span></span>
* <span data-ttu-id="efa62-152">目前阻止「遠端桌面」連線的 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="efa62-152">A proxy server preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="efa62-153">目前在邊緣網路中的裝置上執行且阻止「遠端桌面」連線的入侵偵測或網路監視軟體。</span><span class="sxs-lookup"><span data-stu-id="efa62-153">Intrusion detection or network monitoring software running on devices in your edge network that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="efa62-154">使用您組織內部網路邊緣裝置 tooallow HTTPS 為基礎的遠端桌面連線 toohello 網際網路的網路系統管理員 toocorrect hello 設定。</span><span class="sxs-lookup"><span data-stu-id="efa62-154">Work with your network administrator toocorrect hello settings of your organization intranet edge device tooallow HTTPS-based Remote Desktop connections toohello Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="efa62-155">來源 3：雲端服務端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="efa62-155">Source 3: Cloud service endpoint and ACL</span></span>
<span data-ttu-id="efa62-156">進行建立的 Vm 使用 hello 傳統部署模型，請確認您的是另一個 Azure VM 中 hello 相同雲端服務或虛擬網路可讓遠端桌面連線 tooyour Azure VM。</span><span class="sxs-lookup"><span data-stu-id="efa62-156">For VMs created using hello Classic deployment model, verify that another Azure VM that is in hello same cloud service or virtual network can make Remote Desktop connections tooyour Azure VM.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> <span data-ttu-id="efa62-157">建立資源管理員 中的虛擬機器，請跳過[來源 4： 網路安全性群組](#source-4-network-security-groups)。</span><span class="sxs-lookup"><span data-stu-id="efa62-157">For virtual machines created in Resource Manager, skip too[Source 4: Network Security Groups](#source-4-network-security-groups).</span></span>

<span data-ttu-id="efa62-158">如果您沒有另一個虛擬機器在 hello 相同雲端服務或虛擬網路，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="efa62-158">If you do not have another virtual machine in hello same cloud service or virtual network, create one.</span></span> <span data-ttu-id="efa62-159">中的 hello 步驟[建立在 Azure 中執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="efa62-159">Follow hello steps in [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="efa62-160">Hello 測試完成後，請刪除 hello 測試虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="efa62-160">Delete hello test virtual machine after hello test is completed.</span></span>

<span data-ttu-id="efa62-161">如果您可以透過遠端桌面中的 hello tooa 虛擬主機連接相同雲端服務或虛擬網路中，檢查這些設定：</span><span class="sxs-lookup"><span data-stu-id="efa62-161">If you can connect via Remote Desktop tooa virtual machine in hello same cloud service or virtual network, check for these settings:</span></span>

* <span data-ttu-id="efa62-162">hello hello 目標 VM 上的遠端桌面流量的端點組態： hello 私人 TCP 連接埠的 hello 端點必須符合 hello 的 hello VM 的遠端桌面服務所接聽的 TCP 連接埠 （預設值為 3389）。</span><span class="sxs-lookup"><span data-stu-id="efa62-162">hello endpoint configuration for Remote Desktop traffic on hello target VM: hello private TCP port of hello endpoint must match hello TCP port on which hello VM's Remote Desktop service is listening (default is 3389).</span></span>
* <span data-ttu-id="efa62-163">hello 遠端桌面流量端點 hello 目標 VM 上的 ACL hello: Acl 可讓您 toospecify 允許或拒絕連入流量從 hello 網際網路根據來源 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="efa62-163">hello ACL for hello Remote Desktop traffic endpoint on hello target VM: ACLs allow you toospecify allowed or denied incoming traffic from hello Internet based on its source IP address.</span></span> <span data-ttu-id="efa62-164">設定不正確的 Acl 可以防止內送的遠端桌面流量 toohello 端點。</span><span class="sxs-lookup"><span data-stu-id="efa62-164">Misconfigured ACLs can prevent incoming Remote Desktop traffic toohello endpoint.</span></span> <span data-ttu-id="efa62-165">請檢查您在允許的公用 IP 位址的 proxy 或其他的邊緣伺服器連入流量的 Acl tooensure。</span><span class="sxs-lookup"><span data-stu-id="efa62-165">Check your ACLs tooensure that incoming traffic from your public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="efa62-166">如需詳細資訊，請參閱 [什麼是網路存取控制清單 (ACL)？](../../virtual-network/virtual-networks-acl.md)</span><span class="sxs-lookup"><span data-stu-id="efa62-166">For more information, see [What is a Network Access Control List (ACL)?](../../virtual-network/virtual-networks-acl.md)</span></span>

<span data-ttu-id="efa62-167">toocheck hello 端點是否 hello 問題的來源 hello，移除 hello 目前端點，以及建立新的連線，選擇隨機連接埠在 hello 範圍 49152 – 65535 hello 外部連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="efa62-167">toocheck if hello endpoint is hello source of hello problem, remove hello current endpoint and create a new one, choosing a random port in hello range 49152–65535 for hello external port number.</span></span> <span data-ttu-id="efa62-168">如需詳細資訊，請參閱[如何端點 tooa 虛擬機器 tooset](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="efa62-168">For more information, see [How tooset up endpoints tooa virtual machine](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="efa62-169">來源 4：網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="efa62-169">Source 4: Network Security Groups</span></span>
<span data-ttu-id="efa62-170">網路安全性群組能夠更精確地控制受允許的輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="efa62-170">Network Security Groups allow more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="efa62-171">您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。</span><span class="sxs-lookup"><span data-stu-id="efa62-171">You can create rules spanning subnets and cloud services in an Azure virtual network.</span></span>

<span data-ttu-id="efa62-172">使用[IP 流量確認](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)tooconfirm 如果網路安全性群組中的規則會封鎖從虛擬機器的流量 tooor。</span><span class="sxs-lookup"><span data-stu-id="efa62-172">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm if a rule in a Network Security Group is blocking traffic tooor from a virtual machine.</span></span> <span data-ttu-id="efa62-173">您也可以檢閱有效安全性群組規則 tooensure 輸入 「 允許 」 NSG 規則存在，而且已設定優先權的 RDP 連接埠 （預設值為 3389）。</span><span class="sxs-lookup"><span data-stu-id="efa62-173">You can also review effective security group rules tooensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="efa62-174">如需詳細資訊，請參閱[使用有效的安全性規則 tootroubleshoot VM 流量流程](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。</span><span class="sxs-lookup"><span data-stu-id="efa62-174">For more information, see [Using Effective Security Rules tootroubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

## <a name="source-5-windows-based-azure-vm"></a><span data-ttu-id="efa62-175">來源 5：以 Windows 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="efa62-175">Source 5: Windows-based Azure VM</span></span>
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

<span data-ttu-id="efa62-176">請依照下列中的 hello 指示[本文](reset-rdp.md)。</span><span class="sxs-lookup"><span data-stu-id="efa62-176">Follow hello instructions in [this article](reset-rdp.md).</span></span> <span data-ttu-id="efa62-177">這篇文章會重設 hello hello 虛擬機器上的遠端桌面服務：</span><span class="sxs-lookup"><span data-stu-id="efa62-177">This article resets hello Remote Desktop service on hello virtual machine:</span></span>

* <span data-ttu-id="efa62-178">啟用 hello 「 遠端桌面 」 Windows 防火牆預設規則 （TCP 連接埠 3389）。</span><span class="sxs-lookup"><span data-stu-id="efa62-178">Enable hello "Remote Desktop" Windows Firewall default rule (TCP port 3389).</span></span>
* <span data-ttu-id="efa62-179">藉由設定 hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections 登錄值 too0 啟用遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="efa62-179">Enable Remote Desktop connections by setting hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections registry value too0.</span></span>

<span data-ttu-id="efa62-180">請嘗試 hello 連線從您的電腦一次。</span><span class="sxs-lookup"><span data-stu-id="efa62-180">Try hello connection from your computer again.</span></span> <span data-ttu-id="efa62-181">如果您仍然無法 tooconnect 透過遠端桌面，請檢查下列可能的問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="efa62-181">If you are still not able tooconnect via Remote Desktop, check for hello following possible problems:</span></span>

* <span data-ttu-id="efa62-182">hello 遠端桌面服務未在 hello 目標 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="efa62-182">hello Remote Desktop service is not running on hello target VM.</span></span>
* <span data-ttu-id="efa62-183">hello 遠端桌面服務不會接聽 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="efa62-183">hello Remote Desktop service is not listening on TCP port 3389.</span></span>
* <span data-ttu-id="efa62-184">Windows 防火牆或另一個本機防火牆有阻止遠端桌面流量的輸出規則。</span><span class="sxs-lookup"><span data-stu-id="efa62-184">Windows Firewall or another local firewall has an outbound rule that is preventing Remote Desktop traffic.</span></span>
* <span data-ttu-id="efa62-185">入侵偵測或網路監視 hello Azure 虛擬機器上執行的軟體防止遠端桌面連接。</span><span class="sxs-lookup"><span data-stu-id="efa62-185">Intrusion detection or network monitoring software running on hello Azure virtual machine is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="efa62-186">對於使用 hello 傳統部署模型所建立的 Vm，您可以使用遠端的 Azure PowerShell 工作階段 toohello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="efa62-186">For VMs created using hello classic deployment model, you can use a remote Azure PowerShell session toohello Azure virtual machine.</span></span> <span data-ttu-id="efa62-187">首先，您需要 tooinstall 憑證 hello 虛擬機器的主機的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="efa62-187">First, you need tooinstall a certificate for hello virtual machine's hosting cloud service.</span></span> <span data-ttu-id="efa62-188">跳過[設定安全的遠端 PowerShell 存取 tooAzure 虛擬機器](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe)並下載 hello **InstallWinRMCertAzureVM.ps1**指令碼檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="efa62-188">Go too[Configure Secure Remote PowerShell Access tooAzure Virtual Machines](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) and download hello **InstallWinRMCertAzureVM.ps1** script file tooyour local computer.</span></span>

<span data-ttu-id="efa62-189">接下來，如果尚未安裝 Azure PowerShell，則請先安裝。</span><span class="sxs-lookup"><span data-stu-id="efa62-189">Next, install Azure PowerShell if you haven't already.</span></span> <span data-ttu-id="efa62-190">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="efa62-190">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="efa62-191">接下來，開啟 Azure PowerShell 命令提示字元並變更 hello 資料夾 toohello 的目前位置 hello **InstallWinRMCertAzureVM.ps1**指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="efa62-191">Next, open an Azure PowerShell command prompt and change hello current folder toohello location of hello **InstallWinRMCertAzureVM.ps1** script file.</span></span> <span data-ttu-id="efa62-192">toorun Azure PowerShell 指令碼，您必須設定 hello 正確的執行原則。</span><span class="sxs-lookup"><span data-stu-id="efa62-192">toorun an Azure PowerShell script, you must set hello correct execution policy.</span></span> <span data-ttu-id="efa62-193">執行 hello **Get-executionpolicy**命令 toodetermine 目前的原則層級。</span><span class="sxs-lookup"><span data-stu-id="efa62-193">Run hello **Get-ExecutionPolicy** command toodetermine your current policy level.</span></span> <span data-ttu-id="efa62-194">如需設定 hello 適當層級的資訊，請參閱[Set-executionpolicy](https://technet.microsoft.com/library/hh849812.aspx)。</span><span class="sxs-lookup"><span data-stu-id="efa62-194">For information about setting hello appropriate level, see [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).</span></span>

<span data-ttu-id="efa62-195">接下來，填寫您的 Azure 訂用帳戶名稱、 hello 雲端服務名稱和 （移除 hello < 和 > 字元） 的虛擬機器名稱，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="efa62-195">Next, fill in your Azure subscription name, hello cloud service name, and your virtual machine name (removing hello < and > characters), and then run these commands.</span></span>

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

<span data-ttu-id="efa62-196">您可以從 hello 取得 hello 正確的訂用帳戶名稱*訂用帳戶名稱*屬性 hello 顯示 hello **Get-azuresubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="efa62-196">You can get hello correct subscription name from hello *SubscriptionName* property of hello display of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="efa62-197">您可以從 hello 取得 hello hello 虛擬機器的雲端服務名稱*ServiceName*資料行中的 hello hello 顯示**Get-azurevm**命令。</span><span class="sxs-lookup"><span data-stu-id="efa62-197">You can get hello cloud service name for hello virtual machine from hello *ServiceName* column in hello display of hello **Get-AzureVM** command.</span></span>

<span data-ttu-id="efa62-198">檢查是否有 hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="efa62-198">Check if you have hello new certificate.</span></span> <span data-ttu-id="efa62-199">開啟 hello 目前使用者憑證 嵌入式管理單元，然後查看 hello**受信任的根 Certification Authorities\Certificates**資料夾。</span><span class="sxs-lookup"><span data-stu-id="efa62-199">Open a Certificates snap-in for hello current user and look in hello **Trusted Root Certification Authorities\Certificates** folder.</span></span> <span data-ttu-id="efa62-200">您應該會看到您的雲端服務中發行 toocolumn hello hello DNS 名稱的憑證 (範例： cloudservice4testing.cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="efa62-200">You should see a certificate with hello DNS name of your cloud service in hello Issued toocolumn (example: cloudservice4testing.cloudapp.net).</span></span>

<span data-ttu-id="efa62-201">接下來，使用這些命令起始遠端 Azure PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="efa62-201">Next, initiate a remote Azure PowerShell session by using these commands.</span></span>

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

<span data-ttu-id="efa62-202">輸入有效的系統管理員認證之後, 您應該會看到類似 toohello 下列 Azure PowerShell 命令提示字元：</span><span class="sxs-lookup"><span data-stu-id="efa62-202">After entering valid administrator credentials, you should see something similar toohello following Azure PowerShell prompt:</span></span>

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

<span data-ttu-id="efa62-203">此提示 hello 第一個部分是您的雲端服務名稱，其中包含可能是不同於 「 cloudservice4testing.cloudapp.net"hello 目標 VM。</span><span class="sxs-lookup"><span data-stu-id="efa62-203">hello first part of this prompt is your cloud service name that contains hello target VM, which could be different from "cloudservice4testing.cloudapp.net".</span></span> <span data-ttu-id="efa62-204">您現在可以發出 Azure PowerShell 命令，此雲端服務 tooinvestigate hello 問題所述，並更正 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="efa62-204">You can now issue Azure PowerShell commands for this cloud service tooinvestigate hello problems mentioned and correct hello configuration.</span></span>

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a><span data-ttu-id="efa62-205">toomanually 正確 hello 遠端桌面服務接聽的 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="efa62-205">toomanually correct hello Remote Desktop Services listening TCP port</span></span>
<span data-ttu-id="efa62-206">Hello 遠端 Azure PowerShell 工作階段命令提示字元，執行此命令。</span><span class="sxs-lookup"><span data-stu-id="efa62-206">At hello remote Azure PowerShell session prompt, run this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="efa62-207">hello PortNumber 屬性顯示 hello 目前的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="efa62-207">hello PortNumber property shows hello current port number.</span></span> <span data-ttu-id="efa62-208">如有需要請使用此命令變更 hello 遠端桌面連接埠號碼後 tooits 預設值 (為 3389)。</span><span class="sxs-lookup"><span data-stu-id="efa62-208">If needed, change hello Remote Desktop port number back tooits default value (3389) by using this command.</span></span>

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

<span data-ttu-id="efa62-209">確認 hello 連接埠已變更的 too3389 使用這個命令。</span><span class="sxs-lookup"><span data-stu-id="efa62-209">Verify that hello port has been changed too3389 by using this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="efa62-210">使用這個命令來結束 hello 遠端的 Azure PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="efa62-210">Exit hello remote Azure PowerShell session by using this command.</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="efa62-211">請確認該 hello hello Azure VM 的遠端桌面端點也使用 TCP 連接埠 3398 做為其內部的連接埠。</span><span class="sxs-lookup"><span data-stu-id="efa62-211">Verify that hello Remote Desktop endpoint for hello Azure VM is also using TCP port 3398 as its internal port.</span></span> <span data-ttu-id="efa62-212">重新啟動 hello Azure VM，然後再試一次 hello 遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="efa62-212">Restart hello Azure VM and try hello Remote Desktop connection again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efa62-213">其他資源</span><span class="sxs-lookup"><span data-stu-id="efa62-213">Additional resources</span></span>
[<span data-ttu-id="efa62-214">如何 tooreset 密碼或 hello 遠端桌面服務的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="efa62-214">How tooreset a password or hello Remote Desktop service for Windows virtual machines</span></span>](reset-rdp.md)

[<span data-ttu-id="efa62-215">如何 tooinstall 和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="efa62-215">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

[<span data-ttu-id="efa62-216">疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="efa62-216">Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine</span></span>](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="efa62-217">疑難排解 Azure 虛擬機器上執行的存取 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="efa62-217">Troubleshoot access tooan application running on an Azure virtual machine</span></span>](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

