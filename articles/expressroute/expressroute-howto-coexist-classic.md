---
title: "設定可以並存的 ExpressRoute 和站對站 VPN 連線：傳統：Azure | Microsoft Docs"
description: "本文會引導您針對傳統部署模型設定可以並存的 ExpressRoute 和站對站 VPN 連線。"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="09617-103">設定 ExpressRoute 和站對站並存連線 (傳統)</span><span class="sxs-lookup"><span data-stu-id="09617-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09617-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="09617-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="09617-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="09617-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="09617-106">能夠設定站對站 VPN 和 ExpressRoute 有諸多好處。</span><span class="sxs-lookup"><span data-stu-id="09617-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="09617-107">您可以將站對站 VPN 設定為 ExressRoute 的安全容錯移轉路徑，或使用站對站 VPN 來連接至不是透過 ExpressRoute 連接的網站。</span><span class="sxs-lookup"><span data-stu-id="09617-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="09617-108">本文中將說明設定這兩個案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="09617-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="09617-109">本文適用於傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="09617-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="09617-110">此組態無法使用於入口網站。</span><span class="sxs-lookup"><span data-stu-id="09617-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="09617-111">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="09617-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="09617-112">在執行下列指示之前，必須事先設定 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="09617-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="09617-113">在執行下列步驟之前，請確定您已遵循[建立 ExpressRoute 線路](expressroute-howto-circuit-classic.md)和[設定路由](expressroute-howto-routing-classic.md)的指南。</span><span class="sxs-lookup"><span data-stu-id="09617-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="09617-114">限制</span><span class="sxs-lookup"><span data-stu-id="09617-114">Limits and limitations</span></span>
* <span data-ttu-id="09617-115">**不支援傳輸路由。**</span><span class="sxs-lookup"><span data-stu-id="09617-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="09617-116">您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。</span><span class="sxs-lookup"><span data-stu-id="09617-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="09617-117">**不支援點對站連線。**</span><span class="sxs-lookup"><span data-stu-id="09617-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="09617-118">您無法啟用連接到 ExpressRoute 之相同 VNet 的點對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="09617-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="09617-119">點對站 VPN 和 ExpressRoute 不能並存在相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="09617-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="09617-120">**無法在站對站 VPN 閘道上啟用強制通道。**</span><span class="sxs-lookup"><span data-stu-id="09617-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="09617-121">您只可以「強制」所有網際網路繫結流量透過 ExpressRoute 回到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="09617-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="09617-122">**不支援基本 SKU 閘道。**</span><span class="sxs-lookup"><span data-stu-id="09617-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="09617-123">您必須對 [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)使用非基本 SKU 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="09617-124">**僅支援路由式 VPN 閘道。**</span><span class="sxs-lookup"><span data-stu-id="09617-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="09617-125">您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="09617-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="09617-126">**應該為 VPN 閘道設定靜態路由。**</span><span class="sxs-lookup"><span data-stu-id="09617-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="09617-127">如果您的區域網路連線到 ExpressRoute 和站對站 VPN，您必須在區域網路中設定靜態路由，才能將站對站 VPN 連線路由傳送到公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="09617-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="09617-128">**必須先設定 ExpressRoute 閘道。**</span><span class="sxs-lookup"><span data-stu-id="09617-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="09617-129">您必須先建立 ExpressRoute 閘道器，才能新增站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="09617-130">組態設計</span><span class="sxs-lookup"><span data-stu-id="09617-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="09617-131">設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑</span><span class="sxs-lookup"><span data-stu-id="09617-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="09617-132">您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。</span><span class="sxs-lookup"><span data-stu-id="09617-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="09617-133">這僅適用於連結至 Azure 私用對等路徑的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09617-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="09617-134">對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。</span><span class="sxs-lookup"><span data-stu-id="09617-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="09617-135">ExpressRoute 線路一律為主要連結。</span><span class="sxs-lookup"><span data-stu-id="09617-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="09617-136">只有在 ExpressRoute 線路故障時，資料才能流經站對站 VPN 路徑。</span><span class="sxs-lookup"><span data-stu-id="09617-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="09617-137">雖然當兩個路由相同時，ExpressRoute 線路偏好透過站對站 VPN，但 Azure 會使用最長的相符前置詞來選擇朝向封包目的地的路由。</span><span class="sxs-lookup"><span data-stu-id="09617-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![並存](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="09617-139">設定站對站 VPN 來連線到未透過 ExpressRoute 連接的網站</span><span class="sxs-lookup"><span data-stu-id="09617-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="09617-140">您可以將網路設定成有些網站透過站對站 VPN 直接連線到 Azure，而有些網站透過 ExpressRoute 來連線。</span><span class="sxs-lookup"><span data-stu-id="09617-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![並存](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="09617-142">您無法將虛擬網路設定為轉送路由器。</span><span class="sxs-lookup"><span data-stu-id="09617-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="09617-143">選取要使用的步驟</span><span class="sxs-lookup"><span data-stu-id="09617-143">Selecting the steps to use</span></span>
<span data-ttu-id="09617-144">如果要設定可並存的連線，有兩組不同的程序可供選擇。</span><span class="sxs-lookup"><span data-stu-id="09617-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="09617-145">您所選取的設定程序取決於您是已經有想要連線的現有虛擬網路，還是想要建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09617-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="09617-146">我沒有 VNet 且需要建立一個。</span><span class="sxs-lookup"><span data-stu-id="09617-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="09617-147">如果您還沒有虛擬網路，這個程序將引導您使用傳統部署模型來建立新的虛擬網路，並建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="09617-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="09617-148">若要設定，請依照 [建立新的虛擬網路和並存的連線](#new)一節中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="09617-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="09617-149">我已經有一個傳統部署模型 VNet。</span><span class="sxs-lookup"><span data-stu-id="09617-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="09617-150">您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="09617-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="09617-151">本文的 [為已經存在的 VNet 設定並存的連線](#add) 一節將引導您刪除閘道，然後建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="09617-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="09617-152">請注意，建立新的連線時，您必須以非常特定的順序來完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="09617-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="09617-153">請勿使用其他文章中的指示建立閘道器和連線。</span><span class="sxs-lookup"><span data-stu-id="09617-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="09617-154">在此程序中，建立可以並存的連線將會要求您刪除閘道器，然後設定新的閘道器。</span><span class="sxs-lookup"><span data-stu-id="09617-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="09617-155">這表示當您刪除和重新建立閘道器與連線時，將會有跨設備連線的停機時間，但您不需要將任何 VM 或服務移轉至新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09617-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="09617-156">您的 VM 和服務仍能透過負載平衡器對外通訊，而您能夠在這兩者設定為這樣做時進行閘道器設定。</span><span class="sxs-lookup"><span data-stu-id="09617-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="09617-157"><a name="new"></a>建立新的虛擬網路和並存的連線</span><span class="sxs-lookup"><span data-stu-id="09617-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="09617-158">此程序會引導您建立 VNet，並建立將並存的站對站和 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="09617-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="09617-159">您必須安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="09617-160">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="09617-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="09617-161">請注意，您將針對此組態使用的 Cmdlet 可能與您熟悉的 Cmdlet 有些微不同。</span><span class="sxs-lookup"><span data-stu-id="09617-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="09617-162">請務必使用這些指示中指定的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="09617-163">建立虛擬網路的結構描述。</span><span class="sxs-lookup"><span data-stu-id="09617-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="09617-164">如需關於組態結構描述的詳細資訊，請參閱 [Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09617-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="09617-165">當您建立結構描述時，請務必使用下列值：</span><span class="sxs-lookup"><span data-stu-id="09617-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="09617-166">虛擬網路的閘道器子網路必須是 /27 或更短的首碼 (例如 /26 或 /25)。</span><span class="sxs-lookup"><span data-stu-id="09617-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="09617-167">閘道器連線類型為「專用」。</span><span class="sxs-lookup"><span data-stu-id="09617-167">The gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="09617-168">建立和設定 XML 結構描述檔案後，請上傳該檔案。</span><span class="sxs-lookup"><span data-stu-id="09617-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="09617-169">這樣會建立您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09617-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="09617-170">使用下列 Cmdlet 來上傳檔案，將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09617-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="09617-171"><a name="gw"></a>建立 ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="09617-172">請務必將 GatewaySKU 指定為 *Standard*、*HighPerformance* 或 *UltraPerformance*，並將 GatewayType 指定為 *DynamicRouting*。</span><span class="sxs-lookup"><span data-stu-id="09617-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="09617-173">使用以下範例，將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09617-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="09617-174">將 ExpressRoute 閘道器連結到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="09617-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="09617-175">完成這個步驟之後，內部部署網路和 Azure 之間的連線 (透過 ExpressRoute ) 便會建立。</span><span class="sxs-lookup"><span data-stu-id="09617-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="09617-176"><a name="vpngw"></a>接下來，建立站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="09617-177">GatewaySKU 必須是 *Standard*、*HighPerformance* 或 *UltraPerformance*，而 GatewayType 必須是 *DynamicRouting*。</span><span class="sxs-lookup"><span data-stu-id="09617-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="09617-178">若要擷取虛擬網路閘道設定 (包括閘道識別碼和公用 IP)，請使用 `Get-AzureVirtualNetworkGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="09617-179">建立本機的站台 VPN 閘道實體。</span><span class="sxs-lookup"><span data-stu-id="09617-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="09617-180">此命令不會設定內部部署 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="09617-181">相反地，它可讓您提供本機閘道器設定 (例如公用 IP 與內部位址空間)，使 Azure VPN 閘道能夠與其連線。</span><span class="sxs-lookup"><span data-stu-id="09617-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="09617-182">未在 Netcfg 中定義站對站 VPN 的本機站台。</span><span class="sxs-lookup"><span data-stu-id="09617-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="09617-183">您必須改為使用此 Cmdlet 來指定本機站台參數。</span><span class="sxs-lookup"><span data-stu-id="09617-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="09617-184">您無法使用入口網站或 Netcfg 檔來定義參數。</span><span class="sxs-lookup"><span data-stu-id="09617-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="09617-185">使用下列範例，將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09617-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="09617-186">如果您的區域網路有多個路由，您可以將它們全部放在陣列中傳遞。</span><span class="sxs-lookup"><span data-stu-id="09617-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="09617-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="09617-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="09617-188">若要擷取虛擬網路閘道設定 (包括閘道識別碼和公用 IP)，請使用 `Get-AzureVirtualNetworkGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="09617-189">請參閱下列範例。</span><span class="sxs-lookup"><span data-stu-id="09617-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="09617-190">設定本機 VPN 裝置以連線到新的閘道器。</span><span class="sxs-lookup"><span data-stu-id="09617-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="09617-191">當您設定 VPN 裝置時，請使用於步驟 6 所抓取的資訊。</span><span class="sxs-lookup"><span data-stu-id="09617-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="09617-192">如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="09617-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="09617-193">將 Azure 上的站對站 VPN 閘道連結至本機閘道器。</span><span class="sxs-lookup"><span data-stu-id="09617-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="09617-194">在此範例中，connectedEntityId 是本機的閘道器識別碼，您可以透過執行 `Get-AzureLocalNetworkGateway`找到此識別碼。</span><span class="sxs-lookup"><span data-stu-id="09617-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="09617-195">您可以使用 `Get-AzureVirtualNetworkGateway` Cmdlet 尋找 virtualNetworkGatewayId。</span><span class="sxs-lookup"><span data-stu-id="09617-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="09617-196">完成這個步驟之後，區域網路和 Azure 之間的連線 (透過站對站 VPN 連線) 便會建立。</span><span class="sxs-lookup"><span data-stu-id="09617-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="09617-197"><a name="add"></a>為已經存在的 VNet 設定並存的連線</span><span class="sxs-lookup"><span data-stu-id="09617-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="09617-198">如果您有現有的虛擬網路，請檢查閘道器子網路大小。</span><span class="sxs-lookup"><span data-stu-id="09617-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="09617-199">如果閘道器子網路是/28 或/29，您必須先刪除虛擬網路閘道器，並增加閘道器子網路大小。</span><span class="sxs-lookup"><span data-stu-id="09617-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="09617-200">本節中的步驟將示範如何執行該作業。</span><span class="sxs-lookup"><span data-stu-id="09617-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="09617-201">如果閘道器子網路是/27 以上且虛擬網路是透過 ExpressRoute 連線，則可以略過下列步驟，並且繼續進行上一節中的 [「步驟 6 - 建立站對站 VPN 閘道」](#vpngw) 。</span><span class="sxs-lookup"><span data-stu-id="09617-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="09617-202">當您刪除現有閘道器時，您在進行此設定時，本機設備將會與虛擬網路中斷連線。</span><span class="sxs-lookup"><span data-stu-id="09617-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="09617-203">您必須安裝最新版的 Azure 資源管理員 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="09617-204">如需如何安裝 PowerShell Cmdlet 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="09617-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="09617-205">請注意，您將針對此組態使用的 Cmdlet 可能與您熟悉的 Cmdlet 有些微不同。</span><span class="sxs-lookup"><span data-stu-id="09617-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="09617-206">請務必使用這些指示中指定的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="09617-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="09617-207">刪除現有的 ExpressRoute 或站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="09617-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="09617-208">使用下列 Cmdlet，將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09617-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="09617-209">匯出虛擬網路的結構描述。</span><span class="sxs-lookup"><span data-stu-id="09617-209">Export the virtual network schema.</span></span> <span data-ttu-id="09617-210">使用下列 PowerShell Cmdlet，將該值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="09617-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="09617-211">編輯網路組態檔結構描述，讓閘道器子網路是 /27 或更短的首碼 (例如 /26 或 /25)。</span><span class="sxs-lookup"><span data-stu-id="09617-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="09617-212">請參閱下列範例。</span><span class="sxs-lookup"><span data-stu-id="09617-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="09617-213">如果您的虛擬網路中沒有足夠的 IP 位址可以增加閘道器子網路大小，您必須新增更多 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="09617-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="09617-214">如需關於組態結構描述的詳細資訊，請參閱 [Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09617-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="09617-215">如果您先前的閘道是站對站 VPN，則也必須將連線類型變更為 [專用] 。</span><span class="sxs-lookup"><span data-stu-id="09617-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="09617-216">此時，您必須使用沒有閘道器的 VNet。</span><span class="sxs-lookup"><span data-stu-id="09617-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="09617-217">若要建立新的閘道器並完成連接，您可以繼續進行 [步驟 4 - 建立 ExpressRoute 閘道器](#gw)(您可以在先前的步驟組中找到)。</span><span class="sxs-lookup"><span data-stu-id="09617-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09617-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09617-218">Next steps</span></span>
<span data-ttu-id="09617-219">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="09617-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

