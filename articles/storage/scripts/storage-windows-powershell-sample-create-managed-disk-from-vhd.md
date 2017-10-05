---
title: "Azure PowerShell 指令碼範例 - 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟"
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
ms.openlocfilehash: b9c3d2e8dbf5caa525f82955aceb615cb1c28e93
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>使用 PowerShell 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟

此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立受控磁碟。 使用此指令碼可將專用 (非一般化/已執行過 Sysprep) 的 VHD 匯入至受控 OS 磁碟，以建立虛擬機器。 同時，用它將資料 VHD 匯入到受控資料磁碟。 

請勿在短時間內從 VHD 檔案建立多個相同的受控磁碟。 若要從 VHD 檔案建立受控磁碟，會建立 VHD 檔案的 Blob 快照集，然後將它用於建立受控磁碟。 一分鐘內只能建立一個 Blob 快照集，這會導致磁碟建立因節流而失敗。 若要避免進行此節流，請[從 VHD 檔案建立受控快照集](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)，然後使用受控快照集在短時間內建立多個受控磁碟。 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[主要](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "從 VHD 建立受控磁碟")]


## <a name="script-explanation"></a>指令碼說明

此指令碼使用下列命令從不同訂用帳戶的 VHD 建立受控磁碟。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 建立用於磁碟建立的磁碟組態。 它包含儲存體類型、位置、儲存父 VHD 所在儲存體帳戶的資源識別碼、父 VHD 的 VHD URI。 |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。 |

## <a name="next-steps"></a>後續步驟

[將受控磁碟連結為 OS 磁碟以建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。

您可以在 [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。