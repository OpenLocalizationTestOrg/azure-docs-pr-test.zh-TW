---
title: "設定可以並存的 ExpressRoute 和站對站 VPN 連線：Resource Manager：Azure | Microsoft Docs"
description: "本文會引導您針對 Resource Manager 部署模型設定可以並存的 ExpressRoute 和站對站 VPN 連線。"
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="54f99-103">設定 ExpressRoute 和站對站並存連線</span><span class="sxs-lookup"><span data-stu-id="54f99-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54f99-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54f99-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="54f99-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="54f99-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="54f99-106">設定站對站 VPN 和 ExpressRoute 並存連線有諸多好處。</span><span class="sxs-lookup"><span data-stu-id="54f99-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="54f99-107">您可以將站對站 VPN 設定為 ExressRoute 的安全容錯移轉路徑，或使用站對站 VPN 來連線至不是透過 ExpressRoute 連線的網站。</span><span class="sxs-lookup"><span data-stu-id="54f99-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="54f99-108">本文會說明設定這兩個案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="54f99-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="54f99-109">本文適用於 Resource Manager 部署模型並使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="54f99-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="54f99-110">此組態無法使用於 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="54f99-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54f99-111">在執行下列指示之前，必須事先設定 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="54f99-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="54f99-112">在繼續執行之前，請確定您已遵循[建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)的指南。</span><span class="sxs-lookup"><span data-stu-id="54f99-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="54f99-113">限制</span><span class="sxs-lookup"><span data-stu-id="54f99-113">Limits and limitations</span></span>
* <span data-ttu-id="54f99-114">**不支援傳輸路由。**</span><span class="sxs-lookup"><span data-stu-id="54f99-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="54f99-115">您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。</span><span class="sxs-lookup"><span data-stu-id="54f99-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="54f99-116">**不支援基本 SKU 閘道。**</span><span class="sxs-lookup"><span data-stu-id="54f99-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="54f99-117">您必須對 [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)使用非基本 SKU 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="54f99-118">**僅支援路由式 VPN 閘道。**</span><span class="sxs-lookup"><span data-stu-id="54f99-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="54f99-119">您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="54f99-120">**應該為 VPN 閘道設定靜態路由。**</span><span class="sxs-lookup"><span data-stu-id="54f99-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="54f99-121">如果您的區域網路連線到 ExpressRoute 和站對站 VPN，您必須在區域網路中設定靜態路由，才能將站對站 VPN 連線路由傳送到公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="54f99-122">**必須先設定 ExpressRoute 閘道並加以連結至電路。**</span><span class="sxs-lookup"><span data-stu-id="54f99-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="54f99-123">您必須先建立 ExpressRoute 閘道器並加以連結至電路，才能新增站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="54f99-124">組態設計</span><span class="sxs-lookup"><span data-stu-id="54f99-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="54f99-125">設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑</span><span class="sxs-lookup"><span data-stu-id="54f99-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="54f99-126">您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="54f99-127">這僅適用於連結至 Azure 私用對等路徑的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="54f99-128">對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。</span><span class="sxs-lookup"><span data-stu-id="54f99-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="54f99-129">ExpressRoute 線路一律為主要連結。</span><span class="sxs-lookup"><span data-stu-id="54f99-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="54f99-130">只有在 ExpressRoute 線路故障時，資料才能流經站對站 VPN 路徑。</span><span class="sxs-lookup"><span data-stu-id="54f99-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="54f99-131">雖然當兩個路由相同時，ExpressRoute 線路偏好透過站對站 VPN，但 Azure 會使用最長的相符前置詞來選擇朝向封包目的地的路由。</span><span class="sxs-lookup"><span data-stu-id="54f99-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![並存](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="54f99-133">設定站對站 VPN 來連線到未透過 ExpressRoute 連接的網站</span><span class="sxs-lookup"><span data-stu-id="54f99-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="54f99-134">您可以將網路設定成有些網站透過站對站 VPN 直接連線到 Azure，而有些網站透過 ExpressRoute 來連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![並存](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="54f99-136">您無法將虛擬網路設定為轉送路由器。</span><span class="sxs-lookup"><span data-stu-id="54f99-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="54f99-137">選取要使用的步驟</span><span class="sxs-lookup"><span data-stu-id="54f99-137">Selecting the steps to use</span></span>
<span data-ttu-id="54f99-138">有兩組不同的程序可供選擇。</span><span class="sxs-lookup"><span data-stu-id="54f99-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="54f99-139">您所選取的設定程序取決於您是已經有想要連線的現有虛擬網路，還是想要建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="54f99-140">我沒有 VNet 且需要建立一個。</span><span class="sxs-lookup"><span data-stu-id="54f99-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="54f99-141">如果您還沒有虛擬網路，這個程序將引導您使用 Resource Manager 部署模型來建立新的虛擬網路，並建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="54f99-142">若要設定虛擬網路，請依照[建立新的虛擬網路和並存的連線](#new)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="54f99-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="54f99-143">我已經有一個 Resource Manager 部署模型 VNet。</span><span class="sxs-lookup"><span data-stu-id="54f99-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="54f99-144">您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="54f99-145">[為已經存在的 VNet 設定並存的連線](#add)一節會引導您刪除閘道，然後建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="54f99-146">建立新的連線時，您必須以特定的順序來完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="54f99-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="54f99-147">請勿使用其他文章中的指示建立閘道器和連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="54f99-148">在此程序中，建立可以並存的連線會要求您刪除閘道器，然後設定新的閘道器。</span><span class="sxs-lookup"><span data-stu-id="54f99-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="54f99-149">當您刪除和重新建立閘道器與連線時，將會有跨設備連線的停機時間，但您不需要將任何 VM 或服務移轉至新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="54f99-150">您的 VM 和服務仍能透過負載平衡器對外通訊，而您能夠在這兩者設定為這樣做時進行閘道器設定。</span><span class="sxs-lookup"><span data-stu-id="54f99-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="54f99-151"><a name="new"></a>建立新的虛擬網路和並存的連線</span><span class="sxs-lookup"><span data-stu-id="54f99-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="54f99-152">此程序會引導您建立會並存的 VNet、站對站和 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="54f99-153">安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="54f99-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="54f99-154">如需如何安裝 Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="54f99-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="54f99-155">您針對此組態使用的 Cmdlet 可能與您熟悉的 Cmdlet 有些微不同。</span><span class="sxs-lookup"><span data-stu-id="54f99-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="54f99-156">請務必使用這些指示中指定的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="54f99-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="54f99-157">登入您的帳戶並設定環境。</span><span class="sxs-lookup"><span data-stu-id="54f99-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="54f99-158">建立包含閘道子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="54f99-159">如需關於虛擬網路組態的詳細資訊，請參閱 [Azure 虛擬網路組態](../virtual-network/virtual-networks-create-vnet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="54f99-160">閘道子網路必須是 /27 或更短的首碼 (例如 /26 或 /25)。</span><span class="sxs-lookup"><span data-stu-id="54f99-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="54f99-161">建立新的 VNet。</span><span class="sxs-lookup"><span data-stu-id="54f99-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="54f99-162">新增子網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="54f99-163">儲存 VNet 組態。</span><span class="sxs-lookup"><span data-stu-id="54f99-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="54f99-164"><a name="gw"></a>建立 ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="54f99-165">如需 ExpressRoute 閘道組態的詳細資訊，請參閱 [ExpressRoute 閘道組態](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="54f99-166">GatewaySKU 必須是 *Standard*、*HighPerformance* 或 *UltraPerformance*。</span><span class="sxs-lookup"><span data-stu-id="54f99-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="54f99-167">將 ExpressRoute 閘道器連結到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="54f99-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="54f99-168">完成這個步驟之後，內部部署網路和 Azure 之間的連線 (透過 ExpressRoute ) 便會建立。</span><span class="sxs-lookup"><span data-stu-id="54f99-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="54f99-169">如需連結作業的詳細資訊，請參閱 [將 Vnet 連結到 ExpressRoute](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="54f99-170"><a name="vpngw"></a>接下來，建立站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="54f99-171">如需 VPN 閘道組態的詳細資訊，請參閱[利用站對站連線設定 VNet](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="54f99-172">GatewaySKU 必須是 *Standard*、*HighPerformance* 或 *UltraPerformance*。</span><span class="sxs-lookup"><span data-stu-id="54f99-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="54f99-173">VpnType 必須是 RouteBased 。</span><span class="sxs-lookup"><span data-stu-id="54f99-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="54f99-174">Azure VPN 閘道支援 BGP 路由通訊協定。</span><span class="sxs-lookup"><span data-stu-id="54f99-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="54f99-175">您可以為該虛擬網路指定 ASN (AS 號碼)，方法是在下列命令中新增 -Asn 參數。</span><span class="sxs-lookup"><span data-stu-id="54f99-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="54f99-176">未指定該參數，則會預設為 AS 號碼 65515。</span><span class="sxs-lookup"><span data-stu-id="54f99-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="54f99-177">您可以在 $azureVpn.BgpSettings.BgpPeeringAddress 和 $azureVpn.BgpSettings.Asn 中找到 Azure 用於 VPN 閘道的 BGP 對等互連 IP 和 AS 號碼。</span><span class="sxs-lookup"><span data-stu-id="54f99-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="54f99-178">如需詳細資訊，請參閱針對 Azure VPN 閘道[設定 BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="54f99-179">建立本機的站台 VPN 閘道實體。</span><span class="sxs-lookup"><span data-stu-id="54f99-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="54f99-180">此命令不會設定內部部署 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="54f99-181">相反地，它可讓您提供本機閘道器設定 (例如公用 IP 與內部位址空間)，使 Azure VPN 閘道能夠與其連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="54f99-182">如果您的本機 VPN 裝置只支援靜態路由，您可以利用下列方式設定靜態路由：</span><span class="sxs-lookup"><span data-stu-id="54f99-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="54f99-183">如果您的本機 VPN 裝置支援 BGP，而且您想要啟用動態路由，您必須本機 VPN 裝置所用的知道 BGP 對等互連 IP 和 AS 號碼。</span><span class="sxs-lookup"><span data-stu-id="54f99-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="54f99-184">設定本機 VPN 裝置以連接到新的 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="54f99-185">如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="54f99-186">將 Azure 上的站對站 VPN 閘道連結至本機閘道器。</span><span class="sxs-lookup"><span data-stu-id="54f99-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="54f99-187"><a name="add"></a>為已經存在的 VNet 設定並存的連線</span><span class="sxs-lookup"><span data-stu-id="54f99-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="54f99-188">如果您有現有的虛擬網路，請檢查閘道器子網路大小。</span><span class="sxs-lookup"><span data-stu-id="54f99-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="54f99-189">如果閘道器子網路是/28 或/29，您必須先刪除虛擬網路閘道器，並增加閘道器子網路大小。</span><span class="sxs-lookup"><span data-stu-id="54f99-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="54f99-190">本節中的步驟示範如何執行該作業。</span><span class="sxs-lookup"><span data-stu-id="54f99-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="54f99-191">如果閘道器子網路是/27 以上且虛擬網路是透過 ExpressRoute 連線，則可以略過下列步驟，並且繼續進行上一節中的 [「步驟 6 - 建立站對站 VPN 閘道」](#vpngw) 。</span><span class="sxs-lookup"><span data-stu-id="54f99-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="54f99-192">當您刪除現有閘道器時，您在進行此設定時，本機設備將會與虛擬網路中斷連線。</span><span class="sxs-lookup"><span data-stu-id="54f99-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="54f99-193">您必須安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="54f99-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="54f99-194">如需如何安裝 Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="54f99-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="54f99-195">您針對此組態使用的 Cmdlet 可能與您熟悉的 Cmdlet 有些微不同。</span><span class="sxs-lookup"><span data-stu-id="54f99-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="54f99-196">請務必使用這些指示中指定的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="54f99-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="54f99-197">刪除現有的 ExpressRoute 或站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="54f99-198">刪除閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="54f99-199">新增 /27 或更大的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="54f99-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="54f99-200">如果您的虛擬網路中沒有足夠的 IP 位址可以增加閘道器子網路大小，您必須新增更多 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="54f99-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="54f99-201">儲存 VNet 組態。</span><span class="sxs-lookup"><span data-stu-id="54f99-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="54f99-202">此時，您會使用沒有閘道器的 VNet。</span><span class="sxs-lookup"><span data-stu-id="54f99-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="54f99-203">若要建立新的閘道器並完成連接，您可以繼續進行 [步驟 4 - 建立 ExpressRoute 閘道器](#gw)(您可以在先前的步驟組中找到)。</span><span class="sxs-lookup"><span data-stu-id="54f99-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="54f99-204">將點對站組態新增至 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="54f99-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="54f99-205">您可以在並存設定中，依照下列步驟將點對站組態新增至您的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="54f99-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="54f99-206">新增 VPN 用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="54f99-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="54f99-207">針對您的 VPN 閘道將 VPN 根憑證上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="54f99-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="54f99-208">在此範例中，假設根憑證是儲存於下列 PowerShell Cmdlet 執行所在的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="54f99-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="54f99-209">如需點對站 VPN 的詳細資訊，請參閱 [設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54f99-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54f99-210">Next steps</span></span>
<span data-ttu-id="54f99-211">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="54f99-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
