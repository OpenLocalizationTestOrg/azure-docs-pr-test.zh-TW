---
title: "Azure VPN 閘道常見問題集 | Microsoft Docs"
description: "VPN 閘道常見問題集。 Microsoft Azure 虛擬網路跨單位連線、混合式組態連線和 VPN 閘道的常見問題集。"
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
ms.openlocfilehash: 9f7eb8e63f30d0f3450ad913620e59cd461b75bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="vpn-gateway-faq"></a><span data-ttu-id="774f5-104">VPN 閘道常見問題集</span><span class="sxs-lookup"><span data-stu-id="774f5-104">VPN Gateway FAQ</span></span>

## <span data-ttu-id="774f5-105"><a name="connecting"></a>連線到虛擬網路</span><span class="sxs-lookup"><span data-stu-id="774f5-105"><a name="connecting"></a>Connecting to virtual networks</span></span>

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a><span data-ttu-id="774f5-106">是否可以連接不同 Azure 區域中的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-106">Can I connect virtual networks in different Azure regions?</span></span>

<span data-ttu-id="774f5-107">是。</span><span class="sxs-lookup"><span data-stu-id="774f5-107">Yes.</span></span> <span data-ttu-id="774f5-108">事實上，沒有區域限制。</span><span class="sxs-lookup"><span data-stu-id="774f5-108">In fact, there is no region constraint.</span></span> <span data-ttu-id="774f5-109">一個虛擬網路可以連接到相同區域或不同 Azure 區域中的另一個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="774f5-109">One virtual network can connect to another virtual network in the same region, or in a different Azure region.</span></span> 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a><span data-ttu-id="774f5-110">是否可以使用不同訂用帳戶連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-110">Can I connect virtual networks in different subscriptions?</span></span>

<span data-ttu-id="774f5-111">是。</span><span class="sxs-lookup"><span data-stu-id="774f5-111">Yes.</span></span>

### <a name="can-i-connect-to-multiple-sites-from-a-single-virtual-network"></a><span data-ttu-id="774f5-112">是否可以從單一虛擬網路連接到多個網站？</span><span class="sxs-lookup"><span data-stu-id="774f5-112">Can I connect to multiple sites from a single virtual network?</span></span>

