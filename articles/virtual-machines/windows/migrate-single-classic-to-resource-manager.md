---
title: "aaaMigrate 傳統 VM tooan ARM 管理磁碟 VM |Microsoft 文件"
description: "移轉單一 Azure VM 從 hello 傳統部署模型 tooManaged hello Resource Manager 部署模型中的磁碟。"
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>手動將移轉傳統 VM tooa 中的新 ARM 管理磁碟 VM hello VHD 


本節可協助您 toomigrate 現有的 Azure Vm 從 hello 傳統部署模型太[管理磁碟](managed-disks-overview.md)hello Resource Manager 部署模型中。


## <a name="plan-for-hello-migration-toomanaged-disks"></a>規劃移轉 hello tooManaged 磁碟

本節可協助您 toomake hello 最佳決定 VM 和磁碟類型。


### <a name="location"></a>位置

挑選 Azure 受控磁碟可用的位置。 如果您正在移轉 tooPremium 管理磁碟，也請確定高階儲存體可用規劃至 toomigrate hello 區域中。 如需可用位置的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。

### <a name="vm-sizes"></a>VM 大小

如果您要移轉 tooPremium 管理磁碟，您會有 hello VM 所在的區域中的 hello VM tooPremium 可用儲存體能夠大小 tooupdate hello 大小。 檢閱可支援進階儲存體 hello VM 大小。 hello Azure VM 大小規格中所列[虛擬機器的大小](sizes.md)。
檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。 請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。

### <a name="disk-sizes"></a>磁碟大小

**進階受控磁碟**

有七種型別的進階受控磁碟可以搭配 VM 使用，而且每種都有特定的 IOP 和輸送量限制。 當您選擇 hello VM 的高階磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載時，請考慮這些限制。

| 進階磁碟類型  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 磁碟大小           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| 每一磁碟的 IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| 每一磁碟的輸送量 | 每秒 25 MB  | 每秒 50 MB  | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB | 

**標準受控磁碟**

有七種型別的標準受控磁碟可搭配 VM 使用。 每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。 選擇 hello 根據 hello 容量需求的應用程式的標準管理磁碟類型。

| 標準磁碟類型  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| 磁碟大小           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| 每一磁碟的 IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| 每一磁碟的輸送量 | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 


### <a name="disk-caching-policy"></a>磁碟快取原則 

**進階受控磁碟**

根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。 此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。 對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。

### <a name="pricing"></a>價格

檢閱 hello[定價管理磁碟](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。 定價的高階管理磁碟是與 hello 高階 Unmanaged 磁碟相同。 但標準受控磁碟與標準非受控磁碟的價格不同。


## <a name="checklist"></a>檢查清單

1.  如果您要移轉 tooPremium 管理磁碟，請確定它可以使用您要移轉至 hello 區域中。

2.  決定 hello 您要將新 VM 系列。 如果您要移轉 tooPremium 管理磁碟，它應該是支援高階儲存體。

3.  決定 hello 確切 VM 大小將會使用您要移轉至 hello 區域中可用的。 VM 大小需要 toobe 夠大 toosupport hello 您擁有的資料磁碟數目。 例如，如果您有四個資料磁碟，hello VM 必須有兩個或多個核心。 也請考慮處理能力、記憶體和網路頻寬需求。

4.  有 hello 目前 VM 詳細資料很方便，包括 hello 磁碟清單及其對應的 VHD blob。

為您的應用程式做好停機準備。 toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。 唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。 停機持續時間取決於 hello hello 磁碟 toomigrate 中的資料數量。


## <a name="migrate-hello-vm"></a>移轉 hello VM

為您的應用程式做好停機準備。 toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。 唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。 停機持續時間取決於 hello hello 磁碟 toomigrate 中的資料數量。


1.  首先，設定 hello 一般參數：

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  建立受管理的作業系統磁碟使用 hello VHD 從 hello 傳統 VM。

    請確定您已提供 hello 完成 hello OS VHD toohello $osVhdUri 參數的 URI。 此外，根據您要移轉至的磁碟類型 (進階或標準)，將 **-AccountType** 輸入為 **PremiumLRS** 或 **StandardLRS**。

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  附加 hello OS 磁碟 toohello 新的 VM。

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  從 hello 資料 VHD 檔案建立受管理的資料磁碟，並將它新增 toohello 新的 VM。

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  建立新的 VM hello 藉由設定公用 IP、 虛擬網路和 NIC

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>可能有額外的步驟需要 toosupport 的應用程式不會涵蓋本指南。
>
>

## <a name="next-steps"></a>後續步驟

- Toohello 虛擬機器連線。 如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

