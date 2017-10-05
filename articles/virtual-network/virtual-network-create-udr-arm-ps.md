---
title: "在 Azure 中控制路由和虛擬設備 - PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 控制路由和虛擬應用裝置。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: 3ab24f193c74449ae7414b4ea0675c0aae0211f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="6c2d5-103">使用 PowerShell 建立使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="6c2d5-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c2d5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c2d5-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="6c2d5-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6c2d5-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="6c2d5-106">範本</span><span class="sxs-lookup"><span data-stu-id="6c2d5-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="6c2d5-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="6c2d5-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="6c2d5-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="6c2d5-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="6c2d5-109">使用 Azure 資源之前，請務必了解 Azure 目前有 Azure Resource Manager 和「傳統」兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6c2d5-110">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-resource-manager/resource-manager-deployment-model.md) 。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="6c2d5-111">您可以按一下本文頂端的索引標籤，檢視不同工具的文件。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span>
>

<span data-ttu-id="6c2d5-112">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-112">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="6c2d5-113">您也可以 [在傳統部署模型中建立 UDR](virtual-network-create-udr-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-113">You can also [create UDRs in the classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="6c2d5-114">以下的範例 PowerShell 命令會預期已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-114">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="6c2d5-115">如果您想要以本文件顯示的方式執行命令，請先依照下列方式建置測試環境：部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 [部署至 Azure]，視情況取代預設參數值，然後遵循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="6c2d5-116">建立前端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="6c2d5-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="6c2d5-117">若要根據上述案例建立前端子網路所需的路由表和路徑，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6c2d5-117">To create the route table and route needed for the front-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="6c2d5-118">建立用來傳送到以後端子網路 (192.168.2.0/24) 為目標的路由，以路由傳送所有流量到 **FW1** 虛擬應用裝置 (192.168.0.4)。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-118">Create a route used to send all traffic destined to the back-end subnet (192.168.2.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="6c2d5-119">在包含路由的 **westus** 區域中建立名為 **UDR-FrontEnd** 的路由表。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-119">Create a route table named **UDR-FrontEnd** in the **westus** region that contains the route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="6c2d5-120">建立包含子網路所在之 VNet 的變數。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-120">Create a variable that contains the VNet where the subnet is.</span></span> <span data-ttu-id="6c2d5-121">在我們的案例中，VNet 名為 **TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-121">In our scenario, the VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="6c2d5-122">將上方建立的路由表與 **FrontEnd** 子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-122">Associate the route table created above to the **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="6c2d5-123">上述命令的輸出會顯示虛擬網路設定物件的內容，此物件只存在於您執行 PowerShell 的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-123">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="6c2d5-124">您需要執行 **Set-AzureVirtualNetwork** Cmdlet 來將這些設定儲存至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-124">You need to run the **Set-AzureVirtualNetwork** cmdlet to save these settings to Azure.</span></span>
    > 

5. <span data-ttu-id="6c2d5-125">在 Azure 中儲存新的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-125">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6c2d5-126">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6c2d5-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="6c2d5-127">建立後端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="6c2d5-127">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="6c2d5-128">若要根據上述案例建立後端子網路所需的路由表和路徑，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-128">To create the route table and route needed for the back-end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="6c2d5-129">建立用來傳送到以前端子網路 (192.168.1.0/24) 為目標的路由，以路由傳送所有流量到 **FW1** 虛擬應用裝置 (192.168.0.4)。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-129">Create a route used to send all traffic destined to the front-end subnet (192.168.1.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="6c2d5-130">在包含上方建立的路由 **uswest** 區域中建立名為 **UDR-BackEnd** 的路由表。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-130">Create a route table named **UDR-BackEnd** in the **uswest** region that contains the route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="6c2d5-131">將上方建立的路由表與 **BackEnd** 子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-131">Associate the route table created above to the **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="6c2d5-132">在 Azure 中儲存新的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-132">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6c2d5-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6c2d5-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="6c2d5-134">啟用 FW1 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="6c2d5-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="6c2d5-135">若要啟用 **FW1**所使用之 NIC 中的 IP 轉送，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-135">To enable IP forwarding in the NIC used by **FW1**, follow the steps below.</span></span>

1. <span data-ttu-id="6c2d5-136">建立包含 FW1 所使用 NIC 的設定的變數。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-136">Create a variable that contains the settings for the NIC used by FW1.</span></span> <span data-ttu-id="6c2d5-137">在我們的案例中，NIC 名為 **NICFW1**。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-137">In our scenario, the NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="6c2d5-138">啟用 IP 轉送並儲存 NIC 設定。</span><span class="sxs-lookup"><span data-stu-id="6c2d5-138">Enable IP forwarding, and save the NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="6c2d5-139">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6c2d5-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

