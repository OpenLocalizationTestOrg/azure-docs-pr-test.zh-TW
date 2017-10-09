---
title: "在具有多個 Nic 的 Azure Linux VM aaaCreate |Microsoft 文件"
description: "了解如何將 toocreate Linux VM 具有多個 Nic 附加 tooit 使用 hello Azure CLI 或資源管理員範本。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="23d6e-103">建立 Linux 虛擬機器具有使用 Azure CLI 1.0 hello 的多個 Nic</span><span class="sxs-lookup"><span data-stu-id="23d6e-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="23d6e-104">您可以在具有多個虛擬網路介面 (Nic) 附加 tooit Azure 中建立虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="23d6e-105">常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。</span><span class="sxs-lookup"><span data-stu-id="23d6e-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="23d6e-106">本文章提供快速命令 toocreate 具有多個 Nic 附加 tooit 的 VM。</span><span class="sxs-lookup"><span data-stu-id="23d6e-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="23d6e-107">如需詳細資訊，包括如何 toocreate 內您自己的多個 Nic 撞指令碼，深入了解[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="23d6e-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="23d6e-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="23d6e-109">您必須在建立 VM，而您無法加入現有的 VM 以 hello Azure CLI 1.0 Nic tooan 附加多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="23d6e-110">您可以[加入現有的 VM 以 hello Azure CLI 2.0 Nic tooan](multiple-nics.md)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="23d6e-111">您也可以[建立 hello 原始虛擬磁碟為基礎的 VM](copy-vm.md)並在您將部署的 hello VM 建立多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="23d6e-112">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="23d6e-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="23d6e-113">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="23d6e-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="23d6e-114">[Azure CLI 1.0](#create-supporting-resources) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="23d6e-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="23d6e-115">[Azure CLI 2.0](multiple-nics.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="23d6e-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="23d6e-116">建立支援資源</span><span class="sxs-lookup"><span data-stu-id="23d6e-116">Create supporting resources</span></span>
<span data-ttu-id="23d6e-117">請確定您擁有 hello [Azure CLI](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="23d6e-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="23d6e-118">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="23d6e-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="23d6e-119">範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。</span><span class="sxs-lookup"><span data-stu-id="23d6e-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="23d6e-120">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="23d6e-120">First, create a resource group.</span></span> <span data-ttu-id="23d6e-121">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="23d6e-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="23d6e-122">建立儲存體帳戶 toohold Vm。</span><span class="sxs-lookup"><span data-stu-id="23d6e-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="23d6e-123">hello 下列範例會建立名為的儲存體帳戶*mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="23d6e-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="23d6e-124">建立虛擬網路 tooconnect Vm。</span><span class="sxs-lookup"><span data-stu-id="23d6e-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="23d6e-125">hello 下列範例會建立虛擬網路，名為*myVnet*位址前置詞的*192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="23d6e-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="23d6e-126">建立兩個虛擬網路子網路 - 一個用於前端流量，另一個用於後端流量。</span><span class="sxs-lookup"><span data-stu-id="23d6e-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="23d6e-127">hello 下列範例會建立兩個子網路，名為*mySubnetFrontEnd*和*mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="23d6e-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="23d6e-128">建立及設定多個 NIC</span><span class="sxs-lookup"><span data-stu-id="23d6e-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="23d6e-129">您可以閱讀更多詳細資料[部署多個 Nic 使用 hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)，包括指令碼的迴圈 toocreate 所有 hello Nic hello 程序。</span><span class="sxs-lookup"><span data-stu-id="23d6e-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="23d6e-130">hello 下列範例會建立兩個 Nic，名為*myNic1*和*myNic2*，具有一個 NIC 連接 tooeach 子網路：</span><span class="sxs-lookup"><span data-stu-id="23d6e-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="23d6e-131">通常您也會建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)toohelp 管理，以及將流量分散到您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="23d6e-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="23d6e-132">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="23d6e-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="23d6e-133">繫結程式 Nic toohello 網路安全性群組，請使用`azure network nic set`。</span><span class="sxs-lookup"><span data-stu-id="23d6e-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="23d6e-134">hello 下列範例會繫結*myNic1*和*myNic2*與*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="23d6e-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="23d6e-135">建立 VM，並且附加 hello Nic</span><span class="sxs-lookup"><span data-stu-id="23d6e-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="23d6e-136">在建立 hello VM 時，您現在可以指定多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="23d6e-137">而使用`--nic-name`tooprovide 單一 NIC，改用`--nic-names`，並提供以逗號分隔清單的 Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="23d6e-138">您也需要 tootake 小心，當您選取 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="23d6e-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="23d6e-139">沒有限制，您可以加入 tooa VM 之 Nic 的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="23d6e-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="23d6e-140">深入了解 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="23d6e-141">hello 下列範例示範如何 toospecify 多個 Nic 然後按一下 VM 大小，支援使用多個 Nic (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="23d6e-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="23d6e-142">使用 Resource Manager 範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="23d6e-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="23d6e-143">Azure 資源管理員範本使用宣告式的 JSON 檔案 toodefine 環境。</span><span class="sxs-lookup"><span data-stu-id="23d6e-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="23d6e-144">您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="23d6e-145">資源管理員範本提供方式 toocreate 資源的多個執行個體在部署期間，例如建立多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="23d6e-146">您使用*複製*執行個體 toocreate toospecify hello 數目：</span><span class="sxs-lookup"><span data-stu-id="23d6e-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="23d6e-147">深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="23d6e-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="23d6e-148">您也可以使用`copyIndex()`toothen 附加數字 tooa 資源名稱，可讓您 toocreate `myNic1`， `myNic2`，等 hello 下列範例示範附加 hello 索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="23d6e-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="23d6e-149">您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="23d6e-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23d6e-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23d6e-150">Next steps</span></span>
<span data-ttu-id="23d6e-151">請確定 tooreview [Linux VM 大小](sizes.md)toocreating 具有多個 Nic 的 VM 時。</span><span class="sxs-lookup"><span data-stu-id="23d6e-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="23d6e-152">請注意 toohello 最大的 Nic 數目在支援每個 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="23d6e-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="23d6e-153">請記住，您無法再加入其他 Nic tooan 現有 VM，部署 hello VM 時，您必須建立所有 hello Nic。</span><span class="sxs-lookup"><span data-stu-id="23d6e-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="23d6e-154">請小心規劃您的部署 toomake 確定您已擁有 hello 開始所有 hello 所需的網路連線時。</span><span class="sxs-lookup"><span data-stu-id="23d6e-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

