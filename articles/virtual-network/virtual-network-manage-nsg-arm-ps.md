---
title: "aaaManage 網路安全性群組-Azure PowerShell |Microsoft 文件"
description: "了解如何 toomanage 網路使用 PowerShell 的安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="a6861-103">使用 PowerShell 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="a6861-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a6861-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a6861-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a6861-105">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a6861-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="a6861-106">擷取資訊</span><span class="sxs-lookup"><span data-stu-id="a6861-106">Retrieve Information</span></span>
<span data-ttu-id="a6861-107">您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="a6861-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="a6861-108">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="a6861-108">View existing NSGs</span></span>
<span data-ttu-id="a6861-109">tooview 所有的現有 Nsg 中的訂用帳戶，執行 hello `Get-AzureRmNetworkSecurityGroup` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a6861-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="a6861-110">預期的結果：</span><span class="sxs-lookup"><span data-stu-id="a6861-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="a6861-111">tooview hello 清單 Nsg 在特定的資源群組中，執行 hello `Get-AzureRmNetworkSecurityGroup` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a6861-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="a6861-112">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a6861-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="a6861-113">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="a6861-113">List all rules for an NSG</span></span>
<span data-ttu-id="a6861-114">名為 NSG tooview hello 規則**NSG 前端**，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="a6861-115">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a6861-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="a6861-116">您也可以使用`Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules`toolist hello 預設規則從 hello **NSG 前端**NSG。</span><span class="sxs-lookup"><span data-stu-id="a6861-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="a6861-117">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="a6861-117">View NSGs associations</span></span>
<span data-ttu-id="a6861-118">tooview 哪些資源 hello **NSG 前端**NSG 是關聯，請執行的 hello 的下列命令：</span><span class="sxs-lookup"><span data-stu-id="a6861-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="a6861-119">尋找 hello **NetworkInterfaces**和**子網路**屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6861-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="a6861-120">在 hello 上述範例中，hello NSG 不相關聯的 tooany 網路介面 (Nic)。它是相關聯的 tooa 名為的子網路**前端**。</span><span class="sxs-lookup"><span data-stu-id="a6861-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="a6861-121">管理規則</span><span class="sxs-lookup"><span data-stu-id="a6861-121">Manage rules</span></span>
<span data-ttu-id="a6861-122">您可以加入現有的 NSG 規則 tooan、 編輯現有的規則和移除規則。</span><span class="sxs-lookup"><span data-stu-id="a6861-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="a6861-123">新增規則</span><span class="sxs-lookup"><span data-stu-id="a6861-123">Add a rule</span></span>
<span data-ttu-id="a6861-124">規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="a6861-125">執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a6861-126">執行下列命令 tooadd hello 規則 toohello NSG:</span><span class="sxs-lookup"><span data-stu-id="a6861-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="a6861-127">toosave hello 變更 toohello NSG，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="a6861-128">顯示只有 hello 安全性規則的預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a6861-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="a6861-129">變更規則</span><span class="sxs-lookup"><span data-stu-id="a6861-129">Change a rule</span></span>
<span data-ttu-id="a6861-130">建立上述 tooallow toochange hello 規則輸入流量從 hello**網際網路**，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a6861-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="a6861-131">執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a6861-132">執行下列命令以 hello 新規則設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="a6861-133">toosave hello 變更 toohello NSG，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="a6861-134">顯示只有 hello 安全性規則的預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a6861-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="a6861-135">刪除規則</span><span class="sxs-lookup"><span data-stu-id="a6861-135">Delete a rule</span></span>
1. <span data-ttu-id="a6861-136">執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a6861-137">執行 hello hello NSG 中的下列命令 tooremove hello 規則：</span><span class="sxs-lookup"><span data-stu-id="a6861-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="a6861-138">儲存 hello 所做的變更 toohello NSG，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="a6861-139">預期的輸出顯示只有 hello 安全性規則，請注意 hello **https 規則**不會再列：</span><span class="sxs-lookup"><span data-stu-id="a6861-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="a6861-140">管理關聯</span><span class="sxs-lookup"><span data-stu-id="a6861-140">Manage associations</span></span>
<span data-ttu-id="a6861-141">您可以將關聯 NSG toosubnets 和 Nic。</span><span class="sxs-lookup"><span data-stu-id="a6861-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="a6861-142">您也可以中斷 NSG 與其相關聯的任何資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="a6861-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="a6861-143">關聯 NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="a6861-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="a6861-144">tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="a6861-145">執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a6861-146">執行下列命令 tooretrieve hello 現有 NIC 的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="a6861-147">設定 hello **NetworkSecurityGroup**屬性 hello **NIC** hello 變數 toohello 值**NSG**變數中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="a6861-148">toosave hello 變更 toohello NIC，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="a6861-149">預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性：</span><span class="sxs-lookup"><span data-stu-id="a6861-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="a6861-150">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="a6861-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="a6861-151">toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="a6861-152">執行下列命令 tooretrieve hello 現有 NIC 的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="a6861-153">設定 hello **NetworkSecurityGroup**屬性 hello **NIC**變數太**$null**藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="a6861-154">toosave hello 變更 toohello NIC，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="a6861-155">預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性：</span><span class="sxs-lookup"><span data-stu-id="a6861-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="a6861-156">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="a6861-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="a6861-157">toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路、 完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6861-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="a6861-158">執行下列命令 tooretrieve hello 現有 VNet 的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="a6861-159">執行 hello 下列命令 tooretrieve hello**前端**子網路和儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="a6861-160">設定 hello **NetworkSecurityGroup** hello 屬性**子網路**變數太**$null**輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a6861-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="a6861-161">toosave hello 變更 toohello 子網路，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="a6861-162">預期的輸出顯示只有 hello 屬性的 hello**前端**子網路。</span><span class="sxs-lookup"><span data-stu-id="a6861-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="a6861-163">請注意，沒有 **NetworkSecurityGroup**的屬性：</span><span class="sxs-lookup"><span data-stu-id="a6861-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="a6861-164">NSG tooa 子網路建立關聯</span><span class="sxs-lookup"><span data-stu-id="a6861-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="a6861-165">tooassociate hello **NSG 前端**NSG toohello **FronEnd**一次的子網路，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="a6861-166">執行下列命令 tooretrieve hello 現有 VNet 的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="a6861-167">執行 hello 下列命令 tooretrieve hello**前端**子網路和儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="a6861-168">執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="a6861-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="a6861-169">設定 hello **NetworkSecurityGroup**屬性 hello**子網路**變數太**$null**藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="a6861-170">toosave hello 變更 toohello 子網路，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="a6861-171">預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性 hello**前端**子網路：</span><span class="sxs-lookup"><span data-stu-id="a6861-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="a6861-172">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="a6861-172">Delete an NSG</span></span>
<span data-ttu-id="a6861-173">如果它不是相關聯 tooany 資源，您只能刪除 NSG。</span><span class="sxs-lookup"><span data-stu-id="a6861-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="a6861-174">toodelete NSG 關聯，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a6861-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="a6861-175">toocheck hello 資源相關聯 tooan NSG，執行 hello`azure network nsg show`中所示[檢視 Nsg 關聯](#View-NSGs-associations)。</span><span class="sxs-lookup"><span data-stu-id="a6861-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="a6861-176">如果 hello NSG 相關聯的 tooany Nic，請執行 hello`azure network nic set`中所示[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)的每個 nic。</span><span class="sxs-lookup"><span data-stu-id="a6861-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="a6861-177">如果 hello NSG 相關聯的 tooany 子網路，請執行 hello`azure network vnet subnet set`中所示[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)每個子網路。</span><span class="sxs-lookup"><span data-stu-id="a6861-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="a6861-178">toodelete hello NSG，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6861-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a6861-179">hello`-Force`參數可確保您不需要 tooconfirm hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="a6861-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="a6861-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6861-180">Next steps</span></span>
* <span data-ttu-id="a6861-181">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="a6861-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

