---
title: "使用 Azure CLI 2.0 來複製 Linux VM | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 和受控磁碟來建立 Azure Linux VM 的複本。"
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
ms.openlocfilehash: 7983061a933370803669480296d7625106e1360c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="264a0-103">使用 Azure CLI 2.0 和受控磁碟來建立 Azure Linux VM 的複本</span><span class="sxs-lookup"><span data-stu-id="264a0-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="264a0-104">本文說明如何使用 Azure CLI 2.0 和 Azure Resource Manager 部署模型，建立執行 Linux 之 Azure 虛擬機器 (VM) 的複本。</span><span class="sxs-lookup"><span data-stu-id="264a0-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="264a0-105">您也可以使用 [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="264a0-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="264a0-106">您也可以[上傳 VHD 並從中建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="264a0-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="264a0-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="264a0-107">Prerequisites</span></span>


-   <span data-ttu-id="264a0-108">安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="264a0-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="264a0-109">使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="264a0-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="264a0-110">讓 Azure VM 做為複製的來源。</span><span class="sxs-lookup"><span data-stu-id="264a0-110">Have an Azure VM to use as the source for your copy.</span></span>

## <a name="step-1-stop-the-source-vm"></a><span data-ttu-id="264a0-111">步驟 1︰停止來源 VM</span><span class="sxs-lookup"><span data-stu-id="264a0-111">Step 1: Stop the source VM</span></span>


<span data-ttu-id="264a0-112">使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置來源 VM。</span><span class="sxs-lookup"><span data-stu-id="264a0-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="264a0-113">下列範例會解除配置 **myResourceGroup** 資源群組中名為 **myVM** 的 VM：</span><span class="sxs-lookup"><span data-stu-id="264a0-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-the-source-vm"></a><span data-ttu-id="264a0-114">步驟 2︰複製來源 VM</span><span class="sxs-lookup"><span data-stu-id="264a0-114">Step 2: Copy the source VM</span></span>


<span data-ttu-id="264a0-115">若要複製 VM，您可建立基礎虛擬硬碟的複本。</span><span class="sxs-lookup"><span data-stu-id="264a0-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span></span> <span data-ttu-id="264a0-116">此程序會建立特製化 VHD 做為受控磁碟，其包含與來源 VM 相同的組態和設定。</span><span class="sxs-lookup"><span data-stu-id="264a0-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span></span>

<span data-ttu-id="264a0-117">如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="264a0-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="264a0-118">使用 [az vm list](/cli/azure/vm#list) 列出每部 VM 及其 OS 磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="264a0-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="264a0-119">下列範例會列出名為 **myResourceGroup** 的資源群組中的所有 VM：</span><span class="sxs-lookup"><span data-stu-id="264a0-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="264a0-120">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="264a0-120">The output is similar to the following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="264a0-121">使用 [az disk create](/cli/azure/disk#create) 建立新的受控磁碟，進而複製磁碟。</span><span class="sxs-lookup"><span data-stu-id="264a0-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="264a0-122">下列範例會從名為 **myDisk** 的受控磁碟建立名為 **myCopiedDisk** 的磁碟：</span><span class="sxs-lookup"><span data-stu-id="264a0-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="264a0-123">使用 [az disk list](/cli/azure/disk#list) 來確認此受控磁碟現在位於您的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="264a0-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="264a0-124">下列範例會列出名為 **myResourceGroup** 的資源群組中的受控磁碟：</span><span class="sxs-lookup"><span data-stu-id="264a0-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="264a0-125">跳至[步驟 3︰設定虛擬網路](#step-3-set-up-a-virtual-network)。</span><span class="sxs-lookup"><span data-stu-id="264a0-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="264a0-126">步驟 3︰設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="264a0-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="264a0-127">下列選擇性步驟會建立新的虛擬網路、子網路、公用 IP 位址和虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="264a0-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="264a0-128">如果您為了進行疑難排解或其他部署而複製 VM，您可能不想使用現有虛擬網路中的 VM。</span><span class="sxs-lookup"><span data-stu-id="264a0-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span></span>

<span data-ttu-id="264a0-129">如果您想為所複製的 VM 建立虛擬網路基礎結構，請遵循接下來的幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="264a0-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span></span> <span data-ttu-id="264a0-130">如果不想建立虛擬網路，請跳至[步驟 4：建立 VM](#step-4-create-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="264a0-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="264a0-131">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="264a0-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="264a0-132">下列範例會建立名為 **myVnet** 的虛擬網路和名為 **mySubnet** 的子網路：</span><span class="sxs-lookup"><span data-stu-id="264a0-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="264a0-133">使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP。</span><span class="sxs-lookup"><span data-stu-id="264a0-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="264a0-134">下列範例會建立名為 **myPublicIP** 的公用 IP，其 DNS 名稱為 **mypublicdns**。</span><span class="sxs-lookup"><span data-stu-id="264a0-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span></span> <span data-ttu-id="264a0-135">(DNS 名稱必須是唯一的，因此請提供唯一的名稱。)</span><span class="sxs-lookup"><span data-stu-id="264a0-135">(The DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="264a0-136">使用 [az network nic create](/cli/azure/network/nic#create) 來建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="264a0-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="264a0-137">下列範例會建立連結至 **mySubnet** 子網路且名為 **myNic** 的 NIC：</span><span class="sxs-lookup"><span data-stu-id="264a0-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="264a0-138">步驟 4：建立 VM</span><span class="sxs-lookup"><span data-stu-id="264a0-138">Step 4: Create a VM</span></span>

<span data-ttu-id="264a0-139">您現在可以使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="264a0-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="264a0-140">指定要做為 OS 磁碟的所複製受控磁碟 (--attach-os-disk)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="264a0-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="264a0-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="264a0-141">Next steps</span></span>

<span data-ttu-id="264a0-142">若要了解如何使用 Azure CLI 來管理新的 VM，請參閱 [Azure Resource Manager 的 Azure CLI 命令](../azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="264a0-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
