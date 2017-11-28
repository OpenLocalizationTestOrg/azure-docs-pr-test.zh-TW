---
title: "設定 Azure 站對站連線的強制通道：Resource Manager | Microsoft Docs"
description: "如何 tooredirect 或 'force' 所有網際網路繫結流量後 tooyour 內部位置。"
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
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="90559-103">設定強制通道使用 hello Azure Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="90559-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="90559-104">強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。</span><span class="sxs-lookup"><span data-stu-id="90559-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="90559-105">這是多數企業 IT 原則的重要安全性需求。</span><span class="sxs-lookup"><span data-stu-id="90559-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="90559-106">如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量一律會周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="90559-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="90559-107">Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="90559-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="90559-108">這篇文章會引導您設定強制通道使用 hello Resource Manager 部署模型所建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="90559-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="90559-109">使用 PowerShell，不能透過 hello 入口網站可以設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="90559-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="90559-110">如果您想 tooconfigure 強制通道 hello 傳統部署模型時，請從下列下拉式清單中的 hello 中選取傳統的發行項：</span><span class="sxs-lookup"><span data-stu-id="90559-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="90559-111">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="90559-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="90559-112">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="90559-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="90559-113">有關強制通道</span><span class="sxs-lookup"><span data-stu-id="90559-113">About forced tunneling</span></span>

<span data-ttu-id="90559-114">hello 下列圖表說明如何強制通道的運作。</span><span class="sxs-lookup"><span data-stu-id="90559-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![強制通道](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="90559-116">Hello 上述範例中，在 hello 的前端子網路則不會強制通道。</span><span class="sxs-lookup"><span data-stu-id="90559-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="90559-117">hello hello Frontend 子網路中的工作負載可以繼續 tooaccept，並直接從網際網路 hello 回應 toocustomer 要求。</span><span class="sxs-lookup"><span data-stu-id="90559-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="90559-118">hello mid-tier 和 Backend 子網路會強制通道。</span><span class="sxs-lookup"><span data-stu-id="90559-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="90559-119">這些兩個子網路 toohello 網際網路任何傳出連線會透過其中一個 S2S VPN 通道連接的 hello 強制或重新導向回 tooan 在內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="90559-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="90559-120">這可讓您 toorestrict 和檢查您的虛擬機器從網際網路存取，或雲端服務在 Azure 中，同時繼續 tooenable 您所需的多層式服務架構。</span><span class="sxs-lookup"><span data-stu-id="90559-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="90559-121">如果您的虛擬網路中有沒有網際網路對向工作負載，您也可以套用強制通道 toohello 整個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="90559-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="90559-122">需求和考量</span><span class="sxs-lookup"><span data-stu-id="90559-122">Requirements and considerations</span></span>

<span data-ttu-id="90559-123">Azure 中的強制通道處理會透過虛擬網路使用者定義的路由進行設定。</span><span class="sxs-lookup"><span data-stu-id="90559-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="90559-124">重新導向流量 tooan 內部部署站台以預設路由 toohello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="90559-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="90559-125">如需有關使用者定義路由和虛擬網路的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="90559-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="90559-126">每個虛擬網路的子網路皆有內建的系統路由表。</span><span class="sxs-lookup"><span data-stu-id="90559-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="90559-127">hello 系統路由表具有下列三個路由群組的 hello:</span><span class="sxs-lookup"><span data-stu-id="90559-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="90559-128">**區域的 VNet 路由：**直接 toohello Vm 中的目的地 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="90559-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="90559-129">**在內部部署路由：** toohello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="90559-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="90559-130">**預設路由：**直接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="90559-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="90559-131">目的地的封包 toohello 私人 IP 位址未涵蓋的 hello 前兩個路由會卸除。</span><span class="sxs-lookup"><span data-stu-id="90559-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="90559-132">這個程序會使用使用者定義的路由 (UDR) toocreate 路由表 tooadd 預設路由，並將產生關聯路由表 tooyour VNet 子網路，tooenable 強制通道這些子網路上的 hello。</span><span class="sxs-lookup"><span data-stu-id="90559-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="90559-133">強制通道必須與具有路由型 VPN 閘道的 VNet 相關聯。</span><span class="sxs-lookup"><span data-stu-id="90559-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="90559-134">您在 hello 跨單位本機站台連線的 toohello 虛擬網路之間需要 tooset 「 預設網站 」。</span><span class="sxs-lookup"><span data-stu-id="90559-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="90559-135">此外，hello 內部部署 VPN 裝置必須使用 0.0.0.0/0 做為傳輸選取器設定。</span><span class="sxs-lookup"><span data-stu-id="90559-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="90559-136">未設定這項機制，透過 ExpressRoute 強制通道，但相反地，會啟用透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。</span><span class="sxs-lookup"><span data-stu-id="90559-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="90559-137">如需詳細資訊，請參閱 hello [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)。</span><span class="sxs-lookup"><span data-stu-id="90559-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="90559-138">組態概觀</span><span class="sxs-lookup"><span data-stu-id="90559-138">Configuration overview</span></span>

<span data-ttu-id="90559-139">下列程序的 hello 可協助您建立資源群組和 VNet。</span><span class="sxs-lookup"><span data-stu-id="90559-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="90559-140">然後您將建立 VPN 閘道，並設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="90559-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="90559-141">在此程序中，虛擬網路 'Multitier-vnet' hello 有三個的子網路: '前端'、 'Midtier，' 和 'Backend'，與四個跨單位連線: 'DefaultSiteHQ' 和三個分支。</span><span class="sxs-lookup"><span data-stu-id="90559-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="90559-142">hello 程序步驟設定 hello 'DefaultSiteHQ' hello 預設站台連線的強制通道，以及設定 hello 'Midtier' 和 'Backend' 的子網路 toouse 強制通道。</span><span class="sxs-lookup"><span data-stu-id="90559-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90559-143">開始之前</span><span class="sxs-lookup"><span data-stu-id="90559-143">Before you begin</span></span>

<span data-ttu-id="90559-144">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="90559-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="90559-145">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="90559-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="90559-146">toolog 中</span><span class="sxs-lookup"><span data-stu-id="90559-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="90559-147">設定強制通道</span><span class="sxs-lookup"><span data-stu-id="90559-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="90559-148">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="90559-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="90559-149">建立虛擬網路並指定子網路。</span><span class="sxs-lookup"><span data-stu-id="90559-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="90559-150">建立 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="90559-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="90559-151">建立 hello 路由表和路由規則。</span><span class="sxs-lookup"><span data-stu-id="90559-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="90559-152">讓 hello 路由表 toohello Midtier 和後端子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="90559-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="90559-153">建立 hello 閘道與預設網站。</span><span class="sxs-lookup"><span data-stu-id="90559-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="90559-154">這個步驟需要一些時間 toocomplete，有時 45 分鐘以上，因為您建立和設定 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="90559-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="90559-155">hello **-GatewayDefaultSite**是 hello 指令程式參數，可讓 hello 強制路由組態 toowork，所以請小心 tooconfigure 設定正確。</span><span class="sxs-lookup"><span data-stu-id="90559-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="90559-156">此參數僅適用於 PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="90559-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="90559-157">建立 hello 站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="90559-157">Establish hello Site-to-Site VPN connections.</span></span>

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