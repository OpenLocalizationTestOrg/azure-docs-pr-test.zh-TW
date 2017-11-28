---
title: "aaaAzure VPN 閘道常見問題集 |Microsoft 文件"
description: "hello VPN 閘道常見問題集。 Microsoft Azure 虛擬網路跨單位連線、混合式組態連線和 VPN 閘道的常見問題集。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a><span data-ttu-id="918e9-104">VPN 閘道常見問題集</span><span class="sxs-lookup"><span data-stu-id="918e9-104">VPN Gateway FAQ</span></span>

## <span data-ttu-id="918e9-105"><a name="connecting"></a>Toovirtual 網路連接</span><span class="sxs-lookup"><span data-stu-id="918e9-105"><a name="connecting"></a>Connecting toovirtual networks</span></span>

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a><span data-ttu-id="918e9-106">是否可以連接不同 Azure 區域中的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="918e9-106">Can I connect virtual networks in different Azure regions?</span></span>

<span data-ttu-id="918e9-107">是。</span><span class="sxs-lookup"><span data-stu-id="918e9-107">Yes.</span></span> <span data-ttu-id="918e9-108">事實上，沒有區域限制。</span><span class="sxs-lookup"><span data-stu-id="918e9-108">In fact, there is no region constraint.</span></span> <span data-ttu-id="918e9-109">一個虛擬網路可以連接 tooanother hello 中的虛擬網路相同的區域，或在不同的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="918e9-109">One virtual network can connect tooanother virtual network in hello same region, or in a different Azure region.</span></span> 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a><span data-ttu-id="918e9-110">是否可以使用不同訂用帳戶連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="918e9-110">Can I connect virtual networks in different subscriptions?</span></span>

<span data-ttu-id="918e9-111">是。</span><span class="sxs-lookup"><span data-stu-id="918e9-111">Yes.</span></span>

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a><span data-ttu-id="918e9-112">可以從單一虛擬網路連接 toomultiple 網站嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-112">Can I connect toomultiple sites from a single virtual network?</span></span>

