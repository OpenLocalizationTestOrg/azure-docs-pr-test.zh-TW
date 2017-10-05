---
title: "在 Azure 中建立連接多個 NIC 的 Linux VM | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 或 Resource Manager 範本，來建立連結多個 NIC 的 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="caaad-103">如何在 Azure 中建立有多個網路介面卡的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="caaad-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="caaad-104">您可以在 Azure 中，建立連接多個虛擬網路介面 (NIC) 的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="caaad-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="caaad-105">常見案例是有不同的子網路可用於前端和後端連線，或者專門用來監視或備份解決方案的網路。</span><span class="sxs-lookup"><span data-stu-id="caaad-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="caaad-106">本文詳細說明如何建立連接多個 NIC 的 VM，以及如何在現有的 VM 中新增或移除 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="caaad-107">如需詳細資訊，包括如何在自己的 Bash 指令碼內建立多個 NIC，請深入了解 [部署多個 NIC 的 VM](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="caaad-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="caaad-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="caaad-109">本文詳述如何使用 Azure CLI 2.0 建立具有多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="caaad-110">您也可以使用 [Azure CLI 1.0](multiple-nics-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="caaad-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="caaad-111">建立支援資源</span><span class="sxs-lookup"><span data-stu-id="caaad-111">Create supporting resources</span></span>
<span data-ttu-id="caaad-112">請安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="caaad-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="caaad-113">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="caaad-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="caaad-114">範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。</span><span class="sxs-lookup"><span data-stu-id="caaad-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="caaad-115">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="caaad-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="caaad-116">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="caaad-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="caaad-117">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="caaad-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="caaad-118">下列範例會建立名為 myVnet 的虛擬網路和名為 mySubnetFrontEnd 的子網路：</span><span class="sxs-lookup"><span data-stu-id="caaad-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="caaad-119">使用 [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) 建立後端流量的子網路。</span><span class="sxs-lookup"><span data-stu-id="caaad-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="caaad-120">下列範例會建立名為 mySubnetBackEnd 的子網路：</span><span class="sxs-lookup"><span data-stu-id="caaad-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="caaad-121">使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="caaad-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="caaad-122">下列範例建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="caaad-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="caaad-123">建立及設定多個 NIC</span><span class="sxs-lookup"><span data-stu-id="caaad-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="caaad-124">使用 [az network nic create](/cli/azure/network/nic#create) 建立兩個 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="caaad-125">下列範例會建立兩個連接網路安全性群組的 NIC (名為 myNic1 和 myNic2)，以及一個連接到各個子網路的 NIC：</span><span class="sxs-lookup"><span data-stu-id="caaad-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="caaad-126">建立 VM 並附加 NIC</span><span class="sxs-lookup"><span data-stu-id="caaad-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="caaad-127">當您建立 VM 時，指定您使用 `--nics` 建立的 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="caaad-128">當您選取 VM 大小時也需多加注意。</span><span class="sxs-lookup"><span data-stu-id="caaad-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="caaad-129">您可以新增至 VM 的 NIC 總數是有限制的。</span><span class="sxs-lookup"><span data-stu-id="caaad-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="caaad-130">深入了解 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="caaad-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="caaad-131">使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="caaad-132">下列範例會建立名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="caaad-132">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="caaad-133">將 NIC 新增至 VM</span><span class="sxs-lookup"><span data-stu-id="caaad-133">Add a NIC to a VM</span></span>
<span data-ttu-id="caaad-134">先前的步驟建立了一個有多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="caaad-135">您也可以使用 Azure CLI 2.0 將 NIC 新增至現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="caaad-136">使用 [az network nic create](/cli/azure/network/nic#create) 建立另一個 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="caaad-137">下列範例會建立一個名為 myNic3 的 NIC，此 NIC會連線到後端子網路與在先前步驟中建立的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="caaad-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="caaad-138">若要將 NIC 新增至現有的 VM，請先使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="caaad-139">下列範例會解除配置名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="caaad-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="caaad-140">使用 [az vm nic add](/cli/azure/vm/nic#add) 新增 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="caaad-141">下列範例將 myNic3 新增至 myVM：</span><span class="sxs-lookup"><span data-stu-id="caaad-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="caaad-142">使用 [az vm start](/cli/azure/vm#start) 啟用 VM：</span><span class="sxs-lookup"><span data-stu-id="caaad-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="caaad-143">從 VM 中移除 NIC</span><span class="sxs-lookup"><span data-stu-id="caaad-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="caaad-144">若要將 NIC 從現有的 VM 中移除，請先使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="caaad-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="caaad-145">下列範例會解除配置名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="caaad-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="caaad-146">使用 [az vm nic remove](/cli/azure/vm/nic#remove) 移除 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="caaad-147">下列範例會將 myNic3 從 myVM 中移除：</span><span class="sxs-lookup"><span data-stu-id="caaad-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="caaad-148">使用 [az vm start](/cli/azure/vm#start) 啟用 VM：</span><span class="sxs-lookup"><span data-stu-id="caaad-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="caaad-149">使用 Resource Manager 範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="caaad-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="caaad-150">Azure Resource Manager 範本會使用宣告式 JSON 檔案來定義您的環境。</span><span class="sxs-lookup"><span data-stu-id="caaad-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="caaad-151">您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="caaad-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="caaad-152">Resource Manager 範本提供一種方式，可在部署期間建立資源的多個執行個體，例如建立多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="caaad-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="caaad-153">您使用 *copy* 來指定要建立的執行個體數目：</span><span class="sxs-lookup"><span data-stu-id="caaad-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="caaad-154">深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="caaad-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="caaad-155">您也可以使用 `copyIndex()`，然後在資源名稱後面附加一個數字，讓您能夠建立 `myNic1`、`myNic2`，依此類推。以下顯示附加索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="caaad-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="caaad-156">您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="caaad-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="caaad-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="caaad-157">Next steps</span></span>
<span data-ttu-id="caaad-158">當您嘗試建立一個有多個 NIC 的 VM 時，請檢閱 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="caaad-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="caaad-159">注意每個 VM 大小所支援的 NIC 數目上限。</span><span class="sxs-lookup"><span data-stu-id="caaad-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 