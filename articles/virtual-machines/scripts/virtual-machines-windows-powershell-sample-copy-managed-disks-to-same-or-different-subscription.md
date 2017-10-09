---
title: "PowerShell 指令碼範例-aaaAzure 複製 （移動） 磁碟 toosame 或管理不同訂用帳戶 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-複製 （移動） 管理磁碟 toosame 或不同的訂用帳戶"
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
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a>受管理的複本磁碟區在 hello 相同訂用帳戶或不同的訂用帳戶使用 PowerShell

此指令碼會建立 hello 現有受管理磁碟的副本相同訂用帳戶或其他訂用帳戶。 hello 會建立新磁碟在 hello 相同與 hello 父區域管理磁碟。   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 目標訂用帳戶使用的新受管理的磁碟 hello 識別碼 hello 來源的受管理的磁碟。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | 建立用於磁碟建立的磁碟組態。 它包含 hello 資源識別碼 hello 父磁碟以及父磁碟的 hello 位置相同的位置。  |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | 使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。 |


## <a name="next-steps"></a>後續步驟

[從受控磁碟建立虛擬機器](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
