---
title: "完整的 Linux 環境以 hello Azure CLI 1.0 aaaCreate |Microsoft 文件"
description: "建立儲存體、 Linux VM、 虛擬網路和子網路、 負載平衡器、 NIC、 公用 IP 和網路安全性群組，全部從 hello 以使用 Azure CLI 1.0 hello 接地。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>建立完整的 Linux 環境以 hello Azure CLI 1.0
在這篇文章中，我們將建立一個簡單的網路，當中包含一個負載平衡器，以及一組對開發和簡單運算而言相當實用的 VM。 我們逐步解說 hello 處理命令的命令，直到您有兩個工作，保護您可以連接從任何地方 hello 網際網路的 Linux Vm toowhich。 然後您可以移動 toomore 複雜網路和環境。

沿著 hello 一來，您深入了解 hello 依存性階層，hello Resource Manager 部署模型可讓您，並在它提供有關多少電力。 您會看到 hello 系統的建立方式之後，您可以重建更快速地使用[Azure 資源管理員範本](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 此外，您了解您環境的 hello 部分一起之後，請建立範本 tooautomate 它們可更輕鬆。

hello 環境包含：

* 兩個位於可用性設定組內的 VM。
* 一個在連接埠 80 有負載平衡規則的負載平衡器。
* 網路安全性群組 (NSG) 規則 tooprotect 垃圾流量從您的 VM。

toocreate 這個自訂的環境中，您需要最新的 hello [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Resource Manager 模式中 (`azure config mode arm`)。 您也需要 JSON 剖析工具。 此範例使用 [jq](https://stedolan.github.io/jq/)。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello hello 基底命令 tooupload VM tooAzure。 詳細資訊和內容的每個步驟可以在 hello 文件，開始的 hello rest[這裡](#detailed-walkthrough)。

請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)登入，並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。

建立 hello 資源群組。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`位置：

```azurecli
azure group create -n myResourceGroup -l westeurope
```

使用 hello JSON 剖析器，以確認 hello 資源群組：

```azurecli
azure group show myResourceGroup --json | jq '.'
```

建立 hello 儲存體帳戶。 hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`。 （hello 儲存體帳戶名稱必須是唯一的因此提供您自己的唯一名稱。)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

使用 hello JSON 剖析器，以確認 hello 儲存體帳戶：

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

建立 hello 虛擬網路。 hello 下列範例會建立虛擬網路，名為`myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

建立子網路。 hello 下列範例會建立名為的子網路`mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

請確認 hello 虛擬網路和子網路使用 hello JSON 剖析器：

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

建立公用 IP。 hello 下列範例會建立名為公用 IP `myPublicIP` hello DNS 名稱是`mypublicdns`。 （hello DNS 名稱必須是唯一的因此提供您自己的唯一名稱。)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

建立 hello 負載平衡器。 hello 下列範例會建立名為負載平衡器`myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

建立 hello 負載平衡器的前端 IP 集區，並關聯 hello 公用 IP。 hello 下列範例會建立名為前端的 IP 集區`mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

建立 hello hello 負載平衡器後端 IP 集區。 hello 下列範例會建立名為後端 IP 集區`myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

建立 SSH 輸入的網路位址轉譯 (NAT) 規則 hello 負載平衡器。 hello 下列範例會建立兩個負載平衡器規則，`myLoadBalancerRuleSSH1`和`myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

建立 hello web hello 的輸入的 NAT 規則的負載平衡器。 hello 下列範例會建立名為的負載平衡器規則`myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

建立 hello 負載平衡器健全狀況探查。 hello 下列範例會建立名為 TCP 探查`myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

請確認 hello 負載平衡器、 IP 集區和 NAT 規則使用 hello JSON 剖析器：

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

建立第一個網路介面卡 hello (NIC)。 取代 hello`#####-###-###`區段，並提供您自己的 Azure 訂用帳戶識別碼。 您的訂用帳戶 ID 述 hello 輸出**jq**檢查您要建立 hello 資源時。 您也可以使用 `azure account list`來檢視您的訂用帳戶識別碼。

hello 下列範例會建立名為的 NIC `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

建立 hello 第二個 nic。 hello 下列範例會建立名為的 NIC `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

使用 hello JSON 剖析器，以確認 hello 兩個 Nic:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

