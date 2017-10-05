---
title: "在 Azure 上針對 VM 名稱解析使用內部 DNS | Microsoft Docs"
description: "在 Azure 上針對 VM 名稱解析使用內部 DNS。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="4ecf7-103">在 Azure 上針對 VM 名稱解析使用內部 DNS</span><span class="sxs-lookup"><span data-stu-id="4ecf7-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="4ecf7-104">這篇文章說明如何使用虛擬 NIC 卡 (VNic) 和 DNS 標籤名稱設定 Linux VM 的靜態內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="4ecf7-105">靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="4ecf7-106">這些需求包括：</span><span class="sxs-lookup"><span data-stu-id="4ecf7-106">The requirements are:</span></span>

* [<span data-ttu-id="4ecf7-107">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="4ecf7-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="4ecf7-108">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="4ecf7-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4ecf7-109">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="4ecf7-109">CLI versions to complete the task</span></span>
<span data-ttu-id="4ecf7-110">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="4ecf7-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="4ecf7-111">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="4ecf7-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4ecf7-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="4ecf7-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="4ecf7-113">快速命令</span><span class="sxs-lookup"><span data-stu-id="4ecf7-113">Quick commands</span></span>

<span data-ttu-id="4ecf7-114">如果您需要快速完成工作，接下來這一節將詳細說明所需的命令。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="4ecf7-115">每個步驟的詳細資訊和內容可在文件其他地方找到，[從這裡開始](#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="4ecf7-116">必要條件︰資源群組、VNet、具有 SSH 輸入的 NSG、子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="4ecf7-117">使用靜態內部 DNS 名稱建立 VNic</span><span class="sxs-lookup"><span data-stu-id="4ecf7-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="4ecf7-118">`-r` CLI 旗標是用於設定 DNS 標籤，它提供 VNic 的靜態 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="4ecf7-119">將 VM 部署至 VNet、NSG 並連接 VNic</span><span class="sxs-lookup"><span data-stu-id="4ecf7-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="4ecf7-120">在部署至 Azure 期間，`-N` 將 VNic 連接到新的 VM。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="4ecf7-121">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="4ecf7-121">Detailed walkthrough</span></span>

<span data-ttu-id="4ecf7-122">Azure 上完整的連續整合和連續部署 (CiCd) 基礎結構需要特定的伺服器是靜態或長時間執行的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="4ecf7-123">像虛擬網路 (VNet) 和網路安全性群組 (NSG) 之類的 Azure 資產，最好是當做很少部署的靜態且長久的資源。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="4ecf7-124">VNet 部署之後可供新的部署重複使用，完全不會對基礎結構造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="4ecf7-125">新增至此靜態網路，Git 存放庫伺服器和 Jenkins 自動化伺服器會將 CiCd 傳遞至您的開發或測試環境。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="4ecf7-126">僅可在 Azure 虛擬網路內解析內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="4ecf7-127">因為 DNS 名稱是內部的，它們不會解析至外部網際網路，為基礎結構提供額外安全性。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="4ecf7-128">_將任何範例換成您自己的名稱。_</span><span class="sxs-lookup"><span data-stu-id="4ecf7-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="4ecf7-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="4ecf7-129">Create the Resource group</span></span>

<span data-ttu-id="4ecf7-130">需要資源群組以組織我們在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="4ecf7-131">如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ecf7-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="4ecf7-132">建立 VNet</span><span class="sxs-lookup"><span data-stu-id="4ecf7-132">Create the VNet</span></span>

<span data-ttu-id="4ecf7-133">第一個步驟是建立可放入 VM 的 VNet。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="4ecf7-134">在本逐步解說中，VNet 包含的一個子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="4ecf7-135">如需 Azure VNet 的詳細資訊，請參閱[使用 Azure CLI 建立虛擬網路](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ecf7-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="4ecf7-136">建立 NSG</span><span class="sxs-lookup"><span data-stu-id="4ecf7-136">Create the NSG</span></span>

<span data-ttu-id="4ecf7-137">子網路是建置在現有網路安全性群組的背後，所以我們在子網路之前建置 NSG。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="4ecf7-138">Azure NSG 相當於網路層的防火牆。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="4ecf7-139">如需 Azure NSG 的詳細資訊，請參閱[如何在 Azure CLI 中建立 NSG](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ecf7-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="4ecf7-140">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="4ecf7-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="4ecf7-141">由於需要從網際網路存取 Linux VM，因此需要有規則來允許輸入連接埠 22 流量通過網路流向 Linux VM 的連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="4ecf7-142">將子網路新增至 VNet</span><span class="sxs-lookup"><span data-stu-id="4ecf7-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="4ecf7-143">VNet 內的 VM 必須位於子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="4ecf7-144">每一個 VNet 可以有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="4ecf7-145">建立子網路，並將子網路和 NSG 產生關聯，以便將防火牆新增至子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="4ecf7-146">子網路現在已新增至 VNet 內，而且與 NSG 及與 NSG 規則相關聯。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="4ecf7-147">建立靜態 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="4ecf7-147">Creating static DNS names</span></span>

<span data-ttu-id="4ecf7-148">Azure 非常有彈性，但是若要針對 VM 名稱解析使用 DNS 名稱，您需要使用 DNS 標籤將它們建立為虛擬網路卡 (VNics)。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="4ecf7-149">VNic 很重要，因為您可以將它們連接至不同的 VM 以重複使用，這樣可讓 VNic 保持為靜態資源，而 VM 可以是暫時的。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="4ecf7-150">使用 VNic 上的 DNS 標籤，我們就可以從 VNet 中的其他 VM 啟用簡單名稱解析。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="4ecf7-151">使用可解析的名稱，會讓其他 VM 依據 DNS 名稱 `Jenkins` 存取自動化伺服器，或以 `gitrepo` 存取 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="4ecf7-152">建立 VNic，並將它與先前步驟中建立的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="4ecf7-153">將 VM 部署至 VNet 和 NSG</span><span class="sxs-lookup"><span data-stu-id="4ecf7-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="4ecf7-154">我們現在有 VNet、該 VNet 內的子網路，還有 NSG 做為防火牆來封鎖所有輸入流量 (除了用於 SSH 的連接埠 22)，以保護我們的子網路。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="4ecf7-155">現在可以將 VM 部署在這個現有的網路基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="4ecf7-156">您可以使用 Azure CLI 和 `azure vm create` 命令，將 Linux VM 部署至現有的 Azure 資源群組、VNet、子網路和 VNic。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="4ecf7-157">如需使用 CLI 來部署完整 VM 的詳細資訊，請參閱[使用 Azure CLI 建立完整的 Linux 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ecf7-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="4ecf7-158">我們使用 CLI 旗標來呼叫現有的資源，以指示 Azure 將 VM 部署在現有的網路內。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="4ecf7-159">重申一次，VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="4ecf7-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4ecf7-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ecf7-160">Next steps</span></span>
* [<span data-ttu-id="4ecf7-161">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="4ecf7-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4ecf7-162">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="4ecf7-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
