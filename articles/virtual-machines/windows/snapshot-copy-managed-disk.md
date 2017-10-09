---
title: "Azure 受管理磁碟備份的複本 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 回最新或疑難排解磁碟 Azure 受管理磁碟 toouse 一份問題。"
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟
取得備份的受管理磁碟的快照或從 hello 快照集建立受管理磁碟並將它附加 tooa 測試虛擬機器 tootroubleshoot。 受控快照集是 VM 受控磁碟的完整時間點複本。 它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。 如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。 

## <a name="before-you-begin"></a>開始之前
如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。

## <a name="copy-hello-vhd-with-a-snapshot"></a>使用快照集複製 hello VHD
使用 hello Azure 入口網站或 PowerShell tootake hello 受管理磁碟的快照集。

### <a name="use-azure-portal-tootake-a-snapshot"></a>使用 Azure 入口網站 tootake 快照集 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從開始 hello 左上方，按一下**新增**並搜尋**快照**。
3. 在 hello 快照刀鋒視窗中，按一下 **建立**。
4. 輸入**名稱**hello 快照集。
5. 選取現有[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。 
6. 選取 Azure 資料中心的 [位置]。  
7. 如**來源磁碟**，選取 hello toosnapshot 管理的磁碟。
8. 選取 hello**帳戶類型**toouse toostore hello 快照集。 除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。
9. 按一下 [建立] 。

### <a name="use-powershell-tootake-a-snapshot"></a>使用 PowerShell tootake 快照集
hello 下列步驟顯示如何 tooget hello VHD 磁碟 toobe 複製、 建立 hello 快照設定及取得 hello 磁碟的快照集使用 hello 新增 AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->。 

1. 設定部分參數。 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  取代 hello 參數值：
  -  「 myResourceGroup"hello VM 資源群組。
  -  「 southeastasia"與 hello 管理快照集儲存所在的地理位置。 <!---How do you look these up? -->
  -  「 ContosoMD_datadisk1"hello 名稱與您想 toocopy hello VHD 磁碟。
  -  「 ContosoMD_datadisk1_snapshot1"hello 命名您想 toouse hello 新快照集。

2. 收到 hello VHD 磁碟 toobe 複製。

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. 建立 hello 快照集設定。 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. 取得 hello 快照集。

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
如果您規劃 toouse hello 快照 toocreate 受管理的磁碟，並將它附加 toobe 高執行所需的 VM，使用 hello 參數`-AccountType Premium_LRS`hello 新增 AzureRmSnapshot 命令。 hello 參數建立 hello 快照集，使它儲存為 Premium 管理磁碟。 進階受控磁碟的價格高於「標準」受控磁碟。 因此，使用該參數之前，請確定您真的需要「進階」受控磁碟。


