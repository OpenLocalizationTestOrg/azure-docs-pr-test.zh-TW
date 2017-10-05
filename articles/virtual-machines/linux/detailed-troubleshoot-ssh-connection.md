---
title: "Azure VM 的詳細 SSH 疑難排解 | Microsoft Docs"
description: "針對連線到 Azure 虛擬機器的問題更詳細的 SSH 疑難排解步驟"
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
ms.openlocfilehash: 9ccdb3fbca21264065eeb1c4e46314c62af4c2e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-to-a-linux-vm-in-azure"></a><span data-ttu-id="1f8a6-104">連線到 Azure 中 Linux VM 之問題的詳細 SSH 疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="1f8a6-104">Detailed SSH troubleshooting steps for issues connecting to a Linux VM in Azure</span></span>
<span data-ttu-id="1f8a6-105">SSH 用戶端無法連線至 VM 上的 SSH 服務，可能涉及許多原因。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-105">There are many possible reasons that the SSH client might not be able to reach the SSH service on the VM.</span></span> <span data-ttu-id="1f8a6-106">如果您已經完成較為 [一般的 SSH 疑難排解步驟](troubleshoot-ssh-connection.md)，您必須進一步針對連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-106">If you have followed through the more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md), you need to further troubleshoot the connection issue.</span></span> <span data-ttu-id="1f8a6-107">這篇文章會引導您完成詳細的疑難排解步驟，以判斷 SSH 連線失敗的位置和解決方法。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-107">This article guides you through detailed troubleshooting steps to determine where the SSH connection is failing and how to resolve it.</span></span>

## <a name="take-preliminary-steps"></a><span data-ttu-id="1f8a6-108">採取預備步驟</span><span class="sxs-lookup"><span data-stu-id="1f8a6-108">Take preliminary steps</span></span>
<span data-ttu-id="1f8a6-109">下列圖表顯示相關的元件。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-109">The following diagram shows the components that are involved.</span></span>