建立 hello 網路安全性群組。 hello 下列範例會建立名為的網路安全性群組`myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

加入網路安全性群組 hello 的兩個輸入的規則。 hello 下列範例會建立兩個規則，`myNetworkSecurityGroupRuleSSH`和`myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

使用 hello JSON 剖析器來驗證網路安全性群組 hello 和輸入的規則：

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Hello 網路安全性的繫結群組 toohello 兩個 Nic:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

建立 hello 可用性設定組。 hello 下列範例會建立可用性設定組具名`myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

建立 hello 第一個 Linux VM。 hello 下列範例會建立名為的 VM `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

建立 hello Linux VM 的第二個。 hello 下列範例會建立名為的 VM `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

使用的所有內容都已內建 hello JSON 剖析器 tooverify:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

匯出您新環境 tooa 範本 tooquickly 重新建立新的執行個體：

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說
hello 詳細的步驟，請依照下列說明每個命令為您建置您的環境執行的動作。 當您建置自己的自訂開發環境或生產環境時，這些概念會相當有用。

請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)登入，並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。

## <a name="create-resource-groups-and-choose-deployment-locations"></a>建立資源群組並選擇部署位置
Azure 資源群組是包含組態資訊和中繼資料 tooenable hello 邏輯管理的資源部署的部署邏輯實體。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`位置：

```azurecli
azure group create --name myResourceGroup --location westeurope
```

輸出：

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>建立儲存體帳戶
您需要儲存體帳戶用於您的 VM 磁碟和任何額外資料磁碟的 tooadd。 您幾乎是在建立資源群組之後立即建立儲存體帳戶。

我們在此使用 hello`azure storage account create`命令時，傳送嗨 hello 帳戶，hello 資源群組位置控制，以及您想要的儲存體支援 hello 型別。 hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

輸出：

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

