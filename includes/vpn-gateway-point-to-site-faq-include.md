### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a><span data-ttu-id="e1be8-101">可以使用哪些用戶端作業系統來搭配點對站台？</span><span class="sxs-lookup"><span data-stu-id="e1be8-101">What client operating systems can I use with Point-to-Site?</span></span>

<span data-ttu-id="e1be8-102">支援下列用戶端作業系統的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1be8-102">hello following client operating systems are supported:</span></span>

* <span data-ttu-id="e1be8-103">Windows 7 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-103">Windows 7 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="e1be8-104">Windows Server 2008 R2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-104">Windows Server 2008 R2 (64-bit only)</span></span>
* <span data-ttu-id="e1be8-105">Windows 8 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-105">Windows 8 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="e1be8-106">Windows 8.1 (32 位元和 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-106">Windows 8.1 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="e1be8-107">Windows Server 2012 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-107">Windows Server 2012 (64-bit only)</span></span>
* <span data-ttu-id="e1be8-108">Windows Server 2012 R2 (僅限 64 位元)</span><span class="sxs-lookup"><span data-stu-id="e1be8-108">Windows Server 2012 R2 (64-bit only)</span></span>
* <span data-ttu-id="e1be8-109">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e1be8-109">Windows 10</span></span>

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a><span data-ttu-id="e1be8-110">是否可以對支援 SSTP 的點對站台使用任何軟體 VPN 用戶端？</span><span class="sxs-lookup"><span data-stu-id="e1be8-110">Can I use any software VPN client for Point-to-Site that supports SSTP?</span></span>

<span data-ttu-id="e1be8-111">否。</span><span class="sxs-lookup"><span data-stu-id="e1be8-111">No.</span></span> <span data-ttu-id="e1be8-112">支援是限制只有 toohello Windows 作業系統版本上面所列。</span><span class="sxs-lookup"><span data-stu-id="e1be8-112">Support is limited only toohello Windows operating system versions listed above.</span></span>

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a><span data-ttu-id="e1be8-113">在我的點對站台組態中可以有多少個 VPN 用戶端端點？</span><span class="sxs-lookup"><span data-stu-id="e1be8-113">How many VPN client endpoints can I have in my Point-to-Site configuration?</span></span>

<span data-ttu-id="e1be8-114">我們 too128 VPN 用戶端 toobe 無法 tooconnect tooa 虛擬網路在 hello 支援相同的時間。</span><span class="sxs-lookup"><span data-stu-id="e1be8-114">We support up too128 VPN clients toobe able tooconnect tooa virtual network at hello same time.</span></span>

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a><span data-ttu-id="e1be8-115">是否可以使用自己的內部 PKI 根 CA 進行點對站台連線？</span><span class="sxs-lookup"><span data-stu-id="e1be8-115">Can I use my own internal PKI root CA for Point-to-Site connectivity?</span></span>

<span data-ttu-id="e1be8-116">是。</span><span class="sxs-lookup"><span data-stu-id="e1be8-116">Yes.</span></span> <span data-ttu-id="e1be8-117">先前只能使用自我簽署的根憑證。</span><span class="sxs-lookup"><span data-stu-id="e1be8-117">Previously, only self-signed root certificates could be used.</span></span> <span data-ttu-id="e1be8-118">您仍然可以上傳 20 個根憑證。</span><span class="sxs-lookup"><span data-stu-id="e1be8-118">You can still upload 20 root certificates.</span></span>

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a><span data-ttu-id="e1be8-119">是否可以使用點對站台功能周遊 Proxy 和防火牆？</span><span class="sxs-lookup"><span data-stu-id="e1be8-119">Can I traverse proxies and firewalls using Point-to-Site capability?</span></span>

<span data-ttu-id="e1be8-120">是。</span><span class="sxs-lookup"><span data-stu-id="e1be8-120">Yes.</span></span> <span data-ttu-id="e1be8-121">我們使用 SSTP （安全通訊端通道通訊協定） tootunnel 通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="e1be8-121">We use SSTP (Secure Socket Tunneling Protocol) tootunnel through firewalls.</span></span> <span data-ttu-id="e1be8-122">此通道將會顯示為 HTTPs 連線。</span><span class="sxs-lookup"><span data-stu-id="e1be8-122">This tunnel will appear as an HTTPs connection.</span></span>

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a><span data-ttu-id="e1be8-123">如果我重新啟動設定點對站用戶端電腦時，會 hello VPN 自動重新連線嗎？</span><span class="sxs-lookup"><span data-stu-id="e1be8-123">If I restart a client computer configured for Point-to-Site, will hello VPN automatically reconnect?</span></span>

