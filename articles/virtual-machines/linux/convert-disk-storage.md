---
title: "aaaConvert Azure 受管理磁碟儲存體從標準 toopremium，反之亦然 |Microsoft 文件"
description: "從標準 toopremium，反之亦然，使用 Azure CLI，如何 tooconvert Azure 管理磁碟儲存體。"
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
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>轉換 Azure 受管理磁碟儲存體從標準 toopremium，反之亦然

受控磁碟提供兩個儲存體選項：[進階](../../storage/storage-premium-storage.md) (以 SSD 為基礎) 和[標準](../../storage/storage-standard-storage.md) (以 HDD 為基礎)。 它可讓您根據您的效能需求的最少停機時間與 hello 兩個選項之間的 tooeasily 交換器。 這項功能不適用於非受控磁碟。 但您可以輕鬆地[toomanaged 磁碟轉換](convert-unmanaged-to-managed-disks.md)tooeasily 切換 hello 兩個選項。

本文將說明從標準 toopremium，反之亦然使用 Azure CLI tooconvert 管理磁碟的方式。 如果您需要 tooinstall，或將它升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli.md)。 

## <a name="before-you-begin"></a>開始之前

* hello 轉換所需的 hello VM 重新啟動，因此排程在預先存在的維護期間的 hello 移轉磁碟儲存體。 
* 如果您第一次使用未受管理的磁碟， [toomanaged 磁碟轉換](convert-unmanaged-to-managed-disks.md)toouse hello 兩個儲存體選項之間這個發行項 tooswitch。 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>轉換所有 hello 受管理的 VM 磁碟從標準 toopremium，反之亦然

在下列範例的 hello，我們會示範如何 tooswitch 所有 hello VM 從標準 toopremium 儲存體的磁碟。 toouse premium 管理的磁碟，您的 VM 必須使用[VM 大小](sizes.md)支援進階儲存體。 此範例也會切換 tooa 支援進階儲存體的大小。

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>將受管理的磁碟轉換從標準 toopremium，反之亦然

您的開發/測試工作負載，您可能想 toohave 混合的標準和進階磁碟 tooreduce 成本。 您可以升級 toopremium 存放裝置，需要更佳的效能 hello 磁碟完成。 在下列範例的 hello，我們會示範如何 tooswitch 單一磁碟的 VM 從標準 toopremium 儲存體，反之亦然。 toouse premium 管理的磁碟，您的 VM 必須使用[VM 大小](sizes.md)支援進階儲存體。 此範例也會切換 tooa 支援進階儲存體的大小。

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>後續步驟

使用[快照](snapshot-copy-managed-disk.md)來取得 VM 的唯讀複本。

