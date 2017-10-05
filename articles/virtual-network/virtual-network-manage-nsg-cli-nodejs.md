---
title: "管理網路安全性群組 - Azure CLI 1.0 | Microsoft Docs"
description: "了解如何使用 Azure 命令列介面 (CLI) 1.0 管理網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e53c3ff2ffbef95d6b72ca6afb3b4de377f0389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="f265a-103">使用 Azure CLI 1.0 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="f265a-103">Manage network security groups using the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f265a-104">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="f265a-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="f265a-105">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="f265a-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="f265a-106">[Azure CLI 1.0](#View-existing-NSGs) – 適用於傳統和資源管理部署模型的 CLI</span><span class="sxs-lookup"><span data-stu-id="f265a-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="f265a-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - 適用於資源管理部署模型的新一代 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="f265a-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f265a-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f265a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f265a-109">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f265a-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="f265a-110">擷取資訊</span><span class="sxs-lookup"><span data-stu-id="f265a-110">Retrieve Information</span></span>
<span data-ttu-id="f265a-111">您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="f265a-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="f265a-112">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="f265a-112">View existing NSGs</span></span>
<span data-ttu-id="f265a-113">若要檢視特定資源群組中的 NSG 清單，請執行 `azure network nsg list` 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="f265a-114">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting the network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="f265a-115">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="f265a-115">List all rules for an NSG</span></span>
<span data-ttu-id="f265a-116">若要檢視名為 **NSG-FrontEnd** 之 NSG 的規則，請執行 `azure network nsg show` 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="f265a-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="f265a-118">您也可以使用 `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` 從 **NSG-FrontEnd** NSG 列出規則。</span><span class="sxs-lookup"><span data-stu-id="f265a-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="f265a-119">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-119">View NSG associations</span></span>

<span data-ttu-id="f265a-120">若要檢視與 **NSG-FrontEnd** NSG 相關聯的資源，請執行 `azure network nsg show` 命令，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="f265a-121">請注意，唯一的差別是使用 **--json** 參數。</span><span class="sxs-lookup"><span data-stu-id="f265a-121">Notice that the only difference is the use of the **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="f265a-122">尋找 **networkInterfaces** 和 **subnets** 屬性，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f265a-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="f265a-123">在上述範例中，NSG 沒有與任何網路介面 (NIC) 相關聯，而是與名稱為 **FrontEnd**的子網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="f265a-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="f265a-124">管理規則</span><span class="sxs-lookup"><span data-stu-id="f265a-124">Manage rules</span></span>
<span data-ttu-id="f265a-125">您可以將規則新增至現有的 NSG、編輯現有的規則，以及移除規則。</span><span class="sxs-lookup"><span data-stu-id="f265a-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="f265a-126">新增規則</span><span class="sxs-lookup"><span data-stu-id="f265a-126">Add a rule</span></span>
<span data-ttu-id="f265a-127">若要將規則新增至 **NSG-FrontEnd** NSG，以允許來自任何電腦的**輸入**流量流向連接埠 **443**，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access to port 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="f265a-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up the network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="f265a-129">變更規則</span><span class="sxs-lookup"><span data-stu-id="f265a-129">Change a rule</span></span>
<span data-ttu-id="f265a-130">若要變更以上所建立的規則，僅允許來自**網際網路**的輸入流量，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="f265a-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up the network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="f265a-132">刪除規則</span><span class="sxs-lookup"><span data-stu-id="f265a-132">Delete a rule</span></span>
<span data-ttu-id="f265a-133">若要刪除以上所建立的規則，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-133">To delete the rule created above, run the following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="f265a-134">`--quiet` 參數可確保您不需要確認刪除。</span><span class="sxs-lookup"><span data-stu-id="f265a-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span></span>
>

<span data-ttu-id="f265a-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up the network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="f265a-136">管理關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-136">Manage associations</span></span>
<span data-ttu-id="f265a-137">您可以建立 NSG 與子網路和 NIC 的關聯。</span><span class="sxs-lookup"><span data-stu-id="f265a-137">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="f265a-138">您也可以中斷 NSG 與其相關聯的任何資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="f265a-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="f265a-139">建立 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-139">Associate an NSG to a NIC</span></span>
<span data-ttu-id="f265a-140">若要建立 **NSG-FrontEnd** NSG 與 **TestNICWeb1** NIC 的關聯，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="f265a-141">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Looking up the network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="f265a-142">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="f265a-143">若要中斷 **NSG-FrontEnd** NSG 與 **TestNICWeb1** NIC 的關聯，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="f265a-144">請注意 `network-security-group-id` 參數的 "" (空的) 值。</span><span class="sxs-lookup"><span data-stu-id="f265a-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span></span> <span data-ttu-id="f265a-145">這是移除與 NSG 之關聯的方法。</span><span class="sxs-lookup"><span data-stu-id="f265a-145">That is how you remove an association to an NSG.</span></span> <span data-ttu-id="f265a-146">您無法使用 `network-security-group-name` 參數來這樣做。</span><span class="sxs-lookup"><span data-stu-id="f265a-146">You can't do the same with the `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="f265a-147">預期的結果：</span><span class="sxs-lookup"><span data-stu-id="f265a-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="f265a-148">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="f265a-149">若要中斷 **NSG-FrontEnd** NSG 與 **FrontEnd** 子網路的關聯，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="f265a-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up the subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up the subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="f265a-151">建立 NSG 至子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="f265a-151">Associate an NSG to a subnet</span></span>
<span data-ttu-id="f265a-152">若要重新建立 **NSG-FrontEnd** NSG 與 **FrontEnd** 子網路的關聯，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f265a-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="f265a-153">上述命令能生效的原因，在於 **NSG-FrontEnd** NSG 與虛擬網路 **TestVNet** 位於相同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="f265a-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span></span> <span data-ttu-id="f265a-154">如果 NSG 位於不同資源群組，您需要改用 `--network-security-group-id` 參數並提供 NSG 的完整識別碼。</span><span class="sxs-lookup"><span data-stu-id="f265a-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span></span> <span data-ttu-id="f265a-155">您可以執行 `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json`，並尋找 **id** 屬性，即可擷取此識別碼。</span><span class="sxs-lookup"><span data-stu-id="f265a-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span></span> 
> 

<span data-ttu-id="f265a-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up the subnet "FrontEnd"
        + Looking up the network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="f265a-157">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="f265a-157">Delete an NSG</span></span>
<span data-ttu-id="f265a-158">您只能刪除與任何資源沒有關聯的 NSG。</span><span class="sxs-lookup"><span data-stu-id="f265a-158">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="f265a-159">若要刪除 NSG，請依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="f265a-159">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="f265a-160">若要檢查與 NSG 相關聯的資源，請執行 `azure network nsg show` ，如 [檢視 NSG 關聯](#View-NSGs-associations)中所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="f265a-161">如果 NSG 與任何 NIC 相關聯，為每個 NIC 執行 `azure network nic set` ，如 [中斷 NSG 與 NIC 的關聯](#Dissociate-an-NSG-from-a-NIC) 中所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="f265a-162">如果 NSG 與任何子網路相關聯，為每個子網路執行 `azure network vnet subnet set` ，如 [中斷 NSG 與子網路的關聯](#Dissociate-an-NSG-from-a-subnet) 中所示。</span><span class="sxs-lookup"><span data-stu-id="f265a-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="f265a-163">若要刪除 NSG，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f265a-163">To delete the NSG, run the following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="f265a-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="f265a-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up the network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="f265a-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f265a-165">Next steps</span></span>
* <span data-ttu-id="f265a-166">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="f265a-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

