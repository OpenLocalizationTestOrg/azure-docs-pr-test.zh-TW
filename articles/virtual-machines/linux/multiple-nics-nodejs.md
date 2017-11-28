---
title: "在 Azure 中建立連接多個 NIC 的 Linux VM | Microsoft Docs"
description: "了解如何使用 Azure CLI 或 Resource Manager 範本，來建立連接多個 NIC 的 Linux VM。"
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
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="de2e1-103">使用 Azure CLI 1.0 建立連接多個 NIC 的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="de2e1-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="de2e1-104">您可以在 Azure 中，建立連接多個虛擬網路介面 (NIC) 的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="de2e1-105">常見案例是有不同的子網路可用於前端和後端連線，或者專門用來監視或備份解決方案的網路。</span><span class="sxs-lookup"><span data-stu-id="de2e1-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="de2e1-106">本文提供快速命令來建立連接多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="de2e1-107">如需詳細資訊，包括如何在自己的 Bash 指令碼內建立多個 NIC，請深入了解 [部署多個 NIC 的 VM](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="de2e1-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="de2e1-109">當您建立 VM 時，必須連接多個 NIC - 您無法使用 Azure CLI 1.0 將 NIC 新增至現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="de2e1-110">您可以[使用 Azure CLI 2.0 將 NIC 新增至現有的 VM](multiple-nics.md)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="de2e1-111">您也可以[根據原始虛擬磁碟建立 VM](copy-vm.md)，並且在部署 VM 時建立多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="de2e1-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="de2e1-112">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="de2e1-112">CLI versions to complete the task</span></span>
<span data-ttu-id="de2e1-113">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="de2e1-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="de2e1-114">[Azure CLI 1.0](#create-supporting-resources) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="de2e1-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="de2e1-115">[Azure CLI 2.0](multiple-nics.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="de2e1-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="de2e1-116">建立支援資源</span><span class="sxs-lookup"><span data-stu-id="de2e1-116">Create supporting resources</span></span>
<span data-ttu-id="de2e1-117">確定您已登入 [Azure CLI](../../cli-install-nodejs.md)，並且使用的是 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="de2e1-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="de2e1-118">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="de2e1-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="de2e1-119">範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="de2e1-120">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="de2e1-120">First, create a resource group.</span></span> <span data-ttu-id="de2e1-121">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="de2e1-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="de2e1-122">建立儲存體帳戶以放置您的 VM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="de2e1-123">下列範例會建立名為 mystorageaccount 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="de2e1-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="de2e1-124">建立要與 VM 連線的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="de2e1-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="de2e1-125">下列範例會建立名為 myVnet 的虛擬網路，位址首碼為 192.168.0.0/16：</span><span class="sxs-lookup"><span data-stu-id="de2e1-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="de2e1-126">建立兩個虛擬網路子網路 - 一個用於前端流量，另一個用於後端流量。</span><span class="sxs-lookup"><span data-stu-id="de2e1-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="de2e1-127">下列範例會建立兩個子網路，名為 mySubnetFrontEnd 和 mySubnetBackEnd：</span><span class="sxs-lookup"><span data-stu-id="de2e1-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="de2e1-128">建立及設定多個 NIC</span><span class="sxs-lookup"><span data-stu-id="de2e1-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="de2e1-129">您可以深入了解更多有關 [使用 Azure CLI 部署多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)的詳細資訊，包括撰寫可進行迴圈程序的指令碼來建立所有的 NIC。</span><span class="sxs-lookup"><span data-stu-id="de2e1-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="de2e1-130">下列範例會建立兩個 NIC，名為 myNic1 與 myNic2，以及一個連線到各個子網路的 NIC：</span><span class="sxs-lookup"><span data-stu-id="de2e1-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

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

<span data-ttu-id="de2e1-131">通常您也可以建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)來協助管理，以及將流量分散到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="de2e1-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="de2e1-132">下列範例建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="de2e1-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="de2e1-133">使用 `azure network nic set`將您的 NIC 繫結至網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="de2e1-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="de2e1-134">下列範例會將 myNic1 和 myNic2 與 myNetworkSecurityGroup 繫結：</span><span class="sxs-lookup"><span data-stu-id="de2e1-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="de2e1-135">建立 VM 並附加 NIC</span><span class="sxs-lookup"><span data-stu-id="de2e1-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="de2e1-136">建立 VM 時，您現在可以指定多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="de2e1-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="de2e1-137">不使用 `--nic-name` 提供單一 NIC，而改用 `--nic-names`，並提供以逗號分隔的 NIC 清單。</span><span class="sxs-lookup"><span data-stu-id="de2e1-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="de2e1-138">當您選取 VM 大小時也需多加注意。</span><span class="sxs-lookup"><span data-stu-id="de2e1-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="de2e1-139">您可以新增至 VM 的 NIC 總數是有限制的。</span><span class="sxs-lookup"><span data-stu-id="de2e1-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="de2e1-140">深入了解 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="de2e1-141">下列範例示範如何指定多個 NIC，然後是使用多個 NIC 支援的 VM 大小 (Standard_DS2_v2)：</span><span class="sxs-lookup"><span data-stu-id="de2e1-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="de2e1-142">使用 Resource Manager 範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="de2e1-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="de2e1-143">Azure Resource Manager 範本會使用宣告式 JSON 檔案來定義您的環境。</span><span class="sxs-lookup"><span data-stu-id="de2e1-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="de2e1-144">您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="de2e1-145">Resource Manager 範本提供一種方式，可在部署期間建立資源的多個執行個體，例如建立多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="de2e1-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="de2e1-146">您使用 *copy* 來指定要建立的執行個體數目：</span><span class="sxs-lookup"><span data-stu-id="de2e1-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="de2e1-147">深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="de2e1-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="de2e1-148">您也可以使用 `copyIndex()`，然後在資源名稱後面附加一個數字，讓您能夠建立 `myNic1`、`myNic2`，依此類推。以下顯示附加索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="de2e1-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="de2e1-149">您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="de2e1-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de2e1-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de2e1-150">Next steps</span></span>
<span data-ttu-id="de2e1-151">嘗試建立具有多個 NIC 的 VM 時，請務必檢閱 [Linux VM 大小](sizes.md) 。</span><span class="sxs-lookup"><span data-stu-id="de2e1-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="de2e1-152">注意每個 VM 大小所支援的 NIC 數目上限。</span><span class="sxs-lookup"><span data-stu-id="de2e1-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="de2e1-153">請記住，您無法在現有 VM 中新增其他 NIC，您必須在部署 VM 時建立所有 NIC。</span><span class="sxs-lookup"><span data-stu-id="de2e1-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="de2e1-154">小心規劃您的部署，以確定您一開始就會有所有需要的網路連線。</span><span class="sxs-lookup"><span data-stu-id="de2e1-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

