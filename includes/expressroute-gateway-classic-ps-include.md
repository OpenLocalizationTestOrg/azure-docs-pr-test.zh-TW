<span data-ttu-id="2cf81-101">您必須先建立 VNET 和閘道器子網路，才能進行下列工作。</span><span class="sxs-lookup"><span data-stu-id="2cf81-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="2cf81-102">如需詳細資訊，請參閱 [使用傳統入口網站設定虛擬網路](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="2cf81-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="2cf81-103">新增閘道</span><span class="sxs-lookup"><span data-stu-id="2cf81-103">Add a gateway</span></span>
<span data-ttu-id="2cf81-104">使用以下的命令建立閘道器。</span><span class="sxs-lookup"><span data-stu-id="2cf81-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="2cf81-105">所有的值請務必替換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="2cf81-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="2cf81-106">確認已建立閘道</span><span class="sxs-lookup"><span data-stu-id="2cf81-106">Verify the gateway was created</span></span>
<span data-ttu-id="2cf81-107">使用下列命令，確認已建立閘道。</span><span class="sxs-lookup"><span data-stu-id="2cf81-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="2cf81-108">這個命令也會擷取閘道器識別碼，您在其他作業會需要它。</span><span class="sxs-lookup"><span data-stu-id="2cf81-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="2cf81-109">調整閘道器大小</span><span class="sxs-lookup"><span data-stu-id="2cf81-109">Resize a gateway</span></span>
<span data-ttu-id="2cf81-110">有幾個 [閘道 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="2cf81-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="2cf81-111">您可以使用下列命令隨時變更閘道器 SKU。</span><span class="sxs-lookup"><span data-stu-id="2cf81-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cf81-112">此命令不適用於 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="2cf81-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="2cf81-113">若要將您的閘道變更為 UltraPerformance 閘道，請先移除現有的 ExpressRoute 閘道，然後建立新的 UltraPerformance 閘道。</span><span class="sxs-lookup"><span data-stu-id="2cf81-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="2cf81-114">若要從 UltraPerformance 閘道降級您的閘道，請先移除 UltraPerformance 閘道，然後建立新的閘道。</span><span class="sxs-lookup"><span data-stu-id="2cf81-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="2cf81-115">移除閘道器</span><span class="sxs-lookup"><span data-stu-id="2cf81-115">Remove a gateway</span></span>
<span data-ttu-id="2cf81-116">使用以下的命令移除閘道器</span><span class="sxs-lookup"><span data-stu-id="2cf81-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>