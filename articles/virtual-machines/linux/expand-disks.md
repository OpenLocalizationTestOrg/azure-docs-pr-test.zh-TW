---
title: "在 Azure 中擴充 Linux VM 上的虛擬硬碟 | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 擴充 Linux VM 上的虛擬硬碟"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="199ce-103">如何使用 Azure CLI 擴充 Linux VM 上的虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="199ce-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="199ce-104">在 Azure 中，Linux 虛擬機器 (VM) 上作業系統 (OS) 的預設虛擬硬碟大小通常是 30 GB。</span><span class="sxs-lookup"><span data-stu-id="199ce-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="199ce-105">您可以[新增資料磁碟](add-disk.md)來提供更多儲存空間，但您也可能想要擴充既有的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="199ce-106">本文將詳細說明如何使用 Azure CLI 2.0 來擴充 Linux VM 的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="199ce-107">您也可以使用 [Azure CLI 1.0](expand-disks-nodejs.md) 來擴充非受控的 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="199ce-108">在執行磁碟調整大小作業前，務必備份資料。</span><span class="sxs-lookup"><span data-stu-id="199ce-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="199ce-109">如需詳細資訊，請參閱[在 Azure 中備份 Linux 虛擬機器](tutorial-backup-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="199ce-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="199ce-110">擴充磁碟</span><span class="sxs-lookup"><span data-stu-id="199ce-110">Expand disk</span></span>
<span data-ttu-id="199ce-111">請確定您已安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="199ce-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="199ce-112">本文需要 Azure 中存有一個虛擬機器，且該虛擬機器至少掛載一個已備妥使用的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="199ce-113">如果您還沒有可使用的虛擬機器，請參閱[建立並準備掛載有資料磁碟的虛擬機器](tutorial-manage-disks.md#create-and-attach-disks)。</span><span class="sxs-lookup"><span data-stu-id="199ce-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="199ce-114">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="199ce-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="199ce-115">範例參數名稱包含 myResourceGroup 與 myVM。</span><span class="sxs-lookup"><span data-stu-id="199ce-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="199ce-116">當 VM 正在執行時，無法對虛擬硬碟執行作業。</span><span class="sxs-lookup"><span data-stu-id="199ce-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="199ce-117">使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置您的 VM。</span><span class="sxs-lookup"><span data-stu-id="199ce-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="199ce-118">下列範例會解除配置名為 myResourceGroup 資源群組中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="199ce-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="199ce-119">`az vm stop` 不會釋放計算資源。</span><span class="sxs-lookup"><span data-stu-id="199ce-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="199ce-120">若要釋放計算資源，請使用 `az vm deallocate`。</span><span class="sxs-lookup"><span data-stu-id="199ce-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="199ce-121">必須解除配置 VM，才能擴充虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="199ce-122">使用 [az disk list](/cli/azure/disk#list) 來檢視資源群組中的受控磁碟清單。</span><span class="sxs-lookup"><span data-stu-id="199ce-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="199ce-123">下列範例會顯示名為 myResourceGroup 之資源群組中的受控磁碟清單：</span><span class="sxs-lookup"><span data-stu-id="199ce-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="199ce-124">使用 [az disk update](/cli/azure/disk#update) 擴充所需的磁碟。</span><span class="sxs-lookup"><span data-stu-id="199ce-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="199ce-125">下列範例會將名為 myDataDisk 的受控磁碟大小擴充為 200 GB：</span><span class="sxs-lookup"><span data-stu-id="199ce-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="199ce-126">當您擴充受控磁碟時，更新的大小會對應至最接近的受控磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="199ce-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="199ce-127">如需可用受控磁碟大小和階層的表格，請參閱 [Azure 受控磁碟概觀 - 價格和計費](../windows/managed-disks-overview.md#pricing-and-billing)。</span><span class="sxs-lookup"><span data-stu-id="199ce-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="199ce-128">使用 [az vm create](/cli/azure/vm#start) 啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="199ce-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="199ce-129">下列範例會啟動名為 myResourceGroup 資源群組中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="199ce-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="199ce-130">使用適當的認證以 SSH 登入 VM。</span><span class="sxs-lookup"><span data-stu-id="199ce-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="199ce-131">您可以使用 [az vm show](/cli/azure/vm#show) 取得虛擬機器的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="199ce-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="199ce-132">若要使用展開的硬碟，您需要展開硬碟下的分割區與檔案系統。</span><span class="sxs-lookup"><span data-stu-id="199ce-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="199ce-133">a.</span><span class="sxs-lookup"><span data-stu-id="199ce-133">a.</span></span> <span data-ttu-id="199ce-134">若磁碟已掛載，則卸載磁碟：</span><span class="sxs-lookup"><span data-stu-id="199ce-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="199ce-135">b.</span><span class="sxs-lookup"><span data-stu-id="199ce-135">b.</span></span> <span data-ttu-id="199ce-136">使用 `parted` 來檢視磁碟資訊與調整分割區大小：</span><span class="sxs-lookup"><span data-stu-id="199ce-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="199ce-137">使用 `print` 來檢視既有磁碟分割配置的資訊。</span><span class="sxs-lookup"><span data-stu-id="199ce-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="199ce-138">輸出結果會類似於以下範例，範例中顯示分割區下的磁碟大小為 215 Gb：</span><span class="sxs-lookup"><span data-stu-id="199ce-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="199ce-139">c.</span><span class="sxs-lookup"><span data-stu-id="199ce-139">c.</span></span> <span data-ttu-id="199ce-140">使用 `resizepart` 來展開分割區。</span><span class="sxs-lookup"><span data-stu-id="199ce-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="199ce-141">輸入分割區編號 *1* 以及新分割區的大小：</span><span class="sxs-lookup"><span data-stu-id="199ce-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="199ce-142">d.</span><span class="sxs-lookup"><span data-stu-id="199ce-142">d.</span></span> <span data-ttu-id="199ce-143">若要結束，請輸入 `quit`</span><span class="sxs-lookup"><span data-stu-id="199ce-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="199ce-144">分割區調整大小後，使用 `e2fsck` 來確認分割區的一致性：</span><span class="sxs-lookup"><span data-stu-id="199ce-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="199ce-145">使用 `resize2fs` 來調整檔案系統大小：</span><span class="sxs-lookup"><span data-stu-id="199ce-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="199ce-146">將分割區掛載至所需位置，像是 `/datadrive`：</span><span class="sxs-lookup"><span data-stu-id="199ce-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="199ce-147">若要確認 OS 磁碟已調整大小，請使用 `df -h`。</span><span class="sxs-lookup"><span data-stu-id="199ce-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="199ce-148">下列輸出範例顯示資料磁碟 (*/dev/sdc1*) 現在是 200 GB：</span><span class="sxs-lookup"><span data-stu-id="199ce-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="199ce-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="199ce-149">Next steps</span></span>
<span data-ttu-id="199ce-150">如果您需要更多儲存空間，您也可以[將資料磁碟新增至 Linux VM](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="199ce-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="199ce-151">如需磁碟加密的詳細資訊，請參閱[使用 Azure CLI 將 Linux VM 上的磁碟加密](encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="199ce-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
