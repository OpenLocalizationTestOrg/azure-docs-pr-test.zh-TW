> [!NOTE]
> * <span data-ttu-id="e4435-101">當移轉從舊的 SKU tooa，hello VPN 閘道的公用 IP 位址將會變更新 SKU。</span><span class="sxs-lookup"><span data-stu-id="e4435-101">hello VPN gateway Public IP address will change when migrating from an old SKU tooa new SKU.</span></span>
> * <span data-ttu-id="e4435-102">您無法移轉傳統 VPN 閘道 toohello 新 Sku。</span><span class="sxs-lookup"><span data-stu-id="e4435-102">You can't migrate classic VPN gateways toohello new SKUs.</span></span> <span data-ttu-id="e4435-103">傳統 VPN 閘道可以只使用 hello 傳統的 （舊） Sku。</span><span class="sxs-lookup"><span data-stu-id="e4435-103">Classic VPN gateways can only use hello legacy (old) SKUs.</span></span>
> 

<span data-ttu-id="e4435-104">您不可以調整您的 Azure VPN 閘道之間 hello 舊的 Sku 和 hello 新 SKU 系列。</span><span class="sxs-lookup"><span data-stu-id="e4435-104">You can't resize your Azure VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="e4435-105">如果您有使用 hello 的 hello Sku 的舊版本的 VPN 閘道 hello Resource Manager 部署模型中，您可以移轉 toohello 新 Sku。</span><span class="sxs-lookup"><span data-stu-id="e4435-105">If you have VPN gateways in hello Resource Manager deployment model that are using hello older version of hello SKUs, you can migrate toohello new SKUs.</span></span> <span data-ttu-id="e4435-106">toomigrate，刪除虛擬網路，hello 現有的 VPN 閘道，然後建立一個新。</span><span class="sxs-lookup"><span data-stu-id="e4435-106">toomigrate, you delete hello existing VPN gateway for your virtual network, then create a new one.</span></span>

<span data-ttu-id="e4435-107">移轉工作流程：</span><span class="sxs-lookup"><span data-stu-id="e4435-107">Migration workflow:</span></span>

1. <span data-ttu-id="e4435-108">移除任何連線 toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="e4435-108">Remove any connections toohello virtual network gateway.</span></span>
2. <span data-ttu-id="e4435-109">刪除 hello 舊的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="e4435-109">Delete hello old VPN gateway.</span></span>
3. <span data-ttu-id="e4435-110">建立 hello 新的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="e4435-110">Create hello new VPN gateway.</span></span>
4. <span data-ttu-id="e4435-111">更新您的內部部署 VPN 裝置 hello 新 VPN 閘道 IP 位址 （適用於站對站連線）。</span><span class="sxs-lookup"><span data-stu-id="e4435-111">Update your on-premises VPN devices with hello new VPN gateway IP address (for Site-to-Site connections).</span></span>
5. <span data-ttu-id="e4435-112">更新 hello toothis 閘道將會連接任何 VNet 對 VNet 區域網路閘道的閘道 IP 位址值。</span><span class="sxs-lookup"><span data-stu-id="e4435-112">Update hello gateway IP address value for any VNet-to-VNet local network gateways that will connect toothis gateway.</span></span>
6. <span data-ttu-id="e4435-113">下載新的用戶端 VPN 組態封裝 P2S 用戶端透過此 VPN 閘道連線 toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e4435-113">Download new client VPN configuration packages for P2S clients connecting toohello virtual network through this VPN gateway.</span></span>
7. <span data-ttu-id="e4435-114">重新建立 hello 連線 toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="e4435-114">Recreate hello connections toohello virtual network gateway.</span></span>
