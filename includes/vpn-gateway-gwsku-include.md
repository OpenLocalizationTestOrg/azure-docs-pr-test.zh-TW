<span data-ttu-id="b7c6c-101">當您建立虛擬網路閘道時，您會需要 toospecify hello 閘道 SKU 的 toouse。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-101">When you create a virtual network gateway, you need toospecify hello gateway SKU that you want toouse.</span></span> <span data-ttu-id="b7c6c-102">選取符合需求的工作負載、 輸送量、 功能和 Sla hello 類型為基礎的 hello Sku。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-102">Select hello SKUs that satisfy your requirements based on hello types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="b7c6c-103"><a name="workloads"></a>生產與開發測試工作負載</span><span class="sxs-lookup"><span data-stu-id="b7c6c-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="b7c6c-104">Sla 」 和 「 功能集 toohello 差異，因為我們建議您遵循 Sku 生產環境的 hello*與*開發測試：</span><span class="sxs-lookup"><span data-stu-id="b7c6c-104">Due toohello differences in SLAs and feature sets, we recommend hello following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="b7c6c-105">**工作負載**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-105">**Workload**</span></span>                       | <span data-ttu-id="b7c6c-106">**SKU**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="b7c6c-107">**生產、重要工作負載**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-107">**Production, critical workloads**</span></span> | <span data-ttu-id="b7c6c-108">VpnGw1、VpnGw2、VpnGw3</span><span class="sxs-lookup"><span data-stu-id="b7c6c-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="b7c6c-109">**開發測試或概念證明**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="b7c6c-110">基本</span><span class="sxs-lookup"><span data-stu-id="b7c6c-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="b7c6c-111">如果您使用舊的 hello hello 生產 SKU 建議的 Sku 是標準和高效能的分散式 Sku。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-111">If you are using hello old SKUs, hello production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="b7c6c-112">如需 hello 舊 Sku，請參閱[閘道 Sku (舊版 Sku)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-112">For information on hello old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="b7c6c-113"><a name="feature"></a>閘道 SKU 功能集</span><span class="sxs-lookup"><span data-stu-id="b7c6c-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="b7c6c-114">hello 新的閘道 Sku 簡化 hello hello 閘道所提供的功能集：</span><span class="sxs-lookup"><span data-stu-id="b7c6c-114">hello new gateway SKUs streamline hello feature sets offered on hello gateways:</span></span>

| <span data-ttu-id="b7c6c-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-115">**SKU**</span></span>| <span data-ttu-id="b7c6c-116">**特性**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="b7c6c-117">**基本**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-117">**Basic**</span></span>   | <span data-ttu-id="b7c6c-118">**路由式 VPN**：10 個通道 (含 P2S)</span><span class="sxs-lookup"><span data-stu-id="b7c6c-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="b7c6c-119">**原則式 VPN** (IKEv1)：1 個通道；沒有 P2S</span><span class="sxs-lookup"><span data-stu-id="b7c6c-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="b7c6c-120">**VpnGw1、VpnGw2 和 VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="b7c6c-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="b7c6c-121">**路由式 VPN**： 向上 too30 通道 （*） P2S、 BGP，主動-主動、 自訂 IPsec/IKE 原則、 ExpressRoute 或 VPN 共存</span><span class="sxs-lookup"><span data-stu-id="b7c6c-121">**Route-based VPN**: up too30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="b7c6c-122">(*)您可以設定 「 PolicyBasedTrafficSelectors"tooconnect 路由式 VPN 閘道 （VpnGw1、 VpnGw2、 VpnGw3） toomultiple 內部以原則為基礎的防火牆裝置。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-122">(*) You can configure "PolicyBasedTrafficSelectors" tooconnect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="b7c6c-123">請參閱太[連接 VPN 閘道 toomultiple 內部以原則為基礎的 VPN 裝置使用 PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-123">Refer too[Connect VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="b7c6c-124"><a name="resize"></a>調整閘道 SKU 的大小</span><span class="sxs-lookup"><span data-stu-id="b7c6c-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="b7c6c-125">您可以調整 VpnGw1、VpnGw2 和 VpnGw3 SKU 之間的大小。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="b7c6c-126">當使用 hello 舊閘道 Sku，您可以調整之間 Basic、 Standard 和高效能的分散式 Sku。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-126">When working with hello old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="b7c6c-127">您**無法**調整大小，從基本/標準/HighPerformance Sku toohello 新 VpnGw1/VpnGw2/VpnGw3 Sku。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs toohello new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="b7c6c-128">您必須，相反地，[移轉](#migrate)toohello 新 Sku。</span><span class="sxs-lookup"><span data-stu-id="b7c6c-128">You must, instead, [migrate](#migrate) toohello new SKUs.</span></span>

###  <span data-ttu-id="b7c6c-129"><a name="migrate"></a>從舊的 Sku toohello 移轉新的 Sku</span><span class="sxs-lookup"><span data-stu-id="b7c6c-129"><a name="migrate"></a>Migrating from old SKUs toohello new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
