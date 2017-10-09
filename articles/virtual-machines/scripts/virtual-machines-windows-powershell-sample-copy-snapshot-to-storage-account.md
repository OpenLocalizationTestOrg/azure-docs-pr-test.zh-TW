---
title: "PowerShell 指令碼範例做為不同的區域中的 VHD tooa 儲存體帳戶匯出/複製快照集 aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例做為相同的不同區域中的 VHD tooa 儲存體帳戶匯出/複製快照集"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>匯出/受管理的快照集以複製 VHD tooa 儲存體帳戶中不同的區域，使用 PowerShell

此指令碼匯出不同的區域中的受管理的快照集 tooa 儲存體帳戶。 它第一次會產生 hello hello 快照集的 SAS URI，然後使用它 toocopy 它 tooa 不同地區中的儲存體帳戶。 此指令碼 toomaintain 中使用備份的受管理的磁碟不同地區的災害復原。  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>指令碼說明

此指令碼，會使用下列命令 toogenerate managed 快照和複本 hello 的 SAS URI 的快照集使用 SAS URI tooa 儲存體帳戶。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | 產生的快照，不使用的 toocopy SAS URI 它 tooa 儲存體帳戶。 |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | 建立使用 hello 帳戶名稱和金鑰的儲存體帳戶內容。 這個內容可以是使用的 tooperform hello 儲存體帳戶上的讀取/寫入作業。 |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | 複製 hello 基礎 VHD 的快照集 tooa 儲存體帳戶 |

## <a name="next-steps"></a>後續步驟

[從 VHD 建立受控磁碟](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[從受控磁碟建立虛擬機器](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
