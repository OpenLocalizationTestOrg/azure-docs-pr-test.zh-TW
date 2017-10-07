---
title: "虛擬網路 tooan ExpressRoute 電路的連結： PowerShell: Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路使用 hello Resource Manager 部署模型和 PowerShell 的方式。"
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="56488-103">連接虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="56488-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56488-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="56488-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="56488-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56488-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="56488-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56488-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="56488-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="56488-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="56488-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="56488-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="56488-109">這篇文章可協助您使用 hello Resource Manager 部署模型和 PowerShell 連結虛擬網路 (Vnet) tooAzure ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="56488-110">虛擬網路可以 hello 中相同的訂用帳戶或其他訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="56488-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="56488-111">本文也會顯示如何 tooupdate 虛擬網路連結。</span><span class="sxs-lookup"><span data-stu-id="56488-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="56488-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="56488-112">Before you begin</span></span>
* <span data-ttu-id="56488-113">安裝 hello hello Azure PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="56488-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="56488-114">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="56488-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="56488-115">檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="56488-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="56488-116">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="56488-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="56488-117">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和已啟用連線提供者的 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="56488-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="56488-118">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="56488-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="56488-119">請參閱 hello[設定路由](expressroute-howto-routing-arm.md)路由指示的發行項。</span><span class="sxs-lookup"><span data-stu-id="56488-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="56488-120">請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。</span><span class="sxs-lookup"><span data-stu-id="56488-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="56488-121">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="56488-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="56488-122">請依照下列指示 hello 太[建立 expressroute 的虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="56488-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="56488-123">Expressroute 的虛擬網路閘道使用 hello gatewaytype 的授權 'ExpressRoute'，不是 VPN。</span><span class="sxs-lookup"><span data-stu-id="56488-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="56488-124">您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="56488-125">所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="56488-126">您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目，如果啟用 hello ExpressRoute premium add-on。</span><span class="sxs-lookup"><span data-stu-id="56488-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="56488-127">檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="56488-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="56488-128">連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路</span><span class="sxs-lookup"><span data-stu-id="56488-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="56488-129">您可以使用下列 cmdlet 的 hello 連接虛擬網路閘道 tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="56488-130">請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56488-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="56488-131">在不同的訂用帳戶 tooa 電路的虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="56488-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="56488-132">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="56488-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="56488-133">hello 遵循圖顯示的簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56488-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="56488-134">Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56488-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="56488-135">每個 hello hello 組織內的部門可以使用自己的訂用帳戶部署其服務-但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="56488-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="56488-136">單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="56488-137">Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="56488-138">Hello ExpressRoute 電路的連線和頻寬費用將會套用的 toohello 訂用帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="56488-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="56488-139">所有虛擬網路共用 hello 相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="56488-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="56488-141">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="56488-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="56488-142">hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。</span><span class="sxs-lookup"><span data-stu-id="56488-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="56488-143">hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。</span><span class="sxs-lookup"><span data-stu-id="56488-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="56488-144">循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="56488-145">電路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="56488-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="56488-146">hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="56488-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="56488-147">撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結連線。</span><span class="sxs-lookup"><span data-stu-id="56488-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="56488-148">循環擁有者作業</span><span class="sxs-lookup"><span data-stu-id="56488-148">Circuit owner operations</span></span>

<span data-ttu-id="56488-149">**toocreate 授權**</span><span class="sxs-lookup"><span data-stu-id="56488-149">**toocreate an authorization**</span></span>

<span data-ttu-id="56488-150">hello 電路擁有者建立的授權。</span><span class="sxs-lookup"><span data-stu-id="56488-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="56488-151">這會導致 hello 建立的授權金鑰可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="56488-152">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="56488-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="56488-153">下列指令程式的程式碼片段說明如何 hello toocreate 授權：</span><span class="sxs-lookup"><span data-stu-id="56488-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="56488-154">hello 授權金鑰和狀態，將會包含 hello 回應 toothis:</span><span class="sxs-lookup"><span data-stu-id="56488-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="56488-155">**tooreview 授權**</span><span class="sxs-lookup"><span data-stu-id="56488-155">**tooreview authorizations**</span></span>

<span data-ttu-id="56488-156">hello 電路擁有者可以檢閱由執行下列 cmdlet 的 hello 特定電路發出的所有授權：</span><span class="sxs-lookup"><span data-stu-id="56488-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="56488-157">**tooadd 授權**</span><span class="sxs-lookup"><span data-stu-id="56488-157">**tooadd authorizations**</span></span>

<span data-ttu-id="56488-158">hello 電路擁有者可以使用下列 cmdlet 的 hello 來新增授權：</span><span class="sxs-lookup"><span data-stu-id="56488-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="56488-159">**toodelete 授權**</span><span class="sxs-lookup"><span data-stu-id="56488-159">**toodelete authorizations**</span></span>

<span data-ttu-id="56488-160">hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="56488-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="56488-161">循環使用者作業</span><span class="sxs-lookup"><span data-stu-id="56488-161">Circuit user operations</span></span>

<span data-ttu-id="56488-162">hello 電路使用者需要 hello 對等識別碼與 hello 電路擁有者從授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="56488-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="56488-163">hello 授權金鑰是 GUID。</span><span class="sxs-lookup"><span data-stu-id="56488-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="56488-164">對等識別碼可以檢查從 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="56488-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="56488-165">**tooredeem 連線授權**</span><span class="sxs-lookup"><span data-stu-id="56488-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="56488-166">hello 循環使用者可以執行下列 cmdlet tooredeem hello 連結授權：</span><span class="sxs-lookup"><span data-stu-id="56488-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="56488-167">**toorelease 連線授權**</span><span class="sxs-lookup"><span data-stu-id="56488-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="56488-168">您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。</span><span class="sxs-lookup"><span data-stu-id="56488-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="56488-169">修改虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="56488-169">Modify a virtual network connection</span></span>
<span data-ttu-id="56488-170">您可以更新虛擬網路連線的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="56488-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="56488-171">**tooupdate hello 連接權數**</span><span class="sxs-lookup"><span data-stu-id="56488-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="56488-172">您的虛擬網路可以連接的 toomultiple ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="56488-173">您可能會收到相同的前置詞的 hello 從多個 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="56488-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="56488-174">您可以變更的 toochoose 哪些連線 toosend 流量目的地為此前置詞， *RoutingWeight*的連線。</span><span class="sxs-lookup"><span data-stu-id="56488-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="56488-175">流量將會傳送 hello 連線以最高的 hello *RoutingWeight*。</span><span class="sxs-lookup"><span data-stu-id="56488-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="56488-176">hello 範圍*RoutingWeight*是 0 too32000。</span><span class="sxs-lookup"><span data-stu-id="56488-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="56488-177">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="56488-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56488-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56488-178">Next steps</span></span>
<span data-ttu-id="56488-179">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="56488-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
