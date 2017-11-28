---
title: "使用 Azure CLI 1.0 擴充 Linux VM 上的 OS 磁碟 | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 和 Resource Manager 部署模型，來擴充 Linux VM 上的作業系統 (OS) 虛擬磁碟"
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
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="1f9a7-103">透過 Azure CLI 1.0 使用 Azure CLI 擴充 Linux VM 上的 OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="1f9a7-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="1f9a7-104">在 Azure 中，Linux 虛擬機器 (VM) 上作業系統 (OS) 的預設虛擬硬碟大小通常是 30 GB。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="1f9a7-105">您可以[新增資料磁碟](add-disk.md)，以提供更多儲存空間，但您也可能想要擴充 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="1f9a7-106">本文將詳細說明如何搭配使用非受控磁碟與 Azure CLI 1.0，來擴充 Linux VM 的 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1f9a7-107">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="1f9a7-107">CLI versions to complete the task</span></span>
<span data-ttu-id="1f9a7-108">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="1f9a7-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1f9a7-109">[Azure CLI 1.0](#prerequisites) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="1f9a7-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1f9a7-110">[Azure CLI 2.0](expand-disks.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="1f9a7-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f9a7-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="1f9a7-111">Prerequisites</span></span>
<span data-ttu-id="1f9a7-112">您需要安裝[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)，而且已使用 Resource Manager 模式登入 [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1f9a7-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1f9a7-113">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1f9a7-114">範例參數名稱包含 myResourceGroup 與 myVM。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="1f9a7-115">擴充 OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="1f9a7-115">Expand OS disk</span></span>

1. <span data-ttu-id="1f9a7-116">當 VM 正在執行時，無法對虛擬硬碟執行作業。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="1f9a7-117">下列範例會停止並解除配置名為 myResourceGroup 的資源群組中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="1f9a7-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="1f9a7-118">`azure vm stop` 不會釋放計算資源。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="1f9a7-119">若要釋放計算資源，請使用 `azure vm deallocate`。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="1f9a7-120">必須解除配置 VM，才能擴充虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="1f9a7-121">使用 `azure vm set` 命令來更新非受控 OS 磁碟的大小。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="1f9a7-122">下列範例會將名為 myResourceGroup 的資源群組中名為 myVM 的 VM 更新為 50 GB：</span><span class="sxs-lookup"><span data-stu-id="1f9a7-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="1f9a7-123">啟動您的 VM，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1f9a7-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="1f9a7-124">使用適當的認證以 SSH 登入 VM。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="1f9a7-125">若要確認 OS 磁碟已調整大小，請使用 `df -h`。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="1f9a7-126">下列範例輸出顯示主要磁碟分割 (/dev/sda1) 現在是 50 GB：</span><span class="sxs-lookup"><span data-stu-id="1f9a7-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="1f9a7-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f9a7-127">Next steps</span></span>
<span data-ttu-id="1f9a7-128">如果您需要更多儲存空間，您也可以[將資料磁碟新增至 Linux VM](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="1f9a7-129">如需磁碟加密的詳細資訊，請參閱[使用 Azure CLI 將 Linux VM 上的磁碟加密](encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="1f9a7-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
