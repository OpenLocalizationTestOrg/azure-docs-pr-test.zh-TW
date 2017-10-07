---
title: "在具有多個 Nic 的 Azure Linux VM aaaCreate |Microsoft 文件"
description: "了解如何將 toocreate Linux VM 具有多個 Nic 附加 tooit 使用 hello Azure CLI 2.0 或資源管理員範本。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>如何 toocreate Azure 中 Linux 虛擬機器，與多個網路介面卡
您可以在具有多個虛擬網路介面 (Nic) 附加 tooit Azure 中建立虛擬機器 (VM)。 常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。 這篇文章說明如何 toocreate 具有多個 Nic VM 附加 tooit 以及如何從現有的 VM tooadd 或移除 Nic。 如需詳細資訊，包括如何 toocreate 內您自己的多個 Nic 撞指令碼，深入了解[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。 不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。

這篇文章說明具有使用多個 Nic VM 的 toocreate hello Azure CLI 2.0 的方式。 您也可以執行下列步驟以 hello [Azure CLI 1.0](multiple-nics-nodejs.md)。


## <a name="create-supporting-resources"></a>建立支援資源
最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。

首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。 hello 下列範例會建立虛擬網路，名為*myVnet*和名為的子網路*mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

建立子網路與 hello 後端流量[az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)。 hello 下列範例會建立名為的子網路*mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>建立及設定多個 NIC
使用 [az network nic create](/cli/azure/network/nic#create) 建立兩個 NIC。 hello 下列範例會建立兩個 Nic，名為*myNic1*和*myNic2*、 相互連結 hello 網路安全性群組，具有一個 NIC 連接 tooeach 子網路：

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>建立 VM，並且附加 hello Nic
當您建立指定 hello Nic hello VM，您建立與`--nics`。 您也需要 tootake 小心，當您選取 hello VM 大小。 沒有限制，您可以加入 tooa VM 之 Nic 的 hello 總數。 深入了解 [Linux VM 大小](sizes.md)。 

使用 [az vm create](/cli/azure/vm#create) 來建立 VM。 hello 下列範例會建立名為的 VM *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>新增 NIC tooa VM
建立具有多個 Nic VM hello 的上一個步驟。 您也可以加入 Nic tooan hello Azure CLI 2.0 與現有的 VM。 

使用 [az network nic create](/cli/azure/network/nic#create) 建立另一個 NIC。 hello 下列範例會建立名為的 NIC *myNic3* toohello 後端子網路與網路安全性群組 hello 前述步驟中建立連接：

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd NIC tooan 現有 VM，第一次解除配置 hello 與 VM [az vm 解除配置](/cli/azure/vm#deallocate)。 hello 下列範例會取消配置 hello 名為 VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

新增 hello 與 NIC [az vm nic 新增](/cli/azure/vm/nic#add)。 hello 下列範例會將*myNic3*太*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

啟動 hello 與 VM [az vm 啟動](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>從 VM 中移除 NIC
tooremove NIC，以從現有的 VM，第一次解除配置 hello VM 與[az vm 解除配置](/cli/azure/vm#deallocate)。 hello 下列範例會取消配置 hello 名為 VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

移除 hello 與 NIC [az vm nic 移除](/cli/azure/vm/nic#remove)。 hello 下列範例會移除*myNic3*從*myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

啟動 hello 與 VM [az vm 啟動](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
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
檢閱[Linux VM 大小](sizes.md)toocreating 具有多個 Nic 的 VM 時。 請注意 toohello 最大的 Nic 數目在支援每個 VM 的大小。 
