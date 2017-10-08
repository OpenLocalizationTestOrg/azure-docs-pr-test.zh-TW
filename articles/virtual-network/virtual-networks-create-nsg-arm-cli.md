---
title: "aaaCreate 網路安全性群組-Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署使用 hello Azure CLI 2.0 的網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="6437e-103">建立網路安全性群組，使用 Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="6437e-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6437e-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="6437e-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="6437e-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="6437e-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="6437e-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="6437e-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="6437e-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="6437e-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="6437e-108">hello 範例 Azure CLI 2.0 命令下列預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="6437e-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="6437e-109">建立 hello NSG hello`FrontEnd`子網路</span><span class="sxs-lookup"><span data-stu-id="6437e-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="6437e-110">toocreate NSG 名為*NSG 前端*根據上述的 hello 情況，請遵循 hello 步驟下列。</span><span class="sxs-lookup"><span data-stu-id="6437e-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="6437e-111">如果您尚未，安裝並設定最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="6437e-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="6437e-112">建立使用 hello NSG [az 網路 nsg 建立](/cli/azure/network/nsg#create)命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="6437e-113">參數：</span><span class="sxs-lookup"><span data-stu-id="6437e-113">Parameters:</span></span>
   
   * <span data-ttu-id="6437e-114">`--resource-group`: Hello hello NSG 建立所在的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="6437e-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="6437e-115">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="6437e-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="6437e-116">`--location`: Azure hello 新的 NSG 建立所在的區域。</span><span class="sxs-lookup"><span data-stu-id="6437e-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="6437e-117">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="6437e-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="6437e-118">`--name`: Hello 名稱新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="6437e-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="6437e-119">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="6437e-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="6437e-120">hello 預期輸出為相當多的資訊，包括所有 hello 預設規則的清單。</span><span class="sxs-lookup"><span data-stu-id="6437e-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="6437e-121">hello 下列範例示範使用 JMESPATH 查詢篩選器以 hello hello 預設規則`table`輸出格式：</span><span class="sxs-lookup"><span data-stu-id="6437e-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="6437e-122">輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="6437e-123">建立一個規則，允許存取 tooport 3389 (RDP) 從 hello 網際網路以 hello [az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6437e-124">根據您使用的 hello 殼層，您可能需要 toomodify hello `*` hello 引數，因此為未 tooexpand hello 引數後面之前執行中的字元。</span><span class="sxs-lookup"><span data-stu-id="6437e-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="6437e-125">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="6437e-126">參數：</span><span class="sxs-lookup"><span data-stu-id="6437e-126">Parameters:</span></span>

    * <span data-ttu-id="6437e-127">`--resource-group testrg`: hello 資源群組 toouse。</span><span class="sxs-lookup"><span data-stu-id="6437e-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="6437e-128">請注意，此參數不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6437e-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="6437e-129">`--nsg-name NSG-FrontEnd`: Hello NSG 中的 hello 建立規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="6437e-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="6437e-130">`--name rdp-rule`: Hello 新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="6437e-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="6437e-131">`--access Allow`： hello 規則 （拒絕或允許） 存取層級。</span><span class="sxs-lookup"><span data-stu-id="6437e-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="6437e-132">`--protocol Tcp`︰通訊協定 (Tcp、Udp 或 *)。</span><span class="sxs-lookup"><span data-stu-id="6437e-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="6437e-133">`--direction Inbound`: Hello 連線 （輸入或輸出） 的方向。</span><span class="sxs-lookup"><span data-stu-id="6437e-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="6437e-134">`--priority 100`: Hello 規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="6437e-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="6437e-135">`--source-address-prefix Internet`：CIDR 中的來源位址首碼或使用預設標籤。</span><span class="sxs-lookup"><span data-stu-id="6437e-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="6437e-136">`--source-port-range "*"`：來源連接埠或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="6437e-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="6437e-137">開啟 hello 連接的連接埠。</span><span class="sxs-lookup"><span data-stu-id="6437e-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="6437e-138">`--destination-address-prefix "*"`：CIDR 中的目的地位址首碼或使用預設標籤。</span><span class="sxs-lookup"><span data-stu-id="6437e-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="6437e-139">`--destination-port-range 3389`：目的地連接埠或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="6437e-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="6437e-140">收到 hello 連線要求的連接埠。</span><span class="sxs-lookup"><span data-stu-id="6437e-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="6437e-141">建立一個規則，允許從 hello 網際網路存取 tooport 80 (HTTP) **az 網路 nsg 規則建立**命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="6437e-142">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="6437e-143">繫結 hello NSG toohello**前端**子網路與 hello [az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="6437e-144">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="6437e-145">建立 hello NSG hello`BackEnd`子網路</span><span class="sxs-lookup"><span data-stu-id="6437e-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="6437e-146">toocreate NSG 名為*NSG 後端*根據上述的 hello 情況，請遵循 hello 步驟下列。</span><span class="sxs-lookup"><span data-stu-id="6437e-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="6437e-147">建立 hello `NSG-BackEnd` NSG 與**az 網路 nsg 建立**。</span><span class="sxs-lookup"><span data-stu-id="6437e-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="6437e-148">依照步驟 2，上述，hello 預期的輸出為非常大，包括預設規則。</span><span class="sxs-lookup"><span data-stu-id="6437e-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="6437e-149">建立一個規則，允許存取 tooport 1433 (SQL) 從 hello`FrontEnd`子網路與 hello **az 網路 nsg 規則建立**命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="6437e-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="6437e-151">建立規則，拒絕存取 toohello 網際網路使用 hello **az 網路 nsg 規則建立**命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="6437e-152">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="6437e-153">繫結 hello NSG toohello`BackEnd`子網路使用 hello **az 網路 vnet 子網路集合**命令。</span><span class="sxs-lookup"><span data-stu-id="6437e-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="6437e-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6437e-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
