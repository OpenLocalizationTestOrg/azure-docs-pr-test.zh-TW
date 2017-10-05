---
title: "使用 Azure VPN 閘道的高可用性組態概觀 | Microsoft Docs"
description: "本文提供使用 Azure VPN 閘道的高可用性組態選項概觀。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 3708a2f7c445a161f02416cf8427b1707e1db8f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a><span data-ttu-id="00616-103">高可用性跨單位和 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="00616-103">Highly Available Cross-Premises and VNet-to-VNet Connectivity</span></span>
<span data-ttu-id="00616-104">本文針對使用 Azure VPN 閘道的跨單位和 VNet 對 VNet 連線提供高可用性組態選項的概觀。</span><span class="sxs-lookup"><span data-stu-id="00616-104">This article provides an overview of Highly Available configuration options for your cross-premises and VNet-to-VNet connectivity using Azure VPN gateways.</span></span>

## <span data-ttu-id="00616-105"><a name = "activestandby"></a>關於 Azure VPN 閘道備援</span><span class="sxs-lookup"><span data-stu-id="00616-105"><a name = "activestandby"></a>About Azure VPN gateway redundancy</span></span>
<span data-ttu-id="00616-106">每個 Azure VPN 閘道都是由作用中-待命組態中的兩個執行個體組成。</span><span class="sxs-lookup"><span data-stu-id="00616-106">Every Azure VPN gateway consists of two instances in an active-standby configuration.</span></span> <span data-ttu-id="00616-107">對於作用中執行個體所發生的任何計劃性維護或非計劃性中斷，待命執行個體都會自動進行接管 (容錯移轉)，並繼續 S2S VPN 或 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="00616-107">For any planned maintenance or unplanned disruption that happens to the active instance, the standby instance would take over (failover) automatically, and resume the S2S VPN or VNet-to-VNet connections.</span></span> <span data-ttu-id="00616-108">切換會導致短暫中斷。</span><span class="sxs-lookup"><span data-stu-id="00616-108">The switch over will cause a brief interruption.</span></span> <span data-ttu-id="00616-109">對於計劃性維護，應在 10 到 15 秒內還原連線。</span><span class="sxs-lookup"><span data-stu-id="00616-109">For planned maintenance, the connectivity should be restored within 10 to 15 seconds.</span></span> <span data-ttu-id="00616-110">對於非計劃問題，連線復原會更久，大約 1 分鐘到 1 分半 (最糟的情況)。</span><span class="sxs-lookup"><span data-stu-id="00616-110">For unplanned issues, the connection recovery will be longer, about 1 minute to 1 and a half minutes in the worst case.</span></span> <span data-ttu-id="00616-111">對於閘道的 P2S VPN 用戶端連線，P2S 連接將會中斷連線，而使用者必須從用戶端電腦重新連線。</span><span class="sxs-lookup"><span data-stu-id="00616-111">For P2S VPN client connections to the gateway, the P2S connections will be disconnected and the users will need to reconnect from the client machines.</span></span>

