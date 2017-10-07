---
title: "aaaUse PowerShell tooresize Azure 中的 Windows VM |Microsoft 文件"
description: "調整在 hello Resource Manager 部署模型，使用 Azure Powershell 中建立 Windows 虛擬機器的大小。"
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>調整 Windows VM 大小
本文章將示範如何 tooresize Windows VM，在建立使用 Azure Powershell hello Resource Manager 部署模型。

建立虛擬機器 (VM) 之後，您可以調整 hello VM 向上或向下藉由變更 hello VM 大小。 在某些情況下，您必須先取消配置 hello VM。 這種情況 hello 新大小不是在 hello 硬體叢集目前裝載 hello VM 上使用。

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>調整不在可用性設定組中 Windows VM 的大小
1. 列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. 如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。 視 hello 大小未列出，請繼續 toostep 3。
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. 視 hello 大小未列出，執行下列命令 toodeallocate hello VM、 調整其大小，並重新啟動 hello VM hello。
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> 解除配置 hello VM 釋放任何動態指派 toohello VM 的 IP 位址。 不會影響 hello OS 和資料磁碟。 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>調整在可用性設定組中 Windows VM 的大小
如果 hello 新的可用性設定組中的 VM 大小並不適用於 hello 硬體叢集目前裝載的 hello VM，然後在 hello 可用性設定組中的所有 Vm 需要 toobe tooresize hello VM 解除配置。 您也可能需要 tooupdate hello hello 可用性設定組後一個 VM 已調整大小的其他 Vm 大小。 tooresize 可用性設定組中的 VM 會執行下列步驟的 hello。

1. 列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. 如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。 如果未列出，請移 toostep 3。
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. 如果 hello 需要未列出的大小，請繼續進行下列步驟 toodeallocate hello hello 可用性設定組中的所有 Vm、 調整大小的 Vm，並重新啟動它們。
4. 停止 hello 可用性設定組中的所有 Vm。
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. 調整大小，並重新啟動 hello 可用性設定組中的 hello Vm。
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>後續步驟
* 如需提高延展性，可執行多個 VM 執行個體並相應放大。如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整機器](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)。

