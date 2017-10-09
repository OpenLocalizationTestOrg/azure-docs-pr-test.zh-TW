---
title: "aaaExpand 虛擬硬碟在 Azure 中的 Linux VM 上 |Microsoft 文件"
description: "了解如何 tooexpand 虛擬硬碟與 Linux VM 上 hello Azure CLI 2.0"
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
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="eb29f-103">如何 tooexpand 虛擬硬碟與 Linux VM 上 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb29f-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="eb29f-104">hello hello 作業系統 (OS) 的預設虛擬硬碟大小通常是 30 GB 在 Azure 中 Linux 虛擬機器 (VM) 上。</span><span class="sxs-lookup"><span data-stu-id="eb29f-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="eb29f-105">您可以[加入資料磁碟](add-disk.md)tooprovide 額外的儲存空間，但是您可能希望 tooexpand 的現有資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="eb29f-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="eb29f-106">這篇文章說明 tooexpand 針對 Linux VM 以 hello Azure CLI 2.0 所管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eb29f-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="eb29f-107">您也可以展開與 hello hello unmanaged OS 磁碟[Azure CLI 1.0](expand-disks-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="eb29f-108">在執行磁碟調整大小作業前，務必備份資料。</span><span class="sxs-lookup"><span data-stu-id="eb29f-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="eb29f-109">如需詳細資訊，請參閱[在 Azure 中備份 Linux 虛擬機器](tutorial-backup-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="eb29f-110">擴充磁碟</span><span class="sxs-lookup"><span data-stu-id="eb29f-110">Expand disk</span></span>
<span data-ttu-id="eb29f-111">請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="eb29f-112">本文需要 Azure 中存有一個虛擬機器，且該虛擬機器至少掛載一個已備妥使用的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="eb29f-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="eb29f-113">如果您還沒有可使用的虛擬機器，請參閱[建立並準備掛載有資料磁碟的虛擬機器](tutorial-manage-disks.md#create-and-attach-disks)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="eb29f-114">Hello 在下列範例中，會取代您自己的值範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="eb29f-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="eb29f-115">範例參數名稱包含 myResourceGroup 與 myVM。</span><span class="sxs-lookup"><span data-stu-id="eb29f-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="eb29f-116">虛擬硬碟上的作業無法執行以 hello VM 執行。</span><span class="sxs-lookup"><span data-stu-id="eb29f-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="eb29f-117">使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置您的 VM。</span><span class="sxs-lookup"><span data-stu-id="eb29f-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="eb29f-118">hello 下列範例會取消配置 hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="eb29f-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="eb29f-119">`az vm stop`不會釋放 hello 計算資源。</span><span class="sxs-lookup"><span data-stu-id="eb29f-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="eb29f-120">toorelease 計算資源，請使用`az vm deallocate`。</span><span class="sxs-lookup"><span data-stu-id="eb29f-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="eb29f-121">必須解除配置 hello VM tooexpand hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="eb29f-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="eb29f-122">使用 [az disk list](/cli/azure/disk#list) 來檢視資源群組中的受控磁碟清單。</span><span class="sxs-lookup"><span data-stu-id="eb29f-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="eb29f-123">hello 下列範例顯示的受管理的磁碟清單 hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="eb29f-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="eb29f-124">展開所需的磁碟 hello 與[az 磁碟更新](/cli/azure/disk#update)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="eb29f-125">hello 下列範例會展開 hello 受管理的磁碟，名為*myDataDisk* toobe *200*Gb 大小：</span><span class="sxs-lookup"><span data-stu-id="eb29f-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="eb29f-126">當您展開受管理的磁碟時，更新的 hello 大小會是對應的 toohello 最接近的受管理的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="eb29f-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="eb29f-127">Hello 受管理的可用磁碟大小與層級的資料表，請參閱[Azure 受管理磁碟概觀-定價和計費](../windows/managed-disks-overview.md#pricing-and-billing)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="eb29f-128">使用 [az vm create](/cli/azure/vm#start) 啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="eb29f-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="eb29f-129">下列範例開始 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="eb29f-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="eb29f-130">SSH tooyour VM 與 hello 適當的認證。</span><span class="sxs-lookup"><span data-stu-id="eb29f-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="eb29f-131">您可以取得具有您 VM 的 hello 公用 IP 位址[az vm 顯示](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="eb29f-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="eb29f-132">toouse hello 展開磁碟時，您需要 tooexpand hello 基礎磁碟分割及檔案系統。</span><span class="sxs-lookup"><span data-stu-id="eb29f-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="eb29f-133">a.</span><span class="sxs-lookup"><span data-stu-id="eb29f-133">a.</span></span> <span data-ttu-id="eb29f-134">如果已掛上，取消掛接 hello 磁碟：</span><span class="sxs-lookup"><span data-stu-id="eb29f-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="eb29f-135">b.</span><span class="sxs-lookup"><span data-stu-id="eb29f-135">b.</span></span> <span data-ttu-id="eb29f-136">使用`parted`tooview 磁碟資訊並調整大小 hello 磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="eb29f-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="eb29f-137">檢視與 hello 現有磁碟分割配置的相關資訊`print`。</span><span class="sxs-lookup"><span data-stu-id="eb29f-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="eb29f-138">hello 輸出類似 toohello 之後，範例中，會顯示 hello 基礎磁碟的大小是 215 Gb:</span><span class="sxs-lookup"><span data-stu-id="eb29f-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="eb29f-139">c.</span><span class="sxs-lookup"><span data-stu-id="eb29f-139">c.</span></span> <span data-ttu-id="eb29f-140">展開的資料分割 hello 和`resizepart`。</span><span class="sxs-lookup"><span data-stu-id="eb29f-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="eb29f-141">輸入 hello 分割區編號， *1*，和 hello 新資料分割的大小：</span><span class="sxs-lookup"><span data-stu-id="eb29f-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="eb29f-142">d.</span><span class="sxs-lookup"><span data-stu-id="eb29f-142">d.</span></span> <span data-ttu-id="eb29f-143">tooexit，輸入`quit`</span><span class="sxs-lookup"><span data-stu-id="eb29f-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="eb29f-144">Hello 調整大小的磁碟分割，以確認與 hello 分割區一致性`e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="eb29f-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="eb29f-145">現在調整與 hello filesystem `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="eb29f-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="eb29f-146">掛接 hello 分割 toohello 預期的位置，例如`/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="eb29f-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="eb29f-147">tooverify hello 作業系統磁碟大小已經過調整，請使用`df -h`。</span><span class="sxs-lookup"><span data-stu-id="eb29f-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="eb29f-148">下列範例輸出的 hello 顯示 hello 資料磁碟機， */開發/sdc1*，現在為 200 GB:</span><span class="sxs-lookup"><span data-stu-id="eb29f-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="eb29f-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb29f-149">Next steps</span></span>
<span data-ttu-id="eb29f-150">如果您需要額外的存放裝置，您也[新增資料磁碟 tooa Linux VM](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="eb29f-151">如需磁碟加密的詳細資訊，請參閱[使用 Linux VM 上的加密磁碟 hello Azure CLI](encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="eb29f-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
