---
title: "Azure-PowerShell 中的 aaaControl 路由和虛擬設備 |Microsoft 文件"
description: "深入了解如何使用 PowerShell toocontrol 路由和虛擬裝置。"
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
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="6138e-103">使用 PowerShell 建立使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="6138e-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6138e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6138e-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="6138e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6138e-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="6138e-106">範本</span><span class="sxs-lookup"><span data-stu-id="6138e-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="6138e-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="6138e-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="6138e-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="6138e-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="6138e-109">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="6138e-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6138e-110">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-resource-manager/resource-manager-deployment-model.md) 。</span><span class="sxs-lookup"><span data-stu-id="6138e-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="6138e-111">您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。</span><span class="sxs-lookup"><span data-stu-id="6138e-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="6138e-112">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="6138e-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="6138e-113">您也可以[hello 傳統部署模型中建立 UDRs](virtual-network-create-udr-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="6138e-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="6138e-114">hello 範例 PowerShell 預期簡單的環境中已經建立下列命令會根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="6138e-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="6138e-115">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6138e-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="6138e-116">建立 hello UDR hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="6138e-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="6138e-117">toocreate hello 路由表和所需的 hello 前端子網路的路由會根據上述步驟的完整 hello hello 案例：</span><span class="sxs-lookup"><span data-stu-id="6138e-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="6138e-118">建立使用路由 toosend 所有流量 toohello 後端子 (192.168.2.0/24) 路由傳送 toobe toohello **FW1**虛擬應用裝置 (已將 192.168.0.4)。</span><span class="sxs-lookup"><span data-stu-id="6138e-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="6138e-119">建立名為路由表**UDR 前端**在 hello **uswest**包含 hello 路由的區域。</span><span class="sxs-lookup"><span data-stu-id="6138e-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="6138e-120">建立包含 hello VNet hello 子網路所在的變數。</span><span class="sxs-lookup"><span data-stu-id="6138e-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="6138e-121">在我們的案例中，hello VNet 命名為**TestVNet**。</span><span class="sxs-lookup"><span data-stu-id="6138e-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="6138e-122">關聯的 hello toohello 上面所建立的路由表**前端**子網路。</span><span class="sxs-lookup"><span data-stu-id="6138e-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="6138e-123">hello 上述命令中的 hello 輸出會顯示 hello hello 虛擬網路組態物件，其中只存在於執行 PowerShell 的 hello 電腦上的內容。</span><span class="sxs-lookup"><span data-stu-id="6138e-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="6138e-124">您需要 toorun hello**組 AzureVirtualNetwork** cmdlet toosave 這些設定 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6138e-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="6138e-125">儲存在 Azure 中的 hello 新的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="6138e-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6138e-126">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6138e-126">Expected output:</span></span>
   
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

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="6138e-127">建立 hello UDR hello 後端子網路</span><span class="sxs-lookup"><span data-stu-id="6138e-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="6138e-128">toocreate hello 路由表和路由所需的 hello 後端子根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6138e-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="6138e-129">建立使用路由 toosend 所有流量 toohello 前端的子網路 (192.168.1.0/24) 路由傳送 toobe toohello **FW1**虛擬應用裝置 (已將 192.168.0.4)。</span><span class="sxs-lookup"><span data-stu-id="6138e-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="6138e-130">建立名為路由表**UDR 後端**在 hello **uswest**上面所建立包含 hello 路由的區域。</span><span class="sxs-lookup"><span data-stu-id="6138e-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="6138e-131">關聯的 hello toohello 上面所建立的路由表**後端**子網路。</span><span class="sxs-lookup"><span data-stu-id="6138e-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="6138e-132">儲存在 Azure 中的 hello 新的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="6138e-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="6138e-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6138e-133">Expected output:</span></span>
   
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

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="6138e-134">啟用 FW1 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="6138e-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="6138e-135">tooenable 在 hello NIC 所使用的 IP 轉送**FW1**，依照下列步驟執行 hello。</span><span class="sxs-lookup"><span data-stu-id="6138e-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="6138e-136">建立包含 hello 設定 hello NIC FW1 所使用的變數。</span><span class="sxs-lookup"><span data-stu-id="6138e-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="6138e-137">在我們的案例中，hello NIC 會命名為**NICFW1**。</span><span class="sxs-lookup"><span data-stu-id="6138e-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="6138e-138">啟用 IP 轉送，並儲存 hello NIC 設定。</span><span class="sxs-lookup"><span data-stu-id="6138e-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="6138e-139">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6138e-139">Expected output:</span></span>
   
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