<span data-ttu-id="e1be8-124">根據預設，hello 用戶端電腦將不重新建立 hello VPN 連線自動。</span><span class="sxs-lookup"><span data-stu-id="e1be8-124">By default, hello client computer will not reestablish hello VPN connection automatically.</span></span>

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a><span data-ttu-id="e1be8-125">沒有點對站台支援自動重新連接和 DDNS 上的 hello VPN 用戶端嗎？</span><span class="sxs-lookup"><span data-stu-id="e1be8-125">Does Point-to-Site support auto-reconnect and DDNS on hello VPN clients?</span></span>

<span data-ttu-id="e1be8-126">點對站台 VPN 目前不支援自動重新連接和 DDNS。</span><span class="sxs-lookup"><span data-stu-id="e1be8-126">Auto-reconnect and DDNS are currently not supported in Point-to-Site VPNs.</span></span>

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a><span data-ttu-id="e1be8-127">我可以有站對站和點對站組態共存 hello 相同虛擬網路嗎？</span><span class="sxs-lookup"><span data-stu-id="e1be8-127">Can I have Site-to-Site and Point-to-Site configurations coexist for hello same virtual network?</span></span>

<span data-ttu-id="e1be8-128">是。</span><span class="sxs-lookup"><span data-stu-id="e1be8-128">Yes.</span></span> <span data-ttu-id="e1be8-129">如果閘道是路由式 VPN 類型，這兩個解決方案都可正常運作。</span><span class="sxs-lookup"><span data-stu-id="e1be8-129">Both these solutions will work if you have a RouteBased VPN type for your gateway.</span></span> <span data-ttu-id="e1be8-130">Hello 傳統部署模型，您需要動態閘道。</span><span class="sxs-lookup"><span data-stu-id="e1be8-130">For hello classic deployment model, you need a dynamic gateway.</span></span> <span data-ttu-id="e1be8-131">我們做了不支援點對站靜態路由 VPN 閘道或使用 hello 閘道`-VpnType PolicyBased`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e1be8-131">We do not support Point-to-Site for static routing VPN gateways or gateways using hello `-VpnType PolicyBased` cmdlet.</span></span>

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a><span data-ttu-id="e1be8-132">可以設定點對站台用戶端 tooconnect toomultiple 虛擬網路在 hello 相同的時間？</span><span class="sxs-lookup"><span data-stu-id="e1be8-132">Can I configure a Point-to-Site client tooconnect toomultiple virtual networks at hello same time?</span></span>

<span data-ttu-id="e1be8-133">是，可以的。</span><span class="sxs-lookup"><span data-stu-id="e1be8-133">Yes, it is possible.</span></span> <span data-ttu-id="e1be8-134">但是 hello 虛擬網路不能有重疊的 IP 首碼，而且 hello 點對站位址空間不得重疊 hello 虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="e1be8-134">But hello virtual networks cannot have overlapping IP prefixes and hello Point-to-Site address spaces must not overlap between hello virtual networks.</span></span>

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a><span data-ttu-id="e1be8-135">透過網站間或點對站台連線可以獲得多少輸送量？</span><span class="sxs-lookup"><span data-stu-id="e1be8-135">How much throughput can I expect through Site-to-Site or Point-to-Site connections?</span></span>

<span data-ttu-id="e1be8-136">很難 toomaintain hello 確切的輸送量的 hello VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="e1be8-136">It's difficult toomaintain hello exact throughput of hello VPN tunnels.</span></span> <span data-ttu-id="e1be8-137">IPsec 和 SSTP 為加密嚴謹的 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e1be8-137">IPsec and SSTP are crypto-heavy VPN protocols.</span></span> <span data-ttu-id="e1be8-138">輸送量也受到 hello 延遲和內部部署與 hello 網際網路之間的頻寬。</span><span class="sxs-lookup"><span data-stu-id="e1be8-138">Throughput is also limited by hello latency and bandwidth between your premises and hello Internet.</span></span>