![顯示 SSH 服務元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

<span data-ttu-id="1f8a6-111">下列步驟可協助您隔離失敗的來源，並找出解決方案或因應措施。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-111">The following steps help you isolate the source of the failure and figure out solutions or workarounds.</span></span>

1. <span data-ttu-id="1f8a6-112">在入口網站中檢查 VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-112">Check the status of the VM in the portal.</span></span>
   <span data-ttu-id="1f8a6-113">在 [Azure 入口網站](https://portal.azure.com)中，選取 [虛擬機器] > VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-113">In the [Azure portal](https://portal.azure.com), select **Virtual machines** > *VM name*.</span></span>

   <span data-ttu-id="1f8a6-114">VM 的狀態窗格應該會顯示 [正在執行] 。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-114">The status pane for the VM should show **Running**.</span></span> <span data-ttu-id="1f8a6-115">向下捲動以顯示計算、儲存體和網路資源的近期活動。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-115">Scroll down to show recent activity for compute, storage, and network resources.</span></span>

2. <span data-ttu-id="1f8a6-116">選取 [設定]  以檢查端點、IP 位址、網路安全性群組及其他設定。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-116">Select **Settings** to examine endpoints, IP addresses, network security groups, and other settings.</span></span>

   <span data-ttu-id="1f8a6-117">VM 應該有一個為 SSH 流量定義的端點，您可以在 [端點] 或**[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)**中檢視該端點。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-117">The VM should have an endpoint defined for SSH traffic that you can view in **Endpoints** or **[Network security group](../../virtual-network/virtual-networks-nsg.md)**.</span></span> <span data-ttu-id="1f8a6-118">使用 Resource Manager 來建立之 VM 中的端點會儲存在網路安全性群組中。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-118">Endpoints in VMs that were created by using Resource Manager are stored in a network security group.</span></span> <span data-ttu-id="1f8a6-119">另外，也請確認是否已將規則套用至網路安全性群組，以及子網路中是否有參考這些規則。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-119">Also, verify that the rules have been applied to the network security group and that they're referenced in the subnet.</span></span>

<span data-ttu-id="1f8a6-120">若要確認網路連線，請檢查設定的端點，並判斷您是否可以透過另一個通訊協定 (例如 HTTP 或另一個服務) 連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-120">To verify network connectivity, check the configured endpoints and see if you can reach the VM through another protocol, such as HTTP or another service.</span></span>

<span data-ttu-id="1f8a6-121">在這些步驟之後，請再試一次 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-121">After these steps, try the SSH connection again.</span></span>

## <a name="find-the-source-of-the-issue"></a><span data-ttu-id="1f8a6-122">找出問題來源</span><span class="sxs-lookup"><span data-stu-id="1f8a6-122">Find the source of the issue</span></span>
<span data-ttu-id="1f8a6-123">如果下列方面發生問題或設定錯誤，您電腦上的 SSH 用戶端可能就無法連線到 Azure VM 上的 SSH 服務：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-123">The SSH client on your computer might fail to reach the SSH service on the Azure VM due to issues or misconfigurations in the following areas:</span></span>

* [<span data-ttu-id="1f8a6-124">SSH 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="1f8a6-124">SSH client computer</span></span>](#source-1-ssh-client-computer)
* [<span data-ttu-id="1f8a6-125">組織邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="1f8a6-125">Organization edge device</span></span>](#source-2-organization-edge-device)
* [<span data-ttu-id="1f8a6-126">雲端服務端點和存取控制清單 (ACL)</span><span class="sxs-lookup"><span data-stu-id="1f8a6-126">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="1f8a6-127">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="1f8a6-127">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="1f8a6-128">以 Linux 為基礎的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="1f8a6-128">Linux-based Azure VM</span></span>](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a><span data-ttu-id="1f8a6-129">來源 1：SSH 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="1f8a6-129">Source 1: SSH client computer</span></span>
<span data-ttu-id="1f8a6-130">若要排除電腦為失敗來源的可能性，請確認您的電腦是否能 SSH 連線至另一部以 Linux 為基礎的內部部署電腦。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-130">To eliminate your computer as the source of the failure, verify that it can make SSH connections to another on-premises, Linux-based computer.</span></span>

![強調 SSH 用戶端電腦元件的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

<span data-ttu-id="1f8a6-132">如果連線失敗，請檢查您電腦上是否有下列問題：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-132">If the connection fails, check for the following issues on your computer:</span></span>

* <span data-ttu-id="1f8a6-133">正封鎖輸入或輸出 SSH 流量的本機防火牆設定 (TCP 22)</span><span class="sxs-lookup"><span data-stu-id="1f8a6-133">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span></span>
* <span data-ttu-id="1f8a6-134">正阻止 SSH 連線的本機安裝用戶端 Proxy 軟體</span><span class="sxs-lookup"><span data-stu-id="1f8a6-134">Locally installed client proxy software that is preventing SSH connections</span></span>
* <span data-ttu-id="1f8a6-135">正阻止 SSH 連線的本機安裝網路監視軟體</span><span class="sxs-lookup"><span data-stu-id="1f8a6-135">Locally installed network monitoring software that is preventing SSH connections</span></span>
* <span data-ttu-id="1f8a6-136">其他類型的安全性軟體，這會監視流量或允許/不允許特定類型的流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-136">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span></span>

<span data-ttu-id="1f8a6-137">如果有上述任何情況發生，請暫時停用該軟體，然後再嘗試 SSH 連線到內部部署的電腦，以找出電腦連線被封鎖的原因。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-137">If one of these conditions apply, temporarily disable the software and try an SSH connection to an on-premises computer to find out the reason the connection is being blocked on your computer.</span></span> <span data-ttu-id="1f8a6-138">接著，請和網路管理員合作，修正軟體設定以允許 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-138">Then work with your network administrator to correct the software settings to allow SSH connections.</span></span>

<span data-ttu-id="1f8a6-139">如果您使用憑證驗證，請確認您在主目錄中擁有 ssh 資料夾的下列權限：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-139">If you are using certificate authentication, verify that you have these permissions to the .ssh folder in your home directory:</span></span>

* <span data-ttu-id="1f8a6-140">Chmod 700 ~/.ssh</span><span class="sxs-lookup"><span data-stu-id="1f8a6-140">Chmod 700 ~/.ssh</span></span>
* <span data-ttu-id="1f8a6-141">Chmod 644 ~/.ssh/\*.pub</span><span class="sxs-lookup"><span data-stu-id="1f8a6-141">Chmod 644 ~/.ssh/\*.pub</span></span>
* <span data-ttu-id="1f8a6-142">Chmod 600 ~/.ssh/id_rsa (或您儲存私密金鑰的任何其他檔案)</span><span class="sxs-lookup"><span data-stu-id="1f8a6-142">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span></span>
* <span data-ttu-id="1f8a6-143">Chmod 644 ~/.ssh/known_hosts (包含您已透過 SSH 連接的主機)</span><span class="sxs-lookup"><span data-stu-id="1f8a6-143">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected to via SSH)</span></span>

## <a name="source-2-organization-edge-device"></a><span data-ttu-id="1f8a6-144">來源 2：組織邊緣裝置</span><span class="sxs-lookup"><span data-stu-id="1f8a6-144">Source 2: Organization edge device</span></span>
<span data-ttu-id="1f8a6-145">若要排除組織邊緣裝置為失敗來源的可能性，請確認直接連線到網際網路的電腦能 SSH 連線到您的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-145">To eliminate your organization edge device as the source of the failure, verify that a computer that's directly connected to the Internet can make SSH connections to your Azure VM.</span></span> <span data-ttu-id="1f8a6-146">如果您是透過站對站 VPN 或 Azure ExpressRoute 連線來存取 VM，請跳到 [來源 4：網路安全性群組](#nsg)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-146">If you are accessing the VM over a site-to-site VPN or an Azure ExpressRoute connection, skip to [Source 4: Network security groups](#nsg).</span></span>

![強調組織邊緣裝置的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

<span data-ttu-id="1f8a6-148">如果您沒有直接連線到網際網路的電腦，則請將新的 Azure VM 建立在它自己的資源群組或雲端服務中，然後使用它。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-148">If you don't have a computer that is directly connected to the Internet, create a new Azure VM in its own resource group or cloud service and use it.</span></span> <span data-ttu-id="1f8a6-149">如需詳細資訊，請參閱 [在 Azure 中建立執行 Linux 的虛擬機器](quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-149">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md).</span></span> <span data-ttu-id="1f8a6-150">當您完成測試後，請刪除此資源群組或 VM 及雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-150">Delete the resource group or VM and cloud service when you're done with your testing.</span></span>

<span data-ttu-id="1f8a6-151">如果您可以對直接連線到網際網路的電腦建立 SSH 連線，請檢查組織邊緣裝置的下列項目：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-151">If you can create an SSH connection with a computer that's directly connected to the Internet, check your organization edge device for:</span></span>

* <span data-ttu-id="1f8a6-152">內部防火牆是否導致網際網路 SSH 流量受到封鎖</span><span class="sxs-lookup"><span data-stu-id="1f8a6-152">An internal firewall that's blocking SSH traffic with the Internet</span></span>
* <span data-ttu-id="1f8a6-153">Proxy 伺服器是否阻止 SSH 進行連線</span><span class="sxs-lookup"><span data-stu-id="1f8a6-153">A proxy server that's preventing SSH connections</span></span>
* <span data-ttu-id="1f8a6-154">在邊緣網路裝置上執行的入侵偵測或網路監視軟體是否阻止 SSH 進行連線</span><span class="sxs-lookup"><span data-stu-id="1f8a6-154">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span></span>

<span data-ttu-id="1f8a6-155">請和網路管理員合作，修正組織邊緣裝置的設定，允許網際網路的 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-155">Work with your network administrator to correct the settings of your organization edge devices to allow SSH traffic with the Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="1f8a6-156">來源 3：雲端服務端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="1f8a6-156">Source 3: Cloud service endpoint and ACL</span></span>
> [!NOTE]
> <span data-ttu-id="1f8a6-157">此來源僅適用於使用傳統部署模型所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-157">This source applies only to VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="1f8a6-158">針對使用 Resource Manager 來建立的 VM，請跳到 [來源 4：網路安全性群組](#nsg)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-158">For VMs that were created by using Resource Manager, skip to [source 4: Network security groups](#nsg).</span></span>

<span data-ttu-id="1f8a6-159">若要排除雲端服務端點和 ACL 為失敗來源的可能性，請確認同一個虛擬網路中的其他 Azure VM 是否能 SSH 連線至您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-159">To eliminate the cloud service endpoint and ACL as the source of the failure, verify that another Azure VM in the same virtual network can make SSH connections to your VM.</span></span>

![強調雲端服務端點和 ACL 的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

<span data-ttu-id="1f8a6-161">如果您在相同的虛擬網路中沒有其他 VM，您可以輕鬆建立一部 VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-161">If you don't have another VM in the same virtual network, you can easily create one.</span></span> <span data-ttu-id="1f8a6-162">如需詳細資訊，請參閱 [使用 CLI 在 Azure 上建立 Linux VM](quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-162">For more information, see [Create a Linux VM on Azure using the CLI](quick-create-cli.md).</span></span> <span data-ttu-id="1f8a6-163">當您完成測試後，請刪除額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-163">Delete the extra VM when you are done with your testing.</span></span>

<span data-ttu-id="1f8a6-164">如果您可以與相同虛擬網路中的 VM 建立 SSH 連線，請檢查下列方面：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-164">If you can create an SSH connection with a VM in the same virtual network, check the following areas:</span></span>

* <span data-ttu-id="1f8a6-165">**目標 VM 上的 SSH 流量端點組態。**</span><span class="sxs-lookup"><span data-stu-id="1f8a6-165">**The endpoint configuration for SSH traffic on the target VM.**</span></span> <span data-ttu-id="1f8a6-166">此端點的私用 TCP 連接埠應符合 VM 上 SSH 服務正在接聽的 TCP 連接埠，</span><span class="sxs-lookup"><span data-stu-id="1f8a6-166">The private TCP port of the endpoint should match the TCP port on which the SSH service on the VM is listening.</span></span> <span data-ttu-id="1f8a6-167">預設連接埠為 22。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-167">(The default port is 22).</span></span> <span data-ttu-id="1f8a6-168">請在 Azure 入口網站中，選取 [虛擬機器] > VM 名稱 > [設定] > [端點]，來確認 SSH TCP 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-168">Verify the SSH TCP port number in the Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span></span>
* <span data-ttu-id="1f8a6-169">**目標虛擬機器上的 SSH 流量端點 ACL。**</span><span class="sxs-lookup"><span data-stu-id="1f8a6-169">**The ACL for the SSH traffic endpoint on the target virtual machine.**</span></span> <span data-ttu-id="1f8a6-170">ACL 可讓您指定要根據來源 IP 位址允許或拒絕來自網際網路的連入流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-170">An ACL enables you to specify allowed or denied incoming traffic from the Internet, based on its source IP address.</span></span> <span data-ttu-id="1f8a6-171">設定錯誤的 ACL 會阻止送至端點的連入 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-171">Misconfigured ACLs can prevent incoming SSH traffic to the endpoint.</span></span> <span data-ttu-id="1f8a6-172">檢查您的 ACL，確保允許來自您的 Proxy 或其他邊緣伺服器之公用 IP 位址的連入流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-172">Check your ACLs to ensure that incoming traffic from the public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="1f8a6-173">如需詳細資訊，請參閱 [關於網路存取控制清單 (ACL)](../../virtual-network/virtual-networks-acl.md)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-173">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span></span>

<span data-ttu-id="1f8a6-174">若要排除端點是問題來源的可能性，請移除目前的端點、建立另一個端點，然後指定 SSH 名稱 (TCP 連接埠 22 作為公用及私用連接埠號碼)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-174">To eliminate the endpoint as a source of the problem, remove the current endpoint, create another endpoint, and specify the SSH name (TCP port 22 for the public and private port number).</span></span> <span data-ttu-id="1f8a6-175">如需詳細資訊，請參閱 [在 Azure 中設定虛擬機器的端點](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-175">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="1f8a6-176">來源 4：網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="1f8a6-176">Source 4: Network security groups</span></span>
<span data-ttu-id="1f8a6-177">網路安全性群組可讓您更精確地控制受允許的輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-177">Network security groups enable you to have more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="1f8a6-178">您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-178">You can create rules that span subnets and cloud services in an Azure virtual network.</span></span> <span data-ttu-id="1f8a6-179">請檢查您的網路安全性群組規則，以確保允許往來網際網路的 SSH 流量。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-179">Check your network security group rules to ensure that SSH traffic to and from the Internet is allowed.</span></span>
<span data-ttu-id="1f8a6-180">如需詳細資訊，請參閱 [關於網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-180">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

<span data-ttu-id="1f8a6-181">您也可以使用「IP 確認」來驗證 NSG 組態。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-181">You can also use IP Verify to validate the NSG configuration.</span></span> <span data-ttu-id="1f8a6-182">如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-182">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="source-5-linux-based-azure-virtual-machine"></a><span data-ttu-id="1f8a6-183">來源 5：以 Linux 為基礎的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1f8a6-183">Source 5: Linux-based Azure virtual machine</span></span>
<span data-ttu-id="1f8a6-184">最後一個可能的問題來源就是 Azure 虛擬機器本身。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-184">The last source of possible problems is the Azure virtual machine itself.</span></span>

![強調以 Linux 為基礎的 Azure 虛擬機器的圖表](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

<span data-ttu-id="1f8a6-186">如果您還沒這麼做，請依照 [為 Linux 型虛擬機器重設密碼或 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)中的指示操作。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-186">If you haven't done so already, follow the instructions [to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="1f8a6-187">再次嘗試從您的電腦連線。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-187">Try connecting from your computer again.</span></span> <span data-ttu-id="1f8a6-188">如果仍然失敗，以下是一些可能的問題：</span><span class="sxs-lookup"><span data-stu-id="1f8a6-188">If it still fails, the following are some of the possible issues:</span></span>

* <span data-ttu-id="1f8a6-189">SSH 服務未在目標虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-189">The SSH service is not running on the target virtual machine.</span></span>
* <span data-ttu-id="1f8a6-190">SSH 服務未在 TCP 連接埠 22 上接聽。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-190">The SSH service is not listening on TCP port 22.</span></span> <span data-ttu-id="1f8a6-191">若要進行測試，請在本機電腦上安裝 telnet 用戶端，然後執行 "telnet *cloudServiceName*.cloudapp.net 22"。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-191">To test, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span></span> <span data-ttu-id="1f8a6-192">此步驟可判斷虛擬機器是否允許對 SSH 端點進行輸入和輸出通訊。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-192">This step determines if the virtual machine allows inbound and outbound communication to the SSH endpoint.</span></span>
* <span data-ttu-id="1f8a6-193">目標虛擬機器上的本機防火牆具有防止輸入或輸出 SSH 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-193">The local firewall on the target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span></span>
* <span data-ttu-id="1f8a6-194">在 Azure 虛擬機器上執行的入侵偵測或網路監視軟體正在阻止 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="1f8a6-194">Intrusion detection or network monitoring software that's running on the Azure virtual machine is preventing SSH connections.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f8a6-195">其他資源</span><span class="sxs-lookup"><span data-stu-id="1f8a6-195">Additional resources</span></span>
<span data-ttu-id="1f8a6-196">如需疑難排解應用程式存取的詳細資訊，請參閱[針對存取在 Azure 虛擬機器上執行的應用程式進行疑難排解](troubleshoot-app-connection.md)</span><span class="sxs-lookup"><span data-stu-id="1f8a6-196">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](troubleshoot-app-connection.md)</span></span>
