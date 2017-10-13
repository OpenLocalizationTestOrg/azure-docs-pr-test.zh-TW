---
title: "Azure CLI 指令碼範例 - 篩選 VM 網路流量 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 篩選輸入和輸出 VM 網路流量。"
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
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>篩選輸入和輸出 VM 網路流量

此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。 傳送到前端子網路的輸入流量會限制為 HTTP、HTTPS 及 SSH，而從後端子網路傳送到網際網路的輸出流量則不受允許。 執行此指令碼之後，您將會有一部具有兩個 NIC 的虛擬機器。 每個 NIC 會連線到不同的子網路。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "篩選 VM 網路流量")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令來移除資源群組、VM 和所有相關資源。

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](/cli/azure/network/vnet#create) | 建立 Azure 虛擬網路和前端子網路。 |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | 建立後端子網路。 |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | 將 NSG 與子網路建立關聯。 |
| [az network public-ip create](/cli/azure/network/public-ip#create) | 建立公用 IP 位址以從網際網路存取 VM。 |
| [az network nic create](/cli/azure/network/nic#create) | 建立虛擬網路介面，並將它們連結到虛擬網路的前端和後端子網路。 |
| [az network nsg create](/cli/azure/network/nsg#create) | 建立與前端和後端子網路關聯的網路安全性群組 (NSG)。 |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |建立對特定子網路允許或封鎖特定連接埠的 NSG 規則。 |
| [az vm create](/cli/azure/vm#create) | 建立虛擬機器，並將 NIC 連結到每個 VM。 此命令也會指定要使用的虛擬機器映像和系統管理認證。 |
| [az group delete](/cli/azure/group#delete) | 刪除資源群組及其包含的所有資源。 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](/cli/azure/overview)。

您可以在 [Azure 網路概觀文件](../cli-samples.md)中找到其他網路 CLI 指令碼範例