---
title: "使用 Azure PowerShell 管理 Azure 磁碟 | Microsoft Docs"
description: "教學課程 - 使用 Azure PowerShell 管理 Azure 磁碟"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 58c8ba2682cc9cc8f2089d2a70cc95a03079832e
ms.sourcegitcommit: c87e036fe898318487ea8df31b13b328985ce0e1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2017
---
# <a name="manage-azure-disks-with-powershell"></a>使用 PowerShell 管理 Azure 磁碟

Azure 虛擬機器使用磁碟來儲存 VM 作業系統、應用程式和資料。 建立 VM 時，請務必選擇適合所預期工作負載的磁碟大小和組態。 本教學課程涵蓋部署和管理 VM 磁碟。 您將了解：

> [!div class="checklist"]
> * OS 磁碟和暫存磁碟
> * 資料磁碟
> * 標準和進階磁碟
> * 磁碟效能
> * 連結及準備資料磁碟

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

如果您選擇在本機安裝和使用 PowerShell，本教學課程會要求使用 Azure PowerShell 模組版本 3.6 或更新版本。 執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。 如果您需要升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。 如果您在本機執行 PowerShell，則也需要執行 `Login-AzureRmAccount` 以建立與 Azure 的連線。 

## <a name="default-azure-disks"></a>預設 Azure 磁碟

建立 Azure 虛擬機器後，有兩個磁碟會自動連結到虛擬機器。 

**作業系統磁碟** - 作業系統磁碟可裝載 VM 作業系統，其大小可以高達 4 TB。  預設會將磁碟機代號 c: 指派給 OS 磁碟。 OS 磁碟的磁碟快取組態已針對 OS 效能進行最佳化。 OS 磁碟**不得**裝載應用程式或資料。 請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。

**暫存磁碟** - 暫存磁碟會使用與 VM 位於相同 Azure 主機的固態磁碟機。 暫存磁碟的效能非常好，可用於暫存資料處理等作業。 不過，如果 VM 移至新的主機，則會移除儲存在暫存磁碟上的任何資料。 暫存磁碟的大小取決於 VM 大小。 預設會將磁碟機代號 d: 指派給暫存磁碟。

### <a name="temporary-disk-sizes"></a>暫存磁碟大小

| 類型 | VM 大小 | 暫存磁碟大小上限 (GB) |
|----|----|----|
| [一般用途](sizes-general.md) | A 和 D 系列 | 800 |
| [計算最佳化](sizes-compute.md) | F 系列 | 800 |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md) | D 和 G 系列 | 6144 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md) | L 系列 | 5630 |
| [GPU](sizes-gpu.md) | N 系列 | 1440 |
| [高效能](sizes-hpc.md) | A 和 H 系列 | 2000 |

## <a name="azure-data-disks"></a>Azure 資料磁碟

您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。 資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。 每個資料磁碟的最大容量為 1 TB。 虛擬機器的大小會決定可連結到 VM 的資料磁碟數目。 每個 VM vCPU 可以連結兩個資料磁碟。 

### <a name="max-data-disks-per-vm"></a>每部 VM 的資料磁碟上限

| 類型 | VM 大小 | 每部 VM 的資料磁碟上限 |
|----|----|----|
| [一般用途](sizes-general.md) | A 和 D 系列 | 32 |
| [計算最佳化](sizes-compute.md) | F 系列 | 32 |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md) | D 和 G 系列 | 64 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md) | L 系列 | 64 |
| [GPU](sizes-gpu.md) | N 系列 | 48 |
| [高效能](sizes-hpc.md) | A 和 H 系列 | 32 |

## <a name="vm-disk-types"></a>VM 磁碟類型

Azure 提供兩種類型的磁碟。

### <a name="standard-disk"></a>標準磁碟

標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。 標準磁碟適合用於具成本效益的開發和測試工作負載。

### <a name="premium-disk"></a>進階磁碟

進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。 最適合用於執行生產工作負載的 VM。 進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。 高階磁碟都是以 P10、 P20、 P30、 P40 （P50） 的五種類型，該磁碟的大小會決定磁碟類型。 進行選取時，磁碟大小值會上調為下一個類型。 例如，如果大小低於 128 GB，則磁碟類型會是 P10，介於 129 與 512 GB 會是 P20，512 GB 是 P30，2 TB 是 P40，4 TB 則是 P50。 

### <a name="premium-disk-performance"></a>進階磁碟效能

|進階儲存體磁碟類型 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 磁碟大小 (上調) | 128 GB | 512 GB | 1,024 GB (1 TB) |
| 每一磁碟的 IOPS | 500 | 2,300 | 5,000 |
每一磁碟的輸送量 | 100 MB/秒 | 150 MB/秒 | 200 MB/秒 |

雖然上表指出每個磁碟的最大 IOPS，但可藉由分割多個資料磁碟來達到較高等級的效能。 例如，可以將 64 個資料磁碟連結到 Standard_GS5 VM。 如果上述每個磁碟的大小調整為 P30，就可以達到 80,000 IOPS 的最大值。 如需每部 VM 之最大 IOPS 的詳細資訊，請參閱 [VM 類型和大小](./sizes.md)。

## <a name="create-and-attach-disks"></a>建立和連結磁碟

若要完成本教學課程中的範例，您目前必須具有虛擬機器。 如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。 逐步完成教學課程之後，請視需要取代資源群組和 VM 名稱。

使用 [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig) 建立初始組態。 下列範例會設定大小為 128 GB 的磁碟。

```azurepowershell-interactive
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

使用 [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) 命令來建立資料磁碟。

```azurepowershell-interactive
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

使用 [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 命令來取得您要在其中新增資料磁碟的虛擬機器。

```azurepowershell-interactive
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

使用 [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 命令將資料磁碟新增至虛擬機器組態。

```azurepowershell-interactive
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

使用 [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 命令來更新虛擬機器。

```azurepowershell-interactive
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>準備資料磁碟

將磁碟連結到虛擬機器後，必須將作業系統設定為使用該磁碟。 下列範例示範如何手動設定第一個新增至 VM 的磁碟。 使用[自訂指令碼擴充](./tutorial-automate-vm-deployment.md)也可以自動執行此程序。

### <a name="manual-configuration"></a>手動設定

建立虛擬機器的 RDP 連線。 開啟 PowerShell 並執行這個指令碼。

```azurepowershell-interactive
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解 VM 磁碟的相關主題，像是：

> [!div class="checklist"]
> * OS 磁碟和暫存磁碟
> * 資料磁碟
> * 標準和進階磁碟
> * 磁碟效能
> * 連結及準備資料磁碟

請前進到下一個教學課程，以了解如何自動設定 VM。

> [!div class="nextstepaction"]
> [自動設定 VM](./tutorial-automate-vm-deployment.md)
