---
title: "設定 Azure 站對站連線的強制通道：Resource Manager | Microsoft Docs"
description: "如何重新導向或「強制」所有網際網路繫結流量回到內部部署位置。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 207c53924863eb51ee369fe46d5ad12fb1905c53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="74e68-103">使用 Azure Resource Manager 部署模型設定強制通道</span><span class="sxs-lookup"><span data-stu-id="74e68-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="74e68-104">強制通道可讓您透過站對站 VPN 通道，重新導向或「強制」所有網際網路繫結流量傳回內部部署位置，以便進行檢查和稽核。</span><span class="sxs-lookup"><span data-stu-id="74e68-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="74e68-105">這是多數企業 IT 原則的重要安全性需求。</span><span class="sxs-lookup"><span data-stu-id="74e68-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="74e68-106">若不使用強制通道處理，則來自您 Azure 中 VM 的網際網路繫結流量一律會從 Azure 網路基礎結構直接向外周遊到網際網路，而您無法選擇檢查或稽核流量。</span><span class="sxs-lookup"><span data-stu-id="74e68-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="74e68-107">未經授權的網際網路存取可能會導致資訊洩漏或其他類型的安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="74e68-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="74e68-108">本文會引導您為使用 Resource Manager 部署模型建立的虛擬網路設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="74e68-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="74e68-109">強制通道可使用 PowerShell 設定，而非透過入口網站。</span><span class="sxs-lookup"><span data-stu-id="74e68-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="74e68-110">如果想要設定傳統部署模型的強制通道，請從下列下拉式清單選取傳統文章：</span><span class="sxs-lookup"><span data-stu-id="74e68-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74e68-111">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="74e68-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="74e68-112">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="74e68-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="74e68-113">有關強制通道</span><span class="sxs-lookup"><span data-stu-id="74e68-113">About forced tunneling</span></span>

<span data-ttu-id="74e68-114">下圖說明如何使強制通道正常運作。</span><span class="sxs-lookup"><span data-stu-id="74e68-114">The following diagram illustrates how forced tunneling works.</span></span> 

