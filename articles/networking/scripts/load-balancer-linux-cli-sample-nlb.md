---
title: "CLI 指令碼範例提供高可用性的負載平衡流量 tooVMs aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-負載平衡流量 tooVMs 高可用性"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>負載平衡流量 tooVMs 高可用性

此指令碼範例會建立所需的所有項目 toorun 數個 Ubuntu 虛擬機器設定高可用性和負載平衡的設定。 之後執行 hello 指令碼，您將擁有三部虛擬機器，聯結 tooan Azure 可用性設定組，且可透過 Azure 負載平衡器。 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | 建立 Azure 虛擬網路和子網路。 |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | 建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。 |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | 建立 Azure 負載平衡器。 |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | 建立負載平衡器探查。 負載平衡器探查是使用的 toomonitor hello 負載平衡器集內的每個 VM。 如果任何 VM 變得無法存取，流量不是路由的 toohello VM。 |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 建立負載平衡器規則。 在此範例中，會為連接埠 80 建立規則。 HTTP 流量抵達 hello 負載平衡器時，它是路由的 tooport 80 hello Vm hello LB 集內的其中一個。 |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | 建立負載平衡器網路位址轉譯 (NAT) 規則。  NAT 規則對應 hello 負載平衡器 tooa 連接埠在 VM 上的連接埠。 在此範例中，會為在 hello 負載平衡器集 SSH 流量 tooeach VM 建立 NAT 規則。  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | 建立網路安全性群組 (NSG)，也就是 hello 網際網路和 hello 虛擬機器的安全性界限。 |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | 建立 NSG 規則 tooallow 輸入流量。 在此範例中，會開放連接埠 22 供 SSH 流量使用。 |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | 建立虛擬網路介面卡，並將其附加 toohello 虛擬網路、 子網路和 NSG。 |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 建立可用性設定組。 可用性設定組來確保應用程式執行時間跨實體資源分配 hello 虛擬機器，使得發生失敗時，不受影響 hello 整個集合。 |
| [az vm create](/cli/azure/vm#create) | 建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。 此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他的 Azure 網路 CLI 指令碼範例可以在 hello [Azure 網路文件](../cli-samples.md)。