---
title: "將 Azure 中的 Linux 虛擬機器從非受控磁碟轉換成受控磁碟 - Azure 受控磁碟 | Microsoft Docs"
description: "如何在 Resource Manager 部署模型中使用 Azure CLI 2.0 將 Linux VM 從非受控磁碟轉換成受控磁碟"
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
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="f4a7e-103">將 Linux 虛擬機器從非受控磁碟轉換成受控磁碟</span><span class="sxs-lookup"><span data-stu-id="f4a7e-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="f4a7e-104">如果現有的 Linux 虛擬機器 (VM) 使用非受控磁碟，您可以透過 [Azure 受控磁碟](../windows/managed-disks-overview.md)服務，將這些 VM 轉換成使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="f4a7e-105">此程序會轉換 OS 磁碟和任何附加的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="f4a7e-106">本文說明如何使用 Azure CLI 來轉換 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="f4a7e-107">如果您需要安裝或升級 Azure CLI，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f4a7e-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="f4a7e-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="f4a7e-109">轉換單一執行個體 VM</span><span class="sxs-lookup"><span data-stu-id="f4a7e-109">Convert single-instance VMs</span></span>
<span data-ttu-id="f4a7e-110">本節說明如何將單一執行個體 Azure VM 從非受控磁碟轉換為受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="f4a7e-111">(如果您的 VM 位於可用性設定組中，請參閱下一節)。您可以使用此程序將 VM 從進階 (SSD) 非受控磁碟轉換成進階受控磁碟，或從標準 (HDD) 非受控磁碟轉換成標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="f4a7e-112">使用 [az vm deallocate](/cli/azure/vm#deallocate) 將 VM 解除配置。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="f4a7e-113">下列範例會解除配置 `myResourceGroup` 資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="f4a7e-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="f4a7e-114">使用 [az vm convert](/cli/azure/vm#convert) 將 VM 轉換成受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="f4a7e-115">下列程序會轉換名為 `myVM` 的 VM，包括 OS 磁碟和任何資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="f4a7e-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="f4a7e-116">轉換成受控磁碟之後，使用 [az vm start](/cli/azure/vm#start) 來啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="f4a7e-117">下列範例會啟動 `myResourceGroup` 資源群組中名為 `myVM` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="f4a7e-118">轉換可用性設定組中的 VM</span><span class="sxs-lookup"><span data-stu-id="f4a7e-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="f4a7e-119">如果您想要轉換為受控磁碟的 VM 位於可用性設定組中，您必須先將此可用性設定組轉換為受控可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="f4a7e-120">轉換可用性設定組之前，必須先解除配置可用性設定組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="f4a7e-121">在可用性設定組本身轉換成受控可用性設定組之後，請規劃將所有 VM 轉換成受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="f4a7e-122">然後，啟動所有 VM 並繼續像平常一樣運作。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="f4a7e-123">使用 [az vm availability-set list](/cli/azure/vm/availability-set#list) 來列出可用性設定組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="f4a7e-124">下列範例會列出 `myResourceGroup` 資源群組中名為 `myAvailabilitySet` 的可用性設定組中的所有 VM：</span><span class="sxs-lookup"><span data-stu-id="f4a7e-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="f4a7e-125">使用 [az vm deallocate](/cli/azure/vm#deallocate) 將所有 VM 解除配置。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="f4a7e-126">下列範例會解除配置 `myResourceGroup` 資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="f4a7e-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="f4a7e-127">使用 [az vm availability-set convert](/cli/azure/vm/availability-set#convert) 來轉換可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="f4a7e-128">下列範例會轉換 `myResourceGroup` 資源群組中名為 `myAvailabilitySet` 的可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="f4a7e-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="f4a7e-129">使用 [az vm convert](/cli/azure/vm#convert) 將所有 VM 轉換成受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="f4a7e-130">下列程序會轉換名為 `myVM` 的 VM，包括 OS 磁碟和任何資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="f4a7e-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="f4a7e-131">轉換成受控磁碟之後，使用 [az vm start](/cli/azure/vm#start) 來啟動所有 VM。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="f4a7e-132">下列範例會啟動 `myResourceGroup` 資源群組中名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="f4a7e-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="f4a7e-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4a7e-133">Next steps</span></span>
<span data-ttu-id="f4a7e-134">如需儲存體選項的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4a7e-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
