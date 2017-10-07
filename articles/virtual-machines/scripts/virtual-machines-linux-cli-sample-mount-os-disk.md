---
title: "CLI 指令碼範例掛接作業系統磁碟 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 掛接作業系統磁碟"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>針對 VM 作業系統磁碟進行疑難排解

此指令碼做為資料磁碟 tooa 第二個虛擬機器掛接 hello 失敗或問題的虛擬機器的作業系統磁碟。 在進行磁碟問題或復原資料的疑難排解時，這非常有用。 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | 傳回虛擬機器清單。 在此情況下，hello 查詢選項是使用的 tooreturn hello 虛擬機器的作業系統磁碟。 接著，這個值會加入 tooa 變數名稱 'uri'。 |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | 刪除虛擬機器。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立虛擬機器。  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | 附加磁碟 tooa 虛擬機器。 |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | 傳回 hello 虛擬機器的 IP 位址。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
