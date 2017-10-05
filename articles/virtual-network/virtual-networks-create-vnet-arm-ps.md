---
title: "建立虛擬網路 - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 建立虛擬網路。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="e3a86-103">使用 PowerShell 建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e3a86-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="e3a86-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="e3a86-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e3a86-105">Microsoft 建議透過 Resource Manager 部署模型建立資源。</span><span class="sxs-lookup"><span data-stu-id="e3a86-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="e3a86-106">若要深入了解兩個模型的差異，請閱讀[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a86-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="e3a86-107">本文說明如何使用 PowerShell 透過 Resource Manager 部署模型建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="e3a86-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e3a86-108">您也可以使用其他工具透過 Resource Manager 建立 VNet，或從下列清單中選取不同選項以透過傳統部署模型建立 VNet︰</span><span class="sxs-lookup"><span data-stu-id="e3a86-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3a86-109">入口網站</span><span class="sxs-lookup"><span data-stu-id="e3a86-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="e3a86-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3a86-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="e3a86-111">CLI</span><span class="sxs-lookup"><span data-stu-id="e3a86-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="e3a86-112">範本</span><span class="sxs-lookup"><span data-stu-id="e3a86-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="e3a86-113">入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="e3a86-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="e3a86-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="e3a86-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="e3a86-115">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="e3a86-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="e3a86-116">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e3a86-116">Create a virtual network</span></span>

<span data-ttu-id="e3a86-117">若要使用 PowerShell 建立虛擬網路，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="e3a86-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="e3a86-118">遵循 [如何安裝並設定 Azure PowerShell](/powershell/azure/overview) 中的下列步驟來安裝和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e3a86-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="e3a86-119">如有必要，建立新的資源群組，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e3a86-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="e3a86-120">在此案例中，會建立名為 *TestRG*的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e3a86-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="e3a86-121">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a86-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="e3a86-122">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e3a86-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="e3a86-123">建立新的 VNet，名為 *TestVNet*：</span><span class="sxs-lookup"><span data-stu-id="e3a86-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="e3a86-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e3a86-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="e3a86-125">將虛擬網路物件儲存在收數中：</span><span class="sxs-lookup"><span data-stu-id="e3a86-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="e3a86-126">執行 `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus` 可以將步驟 3 和 4 結合在一起。</span><span class="sxs-lookup"><span data-stu-id="e3a86-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="e3a86-127">將子網路加入到新的 VNet 變數中：</span><span class="sxs-lookup"><span data-stu-id="e3a86-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="e3a86-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e3a86-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="e3a86-129">對您想要建立的每個子網路重複上述步驟 5。</span><span class="sxs-lookup"><span data-stu-id="e3a86-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="e3a86-130">以下命令會為本案例建立 *BackEnd* 子網路：</span><span class="sxs-lookup"><span data-stu-id="e3a86-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="e3a86-131">雖然建立了子網路，但是它們目前只以本機變數的形式存在，並用來擷取您在前述步驟 4 中建立的 VNet。</span><span class="sxs-lookup"><span data-stu-id="e3a86-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="e3a86-132">若要儲存對 Azure 的變更，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="e3a86-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="e3a86-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e3a86-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="e3a86-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3a86-134">Next steps</span></span>

<span data-ttu-id="e3a86-135">了解如何連接︰</span><span class="sxs-lookup"><span data-stu-id="e3a86-135">Learn how to connect:</span></span>

- <span data-ttu-id="e3a86-136">虛擬機器 (VM) 至虛擬網路；請閱讀[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a86-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="e3a86-137">但不是如文章中的步驟建立 VNet 和子網路，而是選取現有的 VNet 和子網路來連接 VM。</span><span class="sxs-lookup"><span data-stu-id="e3a86-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="e3a86-138">虛擬網路至其他虛擬網路；請閱讀[連接 VNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a86-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="e3a86-139">虛擬網路至內部部署網路；使用網站對網站虛擬私人網路 (VPN) 或 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="e3a86-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="e3a86-140">如需了解做法，請閱讀[使用網站對網站 VPN 將 VNet 連接到內部部署網路](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)以及[將 VNet 連結至 ExpressRoute 線路](../expressroute/expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a86-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
