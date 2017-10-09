<span data-ttu-id="bd9ec-101">hello VNet 對 VNet 常見問題集適用於 tooVPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="bd9ec-102">如果您要尋找 VNet 對等互連，請參閱[虛擬網路對等互連](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd9ec-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="bd9ec-103">Azure 會對 VNet 之間的流量收費嗎？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="bd9ec-104">VNet 對 VNet 流量內 hello 相同區域時，兩個方向可以免費使用 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="bd9ec-105">跨區域 VNet 對 VNet 輸出流量的收費的依據 hello 來源區域的 hello 輸出間 VNet 資料傳輸速率。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="bd9ec-106">請參閱 toohello [VPN 閘道定價頁面](https://azure.microsoft.com/pricing/details/vpn-gateway/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="bd9ec-107">如果您要連接的 Vnet 使用 VNet 對等互連，而不是 VPN 閘道，請參閱 hello[定價頁面的虛擬網路](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="bd9ec-108">VNet 對 VNet 流量是否跨網際網路 hello 移動？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="bd9ec-109">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-109">No.</span></span> <span data-ttu-id="bd9ec-110">VNet 對 VNet 流量會透過 Microsoft Azure backbone hello 網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="bd9ec-111">VNet 對 VNet 流量是否安全？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="bd9ec-112">是，它是由 IPsec/IKE 加密保護。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="bd9ec-113">我需要 VPN 裝置 tooconnect Vnet 一起嗎？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="bd9ec-114">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-114">No.</span></span> <span data-ttu-id="bd9ec-115">將多個 Azure 虛擬網路連接在一起並不需要 VPN 裝置，除非需要跨單位連線能力。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="bd9ec-116">我的 Vnet 是否需要在 hello toobe 相同區域？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="bd9ec-117">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-117">No.</span></span> <span data-ttu-id="bd9ec-118">hello 虛擬網路可位於 hello 相同或不同 Azure 區域 （位置）。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="bd9ec-119">如果不在 hello Vnet hello 相同訂用帳戶，並訂閱 hello 需要 toobe hello 相同 AD 租用戶相關聯？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="bd9ec-120">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="bd9ec-121">可以使用 VNet 對 VNet 以及多站台連線嗎？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="bd9ec-122">是。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-122">Yes.</span></span> <span data-ttu-id="bd9ec-123">虛擬網路連線能力可以與多站台 VPN 同時使用。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="bd9ec-124">一個虛擬網路可以連接多少內部部署網站和虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="bd9ec-125">請參閱[閘道需求](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements)表格。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="bd9ec-126">我可以使用 VNet 對 VNet tooconnect Vm 或雲端服務之外 VNet 嗎？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="bd9ec-127">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-127">No.</span></span> <span data-ttu-id="bd9ec-128">VNet 對 VNet 支援連接虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="bd9ec-129">但是不支援連接不在虛擬網路中的虛擬機器或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="bd9ec-130">雲端服務或負載平衡端點是否可以跨越 VNet？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="bd9ec-131">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-131">No.</span></span> <span data-ttu-id="bd9ec-132">即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="bd9ec-133">是否可以使用 PolicyBased VPN 類型進行 VNet 對 VNet 或多站台連線？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="bd9ec-134">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-134">No.</span></span> <span data-ttu-id="bd9ec-135">VNet 對 VNet 和多站台連線需要 VPN 類型為 RouteBased (前稱為動態路由) 的 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="bd9ec-136">我可以連接 VNet 與 RouteBased VPN 類型 tooanother VNet PolicyBased VPN 類型？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="bd9ec-137">否，這兩個虛擬網路必須使用路由式 (先前稱為動態路由) VPN。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="bd9ec-138">VPN 通道是否共用頻寬？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="bd9ec-139">是。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-139">Yes.</span></span> <span data-ttu-id="bd9ec-140">Hello 虛擬網路的所有 VPN 通道共用 hello hello Azure VPN 閘道上的可用頻寬，並且 hello 相同 azure VPN 閘道執行時間 SLA。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="bd9ec-141">是否支援備援通道？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="bd9ec-142">當一個虛擬網路閘道設定為主動-主動時，支援成對虛擬網路之間的備援通道。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="bd9ec-143">VNet 對 VNet 組態的位址空間是否可以重疊？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="bd9ec-144">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-144">No.</span></span> <span data-ttu-id="bd9ec-145">您的 IP 位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="bd9ec-146">在連接的虛擬網路和內部部署本機網站之間是否可以有重疊的位址空間？</span><span class="sxs-lookup"><span data-stu-id="bd9ec-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="bd9ec-147">否。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-147">No.</span></span> <span data-ttu-id="bd9ec-148">您的 IP 位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="bd9ec-148">You can't have overlapping IP address ranges.</span></span>



