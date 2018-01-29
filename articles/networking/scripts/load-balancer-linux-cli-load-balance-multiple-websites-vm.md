---
title: "Azure CLI 指令碼範例 - 使用 Azure CLI 進行多個網站的負載平衡 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用相同的虛擬機器進行多個網站的負載平衡"
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
ms.openlocfilehash: 98b07bfabf2d01c7ae3db7365cfbab3639c6f026
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="load-balance-multiple-websites"></a>進行多個網站的負載平衡

此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。 負載平衡器會將兩個不同 IP 位址的流量傳送至這兩個 VM。 執行指令碼之後，您可以將 Web 伺服器軟體部署至 VM 並主控多個網站 (各有自己的 IP 位址)。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令來移除資源群組、VM 和所有相關資源。

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>指令碼說明

此指令碼使用下列命令建立資源群組、虛擬網路、負載平衡器和所有相關資源。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | 建立 Azure 虛擬網路和子網路。 |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_create) | 建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。 |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#az_network_lb_create) | 建立 Azure 負載平衡器。 |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#az_network_lb_probe_create) | 建立負載平衡器探查。 負載平衡器探查是用來監視負載平衡器集合中的每部 VM。 如有任何 VM 變得無法存取，就不會將流量路由至該 VM。 |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | 建立負載平衡器規則。 在此範例中，會為連接埠 80 建立規則。 HTTP 流量到達負載平衡器時，它會路由傳送至負載平衡器集內其中一個 VM 的連接埠 80。 |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#az_network_lb_frontend_ip_create) | 建立負載平衡器的前端 IP 位址。 |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#az_network_lb_address_pool_create) | 建立後端位址集區。 |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#az_network_nic_create) | 建立虛擬網路卡，並將它連結至虛擬網路和子網路。 |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | 建立可用性設定組。 可用性設定組可將虛擬機器分散到各個實體資源，讓整個集合不致受到萬一發生的失敗所影響，藉此來確保應用程式運作時間。 |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#az_network_nic_ip_config_create) | 建立 IP 設定。 您的訂用帳戶必須啟用 Microsoft.Network/AllowMultipleIpConfigurationsPerNic 功能。 每個 NIC 只能指定一個設定作為主要 IP 設定 (使用 --make-primary 旗標)。 |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#az_vm_availability_set_create) | 建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。 此命令也會指定要使用的虛擬機器映像和管理認證。  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以在 [Azure 網路概觀文件](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 CLI 指令碼範例。
