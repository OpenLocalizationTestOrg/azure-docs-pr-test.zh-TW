<span data-ttu-id="81733-101">您必須建立 VNet 和閘道子網路，才能進行下列工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="81733-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="81733-102">請參閱 hello 文章[設定虛擬網路使用 hello 傳統入口網站](../articles/expressroute/expressroute-howto-vnet-portal-classic.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="81733-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="81733-103">新增閘道</span><span class="sxs-lookup"><span data-stu-id="81733-103">Add a gateway</span></span>
<span data-ttu-id="81733-104">使用以下 toocreate 閘道 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="81733-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="81733-105">是確定 toosubstitute 自己所需的任何值。</span><span class="sxs-lookup"><span data-stu-id="81733-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="81733-106">確認已建立 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="81733-106">Verify hello gateway was created</span></span>
<span data-ttu-id="81733-107">已建立下列 hello 閘道的 tooverify use hello 命令。</span><span class="sxs-lookup"><span data-stu-id="81733-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="81733-108">此命令也會擷取 hello 閘道識別碼，您需要進行其他作業。</span><span class="sxs-lookup"><span data-stu-id="81733-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="81733-109">調整閘道器大小</span><span class="sxs-lookup"><span data-stu-id="81733-109">Resize a gateway</span></span>
<span data-ttu-id="81733-110">有幾個 [閘道 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="81733-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="81733-111">您可以使用下列隨時命令 toochange hello 閘道 SKU 的 hello。</span><span class="sxs-lookup"><span data-stu-id="81733-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81733-112">此命令不適用於 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="81733-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="81733-113">toochange 閘道 tooan UltraPerformance 閘道，先移除現有的 ExpressRoute 閘道的 hello，然後再建立新的 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="81733-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="81733-114">toodowngrade UltraPerformance 閘道，從您的閘道先移除 hello UltraPerformance 閘道，然後再建立新的閘道。</span><span class="sxs-lookup"><span data-stu-id="81733-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="81733-115">移除閘道器</span><span class="sxs-lookup"><span data-stu-id="81733-115">Remove a gateway</span></span>
<span data-ttu-id="81733-116">使用以下 tooremove 閘道 hello 命令</span><span class="sxs-lookup"><span data-stu-id="81733-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>