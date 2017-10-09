---
title: "Linux VM 上以 hello Azure CLI 1.0 的 aaaExpand OS 磁碟 |Microsoft 文件"
description: "了解如何 tooexpand hello 作業系統 (OS) 上使用 Azure CLI 1.0 hello 和 hello Resource Manager 部署模型的 Linux VM 的虛擬磁碟"
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
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="c9441-103">展開 hello Azure CLI 1.0 搭配使用 Azure CLI hello Linux VM 上的作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="c9441-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="c9441-104">hello hello 作業系統 (OS) 的預設虛擬硬碟大小通常是 30 GB 在 Azure 中 Linux 虛擬機器 (VM) 上。</span><span class="sxs-lookup"><span data-stu-id="c9441-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="c9441-105">您可以[加入資料磁碟](add-disk.md)tooprovide 額外的儲存空間，但是您也可以 tooexpand hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="c9441-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="c9441-106">這篇文章說明如何 tooexpand hello OS 磁碟針對 Linux VM 以 hello Azure CLI 1.0 中使用未受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c9441-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c9441-107">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="c9441-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="c9441-108">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="c9441-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c9441-109">[Azure CLI 1.0](#prerequisites) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="c9441-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c9441-110">[Azure CLI 2.0](expand-disks.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="c9441-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9441-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c9441-111">Prerequisites</span></span>
<span data-ttu-id="c9441-112">您需要 hello[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)安裝並登入 tooan [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)，如下所示使用 hello Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="c9441-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c9441-113">Hello 在下列範例中，會取代您自己的值範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="c9441-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c9441-114">範例參數名稱包含 myResourceGroup 與 myVM。</span><span class="sxs-lookup"><span data-stu-id="c9441-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="c9441-115">擴充 OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="c9441-115">Expand OS disk</span></span>

1. <span data-ttu-id="c9441-116">虛擬硬碟上的作業無法執行以 hello VM 執行。</span><span class="sxs-lookup"><span data-stu-id="c9441-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="c9441-117">hello 下列範例會停止並取消配置 hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c9441-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="c9441-118">`azure vm stop`不會釋放 hello 計算資源。</span><span class="sxs-lookup"><span data-stu-id="c9441-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="c9441-119">toorelease 計算資源，請使用`azure vm deallocate`。</span><span class="sxs-lookup"><span data-stu-id="c9441-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="c9441-120">必須解除配置 hello VM tooexpand hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="c9441-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="c9441-121">更新不受管理的 hello OS 磁碟使用 hello hello 大小`azure vm set`命令。</span><span class="sxs-lookup"><span data-stu-id="c9441-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="c9441-122">下列範例會更新 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="c9441-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="c9441-123">啟動您的 VM，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c9441-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="c9441-124">SSH tooyour VM 與 hello 適當的認證。</span><span class="sxs-lookup"><span data-stu-id="c9441-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="c9441-125">tooverify hello 作業系統磁碟大小已經過調整，請使用`df -h`。</span><span class="sxs-lookup"><span data-stu-id="c9441-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="c9441-126">下列範例輸出的 hello 顯示 hello 主要磁碟分割 (*/開發/sda1*) 現在是 50 GB:</span><span class="sxs-lookup"><span data-stu-id="c9441-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="c9441-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9441-127">Next steps</span></span>
<span data-ttu-id="c9441-128">如果您需要額外的存放裝置，您也[新增資料磁碟 tooa Linux VM](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="c9441-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="c9441-129">如需磁碟加密的詳細資訊，請參閱[使用 Linux VM 上的加密磁碟 hello Azure CLI](encrypt-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="c9441-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
