---
title: "aaaOpen 連接埠 tooa Linux VM 與 Azure CLI 1.0 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Linux VM / 使用 hello Azure 資源管理員部署模型和 hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>開啟連接埠和端點 tooa Linux VM 在 Azure 中使用 hello Azure CLI 1.0
您開啟通訊埠，或建立端點，tooa Azure 虛擬機器 (VM) 中藉由建立子網路或 VM 網路介面上的網路篩選條件。 您收到 hello 流量的網路安全性群組附加 toohello 資源上放置控制輸入與輸出流量，這些篩選器。 讓我們使用連接埠 80 上的 Web 流量的常見範例。 本文章將示範如何連接埠 tooa VM 使用 tooopen hello Azure CLI 1.0。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](nsg-quickstart.md) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令
toocreate 網路安全性群組規則您需要和[hello Azure CLI 1.0](../../cli-install-nodejs.md)已安裝且正在使用的 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。

適當地輸入您自己的名稱和位置來建立「網路安全性群組」。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*在 hello *eastus*位置：

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

新增規則 tooallow HTTP 流量 tooyour 網頁伺服器 （或 調整成您自己的案例，例如 SSH 存取或資料庫連線）。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow TCP 連接埠 80 上的流量：

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

將 hello 網路安全性群組與您的 VM 網路介面 (NIC) 產生關聯。 hello 下列範例將名為現有 NIC *myNic* hello 名為的網路安全性群組與*myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

或者，您可以將您的網路安全性群組與虛擬網路子網路，而不是只 toohello 網路介面上之單一 VM。 hello 下列範例將現有的子網路，名為*mySubnet*在 hello *myVnet* hello 名為的網路安全性群組與虛擬網路*myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>網路安全性群組的詳細資訊
這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。 網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。 您可以深入了解 [建立網路安全性群組和 ACL 規則](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。

您可以在 Azure Resource Manager 範本中定義網路安全性群組和 ACL 規則。 深入了解 [使用範本建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-template.md)。

如果您需要 toouse 唯一外部連接埠 tooan 內部連接埠的連接埠轉送 toomap VM 上，使用 負載平衡器和網路位址轉譯 (NAT) 規則。 例如，您可能想 tooexpose TCP 連接埠 8080 外部並且流量導向 tooTCP 連接埠 80 上的 VM。 您可以深入了解 [建立網際網路面向的負載平衡器](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)。

## <a name="next-steps"></a>後續步驟
在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。 您可以找到有關 hello 下列文件中建立更詳細的環境：

* [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)
* [什麼是網路安全性群組 (NSG)？](../../virtual-network/virtual-networks-nsg.md)
* [負載平衡器的 Azure Resource Manager 概觀](../../load-balancer/load-balancer-arm.md)

