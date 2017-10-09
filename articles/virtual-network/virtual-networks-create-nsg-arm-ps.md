---
title: "aaaCreate 網路安全性群組-Azure PowerShell |Microsoft 文件"
description: "深入了解如何 toocreate 及部署使用 PowerShell 的網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="4d9c4-103">使用 PowerShell 建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="4d9c4-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="4d9c4-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4d9c4-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="4d9c4-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="4d9c4-107">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="4d9c4-108">您也可以[hello 傳統部署模型中建立 Nsg](virtual-networks-create-nsg-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="4d9c4-109">hello 範例 PowerShell 預期簡單的環境中已經建立下列命令會根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="4d9c4-110">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="4d9c4-111">如何 toocreate hello NSG hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="4d9c4-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="4d9c4-112">toocreate NSG 名為*NSG 前端*根據 hello 情況，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4d9c4-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="4d9c4-113">如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="4d9c4-114">建立安全性規則，允許從 hello 網際網路 tooport 3389 的存取。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="4d9c4-115">建立安全性規則，允許從 hello 網際網路 tooport 80 的存取。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="4d9c4-116">加入新的 NSG 名為的 tooa 上面所建立的 hello 規則**NSG 前端**。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="4d9c4-117">請檢查輸入 hello 下列建立 hello NSG 中的 hello 規則：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="4d9c4-118">輸出顯示只是 hello 安全性規則：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="4d9c4-119">關聯 NSG toohello 上面所建立的 hello*前端*子網路。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="4d9c4-120">輸出顯示只有 hello*前端*子網路設定，請注意 hello 值 hello **NetworkSecurityGroup**屬性：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="4d9c4-121">hello 上述命令中的 hello 輸出會顯示 hello hello 虛擬網路組態物件，其中只存在於執行 PowerShell 的 hello 電腦上的內容。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="4d9c4-122">您需要 toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave 這些設定 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="4d9c4-123">儲存新的 VNet 設定 tooAzure hello。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="4d9c4-124">輸出顯示只 hello NSG 部分：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="4d9c4-125">如何 toocreate hello NSG hello 後端子</span><span class="sxs-lookup"><span data-stu-id="4d9c4-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="4d9c4-126">toocreate NSG 名為*NSG 後端*根據上述的 hello 情況，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4d9c4-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="4d9c4-127">建立安全性規則，允許從 hello 前端的子網路 tooport 1433 （預設通訊埠供 SQL Server） 的存取。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="4d9c4-128">建立封鎖存取 toohello 網際網路的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="4d9c4-129">加入新的 NSG 名為的 tooa 上面所建立的 hello 規則**NSG 後端**。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="4d9c4-130">關聯 NSG toohello 上面所建立的 hello*後端*子網路。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="4d9c4-131">輸出顯示只有 hello*後端*子網路設定，請注意 hello 值 hello **NetworkSecurityGroup**屬性：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="4d9c4-132">儲存新的 VNet 設定 tooAzure hello。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="4d9c4-133">如何 tooremove NSG</span><span class="sxs-lookup"><span data-stu-id="4d9c4-133">How tooremove an NSG</span></span>
<span data-ttu-id="4d9c4-134">呼叫 toodelete 現有 NSG *NSG 前端*在此情況下，請遵循以下的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="4d9c4-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="4d9c4-135">執行 hello**移除 AzureRmNetworkSecurityGroup**如下所示，而且是確定 tooinclude hello 資源群組 hello NSG 處於。</span><span class="sxs-lookup"><span data-stu-id="4d9c4-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

