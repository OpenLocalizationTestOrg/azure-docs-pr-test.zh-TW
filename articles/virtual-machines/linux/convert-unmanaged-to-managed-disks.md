---
title: "在 Azure 中 Linux 虛擬機器，從 unmanaged aaaConvert 磁碟 toomanaged 磁碟-Azure 受管理磁碟 |Microsoft 文件"
description: "Tooconvert unmanaged 的磁碟 toomanaged 從 Linux VM 磁碟 hello Resource Manager 部署模型中使用 Azure CLI 2.0 的方式"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="9cee5-103">從 unmanaged 的磁碟 toomanaged 磁碟轉換 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9cee5-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="9cee5-104">如果您有現有 Linux 虛擬機器 (Vm)，並且使用未受管理的磁碟，您可以將透過 hello hello Vm toouse 管理磁碟轉換[Azure 受管理磁碟](../windows/managed-disks-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="9cee5-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="9cee5-105">此程序轉換 hello OS 磁碟和任何連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9cee5-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="9cee5-106">本文章將示範如何使用 tooconvert Vm hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="9cee5-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="9cee5-107">如果您需要 tooinstall，或將它升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="9cee5-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="9cee5-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="9cee5-109">轉換單一執行個體 VM</span><span class="sxs-lookup"><span data-stu-id="9cee5-109">Convert single-instance VMs</span></span>
<span data-ttu-id="9cee5-110">本章節涵蓋 tooconvert 單一執行個體中未受管理的 Azure Vm 磁碟 toomanaged 磁碟的方式。</span><span class="sxs-lookup"><span data-stu-id="9cee5-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="9cee5-111">（如果您的 Vm 可用性設定組中，請參閱 hello 下一節）。您可以使用此程序 tooconvert hello Vm 從高階 (SSD) 不受管理磁碟 toopremium 管理磁碟，或從標準 (HDD) 不受管理磁碟 toostandard 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="9cee5-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="9cee5-112">使用解除配置 hello VM [az vm 解除配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="9cee5-113">hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9cee5-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="9cee5-114">使用轉換 hello VM toomanaged 磁碟[az vm 轉換](/cli/azure/vm#convert)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="9cee5-115">下列程序會將轉換的 hello hello 名為 VM `myVM`，包括 hello OS 磁碟和任何資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="9cee5-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="9cee5-116">使用 hello 轉換 toomanaged 磁碟後啟動 hello VM [az vm 啟動](/cli/azure/vm#start)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="9cee5-117">下列範例開始 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="9cee5-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="9cee5-118">轉換可用性設定組中的 VM</span><span class="sxs-lookup"><span data-stu-id="9cee5-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="9cee5-119">如果您想要 tooconvert toomanaged 磁碟都在可用性設定組中的 hello Vm，您必須先管理 tooconvert hello 可用性集 tooa 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9cee5-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="9cee5-120">在轉換 hello 可用性設定組之前，必須取消配置 hello 可用性設定組中的所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="9cee5-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="9cee5-121">計劃 tooconvert hello 可用性之後的所有 Vm toomanaged 磁碟都設定本身已受管理的轉換的 tooa 可用性設定都組。</span><span class="sxs-lookup"><span data-stu-id="9cee5-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="9cee5-122">然後，啟動所有 hello Vm，並持續正常運作。</span><span class="sxs-lookup"><span data-stu-id="9cee5-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="9cee5-123">使用 [az vm availability-set list](/cli/azure/vm/availability-set#list) 來列出可用性設定組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="9cee5-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="9cee5-124">hello 下列範例會列出所有 Vm hello 可用性設定組具名`myAvailabilitySet`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9cee5-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="9cee5-125">解除配置使用的所有 hello Vm [az vm 解除都配置](/cli/azure/vm#deallocate)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="9cee5-126">hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9cee5-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="9cee5-127">轉換 hello 可用性設定組使用[az vm 的可用性設定組轉換](/cli/azure/vm/availability-set#convert)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="9cee5-128">hello 下列範例會將轉換 hello 可用性設定組具名`myAvailabilitySet`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9cee5-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="9cee5-129">使用轉換所有 hello Vm toomanaged 磁碟[az vm 都轉換](/cli/azure/vm#convert)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="9cee5-130">下列程序會將轉換的 hello hello 名為 VM `myVM`，包括 hello OS 磁碟和任何資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="9cee5-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="9cee5-131">啟動所有 hello Vm hello 轉換 toomanaged 磁碟之後，使用[az vm 都啟動](/cli/azure/vm#start)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="9cee5-132">下列範例開始 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9cee5-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="9cee5-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cee5-133">Next steps</span></span>
<span data-ttu-id="9cee5-134">如需儲存體選項的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9cee5-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
