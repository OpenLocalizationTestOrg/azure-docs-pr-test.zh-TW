---
title: "在具有多個 Nic 的 Azure Linux VM aaaCreate |Microsoft 文件"
description: "了解如何將 toocreate Linux VM 具有多個 Nic 附加 tooit 使用 hello Azure CLI 2.0 或資源管理員範本。"
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
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="1a025-103">如何 toocreate Azure 中 Linux 虛擬機器，與多個網路介面卡</span><span class="sxs-lookup"><span data-stu-id="1a025-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="1a025-104">您可以在具有多個虛擬網路介面 (Nic) 附加 tooit Azure 中建立虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="1a025-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="1a025-105">常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。</span><span class="sxs-lookup"><span data-stu-id="1a025-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="1a025-106">這篇文章說明如何 toocreate 具有多個 Nic VM 附加 tooit 以及如何從現有的 VM tooadd 或移除 Nic。</span><span class="sxs-lookup"><span data-stu-id="1a025-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="1a025-107">如需詳細資訊，包括如何 toocreate 內您自己的多個 Nic 撞指令碼，深入了解[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="1a025-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="1a025-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1a025-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="1a025-109">這篇文章說明具有使用多個 Nic VM 的 toocreate hello Azure CLI 2.0 的方式。</span><span class="sxs-lookup"><span data-stu-id="1a025-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="1a025-110">您也可以執行下列步驟以 hello [Azure CLI 1.0](multiple-nics-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="1a025-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="1a025-111">建立支援資源</span><span class="sxs-lookup"><span data-stu-id="1a025-111">Create supporting resources</span></span>
<span data-ttu-id="1a025-112">最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="1a025-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="1a025-113">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1a025-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1a025-114">範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。</span><span class="sxs-lookup"><span data-stu-id="1a025-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="1a025-115">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a025-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1a025-116">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="1a025-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1a025-117">建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。</span><span class="sxs-lookup"><span data-stu-id="1a025-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1a025-118">hello 下列範例會建立虛擬網路，名為*myVnet*和名為的子網路*mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="1a025-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="1a025-119">建立子網路與 hello 後端流量[az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)。</span><span class="sxs-lookup"><span data-stu-id="1a025-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="1a025-120">hello 下列範例會建立名為的子網路*mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="1a025-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="1a025-121">使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="1a025-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="1a025-122">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1a025-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="1a025-123">建立及設定多個 NIC</span><span class="sxs-lookup"><span data-stu-id="1a025-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="1a025-124">使用 [az network nic create](/cli/azure/network/nic#create) 建立兩個 NIC。</span><span class="sxs-lookup"><span data-stu-id="1a025-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1a025-125">hello 下列範例會建立兩個 Nic，名為*myNic1*和*myNic2*、 相互連結 hello 網路安全性群組，具有一個 NIC 連接 tooeach 子網路：</span><span class="sxs-lookup"><span data-stu-id="1a025-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

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

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="1a025-126">建立 VM，並且附加 hello Nic</span><span class="sxs-lookup"><span data-stu-id="1a025-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="1a025-127">當您建立指定 hello Nic hello VM，您建立與`--nics`。</span><span class="sxs-lookup"><span data-stu-id="1a025-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="1a025-128">您也需要 tootake 小心，當您選取 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="1a025-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="1a025-129">沒有限制，您可以加入 tooa VM 之 Nic 的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="1a025-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="1a025-130">深入了解 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="1a025-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="1a025-131">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1a025-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1a025-132">hello 下列範例會建立名為的 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1a025-132">hello following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="1a025-133">新增 NIC tooa VM</span><span class="sxs-lookup"><span data-stu-id="1a025-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="1a025-134">建立具有多個 Nic VM hello 的上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1a025-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="1a025-135">您也可以加入 Nic tooan hello Azure CLI 2.0 與現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="1a025-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="1a025-136">使用 [az network nic create](/cli/azure/network/nic#create) 建立另一個 NIC。</span><span class="sxs-lookup"><span data-stu-id="1a025-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1a025-137">hello 下列範例會建立名為的 NIC *myNic3* toohello 後端子網路與網路安全性群組 hello 前述步驟中建立連接：</span><span class="sxs-lookup"><span data-stu-id="1a025-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="1a025-138">tooadd NIC tooan 現有 VM，第一次解除配置 hello 與 VM [az vm 解除配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="1a025-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="1a025-139">hello 下列範例會取消配置 hello 名為 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1a025-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1a025-140">新增 hello 與 NIC [az vm nic 新增](/cli/azure/vm/nic#add)。</span><span class="sxs-lookup"><span data-stu-id="1a025-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="1a025-141">hello 下列範例會將*myNic3*太*myVM*:</span><span class="sxs-lookup"><span data-stu-id="1a025-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="1a025-142">啟動 hello 與 VM [az vm 啟動](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="1a025-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="1a025-143">從 VM 中移除 NIC</span><span class="sxs-lookup"><span data-stu-id="1a025-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="1a025-144">tooremove NIC，以從現有的 VM，第一次解除配置 hello VM 與[az vm 解除配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="1a025-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="1a025-145">hello 下列範例會取消配置 hello 名為 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1a025-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="1a025-146">移除 hello 與 NIC [az vm nic 移除](/cli/azure/vm/nic#remove)。</span><span class="sxs-lookup"><span data-stu-id="1a025-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="1a025-147">hello 下列範例會移除*myNic3*從*myVM*:</span><span class="sxs-lookup"><span data-stu-id="1a025-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="1a025-148">啟動 hello 與 VM [az vm 啟動](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="1a025-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="1a025-149">使用 Resource Manager 範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="1a025-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="1a025-150">Azure 資源管理員範本使用宣告式的 JSON 檔案 toodefine 環境。</span><span class="sxs-lookup"><span data-stu-id="1a025-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="1a025-151">您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1a025-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1a025-152">資源管理員範本提供方式 toocreate 資源的多個執行個體在部署期間，例如建立多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="1a025-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="1a025-153">您使用*複製*執行個體 toocreate toospecify hello 數目：</span><span class="sxs-lookup"><span data-stu-id="1a025-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="1a025-154">深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="1a025-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="1a025-155">您也可以使用`copyIndex()`toothen 附加數字 tooa 資源名稱，可讓您 toocreate `myNic1`， `myNic2`，等 hello 下列範例示範附加 hello 索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="1a025-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="1a025-156">您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="1a025-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a025-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a025-157">Next steps</span></span>
<span data-ttu-id="1a025-158">檢閱[Linux VM 大小](sizes.md)toocreating 具有多個 Nic 的 VM 時。</span><span class="sxs-lookup"><span data-stu-id="1a025-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="1a025-159">請注意 toohello 最大的 Nic 數目在支援每個 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="1a025-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