![強制通道](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="74e68-116">在上述範例中，前端子網路不會使用強制通道。</span><span class="sxs-lookup"><span data-stu-id="74e68-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="74e68-117">前端子網路中的工作負載可以直接從網際網路繼續接受並回應客戶要求。</span><span class="sxs-lookup"><span data-stu-id="74e68-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="74e68-118">中間層和後端的子網路會使用強制通道。</span><span class="sxs-lookup"><span data-stu-id="74e68-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="74e68-119">任何從這兩個子網路到網際網路的輸出連接會強制或重新導向回 S2S VPN 通道的其中一個內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="74e68-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="74e68-120">這可讓您在 Azure 中限制並檢查來自虛擬機器或雲端服務的網際網路存取，同時繼續啟用您所需的多層式服務架構。</span><span class="sxs-lookup"><span data-stu-id="74e68-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="74e68-121">如果虛擬網路中沒有任何網際網路對向工作負載，您也可以將強制通道處理套用至整個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="74e68-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling to the entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="74e68-122">需求和考量</span><span class="sxs-lookup"><span data-stu-id="74e68-122">Requirements and considerations</span></span>

<span data-ttu-id="74e68-123">Azure 中的強制通道處理會透過虛擬網路使用者定義的路由進行設定。</span><span class="sxs-lookup"><span data-stu-id="74e68-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="74e68-124">將流量重新導向至在內部部署網站時，會表示為至 Azure VPN 閘道的「預設路由」。</span><span class="sxs-lookup"><span data-stu-id="74e68-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="74e68-125">如需有關使用者定義路由和虛擬網路的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="74e68-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="74e68-126">每個虛擬網路的子網路皆有內建的系統路由表。</span><span class="sxs-lookup"><span data-stu-id="74e68-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="74e68-127">系統路由表具有下列 3 個路由群組：</span><span class="sxs-lookup"><span data-stu-id="74e68-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="74e68-128">**本機 VNet 路由：**直接連線到相同虛擬網路中的目的地 VM。</span><span class="sxs-lookup"><span data-stu-id="74e68-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="74e68-129">**內部部署路由：**連線到 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="74e68-129">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="74e68-130">**預設路由：**直接連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="74e68-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="74e68-131">系統將會捨棄尚未由前兩個路由涵蓋之私人 IP 位址目的地的封包。</span><span class="sxs-lookup"><span data-stu-id="74e68-131">Packets destined to the private IP addresses not covered by the previous two routes are dropped.</span></span>
* <span data-ttu-id="74e68-132">此程序使用「使用者定義的路由 (UDR)」建立路由表以新增預設路由，然後將路由表關聯至您的 VNet 子網路，以啟用那些子網路上的強制通道處理。</span><span class="sxs-lookup"><span data-stu-id="74e68-132">This procedure uses user-defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="74e68-133">強制通道必須與具有路由型 VPN 閘道的 VNet 相關聯。</span><span class="sxs-lookup"><span data-stu-id="74e68-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="74e68-134">您需要在連接到虛擬網路的內部部署本機網站間設定「預設網站」。</span><span class="sxs-lookup"><span data-stu-id="74e68-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span> <span data-ttu-id="74e68-135">此外，內部部署 VPN 裝置必須使用 0.0.0.0/0 設定為流量選取器。</span><span class="sxs-lookup"><span data-stu-id="74e68-135">Also, the on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="74e68-136">ExpressRoute 強制通道不會透過這項機制進行設定，相反地，將由透過 ExpressRoute BGP 對等互連工作階段的廣告預設路由進行啟用。</span><span class="sxs-lookup"><span data-stu-id="74e68-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="74e68-137">如需詳細資訊，請參閱 [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)。</span><span class="sxs-lookup"><span data-stu-id="74e68-137">For more information, see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="74e68-138">組態概觀</span><span class="sxs-lookup"><span data-stu-id="74e68-138">Configuration overview</span></span>

<span data-ttu-id="74e68-139">下列程序可協助您建立資源群組和 VNet。</span><span class="sxs-lookup"><span data-stu-id="74e68-139">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="74e68-140">然後您將建立 VPN 閘道，並設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="74e68-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="74e68-141">在此程序中，'MultiTier-VNet' 虛擬網路具有三個子網路：「前端」、「中層」和「後端」，包含四個跨單位連線：DefaultSiteHQ 和三個「分支」。</span><span class="sxs-lookup"><span data-stu-id="74e68-141">In this procedure, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="74e68-142">程序步驟會將 'DefaultSiteHQ' 設定為強制通道處理的預設網站連線，並設定「中層」和「後端」子網路以使用強制通道處理。</span><span class="sxs-lookup"><span data-stu-id="74e68-142">The procedure steps set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the 'Midtier' and 'Backend' subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="74e68-143">開始之前</span><span class="sxs-lookup"><span data-stu-id="74e68-143">Before you begin</span></span>

<span data-ttu-id="74e68-144">安裝最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="74e68-144">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="74e68-145">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="74e68-145">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="to-log-in"></a><span data-ttu-id="74e68-146">登入</span><span class="sxs-lookup"><span data-stu-id="74e68-146">To log in</span></span>

[!INCLUDE [To log in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="74e68-147">設定強制通道</span><span class="sxs-lookup"><span data-stu-id="74e68-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="74e68-148">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="74e68-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="74e68-149">建立虛擬網路並指定子網路。</span><span class="sxs-lookup"><span data-stu-id="74e68-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="74e68-150">建立區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="74e68-150">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="74e68-151">建立路由表和路由規則。</span><span class="sxs-lookup"><span data-stu-id="74e68-151">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="74e68-152">建立路由表與中間層和後端子網路的關聯。</span><span class="sxs-lookup"><span data-stu-id="74e68-152">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="74e68-153">建立預設網站的閘道。</span><span class="sxs-lookup"><span data-stu-id="74e68-153">Create the Gateway with a default site.</span></span> <span data-ttu-id="74e68-154">此步驟需要一些時間才能完成，有時需要 45 分鐘或更久，因為您將建立及設定閘道。</span><span class="sxs-lookup"><span data-stu-id="74e68-154">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="74e68-155">**-GatewayDefaultSite** 是可讓強制路由組態得以運作的 Cmdlet 參數，因此請務必正確地進行此設定。</span><span class="sxs-lookup"><span data-stu-id="74e68-155">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="74e68-156">此參數僅適用於 PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="74e68-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="74e68-157">建立站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="74e68-157">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```