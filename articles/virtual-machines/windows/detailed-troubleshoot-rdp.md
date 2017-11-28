---
title: "在 Azure 中遠端桌面的詳細疑難排解 | Microsoft Docs"
description: "針對您無法透過遠端桌面連線到 Azure 中 Windows 虛擬機器的錯誤，檢閱詳細的疑難排解步驟"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "無法連線到遠端桌面, 疑難排解遠端桌面, 遠端桌面無法連線, 遠端桌面錯誤, 遠端桌面疑難排解, 遠端桌面問題"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: 22080b9402b13fd8162024db10aef5475880e4a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-to-windows-vms-in-azure"></a><span data-ttu-id="869e5-104">Azure 中 Windows VM 之遠端桌面連線問題的詳細疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="869e5-104">Detailed troubleshooting steps for remote desktop connection issues to Windows VMs in Azure</span></span>
<span data-ttu-id="869e5-105">本文章提供診斷和修正複雜的以 Windows 為基礎的 Azure 虛擬機器的遠端桌面錯誤的詳細疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="869e5-105">This article provides detailed troubleshooting steps to diagnose and fix complex Remote Desktop errors for Windows-based Azure virtual machines.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="869e5-106">若要消除較常見的「遠端桌面」錯誤，請務必先閱讀 [遠端桌面的基本疑難排解文章](troubleshoot-rdp-connection.md)，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="869e5-106">To eliminate the more common Remote Desktop errors, make sure to read [the basic troubleshooting article for Remote Desktop](troubleshoot-rdp-connection.md) before proceeding.</span></span>

<span data-ttu-id="869e5-107">您可能會遇到不像 [基本遠端桌面疑難排解指南](troubleshoot-rdp-connection.md)所涵蓋之任何特定錯誤訊息的「遠端桌面」錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="869e5-107">You may encounter a Remote Desktop error message that does not resemble any of the specific error messages covered in [the basic Remote Desktop troubleshooting guide](troubleshoot-rdp-connection.md).</span></span> <span data-ttu-id="869e5-108">請依照下列步驟來判斷「遠端桌面」(RDP) 用戶端為何無法連線至 Azure VM 上的 RDP 服務。</span><span class="sxs-lookup"><span data-stu-id="869e5-108">Follow these steps to determine why the Remote Desktop (RDP) client is unable to connect to the RDP service on the Azure VM.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="869e5-109">如果在本文章中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="869e5-109">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="869e5-110">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="869e5-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="869e5-111">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後按一下 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="869e5-111">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span> <span data-ttu-id="869e5-112">如需關於使用 Azure 支援的資訊，請參閱 [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/support/faq/)。</span><span class="sxs-lookup"><span data-stu-id="869e5-112">For information about using Azure Support, read the [Microsoft Azure Support FAQ](https://azure.microsoft.com/support/faq/).</span></span>

## <a name="components-of-a-remote-desktop-connection"></a><span data-ttu-id="869e5-113">遠端桌面連線的元件</span><span class="sxs-lookup"><span data-stu-id="869e5-113">Components of a Remote Desktop connection</span></span>
<span data-ttu-id="869e5-114">以下是 RDP 連線相關的元件：</span><span class="sxs-lookup"><span data-stu-id="869e5-114">The following components are involved in an RDP connection:</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

<span data-ttu-id="869e5-115">在繼續之前，在心裡檢閱最後一個成功的遠端桌面連線至 VM 以來的變更可能有幫助。</span><span class="sxs-lookup"><span data-stu-id="869e5-115">Before proceeding, it might help to mentally review what has changed since the last successful Remote Desktop connection to the VM.</span></span> <span data-ttu-id="869e5-116">例如：</span><span class="sxs-lookup"><span data-stu-id="869e5-116">For example:</span></span>

