---
title: "aaaManage 網路安全性群組-Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用將 toomanage 網路安全性群組 hello Azure 命令列介面 (CLI) 1.0。"
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
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="ab95a-103">管理使用 hello Azure CLI 1.0 的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ab95a-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ab95a-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="ab95a-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ab95a-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="ab95a-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ab95a-106">[Azure CLI 1.0](#View-existing-NSGs) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="ab95a-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ab95a-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="ab95a-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ab95a-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ab95a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ab95a-109">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="ab95a-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="ab95a-110">擷取資訊</span><span class="sxs-lookup"><span data-stu-id="ab95a-110">Retrieve Information</span></span>
<span data-ttu-id="ab95a-111">您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="ab95a-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="ab95a-112">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="ab95a-112">View existing NSGs</span></span>
<span data-ttu-id="ab95a-113">tooview hello 清單 Nsg 在特定的資源群組中，執行 hello`azure network nsg list`命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="ab95a-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="ab95a-114">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ab95a-115">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="ab95a-115">List all rules for an NSG</span></span>
<span data-ttu-id="ab95a-116">名為 NSG tooview hello 規則**NSG 前端**中執行的 hello`azure network nsg show`命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="ab95a-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="ab95a-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
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
> <span data-ttu-id="ab95a-118">您也可以使用`azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd`hello toolist hello 規則**NSG 前端**NSG。</span><span class="sxs-lookup"><span data-stu-id="ab95a-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="ab95a-119">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="ab95a-119">View NSG associations</span></span>

<span data-ttu-id="ab95a-120">tooview 哪些資源 hello **NSG 前端**NSG 為關聯，請執行 hello`azure network nsg show`命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="ab95a-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="ab95a-121">請注意該 hello 只有差異為 hello hello 使用**-json**參數。</span><span class="sxs-lookup"><span data-stu-id="ab95a-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="ab95a-122">尋找 hello **networkInterfaces**和**子網路**屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="ab95a-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="ab95a-123">在 hello 上述範例中，不是 NSG hello 關聯 tooany 網路介面 (Nic)，而且它是相關聯的 tooa 名為的子網路**前端**。</span><span class="sxs-lookup"><span data-stu-id="ab95a-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="ab95a-124">管理規則</span><span class="sxs-lookup"><span data-stu-id="ab95a-124">Manage rules</span></span>
<span data-ttu-id="ab95a-125">您可以加入現有的 NSG 規則 tooan、 編輯現有的規則和移除規則。</span><span class="sxs-lookup"><span data-stu-id="ab95a-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="ab95a-126">新增規則</span><span class="sxs-lookup"><span data-stu-id="ab95a-126">Add a rule</span></span>
<span data-ttu-id="ab95a-127">規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="ab95a-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="ab95a-129">變更規則</span><span class="sxs-lookup"><span data-stu-id="ab95a-129">Change a rule</span></span>
<span data-ttu-id="ab95a-130">tooallow 上面所建立的 toochange hello 規則輸入流量從 hello**網際網路**，執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ab95a-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="ab95a-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="ab95a-132">刪除規則</span><span class="sxs-lookup"><span data-stu-id="ab95a-132">Delete a rule</span></span>
<span data-ttu-id="ab95a-133">toodelete hello 建立規則，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="ab95a-134">hello`--quiet`參數可確保您不需要 tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="ab95a-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="ab95a-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="ab95a-136">管理關聯</span><span class="sxs-lookup"><span data-stu-id="ab95a-136">Manage associations</span></span>
<span data-ttu-id="ab95a-137">您可以將關聯 NSG toosubnets 和 Nic。</span><span class="sxs-lookup"><span data-stu-id="ab95a-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="ab95a-138">您也可以中斷 NSG 與其相關聯的任何資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="ab95a-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="ab95a-139">關聯 NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="ab95a-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="ab95a-140">tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="ab95a-141">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ab95a-142">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="ab95a-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="ab95a-143">toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="ab95a-144">請注意 hello""（空的） 值 hello`network-security-group-id`參數。</span><span class="sxs-lookup"><span data-stu-id="ab95a-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="ab95a-145">這是您要如何移除關聯 tooan NSG。</span><span class="sxs-lookup"><span data-stu-id="ab95a-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="ab95a-146">您無法以 hello hello 相同`network-security-group-name`參數。</span><span class="sxs-lookup"><span data-stu-id="ab95a-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="ab95a-147">預期的結果：</span><span class="sxs-lookup"><span data-stu-id="ab95a-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ab95a-148">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="ab95a-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="ab95a-149">toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="ab95a-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="ab95a-151">NSG tooa 子網路建立關聯</span><span class="sxs-lookup"><span data-stu-id="ab95a-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="ab95a-152">tooassociate hello **NSG 前端**NSG toohello **FronEnd**子網路同樣地，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="ab95a-153">hello 上述命令只適用於因為 hello **NSG 前端**NSG 處於 hello 與 hello 虛擬網路相同的資源群組**TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="ab95a-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="ab95a-154">如果 hello NSG 是不同資源群組中，您需要 toouse hello`--network-security-group-id`參數，並提供 hello NSG 中的 hello 完整識別碼。</span><span class="sxs-lookup"><span data-stu-id="ab95a-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="ab95a-155">您可以藉由執行擷取 hello 識別碼`azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json`，並尋找 hello**識別碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="ab95a-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="ab95a-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
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

## <a name="delete-an-nsg"></a><span data-ttu-id="ab95a-157">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="ab95a-157">Delete an NSG</span></span>
<span data-ttu-id="ab95a-158">如果它不是相關聯 tooany 資源，您只能刪除 NSG。</span><span class="sxs-lookup"><span data-stu-id="ab95a-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="ab95a-159">toodelete NSG 關聯，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ab95a-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="ab95a-160">toocheck hello 資源相關聯 tooan NSG，執行 hello`azure network nsg show`中所示[檢視 Nsg 關聯](#View-NSGs-associations)。</span><span class="sxs-lookup"><span data-stu-id="ab95a-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="ab95a-161">如果 hello NSG 相關聯的 tooany Nic，請執行 hello`azure network nic set`中所示[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)的每個 nic。</span><span class="sxs-lookup"><span data-stu-id="ab95a-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="ab95a-162">如果 hello NSG 相關聯的 tooany 子網路，請執行 hello`azure network vnet subnet set`中所示[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)每個子網路。</span><span class="sxs-lookup"><span data-stu-id="ab95a-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="ab95a-163">toodelete hello NSG，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab95a-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="ab95a-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="ab95a-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="ab95a-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab95a-165">Next steps</span></span>
* <span data-ttu-id="ab95a-166">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="ab95a-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

