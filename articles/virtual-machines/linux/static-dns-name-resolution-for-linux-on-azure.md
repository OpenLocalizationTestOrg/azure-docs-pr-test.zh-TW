---
title: "搭配 Azure CLI 2.0 使用內部 DNS 進行 VM 名稱解析 | Microsoft Docs"
description: "如何搭配 Azure CLI 2.0 在 Azure 上建立虛擬網路介面卡並使用內部 DNS 進行 VM 名稱解析"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: 992920adb1ae3736d43cc5f0bbb2081a20a1674d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="e9f58-103">在 Azure 上建立虛擬網路介面卡並使用內部 DNS 進行 VM 名稱解析</span><span class="sxs-lookup"><span data-stu-id="e9f58-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="e9f58-104">本文說明如何搭配 Azure CLI 2.0，使用虛擬網路介面卡 (VNic) 和 DNS 標籤名稱來設定 Linux VM 的靜態內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9f58-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span></span> <span data-ttu-id="e9f58-105">您也可以使用 [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="e9f58-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e9f58-106">靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9f58-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="e9f58-107">這些需求包括：</span><span class="sxs-lookup"><span data-stu-id="e9f58-107">The requirements are:</span></span>

* [<span data-ttu-id="e9f58-108">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e9f58-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="e9f58-109">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="e9f58-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="e9f58-110">快速命令</span><span class="sxs-lookup"><span data-stu-id="e9f58-110">Quick commands</span></span>
<span data-ttu-id="e9f58-111">如果您需要快速完成工作，接下來這一節將詳細說明所需的命令。</span><span class="sxs-lookup"><span data-stu-id="e9f58-111">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="e9f58-112">每個步驟的詳細資訊和內容可在文件其他地方找到，從[這裡](#detailed-walkthrough)開始。</span><span class="sxs-lookup"><span data-stu-id="e9f58-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="e9f58-113">若要執行這些步驟，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9f58-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e9f58-114">先決條件︰資源群組、虛擬網路與子網路、具有 SSH 輸入的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e9f58-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="e9f58-115">使用靜態內部 DNS 名稱來建立虛擬網路介面卡</span><span class="sxs-lookup"><span data-stu-id="e9f58-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="e9f58-116">使用 [az network nic create](/cli/azure/network/nic#create) 來建立 vNic。</span><span class="sxs-lookup"><span data-stu-id="e9f58-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="e9f58-117">`--internal-dns-name` CLI 旗標是用來設定 DNS 標籤，可為虛擬網路介面卡 (vNic) 提供靜態 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9f58-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span></span> <span data-ttu-id="e9f58-118">下列範例會建立名為 `myNic` 的 vNic、將它連接到 `myVnet` 虛擬網路，以及建立名為 `jenkins` 的內部 DNS 名稱記錄：</span><span class="sxs-lookup"><span data-stu-id="e9f58-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-the-vnic"></a><span data-ttu-id="e9f58-119">部署 VM 並連接 vNic</span><span class="sxs-lookup"><span data-stu-id="e9f58-119">Deploy a VM and connect the vNic</span></span>
<span data-ttu-id="e9f58-120">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="e9f58-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e9f58-121">在部署至 Azure 的期間，`--nics` 旗標會將 vNic 連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="e9f58-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span></span> <span data-ttu-id="e9f58-122">下列範例會使用「Azure 受控磁碟」建立名為 `myVM` 的 VM，然後連結上一步驟中名為 `myNic` 的 vNic：</span><span class="sxs-lookup"><span data-stu-id="e9f58-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e9f58-123">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="e9f58-123">Detailed walkthrough</span></span>

<span data-ttu-id="e9f58-124">Azure 上完整的連續整合和連續部署 (CiCd) 基礎結構需要特定的伺服器是靜態或長時間執行的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9f58-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span> <span data-ttu-id="e9f58-125">虛擬網路和「網路安全性群組」之類的 Azure 資產，最好是當作很少部署的靜態且長久資源。</span><span class="sxs-lookup"><span data-stu-id="e9f58-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="e9f58-126">虛擬網路部署之後可供新的部署重複使用，完全不會對基礎結構造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="e9f58-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="e9f58-127">您可以稍後為您的開發或測試環境，將 Git 儲存機制伺服器或是會傳遞 CiCd 的 Jenkins 自動化伺服器新增到此虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="e9f58-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span></span>  

<span data-ttu-id="e9f58-128">僅可在 Azure 虛擬網路內解析內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9f58-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="e9f58-129">因為 DNS 名稱是內部的，它們不會解析至外部網際網路，為基礎結構提供額外安全性。</span><span class="sxs-lookup"><span data-stu-id="e9f58-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="e9f58-130">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="e9f58-130">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e9f58-131">範例參數名稱包含 `myResourceGroup`、`myNic` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="e9f58-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="e9f58-132">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e9f58-132">Create the resource group</span></span>
<span data-ttu-id="e9f58-133">首先，使用 [az group create](/cli/azure/group#create)建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e9f58-133">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e9f58-134">下列範例會在 `westus` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="e9f58-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="e9f58-135">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e9f58-135">Create the virtual network</span></span>

<span data-ttu-id="e9f58-136">下一步是建置要在其中啟動 VM 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e9f58-136">The next step is to build a virtual network to launch the VMs into.</span></span> <span data-ttu-id="e9f58-137">在本逐步解說中，此虛擬網路包含一個子網路。</span><span class="sxs-lookup"><span data-stu-id="e9f58-137">The virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="e9f58-138">如需有關 Azure 虛擬網路的詳細資訊，請參閱[使用 Azure CLI 建立虛擬網路](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e9f58-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="e9f58-139">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e9f58-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="e9f58-140">下列範例會建立名為 `myVnet` 的虛擬網路和名為 `mySubnet` 的子網路：</span><span class="sxs-lookup"><span data-stu-id="e9f58-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="e9f58-141">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="e9f58-141">Create the Network Security Group</span></span>
<span data-ttu-id="e9f58-142">「Azure 網路安全性群組」相當於網路層的防火牆。</span><span class="sxs-lookup"><span data-stu-id="e9f58-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="e9f58-143">如需有關「網路安全性群組」的詳細資訊，請參閱[如何在 Azure CLI 中建立 NSG](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e9f58-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="e9f58-144">使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e9f58-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="e9f58-145">下列範例會建立名為 `myNetworkSecurityGroup` 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="e9f58-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-to-allow-ssh"></a><span data-ttu-id="e9f58-146">新增輸入規則以允許 SSH</span><span class="sxs-lookup"><span data-stu-id="e9f58-146">Add an inbound rule to allow SSH</span></span>
<span data-ttu-id="e9f58-147">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 新增網路安全性群組的連入規則。</span><span class="sxs-lookup"><span data-stu-id="e9f58-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="e9f58-148">下列範例會建立名為 `myRuleAllowSSH` 的規則：</span><span class="sxs-lookup"><span data-stu-id="e9f58-148">The following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-the-subnet-with-the-network-security-group"></a><span data-ttu-id="e9f58-149">將子網路與網路安全性群組建立關聯</span><span class="sxs-lookup"><span data-stu-id="e9f58-149">Associate the subnet with the Network Security Group</span></span>
<span data-ttu-id="e9f58-150">若要將將子網路與「網路安全性群組」建立關聯，請使用 [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)。</span><span class="sxs-lookup"><span data-stu-id="e9f58-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="e9f58-151">下列範例會將子網路名稱 `mySubnet` 與名為 `myNetworkSecurityGroup` 的「網路安全性群組」建立關聯：</span><span class="sxs-lookup"><span data-stu-id="e9f58-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-the-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="e9f58-152">建立虛擬網路介面卡與靜態 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="e9f58-152">Create the virtual network interface card and static DNS names</span></span>
<span data-ttu-id="e9f58-153">Azure 非常有彈性，但是若要使用 DNS 名稱來進行 VM 名稱解析，您必須建立包含 DNS 標籤的虛擬網路介面卡 (VNic)。</span><span class="sxs-lookup"><span data-stu-id="e9f58-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="e9f58-154">VNic 很重要，因為您可以在整個基礎結構週期中，藉由將它們連接到不同的 VM 來重複使用它們。</span><span class="sxs-lookup"><span data-stu-id="e9f58-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span></span> <span data-ttu-id="e9f58-155">此方法既可讓 VM 為暫時性，又可將 vNic 保持為靜態資源。</span><span class="sxs-lookup"><span data-stu-id="e9f58-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="e9f58-156">藉由使用 vNic 上的 DNS 標籤，我們便能夠從 VNet 中的其他 VM 啟用簡單名稱解析。</span><span class="sxs-lookup"><span data-stu-id="e9f58-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span> <span data-ttu-id="e9f58-157">使用可解析的名稱，會讓其他 VM 依據 DNS 名稱 `Jenkins` 存取自動化伺服器，或以 `gitrepo` 存取 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9f58-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  

<span data-ttu-id="e9f58-158">使用 [az network nic create](/cli/azure/network/nic#create) 來建立 vNic。</span><span class="sxs-lookup"><span data-stu-id="e9f58-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="e9f58-159">下列範例會建立名為 `myNic` 的 vNic、將它連接到名為 `myVnet` 的 `myVnet` 虛擬網路，以及建立名為 `jenkins` 的內部 DNS 名稱記錄：</span><span class="sxs-lookup"><span data-stu-id="e9f58-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="e9f58-160">將 VM 部署至虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="e9f58-160">Deploy the VM into the virtual network infrastructure</span></span>
<span data-ttu-id="e9f58-161">我們現在有一個虛擬網路和子網路、一個作為防火牆而會封鎖所有輸入流量 (用於 SSH 的連接埠 22 除外) 來保護子網路的「網路安全性群組」，以及一個 vNic。</span><span class="sxs-lookup"><span data-stu-id="e9f58-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="e9f58-162">您現在可以在這個現有的網路基礎結構內部署 VM。</span><span class="sxs-lookup"><span data-stu-id="e9f58-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="e9f58-163">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="e9f58-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e9f58-164">下列範例會使用「Azure 受控磁碟」建立名為 `myVM` 的 VM，然後連結上一步驟中名為 `myNic` 的 vNic：</span><span class="sxs-lookup"><span data-stu-id="e9f58-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="e9f58-165">我們使用 CLI 旗標來呼叫現有的資源，以指示 Azure 將 VM 部署在現有的網路內。</span><span class="sxs-lookup"><span data-stu-id="e9f58-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="e9f58-166">重申一次，VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="e9f58-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e9f58-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9f58-167">Next steps</span></span>
* [<span data-ttu-id="e9f58-168">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="e9f58-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e9f58-169">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="e9f58-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
