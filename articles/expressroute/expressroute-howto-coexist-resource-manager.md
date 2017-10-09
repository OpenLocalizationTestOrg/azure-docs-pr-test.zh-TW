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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="9926d-103">設定 ExpressRoute 和站對站並存連線</span><span class="sxs-lookup"><span data-stu-id="9926d-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9926d-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9926d-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="9926d-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="9926d-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="9926d-106">設定站對站 VPN 和 ExpressRoute 並存連線有諸多好處。</span><span class="sxs-lookup"><span data-stu-id="9926d-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="9926d-107">您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExressRoute，或使用站對站 Vpn tooconnect toosites 不透過 ExpressRoute 連接。</span><span class="sxs-lookup"><span data-stu-id="9926d-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="9926d-108">我們將討論 hello 步驟 tooconfigure 本文章中的這兩種案例。</span><span class="sxs-lookup"><span data-stu-id="9926d-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="9926d-109">本文適用於 toohello Resource Manager 部署模型，並使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9926d-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="9926d-110">此設定不適用於 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9926d-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9926d-111">ExpressRoute 電路必須預先設定，才能執行下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="9926d-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="9926d-112">請確定您已依照 hello 指南太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)在繼續之前。</span><span class="sxs-lookup"><span data-stu-id="9926d-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="9926d-113">限制</span><span class="sxs-lookup"><span data-stu-id="9926d-113">Limits and limitations</span></span>
* <span data-ttu-id="9926d-114">**不支援傳輸路由。**</span><span class="sxs-lookup"><span data-stu-id="9926d-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="9926d-115">您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。</span><span class="sxs-lookup"><span data-stu-id="9926d-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="9926d-116">**不支援基本 SKU 閘道。**</span><span class="sxs-lookup"><span data-stu-id="9926d-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="9926d-117">您必須使用非基本 SKU 閘道可取得這兩個 hello [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 hello [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="9926d-118">**僅支援路由式 VPN 閘道。**</span><span class="sxs-lookup"><span data-stu-id="9926d-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="9926d-119">您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="9926d-120">**應該為 VPN 閘道設定靜態路由。**</span><span class="sxs-lookup"><span data-stu-id="9926d-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="9926d-121">如果您的區域網路連線的 tooboth ExpressRoute 而且網站間 VPN，您必須在您區域網路 tooroute hello 站對站 VPN 連線 toohello 中設定的靜態路由公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="9926d-122">**您必須先設定 ExpressRoute 閘道，並連結 tooa 循環。**</span><span class="sxs-lookup"><span data-stu-id="9926d-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="9926d-123">您必須先建立 hello ExpressRoute 閘道，並將它連結 tooa 循環，然後再新增 hello 站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="9926d-124">組態設計</span><span class="sxs-lookup"><span data-stu-id="9926d-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="9926d-125">設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑</span><span class="sxs-lookup"><span data-stu-id="9926d-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="9926d-126">您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="9926d-127">這適用於僅 toovirtual 網路連結的 toohello Azure 私人互連路徑。</span><span class="sxs-lookup"><span data-stu-id="9926d-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="9926d-128">對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。</span><span class="sxs-lookup"><span data-stu-id="9926d-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="9926d-129">hello ExpressRoute 電路一律為 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="9926d-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="9926d-130">資料流過 hello 站對站 VPN 路徑只有 hello ExpressRoute 電路失敗時。</span><span class="sxs-lookup"><span data-stu-id="9926d-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="9926d-131">雖然 ExpressRoute 循環時，最好透過站對站 VPN 這兩個路由是 hello 相同，則 Azure 會使用 hello 最長前置詞比對 toochoose hello 路由朝向 hello 封包的目的地。</span><span class="sxs-lookup"><span data-stu-id="9926d-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![並存](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="9926d-133">設定站對站 VPN tooconnect toosites 未透過 ExpressRoute 連線</span><span class="sxs-lookup"><span data-stu-id="9926d-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="9926d-134">您可以設定您的網路，其中某些站台直接 tooAzure 透過站對站 VPN 連接，而透過 ExpressRoute 連接某些站台。</span><span class="sxs-lookup"><span data-stu-id="9926d-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![並存](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="9926d-136">您無法將虛擬網路設定為轉送路由器。</span><span class="sxs-lookup"><span data-stu-id="9926d-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="9926d-137">選取 hello 步驟 toouse</span><span class="sxs-lookup"><span data-stu-id="9926d-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="9926d-138">有兩組不同的程序 toochoose 從。</span><span class="sxs-lookup"><span data-stu-id="9926d-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="9926d-139">您選取的 hello 組態程序取決於您擁有現有的虛擬網路，您會想 tooconnect，或是 toocreate 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="9926d-140">我不具有 VNet，而且需要 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="9926d-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="9926d-141">如果您還沒有虛擬網路，這個程序將引導您使用 Resource Manager 部署模型來建立新的虛擬網路，並建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="9926d-142">tooconfigure 虛擬網路，請依照下列中的 hello 步驟[toocreate 新的虛擬網路和共存連線](#new)。</span><span class="sxs-lookup"><span data-stu-id="9926d-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="9926d-143">我已經有一個 Resource Manager 部署模型 VNet。</span><span class="sxs-lookup"><span data-stu-id="9926d-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="9926d-144">您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="9926d-145">hello [tooconfigure 共存連線已存在的 vnet](#add) > 一節將引導您刪除 hello 閘道，然後建立新的 ExpressRoute 以及站台對站台 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="9926d-146">在建立新的連線時 hello，hello 步驟都必須以特定順序完成。</span><span class="sxs-lookup"><span data-stu-id="9926d-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="9926d-147">請勿使用其他發行項 toocreate hello 指示進行，您的閘道和連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="9926d-148">在此程序，建立可同時存在的連線需要您 toodelete 閘道，而然後設定新的閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="9926d-149">您必須跨單位連線的停機時間時就刪除並重新建立您的閘道與連線，但您不需要 toomigrate 任何 Vm 或服務 tooa 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="9926d-150">Vm 和服務仍會無法 toocommunicate 出透過 hello 負載平衡器時所設定的 toodo 因此，設定您的閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="9926d-151"><a name="new"></a>toocreate 新的虛擬網路和共存的連線</span><span class="sxs-lookup"><span data-stu-id="9926d-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="9926d-152">此程序會引導您建立會並存的 VNet、站對站和 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="9926d-153">安裝 Azure PowerShell cmdlet hello hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="9926d-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9926d-154">如需安裝 hello cmdlet 的資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9926d-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="9926d-155">hello cmdlet 可讓您針對此組態可能會與您可能的熟悉稍有不同。</span><span class="sxs-lookup"><span data-stu-id="9926d-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="9926d-156">確定 toouse hello cmdlet 這些指示中指定。</span><span class="sxs-lookup"><span data-stu-id="9926d-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="9926d-157">登入 tooyour 帳戶，並設定 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="9926d-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="9926d-158">建立包含閘道子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="9926d-159">如需 hello 虛擬網路組態的詳細資訊，請參閱[Azure 虛擬網路組態](../virtual-network/virtual-networks-create-vnet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9926d-160">hello 閘道子網路必須 /27 或短的前置詞 （例如 /26 或 /25）。</span><span class="sxs-lookup"><span data-stu-id="9926d-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="9926d-161">建立新的 VNet。</span><span class="sxs-lookup"><span data-stu-id="9926d-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="9926d-162">新增子網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="9926d-163">儲存 hello VNet 組態。</span><span class="sxs-lookup"><span data-stu-id="9926d-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="9926d-164"><a name="gw"></a>建立 ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="9926d-165">如需 hello ExpressRoute 閘道設定的詳細資訊，請參閱[ExpressRoute 閘道組態](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="9926d-166">hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*。</span><span class="sxs-lookup"><span data-stu-id="9926d-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="9926d-167">連結 hello ExpressRoute 閘道 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9926d-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="9926d-168">在完成這個步驟之後，會建立 hello 與內部網路與 Azure 中的，透過 ExpressRoute，之間的連線。</span><span class="sxs-lookup"><span data-stu-id="9926d-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="9926d-169">如需 hello 連結作業的詳細資訊，請參閱[連結 Vnet tooExpressRoute](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="9926d-170"><a name="vpngw"></a>接下來，建立站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="9926d-171">如需 hello VPN 閘道設定的詳細資訊，請參閱[站對站連線設定 VNet](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="9926d-172">hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*。</span><span class="sxs-lookup"><span data-stu-id="9926d-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="9926d-173">hello VpnType 必須*RouteBased*。</span><span class="sxs-lookup"><span data-stu-id="9926d-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="9926d-174">Azure VPN 閘道支援 BGP 路由通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9926d-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="9926d-175">您可以在 hello 下列命令中加入 hello-Asn 交換器，該虛擬網路指定 ASN （AS 號碼）。</span><span class="sxs-lookup"><span data-stu-id="9926d-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="9926d-176">未指定該參數會預設 tooAS 號碼 65515。</span><span class="sxs-lookup"><span data-stu-id="9926d-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="9926d-177">您可以找到 hello BGP 對等 IP 和 hello Azure hello $azureVpn.BgpSettings.BgpPeeringAddress 和 $azureVpn.BgpSettings.Asn 中的 VPN 閘道使用的數字。</span><span class="sxs-lookup"><span data-stu-id="9926d-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="9926d-178">如需詳細資訊，請參閱針對 Azure VPN 閘道[設定 BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="9926d-179">建立本機的站台 VPN 閘道實體。</span><span class="sxs-lookup"><span data-stu-id="9926d-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="9926d-180">此命令不會設定內部部署 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="9926d-181">相反地，它可讓您 tooprovide hello 本機閘道設定，例如 hello 公用 IP 和 hello 在內部部署位址空間，如此 hello Azure VPN 閘道可以連線 tooit。</span><span class="sxs-lookup"><span data-stu-id="9926d-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="9926d-182">如果本機 VPN 裝置僅支援靜態路由，您可以在 hello 下列方式設定 hello 靜態路由：</span><span class="sxs-lookup"><span data-stu-id="9926d-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="9926d-183">如果本機 VPN 裝置支援 hello BGP，並想 tooenable 動態路由，您需要 tooknow hello BGP 對等互連 IP 與 hello 因為數字，您的本機 VPN 裝置使用。</span><span class="sxs-lookup"><span data-stu-id="9926d-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="9926d-184">設定本機 VPN 裝置 tooconnect toohello 新 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="9926d-185">如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="9926d-186">連結 hello Azure toohello 本機閘道上的站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="9926d-187"><a name="add"></a>tooconfigure 共存連線已存在的 vnet</span><span class="sxs-lookup"><span data-stu-id="9926d-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="9926d-188">如果您有現有的虛擬網路，請檢查 hello 閘道子網路大小。</span><span class="sxs-lookup"><span data-stu-id="9926d-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="9926d-189">如果 hello 閘道子網路是/28 或 29，您必須先刪除 hello 虛擬網路閘道並增加 hello 閘道子網路大小。</span><span class="sxs-lookup"><span data-stu-id="9926d-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="9926d-190">hello 本節中的步驟示範 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="9926d-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="9926d-191">Hello 閘道子網路是否 /27 或更大而且透過 ExpressRoute 連接 hello 虛擬網路，您可以略過下列步驟 hello 而太[[步驟 6-建立站對站 VPN 閘道]](#vpngw) hello 前一節中。</span><span class="sxs-lookup"><span data-stu-id="9926d-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="9926d-192">當您刪除 hello 現有閘道時，您本機內部部署將會遺失 hello 連接 tooyour 虛擬網路，當您使用此設定。</span><span class="sxs-lookup"><span data-stu-id="9926d-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="9926d-193">您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9926d-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9926d-194">如需有關如何安裝 cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9926d-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="9926d-195">hello cmdlet 可讓您針對此組態可能會與您可能的熟悉稍有不同。</span><span class="sxs-lookup"><span data-stu-id="9926d-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="9926d-196">確定 toouse hello cmdlet 這些指示中指定。</span><span class="sxs-lookup"><span data-stu-id="9926d-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="9926d-197">刪除 hello 現有 ExpressRoute 或站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="9926d-198">刪除閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="9926d-199">新增 /27 或更大的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="9926d-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9926d-200">如果您沒有足夠的 IP 位址保留在您虛擬網路 tooincrease hello 閘道子網路大小，您需要 tooadd 多個 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="9926d-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="9926d-201">儲存 hello VNet 組態。</span><span class="sxs-lookup"><span data-stu-id="9926d-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="9926d-202">此時，您會使用沒有閘道器的 VNet。</span><span class="sxs-lookup"><span data-stu-id="9926d-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="9926d-203">toocreate 新的閘道完成您的連線，您可以繼續使用[步驟 4-建立 ExpressRoute 閘道](#gw)、 在 hello 前面的步驟中找到。</span><span class="sxs-lookup"><span data-stu-id="9926d-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="9926d-204">tooadd 點對站組態 toohello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="9926d-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="9926d-205">您可以依照下列 tooadd 點對站組態 tooyour 共存安裝程式中的 VPN 閘道的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="9926d-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="9926d-206">新增 VPN 用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="9926d-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="9926d-207">上傳 hello VPN 根憑證 tooAzure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9926d-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="9926d-208">在此範例中，它會假設該 hello 根憑證會儲存在 hello 本機電腦執行下列 PowerShell 指令程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="9926d-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="9926d-209">如需點對站 VPN 的詳細資訊，請參閱 [設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9926d-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9926d-210">Next steps</span></span>
<span data-ttu-id="9926d-211">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="9926d-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
