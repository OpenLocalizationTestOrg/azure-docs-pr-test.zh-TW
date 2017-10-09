---
title: "CLI 指令碼範例-aaaAzure 從快照集建立受管理的磁碟 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 從快照集建立受控磁碟"
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>使用 CLI 從快照集建立受控磁碟

此指令碼會從快照集建立受控磁碟。 使用 toorestore OS 和資料磁碟的快照中的虛擬機器。 從個別的快照集建立 OS 和資料受控磁碟，再連結受控磁碟以建立新的虛擬機器。 您也可以連結從快照集建立的資料磁碟，以還原現有 VM 的資料磁碟。


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 受管理的磁碟，從快照集。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | 取得所有快照集使用 hello 名稱 hello 內容和 hello 快照集的資源群組屬性。 Id 屬性是使用的 toocreate 受管理的磁碟。  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 使用受管理快照集的快照集識別碼建立受控磁碟 |

## <a name="next-steps"></a>後續步驟

[將受控磁碟連結為 OS 磁碟以建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
