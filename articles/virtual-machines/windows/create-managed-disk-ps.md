---
title: "從 VHD 在 Azure 中的受管理磁碟 aaaCreate |Microsoft 文件"
description: "從 Azure 儲存體帳戶，目前正在使用 hello Resource Manager 部署模型的 VHD 建立受管理的磁碟。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>從儲存體帳戶中的非受控磁碟建立受控磁碟

您可以從現有的資料磁碟或 Azure 儲存體帳戶中目前的 OS 磁碟，建立受控磁碟。 您也可建立空的磁碟，以便作為 VM 的新資料磁碟。 

## <a name="before-you-begin"></a>開始之前
如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>從 Azure 儲存體帳戶中的 VHD 建立受控映像

在我們的為受管理磁碟的 VHD 建立磁碟，並將它指派 toohello 參數 hello 範例**$disk1** toouse 更新版本。 

hello 受管理的磁碟將會建立在 hello **West US**位置，請在資源群組名稱**myResourceGroup**。 將名為 hello 磁碟**myDisk** ，將會建立名為的 VHD 檔案從**myDisk.vhd**我們先前上傳 tooa 儲存體帳戶**mystorageaccount**。 高階本機備援儲存體 (LRS) 中，將會建立 hello 受管理的磁碟。 StandardLRS 和 PremiumLRS 是只 hello **-AccountType**選項可用於管理的磁碟。 

1.  設定一些參數

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. 建立 hello 資料磁碟。 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>建立空的資料磁碟作為受控磁碟

在 hello 範例中我們建立空的資料磁碟做為受管理的磁碟，並將它指派 toohello 參數**$dataDisk2** toouse 更新版本。 空的資料磁碟需要 toobe 初始化登入 toohello VM，並使用 diskmgmt.msc 或[使用 WinRM 和指令碼](attach-disk-ps.md#initialize-the-disk)，一旦附加的 tooa 執行 VM。

hello 空的資料磁碟將會建立在 hello**中央美國西部**位置，請在資源群組名稱**myResourceGroup**。 將名為 hello 磁碟**myEmptyDataDisk**。 高階本機備援儲存體 (LRS) 中，將會建立 hello 空的磁碟。 StandardLRS 和 PremiumLRS 是只 hello **-AccountType**選項可用於管理的磁碟。

在此範例中的 hello 磁碟大小為 128 GB，但您應選擇符合您的 VM 上執行任何應用程式的 hello 需求的大小。

1.  設定一些參數

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. 建立 hello 資料磁碟。
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>後續步驟   
- 如果您已經有 VM，即可[附加資料磁碟](attach-disk-portal.md)。
