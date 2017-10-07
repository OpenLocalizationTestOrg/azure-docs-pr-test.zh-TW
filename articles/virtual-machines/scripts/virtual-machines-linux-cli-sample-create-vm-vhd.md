---
title: "CLI 指令碼範例-aaaAzure 建立 VM 的 vhd |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用虛擬硬碟建立 VM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>使用虛擬硬碟建立 VM

此範例會使用 VHD 建立虛擬機器。
它會建立資源群組、 儲存體帳戶和容器，接著它會建立 VM 上傳 hello VHD toohello 容器。
它會取代 hello ssh 公開，所以您需要存取 toohello VM，您的公開金鑰與索引鍵。

您將需要可開機的 VHD。
您可以從 https://azclisamples.blob.core.windows.net/vhds/sample.vhd，下載 hello 我們使用的 VHD，或使用您自己的 VHD。 hello 指令碼會尋找`~/sample.vhd`。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | 列出儲存體帳戶 |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | 檢查儲存體帳戶名稱有效，而且該它尚不存在 |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | 列出 hello 儲存體帳戶金鑰 |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | 檢查 hello blob 是否存在 |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | 在儲存體帳戶中建立容器。 |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | 正在上傳 hello VHD hello 容器中建立 blob。 |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | 搭配`--query`檢查 hello VM 名稱是否正在使用中。 | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | 建立 hello 虛擬機器。 |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | 重設 hello SSH 金鑰 toogive hello 目前使用者存取 toohello VM。 |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | 取得 hello 的 hello 所建立的 VM 的 IP 位址。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