<span data-ttu-id="918e9-113">您可以使用 Windows PowerShell 和 hello Azure REST Api 連接 toomultiple 站台。</span><span class="sxs-lookup"><span data-stu-id="918e9-113">You can connect toomultiple sites by using Windows PowerShell and hello Azure REST APIs.</span></span> <span data-ttu-id="918e9-114">請參閱 hello[多網站和 VNet 對 VNet 連線能力](#V2VMulti)常見問題集 > 一節。</span><span class="sxs-lookup"><span data-stu-id="918e9-114">See hello [Multi-Site and VNet-to-VNet Connectivity](#V2VMulti) FAQ section.</span></span>

### <a name="what-are-my-cross-premises-connection-options"></a><span data-ttu-id="918e9-115">有哪些跨單位連線選項？</span><span class="sxs-lookup"><span data-stu-id="918e9-115">What are my cross-premises connection options?</span></span>

<span data-ttu-id="918e9-116">支援連線 hello 下列跨單位：</span><span class="sxs-lookup"><span data-stu-id="918e9-116">hello following cross-premises connections are supported:</span></span>

* <span data-ttu-id="918e9-117">站對站 – 透過 IPsec (IKE v1 和 IKE v2) 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="918e9-117">Site-to-Site – VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="918e9-118">此類型的連線需要 VPN 裝置或 RRAS。</span><span class="sxs-lookup"><span data-stu-id="918e9-118">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="918e9-119">如需詳細資訊，請參閱[站對站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-119">For more information, see [Site-to-Site](vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="918e9-120">點對站 – 透過 SSTP (安全通訊端通道通訊協定) 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="918e9-120">Point-to-Site – VPN connection over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="918e9-121">此連線不需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="918e9-121">This connection does not require a VPN device.</span></span> <span data-ttu-id="918e9-122">如需詳細資訊，請參閱[點對站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-122">For more information, see [Point-to-Site](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="918e9-123">VNet 對 VNet – 這種類型的連接是 hello 做為站對站組態相同。</span><span class="sxs-lookup"><span data-stu-id="918e9-123">VNet-to-VNet – This type of connection is hello same as a Site-to-Site configuration.</span></span> <span data-ttu-id="918e9-124">VNet tooVNet 是透過 IPsec （IKE v1 和 IKE v2） 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="918e9-124">VNet tooVNet is a VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="918e9-125">並不需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="918e9-125">It does not require a VPN device.</span></span> <span data-ttu-id="918e9-126">如需詳細資訊，請參閱 [VNet 對 VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-126">For more information, see [VNet-to-VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>
* <span data-ttu-id="918e9-127">這是一種可讓您 tooconnect 站對站組態的多站台 – 多個內部部署站台 tooa 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-127">Multi-Site – This is a variation of a Site-to-Site configuration that allows you tooconnect multiple on-premises sites tooa virtual network.</span></span> <span data-ttu-id="918e9-128">如需詳細資訊，請參閱[多網站](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-128">For more information, see [Multi-Site](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="918e9-129">ExpressRoute – ExpressRoute 是從您的 WAN 不 hello 透過 VPN 連線的直接連線 tooAzure 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-129">ExpressRoute – ExpressRoute is a direct connection tooAzure from your WAN, not a VPN connection over hello public Internet.</span></span> <span data-ttu-id="918e9-130">如需詳細資訊，請參閱 hello [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)和 hello [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-130">For more information, see hello [ExpressRoute Technical Overview](../expressroute/expressroute-introduction.md) and hello [ExpressRoute FAQ](../expressroute/expressroute-faqs.md).</span></span>

<span data-ttu-id="918e9-131">如需 VPN 閘道連線的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-131">For more information about VPN gateway connections, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a><span data-ttu-id="918e9-132">Hello 站對站連接和點對站台之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="918e9-132">What is hello difference between a Site-to-Site connection and Point-to-Site?</span></span>

<span data-ttu-id="918e9-133">**站對站**(IPsec/IKE VPN 通道) 介於內部部署位置與 Azure 之間。</span><span class="sxs-lookup"><span data-stu-id="918e9-133">**Site-to-Site** (IPsec/IKE VPN tunnel) configurations are between your on-premises location and Azure.</span></span> <span data-ttu-id="918e9-134">這表示您可以從您的電腦位於您的內部部署 tooany 虛擬機器或虛擬網路，視您選擇 tooconfigure 路由和權限中的角色執行個體連接。</span><span class="sxs-lookup"><span data-stu-id="918e9-134">This means that you can connect from any of your computers located on your premises tooany virtual machine or role instance within your virtual network, depending on how you choose tooconfigure routing and permissions.</span></span> <span data-ttu-id="918e9-135">對於永遠可用的跨單位連線而言，這是不錯的選項，而且非常適合於混合式組態。</span><span class="sxs-lookup"><span data-stu-id="918e9-135">It's a great option for an always-available cross-premises connection and is well-suited for hybrid configurations.</span></span> <span data-ttu-id="918e9-136">這種連接會依賴的 IPsec VPN 應用裝置 （硬體裝置或軟體應用裝置），必須部署在您的網路 hello 邊緣。</span><span class="sxs-lookup"><span data-stu-id="918e9-136">This type of connection relies on an IPsec VPN appliance (hardware device or soft appliance), which must be deployed at hello edge of your network.</span></span> <span data-ttu-id="918e9-137">toocreate 這種連接，您必須具有對外開放的 IPv4 位址不是 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="918e9-137">toocreate this type of connection, you must have an externally facing IPv4 address that is not behind a NAT.</span></span>

<span data-ttu-id="918e9-138">**點對站台**(透過 SSTP VPN) 組態可讓您從單一電腦從任何地方連線 tooanything 位於您虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="918e9-138">**Point-to-Site** (VPN over SSTP) configurations let you connect from a single computer from anywhere tooanything located in your virtual network.</span></span> <span data-ttu-id="918e9-139">它會使用 Windows 內建 VPN 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="918e9-139">It uses hello Windows in-box VPN client.</span></span> <span data-ttu-id="918e9-140">Hello 點對站組態的一部分，您必須安裝憑證和 VPN 用戶端組態封裝，其中包含 hello 設定可讓您的電腦 tooconnect tooany 虛擬機器或 hello 虛擬網路內的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="918e9-140">As part of hello Point-to-Site configuration, you install a certificate and a VPN client configuration package, which contains hello settings that allow your computer tooconnect tooany virtual machine or role instance within hello virtual network.</span></span> <span data-ttu-id="918e9-141">當您想 tooconnect tooa 虛擬網路，但不是位在內部，很棒。</span><span class="sxs-lookup"><span data-stu-id="918e9-141">It's great when you want tooconnect tooa virtual network, but aren't located on-premises.</span></span> <span data-ttu-id="918e9-142">它時也是不錯的選擇您沒有存取 tooVPN 硬體或對外的 IPv4 位址，兩者都是必要的站對站連線。</span><span class="sxs-lookup"><span data-stu-id="918e9-142">It's also a good option when you don't have access tooVPN hardware or an externally facing IPv4 address, both of which are required for a Site-to-Site connection.</span></span>

<span data-ttu-id="918e9-143">您可以設定虛擬網路 toouse 這兩個站台間和點對站同時，只要您在建立使用路由式 VPN 站對站連線您的閘道類型。</span><span class="sxs-lookup"><span data-stu-id="918e9-143">You can configure your virtual network toouse both Site-to-Site and Point-to-Site concurrently, as long as you create your Site-to-Site connection using a route-based VPN type for your gateway.</span></span> <span data-ttu-id="918e9-144">路由式 VPN 類型 hello 傳統部署模型中稱為動態閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-144">Route-based VPN types are called dynamic gateways in hello classic deployment model.</span></span>

## <span data-ttu-id="918e9-145"><a name="gateways"></a>虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="918e9-145"><a name="gateways"></a>Virtual network gateways</span></span>

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a><span data-ttu-id="918e9-146">VPN 閘道是虛擬網路閘道嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-146">Is a VPN gateway a virtual network gateway?</span></span>

<span data-ttu-id="918e9-147">VPN 閘道是一種虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-147">A VPN gateway is a type of virtual network gateway.</span></span> <span data-ttu-id="918e9-148">VPN 閘道可透過公用連線在您的虛擬網路和內部部署位置之間傳送加密流量。</span><span class="sxs-lookup"><span data-stu-id="918e9-148">A VPN gateway sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="918e9-149">您也可以使用虛擬網路之間的 VPN 閘道 toosend 流量。</span><span class="sxs-lookup"><span data-stu-id="918e9-149">You can also use a VPN gateway toosend traffic between virtual networks.</span></span> <span data-ttu-id="918e9-150">當您建立 VPN 閘道時，您會使用 hello-gatewaytype 的授權值 'Vpn'。</span><span class="sxs-lookup"><span data-stu-id="918e9-150">When you create a VPN gateway, you use hello -GatewayType value 'Vpn'.</span></span> <span data-ttu-id="918e9-151">如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-151">For more information, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>

### <a name="what-is-a-policy-based-static-routing-gateway"></a><span data-ttu-id="918e9-152">什麼是以原則為基礎的 (靜態路由) 閘道？</span><span class="sxs-lookup"><span data-stu-id="918e9-152">What is a policy-based (static-routing) gateway?</span></span>

<span data-ttu-id="918e9-153">以原則為基礎的閘道會實作原則式 VPN。</span><span class="sxs-lookup"><span data-stu-id="918e9-153">Policy-based gateways implement policy-based VPNs.</span></span> <span data-ttu-id="918e9-154">原則式 Vpn 會加密，並直接透過 IPsec 通道，根據您在內部部署網路與 hello Azure VNet 之間的位址首碼的 hello 組合的封包。</span><span class="sxs-lookup"><span data-stu-id="918e9-154">Policy-based VPNs encrypt and direct packets through IPsec tunnels based on hello combinations of address prefixes between your on-premises network and hello Azure VNet.</span></span> <span data-ttu-id="918e9-155">hello 原則 （或傳輸選取器） 通常定義為存取清單中 hello VPN 組態。</span><span class="sxs-lookup"><span data-stu-id="918e9-155">hello policy (or Traffic Selector) is usually defined as an access list in hello VPN configuration.</span></span>

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a><span data-ttu-id="918e9-156">什麼是以路由為基礎的 (動態路由) 閘道？</span><span class="sxs-lookup"><span data-stu-id="918e9-156">What is a route-based (dynamic-routing) gateway?</span></span>

<span data-ttu-id="918e9-157">路由式閘道實作 hello 路由式 Vpn。</span><span class="sxs-lookup"><span data-stu-id="918e9-157">Route-based gateways implement hello route-based VPNs.</span></span> <span data-ttu-id="918e9-158">路由式 Vpn hello IP 轉送或路由資料表 toodirect 封包傳送至其相對應的通道介面中使用 「 路由 」。</span><span class="sxs-lookup"><span data-stu-id="918e9-158">Route-based VPNs use "routes" in hello IP forwarding or routing table toodirect packets into their corresponding tunnel interfaces.</span></span> <span data-ttu-id="918e9-159">然後 hello 通道介面加密或解密出 hello 通道 hello 封包。</span><span class="sxs-lookup"><span data-stu-id="918e9-159">hello tunnel interfaces then encrypt or decrypt hello packets in and out of hello tunnels.</span></span> <span data-ttu-id="918e9-160">路由式 Vpn 會設定為任何-到-any hello 原則或流量的選取器 （或萬用字元）。</span><span class="sxs-lookup"><span data-stu-id="918e9-160">hello policy or traffic selector for route-based VPNs are configured as any-to-any (or wild cards).</span></span>

### <a name="do-i-need-a-gatewaysubnet"></a><span data-ttu-id="918e9-161">是否需要 'GatewaySubnet'？</span><span class="sxs-lookup"><span data-stu-id="918e9-161">Do I need a 'GatewaySubnet'?</span></span>

<span data-ttu-id="918e9-162">是。</span><span class="sxs-lookup"><span data-stu-id="918e9-162">Yes.</span></span> <span data-ttu-id="918e9-163">hello 閘道子網路包含 hello hello 虛擬網路閘道服務使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="918e9-163">hello gateway subnet contains hello IP addresses that hello virtual network gateway services use.</span></span> <span data-ttu-id="918e9-164">您的 VNet 中順序 tooconfigure 虛擬網路閘道需要 toocreate 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-164">You need toocreate a gateway subnet for your VNet in order tooconfigure a virtual network gateway.</span></span> <span data-ttu-id="918e9-165">所有的閘道子網路必須命名為 'GatewaySubnet' toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="918e9-165">All gateway subnets must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="918e9-166">請勿將閘道子網路命名為其他名稱。</span><span class="sxs-lookup"><span data-stu-id="918e9-166">Don't name your gateway subnet something else.</span></span> <span data-ttu-id="918e9-167">並不會部署到 Vm 或任何其他 toohello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-167">And don't deploy VMs or anything else toohello gateway subnet.</span></span>

<span data-ttu-id="918e9-168">當您建立 hello 閘道子網路時，您可以指定包含 hello hello 子網路的 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="918e9-168">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="918e9-169">hello hello 閘道子網路中的 IP 位址被配置 toohello 閘道服務。</span><span class="sxs-lookup"><span data-stu-id="918e9-169">hello IP addresses in hello gateway subnet are allocated toohello gateway service.</span></span> <span data-ttu-id="918e9-170">部分設定需要多個 IP 位址 toobe 配置 toohello 閘道服務一樣，其他人。</span><span class="sxs-lookup"><span data-stu-id="918e9-170">Some configurations require more IP addresses toobe allocated toohello gateway services than do others.</span></span> <span data-ttu-id="918e9-171">您想 toomake 確定您的閘道子網路包含足夠的 IP 位址 tooaccommodate 未來的成長和可能的其他新連線設定。</span><span class="sxs-lookup"><span data-stu-id="918e9-171">You want toomake sure your gateway subnet contains enough IP addresses tooaccommodate future growth and possible additional new connection configurations.</span></span> <span data-ttu-id="918e9-172">所以﹐您可以建立像 /29 這麼小的閘道子網路，但建議您建立 /27 或更大 (/27、/26、/25 等) 的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-172">So, while you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /27 or larger (/27, /26, /25 etc.).</span></span> <span data-ttu-id="918e9-173">您想 toocreate，並確認您擁有 hello 閘道子網路會符合這些需求，請查看 hello hello 組態需求。</span><span class="sxs-lookup"><span data-stu-id="918e9-173">Look at hello requirements for hello configuration that you want toocreate and verify that hello gateway subnet you have will meet those requirements.</span></span>

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a><span data-ttu-id="918e9-174">可以部署虛擬機器或角色執行個體 toomy 閘道子網路嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-174">Can I deploy Virtual Machines or role instances toomy gateway subnet?</span></span>

<span data-ttu-id="918e9-175">否。</span><span class="sxs-lookup"><span data-stu-id="918e9-175">No.</span></span>

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a><span data-ttu-id="918e9-176">在建立之前是否可以取得我的 VPN 閘道 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="918e9-176">Can I get my VPN gateway IP address before I create it?</span></span>

<span data-ttu-id="918e9-177">否。</span><span class="sxs-lookup"><span data-stu-id="918e9-177">No.</span></span> <span data-ttu-id="918e9-178">您有 toocreate 您第一次 tooget hello 閘道的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="918e9-178">You have toocreate your gateway first tooget hello IP address.</span></span> <span data-ttu-id="918e9-179">如果您刪除然後重新建立 VPN 閘道，就會變更 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="918e9-179">hello IP address changes if you delete and recreate your VPN gateway.</span></span>

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a><span data-ttu-id="918e9-180">是否可以要求我的 VPN 閘道的靜態公用 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="918e9-180">Can I request a Static Public IP address for my VPN gateway?</span></span>

<span data-ttu-id="918e9-181">否。</span><span class="sxs-lookup"><span data-stu-id="918e9-181">No.</span></span> <span data-ttu-id="918e9-182">僅支援動態 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="918e9-182">Only Dynamic IP address assignment is supported.</span></span> <span data-ttu-id="918e9-183">不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-183">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="918e9-184">hello VPN 閘道 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="918e9-184">hello only time hello VPN gateway IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="918e9-185">hello VPN 閘道的公用 IP 位址不會在調整大小、 重設，或其他內部維護/升級您的 VPN 閘道的變更。</span><span class="sxs-lookup"><span data-stu-id="918e9-185">hello VPN gateway public IP address doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span> 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a><span data-ttu-id="918e9-186">我的 VPN 通道如何獲得驗證？</span><span class="sxs-lookup"><span data-stu-id="918e9-186">How does my VPN tunnel get authenticated?</span></span>

<span data-ttu-id="918e9-187">Azure VPN 使用 PSK (預先共用金鑰) 驗證。</span><span class="sxs-lookup"><span data-stu-id="918e9-187">Azure VPN uses PSK (Pre-Shared Key) authentication.</span></span> <span data-ttu-id="918e9-188">當我們建立 hello VPN 通道，我們就會產生預先共用的金鑰 (PSK)。</span><span class="sxs-lookup"><span data-stu-id="918e9-188">We generate a pre-shared key (PSK) when we create hello VPN tunnel.</span></span> <span data-ttu-id="918e9-189">您可以變更 hello 自動產生 PSK tooyour 自己與 hello 設定預先共用金鑰 PowerShell cmdlet 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="918e9-189">You can change hello auto-generated PSK tooyour own with hello Set Pre-Shared Key PowerShell cmdlet or REST API.</span></span>

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a><span data-ttu-id="918e9-190">我可以使用 hello 設定預先共用金鑰 API tooconfigure 我以原則為基礎 （靜態路由） 閘道 VPN 嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-190">Can I use hello Set Pre-Shared Key API tooconfigure my policy-based (static routing) gateway VPN?</span></span>

<span data-ttu-id="918e9-191">是，hello 設定預先共用金鑰 API 和 PowerShell 指令程式可以使用的 tooconfigure Azure 的以原則為基礎 （靜態） Vpn 和路由為基礎的 （動態） 路由 Vpn。</span><span class="sxs-lookup"><span data-stu-id="918e9-191">Yes, hello Set Pre-Shared Key API and PowerShell cmdlet can be used tooconfigure both Azure policy-based (static) VPNs and route-based (dynamic) routing VPNs.</span></span>

### <a name="can-i-use-other-authentication-options"></a><span data-ttu-id="918e9-192">是否可以使用其他驗證選項？</span><span class="sxs-lookup"><span data-stu-id="918e9-192">Can I use other authentication options?</span></span>

<span data-ttu-id="918e9-193">我們很有限的 toousing 的預先共用的金鑰 (PSK) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="918e9-193">We are limited toousing pre-shared keys (PSK) for authentication.</span></span>

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a><span data-ttu-id="918e9-194">如何指定的流量通過 hello VPN 閘道？</span><span class="sxs-lookup"><span data-stu-id="918e9-194">How do I specify which traffic goes through hello VPN gateway?</span></span>

#### <a name="resource-manager-deployment-model"></a><span data-ttu-id="918e9-195">資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="918e9-195">Resource Manager deployment model</span></span>

* <span data-ttu-id="918e9-196">PowerShell: hello 本機網路閘道，使用"AddressPrefix"toospecify 流量。</span><span class="sxs-lookup"><span data-stu-id="918e9-196">PowerShell: use "AddressPrefix" toospecify traffic for hello local network gateway.</span></span>
* <span data-ttu-id="918e9-197">Azure 入口網站： 瀏覽 toohello 區域網路閘道 > 組態 > 位址空間。</span><span class="sxs-lookup"><span data-stu-id="918e9-197">Azure portal: navigate toohello Local network gateway > Configuration > Address space.</span></span>

#### <a name="classic-deployment-model"></a><span data-ttu-id="918e9-198">傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="918e9-198">Classic deployment model</span></span>

* <span data-ttu-id="918e9-199">Azure 入口網站： 瀏覽 toohello 傳統虛擬網路 > VPN 連線 > 站台對站 VPN 連線 > 本機站台名稱 > 本機站台 > 用戶端的位址空間。</span><span class="sxs-lookup"><span data-stu-id="918e9-199">Azure portal: navigate toohello classic virtual network > VPN connections > Site-to-site VPN connections > Local site name > Local site > Client address space.</span></span> 
* <span data-ttu-id="918e9-200">傳統入口網站： 新增您想要透過 hello 閘道傳送您在本機網路 下 hello 網路 頁面上的虛擬網路的每個範圍。</span><span class="sxs-lookup"><span data-stu-id="918e9-200">Classic portal: add each range that you want sent through hello gateway for your virtual network on hello Networks page under Local Networks.</span></span> 

### <a name="can-i-configure-forced-tunneling"></a><span data-ttu-id="918e9-201">是否可以設定強制通道？</span><span class="sxs-lookup"><span data-stu-id="918e9-201">Can I configure Forced Tunneling?</span></span>

<span data-ttu-id="918e9-202">是。</span><span class="sxs-lookup"><span data-stu-id="918e9-202">Yes.</span></span> <span data-ttu-id="918e9-203">請參閱 [設定強制通道](vpn-gateway-about-forced-tunneling.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-203">See [Configure forced tunneling](vpn-gateway-about-forced-tunneling.md).</span></span>

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a><span data-ttu-id="918e9-204">我可以將我自己在 Azure 中的 VPN 伺服器設定並使用此 tooconnect toomy 在內部部署網路嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-204">Can I set up my own VPN server in Azure and use it tooconnect toomy on-premises network?</span></span>

<span data-ttu-id="918e9-205">是，您可以部署您自己的 VPN 閘道或 Azure 從 hello Azure Marketplace 或建立您自己的 VPN 路由器中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="918e9-205">Yes, you can deploy your own VPN gateways or servers in Azure either from hello Azure Marketplace or creating your own VPN routers.</span></span> <span data-ttu-id="918e9-206">您需要 tooconfigure 使用者定義的路由虛擬網路中 tooensure 流量路由傳送正確的內部網路與您的虛擬網路子網路之間。</span><span class="sxs-lookup"><span data-stu-id="918e9-206">You need tooconfigure user-defined routes in your virtual network tooensure traffic is routed properly between your on-premises networks and your virtual network subnets.</span></span>

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a><span data-ttu-id="918e9-207">為什麼 VPN 閘道上的某些連接埠已開啟？</span><span class="sxs-lookup"><span data-stu-id="918e9-207">Why are certain ports opened on my VPN gateway?</span></span>

<span data-ttu-id="918e9-208">Azure 基礎結構通訊需要這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="918e9-208">They are required for Azure infrastructure communication.</span></span> <span data-ttu-id="918e9-209">它們受到 Azure 憑證的保護 (鎖定)。</span><span class="sxs-lookup"><span data-stu-id="918e9-209">They are protected (locked down) by Azure certificates.</span></span> <span data-ttu-id="918e9-210">沒有適當的憑證，外部實體，包括 hello 客戶的這些閘道，將不會無法 toocause 任何這些端點生效。</span><span class="sxs-lookup"><span data-stu-id="918e9-210">Without proper certificates, external entities, including hello customers of those gateways, will not be able toocause any effect on those endpoints.</span></span>

<span data-ttu-id="918e9-211">VPN 閘道本質上是多重主目錄裝置使用一個點選到 hello 客戶的私人網路，以及一個 NIC 面對 hello 公用網路的 NIC。</span><span class="sxs-lookup"><span data-stu-id="918e9-211">A VPN gateway is fundamentally a multi-homed device with one NIC tapping into hello customer private network, and one NIC facing hello public network.</span></span> <span data-ttu-id="918e9-212">Azure 基礎結構的實體無法挖掘客戶的私人網路，用於相容性因素，因此它們需要 tooutilize 公用端點的通訊基礎結構。</span><span class="sxs-lookup"><span data-stu-id="918e9-212">Azure infrastructure entities cannot tap into customer private networks for compliance reasons, so they need tooutilize public endpoints for infrastructure communication.</span></span> <span data-ttu-id="918e9-213">Azure 的安全性稽核會定期掃描 hello 公用端點。</span><span class="sxs-lookup"><span data-stu-id="918e9-213">hello public endpoints are periodically scanned by Azure security audit.</span></span>

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a><span data-ttu-id="918e9-214">閘道類型、需求和輸送量的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="918e9-214">More information about gateway types, requirements, and throughput</span></span>

<span data-ttu-id="918e9-215">如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-215">For more information, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>

## <span data-ttu-id="918e9-216"><a name="s2s"></a>站對站連線和 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="918e9-216"><a name="s2s"></a>Site-to-Site connections and VPN devices</span></span>

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a><span data-ttu-id="918e9-217">選取 VPN 裝置時應該考慮什麼？</span><span class="sxs-lookup"><span data-stu-id="918e9-217">What should I consider when selecting a VPN device?</span></span>

<span data-ttu-id="918e9-218">我們已與裝置廠商合作驗證一組標準網站間 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="918e9-218">We have validated a set of standard Site-to-Site VPN devices in partnership with device vendors.</span></span> <span data-ttu-id="918e9-219">已知的相容 VPN 裝置、 其對應的組態設定指示或範例和裝置規格的清單位於 hello[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="918e9-219">A list of known compatible VPN devices, their corresponding configuration instructions or samples, and device specs can be found in hello [About VPN devices](vpn-gateway-about-vpn-devices.md) article.</span></span> <span data-ttu-id="918e9-220">Hello 列為已知相容的裝置系列中的所有裝置應該都使用虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-220">All devices in hello device families listed as known compatible should work with Virtual Network.</span></span> <span data-ttu-id="918e9-221">toohelp 設定 VPN 裝置，請參閱 toohello 裝置組態範例或對應 tooappropriate 裝置家族的連結。</span><span class="sxs-lookup"><span data-stu-id="918e9-221">toohelp configure your VPN device, refer toohello device configuration sample or link that corresponds tooappropriate device family.</span></span>

### <a name="where-can-i-find-vpn-device-configuration-settings"></a><span data-ttu-id="918e9-222">哪裡可以找到 VPN 裝置組態設定？</span><span class="sxs-lookup"><span data-stu-id="918e9-222">Where can I find VPN device configuration settings?</span></span>

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a><span data-ttu-id="918e9-223">如何編輯 VPN 裝置組態範例？</span><span class="sxs-lookup"><span data-stu-id="918e9-223">How do I edit VPN device configuration samples?</span></span>

<span data-ttu-id="918e9-224">如需編輯裝置組態範例的相關資訊，請參閱[編輯範例](vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="918e9-224">For information about editing device configuration samples, see [Editing samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a><span data-ttu-id="918e9-225">哪裡可以找到 IPsec 和 IKE 參數？</span><span class="sxs-lookup"><span data-stu-id="918e9-225">Where do I find IPsec and IKE parameters?</span></span>

<span data-ttu-id="918e9-226">如需 IPsec/IKE 參數，請參閱[參數](vpn-gateway-about-vpn-devices.md#ipsec)。</span><span class="sxs-lookup"><span data-stu-id="918e9-226">For IPsec/IKE parameters, see [Parameters](vpn-gateway-about-vpn-devices.md#ipsec).</span></span>

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a><span data-ttu-id="918e9-227">為什麼我的原則型 VPN 通道會在流量閒置時終止？</span><span class="sxs-lookup"><span data-stu-id="918e9-227">Why does my policy-based VPN tunnel go down when traffic is idle?</span></span>

<span data-ttu-id="918e9-228">這是原則型 (也稱為靜態路由) VPN 閘道的預期行為。</span><span class="sxs-lookup"><span data-stu-id="918e9-228">This is expected behavior for policy-based (also known as static routing) VPN gateways.</span></span> <span data-ttu-id="918e9-229">當透過 hello 通道 hello 流量閒置超過 5 分鐘，hello 通道將會終止。</span><span class="sxs-lookup"><span data-stu-id="918e9-229">When hello traffic over hello tunnel is idle for more than 5 minutes, hello tunnel will be torn down.</span></span> <span data-ttu-id="918e9-230">當流量會開始流向任一方向時，將會立即重新建立 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="918e9-230">When traffic starts flowing in either direction, hello tunnel will be reestablished immediately.</span></span>

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a><span data-ttu-id="918e9-231">可以使用軟體 Vpn tooconnect tooAzure 嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-231">Can I use software VPNs tooconnect tooAzure?</span></span>

<span data-ttu-id="918e9-232">我們支援 Windows Server 2012 路由及遠端存取 (RRAS) 伺服器進行網站間跨單位設定。</span><span class="sxs-lookup"><span data-stu-id="918e9-232">We support Windows Server 2012 Routing and Remote Access (RRAS) servers for Site-to-Site cross-premises configuration.</span></span>

<span data-ttu-id="918e9-233">其他軟體 VPN 解決方案應該使用我們的閘道，只要它們符合 tooindustry 標準 IPsec 實作。</span><span class="sxs-lookup"><span data-stu-id="918e9-233">Other software VPN solutions should work with our gateway as long as they conform tooindustry standard IPsec implementations.</span></span> <span data-ttu-id="918e9-234">如需設定和支援的指示，請連絡 hello hello 軟體廠商。</span><span class="sxs-lookup"><span data-stu-id="918e9-234">Contact hello vendor of hello software for configuration and support instructions.</span></span>

## <span data-ttu-id="918e9-235"><a name="P2S"></a>點對站連線</span><span class="sxs-lookup"><span data-stu-id="918e9-235"><a name="P2S"></a>Point-to-Site connections</span></span>

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <span data-ttu-id="918e9-236"><a name="V2VMulti"></a>VNet 對 VNet 和多站台連線</span><span class="sxs-lookup"><span data-stu-id="918e9-236"><a name="V2VMulti"></a>VNet-to-VNet and Multi-Site connections</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a><span data-ttu-id="918e9-237">可以使用我的內部部署站台或 tooanother 虛擬網路之間的 Azure VPN 閘道 tootransit 流量嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-237">Can I use Azure VPN gateway tootransit traffic between my on-premises sites or tooanother virtual network?</span></span>

<span data-ttu-id="918e9-238">**Resource Manager 部署模型**</span><span class="sxs-lookup"><span data-stu-id="918e9-238">**Resource Manager deployment model**</span></span><br>
<span data-ttu-id="918e9-239">是。</span><span class="sxs-lookup"><span data-stu-id="918e9-239">Yes.</span></span> <span data-ttu-id="918e9-240">請參閱 hello [BGP](#bgp)節的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="918e9-240">See hello [BGP](#bgp) section for more information.</span></span>

<span data-ttu-id="918e9-241">**傳統部署模型**</span><span class="sxs-lookup"><span data-stu-id="918e9-241">**Classic deployment model**</span></span><br>
<span data-ttu-id="918e9-242">透過 Azure VPN 閘道傳輸流量可以使用 hello 傳統部署模型，但依賴 hello 網路組態檔中靜態定義的位址空間。</span><span class="sxs-lookup"><span data-stu-id="918e9-242">Transit traffic via Azure VPN gateway is possible using hello classic deployment model, but relies on statically defined address spaces in hello network configuration file.</span></span> <span data-ttu-id="918e9-243">BGP 尚未支援與 Azure 虛擬網路和 VPN 閘道使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="918e9-243">BGP is not yet supported with Azure Virtual Networks and VPN gateways using hello classic deployment model.</span></span> <span data-ttu-id="918e9-244">若沒有 BGP，手動定義傳輸位址空間很容易出錯，因此並不建議。</span><span class="sxs-lookup"><span data-stu-id="918e9-244">Without BGP, manually defining transit address spaces is very error prone, and not recommended.</span></span>

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a><span data-ttu-id="918e9-245">Azure 不會產生相同的 IPsec/IKE 預先共用的 hello 鍵 hello 我所有的 VPN 連線的相同虛擬網路嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-245">Does Azure generate hello same IPsec/IKE pre-shared key for all my VPN connections for hello same virtual network?</span></span>

<span data-ttu-id="918e9-246">否，Azure 預設會針對不同 VPN 連線產生不同的預先共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="918e9-246">No, Azure by default generates different pre-shared keys for different VPN connections.</span></span> <span data-ttu-id="918e9-247">不過，您可以使用 hello 設定 VPN 閘道金鑰 REST API 或 PowerShell cmdlet tooset hello 索引鍵值您偏好。</span><span class="sxs-lookup"><span data-stu-id="918e9-247">However, you can use hello Set VPN Gateway Key REST API or PowerShell cmdlet tooset hello key value you prefer.</span></span> <span data-ttu-id="918e9-248">hello 索引鍵必須是長度的英數字元字串是長度的介於 1 too128 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="918e9-248">hello key MUST be alphanumerical string of length between 1 too128 characters.</span></span>

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a><span data-ttu-id="918e9-249">比起單一虛擬網路，是否可以使用更多的網站間 VPN，取得更多的頻寬？</span><span class="sxs-lookup"><span data-stu-id="918e9-249">Do I get more bandwidth with more Site-to-Site VPNs than for a single virtual network?</span></span>

<span data-ttu-id="918e9-250">否，所有 VPN 通道，包括點對站 Vpn 都共用 hello 相同 Azure VPN 閘道與 hello 可用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="918e9-250">No, all VPN tunnels, including Point-to-Site VPNs, share hello same Azure VPN gateway and hello available bandwidth.</span></span>

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a><span data-ttu-id="918e9-251">是否可以使用多網站 VPN，在我的虛擬網路與內部部署網站之間設定多個通道？</span><span class="sxs-lookup"><span data-stu-id="918e9-251">Can I configure multiple tunnels between my virtual network and my on-premises site using multi-site VPN?</span></span>

<span data-ttu-id="918e9-252">是的但是您必須將 BGP 設定這兩個通道 toohello 上相同的位置。</span><span class="sxs-lookup"><span data-stu-id="918e9-252">Yes, but you must configure BGP on both tunnels toohello same location.</span></span>

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a><span data-ttu-id="918e9-253">是否可以使用點對站台 VPN 搭配具有多個 VPN 通道的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="918e9-253">Can I use Point-to-Site VPNs with my virtual network with multiple VPN tunnels?</span></span>

<span data-ttu-id="918e9-254">是，點對站 (P2S) Vpn 可以搭配 hello 連接 toomultiple 在內部部署網站和其他虛擬網路的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-254">Yes, Point-to-Site (P2S) VPNs can be used with hello VPN gateways connecting toomultiple on-premises sites and other virtual networks.</span></span>

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a><span data-ttu-id="918e9-255">可以連接的虛擬網路與 IPsec Vpn toomy ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="918e9-255">Can I connect a virtual network with IPsec VPNs toomy ExpressRoute circuit?</span></span>

<span data-ttu-id="918e9-256">是，支援此做法。</span><span class="sxs-lookup"><span data-stu-id="918e9-256">Yes, this is supported.</span></span> <span data-ttu-id="918e9-257">如需詳細資訊，請參閱 [設定並存的 ExpressRoute 和網站間 VPN 連線](../expressroute/expressroute-howto-coexist-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-257">For more information, see [Configure ExpressRoute and Site-to-Site VPN connections that coexist](../expressroute/expressroute-howto-coexist-classic.md).</span></span>

## <span data-ttu-id="918e9-258"><a name="ipsecike"></a>IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="918e9-258"><a name="ipsecike"></a>IPsec/IKE policy</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <span data-ttu-id="918e9-259"><a name="bgp"></a>BGP</span><span class="sxs-lookup"><span data-stu-id="918e9-259"><a name="bgp"></a>BGP</span></span>

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <span data-ttu-id="918e9-260"><a name="vms"></a>跨單位連線與 VM</span><span class="sxs-lookup"><span data-stu-id="918e9-260"><a name="vms"></a>Cross-premises connectivity and VMs</span></span>

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a><span data-ttu-id="918e9-261">如果我的虛擬機器位於虛擬網路，而且有跨單位連線，應該如何我連接 toohello VM？</span><span class="sxs-lookup"><span data-stu-id="918e9-261">If my virtual machine is in a virtual network and I have a cross-premises connection, how should I connect toohello VM?</span></span>

<span data-ttu-id="918e9-262">您有幾個選項。</span><span class="sxs-lookup"><span data-stu-id="918e9-262">You have a few options.</span></span> <span data-ttu-id="918e9-263">如果您有 vm 啟用 RDP，您可以使用私人 IP 位址 hello 連接 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="918e9-263">If you have RDP enabled for your VM, you can connect tooyour virtual machine by using hello private IP address.</span></span> <span data-ttu-id="918e9-264">在此情況下，您可以指定 hello 私人 IP 位址和您想 tooconnect 太 (通常為 3389) 的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="918e9-264">In that case, you would specify hello private IP address and hello port that you want tooconnect too(typically 3389).</span></span> <span data-ttu-id="918e9-265">您將需要 tooconfigure hello 連接埠 hello 流量的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="918e9-265">You'll need tooconfigure hello port on your virtual machine for hello traffic.</span></span>

<span data-ttu-id="918e9-266">您也可以從另一個已位於 hello 相同的虛擬機器的私人 IP 位址連線 tooyour 虛擬機器虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="918e9-266">You can also connect tooyour virtual machine by private IP address from another virtual machine that's located on hello same virtual network.</span></span> <span data-ttu-id="918e9-267">您無法使用 hello 私人 IP 位址，如果您從一個位置連接虛擬網路外部的 RDP tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="918e9-267">You can't RDP tooyour virtual machine by using hello private IP address if you are connecting from a location outside of your virtual network.</span></span> <span data-ttu-id="918e9-268">例如，如果您已設定點對站虛擬網路，而且您不要從您的電腦建立連接，您無法連線 toohello 虛擬機器的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="918e9-268">For example, if you have a Point-to-Site virtual network configured and you don't establish a connection from your computer, you can't connect toohello virtual machine by private IP address.</span></span>

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a><span data-ttu-id="918e9-269">如果我的虛擬機器位於具有跨單位連線的虛擬網路，並從我的 VM 的所有 hello 流量都經過該連線？</span><span class="sxs-lookup"><span data-stu-id="918e9-269">If my virtual machine is in a virtual network with cross-premises connectivity, does all hello traffic from my VM go through that connection?</span></span>

<span data-ttu-id="918e9-270">否。</span><span class="sxs-lookup"><span data-stu-id="918e9-270">No.</span></span> <span data-ttu-id="918e9-271">目的地 hello 流量包含在 hello 虛擬網路本機網路 IP 位址範圍，您所指定的 IP 會通過 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-271">Only hello traffic that has a destination IP that is contained in hello virtual network Local Network IP address ranges that you specified will go through hello virtual network gateway.</span></span> <span data-ttu-id="918e9-272">流量具有 hello 虛擬網路內的 IP 保持在 hello 虛擬網路內的目的地。</span><span class="sxs-lookup"><span data-stu-id="918e9-272">Traffic has a destination IP located within hello virtual network stays within hello virtual network.</span></span> <span data-ttu-id="918e9-273">其他流量是透過 hello 負載平衡器 toohello 公用網路中，傳送，或使用強制通道時，如果傳送 hello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="918e9-273">Other traffic is sent through hello load balancer toohello public networks, or if forced tunneling is used, sent through hello Azure VPN gateway.</span></span>

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a><span data-ttu-id="918e9-274">如何疑難排解 RDP 連接 tooa VM</span><span class="sxs-lookup"><span data-stu-id="918e9-274">How do I troubleshoot an RDP connection tooa VM</span></span>

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <span data-ttu-id="918e9-275"><a name="faq"></a>虛擬網路常見問題集</span><span class="sxs-lookup"><span data-stu-id="918e9-275"><a name="faq"></a>Virtual Network FAQ</span></span>

<span data-ttu-id="918e9-276">您可以檢視其他虛擬網路資訊在 hello[虛擬網路常見問題集](../virtual-network/virtual-networks-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-276">You view additional virtual network information in hello [Virtual Network FAQ](../virtual-network/virtual-networks-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="918e9-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="918e9-277">Next steps</span></span>

* <span data-ttu-id="918e9-278">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-278">For more information about VPN Gateway, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="918e9-279">如需 VPN 閘道組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="918e9-279">For more information about VPN Gateway configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>
