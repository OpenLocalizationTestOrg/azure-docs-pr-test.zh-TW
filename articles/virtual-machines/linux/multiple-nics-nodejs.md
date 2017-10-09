---
title: "在具有多個 Nic 的 Azure Linux VM aaaCreate |Microsoft 文件"
description: "了解如何將 toocreate Linux VM 具有多個 Nic 附加 tooit 使用 hello Azure CLI 或資源管理員範本。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>建立 Linux 虛擬機器具有使用 Azure CLI 1.0 hello 的多個 Nic
您可以在具有多個虛擬網路介面 (Nic) 附加 tooit Azure 中建立虛擬機器 (VM)。 常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。 本文章提供快速命令 toocreate 具有多個 Nic 附加 tooit 的 VM。 如需詳細資訊，包括如何 toocreate 內您自己的多個 Nic 撞指令碼，深入了解[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。 不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。

> [!WARNING]
> 您必須在建立 VM，而您無法加入現有的 VM 以 hello Azure CLI 1.0 Nic tooan 附加多個 Nic。 您可以[加入現有的 VM 以 hello Azure CLI 2.0 Nic tooan](multiple-nics.md)。 您也可以[建立 hello 原始虛擬磁碟為基礎的 VM](copy-vm.md)並在您將部署的 hello VM 建立多個 Nic。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#create-supporting-resources) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](multiple-nics.md) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="create-supporting-resources"></a>建立支援資源
請確定您擁有 hello [Azure CLI](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。

首先，建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
azure group create myResourceGroup --location eastus
```

建立儲存體帳戶 toohold Vm。 hello 下列範例會建立名為的儲存體帳戶*mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

建立虛擬網路 tooconnect Vm。 hello 下列範例會建立虛擬網路，名為*myVnet*位址前置詞的*192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

建立兩個虛擬網路子網路 - 一個用於前端流量，另一個用於後端流量。 hello 下列範例會建立兩個子網路，名為*mySubnetFrontEnd*和*mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>建立及設定多個 NIC
您可以閱讀更多詳細資料[部署多個 Nic 使用 hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)，包括指令碼的迴圈 toocreate 所有 hello Nic hello 程序。

hello 下列範例會建立兩個 Nic，名為*myNic1*和*myNic2*，具有一個 NIC 連接 tooeach 子網路：

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

通常您也會建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)toohelp 管理，以及將流量分散到您的 Vm。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

繫結程式 Nic toohello 網路安全性群組，請使用`azure network nic set`。 hello 下列範例會繫結*myNic1*和*myNic2*與*myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>建立 VM，並且附加 hello Nic
在建立 hello VM 時，您現在可以指定多個 Nic。 而使用`--nic-name`tooprovide 單一 NIC，改用`--nic-names`，並提供以逗號分隔清單的 Nic。 您也需要 tootake 小心，當您選取 hello VM 大小。 沒有限制，您可以加入 tooa VM 之 Nic 的 hello 總數。 深入了解 [Linux VM 大小](sizes.md)。 hello 下列範例示範如何 toospecify 多個 Nic 然後按一下 VM 大小，支援使用多個 Nic (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>使用 Resource Manager 範本建立多個 NIC
Azure 資源管理員範本使用宣告式的 JSON 檔案 toodefine 環境。 您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。 資源管理員範本提供方式 toocreate 資源的多個執行個體在部署期間，例如建立多個 Nic。 您使用*複製*執行個體 toocreate toospecify hello 數目：

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。 

您也可以使用`copyIndex()`toothen 附加數字 tooa 資源名稱，可讓您 toocreate `myNic1`， `myNic2`，等 hello 下列範例示範附加 hello 索引值的範例：

```json
"name": "[concat('myNic', copyIndex())]", 
```

您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。

## <a name="next-steps"></a>後續步驟
請確定 tooreview [Linux VM 大小](sizes.md)toocreating 具有多個 Nic 的 VM 時。 請注意 toohello 最大的 Nic 數目在支援每個 VM 的大小。 

請記住，您無法再加入其他 Nic tooan 現有 VM，部署 hello VM 時，您必須建立所有 hello Nic。 請小心規劃您的部署 toomake 確定您已擁有 hello 開始所有 hello 所需的網路連線時。

