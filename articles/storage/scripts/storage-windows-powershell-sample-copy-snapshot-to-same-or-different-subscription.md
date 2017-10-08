---
title: "aaaAzure PowerShell 指令碼範例複製 （移動） 快照集的受管理的磁碟 toosame 或不同的訂用帳戶 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例的受管理的磁碟 toosame 或不同的訂用帳戶的複本 （移動） 快照集"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>使用 PowerShell 複製相同訂用帳戶或不同訂用帳戶中的受控磁碟快照集

此指令碼會建立一份快照集在 hello 相同的同一個訂用帳戶或其他訂用帳戶。 使用此指令碼 toomove 快照 toodifferent 訂用帳戶資料保留的。 將快照集儲存到不同的訂用帳戶中可保護您不因在主要訂用帳戶中意外刪除快照集而產生損失。 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>指令碼說明

此指令碼，會使用下列命令 toocreate hello 目標訂用帳戶的使用中的快照集 hello hello 來源快照集的識別碼。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | 建立用於建立快照集的快照集組態。 它包含 hello 資源識別碼 hello 父快照集和相同 hello 父快照集的位置。  |
| [New-AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | 使用當作參數傳遞的快照集組態、快照集名稱和資源群組名稱來建立快照集。 |


## <a name="next-steps"></a>後續步驟

[從快照集建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
