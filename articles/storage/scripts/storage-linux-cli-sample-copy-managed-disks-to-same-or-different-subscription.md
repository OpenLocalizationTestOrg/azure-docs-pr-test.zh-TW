---
title: "CLI 指令碼範例-aaaAzure 複製 （移動） 磁碟 toosame 或管理不同訂用帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例-複製 （移動） 管理磁碟 toosame 或不同的訂用帳戶"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>複製 toosame 受管理的磁碟或不同的訂用帳戶使用 CLI

此指令碼將複製的受管理的磁碟 toosame 或不同的訂用帳戶，但在 hello 相同區域。 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 目標訂用帳戶使用的新受管理的磁碟 hello 識別碼 hello 來源的受管理的磁碟。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | 取得所有受管理的磁碟使用的 hello 受管理磁碟 hello 名稱和資源群組屬性 hello 屬性。 Id 屬性是使用的 toocopy hello 管理磁碟 toodifferent 訂用帳戶。  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 將受管理的磁碟複製藉由使用識別碼和名稱的不同訂用帳戶中建立新的受管理的磁碟 hello 父管理磁碟。  |

## <a name="next-steps"></a>後續步驟

[從受控磁碟建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
