---
title: "aaaAzure CLI 指令碼範例-建立多層應用程式的網路 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 為多層式應用程式建立虛擬網路。"
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>為多層式應用程式建立網路

此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。 流量 toohello 前端子網路是有限的 tooHTTP 和 SSH，流量 toohello 時後端子是有限的 tooMySQL，3306 的連接埠。 執行 hello 指令碼之後, 您將擁有兩部虛擬機器，您可以部署 web 伺服器和 MySQL 軟體每個子網路的其中一個。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>範例指令碼


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](/cli/azure/network/vnet#create) | 建立 Azure 虛擬網路和前端子網路。 |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | 建立後端子網路。 |
| [az network public-ip create](/cli/azure/network/public-ip#create) | 建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。 |
| [az network nic create](/cli/azure/network/nic#create) | 建立虛擬網路介面，並將其附加 toohello 虛擬網路的前端和後端子網路。 |
| [az network nsg create](/cli/azure/network/nsg#create) | 建立網路安全性群組 (NSG) 相關聯的 toohello 前端和後端子網路。 |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |建立 NSG 規則來允許或封鎖特定連接埠 toospecific 子網路。 |
| [az vm create](/cli/azure/vm#create) | 建立虛擬機器並將附加 NIC tooeach VM。 此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。 |
| [az group delete](/cli/azure/group#delete) | 刪除資源群組及其包含的所有資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](/cli/azure/overview)。

其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)
