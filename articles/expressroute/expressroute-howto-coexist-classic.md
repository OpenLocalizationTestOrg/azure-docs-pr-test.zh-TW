---
title: "設定可以並存的 ExpressRoute 和站對站 VPN 連線：傳統：Azure | Microsoft Docs"
description: "這篇文章會引導您設定 ExpressRoute 和 hello 傳統部署模型可同時存在站對站 VPN 連線。"
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
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="57574-103">設定 ExpressRoute 和站對站並存連線 (傳統)</span><span class="sxs-lookup"><span data-stu-id="57574-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57574-104">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="57574-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="57574-105">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="57574-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="57574-106">Hello 能力 tooconfigure 站對站 VPN 和 ExpressRoute 會有幾項優點。</span><span class="sxs-lookup"><span data-stu-id="57574-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="57574-107">您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExressRoute，或使用站對站 Vpn tooconnect toosites 不透過 ExpressRoute 連接。</span><span class="sxs-lookup"><span data-stu-id="57574-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="57574-108">我們將討論 hello 步驟 tooconfigure 本文章中的這兩種案例。</span><span class="sxs-lookup"><span data-stu-id="57574-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="57574-109">本文適用於 toohello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="57574-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="57574-110">此設定不在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="57574-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="57574-111">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="57574-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="57574-112">ExpressRoute 電路必須預先設定，才能執行下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="57574-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="57574-113">請確定您已依照 hello 指南太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)和[設定路由](expressroute-howto-routing-classic.md)依照下列步驟 hello 之前。</span><span class="sxs-lookup"><span data-stu-id="57574-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="57574-114">限制</span><span class="sxs-lookup"><span data-stu-id="57574-114">Limits and limitations</span></span>
* <span data-ttu-id="57574-115">**不支援傳輸路由。**</span><span class="sxs-lookup"><span data-stu-id="57574-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="57574-116">您無法在透過站對站 VPN 連線的區域網路與透過 ExpressRoute 連線的區域網路之間，進行路由傳送 (透過 Azure)。</span><span class="sxs-lookup"><span data-stu-id="57574-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="57574-117">**不支援點對站連線。**</span><span class="sxs-lookup"><span data-stu-id="57574-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="57574-118">您無法啟用點對站 VPN 連線 toohello 連接的 tooExpressRoute 相同 VNet。</span><span class="sxs-lookup"><span data-stu-id="57574-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="57574-119">點對站 VPN 和 ExpressRoute 不能共存在 hello 相同 VNet。</span><span class="sxs-lookup"><span data-stu-id="57574-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="57574-120">**無法在 hello 站對站 VPN 閘道上啟用強制通道。**</span><span class="sxs-lookup"><span data-stu-id="57574-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="57574-121">您可以只 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署網路透過 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="57574-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="57574-122">**不支援基本 SKU 閘道。**</span><span class="sxs-lookup"><span data-stu-id="57574-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="57574-123">您必須使用非基本 SKU 閘道可取得這兩個 hello [ExpressRoute 閘道](expressroute-about-virtual-network-gateways.md)和 hello [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="57574-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="57574-124">**僅支援路由式 VPN 閘道。**</span><span class="sxs-lookup"><span data-stu-id="57574-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="57574-125">您必須使用路由式 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="57574-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="57574-126">**應該為 VPN 閘道設定靜態路由。**</span><span class="sxs-lookup"><span data-stu-id="57574-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="57574-127">如果您的區域網路連線的 tooboth ExpressRoute 而且網站間 VPN，您必須在您區域網路 tooroute hello 站對站 VPN 連線 toohello 中設定的靜態路由公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="57574-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="57574-128">**必須先設定 ExpressRoute 閘道。**</span><span class="sxs-lookup"><span data-stu-id="57574-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="57574-129">新增 hello 站對站 VPN 閘道之前，您必須先建立 hello ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="57574-130">組態設計</span><span class="sxs-lookup"><span data-stu-id="57574-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="57574-131">設定站對站 VPN 作為 ExpressRoute 的容錯移轉路徑</span><span class="sxs-lookup"><span data-stu-id="57574-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="57574-132">您可以設定站對站 VPN 連線作為 ExpressRoute 的備用連線。</span><span class="sxs-lookup"><span data-stu-id="57574-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="57574-133">這適用於僅 toovirtual 網路連結的 toohello Azure 私人互連路徑。</span><span class="sxs-lookup"><span data-stu-id="57574-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="57574-134">對於可透過 Azure 公用和 Microsoft 對等存取的服務，沒有 VPN 架構的容錯移轉解決方案。</span><span class="sxs-lookup"><span data-stu-id="57574-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="57574-135">hello ExpressRoute 電路一律為 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="57574-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="57574-136">只有 hello ExpressRoute 電路失敗時，資料會流透過 hello 站對站 VPN 的路徑。</span><span class="sxs-lookup"><span data-stu-id="57574-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="57574-137">雖然 ExpressRoute 循環時，最好透過站對站 VPN 這兩個路由是 hello 相同，則 Azure 會使用 hello 最長前置詞比對 toochoose hello 路由朝向 hello 封包的目的地。</span><span class="sxs-lookup"><span data-stu-id="57574-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![並存](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="57574-139">設定站對站 VPN tooconnect toosites 未透過 ExpressRoute 連線</span><span class="sxs-lookup"><span data-stu-id="57574-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="57574-140">您可以設定您的網路，其中某些站台直接 tooAzure 透過站對站 VPN 連接，而透過 ExpressRoute 連接某些站台。</span><span class="sxs-lookup"><span data-stu-id="57574-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![並存](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="57574-142">您無法將虛擬網路設定為轉送路由器。</span><span class="sxs-lookup"><span data-stu-id="57574-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="57574-143">選取 hello 步驟 toouse</span><span class="sxs-lookup"><span data-stu-id="57574-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="57574-144">有兩組不同的程序 toochoose 從順序 tooconfigure 連接中，可以共存。</span><span class="sxs-lookup"><span data-stu-id="57574-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="57574-145">您選取的 hello 組態程序將取決於您是否有現有的虛擬網路，您會想 tooconnect，或是 toocreate 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57574-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="57574-146">我不具有 VNet，而且需要 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="57574-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="57574-147">如果您還沒有虛擬網路，此程序將逐步引導您建立新的虛擬網路使用 hello 傳統部署模型，並建立新的 ExpressRoute 以及站台對站台 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="57574-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="57574-148">tooconfigure，遵循 hello 發行項 > 一節中的 hello 步驟[toocreate 新的虛擬網路和共存連線](#new)。</span><span class="sxs-lookup"><span data-stu-id="57574-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="57574-149">我已經有一個傳統部署模型 VNet。</span><span class="sxs-lookup"><span data-stu-id="57574-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="57574-150">您可能已經有虛擬網路，而且使用現有的站對站 VPN 連線或 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="57574-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="57574-151">hello 文章區段[tooconfigure coexsiting 連線已存在的 vnet](#add)將逐步引導您透過刪除 hello 閘道，然後建立新的 ExpressRoute 和站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="57574-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="57574-152">請注意，在建立新的連線時 hello，hello 必須完成步驟非常特定的順序。</span><span class="sxs-lookup"><span data-stu-id="57574-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="57574-153">請勿使用其他發行項 toocreate hello 指示進行，您的閘道和連線。</span><span class="sxs-lookup"><span data-stu-id="57574-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="57574-154">在此程序，建立可同時存在的連接會需要您 toodelete 您的閘道，然後設定新的閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="57574-155">這表示您必須跨單位連線的停機時間時就刪除並重新建立您的閘道與連線，但您不需要 toomigrate 任何 Vm 或服務 tooa 新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57574-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="57574-156">Vm 和服務仍會無法 toocommunicate 出透過 hello 負載平衡器時所設定的 toodo 因此，設定您的閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="57574-157"><a name="new"></a>toocreate 新的虛擬網路和共存的連線</span><span class="sxs-lookup"><span data-stu-id="57574-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="57574-158">此程序會引導您建立 VNet，並建立將並存的站對站和 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="57574-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="57574-159">您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="57574-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="57574-160">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="57574-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="57574-161">請注意 hello cmdlet，您將使用此組態可能會與您可能的熟悉稍有不同。</span><span class="sxs-lookup"><span data-stu-id="57574-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="57574-162">確定 toouse hello cmdlet 這些指示中指定。</span><span class="sxs-lookup"><span data-stu-id="57574-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="57574-163">建立虛擬網路的結構描述。</span><span class="sxs-lookup"><span data-stu-id="57574-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="57574-164">如需 hello 組態結構描述的詳細資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57574-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="57574-165">當您建立您的結構描述時，請確定您使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="57574-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="57574-166">hello hello 虛擬網路的閘道子網路必須 /27 或短的前置詞 （例如 /26 或 /25）。</span><span class="sxs-lookup"><span data-stu-id="57574-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="57574-167">hello 閘道連線類型是 「 專用。 」</span><span class="sxs-lookup"><span data-stu-id="57574-167">hello gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="57574-168">建立及設定您的 xml 結構描述檔案之後, hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="57574-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="57574-169">這樣會建立您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="57574-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="57574-170">使用下列 cmdlet tooupload hello 檔案，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="57574-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="57574-171"><a name="gw"></a>建立 ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="57574-172">是確定 toospecify hello 做為 GatewaySKU*標準*， *HighPerformance*，或*UltraPerformance* hello 做為 gatewaytype 的授權和*DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="57574-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="57574-173">使用下列範例中，取代為您自己的 hello 值 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="57574-174">連結 hello ExpressRoute 閘道 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="57574-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="57574-175">在完成這個步驟之後，會建立 hello 與內部網路與 Azure 中的，透過 ExpressRoute，之間的連線。</span><span class="sxs-lookup"><span data-stu-id="57574-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="57574-176"><a name="vpngw"></a>接下來，建立站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="57574-177">hello GatewaySKU 必須*標準*， *HighPerformance*，或*UltraPerformance*而且 hello gatewaytype 的授權必須*DynamicRouting*。</span><span class="sxs-lookup"><span data-stu-id="57574-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="57574-178">tooretrieve hello 虛擬網路閘道設定，包括 hello 閘道識別碼和 hello 公用 IP，使用 hello `Get-AzureVirtualNetworkGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="57574-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
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
7. <span data-ttu-id="57574-179">建立本機的站台 VPN 閘道實體。</span><span class="sxs-lookup"><span data-stu-id="57574-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="57574-180">此命令不會設定內部部署 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="57574-181">相反地，它可讓您 tooprovide hello 本機閘道設定，例如 hello 公用 IP 和 hello 在內部部署位址空間，如此 hello Azure VPN 閘道可以連線 tooit。</span><span class="sxs-lookup"><span data-stu-id="57574-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="57574-182">hello netcfg 中未定義本機 hello hello 站對站 VPN 站台。</span><span class="sxs-lookup"><span data-stu-id="57574-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="57574-183">相反地，您必須使用這個指令程式 toospecify hello 本機站台參數。</span><span class="sxs-lookup"><span data-stu-id="57574-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="57574-184">您無法使用入口網站或 hello netcfg 檔案，其定義。</span><span class="sxs-lookup"><span data-stu-id="57574-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="57574-185">使用下列範例中，取代您自己 hello 值 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="57574-186">如果您的區域網路有多個路由，您可以將它們全部放在陣列中傳遞。</span><span class="sxs-lookup"><span data-stu-id="57574-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="57574-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="57574-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="57574-188">tooretrieve hello 虛擬網路閘道設定，包括 hello 閘道識別碼和 hello 公用 IP，使用 hello `Get-AzureVirtualNetworkGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="57574-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="57574-189">請參閱下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="57574-190">設定本機 VPN 裝置 tooconnect toohello 新閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="57574-191">使用您在步驟 6 中設定 VPN 裝置時擷取的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="57574-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="57574-192">如需關於 VPN 裝置組態的詳細資訊，請參閱 [VPN 裝置組態](../vpn-gateway/vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="57574-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="57574-193">連結 hello Azure toohello 本機閘道上的站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="57574-194">在此範例中，connectedEntityId 是 hello 本機閘道識別碼，您可以執行尋找`Get-AzureLocalNetworkGateway`。</span><span class="sxs-lookup"><span data-stu-id="57574-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="57574-195">您可以使用 hello 找到 virtualNetworkGatewayId `Get-AzureVirtualNetworkGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="57574-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="57574-196">這個步驟之後，hello 您區域網路與 Azure 之間 hello 站對站 VPN 連線透過連接。</span><span class="sxs-lookup"><span data-stu-id="57574-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="57574-197"><a name="add"></a>現有的 VNet 的 tooconfigure coexsiting 連線</span><span class="sxs-lookup"><span data-stu-id="57574-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="57574-198">如果您有現有的虛擬網路，請檢查 hello 閘道子網路大小。</span><span class="sxs-lookup"><span data-stu-id="57574-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="57574-199">如果 hello 閘道子網路是/28 或 29，您必須先刪除 hello 虛擬網路閘道並增加 hello 閘道子網路大小。</span><span class="sxs-lookup"><span data-stu-id="57574-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="57574-200">hello 本節中的步驟將示範如何 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="57574-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="57574-201">Hello 閘道子網路是否 /27 或更大而且透過 ExpressRoute 連接 hello 虛擬網路，您可以略過下列步驟 hello 而太[[步驟 6-建立站對站 VPN 閘道]](#vpngw) hello 前一節中。</span><span class="sxs-lookup"><span data-stu-id="57574-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="57574-202">當您刪除 hello 現有閘道時，您本機內部部署將會遺失 hello 連接 tooyour 虛擬網路，當您使用此設定。</span><span class="sxs-lookup"><span data-stu-id="57574-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="57574-203">您將需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="57574-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="57574-204">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="57574-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="57574-205">請注意 hello cmdlet，您將使用此組態可能會與您可能的熟悉稍有不同。</span><span class="sxs-lookup"><span data-stu-id="57574-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="57574-206">確定 toouse hello cmdlet 這些指示中指定。</span><span class="sxs-lookup"><span data-stu-id="57574-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="57574-207">刪除 hello 現有 ExpressRoute 或站對站 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="57574-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="57574-208">使用下列 cmdlet，取代您自己 hello 值 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="57574-209">匯出 hello 虛擬網路的結構描述。</span><span class="sxs-lookup"><span data-stu-id="57574-209">Export hello virtual network schema.</span></span> <span data-ttu-id="57574-210">使用下列 PowerShell cmdlet，取代您自己 hello 值 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="57574-211">編輯 hello 網路組態檔結構描述，以便 hello 閘道子網路是 /27 或短的前置詞 （例如 /26 或 /25）。</span><span class="sxs-lookup"><span data-stu-id="57574-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="57574-212">請參閱下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="57574-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="57574-213">如果您沒有足夠的 IP 位址保留在您虛擬網路 tooincrease hello 閘道子網路大小，您需要 tooadd 多個 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="57574-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="57574-214">如需 hello 組態結構描述的詳細資訊，請參閱[Azure 虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57574-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="57574-215">如果您先前的閘道站對站 VPN，您也必須變更 hello 連線類型太**專用**。</span><span class="sxs-lookup"><span data-stu-id="57574-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="57574-216">此時，您必須使用沒有閘道器的 VNet。</span><span class="sxs-lookup"><span data-stu-id="57574-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="57574-217">toocreate 新的閘道完成您的連線，您可以繼續使用[步驟 4-建立 ExpressRoute 閘道](#gw)、 在 hello 前面的步驟中找到。</span><span class="sxs-lookup"><span data-stu-id="57574-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57574-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57574-218">Next steps</span></span>
<span data-ttu-id="57574-219">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="57574-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

