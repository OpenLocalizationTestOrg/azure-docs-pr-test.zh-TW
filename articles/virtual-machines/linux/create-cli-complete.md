---
title: "aaaCreate hello Azure CLI 2.0 的 Linux 環境 |Microsoft 文件"
description: "建立儲存體、 Linux VM、 虛擬網路和子網路、 負載平衡器、 NIC、 公用 IP 和網路安全性群組，全部從 hello 以使用 Azure CLI 2.0 hello 接地。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>建立完整的 Linux 虛擬機器以 hello Azure CLI
tooquickly 在 Azure 中建立虛擬機器 (VM)，您可以使用單一 Azure CLI 命令，會使用預設值 toocreate 任何必要的支援的資源。 系統會自動建立虛擬網路、公用 IP 位址及網路安全性群組規則等資源。 在實際執行環境的多個控制項使用，您可能建立事先這些資源，然後再新增 Vm toothem。 這篇文章會引導您完成 toocreate VM 和每個 hello 支援資源的一個。

請確定您有最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)和記錄的 tooan Azure 帳戶中[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。

## <a name="create-resource-group"></a>建立資源群組
Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 您必須在建立虛擬機器和支援虛擬網路支援之前，先建立資源群組。 建立 hello 資源群組與[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

根據預設，Azure CLI 命令的 hello 輸出已在 JSON （JavaScript 物件標記法）。 toochange hello 預設輸出 tooa 清單或資料表，比方說，使用[az 設定-輸出](/cli/azure/#configure)。 您也可以加入`--output`tooany 命令一次變更輸出格式。 hello 下列範例顯示 hello JSON 輸出 hello`az group create`命令：

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>建立虛擬網路和子網路
接著在 Azure 中建立虛擬網路並 toowhich 中的子網路，您可以建立您的 Vm。 使用[az 網路 vnet 建立](/cli/azure/network/vnet#create)toocreate 虛擬網路，名為*myVnet*以 hello *192.168.0.0/16*位址前置詞。 您也可以加入名為的子網路*mySubnet* hello 位址前置詞與*192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

hello 輸出會顯示為邏輯建立 hello 虛擬網路內的 hello 子網路：

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>建立公用 IP 位址
現在，讓我們使用 [az network public-ip create](/cli/azure/network/public-ip#create) 來建立公用 IP 位址。 這個公用 IP 位址可讓您 tooconnect tooyour Vm 從 hello 網際網路。 我們 hello 預設位址就是動態的因為也有建立具名的 DNS 項目以 hello`--domain-name-label`選項。 hello 下列範例會建立名為公用 IP *myPublicIP* hello DNS 名稱是*mypublicdns*。 由於 hello DNS 名稱必須是唯一的提供您自己唯一的 DNS 名稱：

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

輸出：

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>建立網路安全性群組
toocontrol hello 流量的流量進出您的 Vm 建立網路安全性群組。 網路安全性群組可以套用的 tooa NIC 或子網路。 hello 下列範例會使用[az 網路 nsg 建立](/cli/azure/network/nsg#create)toocreate 網路安全性群組名稱為*myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

您可以定義規則，允許或拒絕 hello 特定流量。 tooallow 22 (toosupport SSH) 連接埠上的傳入的連接建立輸入的 hello 與網路安全性群組規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow 傳入的連接的連接埠 80 （toosupport web 流量），加入另一個網路安全性群組規則。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

檢查網路安全性群組 hello 和規則[az 網路 nsg 顯示](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

輸出：

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>建立虛擬 NIC
因為您可以套用規則 tootheir 使用以程式設計方式使用虛擬網路介面卡 (Nic)。 您也可以有多個 NIC。 在 hello 下列[az 網路 nic 建立](/cli/azure/network/nic#create)命令時，建立名為的 NIC *myNic*並將它與 hello 網路安全性群組關聯。 hello 公用 IP 位址*myPublicIP*也都與 hello 虛擬 nic。

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

輸出：

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>建立可用性設定組
可用性設定組可協助將 VM 分散到容錯網域和更新網域。 即使您只能建立一個 VM 現在，它會是最佳作法 toouse 可用性集 toomake 它更容易在未來的 hello tooexpand。 

容錯網域定義一個虛擬機器群組，且群組內的虛擬機器會共用通用電源和網路交換器。 根據預設，設定您的可用性設定組中的 hello 虛擬機器之間隔開向上 toothree 容錯網域。 其中一個容錯網域中的硬體問題並不會影響每個執行您應用程式的 VM。

更新網域會指出群組的虛擬機器，可以在 hello 重新開機的基礎實體硬體相同的時間。 在計劃的維護期間網域重新開機的更新中的 hello 順序可能不是循序的但只能有一個更新網域重新開機一次。

Azure 會將它們放置於可用性集合時，將 Vm 會自動分散到 hello 容錯網域和更新網域。 如需詳細資訊，請參閱[管理的 Vm hello 可用性](manage-availability.md)。

請使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 來建立 VM 的可用性設定組。 hello 下列範例會建立可用性設定組具名*myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

hello 輸出備忘稿容錯網域和更新網域：

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>建立 hello Linux Vm
您已建立 hello 網路資源 toosupport 可存取網際網路的 Vm。 現在，請建立 VM 並使用 SSH 金鑰來保護它。 在此情況下，我們會的 toocreate Ubuntu VM 根據 hello 最近 LTS。 您可以使用 [az vm image list](/cli/azure/vm/image#list) 來找出其他映像，如[尋找 Azure VM 映像](cli-ps-findimage.md)所述。

我們也會指定的 SSH 金鑰 toouse 進行驗證。 如果您沒有 SSH 公開金鑰組，您可以[建立它們](mac-create-ssh-keys.md)或使用 hello`--generate-ssh-keys`參數 toocreate 以供您。 如果您已經有金鑰組，此參數就會使用 `~/.ssh` 中的現有金鑰。

透過將我們的所有資源和資訊與 hello 建立 hello VM [az vm 建立](/cli/azure/vm#create)命令。 hello 下列範例會建立名為的 VM *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM 以 hello 時建立 hello 公用 IP 位址所提供的 DNS 項目。 這`fqdn`hello 輸出中顯示為您建立您的 VM:

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

輸出：

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

您可以安裝 NGINX，並查看 hello 流量流程 toohello VM。 請依下列方式安裝 NGINX：

```bash
sudo apt-get install -y nginx
```

toosee hello 預設 NGINX 站台在動作中，開啟網頁瀏覽器，並輸入 FQDN:

![您 VM 上的預設 NGINX 站台](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>以範本形式匯出
如果您現在想 toocreate hello 與其他開發環境相同的參數或實際執行環境符合它嗎？ 資源管理員會使用 JSON 範本，以定義您的環境的所有 hello 參數。 您可以藉由參考此 JSON 範本來建置整個環境。 您可以[手動建立 JSON 範本](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或匯出為您現有環境 toocreate hello JSON 範本。 使用[az 群組匯出](/cli/azure/group#export)tooexport 您的資源群組，如下所示：

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

此命令會建立 hello`myResourceGroup.json`目前的工作目錄中的檔案。 當您從這個範本建立環境時，系統會提示您針對所有 hello 資源名稱。 您也可以加入 hello 範本檔案中填入這些名稱`--include-parameter-default-value`參數 toohello`az group export`命令。 編輯 JSON 範本 toospecify hello 資源檔名稱，或[建立 parameters.json 檔案](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)指定 hello 資源名稱。

從您的範本，使用環境 toocreate [az 群組部署建立](/cli/azure/group/deployment#create)，如下所示：

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

您可能會想 tooread[深入了解如何從範本 toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 了解如何 tooincrementally 更新環境中，使用 hello 參數檔案，以及從單一儲存體位置存取範本。

## <a name="next-steps"></a>後續步驟
您現在已經準備好 toobegin 使用多個網路元件和 Vm。 您可以使用這個範例環境 toobuild 出您的應用程式，此處使用 hello 導入的核心元件。
