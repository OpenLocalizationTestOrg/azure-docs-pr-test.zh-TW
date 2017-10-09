---
title: "aaaAzure CLI 指令碼範例-建立 VM，藉由附加為作業系統磁碟的受管理的磁碟 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 連結受控磁碟作為 OS 磁碟以建立 VM | Microsoft Docs"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>使用現有受控 OS 磁碟搭配 CLI 以建立虛擬機器

此指令碼會連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。 在先前案例中使用此指令碼︰
* 從不同訂用帳戶中的受控磁碟複製而來的現有受控 OS 磁碟建立 VM
* 從特殊化 VHD 檔案建立的現有受控磁碟建立 VM 
* 從快照集建立的現有受控 OS 磁碟建立 VM 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 tooget 管理磁碟屬性中的 hello、 附加受管理的磁碟 tooa 新的 VM，並建立 VM。 Hello 資料表中的每個項目連結 toocommand 特定文件。

| 命令 | 注意事項 |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | 使用磁碟名稱和資源群組名稱取得受控磁碟屬性。 Id 屬性都是使用的 tooattach 受管理的磁碟 tooa 新的 VM |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立使用受控 OS 磁碟的 VM |
## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