我們的資源群組使用 hello tooexamine`azure group show`命令中，我們將使用 hello [jq](https://stedolan.github.io/jq/)工具以及 hello `--json` Azure CLI 選項。 (您可以使用**jsawk**或任何語言文件庫偏好 tooparse hello JSON。)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

輸出：

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

使用 hello CLI tooinvestigate hello 儲存體帳戶，您必須先 tooset hello 帳戶名稱和金鑰。 取代 hello hello 下列範例以您選擇的名稱中的 hello 儲存體帳戶名稱：

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

然後您就可以輕鬆地檢視您的儲存體資訊︰

```azurecli
azure storage container list
```

輸出：

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>建立虛擬網路和子網路
接下來您將 tooneed toocreate 執行於 Azure，您可以在其中建立 Vm 子網路的虛擬網路。 hello 下列範例會建立虛擬網路，名為`myVnet`以 hello`192.168.0.0/16`位址首碼：

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

輸出：

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

同樣地，我們使用的 hello-json 選項`azure group show`和`jq`toosee 如何對建置我們的資源。 我們現在有 `storageAccounts` 資源和 `virtualNetworks` 資源。  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

輸出：

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

現在讓我們來建立子網路中 hello`myVnet`哪些 hello 到已部署的 Vm 虛擬網路。 我們使用 hello`azure network vnet subnet create`命令，以及我們已經建立 hello 資源： hello`myResourceGroup`資源群組和 hello`myVnet`虛擬網路。 在下列範例的 hello，我們將新增名為 「 hello 」 子網路`mySubnet`hello 子網路位址首碼與`192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

輸出：

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

因為 hello 子網路是以邏輯方式 hello 虛擬網路內，所以我們查看 hello 與稍有不同的命令的子網路資訊。 我們使用 hello 命令是`azure network vnet show`，但我們繼續 tooexamine hello JSON 輸出使用`jq`。

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

輸出：

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>建立公用 IP 位址
現在讓我們來建立 hello 公用 IP 位址 (PIP)，我們將指派 tooyour 負載平衡器。 它可讓您從 hello 網際網路 tooconnect tooyour Vm 使用 hello`azure network public-ip create`命令。 Hello 預設位址就是動態的因為我們會建立具名的 DNS 項目在 hello **cloudapp.azure.com**網域使用 hello`--domain-name-label`選項。 hello 下列範例會建立名為公用 IP `myPublicIP` hello DNS 名稱是`mypublicdns`。 由於 hello DNS 名稱必須是唯一的您會提供您自己唯一的 DNS 名稱：

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

輸出：

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

hello 公用 IP 位址也是最上層的資源，因此您可以看到它與`azure group show`。

```azurecli
azure group show myResourceGroup --json | jq '.'
```

輸出：

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

您可以調查資源詳細資料，包括 hello 完整的網域名稱 (FQDN) 的 hello 子網域，使用完整的 hello`azure network public-ip show`命令。 就邏輯而言，已配置 hello 公用 IP 位址資源，但尚未指派特定的位址。 tooobtain IP 位址，您將 tooneed 我們尚未建立的負載平衡器。

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

輸出：

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>建立負載平衡器和 IP 集區
當您建立負載平衡器時，它可讓您 toodistribute 流量在多個 Vm。 它也會藉由執行多個回應 toouser 要求的維護或過重的 hello 事件中的 Vm 提供備援 tooyour 應用程式。 hello 下列範例會建立名為負載平衡器`myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

輸出：

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

我們的負載平衡器很空，因此讓我們建立一些 IP 集區。 我們要我們負載平衡器，一個用於 hello 前端，一個用於 hello 後端 toocreate 兩個 IP 集區。 hello 前端 IP 集區是公開可見的。 它也是 hello 位置 toowhich 我們指派 hello 我們稍早建立的 PIP。 然後我們用於 hello 後端集區做為位置到我們 Vm tooconnect。 這樣一來，hello 可以流量經過 hello 負載平衡器 toohello Vm。

首先，讓我們建立前端 IP 集區。 hello 下列範例會建立名為前端集區`myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

輸出：

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

請注意我們如何使用 hello `--public-ip-name` hello 中切換 toopass`myPublicIP`我們稍早建立的。 指派 hello 公用 IP 位址 toohello 負載平衡器可讓您 tooreach hello 網際網路跨 Vm。

接下來，讓我們建立第二個 IP 集區，這次是針對我們的後端流量。 hello 下列範例會建立名為後端集區`myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

輸出：

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

我們可以看到我們負載平衡器與查詢的執行方式`azure network lb show`和檢查 hello JSON 輸出：

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

輸出：

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>建立負載平衡器 NAT 規則
tooget 流量流經我們負載平衡器中，我們需要 toocreate 網路位址轉譯 (NAT) 規則，指定輸入或輸出的動作。 您可以指定 hello 通訊協定 toouse，然後將所需的外部連接埠 toointernal 連接埠對應。 在我們的環境，讓我們來建立 SSH 允許透過我們的負載平衡器 tooour Vm 一些規則。 我們在我們 Vm (我們稍後建立） 上設定 TCP 連接埠 4222 和 4223 toodirect tooTCP 連接埠 22。 hello 下列範例會建立名為的規則`myLoadBalancerRuleSSH1`toomap TCP 連接埠 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

輸出：

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

重複第二個 NAT 規則 SSH hello 程序。 hello 下列範例會建立名為的規則`myLoadBalancerRuleSSH2`toomap TCP 連接埠 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

我們也請繼續進行，並建立為接通 tooour IP 集區中的 hello 規則的網路傳輸的 TCP 連接埠 80 的 NAT 規則。 如果我們連接 hello 規則 tooan IP 集區，而不是個別連結 hello 規則 tooour Vm 我們可以新增或移除 hello IP 集區中的 Vm。 hello 負載平衡器會自動調整 hello 流量的流量。 hello 下列範例會建立名為的規則`myLoadBalancerRuleWeb`toomap TCP 連接埠 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

輸出：

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>建立負載平衡器健全狀況探查
定期的健全狀況探查 hello 位於我們確定它們正在操作和回應 toorequests 所定義的負載平衡器 toomake 後方的 Vm 上的檢查。 如果沒有，請從正在移除作業 tooensure 使用者未被導向 toothem。 您可以定義自訂檢查 hello 健全狀況探查，以及間隔和逾時值。 如需有關健全狀況探查的詳細資訊，請參閱 [負載平衡器探查](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 hello 下列範例會建立 TCP 健全狀況探查具名`myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

輸出：

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

在這裡，我們指定了 15 秒的健全狀況檢查間隔。 我們可以遺漏最多四個探查 （一分鐘） 後再 hello 負載平衡器會將視為該 hello 主機不再正常運作。

## <a name="verify-hello-load-balancer"></a>確認 hello 負載平衡器
現在已完成 hello 負載平衡器組態。 以下是您用 hello 步驟：

1. 您建立了負載平衡器。
2. 您建立前端的 IP 集區，並指派公用 IP tooit。
3. 您建立了 VM 可以連接的後端 IP 集區。
4. 您已建立 NAT 規則，以允許管理，並可讓我們的 web 應用程式的 TCP 連接埠 80 的規則的 SSH toohello Vm。
5. 您已新增健全狀況探查 tooperiodically 核取 hello Vm。 此健全狀況探查可確保使用者不試 tooaccess 不再運作或提供內容的 VM。

讓我們檢閱您負載平衡器現在的樣子︰

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

輸出：

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>以 hello Linux VM 建立 NIC toouse
因為您可以套用規則 tootheir 使用以程式設計方式使用 Nic。 您也可以有多個 NIC。 在 hello 下列`azure network nic create`命令時，則連結 hello NIC toohello 負載後端 IP 集區，並將它關聯以 hello NAT 規則 toopermit SSH 流量。

取代 hello`#####-###-###`區段，並提供您自己的 Azure 訂用帳戶識別碼。 您的訂用帳戶 ID 述 hello 輸出`jq`檢查您要建立 hello 資源時。 您也可以使用 `azure account list`來檢視您的訂用帳戶識別碼。

hello 下列範例會建立名為的 NIC `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

輸出：

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

您可以藉由直接檢查 hello 資源看到 hello 詳細資料。 使用 hello 檢查 hello 資源`azure network nic show`命令：

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

輸出：

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

現在我們建立 hello 再次攔截 tooour 後端 IP 集區中的第二個 NIC。 此時間 hello 第二個 NAT 規則允許 SSH 流量。 hello 下列範例會建立名為的 NIC `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>建立網路安全性群組和規則
現在我們建立網路安全性群組並 hello 控管的輸入的規則存取 toohello nic。 網路安全性群組可以套用的 tooa NIC 或子網路。 您可以定義規則 toocontrol hello 流量的流量進出您的 Vm。 hello 下列範例會建立名為的網路安全性群組`myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

讓我們加入 hello 傳入的 hello NSG tooallow 規則輸入連接埠 22 (toosupport SSH) 連線。 hello 下列範例會建立名為的規則`myNetworkSecurityGroupRuleSSH`tooallow 上的 tcp 通訊埠 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

現在讓我們加入 hello 傳入的 hello NSG tooallow 規則輸入連接埠 80 （toosupport web 流量） 上的連線。 hello 下列範例會建立名為的規則`myNetworkSecurityGroupRuleHTTP`tooallow TCP 連接埠 80 上：

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> hello 輸入的規則是輸入的網路連線的篩選。 在此範例中，我們將繫結 hello NSG toohello Vm 虛擬 NIC，這表示任何要求 tooport 22 傳遞 toohello NIC 透過我們的 VM 上。 這個輸入規則與網路連線相關，而不是與端點 (在傳統部署中會相關的對象) 相關。 tooopen 連接埠，您必須保留 hello`--source-port-range`設定得 '\*' （hello 預設值） tooaccept 傳入要求從**任何**要求連接埠。 連接埠通常是動態的。
>
>

## <a name="bind-toohello-nic"></a>繫結 toohello NIC
繫結 hello NSG toohello Nic。 我們需要 tooconnect 我們 Nic 與我們的網路安全性群組。 執行這兩個命令，設定這兩個我們 Nic toohook:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>建立可用性設定組
可用性設定組可協助將 VM 分散到容錯網域和升級網域。 為 VM 建立可用性設定組。 hello 下列範例會建立可用性設定組具名`myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

容錯網域定義一個虛擬機器群組，且群組內的虛擬機器會共用通用電源和網路交換器。 根據預設，設定您的可用性設定組中的 hello 虛擬機器之間隔開向上 toothree 容錯網域。 hello 的做法是在其中一個錯誤網域中的硬體問題不會影響正在執行您的應用程式的每個 VM。 Azure 會將它們放置於可用性集合時，將 Vm 會自動分散到 hello 容錯網域。

升級網域會指出群組的虛擬機器，可以在 hello 重新開機的基礎實體硬體相同的時間。 重新啟動升級網域的 hello 順序可能不循序計劃在維護期間，但是只有一個升級一次重新開機時。 同樣地，將多個 VM 放在一個可用性設定網站中時，Azure 會自動將它們分散到升級網域。

深入了解[管理的 Vm hello 可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="create-hello-linux-vms"></a>建立 hello Linux Vm
您已經建立可存取網際網路的 toosupport Vm hello 儲存體和網路資源。 現在，讓我們建立這些 VM，並利用沒有密碼的 SSH 金鑰來保障其安全。 在此情況下，我們會的 toocreate Ubuntu VM 根據 hello 最近 LTS。 我們會使用 `azure vm image list`來找出該映像資訊 (如 [尋找 Azure VM 映像](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)所述)。

我們選取映像使用 hello 命令`azure vm image list westeurope canonical | grep LTS`。 在此案例中，我們會使用 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`。 Hello 最後一個欄位中，我們傳遞`latest`以便 hello 未來，我們一律取得 hello 最新的組建。 (我們使用 hello 字串是`canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`)。

下一個步驟是熟悉 tooanyone 人員已經建立 ssh 金鑰的 rsa 公開金鑰和私密金鑰配對 Linux 或 Mac 上使用**透過像是-t rsa-b 2048**。 如果您的 `~/.ssh` 目錄中沒有任何憑證金鑰組，您可以建立它們︰

* 自動透過 hello`azure vm create --generate-ssh-keys`選項。
* 使用由手動[hello 指示 toocreate 它們自己](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

或者，您可以使用 hello`--admin-password`方法 tooauthenticate 建立 SSH 連線之後 hello VM。 這個方法通常較不安全。

我們會帶我們所有的資源和資訊與 hello 建立 hello VM`azure vm create`命令：

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

輸出：

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

您可以立即使用預設的 SSH 金鑰連接 tooyour VM。 請確定您指定 hello 適當的連接埠，因為我們通過 hello 負載平衡器。 （我們的第一個 vm，我們設定 hello NAT 規則 tooforward 連接埠 4222 tooour VM。）

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

輸出：

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

繼續並建立第二個 VM hello 中相同的方式：

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

您現在可以使用 hello 和`azure vm show myResourceGroup myVM1`命令 tooexamine 您已建立。 此時，您的 Ubuntu VM 是在 Azure 中的負載平衡器後方執行，您只能利用 SSH 金鑰組來登入 (因為密碼已被停用)。 您可以安裝 nginx 或 httpd、 部署 web 應用程式，並查看 hello 流量流經 hello 負載平衡器 tooboth 的 hello Vm。

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

輸出：

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>匯出 hello 環境做為範本
既然您已經出此環境中，如果您想 toocreate 建立額外的開發環境以 hello 相同的參數或實際執行環境符合它嗎？ 資源管理員會使用 JSON 範本，以定義您的環境的所有 hello 參數。 您可以藉由參考此 JSON 範本來建置整個環境。 您可以[手動建立 JSON 範本](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或匯出為您現有環境 toocreate hello JSON 範本：

```azurecli
azure group export --name myResourceGroup
```

此命令會建立 hello`myResourceGroup.json`目前的工作目錄中的檔案。 當您從這個範本建立環境時，系統會提示您針對所有 hello 資源名稱，包括 hello hello 負載平衡器、 網路介面或 Vm 的名稱。 您也可以加入 hello 範本檔案中填入這些名稱`-p`或`--includeParameterDefaultValue`參數 toohello`azure group export`稍早所示的命令。 編輯 JSON 範本 toospecify hello 資源檔名稱，或[建立 parameters.json 檔案](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)指定 hello 資源名稱。

toocreate 的環境，從您的範本：

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

您可能會想 tooread[深入了解如何從範本 toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 了解如何 tooincrementally 更新環境中，使用 hello 參數檔案，以及從單一儲存體位置存取範本。

## <a name="next-steps"></a>後續步驟
您現在已經準備好 toobegin 使用多個網路元件和 Vm。 您可以使用這個範例環境 toobuild 出您的應用程式，此處使用 hello 導入的核心元件。
