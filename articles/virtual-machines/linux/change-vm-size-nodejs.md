---
title: "如何使用 Azure CLI 1.0 重新調整 Linux VM 的大小 | Microsoft Docs"
description: "如何藉由變更 VM 的大小來相應增加或相應減少 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 72f5a3cd6463befd5108040ed166984281bfc5f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="0154a-103">使用 Azure CLI 1.0 來調整 Linux VM 大小</span><span class="sxs-lookup"><span data-stu-id="0154a-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="0154a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0154a-104">Overview</span></span>

<span data-ttu-id="0154a-105">部屬虛擬機器 (VM) 之後，您可以藉由變更 [VM 大小][vm-sizes]來相應增加或減少 VM。</span><span class="sxs-lookup"><span data-stu-id="0154a-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="0154a-106">在某些情況下，您必須先解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="0154a-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="0154a-107">如果新的大小無法在裝載 VM 的硬體叢集上取得，可能有這樣的情況。</span><span class="sxs-lookup"><span data-stu-id="0154a-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="0154a-108">本文說明如何使用 [Azure CLI][azure-cli] 重新調整 Linux VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="0154a-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0154a-109">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="0154a-109">CLI versions to complete the task</span></span>
<span data-ttu-id="0154a-110">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="0154a-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="0154a-111">[Azure CLI 1.0](#resize-a-linux-vm) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="0154a-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0154a-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="0154a-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="0154a-113">重新調整 Linux VM 的大小</span><span class="sxs-lookup"><span data-stu-id="0154a-113">Resize a Linux VM</span></span>
<span data-ttu-id="0154a-114">若要重新調整 VM 的大小，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="0154a-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="0154a-115">執行下列 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="0154a-115">Run the following CLI command.</span></span> <span data-ttu-id="0154a-116">這個命令會列出裝載 VM 的硬體叢集上的可用 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="0154a-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="0154a-117">如果有列出所需的大小，請執行以下命令來調整 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="0154a-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="0154a-118">在此程序中 VM 會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0154a-118">The VM will restart during this process.</span></span> <span data-ttu-id="0154a-119">重新啟動之後，您現有的作業系統和資料磁碟將會重新對應。</span><span class="sxs-lookup"><span data-stu-id="0154a-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="0154a-120">暫存磁碟的所有項目將會遺失。</span><span class="sxs-lookup"><span data-stu-id="0154a-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="0154a-121">使用 `--enable-boot-diagnostics` 選項可讓[開機診斷][boot-diagnostics]記錄任何與啟動相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0154a-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="0154a-122">另一方面，如果沒有列出所需的大小，請執行以下命令以將 VM 解除配置、重新調整大小，然後再將它重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0154a-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="0154a-123">將 VM 解除配置也會釋出指派給該 VM 的任何動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0154a-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="0154a-124">不會影響作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0154a-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="0154a-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0154a-125">Next steps</span></span>
<span data-ttu-id="0154a-126">如需提高延展性，可執行多個 VM 執行個體並相應放大。</span><span class="sxs-lookup"><span data-stu-id="0154a-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="0154a-127">如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整 Linux 機器][scale-set]。</span><span class="sxs-lookup"><span data-stu-id="0154a-127">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
