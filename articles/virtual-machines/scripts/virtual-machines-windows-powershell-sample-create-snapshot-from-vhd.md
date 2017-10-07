---
title: "aaaAzure PowerShell 指令碼範例為建立快照集 VHD toocreate 從多個受管理的相同磁碟在短時間內 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-建立快照集 VHD toocreate 從多個受管理的相同磁碟在短時間內"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>建立快照集 VHD toocreate 從多個受管理的相同磁碟小型一段時間內使用 PowerShell

此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立快照集。 使用此指令碼 tooimport 特製化 (無法一般化/執行過 sysprep) VHD tooa 快照集，然後再使用多個受管理的相同磁碟 hello 快照 toocreate 在短時間內。 此外，使用 tooimport 資料 VHD tooa 快照集，然後再使用多個受管理的磁碟 hello 快照 toocreate 在短時間內。 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 受管理的磁碟從不同的訂用帳戶中的 VHD。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 建立用於磁碟建立的磁碟組態。 它包含存放裝置類型、 位置、 hello hello 父 VHD 的儲存位置的儲存體帳戶的資源 Id 和 hello 父系 VHD 的 VHD URI。 |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。 |

## <a name="next-steps"></a>後續步驟

[從快照集建立受控磁碟](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[將受控磁碟連結為 OS 磁碟以建立虛擬機器](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
