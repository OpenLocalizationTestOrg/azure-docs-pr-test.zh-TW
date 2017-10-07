---
title: "aaaCopy Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 toocreate Azure Linux VM 使用 Azure CLI 2.0 和管理磁碟的複本。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="b5fb0-103">使用 Azure CLI 2.0 和受控磁碟來建立 Azure Linux VM 的複本</span><span class="sxs-lookup"><span data-stu-id="b5fb0-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="b5fb0-104">本文章將示範如何 toocreate 一份您執行 Azure 虛擬機器 (VM) 使用 Linux hello Azure CLI 2.0 和 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="b5fb0-105">您也可以執行下列步驟以 hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b5fb0-106">您也可以[上傳 VHD 並從中建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5fb0-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b5fb0-107">Prerequisites</span></span>


-   <span data-ttu-id="b5fb0-108">安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="b5fb0-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="b5fb0-109">使用的 Azure 帳戶登入 tooan [az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="b5fb0-110">有 Azure VM toouse 為 hello 您複製的來源。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="b5fb0-111">步驟 1： 停止 hello 來源 VM</span><span class="sxs-lookup"><span data-stu-id="b5fb0-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="b5fb0-112">Deallocate hello 來源 VM 使用[az vm 解除配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="b5fb0-113">hello 下列範例會取消配置 hello 名為 VM **myVM** hello 資源群組中**myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b5fb0-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="b5fb0-114">步驟 2： 複製 hello 來源 VM</span><span class="sxs-lookup"><span data-stu-id="b5fb0-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="b5fb0-115">toocopy VM，您會建立一份 hello 基礎虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="b5fb0-116">此程序會建立特殊的 VHD 做為受管理的磁碟包含 hello 來源 VM 相同的組態和 hello 的設定。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="b5fb0-117">如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="b5fb0-118">列出每個 VM 和 hello 名稱含有其 OS 磁碟[az vm 清單](/cli/azure/vm#list)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="b5fb0-119">hello 下列範例會列出名為的資源群組中所有 Vm **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b5fb0-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="b5fb0-120">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="b5fb0-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="b5fb0-121">使用磁碟管理來建立新的複製 hello 磁碟[az 磁碟建立](/cli/azure/disk#create)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="b5fb0-122">hello 下列範例會建立名為的磁碟**myCopiedDisk** hello 從受管理磁碟名為**myDisk**:</span><span class="sxs-lookup"><span data-stu-id="b5fb0-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="b5fb0-123">使用確認正在資源群組中的受管理的 hello 磁碟[az 磁碟清單](/cli/azure/disk#list)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="b5fb0-124">hello 下列範例會列出名為 「 hello 資源群組中的受管理的 hello 磁碟**myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b5fb0-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="b5fb0-125">略過太[「 步驟 3： 設定虛擬網路 」](#step-3-set-up-a-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="b5fb0-126">步驟 3︰設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b5fb0-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="b5fb0-127">hello 下列選擇性步驟建立新的虛擬網路、 子網路、 公用 IP 位址，與虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="b5fb0-128">如果您複製 VM 疑難排解用途或其他部署，您可能不想 toouse 中現有的虛擬網路的 VM。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="b5fb0-129">如果您想要複製 Vm toocreate 虛擬網路基礎結構，後續 hello 接下來的幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="b5fb0-130">如果您不想 toocreate 虛擬網路，請略過太[步驟 4： 建立 VM](#step-4-create-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="b5fb0-131">使用建立虛擬網路的 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b5fb0-132">hello 下列範例會建立虛擬網路，名為**myVnet**和名為的子網路**mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="b5fb0-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="b5fb0-133">使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="b5fb0-134">hello 下列範例會建立名為公用 IP **myPublicIP** hello DNS 名稱是**mypublicdns**。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="b5fb0-135">（hello DNS 名稱必須是唯一的因此提供唯一的名稱。)</span><span class="sxs-lookup"><span data-stu-id="b5fb0-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="b5fb0-136">建立 hello NIC 使用[az 網路 nic 建立](/cli/azure/network/nic#create)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="b5fb0-137">hello 下列範例會建立名為的 NIC **myNic**的附加的 toothe **mySubnet**子網路：</span><span class="sxs-lookup"><span data-stu-id="b5fb0-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="b5fb0-138">步驟 4：建立 VM</span><span class="sxs-lookup"><span data-stu-id="b5fb0-138">Step 4: Create a VM</span></span>

<span data-ttu-id="b5fb0-139">您現在可以使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="b5fb0-140">指定 hello 複製為 hello OS 磁碟的受管理的磁碟 toouse (-附加 os 磁碟)，如下：</span><span class="sxs-lookup"><span data-stu-id="b5fb0-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="b5fb0-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5fb0-141">Next steps</span></span>

<span data-ttu-id="b5fb0-142">toolearn 如何 toouse Azure CLI toomanage 新的 VM，請參閱[hello Azure 資源管理員的 Azure CLI 命令](../azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="b5fb0-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
