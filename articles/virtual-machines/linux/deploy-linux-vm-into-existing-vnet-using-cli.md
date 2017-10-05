---
title: "使用 Azure CLI 2.0 將 Linux VM 部署到現有網路 | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 將 Linux 虛擬機器部署至現有虛擬網路"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="1abef-103">如何使用 Azure CLI 將 Linux 虛擬機器部署至現有的 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="1abef-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="1abef-104">此文章說明如何使用 Azure CLI 2.0 將虛擬機器 (VM) 部署至現有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1abef-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="1abef-105">這些需求包括：</span><span class="sxs-lookup"><span data-stu-id="1abef-105">The requirements are:</span></span>

- [<span data-ttu-id="1abef-106">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="1abef-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="1abef-107">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="1abef-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="1abef-108">您也可以使用 [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="1abef-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1abef-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="1abef-109">Quick Commands</span></span>
<span data-ttu-id="1abef-110">如果您需要快速完成工作，下列章節詳細說明需要的命令。</span><span class="sxs-lookup"><span data-stu-id="1abef-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="1abef-111">每個步驟的詳細資訊和內容可在文件其他地方找到，[從這裡開始](#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="1abef-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="1abef-112">若要建立此自訂環境，您需要安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1abef-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1abef-113">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1abef-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1abef-114">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="1abef-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="1abef-115">**必要條件︰**Azure 資源群組、虛擬網路與子網路、允許 SSH 連入流量的網路安全性群組，以及虛擬網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="1abef-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="1abef-116">將 VM 部署至虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="1abef-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1abef-117">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="1abef-117">Detailed walkthrough</span></span>

<span data-ttu-id="1abef-118">像虛擬網路和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。</span><span class="sxs-lookup"><span data-stu-id="1abef-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="1abef-119">虛擬網路部署之後可供新的部署重複使用，完全不會對基礎結構造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="1abef-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="1abef-120">將虛擬網路想像成傳統的硬體網路交換器，您就不需要在每次部署時設定全新的硬體交換器。</span><span class="sxs-lookup"><span data-stu-id="1abef-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="1abef-121">有了正確設定的虛擬網路，您就可以一次又一次地將新的 VM 部署至該虛擬網路，整個虛擬網路生命週期內所需的變動極少 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="1abef-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="1abef-122">若要建立此自訂環境，您需要安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1abef-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1abef-123">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1abef-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1abef-124">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="1abef-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="1abef-125">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1abef-125">Create the resource group</span></span>

<span data-ttu-id="1abef-126">首先，建立 Azure 資源群組來組織您在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="1abef-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="1abef-127">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1abef-128">使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1abef-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1abef-129">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="1abef-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="1abef-130">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="1abef-130">Create the virtual network</span></span>

<span data-ttu-id="1abef-131">我們現在開始建置可放入 VM 的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1abef-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="1abef-132">如需虛擬網路的詳細資訊，請參閱[使用 Azure CLI 建立虛擬網路](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="1abef-133">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1abef-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1abef-134">下列範例會建立名為 myVnet 的虛擬網路和名為 mySubnet 的子網路：</span><span class="sxs-lookup"><span data-stu-id="1abef-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="1abef-135">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="1abef-135">Create the network security group</span></span>

<span data-ttu-id="1abef-136">Azure 網路安全性群組相當於網路層的防火牆。</span><span class="sxs-lookup"><span data-stu-id="1abef-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="1abef-137">如需網路安全性群組的詳細資訊，請參閱[如何使用 Azure CLI 建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="1abef-138">使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="1abef-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="1abef-139">下列範例建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="1abef-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="1abef-140">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="1abef-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="1abef-141">由於需要從網際網路存取 VM，因此需要有規則來允許輸入連接埠 22 流量通過網路流向 VM 的連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="1abef-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="1abef-142">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 新增網路安全性群組的連入規則。</span><span class="sxs-lookup"><span data-stu-id="1abef-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="1abef-143">下列範例會建立名為 myNetworkSecurityGroupRuleSSH 的規則：</span><span class="sxs-lookup"><span data-stu-id="1abef-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="1abef-144">將子網路連接至網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="1abef-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="1abef-145">網路安全性群組規則可以套用至子網路或特定虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="1abef-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="1abef-146">讓我們將網路安全性群組連接至子網路。</span><span class="sxs-lookup"><span data-stu-id="1abef-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="1abef-147">使用 [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) 將您的子網路連接至網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="1abef-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="1abef-148">將虛擬網路介面卡新增至子網路</span><span class="sxs-lookup"><span data-stu-id="1abef-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="1abef-149">虛擬網路介面卡 (VNic) 很重要，因為您可以將它們連接至不同的 VM 以重複使用它們。</span><span class="sxs-lookup"><span data-stu-id="1abef-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="1abef-150">雖然 VM 可以是暫時性的，但是這樣重複使用可讓您將 VNic 保持為靜態資源。</span><span class="sxs-lookup"><span data-stu-id="1abef-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="1abef-151">使用 [az network nic create](/cli/azure/network/nic#create) 建立 VNic，並將它與子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1abef-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1abef-152">下列範例會建立名為 myNic 的 VNic：</span><span class="sxs-lookup"><span data-stu-id="1abef-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="1abef-153">將 VM 部署至虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="1abef-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="1abef-154">您現在透過封鎖除 SSH 的連接埠 22 之外所有的輸入流量，讓虛擬網路、子網路與網路安全性群組來保護子網路。</span><span class="sxs-lookup"><span data-stu-id="1abef-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="1abef-155">現在可以將 VM 部署在這個現有的網路基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="1abef-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="1abef-156">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1abef-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1abef-157">如需使用旗標搭配 Azure CLI 2.0 來部署完整 VM 的詳細資訊，請參閱[使用 Azure CLI 建立完整的 Linux 環境](create-cli-complete.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="1abef-158">下列範例使用 Azure 受控磁碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1abef-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="1abef-159">這些磁碟是由 Azure 平台處理，不需要任何準備或位置來儲存它們。</span><span class="sxs-lookup"><span data-stu-id="1abef-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="1abef-160">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../../storage/storage-managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="1abef-161">如果您想要使用非受控磁碟，請參閱下列其他附註。</span><span class="sxs-lookup"><span data-stu-id="1abef-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="1abef-162">如果您使用受控磁碟，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="1abef-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="1abef-163">如果您想要使用使用預設未受控磁碟，則需要將下列其他參數新增至後續命令，以在名為 `mystorageaccount` 的儲存體帳戶中建立非受控磁碟：</span><span class="sxs-lookup"><span data-stu-id="1abef-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="1abef-164">您可以使用 CLI 旗標來呼叫現有的資源，以指示 Azure 將 VM 部署在現有的網路內。</span><span class="sxs-lookup"><span data-stu-id="1abef-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="1abef-165">虛擬網路和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="1abef-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="1abef-166">在此範例中，您沒有建立公用 IP 位址並將它指派給 VNic，因此無法透過網際網路公開地存取此 VM。</span><span class="sxs-lookup"><span data-stu-id="1abef-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="1abef-167">如需詳細資訊，請參閱[使用 Azure CLI 建立具有靜態公用 IP 的 VM](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1abef-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1abef-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1abef-168">Next steps</span></span>
<span data-ttu-id="1abef-169">如需以各種方式在 Azure 中建立虛擬機器的詳細資訊，請參閱下列資源︰</span><span class="sxs-lookup"><span data-stu-id="1abef-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="1abef-170">使用 Azure Resource Manager 範本和 Azure CLI 部署和管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1abef-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="1abef-171">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="1abef-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="1abef-172">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="1abef-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
