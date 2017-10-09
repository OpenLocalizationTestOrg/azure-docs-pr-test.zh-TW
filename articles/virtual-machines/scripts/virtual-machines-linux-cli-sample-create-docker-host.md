---
title: "CLI 指令碼範例-aaaAzure 建立 Docker 主機 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Docker 主機"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a>建立含 Docker 功能的 VM

這個指令碼會建立啟用 Docker 功能的虛擬機器，並啟動執行 NGINX 的 Docker 容器。 執行 hello 指令碼之後, 您可以透過 hello hello Azure 虛擬機器的 FQDN 存取 hello NGINX 網頁伺服器。 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 部署的 hello。 Hello 資料表中的每個項目連結 toocommand 特定文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | 建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和網路安全性群組。 此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) | 建立網路安全性群組規則 tooallow 輸入流量。 在此範例中，會開放連接埠 80 供 HTTP 流量使用。 |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | 新增並執行虛擬機器擴充功能 tooa VM。 在此範例中，hello Docker VM 擴充功能是使用的 tooconfigure Docker 主機。|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
