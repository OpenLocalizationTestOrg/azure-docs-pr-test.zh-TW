---
title: "Azure CLI 指令碼範例 - 使用 VM 平衡流量負載以達到高可用性 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 VM 平衡流量負載以達到高可用性"
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
ms.openlocfilehash: b04e9b22fa35f6202bc3fee547519b679f439a3d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="load-balance-traffic-to-vms-for-high-availability"></a>使用 VM 平衡流量負載以達到高可用性

此指令碼範例會建立所需的一切，以執行數部依據高可用性和負載平衡組態所設定的 Ubuntu 虛擬機器。 執行指令碼之後，您將擁有三部已加入至 Azure 可用性設定組並可透過 Azure Load Balancer 存取的虛擬機器。 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令來移除資源群組、VM 和所有相關資源。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。 下表中的每個命令都會連結至命令特定的文件。

| 命令 | 注意事項 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | 建立用來存放所有資源的資源群組。 |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | 建立 Azure 虛擬網路和子網路。 |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_create) | 建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。 |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#az_network_lb_create) | 建立 Azure 負載平衡器。 |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#az_network_lb_probe_create) | 建立負載平衡器探查。 負載平衡器探查是用來監視負載平衡器集合中的每部 VM。 如有任何 VM 變得無法存取，就不會將流量路由至該 VM。 |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | 建立負載平衡器規則。 在此範例中，會為連接埠 80 建立規則。 HTTP 流量到達負載平衡器時，它會路由傳送至 LB 集內其中一部 VM 的連接埠 80。 |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#az_network_lb_inbound_nat_rule_create) | 建立負載平衡器網路位址轉譯 (NAT) 規則。  NAT 規則會將負載平衡器的連接埠對應至 VM 上的連接埠。 在此範例中，會為傳送到負載平衡器集合中每部 VM 的 SSH 流量建立 NAT 規則。  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#az_network_nsg_create) | 建立網路安全性群組 (NSG)，做為網際網路和虛擬機器之間的安全性界限。 |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#az_network_nsg_rule_create) | 建立允許輸入流量的 NSG 規則。 在此範例中，會開放連接埠 22 供 SSH 流量使用。 |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#az_network_nic_create) | 建立虛擬網路卡，並將它連接至虛擬網路、子網路及 NSG。 |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | 建立可用性設定組。 可用性設定組可將虛擬機器分散到各個實體資源，讓整個集合不致受到萬一發生的失敗所影響，藉此來確保應用程式運作時間。 |
| [az vm create](/cli/azure/vm#create) | 建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。 此命令也會指定要使用的虛擬機器映像和管理認證。  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。

您可以在 [Azure 網路文件](../cli-samples.md)中找到其他 Azure 網路 CLI 指令碼範例。