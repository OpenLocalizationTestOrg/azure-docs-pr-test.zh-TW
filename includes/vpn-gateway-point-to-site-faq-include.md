### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a><span data-ttu-id="48a20-101">可以使用哪些用戶端作業系統來搭配點對站台？</span><span class="sxs-lookup"><span data-stu-id="48a20-101">What client operating systems can I use with Point-to-Site?</span></span>

<span data-ttu-id="48a20-102">以下為支援的用戶端作業系統：</span><span class="sxs-lookup"><span data-stu-id="48a20-102">The following client operating systems are supported:</span></span>

* <span data-ttu-id="48a20-103">Windows 7 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-103">Windows 7 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="48a20-104">Windows Server 2008 R2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-104">Windows Server 2008 R2 (64-bit only)</span></span>
* <span data-ttu-id="48a20-105">Windows 8 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-105">Windows 8 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="48a20-106">Windows 8.1 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-106">Windows 8.1 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="48a20-107">Windows Server 2012 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-107">Windows Server 2012 (64-bit only)</span></span>
* <span data-ttu-id="48a20-108">Windows Server 2012 R2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="48a20-108">Windows Server 2012 R2 (64-bit only)</span></span>
* <span data-ttu-id="48a20-109">Windows 10</span><span class="sxs-lookup"><span data-stu-id="48a20-109">Windows 10</span></span>

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a><span data-ttu-id="48a20-110">是否可以對支援 SSTP 的點對站台使用任何軟體 VPN 用戶端？</span><span class="sxs-lookup"><span data-stu-id="48a20-110">Can I use any software VPN client for Point-to-Site that supports SSTP?</span></span>

<span data-ttu-id="48a20-111">否。</span><span class="sxs-lookup"><span data-stu-id="48a20-111">No.</span></span> <span data-ttu-id="48a20-112">支援只限於上面所列的 Windows 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="48a20-112">Support is limited only to the Windows operating system versions listed above.</span></span>

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a><span data-ttu-id="48a20-113">在我的點對站台組態中可以有多少個 VPN 用戶端端點？</span><span class="sxs-lookup"><span data-stu-id="48a20-113">How many VPN client endpoints can I have in my Point-to-Site configuration?</span></span>

<span data-ttu-id="48a20-114">我們最多支援 128 個 VPN 用戶端可以同時連線到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="48a20-114">We support up to 128 VPN clients to be able to connect to a virtual network at the same time.</span></span>

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a><span data-ttu-id="48a20-115">是否可以使用自己的內部 PKI 根 CA 進行點對站台連線？</span><span class="sxs-lookup"><span data-stu-id="48a20-115">Can I use my own internal PKI root CA for Point-to-Site connectivity?</span></span>

<span data-ttu-id="48a20-116">是。</span><span class="sxs-lookup"><span data-stu-id="48a20-116">Yes.</span></span> <span data-ttu-id="48a20-117">先前只能使用自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="48a20-117">Previously, only self-signed root certificates could be used.</span></span> <span data-ttu-id="48a20-118">您仍然可以上傳 20 個根憑證。</span><span class="sxs-lookup"><span data-stu-id="48a20-118">You can still upload 20 root certificates.</span></span>

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a><span data-ttu-id="48a20-119">是否可以使用點對站台功能周遊 Proxy 和防火牆？</span><span class="sxs-lookup"><span data-stu-id="48a20-119">Can I traverse proxies and firewalls using Point-to-Site capability?</span></span>

<span data-ttu-id="48a20-120">是。</span><span class="sxs-lookup"><span data-stu-id="48a20-120">Yes.</span></span> <span data-ttu-id="48a20-121">我們使用 SSTP (安全通訊端通道通訊協定) 穿過防火牆。</span><span class="sxs-lookup"><span data-stu-id="48a20-121">We use SSTP (Secure Socket Tunneling Protocol) to tunnel through firewalls.</span></span> <span data-ttu-id="48a20-122">此通道將會顯示為 HTTPs 連線。</span><span class="sxs-lookup"><span data-stu-id="48a20-122">This tunnel will appear as an HTTPs connection.</span></span>

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-the-vpn-automatically-reconnect"></a><span data-ttu-id="48a20-123">如果我重新啟動針對點對站台設定的用戶端電腦，VPN 將自動重新連線嗎？</span><span class="sxs-lookup"><span data-stu-id="48a20-123">If I restart a client computer configured for Point-to-Site, will the VPN automatically reconnect?</span></span>

