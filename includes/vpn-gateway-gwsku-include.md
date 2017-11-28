<span data-ttu-id="c1f00-101">建立虛擬網路閘道時，您必須指定想要使用的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="c1f00-101">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="c1f00-102">根據工作負載、輸送量、功能和 SLA 的類型，選取符合您需求的 SKU。</span><span class="sxs-lookup"><span data-stu-id="c1f00-102">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="c1f00-103"><a name="workloads"></a>生產與開發測試工作負載</span><span class="sxs-lookup"><span data-stu-id="c1f00-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="c1f00-104">由於 SLA 和功能集的差異，我們建議將下列 SKU 用於產生與開發測試：</span><span class="sxs-lookup"><span data-stu-id="c1f00-104">Due to the differences in SLAs and feature sets, we recommend the following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="c1f00-105">**工作負載**</span><span class="sxs-lookup"><span data-stu-id="c1f00-105">**Workload**</span></span>                       | <span data-ttu-id="c1f00-106">**SKU**</span><span class="sxs-lookup"><span data-stu-id="c1f00-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="c1f00-107">**生產、重要工作負載**</span><span class="sxs-lookup"><span data-stu-id="c1f00-107">**Production, critical workloads**</span></span> | <span data-ttu-id="c1f00-108">VpnGw1、VpnGw2、VpnGw3</span><span class="sxs-lookup"><span data-stu-id="c1f00-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="c1f00-109">**開發測試或概念證明**</span><span class="sxs-lookup"><span data-stu-id="c1f00-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="c1f00-110">基本</span><span class="sxs-lookup"><span data-stu-id="c1f00-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="c1f00-111">如果您使用舊式 SKU，生產 SKU 建議為基本和高效能 SKU。</span><span class="sxs-lookup"><span data-stu-id="c1f00-111">If you are using the old SKUs, the production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="c1f00-112">如需舊式 SKU 的相關資訊，請參閱[閘道 SKU (舊版 SKU)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="c1f00-112">For information on the old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="c1f00-113"><a name="feature"></a>閘道 SKU 功能集</span><span class="sxs-lookup"><span data-stu-id="c1f00-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="c1f00-114">新式閘道 SKU 可簡化閘道上提供的功能集：</span><span class="sxs-lookup"><span data-stu-id="c1f00-114">The new gateway SKUs streamline the feature sets offered on the gateways:</span></span>

| <span data-ttu-id="c1f00-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="c1f00-115">**SKU**</span></span>| <span data-ttu-id="c1f00-116">**特性**</span><span class="sxs-lookup"><span data-stu-id="c1f00-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="c1f00-117">**基本**</span><span class="sxs-lookup"><span data-stu-id="c1f00-117">**Basic**</span></span>   | <span data-ttu-id="c1f00-118">**路由式 VPN**：10 個通道 (含 P2S)</span><span class="sxs-lookup"><span data-stu-id="c1f00-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="c1f00-119">**原則式 VPN** (IKEv1)：1 個通道；沒有 P2S</span><span class="sxs-lookup"><span data-stu-id="c1f00-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="c1f00-120">**VpnGw1、VpnGw2 和 VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="c1f00-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="c1f00-121">**路由式 VPN**：最多 30 個通道 (*)，P2S、BGP、主動-主動、自訂 IPsec/IKE 原則、ExpressRoute/VPN 共存</span><span class="sxs-lookup"><span data-stu-id="c1f00-121">**Route-based VPN**: up to 30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="c1f00-122">(*) 您可以設定 "PolicyBasedTrafficSelectors"，將以路由為基礎的 VPN 閘道 (VpnGw1、VpnGw2、VpnGw3) 連線至多個內部部署以原則為基礎的防火牆裝置。</span><span class="sxs-lookup"><span data-stu-id="c1f00-122">(*) You can configure "PolicyBasedTrafficSelectors" to connect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) to multiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="c1f00-123">如需詳細資訊，請參閱[使用 PowerShell 將 VPN 閘道連線至多個內部部署原則式 VPN 裝置](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="c1f00-123">Refer to [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="c1f00-124"><a name="resize"></a>調整閘道 SKU 的大小</span><span class="sxs-lookup"><span data-stu-id="c1f00-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="c1f00-125">您可以調整 VpnGw1、VpnGw2 和 VpnGw3 SKU 之間的大小。</span><span class="sxs-lookup"><span data-stu-id="c1f00-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="c1f00-126">使用舊式閘道 SKU 時，您可以在基本、標準和高效能 SKU 之間調整大小。</span><span class="sxs-lookup"><span data-stu-id="c1f00-126">When working with the old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="c1f00-127">您**無法**將大小從基本/標準/高效能 SKU 調整為新的 VpnGw1/VpnGw2/VpnGw3 SKU。</span><span class="sxs-lookup"><span data-stu-id="c1f00-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs to the new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="c1f00-128">您反而必須[移轉](#migrate)至新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="c1f00-128">You must, instead, [migrate](#migrate) to the new SKUs.</span></span>

###  <span data-ttu-id="c1f00-129"><a name="migrate"></a>從舊式 SKU 移轉至新的 SKU</span><span class="sxs-lookup"><span data-stu-id="c1f00-129"><a name="migrate"></a>Migrating from old SKUs to the new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
