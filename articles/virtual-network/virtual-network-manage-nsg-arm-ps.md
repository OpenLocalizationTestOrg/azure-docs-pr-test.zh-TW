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
# <a name="manage-network-security-groups-using-powershell"></a>使用 PowerShell 管理網路安全性群組

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。 本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>擷取資訊
您可以檢視您現有的 NSG、擷取現有 NSG 的規則，並找出與 NSG 相關聯的資源。

### <a name="view-existing-nsgs"></a>檢視現有的 NSG
tooview 所有的現有 Nsg 中的訂用帳戶，執行 hello `Get-AzureRmNetworkSecurityGroup` cmdlet。

預期的結果：

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


tooview hello 清單 Nsg 在特定的資源群組中，執行 hello `Get-AzureRmNetworkSecurityGroup` cmdlet。

預期的輸出：

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

### <a name="list-all-rules-for-an-nsg"></a>列出 NSG 的所有規則
名為 NSG tooview hello 規則**NSG 前端**，輸入下列命令的 hello:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

預期的輸出：

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
> 您也可以使用`Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules`toolist hello 預設規則從 hello **NSG 前端**NSG。
> 

### <a name="view-nsgs-associations"></a>檢視 NSG 關聯
tooview 哪些資源 hello **NSG 前端**NSG 是關聯，請執行的 hello 的下列命令：

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

尋找 hello **NetworkInterfaces**和**子網路**屬性如下所示：

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

在 hello 上述範例中，hello NSG 不相關聯的 tooany 網路介面 (Nic)。它是相關聯的 tooa 名為的子網路**前端**。

## <a name="manage-rules"></a>管理規則
您可以加入現有的 NSG 規則 tooan、 編輯現有的規則和移除規則。

### <a name="add-a-rule"></a>新增規則
規則，允許 tooadd**輸入**流量 tooport **443**從任何機器 toohello **NSG 前端**NSG，完成下列步驟的 hello:

1. 執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. 執行下列命令 tooadd hello 規則 toohello NSG:

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

3. toosave hello 變更 toohello NSG，執行下列命令的 hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    顯示只有 hello 安全性規則的預期的輸出：
   
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

### <a name="change-a-rule"></a>變更規則
建立上述 tooallow toochange hello 規則輸入流量從 hello**網際網路**，請遵循下列 hello 步驟。

1. 執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. 執行下列命令以 hello 新規則設定的 hello:

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

3. toosave hello 變更 toohello NSG，執行下列命令的 hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    顯示只有 hello 安全性規則的預期的輸出：
   
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

### <a name="delete-a-rule"></a>刪除規則
1. 執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. 執行 hello hello NSG 中的下列命令 tooremove hello 規則：

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. 儲存 hello 所做的變更 toohello NSG，藉由執行下列命令的 hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    預期的輸出顯示只有 hello 安全性規則，請注意 hello **https 規則**不會再列：
   
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

## <a name="manage-associations"></a>管理關聯
您可以將關聯 NSG toosubnets 和 Nic。 您也可以中斷 NSG 與其相關聯的任何資源的關聯。

### <a name="associate-an-nsg-tooa-nic"></a>關聯 NSG tooa NIC
tooassociate hello **NSG 前端**NSG toohello **TestNICWeb1** NIC，完成下列步驟的 hello:

1. 執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. 執行下列命令 tooretrieve hello 現有 NIC 的 hello，並將它儲存在變數中：

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. 設定 hello **NetworkSecurityGroup**屬性 hello **NIC** hello 變數 toohello 值**NSG**變數中，輸入下列命令的 hello:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello 變更 toohello NIC，執行下列命令的 hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性：
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>中斷 NSG 與 NIC 的關聯
toodissociate hello **NSG 前端**hello 從 NSG **TestNICWeb1** NIC，完成下列步驟的 hello:

1. 執行下列命令 tooretrieve hello 現有 NIC 的 hello，並將它儲存在變數中：

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. 設定 hello **NetworkSecurityGroup**屬性 hello **NIC**變數太**$null**藉由執行下列命令的 hello:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello 變更 toohello NIC，執行下列命令的 hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性：
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>中斷 NSG 與子網路的關聯
toodissociate hello **NSG 前端**hello 從 NSG**前端**子網路、 完整 hello 下列步驟：

1. 執行下列命令 tooretrieve hello 現有 VNet 的 hello，並將它儲存在變數中：

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. 執行 hello 下列命令 tooretrieve hello**前端**子網路和儲存在變數中：

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. 設定 hello **NetworkSecurityGroup** hello 屬性**子網路**變數太**$null**輸入 hello 下列命令：

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello 變更 toohello 子網路，執行下列命令的 hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    預期的輸出顯示只有 hello 屬性的 hello**前端**子網路。 請注意，沒有 **NetworkSecurityGroup**的屬性：
   
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

### <a name="associate-an-nsg-tooa-subnet"></a>NSG tooa 子網路建立關聯
tooassociate hello **NSG 前端**NSG toohello **FronEnd**一次的子網路，完成下列步驟的 hello:

1. 執行下列命令 tooretrieve hello 現有 VNet 的 hello，並將它儲存在變數中：

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. 執行 hello 下列命令 tooretrieve hello**前端**子網路和儲存在變數中：

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. 執行下列命令 tooretrieve hello 現有 NSG 中的 hello，並將它儲存在變數中：

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. 設定 hello **NetworkSecurityGroup**屬性 hello**子網路**變數太**$null**藉由執行下列命令的 hello:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello 變更 toohello 子網路，執行下列命令的 hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    預期的輸出顯示只有 hello **NetworkSecurityGroup**屬性 hello**前端**子網路：
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>刪除 NSG
如果它不是相關聯 tooany 資源，您只能刪除 NSG。 toodelete NSG 關聯，請遵循下列 hello 步驟。

1. toocheck hello 資源相關聯 tooan NSG，執行 hello`azure network nsg show`中所示[檢視 Nsg 關聯](#View-NSGs-associations)。
2. 如果 hello NSG 相關聯的 tooany Nic，請執行 hello`azure network nic set`中所示[中斷 NIC 的 NSG 關聯](#Dissociate-an-NSG-from-a-NIC)的每個 nic。 
3. 如果 hello NSG 相關聯的 tooany 子網路，請執行 hello`azure network vnet subnet set`中所示[中斷關聯子網路的 NSG](#Dissociate-an-NSG-from-a-subnet)每個子網路。
4. toodelete hello NSG，執行下列命令的 hello:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > hello`-Force`參數可確保您不需要 tooconfirm hello 刪除。
   > 

## <a name="next-steps"></a>後續步驟
* [啟用 NSG 的記錄](virtual-network-nsg-manage-log.md) 。

