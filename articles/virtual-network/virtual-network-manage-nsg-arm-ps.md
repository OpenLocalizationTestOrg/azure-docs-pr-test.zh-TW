---
title: "管理網路安全性群組 - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 管理網路安全性群組。"
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
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="6cc95-103">使用 PowerShell 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6cc95-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6cc95-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6cc95-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6cc95-105">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6cc95-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="6cc95-106">擷取資訊</span><span class="sxs-lookup"><span data-stu-id="6cc95-106">Retrieve Information</span></span>
<span data-ttu-id="6cc95-107">您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="6cc95-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="6cc95-108">檢視現有的 NSG</span><span class="sxs-lookup"><span data-stu-id="6cc95-108">View existing NSGs</span></span>
<span data-ttu-id="6cc95-109">若要檢視訂用帳戶中所有現有的 NSG，請執行 `Get-AzureRmNetworkSecurityGroup` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6cc95-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="6cc95-110">預期的結果：</span><span class="sxs-lookup"><span data-stu-id="6cc95-110">Expected result:</span></span>

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


<span data-ttu-id="6cc95-111">若要檢視特定資源群組中的 NSG 清單，請執行 `Get-AzureRmNetworkSecurityGroup` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6cc95-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="6cc95-112">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6cc95-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="6cc95-113">列出 NSG 的所有規則</span><span class="sxs-lookup"><span data-stu-id="6cc95-113">List all rules for an NSG</span></span>
<span data-ttu-id="6cc95-114">若要檢視名為 **NSG-FrontEnd** 之 NSG 的規則，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="6cc95-115">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6cc95-115">Expected output:</span></span>

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
> <span data-ttu-id="6cc95-116">您也可以使用 `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` 從 **NSG-FrontEnd** NSG 列出預設的規則。</span><span class="sxs-lookup"><span data-stu-id="6cc95-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="6cc95-117">檢視 NSG 關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-117">View NSGs associations</span></span>
<span data-ttu-id="6cc95-118">若要檢視與 **NSG-FrontEnd** NSG 相關聯的資源，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="6cc95-119">尋找 **NetworkInterfaces** 和 **Subnets** 屬性，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="6cc95-120">在前一個範例中，NSG 沒有與任何網路介面 (NIC) 相關聯，而是與名稱為 **FrontEnd** 的子網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="6cc95-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="6cc95-121">管理規則</span><span class="sxs-lookup"><span data-stu-id="6cc95-121">Manage rules</span></span>
<span data-ttu-id="6cc95-122">您可以將規則新增至現有的 NSG、編輯現有的規則，以及移除規則。</span><span class="sxs-lookup"><span data-stu-id="6cc95-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="6cc95-123">新增規則</span><span class="sxs-lookup"><span data-stu-id="6cc95-123">Add a rule</span></span>
<span data-ttu-id="6cc95-124">若要新增規則，允許來自任何電腦的連接埠 **443** 的**輸入**流量流向 **NSG-FrontEnd** NSG，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc95-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="6cc95-125">執行下列命令來擷取現有的 NSG，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="6cc95-126">執行下列命令，將規則新增至 NSG：</span><span class="sxs-lookup"><span data-stu-id="6cc95-126">Run the following command to add a rule to the NSG:</span></span>

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

3. <span data-ttu-id="6cc95-127">若要儲存對 NSG 所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="6cc95-128">僅顯示安全性規則的預期輸出：</span><span class="sxs-lookup"><span data-stu-id="6cc95-128">Expected output showing only the security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="6cc95-129">變更規則</span><span class="sxs-lookup"><span data-stu-id="6cc95-129">Change a rule</span></span>
<span data-ttu-id="6cc95-130">若要變更以上所建立的規則，僅允許來自 **網際網路** 的輸入流量，請依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="6cc95-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="6cc95-131">執行下列命令來擷取現有的 NSG，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="6cc95-132">使用新的規則設定執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-132">Run the following command with the new rule settings:</span></span>

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

