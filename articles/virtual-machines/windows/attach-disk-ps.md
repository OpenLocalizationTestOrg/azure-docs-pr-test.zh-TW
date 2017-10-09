---
title: "使用 PowerShell 在 Azure 中的 Windows VM 資料磁碟 tooa aaaAttach |Microsoft 文件"
description: "Tooattach 新的或現有的資料磁碟 tooa Windows VM 如何使用 PowerShell 和 hello Resource Manager 部署模型。"
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
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>附加資料磁碟 tooa Windows VM 使用 PowerShell

本文章將示範如何 tooattach 新的和現有磁碟 tooa 使用 PowerShell 的 Windows 虛擬機器。 如果您的 VM 使用受控磁碟，您可以附加其他受控資料磁碟。 您也可以附加 unmanaged 的資料磁碟 tooa 使用未受管理的磁碟儲存體帳戶中的 VM。

這麼做之前，請先檢閱下列提示：
* hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* toouse 高階儲存體，您將需要進階儲存體啟用像 hello DS 系列或 GS 系列虛擬機器的 VM 大小。 您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。 僅特定地區可用進階儲存體。 如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="before-you-begin"></a>開始之前
如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>加入空的資料磁碟 tooa 的虛擬機器

這個範例會示範如何 tooadd 空的資料磁碟 tooan 現有的虛擬機器。

### <a name="using-managed-disks"></a>使用受控磁碟

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>使用儲存體帳戶中的非受控磁碟

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>初始化 hello 磁碟

加入空的磁碟之後，您需要 tooinitialize 它。 tooinitialize hello 磁碟，您可以登入 tooa VM 並使用磁碟管理。 如果您在建立時啟用 WinRM 和 hello VM 上的憑證，您可以使用遠端 PowerShell tooinitialize hello 磁碟。 您也可以使用自訂指令碼擴充： 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
hello 指令碼檔案可以包含此程式碼 tooinitialize hello 磁碟像這樣：

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>附加現有的資料磁碟 tooa VM

您也可以將現有的 VHD 附加為受管理的資料磁碟 tooa 虛擬機器。 

### <a name="using-managed-disks"></a>使用受控磁碟

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>後續步驟

建立[快照集](snapshot-copy-managed-disk.md)。
