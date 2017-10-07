---
title: "CLI 指令碼範例-aaaAzure 從快照集建立的 VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 從快照集建立 VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a>使用 CLI 從快照集建立虛擬機器

此指令碼會從 OS 磁碟的快照集建立虛擬機器。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 受管理的磁碟，虛擬機器的 hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | 使用快照集名稱和資源群組名稱取得快照集。 傳回物件 id 屬性是 hello 的使用的 toocreate 受管理的磁碟。  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 使用快照集識別碼、磁碟名稱、儲存體類型和大小，從快照集建立受控磁碟  |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立使用受控 OS 磁碟的 VM |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
