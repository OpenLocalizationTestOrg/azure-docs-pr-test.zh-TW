---
title: "CLI 指令碼範例做為不同的區域中的 VHD tooa 儲存體帳戶匯出/複製快照集 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-匯出/複製快照集，與相同或不同的訂用帳戶中的 VHD tooa 儲存體帳戶"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>匯出/受管理的快照集以複製 VHD tooa 儲存體帳戶中不同的區域與 CLI

此指令碼匯出不同的區域中的受管理的快照集 tooa 儲存體帳戶。 它第一次會產生 hello hello 快照集的 SAS URI，然後使用它 toocopy 它 tooa 不同地區中的儲存體帳戶。 此指令碼 toomaintain 中使用備份的受管理的磁碟不同地區的災害復原。 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>指令碼說明

此指令碼，會使用下列命令 toogenerate managed 快照和複本 hello 的 SAS URI 的快照集使用 SAS URI tooa 儲存體帳戶。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | 產生已使用的 toocopy 基礎 VHD 檔案 tooa 儲存體帳戶，或下載它的唯讀 SAS tooon 內部部署  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | 以非同步方式將 blob 複製從一個儲存體帳戶 tooanother |

## <a name="next-steps"></a>後續步驟

[從 VHD 建立受控磁碟](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[從受控磁碟建立虛擬機器](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
