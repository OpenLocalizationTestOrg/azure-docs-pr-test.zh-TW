---
title: "aaaAzure CLI 指令碼範例-從 hello 的儲存體帳戶的 VHD 檔案建立受管理的磁碟相同的訂用帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例： 建立受管理的磁碟儲存體帳戶中 hello 的 VHD 檔案從相同訂用帳戶"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>從 VHD 檔案 hello 的儲存體帳戶中建立受管理的磁碟使用 CLI 的相同訂用帳戶

此指令碼會建立受管理的磁碟儲存體帳戶中 hello 的 VHD 檔案從相同訂用帳戶。 使用此指令碼 tooimport 特製化 (無法一般化/執行過 sysprep) VHD toomanaged OS 磁碟 toocreate 虛擬機器。 或者，您也可以使用它 tooimport 資料 VHD toomanaged 資料磁碟。 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate VHD 從受管理的磁碟。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | 建立受管理的磁碟在 hello 的儲存體帳戶中使用的 VHD URI 相同訂用帳戶 |

## <a name="next-steps"></a>後續步驟

[將受控磁碟連結為 OS 磁碟以建立虛擬機器](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
