---
title: "aaaOpen 連接埠 tooa Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Linux VM / 使用 hello Azure 資源管理員部署模型和 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>使用 Azure CLI hello 開啟連接埠和端點 tooa Linux VM
您開啟通訊埠，或建立端點，tooa Azure 虛擬機器 (VM) 中藉由建立子網路或 VM 網路介面上的網路篩選條件。 您收到 hello 流量的網路安全性群組附加 toohello 資源上放置控制輸入與輸出流量，這些篩選器。 讓我們使用連接埠 80 上的 Web 流量的常見範例。 本文章將示範如何 tooopen 以 hello Azure CLI 2.0 連接埠 tooa VM。 您也可以執行下列步驟以 hello [Azure CLI 1.0](nsg-quickstart-nodejs.md)。


## <a name="quick-commands"></a>快速命令
toocreate 網路安全性的群組和規則，您需要最新 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。

建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*在 hello *eastus*位置：

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

新增具有規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)tooallow HTTP 流量 tooyour 網頁伺服器 （或 調整成您自己的案例，例如 SSH 存取或資料庫連線）。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow TCP 連接埠 80 上的流量：

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

關聯 hello 網路安全性群組與您的 VM 網路介面 (NIC) [az 網路 nic 更新](/cli/azure/network/nic#update)。 hello 下列範例將名為現有 NIC *myNic* hello 名為的網路安全性群組與*myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

或者，您可以將您的網路安全性群組與虛擬網路子網路與[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)而不是只 toohello 網路介面上之單一 VM。 hello 下列範例將現有的子網路，名為*mySubnet*在 hello *myVnet* hello 名為的網路安全性群組與虛擬網路*myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>網路安全性群組的詳細資訊
這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。 網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。 您可以深入了解 [建立網路安全性群組和 ACL 規則](tutorial-virtual-network.md#secure-network-traffic)。

針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。 hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。 如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。

## <a name="next-steps"></a>後續步驟
在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。 您可以找到有關 hello 下列文件中建立更詳細的環境：

* [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)
* [什麼是網路安全性群組 (NSG)？](../../virtual-network/virtual-networks-nsg.md)
