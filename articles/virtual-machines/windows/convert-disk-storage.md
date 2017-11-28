---
title: "aaaConvert Azure 受管理磁碟儲存體從標準 toopremium，反之亦然 |Microsoft 文件"
description: "如何 tooconvert Azure 管理的磁碟從標準 toopremium，反之亦然，使用 Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="6172f-103">轉換 Azure 受管理磁碟儲存體從標準 toopremium，反之亦然</span><span class="sxs-lookup"><span data-stu-id="6172f-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="6172f-104">受控磁碟提供兩個儲存體選項：[進階](../../storage/storage-premium-storage.md) (以 SSD 為基礎) 和[標準](../../storage/storage-standard-storage.md) (以 HDD 為基礎)。</span><span class="sxs-lookup"><span data-stu-id="6172f-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="6172f-105">它可讓您根據您的效能需求的最少停機時間與 hello 兩個選項之間的 tooeasily 交換器。</span><span class="sxs-lookup"><span data-stu-id="6172f-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="6172f-106">這項功能不適用於非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="6172f-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="6172f-107">但您可以輕鬆地[toomanaged 磁碟轉換](convert-unmanaged-to-managed-disks.md)tooeasily 切換 hello 兩個選項。</span><span class="sxs-lookup"><span data-stu-id="6172f-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="6172f-108">本文將說明從標準 toopremium，反之亦然使用 Azure PowerShell tooconvert 管理磁碟的方式。</span><span class="sxs-lookup"><span data-stu-id="6172f-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure PowerShell.</span></span> <span data-ttu-id="6172f-109">如果您需要 tooinstall，或將它升級，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="6172f-109">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6172f-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="6172f-110">Before you begin</span></span>

* <span data-ttu-id="6172f-111">hello 轉換所需的 hello VM 重新啟動，因此排程在預先存在的維護期間的 hello 移轉磁碟儲存體。</span><span class="sxs-lookup"><span data-stu-id="6172f-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="6172f-112">如果您第一次使用未受管理的磁碟， [toomanaged 磁碟轉換](convert-unmanaged-to-managed-disks.md)toouse hello 兩個儲存體選項之間這個發行項 tooswitch。</span><span class="sxs-lookup"><span data-stu-id="6172f-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="6172f-113">轉換所有 hello 受管理的 VM 磁碟從標準 toopremium，反之亦然</span><span class="sxs-lookup"><span data-stu-id="6172f-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="6172f-114">在下列範例的 hello，我們會示範如何 tooswitch 所有 hello VM 從標準 toopremium 儲存體的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6172f-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="6172f-115">toouse premium 管理的磁碟，您的 VM 必須使用[VM 大小](sizes.md)支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="6172f-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="6172f-116">此範例也會切換 tooa 支援進階儲存體的大小。</span><span class="sxs-lookup"><span data-stu-id="6172f-116">This example also switches tooa size that supports premium storage.</span></span>

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="6172f-117">將受管理的磁碟轉換從標準 toopremium，反之亦然</span><span class="sxs-lookup"><span data-stu-id="6172f-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="6172f-118">您的開發/測試工作負載，您可能想 toohave 混合的標準和進階磁碟 tooreduce 成本。</span><span class="sxs-lookup"><span data-stu-id="6172f-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="6172f-119">您可以升級 toopremium 存放裝置，需要更佳的效能 hello 磁碟完成。</span><span class="sxs-lookup"><span data-stu-id="6172f-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="6172f-120">在下列範例的 hello，我們會示範如何 tooswitch 單一磁碟的 VM 從標準 toopremium 儲存體，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="6172f-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="6172f-121">toouse premium 管理的磁碟，您的 VM 必須使用[VM 大小](sizes.md)支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="6172f-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="6172f-122">此範例也會切換 tooa 支援進階儲存體的大小。</span><span class="sxs-lookup"><span data-stu-id="6172f-122">This example also switches tooa size that supports premium storage.</span></span>

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a><span data-ttu-id="6172f-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6172f-123">Next steps</span></span>

<span data-ttu-id="6172f-124">使用[快照](snapshot-copy-managed-disk.md)來取得 VM 的唯讀複本。</span><span class="sxs-lookup"><span data-stu-id="6172f-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

