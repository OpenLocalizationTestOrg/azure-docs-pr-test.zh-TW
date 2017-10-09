---
title: "aaaHow tooresize Linux VM 以 hello Azure CLI 1.0 |Microsoft 文件"
description: "如何 tooscale 向上或向下 Linux 虛擬機器，藉由變更調整 hello VM 大小。"
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
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="098d4-103">使用 Azure CLI 1.0 來調整 Linux VM 大小</span><span class="sxs-lookup"><span data-stu-id="098d4-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="098d4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="098d4-104">Overview</span></span>

<span data-ttu-id="098d4-105">佈建虛擬機器 (VM) 之後，您可以調整 hello VM 向上或向下藉由變更 hello [VM 大小][vm-sizes]。</span><span class="sxs-lookup"><span data-stu-id="098d4-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="098d4-106">在某些情況下，您必須先取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="098d4-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="098d4-107">這種情況 hello 新大小不是在裝載 hello VM hello 硬體叢集上使用。</span><span class="sxs-lookup"><span data-stu-id="098d4-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="098d4-108">本文將說明如何使用 hello Linux VM 的 tooresize [Azure CLI][azure-cli]。</span><span class="sxs-lookup"><span data-stu-id="098d4-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="098d4-109">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="098d4-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="098d4-110">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="098d4-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="098d4-111">[Azure CLI 1.0](#resize-a-linux-vm) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="098d4-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="098d4-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="098d4-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="098d4-113">重新調整 Linux VM 的大小</span><span class="sxs-lookup"><span data-stu-id="098d4-113">Resize a Linux VM</span></span>
<span data-ttu-id="098d4-114">tooresize VM，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="098d4-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="098d4-115">執行下列 CLI 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="098d4-115">Run hello following CLI command.</span></span> <span data-ttu-id="098d4-116">此命令會列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="098d4-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="098d4-117">如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="098d4-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="098d4-118">hello VM 會重新啟動此程序期間。</span><span class="sxs-lookup"><span data-stu-id="098d4-118">hello VM will restart during this process.</span></span> <span data-ttu-id="098d4-119">Hello 重新啟動之後，您現有的作業系統和資料磁碟將會重新對應。</span><span class="sxs-lookup"><span data-stu-id="098d4-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="098d4-120">Hello 暫存磁碟的任何項目將會遺失。</span><span class="sxs-lookup"><span data-stu-id="098d4-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="098d4-121">使用 hello`--enable-boot-diagnostics`選項可讓[開機診斷][boot-diagnostics]，toolog 任何錯誤的相關的 toostartup。</span><span class="sxs-lookup"><span data-stu-id="098d4-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="098d4-122">否則，視 hello 大小未列出，執行下列命令 toodeallocate hello VM、 調整其大小，然後再重新啟動 hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="098d4-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="098d4-123">解除配置 hello VM 也會釋放指派 toohello VM 的任何動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="098d4-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="098d4-124">不會影響 hello OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="098d4-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="098d4-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="098d4-125">Next steps</span></span>
<span data-ttu-id="098d4-126">如需提高延展性，可執行多個 VM 執行個體並相應放大。如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整 Linux 機器][scale-set]。</span><span class="sxs-lookup"><span data-stu-id="098d4-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