<span data-ttu-id="774f5-113">您可以使用 Windows PowerShell 和 Azure REST API 連接到多個網站。</span><span class="sxs-lookup"><span data-stu-id="774f5-113">You can connect to multiple sites by using Windows PowerShell and the Azure REST APIs.</span></span> <span data-ttu-id="774f5-114">請參閱＜ [多網站和 VNet 對 VNet 連線能力](#V2VMulti) ＞常見問題集一節。</span><span class="sxs-lookup"><span data-stu-id="774f5-114">See the [Multi-Site and VNet-to-VNet Connectivity](#V2VMulti) FAQ section.</span></span>

### <a name="what-are-my-cross-premises-connection-options"></a><span data-ttu-id="774f5-115">有哪些跨單位連線選項？</span><span class="sxs-lookup"><span data-stu-id="774f5-115">What are my cross-premises connection options?</span></span>

<span data-ttu-id="774f5-116">支援下列跨單位連線：</span><span class="sxs-lookup"><span data-stu-id="774f5-116">The following cross-premises connections are supported:</span></span>

* <span data-ttu-id="774f5-117">站對站 – 透過 IPsec (IKE v1 和 IKE v2) 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="774f5-117">Site-to-Site – VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="774f5-118">此類型的連線需要 VPN 裝置或 RRAS。</span><span class="sxs-lookup"><span data-stu-id="774f5-118">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="774f5-119">如需詳細資訊，請參閱[站對站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-119">For more information, see [Site-to-Site](vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="774f5-120">點對站 – 透過 SSTP (安全通訊端通道通訊協定) 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="774f5-120">Point-to-Site – VPN connection over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="774f5-121">此連線不需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="774f5-121">This connection does not require a VPN device.</span></span> <span data-ttu-id="774f5-122">如需詳細資訊，請參閱[點對站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-122">For more information, see [Point-to-Site](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="774f5-123">VNet 對 VNet – 此類型的連線與站對站組態相同。</span><span class="sxs-lookup"><span data-stu-id="774f5-123">VNet-to-VNet – This type of connection is the same as a Site-to-Site configuration.</span></span> <span data-ttu-id="774f5-124">VNet 對 VNet 是透過 IPsec (IKE v1 和 IKE v2) 的 VPN 連線，</span><span class="sxs-lookup"><span data-stu-id="774f5-124">VNet to VNet is a VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="774f5-125">並不需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="774f5-125">It does not require a VPN device.</span></span> <span data-ttu-id="774f5-126">如需詳細資訊，請參閱 [VNet 對 VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-126">For more information, see [VNet-to-VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>
* <span data-ttu-id="774f5-127">多網站 - 這是站對站組態的變體，可讓您將多個內部部署網站連線至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="774f5-127">Multi-Site – This is a variation of a Site-to-Site configuration that allows you to connect multiple on-premises sites to a virtual network.</span></span> <span data-ttu-id="774f5-128">如需詳細資訊，請參閱[多網站](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-128">For more information, see [Multi-Site](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span></span>
* <span data-ttu-id="774f5-129">ExpressRoute - ExpressRoute 是從 WAN 到 Azure 的直接連線，而不是透過公用網際網路的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="774f5-129">ExpressRoute – ExpressRoute is a direct connection to Azure from your WAN, not a VPN connection over the public Internet.</span></span> <span data-ttu-id="774f5-130">如需詳細資訊，請參閱 [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)和 [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-130">For more information, see the [ExpressRoute Technical Overview](../expressroute/expressroute-introduction.md) and the [ExpressRoute FAQ](../expressroute/expressroute-faqs.md).</span></span>

<span data-ttu-id="774f5-131">如需 VPN 閘道連線的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-131">For more information about VPN gateway connections, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

### <a name="what-is-the-difference-between-a-site-to-site-connection-and-point-to-site"></a><span data-ttu-id="774f5-132">網站間連線和點對站台之間的差異為何？</span><span class="sxs-lookup"><span data-stu-id="774f5-132">What is the difference between a Site-to-Site connection and Point-to-Site?</span></span>

<span data-ttu-id="774f5-133">**站對站**(IPsec/IKE VPN 通道) 介於內部部署位置與 Azure 之間。</span><span class="sxs-lookup"><span data-stu-id="774f5-133">**Site-to-Site** (IPsec/IKE VPN tunnel) configurations are between your on-premises location and Azure.</span></span> <span data-ttu-id="774f5-134">這表示視您選擇如何設定路由和權限而定﹐您可以從任何位於您內部部署的電腦連線至虛擬網路內的任何虛擬機器或角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="774f5-134">This means that you can connect from any of your computers located on your premises to any virtual machine or role instance within your virtual network, depending on how you choose to configure routing and permissions.</span></span> <span data-ttu-id="774f5-135">對於永遠可用的跨單位連線而言，這是不錯的選項，而且非常適合於混合式組態。</span><span class="sxs-lookup"><span data-stu-id="774f5-135">It's a great option for an always-available cross-premises connection and is well-suited for hybrid configurations.</span></span> <span data-ttu-id="774f5-136">這種類型的連線依賴 IPsec VPN 應用裝置 (硬體裝置或軟體應用裝置)，而此應用裝置必須部署在網路的邊緣。</span><span class="sxs-lookup"><span data-stu-id="774f5-136">This type of connection relies on an IPsec VPN appliance (hardware device or soft appliance), which must be deployed at the edge of your network.</span></span> <span data-ttu-id="774f5-137">若要建立此類型的連線，您必須擁有不在 NAT 之後的對外公開 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="774f5-137">To create this type of connection, you must have an externally facing IPv4 address that is not behind a NAT.</span></span>

<span data-ttu-id="774f5-138">**點對站** (VPN over SSTP) 組態可讓您從任何地方的單一電腦連線到位於虛擬網路的任何項目。</span><span class="sxs-lookup"><span data-stu-id="774f5-138">**Point-to-Site** (VPN over SSTP) configurations let you connect from a single computer from anywhere to anything located in your virtual network.</span></span> <span data-ttu-id="774f5-139">並會使用 Windows 內建的 VPN 用戶端。</span><span class="sxs-lookup"><span data-stu-id="774f5-139">It uses the Windows in-box VPN client.</span></span> <span data-ttu-id="774f5-140">做為點對站台組態的一部分，您會安裝憑證和 VPN 用戶端組態封裝，其中包含可讓您的電腦連接到虛擬網路內任何虛擬機器或角色執行個體的設定。</span><span class="sxs-lookup"><span data-stu-id="774f5-140">As part of the Point-to-Site configuration, you install a certificate and a VPN client configuration package, which contains the settings that allow your computer to connect to any virtual machine or role instance within the virtual network.</span></span> <span data-ttu-id="774f5-141">當您想要連接到不在內部部署的虛擬網路時，這樣做很有用。</span><span class="sxs-lookup"><span data-stu-id="774f5-141">It's great when you want to connect to a virtual network, but aren't located on-premises.</span></span> <span data-ttu-id="774f5-142">當您無權存取 VPN 硬體或對外公開的 IPv4 位址時也是不錯的選項，因為這兩者都是網站間連線的必要項目。</span><span class="sxs-lookup"><span data-stu-id="774f5-142">It's also a good option when you don't have access to VPN hardware or an externally facing IPv4 address, both of which are required for a Site-to-Site connection.</span></span>

<span data-ttu-id="774f5-143">您可以將虛擬網路設定為同時使用網站間和點對站台，只要您使用路由式 VPN 類型來為閘道建立網站間連線即可。</span><span class="sxs-lookup"><span data-stu-id="774f5-143">You can configure your virtual network to use both Site-to-Site and Point-to-Site concurrently, as long as you create your Site-to-Site connection using a route-based VPN type for your gateway.</span></span> <span data-ttu-id="774f5-144">路由式 VPN 類型在傳統部署模型中稱為「動態閘道」。</span><span class="sxs-lookup"><span data-stu-id="774f5-144">Route-based VPN types are called dynamic gateways in the classic deployment model.</span></span>

## <span data-ttu-id="774f5-145"><a name="gateways"></a>虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="774f5-145"><a name="gateways"></a>Virtual network gateways</span></span>

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a><span data-ttu-id="774f5-146">VPN 閘道是虛擬網路閘道嗎？</span><span class="sxs-lookup"><span data-stu-id="774f5-146">Is a VPN gateway a virtual network gateway?</span></span>

<span data-ttu-id="774f5-147">VPN 閘道是一種虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="774f5-147">A VPN gateway is a type of virtual network gateway.</span></span> <span data-ttu-id="774f5-148">VPN 閘道可透過公用連線在您的虛擬網路和內部部署位置之間傳送加密流量。</span><span class="sxs-lookup"><span data-stu-id="774f5-148">A VPN gateway sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="774f5-149">您也可以使用 VPN 閘道在虛擬網路之間傳送流量。</span><span class="sxs-lookup"><span data-stu-id="774f5-149">You can also use a VPN gateway to send traffic between virtual networks.</span></span> <span data-ttu-id="774f5-150">當您建立 VPN 閘道時，您可以使用 -GatewayType 值 'Vpn'。</span><span class="sxs-lookup"><span data-stu-id="774f5-150">When you create a VPN gateway, you use the -GatewayType value 'Vpn'.</span></span> <span data-ttu-id="774f5-151">如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-151">For more information, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>

### <a name="what-is-a-policy-based-static-routing-gateway"></a><span data-ttu-id="774f5-152">什麼是以原則為基礎的 (靜態路由) 閘道？</span><span class="sxs-lookup"><span data-stu-id="774f5-152">What is a policy-based (static-routing) gateway?</span></span>

<span data-ttu-id="774f5-153">以原則為基礎的閘道會實作原則式 VPN。</span><span class="sxs-lookup"><span data-stu-id="774f5-153">Policy-based gateways implement policy-based VPNs.</span></span> <span data-ttu-id="774f5-154">原則式 VPN 會根據內部部署網路與 Azure VNet 之間的位址首碼組合，透過 IPsec 通道加密和直接封包。</span><span class="sxs-lookup"><span data-stu-id="774f5-154">Policy-based VPNs encrypt and direct packets through IPsec tunnels based on the combinations of address prefixes between your on-premises network and the Azure VNet.</span></span> <span data-ttu-id="774f5-155">原則 (或流量選取器) 通常定義為 VPN 組態中的存取清單。</span><span class="sxs-lookup"><span data-stu-id="774f5-155">The policy (or Traffic Selector) is usually defined as an access list in the VPN configuration.</span></span>

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a><span data-ttu-id="774f5-156">什麼是以路由為基礎的 (動態路由) 閘道？</span><span class="sxs-lookup"><span data-stu-id="774f5-156">What is a route-based (dynamic-routing) gateway?</span></span>

<span data-ttu-id="774f5-157">路由式閘道實作路由式 VPN。</span><span class="sxs-lookup"><span data-stu-id="774f5-157">Route-based gateways implement the route-based VPNs.</span></span> <span data-ttu-id="774f5-158">路由式 VPN 會使用 IP 轉送或路由表中的「路由」，直接封包至其對應的通道介面。</span><span class="sxs-lookup"><span data-stu-id="774f5-158">Route-based VPNs use "routes" in the IP forwarding or routing table to direct packets into their corresponding tunnel interfaces.</span></span> <span data-ttu-id="774f5-159">然後，通道介面會加密或解密輸入和輸出通道的封包。</span><span class="sxs-lookup"><span data-stu-id="774f5-159">The tunnel interfaces then encrypt or decrypt the packets in and out of the tunnels.</span></span> <span data-ttu-id="774f5-160">路由式 VPN 的原則或流量選取器會設定為任意對任意 (或萬用字元)。</span><span class="sxs-lookup"><span data-stu-id="774f5-160">The policy or traffic selector for route-based VPNs are configured as any-to-any (or wild cards).</span></span>

### <a name="do-i-need-a-gatewaysubnet"></a><span data-ttu-id="774f5-161">是否需要 'GatewaySubnet'？</span><span class="sxs-lookup"><span data-stu-id="774f5-161">Do I need a 'GatewaySubnet'?</span></span>

<span data-ttu-id="774f5-162">是。</span><span class="sxs-lookup"><span data-stu-id="774f5-162">Yes.</span></span> <span data-ttu-id="774f5-163">閘道子網路包含虛擬網路閘道服務使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="774f5-163">The gateway subnet contains the IP addresses that the virtual network gateway services use.</span></span> <span data-ttu-id="774f5-164">若要設定虛擬網路閘道，您必須為 VNet 建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="774f5-164">You need to create a gateway subnet for your VNet in order to configure a virtual network gateway.</span></span> <span data-ttu-id="774f5-165">所有閘道子網路都必須命名為 'GatewaySubnet' 才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="774f5-165">All gateway subnets must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="774f5-166">請勿將閘道子網路命名為其他名稱。</span><span class="sxs-lookup"><span data-stu-id="774f5-166">Don't name your gateway subnet something else.</span></span> <span data-ttu-id="774f5-167">請勿對閘道子網路部署 VM 或任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="774f5-167">And don't deploy VMs or anything else to the gateway subnet.</span></span>

<span data-ttu-id="774f5-168">當您建立閘道子網路時，您可指定子網路包含的 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="774f5-168">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="774f5-169">閘道子網路中的 IP 位址會配置給閘道服務。</span><span class="sxs-lookup"><span data-stu-id="774f5-169">The IP addresses in the gateway subnet are allocated to the gateway service.</span></span> <span data-ttu-id="774f5-170">某些組態要求將較多 IP 位址配置給閘道服務 (相較於其他服務)。</span><span class="sxs-lookup"><span data-stu-id="774f5-170">Some configurations require more IP addresses to be allocated to the gateway services than do others.</span></span> <span data-ttu-id="774f5-171">您想要確定您的閘道子網路包含足夠的 IP 位址，以因應未來成長及可能的其他新連線組態。</span><span class="sxs-lookup"><span data-stu-id="774f5-171">You want to make sure your gateway subnet contains enough IP addresses to accommodate future growth and possible additional new connection configurations.</span></span> <span data-ttu-id="774f5-172">所以﹐您可以建立像 /29 這麼小的閘道子網路，但建議您建立 /27 或更大 (/27、/26、/25 等) 的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="774f5-172">So, while you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /27 or larger (/27, /26, /25 etc.).</span></span> <span data-ttu-id="774f5-173">查看您想要建立的組態需求﹐並確認您擁有的閘道子網路將符合這些需求。</span><span class="sxs-lookup"><span data-stu-id="774f5-173">Look at the requirements for the configuration that you want to create and verify that the gateway subnet you have will meet those requirements.</span></span>

### <a name="can-i-deploy-virtual-machines-or-role-instances-to-my-gateway-subnet"></a><span data-ttu-id="774f5-174">是否可以將虛擬機器或角色執行個體部署到閘道子網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-174">Can I deploy Virtual Machines or role instances to my gateway subnet?</span></span>

<span data-ttu-id="774f5-175">否。</span><span class="sxs-lookup"><span data-stu-id="774f5-175">No.</span></span>

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a><span data-ttu-id="774f5-176">在建立之前是否可以取得我的 VPN 閘道 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="774f5-176">Can I get my VPN gateway IP address before I create it?</span></span>

<span data-ttu-id="774f5-177">否。</span><span class="sxs-lookup"><span data-stu-id="774f5-177">No.</span></span> <span data-ttu-id="774f5-178">您必須先建立閘道才能取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="774f5-178">You have to create your gateway first to get the IP address.</span></span> <span data-ttu-id="774f5-179">如果您刪除並重新建立 VPN 閘道，IP 位址就會變更。</span><span class="sxs-lookup"><span data-stu-id="774f5-179">The IP address changes if you delete and recreate your VPN gateway.</span></span>

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a><span data-ttu-id="774f5-180">是否可以要求我的 VPN 閘道的靜態公用 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="774f5-180">Can I request a Static Public IP address for my VPN gateway?</span></span>

<span data-ttu-id="774f5-181">否。</span><span class="sxs-lookup"><span data-stu-id="774f5-181">No.</span></span> <span data-ttu-id="774f5-182">僅支援動態 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="774f5-182">Only Dynamic IP address assignment is supported.</span></span> <span data-ttu-id="774f5-183">不過，這不表示 IP 位址變更之後已被指派至您的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="774f5-183">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="774f5-184">VPN 閘道 IP 位址只會在刪除或重新建立閘道時變更。</span><span class="sxs-lookup"><span data-stu-id="774f5-184">The only time the VPN gateway IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="774f5-185">VPN 閘道公用 IP 位址不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="774f5-185">The VPN gateway public IP address doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span> 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a><span data-ttu-id="774f5-186">我的 VPN 通道如何獲得驗證？</span><span class="sxs-lookup"><span data-stu-id="774f5-186">How does my VPN tunnel get authenticated?</span></span>

<span data-ttu-id="774f5-187">Azure VPN 使用 PSK (預先共用金鑰) 驗證。</span><span class="sxs-lookup"><span data-stu-id="774f5-187">Azure VPN uses PSK (Pre-Shared Key) authentication.</span></span> <span data-ttu-id="774f5-188">當建立 VPN 通道時，就會產生預先共用金鑰 (PSK)。</span><span class="sxs-lookup"><span data-stu-id="774f5-188">We generate a pre-shared key (PSK) when we create the VPN tunnel.</span></span> <span data-ttu-id="774f5-189">您可以使用設定預先共用金鑰 PowerShell Cmdlet 或 REST API，將自動產生的 PSK 變更為您自己的。</span><span class="sxs-lookup"><span data-stu-id="774f5-189">You can change the auto-generated PSK to your own with the Set Pre-Shared Key PowerShell cmdlet or REST API.</span></span>

### <a name="can-i-use-the-set-pre-shared-key-api-to-configure-my-policy-based-static-routing-gateway-vpn"></a><span data-ttu-id="774f5-190">是否可以使用「設定預先共用金鑰 API」來設定我的原則式 (靜態路由) 閘道 VPN？</span><span class="sxs-lookup"><span data-stu-id="774f5-190">Can I use the Set Pre-Shared Key API to configure my policy-based (static routing) gateway VPN?</span></span>

<span data-ttu-id="774f5-191">是，設定預先共用金鑰 API 和 PowerShell Cmdlet 可用來同時設定 Azure 原則式 (靜態) VPN 和路由式 (動態) 路由 VPN。</span><span class="sxs-lookup"><span data-stu-id="774f5-191">Yes, the Set Pre-Shared Key API and PowerShell cmdlet can be used to configure both Azure policy-based (static) VPNs and route-based (dynamic) routing VPNs.</span></span>

### <a name="can-i-use-other-authentication-options"></a><span data-ttu-id="774f5-192">是否可以使用其他驗證選項？</span><span class="sxs-lookup"><span data-stu-id="774f5-192">Can I use other authentication options?</span></span>

<span data-ttu-id="774f5-193">我們受限於只能使用預先共用的金鑰 (PSK) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="774f5-193">We are limited to using pre-shared keys (PSK) for authentication.</span></span>

### <a name="how-do-i-specify-which-traffic-goes-through-the-vpn-gateway"></a><span data-ttu-id="774f5-194">如何指定通過 VPN 閘道的流量？</span><span class="sxs-lookup"><span data-stu-id="774f5-194">How do I specify which traffic goes through the VPN gateway?</span></span>

#### <a name="resource-manager-deployment-model"></a><span data-ttu-id="774f5-195">資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="774f5-195">Resource Manager deployment model</span></span>

* <span data-ttu-id="774f5-196">PowerShell：使用 "AddressPrefix" 以指定區域網路閘道的流量。</span><span class="sxs-lookup"><span data-stu-id="774f5-196">PowerShell: use "AddressPrefix" to specify traffic for the local network gateway.</span></span>
* <span data-ttu-id="774f5-197">Azure 入口網站：瀏覽至 [區域網路閘道] > [組態] > [位址空間]。</span><span class="sxs-lookup"><span data-stu-id="774f5-197">Azure portal: navigate to the Local network gateway > Configuration > Address space.</span></span>

#### <a name="classic-deployment-model"></a><span data-ttu-id="774f5-198">傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="774f5-198">Classic deployment model</span></span>

* <span data-ttu-id="774f5-199">Azure 入口網站︰瀏覽至傳統虛擬網路 > VPN 連線 > 站對站 VPN 連線 > 本機網站名稱 > 本機網站 > 用戶端位址空間。</span><span class="sxs-lookup"><span data-stu-id="774f5-199">Azure portal: navigate to the classic virtual network > VPN connections > Site-to-site VPN connections > Local site name > Local site > Client address space.</span></span> 
* <span data-ttu-id="774f5-200">傳統入口網站：在 [網路] 頁面的 [區域網路] 下，新增每一個您想要虛擬網路透過閘道傳送的範圍。</span><span class="sxs-lookup"><span data-stu-id="774f5-200">Classic portal: add each range that you want sent through the gateway for your virtual network on the Networks page under Local Networks.</span></span> 

### <a name="can-i-configure-forced-tunneling"></a><span data-ttu-id="774f5-201">是否可以設定強制通道？</span><span class="sxs-lookup"><span data-stu-id="774f5-201">Can I configure Forced Tunneling?</span></span>

<span data-ttu-id="774f5-202">是。</span><span class="sxs-lookup"><span data-stu-id="774f5-202">Yes.</span></span> <span data-ttu-id="774f5-203">請參閱 [設定強制通道](vpn-gateway-about-forced-tunneling.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-203">See [Configure forced tunneling](vpn-gateway-about-forced-tunneling.md).</span></span>

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-to-connect-to-my-on-premises-network"></a><span data-ttu-id="774f5-204">是否可以在 Azure 中設定自己的 VPN 伺服器，並用來連接到內部部署網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-204">Can I set up my own VPN server in Azure and use it to connect to my on-premises network?</span></span>

<span data-ttu-id="774f5-205">是，您可以從 Azure Marketplace 或建立自己的 VPN 路由器，在 Azure 中部署自己的 VPN 閘道或伺服器。</span><span class="sxs-lookup"><span data-stu-id="774f5-205">Yes, you can deploy your own VPN gateways or servers in Azure either from the Azure Marketplace or creating your own VPN routers.</span></span> <span data-ttu-id="774f5-206">您需要在虛擬網路中設定使用者定義的路由，以確保在您的內部部署網路與虛擬網路子網路之間適當地路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="774f5-206">You need to configure user-defined routes in your virtual network to ensure traffic is routed properly between your on-premises networks and your virtual network subnets.</span></span>

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a><span data-ttu-id="774f5-207">為什麼 VPN 閘道上的某些連接埠已開啟？</span><span class="sxs-lookup"><span data-stu-id="774f5-207">Why are certain ports opened on my VPN gateway?</span></span>

<span data-ttu-id="774f5-208">Azure 基礎結構通訊需要這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="774f5-208">They are required for Azure infrastructure communication.</span></span> <span data-ttu-id="774f5-209">它們受到 Azure 憑證的保護 (鎖定)。</span><span class="sxs-lookup"><span data-stu-id="774f5-209">They are protected (locked down) by Azure certificates.</span></span> <span data-ttu-id="774f5-210">若沒有適當的憑證，外部實體 (包括這些閘道的客戶) 將無法對這些端點造成任何影響。</span><span class="sxs-lookup"><span data-stu-id="774f5-210">Without proper certificates, external entities, including the customers of those gateways, will not be able to cause any effect on those endpoints.</span></span>

<span data-ttu-id="774f5-211">VPN 閘道基本上是一個多重主目錄的裝置，擁有一個使用客戶私人網路的 NIC，以及一個面向公用網路的 NIC。</span><span class="sxs-lookup"><span data-stu-id="774f5-211">A VPN gateway is fundamentally a multi-homed device with one NIC tapping into the customer private network, and one NIC facing the public network.</span></span> <span data-ttu-id="774f5-212">Azure 基礎結構實體因為相容性，無法使用客戶私人網路，因此他們需要利用公用端點進行基礎結構通訊。</span><span class="sxs-lookup"><span data-stu-id="774f5-212">Azure infrastructure entities cannot tap into customer private networks for compliance reasons, so they need to utilize public endpoints for infrastructure communication.</span></span> <span data-ttu-id="774f5-213">Azure 安全性稽核會定期掃描公用端點。</span><span class="sxs-lookup"><span data-stu-id="774f5-213">The public endpoints are periodically scanned by Azure security audit.</span></span>

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a><span data-ttu-id="774f5-214">閘道類型、需求和輸送量的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="774f5-214">More information about gateway types, requirements, and throughput</span></span>

<span data-ttu-id="774f5-215">如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-215">For more information, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>

## <span data-ttu-id="774f5-216"><a name="s2s"></a>站對站連線和 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="774f5-216"><a name="s2s"></a>Site-to-Site connections and VPN devices</span></span>

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a><span data-ttu-id="774f5-217">選取 VPN 裝置時應該考慮什麼？</span><span class="sxs-lookup"><span data-stu-id="774f5-217">What should I consider when selecting a VPN device?</span></span>

<span data-ttu-id="774f5-218">我們已與裝置廠商合作驗證一組標準網站間 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="774f5-218">We have validated a set of standard Site-to-Site VPN devices in partnership with device vendors.</span></span> <span data-ttu-id="774f5-219">在[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)一文中可找到已知的相容 VPN 裝置、其對應組態指示或範例和裝置規格的清單。</span><span class="sxs-lookup"><span data-stu-id="774f5-219">A list of known compatible VPN devices, their corresponding configuration instructions or samples, and device specs can be found in the [About VPN devices](vpn-gateway-about-vpn-devices.md) article.</span></span> <span data-ttu-id="774f5-220">裝置系列中列為已知相容裝置的所有裝置應該使用虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="774f5-220">All devices in the device families listed as known compatible should work with Virtual Network.</span></span> <span data-ttu-id="774f5-221">為了協助設定 VPN 裝置，請參閱裝置組態範例或對應到適當裝置系列的連結。</span><span class="sxs-lookup"><span data-stu-id="774f5-221">To help configure your VPN device, refer to the device configuration sample or link that corresponds to appropriate device family.</span></span>

### <a name="where-can-i-find-vpn-device-configuration-settings"></a><span data-ttu-id="774f5-222">哪裡可以找到 VPN 裝置組態設定？</span><span class="sxs-lookup"><span data-stu-id="774f5-222">Where can I find VPN device configuration settings?</span></span>

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a><span data-ttu-id="774f5-223">如何編輯 VPN 裝置組態範例？</span><span class="sxs-lookup"><span data-stu-id="774f5-223">How do I edit VPN device configuration samples?</span></span>

<span data-ttu-id="774f5-224">如需編輯裝置組態範例的相關資訊，請參閱[編輯範例](vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="774f5-224">For information about editing device configuration samples, see [Editing samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a><span data-ttu-id="774f5-225">哪裡可以找到 IPsec 和 IKE 參數？</span><span class="sxs-lookup"><span data-stu-id="774f5-225">Where do I find IPsec and IKE parameters?</span></span>

<span data-ttu-id="774f5-226">如需 IPsec/IKE 參數，請參閱[參數](vpn-gateway-about-vpn-devices.md#ipsec)。</span><span class="sxs-lookup"><span data-stu-id="774f5-226">For IPsec/IKE parameters, see [Parameters](vpn-gateway-about-vpn-devices.md#ipsec).</span></span>

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a><span data-ttu-id="774f5-227">為什麼我的原則型 VPN 通道會在流量閒置時終止？</span><span class="sxs-lookup"><span data-stu-id="774f5-227">Why does my policy-based VPN tunnel go down when traffic is idle?</span></span>

<span data-ttu-id="774f5-228">這是原則型 (也稱為靜態路由) VPN 閘道的預期行為。</span><span class="sxs-lookup"><span data-stu-id="774f5-228">This is expected behavior for policy-based (also known as static routing) VPN gateways.</span></span> <span data-ttu-id="774f5-229">當通道上的流量閒置超過 5 分鐘時，通道就會終止。</span><span class="sxs-lookup"><span data-stu-id="774f5-229">When the traffic over the tunnel is idle for more than 5 minutes, the tunnel will be torn down.</span></span> <span data-ttu-id="774f5-230">當流量開始流向任何一個方向時，便會立即重新建立通道。</span><span class="sxs-lookup"><span data-stu-id="774f5-230">When traffic starts flowing in either direction, the tunnel will be reestablished immediately.</span></span>

### <a name="can-i-use-software-vpns-to-connect-to-azure"></a><span data-ttu-id="774f5-231">可以使用軟體 VPN 連接到 Azure 嗎？</span><span class="sxs-lookup"><span data-stu-id="774f5-231">Can I use software VPNs to connect to Azure?</span></span>

<span data-ttu-id="774f5-232">我們支援 Windows Server 2012 路由及遠端存取 (RRAS) 伺服器進行網站間跨單位設定。</span><span class="sxs-lookup"><span data-stu-id="774f5-232">We support Windows Server 2012 Routing and Remote Access (RRAS) servers for Site-to-Site cross-premises configuration.</span></span>

<span data-ttu-id="774f5-233">其他軟體 VPN 解決方案只要符合業界標準 IPsec 實作，應該就能使用我們的閘道。</span><span class="sxs-lookup"><span data-stu-id="774f5-233">Other software VPN solutions should work with our gateway as long as they conform to industry standard IPsec implementations.</span></span> <span data-ttu-id="774f5-234">如需設定和支援指示，請連絡軟體供應商。</span><span class="sxs-lookup"><span data-stu-id="774f5-234">Contact the vendor of the software for configuration and support instructions.</span></span>

## <span data-ttu-id="774f5-235"><a name="P2S"></a>點對站連線</span><span class="sxs-lookup"><span data-stu-id="774f5-235"><a name="P2S"></a>Point-to-Site connections</span></span>

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <span data-ttu-id="774f5-236"><a name="V2VMulti"></a>VNet 對 VNet 和多站台連線</span><span class="sxs-lookup"><span data-stu-id="774f5-236"><a name="V2VMulti"></a>VNet-to-VNet and Multi-Site connections</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-to-transit-traffic-between-my-on-premises-sites-or-to-another-virtual-network"></a><span data-ttu-id="774f5-237">是否可以使用 Azure VPN 閘道，在我的內部部署網站之間傳輸流量，或將流量傳輸到另一個虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-237">Can I use Azure VPN gateway to transit traffic between my on-premises sites or to another virtual network?</span></span>

<span data-ttu-id="774f5-238">**Resource Manager 部署模型**</span><span class="sxs-lookup"><span data-stu-id="774f5-238">**Resource Manager deployment model**</span></span><br>
<span data-ttu-id="774f5-239">是。</span><span class="sxs-lookup"><span data-stu-id="774f5-239">Yes.</span></span> <span data-ttu-id="774f5-240">如需詳細資訊，請參閱 [BGP](#bgp) 一節。</span><span class="sxs-lookup"><span data-stu-id="774f5-240">See the [BGP](#bgp) section for more information.</span></span>

<span data-ttu-id="774f5-241">**傳統部署模型**</span><span class="sxs-lookup"><span data-stu-id="774f5-241">**Classic deployment model**</span></span><br>
<span data-ttu-id="774f5-242">使用傳統部署模型即可透過 Azure VPN 閘道傳輸流量，但其依賴網路組態檔中靜態定義的位址空間。</span><span class="sxs-lookup"><span data-stu-id="774f5-242">Transit traffic via Azure VPN gateway is possible using the classic deployment model, but relies on statically defined address spaces in the network configuration file.</span></span> <span data-ttu-id="774f5-243">使用傳統部署模型的 Azure 虛擬網路和 VPN 閘道尚未支援 BGP。</span><span class="sxs-lookup"><span data-stu-id="774f5-243">BGP is not yet supported with Azure Virtual Networks and VPN gateways using the classic deployment model.</span></span> <span data-ttu-id="774f5-244">若沒有 BGP，手動定義傳輸位址空間很容易出錯，因此並不建議。</span><span class="sxs-lookup"><span data-stu-id="774f5-244">Without BGP, manually defining transit address spaces is very error prone, and not recommended.</span></span>

### <a name="does-azure-generate-the-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-the-same-virtual-network"></a><span data-ttu-id="774f5-245">Azure 是否針對相同虛擬網路的所有我的 VPN 連線產生相同的 IPsec/IKE 預先共用金鑰？</span><span class="sxs-lookup"><span data-stu-id="774f5-245">Does Azure generate the same IPsec/IKE pre-shared key for all my VPN connections for the same virtual network?</span></span>

<span data-ttu-id="774f5-246">否，Azure 預設會針對不同 VPN 連線產生不同的預先共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="774f5-246">No, Azure by default generates different pre-shared keys for different VPN connections.</span></span> <span data-ttu-id="774f5-247">不過，您可以使用設定 VPN 閘道金鑰 REST API 或 PowerShell Cmdlet 來設定您偏好的金鑰值。</span><span class="sxs-lookup"><span data-stu-id="774f5-247">However, you can use the Set VPN Gateway Key REST API or PowerShell cmdlet to set the key value you prefer.</span></span> <span data-ttu-id="774f5-248">金鑰必須是長度介於 1 到 128 個字元的英數字串。</span><span class="sxs-lookup"><span data-stu-id="774f5-248">The key MUST be alphanumerical string of length between 1 to 128 characters.</span></span>

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a><span data-ttu-id="774f5-249">比起單一虛擬網路，是否可以使用更多的網站間 VPN，取得更多的頻寬？</span><span class="sxs-lookup"><span data-stu-id="774f5-249">Do I get more bandwidth with more Site-to-Site VPNs than for a single virtual network?</span></span>

<span data-ttu-id="774f5-250">否，所有 VPN 通道 (包括點對站 VPN) 都共用相同的 Azure VPN 閘道與可用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="774f5-250">No, all VPN tunnels, including Point-to-Site VPNs, share the same Azure VPN gateway and the available bandwidth.</span></span>

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a><span data-ttu-id="774f5-251">是否可以使用多網站 VPN，在我的虛擬網路與內部部署網站之間設定多個通道？</span><span class="sxs-lookup"><span data-stu-id="774f5-251">Can I configure multiple tunnels between my virtual network and my on-premises site using multi-site VPN?</span></span>

<span data-ttu-id="774f5-252">是，但您必須將這兩個通道上的 BGP 設定為相同的位置。</span><span class="sxs-lookup"><span data-stu-id="774f5-252">Yes, but you must configure BGP on both tunnels to the same location.</span></span>

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a><span data-ttu-id="774f5-253">是否可以使用點對站台 VPN 搭配具有多個 VPN 通道的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="774f5-253">Can I use Point-to-Site VPNs with my virtual network with multiple VPN tunnels?</span></span>

<span data-ttu-id="774f5-254">是，點對站台 (P2S) VPN 可以與連接到多個內部部署網站和其他虛擬網路的 VPN 閘道搭配使用。</span><span class="sxs-lookup"><span data-stu-id="774f5-254">Yes, Point-to-Site (P2S) VPNs can be used with the VPN gateways connecting to multiple on-premises sites and other virtual networks.</span></span>

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-to-my-expressroute-circuit"></a><span data-ttu-id="774f5-255">是否可以將使用 IPsec VPN 的虛擬網路連接到我的 ExpressRoute 線路？</span><span class="sxs-lookup"><span data-stu-id="774f5-255">Can I connect a virtual network with IPsec VPNs to my ExpressRoute circuit?</span></span>

<span data-ttu-id="774f5-256">是，支援此做法。</span><span class="sxs-lookup"><span data-stu-id="774f5-256">Yes, this is supported.</span></span> <span data-ttu-id="774f5-257">如需詳細資訊，請參閱 [設定並存的 ExpressRoute 和網站間 VPN 連線](../expressroute/expressroute-howto-coexist-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-257">For more information, see [Configure ExpressRoute and Site-to-Site VPN connections that coexist](../expressroute/expressroute-howto-coexist-classic.md).</span></span>

## <span data-ttu-id="774f5-258"><a name="ipsecike"></a>IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="774f5-258"><a name="ipsecike"></a>IPsec/IKE policy</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <span data-ttu-id="774f5-259"><a name="bgp"></a>BGP</span><span class="sxs-lookup"><span data-stu-id="774f5-259"><a name="bgp"></a>BGP</span></span>

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <span data-ttu-id="774f5-260"><a name="vms"></a>跨單位連線與 VM</span><span class="sxs-lookup"><span data-stu-id="774f5-260"><a name="vms"></a>Cross-premises connectivity and VMs</span></span>

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-to-the-vm"></a><span data-ttu-id="774f5-261">如果我的虛擬機器在虛擬網路中，而且我有跨單位連線，應該如何連接至 VM？</span><span class="sxs-lookup"><span data-stu-id="774f5-261">If my virtual machine is in a virtual network and I have a cross-premises connection, how should I connect to the VM?</span></span>

<span data-ttu-id="774f5-262">您有幾個選項。</span><span class="sxs-lookup"><span data-stu-id="774f5-262">You have a few options.</span></span> <span data-ttu-id="774f5-263">如果您的 VM 已啟用 RDP，您可以使用私人 IP 位址連線到您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="774f5-263">If you have RDP enabled for your VM, you can connect to your virtual machine by using the private IP address.</span></span> <span data-ttu-id="774f5-264">在此情況下，您會指定私人 IP 位址以及您想要連線的連接埠 (通常為 3389)。</span><span class="sxs-lookup"><span data-stu-id="774f5-264">In that case, you would specify the private IP address and the port that you want to connect to (typically 3389).</span></span> <span data-ttu-id="774f5-265">您將需要在虛擬機器上設定流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="774f5-265">You'll need to configure the port on your virtual machine for the traffic.</span></span>

<span data-ttu-id="774f5-266">您也可以從位於相同虛擬網路的另一部虛擬機器經由私人 IP 位址連線到您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="774f5-266">You can also connect to your virtual machine by private IP address from another virtual machine that's located on the same virtual network.</span></span> <span data-ttu-id="774f5-267">如果您是從虛擬網路外的位置連線，則無法使用私人 IP 位址透過 RDP 連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="774f5-267">You can't RDP to your virtual machine by using the private IP address if you are connecting from a location outside of your virtual network.</span></span> <span data-ttu-id="774f5-268">例如，如果您已設定點對站台虛擬網路，而且未從您的電腦建立連線，則無法經由私人 IP 位址連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="774f5-268">For example, if you have a Point-to-Site virtual network configured and you don't establish a connection from your computer, you can't connect to the virtual machine by private IP address.</span></span>

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-the-traffic-from-my-vm-go-through-that-connection"></a><span data-ttu-id="774f5-269">如果我的虛擬機器位於具有跨單位連線能力的虛擬網路，所有來自我的 VM 的流量是否都會通過該連線？</span><span class="sxs-lookup"><span data-stu-id="774f5-269">If my virtual machine is in a virtual network with cross-premises connectivity, does all the traffic from my VM go through that connection?</span></span>

<span data-ttu-id="774f5-270">否。</span><span class="sxs-lookup"><span data-stu-id="774f5-270">No.</span></span> <span data-ttu-id="774f5-271">只有目地的 IP 包含在您指定之虛擬網路區域網路 IP 位址範圍的流量，才會通過虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="774f5-271">Only the traffic that has a destination IP that is contained in the virtual network Local Network IP address ranges that you specified will go through the virtual network gateway.</span></span> <span data-ttu-id="774f5-272">目的地 IP 位於虛擬網路內的流量仍會留在虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="774f5-272">Traffic has a destination IP located within the virtual network stays within the virtual network.</span></span> <span data-ttu-id="774f5-273">其他流量是透過負載平衡器傳送至公用網路，或者如果使用強制通道，則透過 Azure VPN 閘道傳送。</span><span class="sxs-lookup"><span data-stu-id="774f5-273">Other traffic is sent through the load balancer to the public networks, or if forced tunneling is used, sent through the Azure VPN gateway.</span></span>

### <a name="how-do-i-troubleshoot-an-rdp-connection-to-a-vm"></a><span data-ttu-id="774f5-274">如何針對 VM 的 RDP 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="774f5-274">How do I troubleshoot an RDP connection to a VM</span></span>

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <span data-ttu-id="774f5-275"><a name="faq"></a>虛擬網路常見問題集</span><span class="sxs-lookup"><span data-stu-id="774f5-275"><a name="faq"></a>Virtual Network FAQ</span></span>

<span data-ttu-id="774f5-276">您可以在 [虛擬網路常見問題集](../virtual-network/virtual-networks-faq.md)中檢視其他虛擬網路資訊。</span><span class="sxs-lookup"><span data-stu-id="774f5-276">You view additional virtual network information in the [Virtual Network FAQ](../virtual-network/virtual-networks-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="774f5-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="774f5-277">Next steps</span></span>

* <span data-ttu-id="774f5-278">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-278">For more information about VPN Gateway, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="774f5-279">如需 VPN 閘道組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="774f5-279">For more information about VPN Gateway configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>
