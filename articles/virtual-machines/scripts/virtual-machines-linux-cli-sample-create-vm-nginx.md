---
title: "aaaAzure CLI 指令碼範例-使用 NGINX 建立 Linux VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 NGINX 建立 Linux VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>使用 NGINX 建立 VM

此指令碼會建立 Azure 虛擬機器，並使用 hello Azure 虛擬機器自訂指令碼擴充 tooinstall NGINX。 執行 hello 指令碼之後, 您可以存取示範網站 hello 虛擬機器的 hello 公用 IP 位址。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>自訂指令碼延伸模組

hello 自訂指令碼延伸模組複製到 hello 虛擬機器上的此指令碼。 hello 指令碼接著會執行 tooinstall 和 NGINX 網頁伺服器設定。 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立 hello 虛擬機器。 此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | 建立網路安全性群組規則 tooallow 輸入流量。 在此範例中，會開放連接埠 80 供 HTTP 流量使用。 |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | 新增並執行虛擬機器擴充功能 tooa VM。 在此範例中，hello 自訂指令碼延伸模組是使用的 tooinstall NGINX。|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
