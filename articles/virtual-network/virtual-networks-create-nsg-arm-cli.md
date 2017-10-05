---
title: "建立網路安全性群組 - Azure CLI 2.0 | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 建立和部署網路安全性群組。"
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
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="25193-103">使用 Azure CLI 2.0 建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="25193-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="25193-104">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="25193-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="25193-105">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="25193-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="25193-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – 適用於傳統和資源管理部署模型的 CLI</span><span class="sxs-lookup"><span data-stu-id="25193-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="25193-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - 適用於資源管理部署模型的新一代 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="25193-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="25193-108">以下的 Azure CLI 2.0 命令範例是假設您已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="25193-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="25193-109">建立 `FrontEnd` 子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="25193-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="25193-110">若要根據上述案例建立名為 *NSG-FrontEnd* 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="25193-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="25193-111">安裝及設定最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) (若您尚未這麼做)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="25193-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="25193-112">使用 [az network nsg create](/cli/azure/network/nsg#create) 命令建立 NSG。</span><span class="sxs-lookup"><span data-stu-id="25193-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="25193-113">參數：</span><span class="sxs-lookup"><span data-stu-id="25193-113">Parameters:</span></span>
   
   * <span data-ttu-id="25193-114">`--resource-group`：要在其中建立 NSG 之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="25193-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="25193-115">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="25193-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="25193-116">`--location`：要在其中建立新 NSG 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="25193-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="25193-117">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="25193-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="25193-118">`--name`：新 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="25193-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="25193-119">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="25193-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="25193-120">預期的輸出會是相當多的資訊，包括所有預設規則的清單。</span><span class="sxs-lookup"><span data-stu-id="25193-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="25193-121">下列範例顯示搭配使用 JMESPATH 查詢篩選和 `table` 輸出格式的預設規則︰</span><span class="sxs-lookup"><span data-stu-id="25193-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="25193-122">輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="25193-123">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 命令來建立規則，允許從網際網路存取連接埠 3389 (RDP)。</span><span class="sxs-lookup"><span data-stu-id="25193-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="25193-124">根據您所使用的殼層，您可能需要修改下列引數中的 `*` 字元，以免在執行之前就展開引數。</span><span class="sxs-lookup"><span data-stu-id="25193-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
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
   
    <span data-ttu-id="25193-125">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-125">Expected output:</span></span>
   
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

    <span data-ttu-id="25193-126">參數：</span><span class="sxs-lookup"><span data-stu-id="25193-126">Parameters:</span></span>

    * <span data-ttu-id="25193-127">`--resource-group testrg`：要使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="25193-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="25193-128">請注意，此參數不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="25193-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="25193-129">`--nsg-name NSG-FrontEnd`：要在其中建立規則之 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="25193-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="25193-130">`--name rdp-rule`：新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="25193-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="25193-131">`--access Allow`：規則 (拒絕或允許) 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="25193-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="25193-132">`--protocol Tcp`︰通訊協定 (Tcp、Udp 或 *)。</span><span class="sxs-lookup"><span data-stu-id="25193-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="25193-133">`--direction Inbound`：連線 (輸入或輸出) 的方向。</span><span class="sxs-lookup"><span data-stu-id="25193-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="25193-134">`--priority 100`：規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="25193-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="25193-135">`--source-address-prefix Internet`：CIDR 中的來源位址首碼或使用預設標籤。</span><span class="sxs-lookup"><span data-stu-id="25193-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="25193-136">`--source-port-range "*"`：來源連接埠或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="25193-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="25193-137">開啟了連線的連接埠。</span><span class="sxs-lookup"><span data-stu-id="25193-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="25193-138">`--destination-address-prefix "*"`：CIDR 中的目的地位址首碼或使用預設標籤。</span><span class="sxs-lookup"><span data-stu-id="25193-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="25193-139">`--destination-port-range 3389`：目的地連接埠或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="25193-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="25193-140">收到連線要求的連接埠。</span><span class="sxs-lookup"><span data-stu-id="25193-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="25193-141">使用 **az network nsg rule create**  命令來建立規則，允許從網際網路存取連接埠 80 (HTTP)。</span><span class="sxs-lookup"><span data-stu-id="25193-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="25193-142">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="25193-143">使用 [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) 命令，將 NSG 繫結至 **FrontEnd** 子網路。</span><span class="sxs-lookup"><span data-stu-id="25193-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="25193-144">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-144">Expected output:</span></span>
   
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

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="25193-145">建立 `BackEnd` 子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="25193-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="25193-146">若要根據上述案例建立名為 *NSG-BackEnd* 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="25193-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="25193-147">使用 **az network nsg create** 建立 `NSG-BackEnd` NSG。</span><span class="sxs-lookup"><span data-stu-id="25193-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="25193-148">和前面的步驟 2 一樣，預期的輸出會相當大，其中會包括預設規則。</span><span class="sxs-lookup"><span data-stu-id="25193-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="25193-149">使用 **az network nsg rule create** 命令來建立允許從 `FrontEnd` 子網路存取連接埠 1433 (SQL)。</span><span class="sxs-lookup"><span data-stu-id="25193-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="25193-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-150">Expected output:</span></span>

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

3. <span data-ttu-id="25193-151">使用 **az network nsg rule create** 命令來建立拒絕存取網際網路的規則。</span><span class="sxs-lookup"><span data-stu-id="25193-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="25193-152">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="25193-153">使用 **az network vnet subnet set** 命令將 NSG 繫結至 `BackEnd` 子網路。</span><span class="sxs-lookup"><span data-stu-id="25193-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="25193-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="25193-154">Expected output:</span></span>
   
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
