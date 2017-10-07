---
title: "aaaAzure CLI 指令碼範例透過網路的虛擬設備的路由傳送流量 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 透過防火牆網路虛擬設備來路由傳送流量。"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>透過網路虛擬設備來路由傳送流量

此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。 它也會將啟用的 tooroute 流量 hello 兩個子網路之間轉送 ip 建立 VM。 執行 hello 指令碼之後，您可以部署網路的軟體，例如防火牆應用程式，toohello VM。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>範例指令碼


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

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
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | 建立後端和 DMZ 子網路。 |
| [az network public-ip create](/cli/azure/network/public-ip#create) | 建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。 |
| [az network nic create](/cli/azure/network/nic#create) | 建立虛擬網路介面並為它啟用 IP 轉送功能。 |
| [az network nsg create](/cli/azure/network/nsg#create) | 建立網路安全性群組 (NSG)。 |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) | 建立允許 HTTP 和 HTTPS 連接埠輸入 toohello VM 的 NSG 規則。 |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)| 路由資料表 toosubnets 和相關聯 hello Nsg。 |
| [az network route-table create](/cli/azure/network/route-table#create)| 為所有路由建立一個路由表。 |
| [az network route-table route create](/cli/azure/network/route-table/route#create)| 建立路由 tooroute hello 網際網路透過 hello VM 子網路之間的流量。 |
| [az vm create](/cli/azure/vm#create) | 建立虛擬機器，並附加 hello NIC tooit。 此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。 |
| [az group delete](/cli/azure/group#delete) | 刪除資源群組及其包含的所有資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](/cli/azure/overview)。

其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)
