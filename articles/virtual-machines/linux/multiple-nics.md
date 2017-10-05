---
title: "在 Azure 中建立連接多個 NIC 的 Linux VM | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 或 Resource Manager 範本，來建立連結多個 NIC 的 Linux VM。"
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
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>如何在 Azure 中建立有多個網路介面卡的 Linux 虛擬機器
您可以在 Azure 中，建立連接多個虛擬網路介面 (NIC) 的虛擬機器 (VM)。 常見案例是有不同的子網路可用於前端和後端連線，或者專門用來監視或備份解決方案的網路。 本文詳細說明如何建立連接多個 NIC 的 VM，以及如何在現有的 VM 中新增或移除 NIC。 如需詳細資訊，包括如何在自己的 Bash 指令碼內建立多個 NIC，請深入了解 [部署多個 NIC 的 VM](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)。 不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。

本文詳述如何使用 Azure CLI 2.0 建立具有多個 NIC 的 VM。 您也可以使用 [Azure CLI 1.0](multiple-nics-nodejs.md) 來執行這些步驟。


## <a name="create-supporting-resources"></a>建立支援資源
請安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。

在下列範例中，請以您自己的值取代範例參數名稱。 範例參數名稱包含 myResourceGroup、mystorageaccount 和 myVM。

首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：

```azurecli
az group create --name myResourceGroup --location eastus
```

使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。 下列範例會建立名為 myVnet 的虛擬網路和名為 mySubnetFrontEnd 的子網路：

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

使用 [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) 建立後端流量的子網路。 下列範例會建立名為 mySubnetBackEnd 的子網路：

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。 下列範例建立名為 myNetworkSecurityGroup 的網路安全性群組：

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>建立及設定多個 NIC
使用 [az network nic create](/cli/azure/network/nic#create) 建立兩個 NIC。 下列範例會建立兩個連接網路安全性群組的 NIC (名為 myNic1 和 myNic2)，以及一個連接到各個子網路的 NIC：

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

## <a name="create-a-vm-and-attach-the-nics"></a>建立 VM 並附加 NIC
當您建立 VM 時，指定您使用 `--nics` 建立的 NIC。 當您選取 VM 大小時也需多加注意。 您可以新增至 VM 的 NIC 總數是有限制的。 深入了解 [Linux VM 大小](sizes.md)。 

使用 [az vm create](/cli/azure/vm#create) 建立 VM。 下列範例會建立名為 myVM 的 VM：

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

## <a name="add-a-nic-to-a-vm"></a>將 NIC 新增至 VM
先前的步驟建立了一個有多個 NIC 的 VM。 您也可以使用 Azure CLI 2.0 將 NIC 新增至現有的 VM。 

使用 [az network nic create](/cli/azure/network/nic#create) 建立另一個 NIC。 下列範例會建立一個名為 myNic3 的 NIC，此 NIC會連線到後端子網路與在先前步驟中建立的網路安全性群組：

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

若要將 NIC 新增至現有的 VM，請先使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM。 下列範例會解除配置名為 myVM 的 VM：

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

使用 [az vm nic add](/cli/azure/vm/nic#add) 新增 NIC。 下列範例將 myNic3 新增至 myVM：

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

使用 [az vm start](/cli/azure/vm#start) 啟用 VM：

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>從 VM 中移除 NIC
若要將 NIC 從現有的 VM 中移除，請先使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM。 下列範例會解除配置名為 myVM 的 VM：

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

使用 [az vm nic remove](/cli/azure/vm/nic#remove) 移除 NIC。 下列範例會將 myNic3 從 myVM 中移除：

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

使用 [az vm start](/cli/azure/vm#start) 啟用 VM：

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>使用 Resource Manager 範本建立多個 NIC
Azure Resource Manager 範本會使用宣告式 JSON 檔案來定義您的環境。 您可以閱讀 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。 Resource Manager 範本提供一種方式，可在部署期間建立資源的多個執行個體，例如建立多個 NIC。 您使用 *copy* 來指定要建立的執行個體數目：

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

深入了解[使用 *copy* 建立多個執行個體](../../resource-group-create-multiple.md)。 

您也可以使用 `copyIndex()`，然後在資源名稱後面附加一個數字，讓您能夠建立 `myNic1`、`myNic2`，依此類推。以下顯示附加索引值的範例：

```json
"name": "[concat('myNic', copyIndex())]", 
```

您可以閱讀 [使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。

## <a name="next-steps"></a>後續步驟
當您嘗試建立一個有多個 NIC 的 VM 時，請檢閱 [Linux VM 大小](sizes.md)。 注意每個 VM 大小所支援的 NIC 數目上限。 