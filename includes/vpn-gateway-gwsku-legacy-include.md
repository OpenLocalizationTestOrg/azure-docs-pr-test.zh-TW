<span data-ttu-id="4d692-101">hello 舊版 （舊） VPN 閘道 Sku 為：</span><span class="sxs-lookup"><span data-stu-id="4d692-101">hello legacy (old) VPN gateway SKUs are:</span></span>

* <span data-ttu-id="4d692-102">基本</span><span class="sxs-lookup"><span data-stu-id="4d692-102">Basic</span></span>
* <span data-ttu-id="4d692-103">標準</span><span class="sxs-lookup"><span data-stu-id="4d692-103">Standard</span></span>
* <span data-ttu-id="4d692-104">高效能</span><span class="sxs-lookup"><span data-stu-id="4d692-104">HighPerformance</span></span>

<span data-ttu-id="4d692-105">VPN 閘道不使用 hello UltraPerformance 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="4d692-105">VPN Gateway does not use hello UltraPerformance gateway SKU.</span></span> <span data-ttu-id="4d692-106">Hello UltraPerformance SKU 的相關資訊，請參閱 hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md)文件。</span><span class="sxs-lookup"><span data-stu-id="4d692-106">For information about hello UltraPerformance SKU, see hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.</span></span>

<span data-ttu-id="4d692-107">當使用 hello 舊版 Sku，請考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4d692-107">When working with hello legacy SKUs, consider hello following:</span></span>

* <span data-ttu-id="4d692-108">如果您想 toouse PolicyBased VPN 類型時，您必須使用 hello Basic SKU。</span><span class="sxs-lookup"><span data-stu-id="4d692-108">If you want toouse a PolicyBased VPN type, you must use hello Basic SKU.</span></span> <span data-ttu-id="4d692-109">其他所有 SKU 均不支援原則式 VPN (先前稱為靜態路由)。</span><span class="sxs-lookup"><span data-stu-id="4d692-109">PolicyBased VPNs (previously called Static Routing) are not supported on any other SKU.</span></span>
* <span data-ttu-id="4d692-110">在 hello Basic SKU 上不支援 BGP。</span><span class="sxs-lookup"><span data-stu-id="4d692-110">BGP is not supported on hello Basic SKU.</span></span>
* <span data-ttu-id="4d692-111">ExpressRoute VPN 閘道共存 hello Basic SKU 上不支援組態。</span><span class="sxs-lookup"><span data-stu-id="4d692-111">ExpressRoute-VPN Gateway coexist configurations are not supported on hello Basic SKU.</span></span>
* <span data-ttu-id="4d692-112">只有 hello HighPerformance SKU 上可以設定主動-主動 S2S VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="4d692-112">Active-active S2S VPN Gateway connections can be configured on hello HighPerformance SKU only.</span></span>
