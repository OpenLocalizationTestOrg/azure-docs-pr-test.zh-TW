---
title: "Windows 虛擬機器從 unmanaged aaaConvert 磁碟 toomanaged 磁碟-Azure 受管理磁碟 |Microsoft 文件"
description: "如何 tooconvert 從 unmanaged 的磁碟 toomanaged Windows VM 磁碟在 hello Resource Manager 部署模型中使用 PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>從 unmanaged 的磁碟 toomanaged 磁碟轉換 Windows 虛擬機器

如果您有現有 Windows 虛擬機器 (Vm)，並且使用未受管理的磁碟，您可以將透過 hello hello Vm toouse 管理磁碟轉換[Azure 受管理磁碟](managed-disks-overview.md)服務。 此程序轉換 hello OS 磁碟和任何連接的資料磁碟。

本文章將示範如何使用 Azure PowerShell tooconvert Vm。 如果您需要 tooinstall，或將它升級，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps.md)。

## <a name="before-you-begin"></a>開始之前


* 檢閱[hello 移轉計劃 tooManaged 磁碟](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)。

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>轉換單一執行個體 VM
本章節涵蓋 tooconvert 單一執行個體中未受管理的 Azure Vm 磁碟 toomanaged 磁碟的方式。 （如果您的 Vm 可用性設定組中，請參閱 hello 下一節）。 

1. Deallocate hello VM 使用 hello[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet。 hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. 使用 hello 轉換 hello VM toomanaged 磁碟[ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet。 下列程序會將轉換的 hello hello 先前的 VM，包括 hello OS 磁碟和任何資料磁碟：

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. 使用 hello 轉換 toomanaged 磁碟後啟動 hello VM[開始 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)。 下列範例會重新啟動的 hello hello 先前的 VM:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>轉換可用性設定組中的 VM

如果您想要 tooconvert toomanaged 磁碟都在可用性設定組中的 hello Vm，您必須先管理 tooconvert hello 可用性集 tooa 可用性設定組。

1. 轉換 hello 可用性設定組使用 hello[更新 AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet。 下列範例更新 hello 可用性設定組具名的 hello `myAvailabilitySet` hello 資源群組中名為`myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  如果您的可用性設定組所在的 hello 區域只有 2 的受管理的容錯網域，但 hello 未受管理的容錯網域數目是 3，此命令會顯示錯誤類似太 「 hello 指定容錯網域計數 3 必須落在 hello 範圍 1 too2。 」 tooresolve hello 錯誤、 更新 hello 容錯網域 too2 和 update`Sku`太`Aligned`，如下所示：

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. 解除配置，並轉換 hello 可用性設定組中的 hello Vm。 hello 下列指令碼解除配置每個 VM 使用 hello[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet，將它轉換使用[ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)，並重新啟動使用[開始 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>疑難排解

如果在轉換期間，發生錯誤，或如果 VM 是處於失敗狀態，因為先前的轉換中的問題，執行 hello `ConvertTo-AzureRmVMManagedDisk` cmdlet 一次。 簡單的重試通常會解除封鎖 hello 的情況。


## <a name="next-steps"></a>後續步驟

[轉換受管理的標準磁碟 toopremium](convert-disk-storage.md)

使用[快照](snapshot-copy-managed-disk.md)來取得 VM 的唯讀複本。

