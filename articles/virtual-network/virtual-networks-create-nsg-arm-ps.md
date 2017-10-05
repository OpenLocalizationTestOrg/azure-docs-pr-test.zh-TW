---
title: "建立網路安全性群組 - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 建立和部署網路安全性群組。"
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
ms.openlocfilehash: 26fe67b43d63c6685d8ae7644dd7df6931a4d2a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="7e240-103">使用 PowerShell 建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7e240-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="7e240-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="7e240-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7e240-105">Microsoft 建議透過 Resource Manager 部署模型建立資源。</span><span class="sxs-lookup"><span data-stu-id="7e240-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="7e240-106">若要深入了解兩個模型的差異，請閱讀[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="7e240-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="7e240-107">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="7e240-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="7e240-108">您也可以 [在傳統部署模型中建立 NSG](virtual-networks-create-nsg-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="7e240-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="7e240-109">以下的範例 PowerShell 命令會預期已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="7e240-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="7e240-110">如果您想要以本文件顯示的方式執行命令，請先依照下列方式建置測試環境：部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)，按一下 [部署至 Azure]，視情況取代預設參數值，然後遵循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="7e240-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="7e240-111">如何建立前端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="7e240-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="7e240-112">若要根據案例建立名為 NSG-FrontEnd 的 NSG，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7e240-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="7e240-113">如果您從未用過 Azure PowerShell，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) ，並遵循其中的所有指示登入 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7e240-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="7e240-114">建立允許從網際網路存取連接埠 3389 的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="7e240-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="7e240-115">建立允許從網際網路存取連接埠 80 的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="7e240-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="7e240-116">將上述建立的規則加入名為 **NSG-FrontEnd**的新 NSG。</span><span class="sxs-lookup"><span data-stu-id="7e240-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="7e240-117">輸入下列項目可檢查 NSG 中建立的規則︰</span><span class="sxs-lookup"><span data-stu-id="7e240-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="7e240-118">輸出僅顯示安全性規則：</span><span class="sxs-lookup"><span data-stu-id="7e240-118">Output showing just the security rules:</span></span>
   
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
6. <span data-ttu-id="7e240-119">將上述建立的 NSG 與 *FrontEnd* 子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="7e240-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="7e240-120">輸出僅顯示 *FrontEnd* 子網路設定，請注意 **NetworkSecurityGroup** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="7e240-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
   > <span data-ttu-id="7e240-121">上述命令的輸出會顯示虛擬網路設定物件的內容，此物件只存在於您執行 PowerShell 的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7e240-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="7e240-122">您需要執行 `Set-AzureRmVirtualNetwork` Cmdlet 來將這些設定儲存至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7e240-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="7e240-123">將新的 VNet 設定儲存至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7e240-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="7e240-124">輸出僅顯示 NSG 部分：</span><span class="sxs-lookup"><span data-stu-id="7e240-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="7e240-125">如何建立後端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="7e240-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="7e240-126">若要根據上述案例建立名為 NSG-BackEnd 的 NSG，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7e240-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="7e240-127">建立允許從前端子網路存取連接埠 1433 (SQL Server 所使用的預設連接埠) 的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="7e240-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="7e240-128">建立封鎖存取網際網路的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="7e240-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="7e240-129">將於上方建立的規則加入名為 **NSG-BackEnd**的新 NSG。</span><span class="sxs-lookup"><span data-stu-id="7e240-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="7e240-130">將於上方建立的 NSG 與 *BackEnd* 子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="7e240-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="7e240-131">輸出僅顯示 *BackEnd* 子網路設定，請注意 **NetworkSecurityGroup** 屬性的值：</span><span class="sxs-lookup"><span data-stu-id="7e240-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
5. <span data-ttu-id="7e240-132">將新的 VNet 設定儲存至 Azure。</span><span class="sxs-lookup"><span data-stu-id="7e240-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="7e240-133">如何移除 NSG</span><span class="sxs-lookup"><span data-stu-id="7e240-133">How to remove an NSG</span></span>
<span data-ttu-id="7e240-134">若要刪除現有的 NSG (在此案例中稱為 *NSG-Frontend*)，請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7e240-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="7e240-135">執行如下所示的 **Remove-AzureRmNetworkSecurityGroup**，並確定加入 NSG 所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7e240-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

