---
title: "Azure vm 的 aaaDetailed SSH 疑難排解 |Microsoft 文件"
description: "更詳細的 SSH 連接 tooan Azure 虛擬機器的問題的疑難排解步驟"
keywords: "ssh 連線被拒, ssh 錯誤, azure ssh, SSH 連線失敗"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a><span data-ttu-id="ad270-104">詳細的 SSH 連接 tooa Linux VM 在 Azure 中的問題的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="ad270-104">Detailed SSH troubleshooting steps for issues connecting tooa Linux VM in Azure</span></span>
<span data-ttu-id="ad270-105">有許多原因會造成該 hello SSH 用戶端可能無法在 hello VM 可以 tooreach hello SSH 服務。</span><span class="sxs-lookup"><span data-stu-id="ad270-105">There are many possible reasons that hello SSH client might not be able tooreach hello SSH service on hello VM.</span></span> <span data-ttu-id="ad270-106">如果您有更遵循透過 hello[疑難排解步驟的一般 SSH](troubleshoot-ssh-connection.md)，您需要 toofurther hello 連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ad270-106">If you have followed through hello more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md), you need toofurther troubleshoot hello connection issue.</span></span> <span data-ttu-id="ad270-107">這篇文章會引導您完成詳細的疑難排解步驟 toodetermine 其中 hello SSH 連線失敗，以及如何 tooresolve 它。</span><span class="sxs-lookup"><span data-stu-id="ad270-107">This article guides you through detailed troubleshooting steps toodetermine where hello SSH connection is failing and how tooresolve it.</span></span>

## <a name="take-preliminary-steps"></a><span data-ttu-id="ad270-108">採取預備步驟</span><span class="sxs-lookup"><span data-stu-id="ad270-108">Take preliminary steps</span></span>
<span data-ttu-id="ad270-109">hello 下列圖表顯示 hello 牽涉到的元件。</span><span class="sxs-lookup"><span data-stu-id="ad270-109">hello following diagram shows hello components that are involved.</span></span>