3. <span data-ttu-id="6cc95-133">若要儲存對 NSG 所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="6cc95-134">僅顯示安全性規則的預期輸出：</span><span class="sxs-lookup"><span data-stu-id="6cc95-134">Expected output showing only the security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="6cc95-135">刪除規則</span><span class="sxs-lookup"><span data-stu-id="6cc95-135">Delete a rule</span></span>
1. <span data-ttu-id="6cc95-136">執行下列命令來擷取現有的 NSG，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="6cc95-137">執行下列命令，從 NSG 中移除規則︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="6cc95-138">執行下列命令，以儲存對 NSG 所進行的變更：</span><span class="sxs-lookup"><span data-stu-id="6cc95-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="6cc95-139">僅顯示安全性規則的預期輸出，請注意，不再列出 **https-rule** ︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="6cc95-140">管理關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-140">Manage associations</span></span>
<span data-ttu-id="6cc95-141">您可以建立 NSG 與子網路和 NIC 的關聯。</span><span class="sxs-lookup"><span data-stu-id="6cc95-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="6cc95-142">您也可以中斷 NSG 與其相關聯的任何資源的關聯。</span><span class="sxs-lookup"><span data-stu-id="6cc95-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="6cc95-143">建立 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="6cc95-144">若要建立 **NSG-FrontEnd** NSG 與 **TestNICWeb1** NIC 的關聯，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc95-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="6cc95-145">執行下列命令來擷取現有的 NSG，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="6cc95-146">執行下列命令來擷取現有的 NIC，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="6cc95-147">輸入下列命令，將 **NIC** 變數的 **NetworkSecurityGroup** 屬性設定為 **NSG** 變數的值：</span><span class="sxs-lookup"><span data-stu-id="6cc95-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="6cc95-148">若要儲存對 NIC 所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="6cc95-149">僅顯示 **NetworkSecurityGroup** 屬性的預期輸出︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="6cc95-150">中斷 NSG 與 NIC 的關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="6cc95-151">若要中斷 **NSG-FrontEnd** NSG 與 **TestNICWeb1** NIC 的關聯，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc95-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="6cc95-152">執行下列命令來擷取現有的 NIC，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="6cc95-153">執行下列命令，將 **NIC** 變數的 **NetworkSecurityGroup** 屬性設定為 **$null**：</span><span class="sxs-lookup"><span data-stu-id="6cc95-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="6cc95-154">若要儲存對 NIC 所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="6cc95-155">僅顯示 **NetworkSecurityGroup** 屬性的預期輸出︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="6cc95-156">中斷 NSG 與子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="6cc95-157">若要中斷 **NSG-FrontEnd** NSG 與 **FrontEnd** 子網路的關聯，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc95-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="6cc95-158">執行下列命令來擷取現有的 VNet，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="6cc95-159">執行下列命令來擷取 **FrontEnd** 子網路，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="6cc95-160">輸入下列命令，將 **subnet** 變數的 **NetworkSecurityGroup** 屬性設定為 **$null**：</span><span class="sxs-lookup"><span data-stu-id="6cc95-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="6cc95-161">若要儲存對子網路所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6cc95-162">僅顯示 **FrontEnd** 子網路屬性的預期輸出。</span><span class="sxs-lookup"><span data-stu-id="6cc95-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="6cc95-163">請注意，沒有 **NetworkSecurityGroup**的屬性：</span><span class="sxs-lookup"><span data-stu-id="6cc95-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="6cc95-164">建立 NSG 至子網路的關聯</span><span class="sxs-lookup"><span data-stu-id="6cc95-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="6cc95-165">若要建立 **NSG-FrontEnd** NSG 與 **FronEnd** 子網路的關聯，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cc95-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="6cc95-166">執行下列命令來擷取現有的 VNet，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="6cc95-167">執行下列命令來擷取 **FrontEnd** 子網路，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="6cc95-168">執行下列命令來擷取現有的 NSG，並將其儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6cc95-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="6cc95-169">執行下列命令，將 **subnet** 變數的 **NetworkSecurityGroup** 屬性設定為 **$null**：</span><span class="sxs-lookup"><span data-stu-id="6cc95-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="6cc95-170">若要儲存對子網路所進行的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cc95-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6cc95-171">僅顯示 **FrontEnd** 子網路的 **NetworkSecurityGroup** 屬性的預期輸出︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="6cc95-172">刪除 NSG</span><span class="sxs-lookup"><span data-stu-id="6cc95-172">Delete an NSG</span></span>
<span data-ttu-id="6cc95-173">您只能刪除與任何資源沒有關聯的 NSG。</span><span class="sxs-lookup"><span data-stu-id="6cc95-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="6cc95-174">若要刪除 NSG，請依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="6cc95-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="6cc95-175">若要檢查與 NSG 相關聯的資源，請執行 `azure network nsg show` ，如 [檢視 NSG 關聯](#View-NSGs-associations)中所示。</span><span class="sxs-lookup"><span data-stu-id="6cc95-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="6cc95-176">如果 NSG 與任何 NIC 相關聯，為每個 NIC 執行 `azure network nic set` ，如 [中斷 NSG 與 NIC 的關聯](#Dissociate-an-NSG-from-a-NIC) 中所示。</span><span class="sxs-lookup"><span data-stu-id="6cc95-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="6cc95-177">如果 NSG 與任何子網路相關聯，為每個子網路執行 `azure network vnet subnet set` ，如 [中斷 NSG 與子網路的關聯](#Dissociate-an-NSG-from-a-subnet) 中所示。</span><span class="sxs-lookup"><span data-stu-id="6cc95-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="6cc95-178">若要刪除 NSG，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6cc95-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="6cc95-179">`-Force` 參數可確保您不需要確認刪除。</span><span class="sxs-lookup"><span data-stu-id="6cc95-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="6cc95-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cc95-180">Next steps</span></span>
* <span data-ttu-id="6cc95-181">[啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。</span><span class="sxs-lookup"><span data-stu-id="6cc95-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

