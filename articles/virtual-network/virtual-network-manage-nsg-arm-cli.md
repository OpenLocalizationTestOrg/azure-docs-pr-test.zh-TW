---
title: "aaaManage 網路安全性群組-Azure CLI 2.0 |Microsoft 文件"
description: "了解如何使用將 toomanage 網路安全性群組 hello Azure 命令列介面 (CLI) 2.0。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="ff6a9-103">管理使用 hello Azure CLI 2.0 的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ff6a9-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ff6a9-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="ff6a9-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ff6a9-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ff6a9-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="ff6a9-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ff6a9-107">[Azure CLI 2.0](#View-existing-NSGs) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="ff6a9-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ff6a9-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff6a9-109">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="ff6a9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff6a9-110">Prerequisite</span></span>
<span data-ttu-id="ff6a9-111">如果您尚未，安裝並設定最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="ff6a9-112">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="ff6a9-112">View existing NSGs</span></span>
<span data-ttu-id="ff6a9-113">tooview hello 清單 Nsg 在特定的資源群組中，執行 hello [az 網路 nsg 清單](/cli/azure/network/nsg#list)命令搭配`-o table`輸出格式：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="ff6a9-114">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ff6a9-115">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="ff6a9-115">List all rules for an NSG</span></span>
<span data-ttu-id="ff6a9-116">名為 NSG tooview hello 規則**NSG 前端**中執行的 hello [az 網路 nsg 顯示](/cli/azure/network/nsg#show)命令使用[JMESPATH 查詢篩選器](/cli/azure/query-az-cli2)和 hello`-o table`輸出格式：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="ff6a9-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="ff6a9-118">您也可以使用[az 網路 nsg 規則清單](/cli/azure/network/nsg/rule#list)toolist 只有 hello 自訂規則從 NSG。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="ff6a9-119">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="ff6a9-119">View NSG associations</span></span>

<span data-ttu-id="ff6a9-120">tooview 哪些資源 hello **NSG 前端**NSG 為關聯，請執行 hello`az network nsg show`命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="ff6a9-121">尋找 hello **networkInterfaces**和**子網路**屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="ff6a9-122">在 hello 上述範例中，不是 NSG hello 關聯 tooany 網路介面 (Nic)，而且它是相關聯的 tooa 名為的子網路**前端**。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="ff6a9-123">新增規則</span><span class="sxs-lookup"><span data-stu-id="ff6a9-123">Add a rule</span></span>
<span data-ttu-id="ff6a9-124">規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff6a9-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="ff6a9-125">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="ff6a9-126">變更規則</span><span class="sxs-lookup"><span data-stu-id="ff6a9-126">Change a rule</span></span>
<span data-ttu-id="ff6a9-127">建立上述 tooallow toochange hello 規則輸入流量從 hello**網際網路**僅執行 hello [az 網路 nsg 規則更新](/cli/azure/network/nsg/rule#update)命令：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="ff6a9-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="ff6a9-129">刪除規則</span><span class="sxs-lookup"><span data-stu-id="ff6a9-129">Delete a rule</span></span>
<span data-ttu-id="ff6a9-130">toodelete hello 建立規則，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff6a9-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="ff6a9-131">關聯 NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="ff6a9-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="ff6a9-132">tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，使用 hello [az 網路 nic 更新](/cli/azure/network/nic#update)命令：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="ff6a9-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ff6a9-134">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="ff6a9-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="ff6a9-135">toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，執行 hello [az 網路 nsg 規則更新](/cli/azure/network/nsg/rule#update)命令一次，但取代 hello `--network-security-group`引數與空字串 (`""`)。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="ff6a9-136">在 hello 輸出 hello `networkSecurityGroup` toonull 設定機碼。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ff6a9-137">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="ff6a9-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="ff6a9-138">toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路，再次執行 hello [az 網路 nsg 規則更新](/cli/azure/network/nsg/rule#update)命令一次，但取代 hello `--network-security-group`引數與空字串 (`""`)。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="ff6a9-139">在 hello 輸出 hello `networkSecurityGroup` toonull 設定機碼。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="ff6a9-140">NSG tooa 子網路建立關聯</span><span class="sxs-lookup"><span data-stu-id="ff6a9-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="ff6a9-141">tooassociate hello **NSG 前端**NSG toohello**前端**子網路同樣地，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff6a9-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="ff6a9-142">在 hello 輸出 hello`networkSecurityGroup`金鑰都有類似的 hello 值的項目：</span><span class="sxs-lookup"><span data-stu-id="ff6a9-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="ff6a9-143">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="ff6a9-143">Delete an NSG</span></span>
<span data-ttu-id="ff6a9-144">如果它不是相關聯 tooany 資源，您只能刪除 NSG。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="ff6a9-145">toodelete NSG 關聯，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="ff6a9-146">toocheck hello 資源相關聯 tooan NSG，執行 hello`azure network nsg show`中所示[檢視 Nsg 關聯](#View-NSGs-associations)。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="ff6a9-147">如果 hello NSG 相關聯的 tooany Nic，請執行 hello`azure network nic set`中所示[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)的每個 nic。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="ff6a9-148">如果 hello NSG 相關聯的 tooany 子網路，請執行 hello`azure network vnet subnet set`中所示[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)每個子網路。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="ff6a9-149">toodelete hello NSG，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff6a9-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="ff6a9-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff6a9-150">Next steps</span></span>
* <span data-ttu-id="ff6a9-151">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="ff6a9-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

