<span data-ttu-id="71faf-101">VNet 對 VNet 常見問題集適用於 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="71faf-101">The VNet-to-VNet FAQ applies to VPN Gateway connections.</span></span> <span data-ttu-id="71faf-102">如果您要尋找 VNet 對等互連，請參閱[虛擬網路對等互連](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="71faf-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="71faf-103">Azure 會對 VNet 之間的流量收費嗎？</span><span class="sxs-lookup"><span data-stu-id="71faf-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="71faf-104">使用 VPN 閘道連線時，相同區域內的 VNet 對 VNet 流量雙向皆為免費。</span><span class="sxs-lookup"><span data-stu-id="71faf-104">VNet-to-VNet traffic within the same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="71faf-105">跨區域 VNet 對 VNet 輸出流量會根據來源區域的輸出 VNet 間資料傳輸費率收費。</span><span class="sxs-lookup"><span data-stu-id="71faf-105">Cross region VNet-to-VNet egress traffic is charged with the outbound inter-VNet data transfer rates based on the source regions.</span></span> <span data-ttu-id="71faf-106">如需詳細資訊，請參閱 [VPN 閘道定價頁面](https://azure.microsoft.com/pricing/details/vpn-gateway/)。</span><span class="sxs-lookup"><span data-stu-id="71faf-106">Refer to the [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="71faf-107">如果您要使用 VNet 對等互連而非 VPN 閘道來連線 Vnet，請參閱[虛擬網路定價頁面](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="71faf-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see the [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a><span data-ttu-id="71faf-108">VNet 對 VNet 流量是否會透過網際網路傳輸？</span><span class="sxs-lookup"><span data-stu-id="71faf-108">Does VNet-to-VNet traffic travel across the Internet?</span></span>

<span data-ttu-id="71faf-109">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-109">No.</span></span> <span data-ttu-id="71faf-110">VNet 對 VNet 流量會透過 Microsoft Azure 骨幹傳輸，而非透過網際網路。</span><span class="sxs-lookup"><span data-stu-id="71faf-110">VNet-to-VNet traffic travels across the Microsoft Azure backbone, not the Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="71faf-111">VNet 對 VNet 流量是否安全？</span><span class="sxs-lookup"><span data-stu-id="71faf-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="71faf-112">是，它是由 IPsec/IKE 加密保護。</span><span class="sxs-lookup"><span data-stu-id="71faf-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a><span data-ttu-id="71faf-113">我需要將 VNet 連接在一起的 VPN 裝置嗎？</span><span class="sxs-lookup"><span data-stu-id="71faf-113">Do I need a VPN device to connect VNets together?</span></span>

<span data-ttu-id="71faf-114">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-114">No.</span></span> <span data-ttu-id="71faf-115">將多個 Azure 虛擬網路連接在一起並不需要 VPN 裝置，除非需要跨單位連線能力。</span><span class="sxs-lookup"><span data-stu-id="71faf-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-to-be-in-the-same-region"></a><span data-ttu-id="71faf-116">我的 VNet 需要位於相同區域嗎？</span><span class="sxs-lookup"><span data-stu-id="71faf-116">Do my VNets need to be in the same region?</span></span>

<span data-ttu-id="71faf-117">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-117">No.</span></span> <span data-ttu-id="71faf-118">虛擬網路可位於相同或不同的 Azure 區域 (位置)。</span><span class="sxs-lookup"><span data-stu-id="71faf-118">The virtual networks can be in the same or different Azure regions (locations).</span></span>

### <a name="if-the-vnets-are-not-in-the-same-subscription-do-the-subscriptions-need-to-be-associated-with-the-same-ad-tenant"></a><span data-ttu-id="71faf-119">如果 Vnet 不在相同的訂用帳戶中，訂用帳戶是否需要與相同的 AD 租用戶相關聯？</span><span class="sxs-lookup"><span data-stu-id="71faf-119">If the VNets are not in the same subscription, do the subscriptions need to be associated with the same AD tenant?</span></span>

<span data-ttu-id="71faf-120">編號</span><span class="sxs-lookup"><span data-stu-id="71faf-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="71faf-121">可以使用 VNet 對 VNet 以及多站台連線嗎？</span><span class="sxs-lookup"><span data-stu-id="71faf-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="71faf-122">是。</span><span class="sxs-lookup"><span data-stu-id="71faf-122">Yes.</span></span> <span data-ttu-id="71faf-123">虛擬網路連線能力可以與多站台 VPN 同時使用。</span><span class="sxs-lookup"><span data-stu-id="71faf-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="71faf-124">一個虛擬網路可以連接多少內部部署網站和虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="71faf-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="71faf-125">請參閱[閘道需求](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements)表格。</span><span class="sxs-lookup"><span data-stu-id="71faf-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="71faf-126">是否可以使用 VNet 對 VNet 連線來連接 VNet 外部的 VM 或雲端服務？</span><span class="sxs-lookup"><span data-stu-id="71faf-126">Can I use VNet-to-VNet to connect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="71faf-127">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-127">No.</span></span> <span data-ttu-id="71faf-128">VNet 對 VNet 支援連接虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="71faf-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="71faf-129">但是不支援連接不在虛擬網路中的虛擬機器或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="71faf-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="71faf-130">雲端服務或負載平衡端點是否可以跨越 VNet？</span><span class="sxs-lookup"><span data-stu-id="71faf-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="71faf-131">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-131">No.</span></span> <span data-ttu-id="71faf-132">即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="71faf-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="71faf-133">是否可以使用 PolicyBased VPN 類型進行 VNet 對 VNet 或多站台連線？</span><span class="sxs-lookup"><span data-stu-id="71faf-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="71faf-134">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-134">No.</span></span> <span data-ttu-id="71faf-135">VNet 對 VNet 和多站台連線需要 VPN 類型為 RouteBased (前稱為動態路由) 的 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="71faf-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="71faf-136">是否可以將 RouteBased VPN 類型的 VNet 連線到另一個 PolicyBased VPN 類型的 VNet？</span><span class="sxs-lookup"><span data-stu-id="71faf-136">Can I connect a VNet with a RouteBased VPN Type to another VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="71faf-137">否，這兩個虛擬網路必須使用路由式 (先前稱為動態路由) VPN。</span><span class="sxs-lookup"><span data-stu-id="71faf-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="71faf-138">VPN 通道是否共用頻寬？</span><span class="sxs-lookup"><span data-stu-id="71faf-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="71faf-139">是。</span><span class="sxs-lookup"><span data-stu-id="71faf-139">Yes.</span></span> <span data-ttu-id="71faf-140">虛擬網路的所有 VPN 通道一起共用 Azure VPN 閘道上可用的頻寬，以及 Azure 中相同的 VPN 閘道運作時間 SLA。</span><span class="sxs-lookup"><span data-stu-id="71faf-140">All VPN tunnels of the virtual network share the available bandwidth on the Azure VPN gateway and the same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="71faf-141">是否支援備援通道？</span><span class="sxs-lookup"><span data-stu-id="71faf-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="71faf-142">當一個虛擬網路閘道設定為主動-主動時，支援成對虛擬網路之間的備援通道。</span><span class="sxs-lookup"><span data-stu-id="71faf-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="71faf-143">VNet 對 VNet 組態的位址空間是否可以重疊？</span><span class="sxs-lookup"><span data-stu-id="71faf-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="71faf-144">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-144">No.</span></span> <span data-ttu-id="71faf-145">您的 IP 位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="71faf-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="71faf-146">在連接的虛擬網路和內部部署本機網站之間是否可以有重疊的位址空間？</span><span class="sxs-lookup"><span data-stu-id="71faf-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="71faf-147">否。</span><span class="sxs-lookup"><span data-stu-id="71faf-147">No.</span></span> <span data-ttu-id="71faf-148">您的 IP 位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="71faf-148">You can't have overlapping IP address ranges.</span></span>