* <span data-ttu-id="869e5-117">VM 或包含 VM 之雲端服務的公用 IP 位址 (也稱為虛擬 IP 位址 [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) 已變更。</span><span class="sxs-lookup"><span data-stu-id="869e5-117">The public IP address of the VM or the cloud service containing the VM (also called the virtual IP address [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) has changed.</span></span> <span data-ttu-id="869e5-118">RDP 失敗的原因可能是 DNS 用戶端快取仍然有針對該 DNS 名稱註冊的「舊 IP 位址」  。</span><span class="sxs-lookup"><span data-stu-id="869e5-118">The RDP failure could be because your DNS client cache still has the *old IP address* registered for the DNS name.</span></span> <span data-ttu-id="869e5-119">請清除 DNS 用戶端快取並嘗試再次連接 VM。</span><span class="sxs-lookup"><span data-stu-id="869e5-119">Flush your DNS client cache and try connecting the VM again.</span></span> <span data-ttu-id="869e5-120">或嘗試直接與新的 VIP 連接。</span><span class="sxs-lookup"><span data-stu-id="869e5-120">Or try connecting directly with the new VIP.</span></span>
* <span data-ttu-id="869e5-121">您使用協力廠商應用程式來管理「遠端桌面」連線，而不是使用 Azure 入口網站所產生的連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-121">You are using a third-party application to manage your Remote Desktop connections instead of using the connection generated by the Azure portal.</span></span> <span data-ttu-id="869e5-122">請確認應用程式組態包含正確的「遠端桌面」流量 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="869e5-122">Verify that the application configuration includes the correct TCP port for the Remote Desktop traffic.</span></span> <span data-ttu-id="869e5-123">您可以在 [Azure 入口網站](https://portal.azure.com)中查看傳統虛擬機器的這個連接埠，方法是按一下該 VM 的 [設定] > [端點]。</span><span class="sxs-lookup"><span data-stu-id="869e5-123">You can check this port for a classic virtual machine in the [Azure portal](https://portal.azure.com), by clicking the VM's Settings > Endpoints.</span></span>

## <a name="preliminary-steps"></a><span data-ttu-id="869e5-124">預備步驟</span><span class="sxs-lookup"><span data-stu-id="869e5-124">Preliminary steps</span></span>
<span data-ttu-id="869e5-125">繼續詳細疑難排解之前，</span><span class="sxs-lookup"><span data-stu-id="869e5-125">Before proceeding to the detailed troubleshooting,</span></span>

* <span data-ttu-id="869e5-126">檢查 Azure 入口網站中虛擬機器的狀態，以找出是否有任何明顯的問題。</span><span class="sxs-lookup"><span data-stu-id="869e5-126">Check the status of the virtual machine in the Azure portal for any obvious issues.</span></span>
* <span data-ttu-id="869e5-127">依照 [基本疑難排解指南中常見 RDP 錯誤的快速檢修步驟](troubleshoot-rdp-connection.md#quick-troubleshooting-steps)操作。</span><span class="sxs-lookup"><span data-stu-id="869e5-127">Follow the [quick fix steps for common RDP errors in the basic troubleshooting guide](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).</span></span>

<span data-ttu-id="869e5-128">嘗試在完成這些步驟之後透過遠端桌面重新連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="869e5-128">Try reconnecting to the VM via Remote Desktop after these steps.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="869e5-129">詳細的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="869e5-129">Detailed troubleshooting steps</span></span>
<span data-ttu-id="869e5-130">由於下列來源的問題，可能會造成遠端桌面用戶端無法連線到 Azure VM 上的遠端桌面服務：</span><span class="sxs-lookup"><span data-stu-id="869e5-130">The Remote Desktop client may not be able to reach the Remote Desktop service on the Azure VM due to issues at the following sources:</span></span>

* [<span data-ttu-id="869e5-131">遠端桌面用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="869e5-131">Remote Desktop client computer</span></span>](#source-1-remote-desktop-client-computer)
* [<span data-ttu-id="869e5-132">組織內部網路的邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="869e5-132">Organization intranet edge device</span></span>](#source-2-organization-intranet-edge-device)
* [<span data-ttu-id="869e5-133">雲端服務端點和存取控制清單 (ACL)</span><span class="sxs-lookup"><span data-stu-id="869e5-133">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="869e5-134">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="869e5-134">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="869e5-135">以 Windows 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="869e5-135">Windows-based Azure VM</span></span>](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a><span data-ttu-id="869e5-136">來源 1：遠端桌面用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="869e5-136">Source 1: Remote Desktop client computer</span></span>
<span data-ttu-id="869e5-137">請確認您的電腦能夠建立「遠端桌面」連線，來連接到另一部內部部署且以 Windows 為基礎的電腦。</span><span class="sxs-lookup"><span data-stu-id="869e5-137">Verify that your computer can make Remote Desktop connections to another on-premises, Windows-based computer.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

<span data-ttu-id="869e5-138">如果不能，請檢查您電腦上的下列設定：</span><span class="sxs-lookup"><span data-stu-id="869e5-138">If you cannot, check for the following settings on your computer:</span></span>

* <span data-ttu-id="869e5-139">目前封鎖「遠端桌面」流量的本機防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="869e5-139">A local firewall setting that is blocking Remote Desktop traffic.</span></span>
* <span data-ttu-id="869e5-140">目前阻止「遠端桌面」連線的本機安裝用戶端 Proxy 軟體。</span><span class="sxs-lookup"><span data-stu-id="869e5-140">Locally installed client proxy software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="869e5-141">目前阻止「遠端桌面」連線的本機安裝網路監視軟體。</span><span class="sxs-lookup"><span data-stu-id="869e5-141">Locally installed network monitoring software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="869e5-142">目前阻止「遠端桌面」連線的其他類型安全性軟體，這些軟體會監視流量或允許/不允許特定類型的流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-142">Other types of security software that either monitor traffic or allow/disallow specific types of traffic that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="869e5-143">在所有這些情況下，請暫時停用軟體，然後嘗試透過「遠端連線」連接到內部部署電腦。</span><span class="sxs-lookup"><span data-stu-id="869e5-143">In all these cases, temporarily disable the software and try to connect to an on-premises computer via Remote Desktop.</span></span> <span data-ttu-id="869e5-144">如果這樣即可找出造成這個問題的實際原因，請和網路管理員合作，修正軟體設定以允許遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-144">If you can find out the actual cause this way, work with your network administrator to correct the software settings to allow Remote Desktop connections.</span></span>

## <a name="source-2-organization-intranet-edge-device"></a><span data-ttu-id="869e5-145">來源 2：組織內部網路的邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="869e5-145">Source 2: Organization intranet edge device</span></span>
<span data-ttu-id="869e5-146">請確認直接連接到網際網路的電腦能遠端連線到您的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="869e5-146">Verify that a computer directly connected to the Internet can make Remote Desktop connections to your Azure virtual machine.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

<span data-ttu-id="869e5-147">如果您沒有直接連線到網際網路的電腦，則在資源群組或雲端服務中建立和測試新的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="869e5-147">If you do not have a computer that is directly connected to the Internet, create and test with a new Azure virtual machine in a resource group or cloud service.</span></span> <span data-ttu-id="869e5-148">如需詳細資訊，請參閱 [在 Azure 中建立執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="869e5-148">For more information, see [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="869e5-149">測試完成之後，您可以刪除虛擬機器和資源群組或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="869e5-149">You can delete the virtual machine and the resource group or the cloud service, after the test.</span></span>

<span data-ttu-id="869e5-150">如果您可以對直接連線到網際網路的電腦建立遠端桌面連線，請檢查組織內部網路的邊緣裝置之下列項目：</span><span class="sxs-lookup"><span data-stu-id="869e5-150">If you can create a Remote Desktop connection with a computer directly attached to the Internet, check your organization intranet edge device for:</span></span>

* <span data-ttu-id="869e5-151">目前封鎖對網際網路之 HTTPS 連線的內部防火牆。</span><span class="sxs-lookup"><span data-stu-id="869e5-151">An internal firewall blocking HTTPS connections to the Internet.</span></span>
* <span data-ttu-id="869e5-152">目前阻止「遠端桌面」連線的 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="869e5-152">A proxy server preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="869e5-153">目前在邊緣網路中的裝置上執行且阻止「遠端桌面」連線的入侵偵測或網路監視軟體。</span><span class="sxs-lookup"><span data-stu-id="869e5-153">Intrusion detection or network monitoring software running on devices in your edge network that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="869e5-154">請和網路管理員合作，修正您組織內部網路的邊緣裝置設定，允許以 HTTPS 為基礎的網際網路遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-154">Work with your network administrator to correct the settings of your organization intranet edge device to allow HTTPS-based Remote Desktop connections to the Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="869e5-155">來源 3：雲端服務端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="869e5-155">Source 3: Cloud service endpoint and ACL</span></span>
<span data-ttu-id="869e5-156">對於使用傳統部署模型建立的 VM，請確認另一部位於相同雲端服務或虛擬網路中的 Azure VM 能夠對您的 Azure VM 進行「遠端桌面」連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-156">For VMs created using the Classic deployment model, verify that another Azure VM that is in the same cloud service or virtual network can make Remote Desktop connections to your Azure VM.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> <span data-ttu-id="869e5-157">如果是在資源管理員中建立的虛擬機器，請跳到 [來源 4：網路安全性群組](#source-4-network-security-groups)。</span><span class="sxs-lookup"><span data-stu-id="869e5-157">For virtual machines created in Resource Manager, skip to [Source 4: Network Security Groups](#source-4-network-security-groups).</span></span>

<span data-ttu-id="869e5-158">如果您沒有另一部虛擬機器位於相同的雲端服務或虛擬網路中，請建立一部。</span><span class="sxs-lookup"><span data-stu-id="869e5-158">If you do not have another virtual machine in the same cloud service or virtual network, create one.</span></span> <span data-ttu-id="869e5-159">依照 [在 Azure 中建立執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)中的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="869e5-159">Follow the steps in [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="869e5-160">測試完成之後，請刪除測試虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="869e5-160">Delete the test virtual machine after the test is completed.</span></span>

<span data-ttu-id="869e5-161">如果您可以透過「遠端桌面」連線到位於相同雲端服務或虛擬網路中的虛擬機器，請檢查下列設定：</span><span class="sxs-lookup"><span data-stu-id="869e5-161">If you can connect via Remote Desktop to a virtual machine in the same cloud service or virtual network, check for these settings:</span></span>

* <span data-ttu-id="869e5-162">目標 VM 上的遠端桌面流量端點組態：端點的私用 TCP 連接埠必須符合 VM 的遠端桌面服務所接聽的 TCP 連接埠 (預設值為 3389)。</span><span class="sxs-lookup"><span data-stu-id="869e5-162">The endpoint configuration for Remote Desktop traffic on the target VM: The private TCP port of the endpoint must match the TCP port on which the VM's Remote Desktop service is listening (default is 3389).</span></span>
* <span data-ttu-id="869e5-163">目標 VM 上的遠端桌面流量端點的 ACL：ACL 讓您可指定要根據來源 IP 位址允許或拒絕來自網際網路的連入流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-163">The ACL for the Remote Desktop traffic endpoint on the target VM: ACLs allow you to specify allowed or denied incoming traffic from the Internet based on its source IP address.</span></span> <span data-ttu-id="869e5-164">設定錯誤的 ACL 會阻止送至端點的連入遠端桌面流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-164">Misconfigured ACLs can prevent incoming Remote Desktop traffic to the endpoint.</span></span> <span data-ttu-id="869e5-165">檢查您的 ACL，以確保允許來自您的 Proxy 或其他邊緣伺服器的公用 IP 位址之連入流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-165">Check your ACLs to ensure that incoming traffic from your public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="869e5-166">如需詳細資訊，請參閱 [什麼是網路存取控制清單 (ACL)？](../../virtual-network/virtual-networks-acl.md)</span><span class="sxs-lookup"><span data-stu-id="869e5-166">For more information, see [What is a Network Access Control List (ACL)?](../../virtual-network/virtual-networks-acl.md)</span></span>

<span data-ttu-id="869e5-167">若要檢查端點是否為問題來源，請移除目前的端點，再選擇外部連接埠號碼介於 49152 到 65535 的隨機連接埠來建立新的端點。</span><span class="sxs-lookup"><span data-stu-id="869e5-167">To check if the endpoint is the source of the problem, remove the current endpoint and create a new one, choosing a random port in the range 49152–65535 for the external port number.</span></span> <span data-ttu-id="869e5-168">如需詳細資訊，請參閱[如何設定虛擬機器的端點](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="869e5-168">For more information, see [How to set up endpoints to a virtual machine](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="869e5-169">來源 4：網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="869e5-169">Source 4: Network Security Groups</span></span>
<span data-ttu-id="869e5-170">網路安全性群組能夠更精確地控制受允許的輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-170">Network Security Groups allow more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="869e5-171">您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。</span><span class="sxs-lookup"><span data-stu-id="869e5-171">You can create rules spanning subnets and cloud services in an Azure virtual network.</span></span>

<span data-ttu-id="869e5-172">使用 [IP 流量驗證](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)來確認網路安全性群組中的規則是否會封鎖虛擬機器的輸入或輸出流量。</span><span class="sxs-lookup"><span data-stu-id="869e5-172">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a Network Security Group is blocking traffic to or from a virtual machine.</span></span> <span data-ttu-id="869e5-173">您也可以檢閱有效的安全性群組規則，以確保輸入「允許」NSG 規則存在並已針對 RDP 連接埠 (預設值 3389) 設定優先順序。</span><span class="sxs-lookup"><span data-stu-id="869e5-173">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="869e5-174">如需詳細資訊，請參閱[使用有效安全性規則對 VM 流量流程進行疑難排解](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。</span><span class="sxs-lookup"><span data-stu-id="869e5-174">For more information, see [Using Effective Security Rules to troubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

## <a name="source-5-windows-based-azure-vm"></a><span data-ttu-id="869e5-175">來源 5：以 Windows 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="869e5-175">Source 5: Windows-based Azure VM</span></span>
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

<span data-ttu-id="869e5-176">請依照[本文](reset-rdp.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="869e5-176">Follow the instructions in [this article](reset-rdp.md).</span></span> <span data-ttu-id="869e5-177">這篇文章會重設虛擬機器上的「遠端桌面」服務：</span><span class="sxs-lookup"><span data-stu-id="869e5-177">This article resets the Remote Desktop service on the virtual machine:</span></span>

* <span data-ttu-id="869e5-178">啟用「遠端桌面」 Windows 防火牆預設規則 (TCP 連接埠 3389)。</span><span class="sxs-lookup"><span data-stu-id="869e5-178">Enable the "Remote Desktop" Windows Firewall default rule (TCP port 3389).</span></span>
* <span data-ttu-id="869e5-179">藉由將 HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections 登錄值設為 0 ，啟用遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-179">Enable Remote Desktop connections by setting the HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections registry value to 0.</span></span>

<span data-ttu-id="869e5-180">再次嘗試來自您電腦的連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-180">Try the connection from your computer again.</span></span> <span data-ttu-id="869e5-181">如果您還是無法透過遠端桌面連線，請檢查下列可能的問題：</span><span class="sxs-lookup"><span data-stu-id="869e5-181">If you are still not able to connect via Remote Desktop, check for the following possible problems:</span></span>

* <span data-ttu-id="869e5-182">遠端桌面服務未在目標 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="869e5-182">The Remote Desktop service is not running on the target VM.</span></span>
* <span data-ttu-id="869e5-183">遠端桌面服務未在 TCP 連接埠 3389 上接聽。</span><span class="sxs-lookup"><span data-stu-id="869e5-183">The Remote Desktop service is not listening on TCP port 3389.</span></span>
* <span data-ttu-id="869e5-184">Windows 防火牆或另一個本機防火牆有阻止遠端桌面流量的輸出規則。</span><span class="sxs-lookup"><span data-stu-id="869e5-184">Windows Firewall or another local firewall has an outbound rule that is preventing Remote Desktop traffic.</span></span>
* <span data-ttu-id="869e5-185">在 Azure 虛擬機器上執行的入侵偵測或網路監視軟體正在阻止遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-185">Intrusion detection or network monitoring software running on the Azure virtual machine is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="869e5-186">對於使用傳統部署模型所建立的 VM，您可以使用關於 Azure 虛擬機器的遠端 Azure PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="869e5-186">For VMs created using the classic deployment model, you can use a remote Azure PowerShell session to the Azure virtual machine.</span></span> <span data-ttu-id="869e5-187">首先，您需要為虛擬機器的代管雲端服務安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="869e5-187">First, you need to install a certificate for the virtual machine's hosting cloud service.</span></span> <span data-ttu-id="869e5-188">移至 [設定對 Azure 虛擬機器的安全遠端 PowerShell 存取](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) ，然後將 **InstallWinRMCertAzureVM.ps1** 指令檔下載到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="869e5-188">Go to [Configure Secure Remote PowerShell Access to Azure Virtual Machines](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) and download the **InstallWinRMCertAzureVM.ps1** script file to your local computer.</span></span>

<span data-ttu-id="869e5-189">接下來，如果尚未安裝 Azure PowerShell，則請先安裝。</span><span class="sxs-lookup"><span data-stu-id="869e5-189">Next, install Azure PowerShell if you haven't already.</span></span> <span data-ttu-id="869e5-190">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="869e5-190">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="869e5-191">接下來，開啟 Azure PowerShell 命令提示字元，並將目前資料夾變更為 **InstallWinRMCertAzureVM.ps1** 指令碼檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="869e5-191">Next, open an Azure PowerShell command prompt and change the current folder to the location of the **InstallWinRMCertAzureVM.ps1** script file.</span></span> <span data-ttu-id="869e5-192">若要執行 Azure PowerShell 指令碼，您必須設定正確的執行原則。</span><span class="sxs-lookup"><span data-stu-id="869e5-192">To run an Azure PowerShell script, you must set the correct execution policy.</span></span> <span data-ttu-id="869e5-193">請執行 **Get-ExecutionPolicy** 命令來判斷您目前的原則層級。</span><span class="sxs-lookup"><span data-stu-id="869e5-193">Run the **Get-ExecutionPolicy** command to determine your current policy level.</span></span> <span data-ttu-id="869e5-194">如需設定適當層級的相關資訊，請參閱 [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx)。</span><span class="sxs-lookup"><span data-stu-id="869e5-194">For information about setting the appropriate level, see [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).</span></span>

<span data-ttu-id="869e5-195">接下來，請填入您的 Azure 訂用帳戶名稱、雲端服務名稱以及虛擬機器名稱 (移除 "<" 和 ">" 字元)，然後再執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="869e5-195">Next, fill in your Azure subscription name, the cloud service name, and your virtual machine name (removing the < and > characters), and then run these commands.</span></span>

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of the cloud service that contains the target virtual machine>"
$vmName="<Name of the target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

<span data-ttu-id="869e5-196">您可以從 **Get-AzureSubscription** 命令顯示畫面中的 *SubscriptionName* 屬性，取得正確的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="869e5-196">You can get the correct subscription name from the *SubscriptionName* property of the display of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="869e5-197">您可以從 **Get-AzureVM** 命令顯示畫面中的 *ServiceName* 欄，取得虛擬機器的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="869e5-197">You can get the cloud service name for the virtual machine from the *ServiceName* column in the display of the **Get-AzureVM** command.</span></span>

<span data-ttu-id="869e5-198">請檢查您是否擁有新憑證。</span><span class="sxs-lookup"><span data-stu-id="869e5-198">Check if you have the new certificate.</span></span> <span data-ttu-id="869e5-199">開啟目前使用者的 [憑證] 嵌入式管理單元，然後查看 [受信任的根憑證授權單位\憑證] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="869e5-199">Open a Certificates snap-in for the current user and look in the **Trusted Root Certification Authorities\Certificates** folder.</span></span> <span data-ttu-id="869e5-200">您應該在 Issued To 資料行中查看具有您的雲端服務之 DNS 名稱的憑證 (範例：cloudservice4testing.cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="869e5-200">You should see a certificate with the DNS name of your cloud service in the Issued To column (example: cloudservice4testing.cloudapp.net).</span></span>

<span data-ttu-id="869e5-201">接下來，使用這些命令起始遠端 Azure PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="869e5-201">Next, initiate a remote Azure PowerShell session by using these commands.</span></span>

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

<span data-ttu-id="869e5-202">輸入有效的系統管理員認證之後，您應該會看到類似下列 Azure PowerShell 提示字元的內容：</span><span class="sxs-lookup"><span data-stu-id="869e5-202">After entering valid administrator credentials, you should see something similar to the following Azure PowerShell prompt:</span></span>

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

<span data-ttu-id="869e5-203">此提示的第一個部分是您的雲端服務名稱，其中包含目標 VM，這可以與 "cloudservice4testing.cloudapp.net" 不同。</span><span class="sxs-lookup"><span data-stu-id="869e5-203">The first part of this prompt is your cloud service name that contains the target VM, which could be different from "cloudservice4testing.cloudapp.net".</span></span> <span data-ttu-id="869e5-204">您現在可以針對此雲端服務發出 Azure PowerShell 命令，以調查所提到的問題並修正組態。</span><span class="sxs-lookup"><span data-stu-id="869e5-204">You can now issue Azure PowerShell commands for this cloud service to investigate the problems mentioned and correct the configuration.</span></span>

### <a name="to-manually-correct-the-remote-desktop-services-listening-tcp-port"></a><span data-ttu-id="869e5-205">若要手動更正接聽 TCP 連接埠的遠端桌面服務</span><span class="sxs-lookup"><span data-stu-id="869e5-205">To manually correct the Remote Desktop Services listening TCP port</span></span>
<span data-ttu-id="869e5-206">針對遠端 Azure PowerShell 工作階段提示字元，請執行此命令。</span><span class="sxs-lookup"><span data-stu-id="869e5-206">At the remote Azure PowerShell session prompt, run this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="869e5-207">PortNumber 屬性會顯示目前的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="869e5-207">The PortNumber property shows the current port number.</span></span> <span data-ttu-id="869e5-208">如有需要，請使用此命令，將遠端桌面連接埠號碼變更回預設值 (3389)。</span><span class="sxs-lookup"><span data-stu-id="869e5-208">If needed, change the Remote Desktop port number back to its default value (3389) by using this command.</span></span>

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

<span data-ttu-id="869e5-209">確認已使用此命令將連接埠變更為 3389。</span><span class="sxs-lookup"><span data-stu-id="869e5-209">Verify that the port has been changed to 3389 by using this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="869e5-210">使用此命令結束遠端 Azure PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="869e5-210">Exit the remote Azure PowerShell session by using this command.</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="869e5-211">確認 Azure VM 的遠端桌面端點也正在使用 TCP 連接埠 3398 做為其內部連接埠。</span><span class="sxs-lookup"><span data-stu-id="869e5-211">Verify that the Remote Desktop endpoint for the Azure VM is also using TCP port 3398 as its internal port.</span></span> <span data-ttu-id="869e5-212">重新啟動 Azure VM，然後再試一次遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="869e5-212">Restart the Azure VM and try the Remote Desktop connection again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="869e5-213">其他資源</span><span class="sxs-lookup"><span data-stu-id="869e5-213">Additional resources</span></span>
[<span data-ttu-id="869e5-214">如何重設 Windows 虛擬機器的密碼或遠端桌面服務</span><span class="sxs-lookup"><span data-stu-id="869e5-214">How to reset a password or the Remote Desktop service for Windows virtual machines</span></span>](reset-rdp.md)

[<span data-ttu-id="869e5-215">如何安裝和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="869e5-215">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

[<span data-ttu-id="869e5-216">疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線</span><span class="sxs-lookup"><span data-stu-id="869e5-216">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="869e5-217">疑難排解在 Azure 虛擬機器上執行的應用程式存取</span><span class="sxs-lookup"><span data-stu-id="869e5-217">Troubleshoot access to an application running on an Azure virtual machine</span></span>](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