![顯示 SSH 服務元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

<span data-ttu-id="ad270-111">hello 下列步驟協助您找出 hello 失敗的 hello 來源，並找出因應措施或解決方案。</span><span class="sxs-lookup"><span data-stu-id="ad270-111">hello following steps help you isolate hello source of hello failure and figure out solutions or workarounds.</span></span>

1. <span data-ttu-id="ad270-112">檢查 hello hello 入口網站中的 hello VM 狀態。</span><span class="sxs-lookup"><span data-stu-id="ad270-112">Check hello status of hello VM in hello portal.</span></span>
   <span data-ttu-id="ad270-113">在 hello [Azure 入口網站](https://portal.azure.com)，選取**虛擬機器** > *VM 名稱*。</span><span class="sxs-lookup"><span data-stu-id="ad270-113">In hello [Azure portal](https://portal.azure.com), select **Virtual machines** > *VM name*.</span></span>

   <span data-ttu-id="ad270-114">hello hello VM 的狀態 窗格應該會顯示**執行**。</span><span class="sxs-lookup"><span data-stu-id="ad270-114">hello status pane for hello VM should show **Running**.</span></span> <span data-ttu-id="ad270-115">捲動 tooshow 計算、 儲存體和網路資源的最近活動。</span><span class="sxs-lookup"><span data-stu-id="ad270-115">Scroll down tooshow recent activity for compute, storage, and network resources.</span></span>

2. <span data-ttu-id="ad270-116">選取**設定**tooexamine 端點、 IP 位址、 網路安全性群組和其他設定。</span><span class="sxs-lookup"><span data-stu-id="ad270-116">Select **Settings** tooexamine endpoints, IP addresses, network security groups, and other settings.</span></span>

   <span data-ttu-id="ad270-117">hello VM 應該擁有端點，可定義您可以檢視中的 SSH 流量**端點**或**[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)**。</span><span class="sxs-lookup"><span data-stu-id="ad270-117">hello VM should have an endpoint defined for SSH traffic that you can view in **Endpoints** or **[Network security group](../../virtual-network/virtual-networks-nsg.md)**.</span></span> <span data-ttu-id="ad270-118">使用 Resource Manager 來建立之 VM 中的端點會儲存在網路安全性群組中。</span><span class="sxs-lookup"><span data-stu-id="ad270-118">Endpoints in VMs that were created by using Resource Manager are stored in a network security group.</span></span> <span data-ttu-id="ad270-119">此外，請確認 hello 規則已套用的 toohello 網路安全性群組，和它們所參考 hello 子網路中。</span><span class="sxs-lookup"><span data-stu-id="ad270-119">Also, verify that hello rules have been applied toohello network security group and that they're referenced in hello subnet.</span></span>

<span data-ttu-id="ad270-120">tooverify 網路連線，請檢查 hello 設定端點，並請參閱可連線到另一個通訊協定，例如 HTTP 或其他服務的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="ad270-120">tooverify network connectivity, check hello configured endpoints and see if you can reach hello VM through another protocol, such as HTTP or another service.</span></span>

<span data-ttu-id="ad270-121">完成這些步驟之後, 再試一次 hello SSH 連線一次。</span><span class="sxs-lookup"><span data-stu-id="ad270-121">After these steps, try hello SSH connection again.</span></span>

## <a name="find-hello-source-of-hello-issue"></a><span data-ttu-id="ad270-122">找出 hello hello 問題來源</span><span class="sxs-lookup"><span data-stu-id="ad270-122">Find hello source of hello issue</span></span>
<span data-ttu-id="ad270-123">hello SSH 用戶端電腦上的可能會因為 tooissues 或 hello 下列區域中的錯誤設定 hello Azure VM 上 tooreach hello SSH 服務失敗：</span><span class="sxs-lookup"><span data-stu-id="ad270-123">hello SSH client on your computer might fail tooreach hello SSH service on hello Azure VM due tooissues or misconfigurations in hello following areas:</span></span>

* [<span data-ttu-id="ad270-124">SSH 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="ad270-124">SSH client computer</span></span>](#source-1-ssh-client-computer)
* [<span data-ttu-id="ad270-125">組織邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="ad270-125">Organization edge device</span></span>](#source-2-organization-edge-device)
* [<span data-ttu-id="ad270-126">雲端服務端點和存取控制清單 (ACL)</span><span class="sxs-lookup"><span data-stu-id="ad270-126">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="ad270-127">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ad270-127">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="ad270-128">以 Linux 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="ad270-128">Linux-based Azure VM</span></span>](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a><span data-ttu-id="ad270-129">來源 1：SSH 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="ad270-129">Source 1: SSH client computer</span></span>
<span data-ttu-id="ad270-130">tooeliminate 為 hello 來源 hello 失敗的電腦驗證，它可以進行 SSH 連線 tooanother 內部，以 Linux 為基礎的電腦。</span><span class="sxs-lookup"><span data-stu-id="ad270-130">tooeliminate your computer as hello source of hello failure, verify that it can make SSH connections tooanother on-premises, Linux-based computer.</span></span>

![強調 SSH 用戶端電腦元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

<span data-ttu-id="ad270-132">如果 hello 連線失敗，請檢查您的電腦上下列問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad270-132">If hello connection fails, check for hello following issues on your computer:</span></span>

* <span data-ttu-id="ad270-133">正封鎖輸入或輸出 SSH 流量的本機防火牆設定 (TCP 22)</span><span class="sxs-lookup"><span data-stu-id="ad270-133">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span></span>
* <span data-ttu-id="ad270-134">正阻止 SSH 連線的本機安裝用戶端 Proxy 軟體</span><span class="sxs-lookup"><span data-stu-id="ad270-134">Locally installed client proxy software that is preventing SSH connections</span></span>
* <span data-ttu-id="ad270-135">正阻止 SSH 連線的本機安裝網路監視軟體</span><span class="sxs-lookup"><span data-stu-id="ad270-135">Locally installed network monitoring software that is preventing SSH connections</span></span>
* <span data-ttu-id="ad270-136">其他類型的安全性軟體，這會監視流量或允許/不允許特定類型的流量。</span><span class="sxs-lookup"><span data-stu-id="ad270-136">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span></span>

<span data-ttu-id="ad270-137">如果其中一種情形適用，暫時停用 hello 軟體，然後再次嘗試 SSH 連線 tooan 在內部部署電腦 toofind 出 hello hello 連接您的電腦已封鎖的原因。</span><span class="sxs-lookup"><span data-stu-id="ad270-137">If one of these conditions apply, temporarily disable hello software and try an SSH connection tooan on-premises computer toofind out hello reason hello connection is being blocked on your computer.</span></span> <span data-ttu-id="ad270-138">然後使用您的網路系統管理員 toocorrect hello 軟體設定 tooallow SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="ad270-138">Then work with your network administrator toocorrect hello software settings tooallow SSH connections.</span></span>

<span data-ttu-id="ad270-139">如果您使用憑證驗證，確認您擁有這些權限 toohello.ssh 資料夾主目錄中：</span><span class="sxs-lookup"><span data-stu-id="ad270-139">If you are using certificate authentication, verify that you have these permissions toohello .ssh folder in your home directory:</span></span>

* <span data-ttu-id="ad270-140">Chmod 700 ~/.ssh</span><span class="sxs-lookup"><span data-stu-id="ad270-140">Chmod 700 ~/.ssh</span></span>
* <span data-ttu-id="ad270-141">Chmod 644 ~/.ssh/\*.pub</span><span class="sxs-lookup"><span data-stu-id="ad270-141">Chmod 644 ~/.ssh/\*.pub</span></span>
* <span data-ttu-id="ad270-142">Chmod 600 ~/.ssh/id_rsa (或您儲存私密金鑰的任何其他檔案)</span><span class="sxs-lookup"><span data-stu-id="ad270-142">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span></span>
* <span data-ttu-id="ad270-143">Chmod 644 ~/.ssh/known_hosts （包含您已連接 toovia SSH 主機）</span><span class="sxs-lookup"><span data-stu-id="ad270-143">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected toovia SSH)</span></span>

## <a name="source-2-organization-edge-device"></a><span data-ttu-id="ad270-144">來源 2：組織邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="ad270-144">Source 2: Organization edge device</span></span>
<span data-ttu-id="ad270-145">tooeliminate hello 失敗的來源 hello，為您的組織邊緣裝置會確認是否有直接連線 toohello 網際網路的電腦可以建立 SSH 連線 tooyour Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ad270-145">tooeliminate your organization edge device as hello source of hello failure, verify that a computer that's directly connected toohello Internet can make SSH connections tooyour Azure VM.</span></span> <span data-ttu-id="ad270-146">如果您要存取 hello VM 透過站對站 VPN、 Azure ExpressRoute 連線，請略過太[來源 4： 網路安全性群組](#nsg)。</span><span class="sxs-lookup"><span data-stu-id="ad270-146">If you are accessing hello VM over a site-to-site VPN or an Azure ExpressRoute connection, skip too[Source 4: Network security groups](#nsg).</span></span>

![強調組織邊緣裝置的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

<span data-ttu-id="ad270-148">如果您沒有直接連接的 toohello 網際網路的電腦，在它自己的資源群組或雲端服務中建立新的 Azure VM，並使用它。</span><span class="sxs-lookup"><span data-stu-id="ad270-148">If you don't have a computer that is directly connected toohello Internet, create a new Azure VM in its own resource group or cloud service and use it.</span></span> <span data-ttu-id="ad270-149">如需詳細資訊，請參閱 [在 Azure 中建立執行 Linux 的虛擬機器](quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ad270-149">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md).</span></span> <span data-ttu-id="ad270-150">當您完成與您的測試，請刪除 hello 資源的群組或 VM 和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ad270-150">Delete hello resource group or VM and cloud service when you're done with your testing.</span></span>

<span data-ttu-id="ad270-151">如果已直接連接 toohello 網際網路的電腦，您可以建立 SSH 連線，請檢查您組織的邊緣裝置進行：</span><span class="sxs-lookup"><span data-stu-id="ad270-151">If you can create an SSH connection with a computer that's directly connected toohello Internet, check your organization edge device for:</span></span>

* <span data-ttu-id="ad270-152">內部防火牆封鎖 SSH hello 網際網路流量</span><span class="sxs-lookup"><span data-stu-id="ad270-152">An internal firewall that's blocking SSH traffic with hello Internet</span></span>
* <span data-ttu-id="ad270-153">Proxy 伺服器是否阻止 SSH 進行連線</span><span class="sxs-lookup"><span data-stu-id="ad270-153">A proxy server that's preventing SSH connections</span></span>
* <span data-ttu-id="ad270-154">在邊緣網路裝置上執行的入侵偵測或網路監視軟體是否阻止 SSH 進行連線</span><span class="sxs-lookup"><span data-stu-id="ad270-154">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span></span>

<span data-ttu-id="ad270-155">使用您的組織邊緣裝置 tooallow SSH 的流量以 hello 網際網路的網路系統管理員 toocorrect hello 設定。</span><span class="sxs-lookup"><span data-stu-id="ad270-155">Work with your network administrator toocorrect hello settings of your organization edge devices tooallow SSH traffic with hello Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="ad270-156">來源 3：雲端服務端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="ad270-156">Source 3: Cloud service endpoint and ACL</span></span>
> [!NOTE]
> <span data-ttu-id="ad270-157">此來源適用於使用 hello 傳統部署模型所建立的 tooVMs。</span><span class="sxs-lookup"><span data-stu-id="ad270-157">This source applies only tooVMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="ad270-158">對於使用資源管理員所建立的 Vm，請跳過[來源 4： 網路安全性群組](#nsg)。</span><span class="sxs-lookup"><span data-stu-id="ad270-158">For VMs that were created by using Resource Manager, skip too[source 4: Network security groups](#nsg).</span></span>

<span data-ttu-id="ad270-159">tooeliminate hello 雲端服務端點和為 hello hello 失敗來源的 ACL，請確認在另一個 Azure VM hello 相同虛擬網路可讓 SSH 連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="ad270-159">tooeliminate hello cloud service endpoint and ACL as hello source of hello failure, verify that another Azure VM in hello same virtual network can make SSH connections tooyour VM.</span></span>

![強調雲端服務端點和 ACL 的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

<span data-ttu-id="ad270-161">如果您沒有在 hello 另一個 VM 相同的虛擬網路，您可以輕鬆地建立一個。</span><span class="sxs-lookup"><span data-stu-id="ad270-161">If you don't have another VM in hello same virtual network, you can easily create one.</span></span> <span data-ttu-id="ad270-162">如需詳細資訊，請參閱[使用 hello CLI 在 Azure 上建立 Linux VM](quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ad270-162">For more information, see [Create a Linux VM on Azure using hello CLI](quick-create-cli.md).</span></span> <span data-ttu-id="ad270-163">刪除 hello 額外的 VM，當您在與您的測試。</span><span class="sxs-lookup"><span data-stu-id="ad270-163">Delete hello extra VM when you are done with your testing.</span></span>

<span data-ttu-id="ad270-164">如果您可以使用中的 VM 建立 SSH 連線 hello 相同虛擬網路，請檢查下列區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad270-164">If you can create an SSH connection with a VM in hello same virtual network, check hello following areas:</span></span>

* <span data-ttu-id="ad270-165">**hello hello 目標 VM 上的 SSH 流量的端點組態。**</span><span class="sxs-lookup"><span data-stu-id="ad270-165">**hello endpoint configuration for SSH traffic on hello target VM.**</span></span> <span data-ttu-id="ad270-166">hello 私人 TCP 連接埠的 hello 端點應該符合 hello 的 hello SSH hello VM 上的服務所接聽的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ad270-166">hello private TCP port of hello endpoint should match hello TCP port on which hello SSH service on hello VM is listening.</span></span> <span data-ttu-id="ad270-167">（hello 預設連接埠為 22）。</span><span class="sxs-lookup"><span data-stu-id="ad270-167">(hello default port is 22).</span></span> <span data-ttu-id="ad270-168">確認選取的 hello Azure 入口網站中的 hello SSH TCP 通訊埠編號**虛擬機器** > *VM 名稱* > **設定** > **端點**。</span><span class="sxs-lookup"><span data-stu-id="ad270-168">Verify hello SSH TCP port number in hello Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span></span>
* <span data-ttu-id="ad270-169">**hello hello 目標虛擬機器上的 hello SSH 流量端點 ACL。**</span><span class="sxs-lookup"><span data-stu-id="ad270-169">**hello ACL for hello SSH traffic endpoint on hello target virtual machine.**</span></span> <span data-ttu-id="ad270-170">ACL 可讓您 toospecify 允許或拒絕連入流量從 hello 網際網路，根據其來源 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ad270-170">An ACL enables you toospecify allowed or denied incoming traffic from hello Internet, based on its source IP address.</span></span> <span data-ttu-id="ad270-171">設定不正確的 Acl 可以防止傳入 SSH 流量 toohello 端點。</span><span class="sxs-lookup"><span data-stu-id="ad270-171">Misconfigured ACLs can prevent incoming SSH traffic toohello endpoint.</span></span> <span data-ttu-id="ad270-172">請檢查您允許您的 proxy 或其他的邊緣伺服器 hello 公用 IP 位址的連入流量的 Acl tooensure。</span><span class="sxs-lookup"><span data-stu-id="ad270-172">Check your ACLs tooensure that incoming traffic from hello public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="ad270-173">如需詳細資訊，請參閱 [關於網路存取控制清單 (ACL)](../../virtual-network/virtual-networks-acl.md)。</span><span class="sxs-lookup"><span data-stu-id="ad270-173">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span></span>

<span data-ttu-id="ad270-174">tooeliminate hello 端點做為來源的 hello 問題，請移除 hello 目前端點、 建立另一個端點，並指定 hello SSH 名稱 （TCP 連接埠 22 hello 公用和私用連接埠號碼）。</span><span class="sxs-lookup"><span data-stu-id="ad270-174">tooeliminate hello endpoint as a source of hello problem, remove hello current endpoint, create another endpoint, and specify hello SSH name (TCP port 22 for hello public and private port number).</span></span> <span data-ttu-id="ad270-175">如需詳細資訊，請參閱 [在 Azure 中設定虛擬機器的端點](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ad270-175">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="ad270-176">來源 4：網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ad270-176">Source 4: Network security groups</span></span>
<span data-ttu-id="ad270-177">網路安全性群組可讓您 toohave 允許輸入和輸出流量的更細微的控制。</span><span class="sxs-lookup"><span data-stu-id="ad270-177">Network security groups enable you toohave more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="ad270-178">您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。</span><span class="sxs-lookup"><span data-stu-id="ad270-178">You can create rules that span subnets and cloud services in an Azure virtual network.</span></span> <span data-ttu-id="ad270-179">請檢查網路安全性群組規則 tooensure hello 允許網際網路從該 SSH 流量 tooand。</span><span class="sxs-lookup"><span data-stu-id="ad270-179">Check your network security group rules tooensure that SSH traffic tooand from hello Internet is allowed.</span></span>
<span data-ttu-id="ad270-180">如需詳細資訊，請參閱 [關於網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="ad270-180">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

<span data-ttu-id="ad270-181">您也可以使用 IP 確認 toovalidate hello NSG 組態。</span><span class="sxs-lookup"><span data-stu-id="ad270-181">You can also use IP Verify toovalidate hello NSG configuration.</span></span> <span data-ttu-id="ad270-182">如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。</span><span class="sxs-lookup"><span data-stu-id="ad270-182">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="source-5-linux-based-azure-virtual-machine"></a><span data-ttu-id="ad270-183">來源 5：以 Linux 為基礎的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ad270-183">Source 5: Linux-based Azure virtual machine</span></span>
<span data-ttu-id="ad270-184">hello 最後一個可能發生的問題來源是 hello Azure 虛擬機器本身。</span><span class="sxs-lookup"><span data-stu-id="ad270-184">hello last source of possible problems is hello Azure virtual machine itself.</span></span>

![強調以 Linux 為基礎的 Azure 虛擬機器的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

<span data-ttu-id="ad270-186">如果還沒有這麼做，請依照 hello 指示[tooreset 密碼或 SSH Linux 型虛擬機器](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ad270-186">If you haven't done so already, follow hello instructions [tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="ad270-187">再次嘗試從您的電腦連線。</span><span class="sxs-lookup"><span data-stu-id="ad270-187">Try connecting from your computer again.</span></span> <span data-ttu-id="ad270-188">如果仍然失敗，則會 hello 以下是一些 hello 可能的問題：</span><span class="sxs-lookup"><span data-stu-id="ad270-188">If it still fails, hello following are some of hello possible issues:</span></span>

* <span data-ttu-id="ad270-189">hello SSH 服務未執行 hello 目標虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="ad270-189">hello SSH service is not running on hello target virtual machine.</span></span>
* <span data-ttu-id="ad270-190">hello SSH 服務不會接聽 TCP 通訊埠 22。</span><span class="sxs-lookup"><span data-stu-id="ad270-190">hello SSH service is not listening on TCP port 22.</span></span> <span data-ttu-id="ad270-191">tootest，在本機電腦上安裝 telnet 用戶端，並執行 「 telnet *cloudServiceName*。.cloudapp.net 22"。</span><span class="sxs-lookup"><span data-stu-id="ad270-191">tootest, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span></span> <span data-ttu-id="ad270-192">此步驟決定 hello 虛擬機器時可允許傳入和傳出通訊 toohello SSH 的端點。</span><span class="sxs-lookup"><span data-stu-id="ad270-192">This step determines if hello virtual machine allows inbound and outbound communication toohello SSH endpoint.</span></span>
* <span data-ttu-id="ad270-193">hello hello 目標虛擬機器上的本機防火牆有使輸入或輸出 SSH 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="ad270-193">hello local firewall on hello target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span></span>
* <span data-ttu-id="ad270-194">入侵偵測或網路監視 hello Azure 虛擬機器執行的軟體防止 SSH 連接。</span><span class="sxs-lookup"><span data-stu-id="ad270-194">Intrusion detection or network monitoring software that's running on hello Azure virtual machine is preventing SSH connections.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad270-195">其他資源</span><span class="sxs-lookup"><span data-stu-id="ad270-195">Additional resources</span></span>
<span data-ttu-id="ad270-196">如需疑難排解應用程式存取的詳細資訊，請參閱[疑難排解存取 tooan 應用程式在 Azure 虛擬機器上執行](troubleshoot-app-connection.md)</span><span class="sxs-lookup"><span data-stu-id="ad270-196">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](troubleshoot-app-connection.md)</span></span>