<span data-ttu-id="48a20-124">用戶端電腦預設為不會自動重新建立 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="48a20-124">By default, the client computer will not reestablish the VPN connection automatically.</span></span>

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-the-vpn-clients"></a><span data-ttu-id="48a20-125">在 VPN 用戶端上點對站台支援自動重新連接和 DDNS 嗎？</span><span class="sxs-lookup"><span data-stu-id="48a20-125">Does Point-to-Site support auto-reconnect and DDNS on the VPN clients?</span></span>

<span data-ttu-id="48a20-126">點對站台 VPN 目前不支援自動重新連接和 DDNS。</span><span class="sxs-lookup"><span data-stu-id="48a20-126">Auto-reconnect and DDNS are currently not supported in Point-to-Site VPNs.</span></span>

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-the-same-virtual-network"></a><span data-ttu-id="48a20-127">對於相同的虛擬網路，網站間和點對站台組態是否可以同時存在？</span><span class="sxs-lookup"><span data-stu-id="48a20-127">Can I have Site-to-Site and Point-to-Site configurations coexist for the same virtual network?</span></span>

<span data-ttu-id="48a20-128">是。</span><span class="sxs-lookup"><span data-stu-id="48a20-128">Yes.</span></span> <span data-ttu-id="48a20-129">如果閘道是路由式 VPN 類型，這兩個解決方案都可正常運作。</span><span class="sxs-lookup"><span data-stu-id="48a20-129">Both these solutions will work if you have a RouteBased VPN type for your gateway.</span></span> <span data-ttu-id="48a20-130">如果是傳統部署模型，則需要動態閘道。</span><span class="sxs-lookup"><span data-stu-id="48a20-130">For the classic deployment model, you need a dynamic gateway.</span></span> <span data-ttu-id="48a20-131">靜態路由 VPN 閘道或使用 `-VpnType PolicyBased` cmdlet 的閘道不支援點對站。</span><span class="sxs-lookup"><span data-stu-id="48a20-131">We do not support Point-to-Site for static routing VPN gateways or gateways using the `-VpnType PolicyBased` cmdlet.</span></span>

### <a name="can-i-configure-a-point-to-site-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a><span data-ttu-id="48a20-132">是否可以將點對站台用戶端設定為同時連接到多個虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="48a20-132">Can I configure a Point-to-Site client to connect to multiple virtual networks at the same time?</span></span>

<span data-ttu-id="48a20-133">是，可以的。</span><span class="sxs-lookup"><span data-stu-id="48a20-133">Yes, it is possible.</span></span> <span data-ttu-id="48a20-134">但是虛擬網路不能有重疊的 IP 前置詞，而且點對站台位址空間在虛擬網路之間不得重疊。</span><span class="sxs-lookup"><span data-stu-id="48a20-134">But the virtual networks cannot have overlapping IP prefixes and the Point-to-Site address spaces must not overlap between the virtual networks.</span></span>

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a><span data-ttu-id="48a20-135">透過網站間或點對站台連線可以獲得多少輸送量？</span><span class="sxs-lookup"><span data-stu-id="48a20-135">How much throughput can I expect through Site-to-Site or Point-to-Site connections?</span></span>

<span data-ttu-id="48a20-136">很難維護 VPN 通道的確切輸送量。</span><span class="sxs-lookup"><span data-stu-id="48a20-136">It's difficult to maintain the exact throughput of the VPN tunnels.</span></span> <span data-ttu-id="48a20-137">IPsec 和 SSTP 為加密嚴謹的 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="48a20-137">IPsec and SSTP are crypto-heavy VPN protocols.</span></span> <span data-ttu-id="48a20-138">輸送量也會受限於內部部署與網際網路之間的延遲和頻寬。</span><span class="sxs-lookup"><span data-stu-id="48a20-138">Throughput is also limited by the latency and bandwidth between your premises and the Internet.</span></span>