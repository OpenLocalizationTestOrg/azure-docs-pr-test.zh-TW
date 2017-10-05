---
title: "將 Azure 受控磁碟儲存體從標準轉換至進階，反之亦然 | Microsoft Docs"
description: "如何使用 Azure CLI 將 Azure 受控磁碟儲存體從標準轉換至進階，反之亦然。"
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 0380b4aaa23b4aaba4c67d05e2d62f3ef41d6a32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="18f74-103">將 Azure 受控磁碟儲存體從標準轉換至進階，反之亦然</span><span class="sxs-lookup"><span data-stu-id="18f74-103">Convert Azure managed disks storage from standard to premium, and vice versa</span></span>

<span data-ttu-id="18f74-104">受控磁碟提供兩個儲存體選項：[進階](../../storage/storage-premium-storage.md) (以 SSD 為基礎) 和[標準](../../storage/storage-standard-storage.md) (以 HDD 為基礎)。</span><span class="sxs-lookup"><span data-stu-id="18f74-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="18f74-105">它可讓您根據您的效能需求，在兩個選項之間，以最少的停機時間輕鬆切換。</span><span class="sxs-lookup"><span data-stu-id="18f74-105">It allows you to easily switch between the two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="18f74-106">這項功能不適用於非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="18f74-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="18f74-107">但您可以輕鬆地[轉換為受控磁碟](convert-unmanaged-to-managed-disks.md)，以在兩個選項之間輕鬆切換。</span><span class="sxs-lookup"><span data-stu-id="18f74-107">But you can easily [convert to managed disks](convert-unmanaged-to-managed-disks.md) to easily switch between the two options.</span></span>

<span data-ttu-id="18f74-108">本文說明如何使用 Azure CLI 將受控磁碟從標準轉換至進階，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="18f74-108">This article shows you how to convert managed disks from standard to premium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="18f74-109">如果您需要安裝或升級 Azure CLI，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="18f74-109">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="18f74-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="18f74-110">Before you begin</span></span>

* <span data-ttu-id="18f74-111">轉換需要重新啟動 VM，因此請在預先存在的維護期間排定磁碟儲存體移轉。</span><span class="sxs-lookup"><span data-stu-id="18f74-111">The conversion requires a restart of the VM, so schedule the migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="18f74-112">如果您使用非受控磁碟，請先[轉換為受控磁碟](convert-unmanaged-to-managed-disks.md)，以使用本文在兩個儲存體選項之間切換。</span><span class="sxs-lookup"><span data-stu-id="18f74-112">If you are using unmanaged disks, first [convert to managed disks](convert-unmanaged-to-managed-disks.md) to use this article to switch between the two storage options.</span></span> 


## <a name="convert-all-the-managed-disks-of-a-vm-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="18f74-113">將 VM 的所有受控磁碟從標準轉換至進階，反之亦然</span><span class="sxs-lookup"><span data-stu-id="18f74-113">Convert all the managed disks of a VM from standard to premium, and vice versa</span></span>

<span data-ttu-id="18f74-114">在下列範例中，我們會示範如何將 VM 的所有磁碟從標準儲存體切換成進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="18f74-114">In the following example, we show how to switch all the disks of a VM from standard to premium storage.</span></span> <span data-ttu-id="18f74-115">若要使用進階受控磁碟，您的 VM 必須使用可支援進階儲存體的 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="18f74-115">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="18f74-116">此範例也會切換成可支援進階儲存體的大小。</span><span class="sxs-lookup"><span data-stu-id="18f74-116">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the virtual machine
rgName='yourResourceGroup'

#Name of the virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate the VM before changing the size of the VM
az vm deallocate --name $vmName --resource-group $rgName

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update the sku of all the data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update the sku of the OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-to-premium-and-vice-versa"></a><span data-ttu-id="18f74-117">將受控磁碟從標準轉換至進階，反之亦然</span><span class="sxs-lookup"><span data-stu-id="18f74-117">Convert a managed disk from standard to premium, and vice versa</span></span>

<span data-ttu-id="18f74-118">對於您的開發/測試工作負載，您可能希望混合標準和進階磁碟，以降低成本。</span><span class="sxs-lookup"><span data-stu-id="18f74-118">For your dev/test workload, you may want to have mixture of standard and premium disks to reduce your cost.</span></span> <span data-ttu-id="18f74-119">您可以藉由升級至進階儲存體來完成此作業，僅限需要更佳效能的磁碟。</span><span class="sxs-lookup"><span data-stu-id="18f74-119">You can accomplish it by upgrading to premium storage, only the disks that require better performance.</span></span> <span data-ttu-id="18f74-120">在下列範例中，我們會示範如何將 VM 的單一磁碟從標準儲存體切換成進階儲存體，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="18f74-120">In the following example, we show how to switch a single disk of a VM from standard to premium storage, and vice versa.</span></span> <span data-ttu-id="18f74-121">若要使用進階受控磁碟，您的 VM 必須使用可支援進階儲存體的 [VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="18f74-121">To use premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="18f74-122">此範例也會切換成可支援進階儲存體的大小。</span><span class="sxs-lookup"><span data-stu-id="18f74-122">This example also switches to a size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains the managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard to premium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get the parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate the VM before changing the size of the VM
az vm deallocate --ids $vmId 

#Change the VM size to a size that supports premium storage 
#Skip this step if converting storage from premium to standard
az vm resize --ids $vmId --size $size

# Update the sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="18f74-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18f74-123">Next steps</span></span>

<span data-ttu-id="18f74-124">使用[快照](snapshot-copy-managed-disk.md)來取得 VM 的唯讀複本。</span><span class="sxs-lookup"><span data-stu-id="18f74-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

