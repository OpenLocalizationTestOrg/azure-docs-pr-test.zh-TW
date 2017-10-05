---
title: "將虛擬網路連結到 ExpressRoute 線路：PowerShell：Azure | Microsoft Docs"
description: "本文提供以下內容的概觀：如何使用 Resource Manager 部署模型和 PowerShell 將虛擬網路 (VNet) 連結到 ExpressRoute 線路。"
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
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="4fa8d-103">將虛擬網路連線到 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="4fa8d-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fa8d-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4fa8d-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="4fa8d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fa8d-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="4fa8d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4fa8d-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="4fa8d-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4fa8d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="4fa8d-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="4fa8d-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="4fa8d-109">本文會協助您使用 Resource Manager 部署模型和 PowerShell，將虛擬網路 (VNet) 連結到 Azure ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="4fa8d-110">虛擬網路可以位於相同的訂用帳戶中，或屬於另一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="4fa8d-111">本文也會示範如何更新虛擬網路連結。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4fa8d-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="4fa8d-112">Before you begin</span></span>
* <span data-ttu-id="4fa8d-113">安裝最新版的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="4fa8d-114">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="4fa8d-115">開始設定之前，請先檢閱[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)及[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="4fa8d-116">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="4fa8d-117">遵循指示來 [建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="4fa8d-118">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="4fa8d-119">請參閱 [設定路由](expressroute-howto-routing-arm.md) 一文，以取得路由指示。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="4fa8d-120">請確定已設定 Azure 私用對等，且已開啟您的網路與 Microsoft 之間的 BGP 對等，讓您可以啟用端對端連線。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="4fa8d-121">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="4fa8d-122">請依照指示[為 ExpressRoute 建立虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="4fa8d-123">ExpressRoute 的虛擬網路閘道會使用 GatewayType 'ExpressRoute'，而不是 VPN。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="4fa8d-124">您最多可以將 10 個虛擬網路連結至標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="4fa8d-125">在使用標準 ExpressRoute 電路時，所有虛擬網路都必須位於相同的地理政治區域內。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="4fa8d-126">如果您已啟用 ExpressRoute 高階附加元件，則可連結 ExpressRoute 電路的地理政治區域以外的虛擬網路，或是將大量的虛擬網路連接到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="4fa8d-127">如需高階附加元件的詳細資訊，請參閱 [常見問題集](expressroute-faqs.md) 。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="4fa8d-128">將相同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="4fa8d-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="4fa8d-129">您可以使用下列 Cmdlet，將虛擬網路閘道連結到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="4fa8d-130">執行 Cmdlet 之前，請確定您已建立虛擬網路閘道，並準備好進行連結。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="4fa8d-131">將不同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="4fa8d-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="4fa8d-132">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="4fa8d-133">下圖顯示簡單的圖解，示範多個訂用帳戶共用 ExpressRoute 線路的方式。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="4fa8d-134">大型雲端內的每個較小型雲端，會用來代表屬於組織內不同部門的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="4fa8d-135">組織內的每個部門都可以使用自己的訂用帳戶來部署它們的服務，但可共用單一 ExpressRoute 線路，以連接回內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="4fa8d-136">單一部門 (在此範例中：IT) 可以擁有 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="4fa8d-137">組織內的其他訂用帳戶可以使用 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="4fa8d-138">訂用帳戶擁有者需支付 ExpressRoute 循環的連線和頻寬費用。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="4fa8d-139">所有虛擬網路都會共用相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="4fa8d-141">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="4fa8d-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="4fa8d-142">「線路擁有者」是 ExpressRoute 線路資源的已授權「進階使用者」。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="4fa8d-143">電路擁有者能夠建立可由「電路使用者」兌換的授權。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="4fa8d-144">線路使用者是虛擬網路閘道的擁有者，與 ExpressRoute 線路位於不同的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="4fa8d-145">電路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="4fa8d-146">電路擁有者能夠隨時修改及撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="4fa8d-147">如果撤銷授權，則在存取權遭撤銷的訂用帳戶中，所有連結連線均會被刪除。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="4fa8d-148">循環擁有者作業</span><span class="sxs-lookup"><span data-stu-id="4fa8d-148">Circuit owner operations</span></span>

<span data-ttu-id="4fa8d-149">**建立授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-149">**To create an authorization**</span></span>

<span data-ttu-id="4fa8d-150">電路擁有者會建立授權。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="4fa8d-151">這樣即會建立授權金鑰，讓電路使用者可用來將其虛擬網路閘道連接到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="4fa8d-152">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="4fa8d-153">下列 Cmdlet 程式碼片段示範如何建立授權：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="4fa8d-154">對此動作的回應將包含授權金鑰和狀態：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="4fa8d-155">**檢閱授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-155">**To review authorizations**</span></span>

<span data-ttu-id="4fa8d-156">線路擁有者可以藉由執行下列 Cmdlet，來檢閱特定線路上發出的所有授權：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="4fa8d-157">**新增授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-157">**To add authorizations**</span></span>

<span data-ttu-id="4fa8d-158">線路擁有者可以使用下列 Cmdlet 來新增授權：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="4fa8d-159">**刪除授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-159">**To delete authorizations**</span></span>

<span data-ttu-id="4fa8d-160">線路擁有者可以使用下列 Cmdlet 來撤銷/刪除使用者的授權：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="4fa8d-161">循環使用者作業</span><span class="sxs-lookup"><span data-stu-id="4fa8d-161">Circuit user operations</span></span>

<span data-ttu-id="4fa8d-162">電路使用者需要具備對等識別碼以及電路擁有者所提供的授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="4fa8d-163">授權金鑰是 GUID。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="4fa8d-164">您可以從下列命令檢查「對等識別碼」：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="4fa8d-165">**兌換連線授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="4fa8d-166">線路使用者可以執行下列 Cmdlet 來兌換連結授權：</span><span class="sxs-lookup"><span data-stu-id="4fa8d-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="4fa8d-167">**釋出連線授權**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-167">**To release a connection authorization**</span></span>

<span data-ttu-id="4fa8d-168">您可以藉由刪除將 ExpressRoute 線路連結到虛擬網路的連線來釋出授權。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="4fa8d-169">修改虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="4fa8d-169">Modify a virtual network connection</span></span>
<span data-ttu-id="4fa8d-170">您可以更新虛擬網路連線的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="4fa8d-171">**更新連線權數**</span><span class="sxs-lookup"><span data-stu-id="4fa8d-171">**To update the connection weight**</span></span>

<span data-ttu-id="4fa8d-172">您的虛擬網路可以連接到多個 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="4fa8d-173">您可能會收到來自多個 ExpressRoute 線路的相同前置詞。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="4fa8d-174">若要選擇要使用哪一個連線來傳送目的為此前置詞的流量，您可以變更連線的 *RoutingWeight*。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="4fa8d-175">流量將透過具有最高 *RoutingWeight* 的連線來傳送。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="4fa8d-176">*RoutingWeight* 的範圍是從 0 到 32000。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="4fa8d-177">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fa8d-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fa8d-178">Next steps</span></span>
<span data-ttu-id="4fa8d-179">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="4fa8d-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
