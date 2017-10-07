---
title: "CLI 指令碼範例複製 （移動） 快照集的受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI 的複本 （移動） 快照集"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI 的快照集複製

此指令碼將複製的受管理的磁碟 toosame 或不同的訂用帳戶的快照集。 使用此指令碼 toomove 快照式 toodifferent 訂閱 hello 與 hello 父快照集相同的區域。


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>指令碼說明

此指令碼，會使用下列命令 toocreate hello 目標訂用帳戶的使用中的快照集 hello hello 來源快照集的識別碼。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | 取得所有快照集使用 hello 名稱 hello 內容和 hello 快照集的資源群組屬性。 Id 屬性是使用的 toocopy hello 快照 toodifferent 訂用帳戶。  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | 複製識別碼和名稱，藉由使用不同訂用帳戶中建立快照集的快照集 hello hello 父快照集。  |

## <a name="next-steps"></a>後續步驟

[從快照集建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
