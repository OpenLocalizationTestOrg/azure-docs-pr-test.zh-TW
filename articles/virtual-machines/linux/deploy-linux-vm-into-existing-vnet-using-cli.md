---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure CLI 2.0 |Microsoft 文件"
description: "了解如何 toodeploy Linux 虛擬機器到現有的虛擬網路使用 hello Azure CLI 2.0"
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
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="ff1da-103">如何在 Linux 虛擬機器，在現有的 Azure 虛擬網路以 hello Azure CLI toodeploy</span><span class="sxs-lookup"><span data-stu-id="ff1da-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="ff1da-104">本文章將示範如何 toouse 會 hello Azure CLI 2.0 toodeploy 虛擬機器 (VM)，在現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ff1da-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="ff1da-105">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="ff1da-105">hello requirements are:</span></span>

- [<span data-ttu-id="ff1da-106">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="ff1da-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="ff1da-107">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="ff1da-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="ff1da-108">您也可以執行下列步驟以 hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ff1da-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="ff1da-109">Quick Commands</span></span>
<span data-ttu-id="ff1da-110">如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="ff1da-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="ff1da-111">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="ff1da-112">toocreate 這個自訂的環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ff1da-113">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="ff1da-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ff1da-114">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="ff1da-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="ff1da-115">**必要條件︰**Azure 資源群組、虛擬網路與子網路、允許 SSH 連入流量的網路安全性群組，以及虛擬網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="ff1da-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="ff1da-116">部署 hello VM hello 虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="ff1da-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ff1da-117">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="ff1da-117">Detailed walkthrough</span></span>

<span data-ttu-id="ff1da-118">像虛擬網路和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。</span><span class="sxs-lookup"><span data-stu-id="ff1da-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="ff1da-119">部署虛擬網路之後可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。</span><span class="sxs-lookup"><span data-stu-id="ff1da-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="ff1da-120">考慮為傳統的硬體的網路交換器的虛擬網路-不需要的 tooconfigure 全新的硬體交換器每一次部署。</span><span class="sxs-lookup"><span data-stu-id="ff1da-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="ff1da-121">有正確設定的虛擬網路，您可以繼續 toodeploy 在該反覆與少的虛擬網路的新 Vm，如果有的話，需要變更虛擬網路的 hello hello 生命週期。</span><span class="sxs-lookup"><span data-stu-id="ff1da-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="ff1da-122">toocreate 這個自訂的環境中，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ff1da-123">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="ff1da-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ff1da-124">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="ff1da-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="ff1da-125">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="ff1da-125">Create hello resource group</span></span>

<span data-ttu-id="ff1da-126">首先，建立 Azure 資源群組 tooorganize 您在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="ff1da-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="ff1da-127">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ff1da-128">建立 hello 資源群組與[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ff1da-129">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="ff1da-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="ff1da-130">建立 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ff1da-130">Create hello virtual network</span></span>

<span data-ttu-id="ff1da-131">可讓建置 Azure 虛擬網路 toolaunch hello 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="ff1da-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="ff1da-132">如需有關虛擬網路的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="ff1da-133">建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ff1da-134">hello 下列範例會建立虛擬網路，名為*myVnet*和名為的子網路*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="ff1da-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="ff1da-135">建立 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ff1da-135">Create hello network security group</span></span>

<span data-ttu-id="ff1da-136">Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。</span><span class="sxs-lookup"><span data-stu-id="ff1da-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="ff1da-137">如需網路安全性群組的詳細資訊，請參閱[如何 toocreate 網路安全性群組中 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="ff1da-138">建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="ff1da-139">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ff1da-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="ff1da-140">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="ff1da-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="ff1da-141">hello VM 需要從 hello 網際網路，所以規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello VM 上所需的存取。</span><span class="sxs-lookup"><span data-stu-id="ff1da-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="ff1da-142">新增輸入的規則 hello 與網路安全性群組[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="ff1da-143">hello 下列範例會建立名為的規則*myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="ff1da-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="ff1da-144">附加 hello 子網路 toohello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ff1da-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="ff1da-145">hello 網路安全性群組規則可以套用的 tooa 子網路或特定虛擬網路介面。</span><span class="sxs-lookup"><span data-stu-id="ff1da-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="ff1da-146">可讓附加 hello 網路安全性群組 tooour 子網路。</span><span class="sxs-lookup"><span data-stu-id="ff1da-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="ff1da-147">附加您子網路 toohello 網路安全性群組與[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="ff1da-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="ff1da-148">新增虛擬網路介面卡 toohello 子網路</span><span class="sxs-lookup"><span data-stu-id="ff1da-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="ff1da-149">虛擬網路介面卡 (VNics) 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm。</span><span class="sxs-lookup"><span data-stu-id="ff1da-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="ff1da-150">這種重新使用可讓您 tookeep hello VNic 為靜態資源時可能是暫時的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="ff1da-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="ff1da-151">建立 VNic，並將它與 hello 的子網路關聯[az 網路 nic 建立](/cli/azure/network/nic#create)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ff1da-152">hello 下列範例會建立名為 VNic *myNic*:</span><span class="sxs-lookup"><span data-stu-id="ff1da-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="ff1da-153">部署 hello VM hello 虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="ff1da-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="ff1da-154">您現在會有虛擬網路和子網路和安全性群組 tooprotect hello 子網路透過 ssh 封鎖所有傳入的流量，除了連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="ff1da-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="ff1da-155">hello VM 現在可以部署在現有的網路基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="ff1da-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="ff1da-156">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ff1da-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ff1da-157">如需 hello 旗標與 hello Azure CLI 2.0 toodeploy toouse 完成 VM，請參閱 <<c0> [ 完整 Linux 環境建立使用 Azure CLI hello](create-cli-complete.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="ff1da-158">hello 下列範例會建立使用 Azure 受管理磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="ff1da-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="ff1da-159">這些磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。</span><span class="sxs-lookup"><span data-stu-id="ff1da-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="ff1da-160">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../../storage/storage-managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="ff1da-161">如果您想 toouse unmanaged 磁碟，請參閱 hello 下列的其他注意事項。</span><span class="sxs-lookup"><span data-stu-id="ff1da-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="ff1da-162">如果您使用受控磁碟，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="ff1da-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="ff1da-163">如果您想 toouse unmanaged 磁碟時，您需要下列額外的參數 toohello 繼續命令 toocreate unmanaged 磁碟 hello 儲存體帳戶中的 tooadd hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ff1da-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="ff1da-164">使用 hello CLI 旗標 toocall 出現有的資源，指示 Azure toodeploy hello VM hello 現有網路內。</span><span class="sxs-lookup"><span data-stu-id="ff1da-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="ff1da-165">虛擬網路和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="ff1da-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="ff1da-166">在此範例中，您建立，且指派公用 IP 位址 toohello VNic，讓此 VM 不是可公開存取 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ff1da-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="ff1da-167">如需詳細資訊，請參閱[建立 VM 的靜態公用 ip 位址使用 hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ff1da-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff1da-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff1da-168">Next steps</span></span>
<span data-ttu-id="ff1da-169">如需在 Azure 中的方式 toocreate 虛擬機器的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff1da-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="ff1da-170">使用 Azure Resource Manager 範本 toocreate 特定部署</span><span class="sxs-lookup"><span data-stu-id="ff1da-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="ff1da-171">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="ff1da-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="ff1da-172">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="ff1da-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
