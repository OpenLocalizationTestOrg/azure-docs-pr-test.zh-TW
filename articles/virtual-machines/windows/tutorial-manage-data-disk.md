---
title: "aaaManage Azure 磁碟以 hello Azure PowerShell |Microsoft 文件"
description: "教學課程-管理以 hello Azure PowerShell 的 Azure 磁碟"
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>使用 PowerShell 管理 Azure 磁碟

Azure 虛擬機器使用的磁碟 toostore hello Vm 作業系統、 應用程式和資料。 建立 VM 時，重要 toochoose 磁碟大小和設定適當的 toohello 預期工作負載。 本教學課程涵蓋部署和管理 VM 磁碟。 您將了解：

> [!div class="checklist"]
> * OS 磁碟和暫存磁碟
> * 資料磁碟
> * 標準和進階磁碟
> * 磁碟效能
> * 連結及準備資料磁碟

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="default-azure-disks"></a>預設 Azure 磁碟

建立 Azure 虛擬機器時，兩個磁碟會自動附加的 toohello 虛擬機器。 

**作業系統磁碟**-作業系統磁碟可以 too1 tb 向上調整大小和主機 hello Vm 的作業系統。  hello OS 磁碟被指派的磁碟機代號*c:*預設。 hello 磁碟快取的 hello 作業系統磁碟組態已針對 OS 效能最佳化。 hello OS 磁碟**不應該**裝載應用程式或資料。 請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。

**暫存磁碟**-暫存磁碟使用固態磁碟機上 hello hello VM 為相同的 Azure 主機。 暫存磁碟的效能非常好，可用於暫存資料處理等作業。 不過，如果 hello VM 移動的 tooa 新主機，就會移除儲存在暫存磁碟上的任何資料。 hello hello 暫存磁碟的大小取決於 hello VM 大小。 預設會將磁碟機代號 d: 指派給暫存磁碟。

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

您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。 資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。 每個資料磁碟的最大容量為 1 TB。 hello hello 虛擬機器大小會決定資料磁碟數目可為附加的 tooa VM。 每個 VM 核心可以連結兩個資料磁碟。 

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

進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。 最適合用於執行生產工作負載的 VM。 進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。 高階磁碟都是以三種類型 (P10，P20，P30)，hello hello 磁碟大小會決定 hello 磁碟類型。 選取時，磁碟大小 hello 值會無條件進位 toohello 下一個類型。 比方說，如果 hello 大小低於 128 GB hello 磁碟類型就是 P10，129 和 512 P20，與超過 512 P30 之間。 

### <a name="premium-disk-performance"></a>進階磁碟效能

|進階儲存體磁碟類型 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 磁碟大小 (上調) | 128 GB | 512 GB | 1,024 GB (1 TB) |
| 每一磁碟的 IOPS | 500 | 2,300 | 5,000 |
每一磁碟的輸送量 | 100 MB/秒 | 150 MB/秒 | 200 MB/秒 |

雖然資料表上方的 hello 會識別每個磁碟的最大 IOPS 較高的效能等級可藉由多個資料磁碟條狀配置。 比方說，磁碟可以是 64 的資料會附加 tooStandard_GS5 VM。 如果上述每個磁碟的大小調整為 P30，就可以達到 80,000 IOPS 的最大值。 如需每部 VM 的最大 IOPS 詳細資訊，請參閱 [Linux VM 大小](./sizes.md)。

## <a name="create-and-attach-disks"></a>建立和連結磁碟

在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。 如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。 當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。

建立 hello 初始組態[新增 AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig)。 hello 下列範例會設定為 128 gb 大小的磁碟。

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

建立 hello 資料磁碟以 hello[新增 AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk)命令。

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get hello 虛擬機器，而您想 tooadd hello 資料磁碟 toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)命令。

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

新增 hello 資料磁碟 toohello 虛擬機器組態 hello[新增 AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk)命令。

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

更新 hello 的虛擬機器以 hello[更新 AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk)命令。

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>準備資料磁碟

一旦磁碟已附加的 toohello 虛擬機器，必須設定 toobe toouse hello 磁碟 hello 作業系統。 hello 下列範例示範如何 toomanually 設定 hello 新增的第一個磁碟 toohello VM。 此程序也可以自動化使用 hello[自訂指令碼延伸](./tutorial-automate-vm-deployment.md)。

### <a name="manual-configuration"></a>手動設定

建立 hello 虛擬機器的 RDP 連接。 開啟 PowerShell 並執行這個指令碼。

```powershell
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

前進 toohello 下一個教學課程的 toolearn 自動化 VM 組態。

> [!div class="nextstepaction"]
> [自動設定 VM](./tutorial-automate-vm-deployment.md)