![作用中-待命](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a><span data-ttu-id="00616-113">高可用性跨單位連線</span><span class="sxs-lookup"><span data-stu-id="00616-113">Highly Available Cross-Premises Connectivity</span></span>
<span data-ttu-id="00616-114">若要為跨單位連線提供更好的可用性，有幾個選項可用︰</span><span class="sxs-lookup"><span data-stu-id="00616-114">To provide better availability for your cross premises connections, there are a couple of options available:</span></span>

* <span data-ttu-id="00616-115">多個內部部署 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="00616-115">Multiple on-premises VPN devices</span></span>
* <span data-ttu-id="00616-116">主動-主動 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="00616-116">Active-active Azure VPN gateway</span></span>
* <span data-ttu-id="00616-117">兩者的組合</span><span class="sxs-lookup"><span data-stu-id="00616-117">Combination of both</span></span>

### <span data-ttu-id="00616-118"><a name = "activeactiveonprem"></a>多個內部部署 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="00616-118"><a name = "activeactiveonprem"></a>Multiple on-premises VPN devices</span></span>
<span data-ttu-id="00616-119">您可以使用內部部署網路中的多個 VPN 裝置連接到 Azure VPN 閘道，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="00616-119">You can use multiple VPN devices from your on-premises network to connect to your Azure VPN gateway, as shown in the following diagram:</span></span>

![多個內部部署 VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

<span data-ttu-id="00616-121">此組態會提供多個作用中通道 (從同一個 Azure VPN 閘道到相同位置的內部部署裝置)。</span><span class="sxs-lookup"><span data-stu-id="00616-121">This configuration provides multiple active tunnels from the same Azure VPN gateway to your on-premises devices in the same location.</span></span> <span data-ttu-id="00616-122">有一些需求和限制︰</span><span class="sxs-lookup"><span data-stu-id="00616-122">There are some requirements and constraints:</span></span>

1. <span data-ttu-id="00616-123">您需要建立從 VPN 裝置至 Azure 的多個 S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="00616-123">You need to create multiple S2S VPN connections from your VPN devices to Azure.</span></span> <span data-ttu-id="00616-124">當您從同一個內部部署網路的多個 VPN 裝置連接到 Azure 時，您需要為每個 VPN 裝置建立一個區域網路閘道，以及一個從 Azure VPN 閘道至區域網路閘道的連線。</span><span class="sxs-lookup"><span data-stu-id="00616-124">When you connect multiple VPN devices from the same on-premises network to Azure, you need to create one local network gateway for each VPN device, and one connection from your Azure VPN gateway to the local network gateway.</span></span>
2. <span data-ttu-id="00616-125">對應到 VPN 裝置的區域網路閘道在 "GatewayIpAddress" 屬性中必須有唯一的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="00616-125">The local network gateways corresponding to your VPN devices must have unique public IP addresses in the "GatewayIpAddress" property.</span></span>
3. <span data-ttu-id="00616-126">此組態需要 BGP。</span><span class="sxs-lookup"><span data-stu-id="00616-126">BGP is required for this configuration.</span></span> <span data-ttu-id="00616-127">代表 VPN 裝置的每個區域網路閘道都必須有在 "BgpPeerIpAddress" 屬性中指定的唯一 BGP 對等 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="00616-127">Each local network gateway representing a VPN device must have a unique BGP peer IP address specified in the "BgpPeerIpAddress" property.</span></span>
4. <span data-ttu-id="00616-128">每個區域網路閘道中的 AddressPrefix 屬性欄位不得重疊。</span><span class="sxs-lookup"><span data-stu-id="00616-128">The AddressPrefix property field in each local network gateway must not overlap.</span></span> <span data-ttu-id="00616-129">您應該在 AddressPrefix 欄位中指定 /32 CIDR 格式的 "BgpPeerIpAddress"，例如 10.200.200.254/32。</span><span class="sxs-lookup"><span data-stu-id="00616-129">You should specify the "BgpPeerIpAddress" in /32 CIDR format in the AddressPrefix field, for example, 10.200.200.254/32.</span></span>
5. <span data-ttu-id="00616-130">您應該使用 BGP 向您的 Azure VPN 閘道通告相同內部部署網路首碼的相同首碼，而流量會同時透過這些通道轉送。</span><span class="sxs-lookup"><span data-stu-id="00616-130">You should use BGP to advertise the same prefixes of the same on-premises network prefixes to your Azure VPN gateway, and the traffic will be forwarded through these tunnels simultaneously.</span></span>
6. <span data-ttu-id="00616-131">每個連線會計入 Azure VPN 閘道的通道數目上限，基本和標準 SKU 的上限為 10，而高效能 SKU 的上限為 30。</span><span class="sxs-lookup"><span data-stu-id="00616-131">Each connection is counted against the maximum number of tunnels for your Azure VPN gateway, 10 for Basic and Standard SKUs, and 30 for HighPerformance SKU.</span></span> 

<span data-ttu-id="00616-132">在此組態中，Azure VPN 閘道仍處於作用中-待命模式，因此，仍會發生如 [上面](#activestandby)所述的相同容錯移轉行為和短暫中斷。</span><span class="sxs-lookup"><span data-stu-id="00616-132">In this configuration, the Azure VPN gateway is still in active-standby mode, so the same failover behavior and brief interruption will still happen as described [above](#activestandby).</span></span> <span data-ttu-id="00616-133">但這項設定可防範內部部署網路和 VPN 裝置發生錯誤或中斷。</span><span class="sxs-lookup"><span data-stu-id="00616-133">But this setup guards against failures or interruptions on your on-premises network and VPN devices.</span></span>

### <a name="active-active-azure-vpn-gateway"></a><span data-ttu-id="00616-134">主動-主動 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="00616-134">Active-active Azure VPN gateway</span></span>
<span data-ttu-id="00616-135">您現在可以在主動-主動組態中建立 Azure VPN 閘道，其中兩個閘道 VM 執行個體將會對內部部署 VPN 裝置建立 S2S VPN 通道，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="00616-135">You can now create an Azure VPN gateway in an active-active configuration, where both instances of the gateway VMs will establish S2S VPN tunnels to your on-premises VPN device, as shown the following diagram:</span></span>

![主動-主動](./media/vpn-gateway-highlyavailable/active-active.png)

<span data-ttu-id="00616-137">在此組態中，每個 Azure 閘道執行個體都會有唯一的公用 IP 位址，而每個執行個體會對在區域網路閘道與連線中指定的內部部署 VPN 裝置建立 IPsec/IKE S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="00616-137">In this configuration, each Azure gateway instance will have a unique public IP address, and each will establish an IPsec/IKE S2S VPN tunnel to your on-premises VPN device specified in your local network gateway and connection.</span></span> <span data-ttu-id="00616-138">請注意，這兩個 VPN 通道實際上屬於相同的連線。</span><span class="sxs-lookup"><span data-stu-id="00616-138">Note that both VPN tunnels are actually part of the same connection.</span></span> <span data-ttu-id="00616-139">您仍必須設定內部部署 VPN 裝置，才能接受或建立對這兩個 Azure VPN 閘道公用 IP 位址的兩個 S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="00616-139">You will still need to configure your on-premises VPN device to accept or establish two S2S VPN tunnels to those two Azure VPN gateway public IP addresses.</span></span>

<span data-ttu-id="00616-140">因為 Azure 閘道執行個體是在主動-主動組態中，所以從 Azure 虛擬網路到內部部署網路的流量會同時透過這兩個通道路由傳送，即使內部部署 VPN 裝置可能偏好其中一個通道亦然。</span><span class="sxs-lookup"><span data-stu-id="00616-140">Because the Azure gateway instances are in active-active configuration, the traffic from your Azure virtual network to your on-premises network will be routed through both tunnels simultaneously, even if your on-premises VPN device may favor one tunnel over the other.</span></span> <span data-ttu-id="00616-141">請注意，除非其中一個執行個體發生維護事件，否則相同的 TCP 或 UDP 流量一律會周遊相同的通道或路徑。</span><span class="sxs-lookup"><span data-stu-id="00616-141">Note though the same TCP or UDP flow will always traverse the same tunnel or path, unless a maintenance event happens on one of the instances.</span></span>

<span data-ttu-id="00616-142">當一個閘道器執行個體發生計劃性維護或非計劃性事件時，從該執行個體至內部部署 VPN 裝置的 IPsec 通道將會中斷。</span><span class="sxs-lookup"><span data-stu-id="00616-142">When a planned maintenance or unplanned event happens to one gateway instance, the IPsec tunnel from that instance to your on-premises VPN device will be disconnected.</span></span> <span data-ttu-id="00616-143">VPN 裝置上的對應路由應會自動移除或撤銷，以便將流量切換到其他作用中 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="00616-143">The corresponding routes on your VPN devices should be removed or withdrawn automatically so that the traffic will be switched over to the other active IPsec tunnel.</span></span> <span data-ttu-id="00616-144">在 Azure 端，會從受影響的執行個體自動切換到作用中執行個體。</span><span class="sxs-lookup"><span data-stu-id="00616-144">On the Azure side, the switch over will happen automatically from the affected instance to the active instance.</span></span>

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a><span data-ttu-id="00616-145">雙重備援︰Azure 和內部部署網路的主動-主動 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="00616-145">Dual-redundancy: active-active VPN gateways for both Azure and on-premises networks</span></span>
<span data-ttu-id="00616-146">最可靠的選項是結合網路和 Azure 上的主動-主動閘道，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="00616-146">The most reliable option is to combine the active-active gateways on both your network and Azure, as shown in the diagram below.</span></span>

![雙重備援](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

<span data-ttu-id="00616-148">您會在主動-主動組態中建立和設定 Azure VPN 閘道，並針對如上所述的兩個內部部署 VPN 裝置，建立兩個區域網路閘道和兩個連線。</span><span class="sxs-lookup"><span data-stu-id="00616-148">Here you create and setup the Azure VPN gateway in an active-active configuration, and create two local network gateways and two connections for your two on-premises VPN devices as described above.</span></span> <span data-ttu-id="00616-149">結果是 Azure 虛擬網路與內部部署網路之間有包含 4 個 IPsec 通道的完整網狀連線。</span><span class="sxs-lookup"><span data-stu-id="00616-149">The result is a full mesh connectivity of 4 IPsec tunnels between your Azure virtual network and your on-premises network.</span></span>

<span data-ttu-id="00616-150">所有閘道和通道都是從 Azure 端起作用，所以流量會同時分散於 4 個通道，而每個 TCP 或 UDP 流量會再次遵循出自 Azure 端的相同通道或路徑。</span><span class="sxs-lookup"><span data-stu-id="00616-150">All gateways and tunnels are active from the Azure side, so the traffic will be spread among all 4 tunnels simultaneously, although each TCP or UDP flow will again follow the same tunnel or path from the Azure side.</span></span> <span data-ttu-id="00616-151">即使分散流量，您可能會看到 IPsec 通道上的輸送量稍微變好，而此組態的主要目標是要達到高可用性。</span><span class="sxs-lookup"><span data-stu-id="00616-151">Even though by spreading the traffic, you may see slightly better throughput over the IPsec tunnels, the primary goal of this configuration is for high availability.</span></span> <span data-ttu-id="00616-152">而且由於分散的統計特性，因此難以提供不同應用程式流量狀況對彙總輸送量有何影響的測量方式。</span><span class="sxs-lookup"><span data-stu-id="00616-152">And due to the statistical nature of the spreading, it is difficult to provide the measurement on how different application traffic conditions will affect the aggregate throughput.</span></span>

<span data-ttu-id="00616-153">此拓撲需要兩個區域網路閘道和兩個連線以支援成對的內部部署 VPN 裝置，而且需要 BGP 才能允許相同內部部署網路的兩個連線。</span><span class="sxs-lookup"><span data-stu-id="00616-153">This topology will require two local network gateways and two connections to support the pair of on-premises VPN devices, and BGP is required to allow the two connections to the same on-premises network.</span></span> <span data-ttu-id="00616-154">這些需求與 [上面](#activeactiveonprem)的需求相同。</span><span class="sxs-lookup"><span data-stu-id="00616-154">These requirements are the same as the [above](#activeactiveonprem).</span></span> 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a><span data-ttu-id="00616-155">透過 Azure VPN 閘道的高可用性 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="00616-155">Highly Available VNet-to-VNet Connectivity through Azure VPN Gateways</span></span>
<span data-ttu-id="00616-156">相同的主動-主動組態也適用於 Azure VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="00616-156">The same active-active configuration can also apply to Azure VNet-to-VNet connections.</span></span> <span data-ttu-id="00616-157">您可以為兩個虛擬網路建立主動-主動 VPN 閘道，並將它們連在一起，以在兩個 VNet 之間形成包含 4 個通道的相同完整網狀連線，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="00616-157">You can create active-active VPN gateways for both virtual networks, and connect them together to form the same full mesh connectivity of 4 tunnels between the two VNets, as shown in the diagram below:</span></span>

![VNet 對 VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

<span data-ttu-id="00616-159">這可確保任何計劃性維護事件的兩個虛擬網路之間一律有一組通道，以提供更好的可用性。</span><span class="sxs-lookup"><span data-stu-id="00616-159">This ensures there are always a pair of tunnels between the two virtual networks for any planned maintenance events, providing even better availability.</span></span> <span data-ttu-id="00616-160">即使適用於跨單位連線的相同拓撲需要兩個連線，如上所示的 VNet 對 VNet 拓樸對每個閘道只需要一個連線。</span><span class="sxs-lookup"><span data-stu-id="00616-160">Even though the same topology for cross-premises connectivity requires two connections, the VNet-to-VNet topology shown above will need only one connection for each gateway.</span></span> <span data-ttu-id="00616-161">此外，除非透過 VNet 對 VNet 連線的傳輸路由是必要的，否則 BGP 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="00616-161">Additionally, BGP is optional unless transit routing over the VNet-to-VNet connection is required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00616-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00616-162">Next steps</span></span>
<span data-ttu-id="00616-163">如需設定主動-主動跨單位和 VNet 對 VNet 連線的步驟，請參閱[設定跨單位和 VNet 對 VNet 連線的主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="00616-163">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

