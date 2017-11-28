<span data-ttu-id="4a636-101">舊版 (舊式) VPN 閘道 SKU 如下：</span><span class="sxs-lookup"><span data-stu-id="4a636-101">The legacy (old) VPN gateway SKUs are:</span></span>

* <span data-ttu-id="4a636-102">基本</span><span class="sxs-lookup"><span data-stu-id="4a636-102">Basic</span></span>
* <span data-ttu-id="4a636-103">標準</span><span class="sxs-lookup"><span data-stu-id="4a636-103">Standard</span></span>
* <span data-ttu-id="4a636-104">高效能</span><span class="sxs-lookup"><span data-stu-id="4a636-104">HighPerformance</span></span>

<span data-ttu-id="4a636-105">VPN 閘道不會使用 UltraPerformance 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="4a636-105">VPN Gateway does not use the UltraPerformance gateway SKU.</span></span> <span data-ttu-id="4a636-106">如需 UltraPerformance SKU 的相關資訊，請參閱 [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="4a636-106">For information about the UltraPerformance SKU, see the [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.</span></span>

<span data-ttu-id="4a636-107">使用舊版 SKU 時，請考慮下列各項：</span><span class="sxs-lookup"><span data-stu-id="4a636-107">When working with the legacy SKUs, consider the following:</span></span>

* <span data-ttu-id="4a636-108">如果您想要使用原則式 VPN 類型，您必須使用基本 SKU。</span><span class="sxs-lookup"><span data-stu-id="4a636-108">If you want to use a PolicyBased VPN type, you must use the Basic SKU.</span></span> <span data-ttu-id="4a636-109">其他所有 SKU 均不支援原則式 VPN (先前稱為靜態路由)。</span><span class="sxs-lookup"><span data-stu-id="4a636-109">PolicyBased VPNs (previously called Static Routing) are not supported on any other SKU.</span></span>
* <span data-ttu-id="4a636-110">基本 SKU 不支援 BGP。</span><span class="sxs-lookup"><span data-stu-id="4a636-110">BGP is not supported on the Basic SKU.</span></span>
* <span data-ttu-id="4a636-111">基本 SKU 不支援 ExpressRoute-VPN 閘道共存組態。</span><span class="sxs-lookup"><span data-stu-id="4a636-111">ExpressRoute-VPN Gateway coexist configurations are not supported on the Basic SKU.</span></span>
* <span data-ttu-id="4a636-112">僅可以在高效能 SKU 上設定主動-主動 S2S VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="4a636-112">Active-active S2S VPN Gateway connections can be configured on the HighPerformance SKU only.</span></span>