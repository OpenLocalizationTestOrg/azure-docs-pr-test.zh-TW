---
title: "aaaAzure CLI 指令碼範例-負載平衡的多個網站以 hello Azure CLI |Microsoft 文件"
description: "Azure CLI 指令碼範例-負載平衡的多個網站 toohello 相同的虛擬機器"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>進行多個網站的負載平衡

此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。 負載平衡器會將兩個不同的流量導向 toohello 兩個 Vm 的 IP 位址。 執行 hello 指令碼之後，可以部署 web 伺服器軟體 toohello Vm，裝載多個 web sites 中，每個都有它自己的 IP 位址。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬網路負載平衡器和所有相關的資源的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | 建立 Azure 虛擬網路和子網路。 |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | 建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。 |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | 建立 Azure 負載平衡器。 |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | 建立負載平衡器探查。 負載平衡器探查是使用的 toomonitor hello 負載平衡器集內的每個 VM。 如果任何 VM 變得無法存取，流量不是路由的 toohello VM。 |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 建立負載平衡器規則。 在此範例中，會為連接埠 80 建立規則。 HTTP 流量抵達 hello 負載平衡器時，它是路由的 tooport 80 hello Vm hello 負載平衡器集內的其中一個。 |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | 建立 hello 負載平衡器的前端 IP 位址。 |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | 建立後端位址集區。 |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | 建立虛擬網路介面卡，並將其附加 toohello 虛擬網路和子網路。 |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | 建立可用性設定組。 可用性設定組來確保應用程式執行時間跨實體資源分配 hello 虛擬機器，使得發生失敗時，不受影響 hello 整個集合。 |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | 建立 IP 設定。 您必須啟用訂用帳戶的 hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic 功能。 只能在一個設定可能會被指定為每個 NIC，使用 hello-請主要旗標 hello 主要 IP 設定。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | 建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。 此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。
