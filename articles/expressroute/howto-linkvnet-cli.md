---
title: "將虛擬網路連結到 ExpressRoute 線路：CLI：Azure | Microsoft Docs"
description: "本文件概述要如何使用 Resource Manager 部署模型和 CLI 將虛擬網路 (VNet) 連結到 ExpressRoute 線路。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="4bf7d-103">使用 CLI 將虛擬網路連線到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="4bf7d-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="4bf7d-104">本文可協助您使用 CLI 將虛擬網路 (VNet) 連結到 Azure ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="4bf7d-105">若要使用 Azure CLI 進行連結，您必須使用 Resource Manager 部署模型建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="4bf7d-106">其可以位於相同的訂用帳戶中，或屬於另一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="4bf7d-107">如果您想要使用不同的方法將 VNet 連線到 ExpressRoute 線路，您可以從下列清單選取文章：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4bf7d-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4bf7d-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="4bf7d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bf7d-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="4bf7d-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4bf7d-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="4bf7d-111">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4bf7d-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="4bf7d-112">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="4bf7d-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="4bf7d-113">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="4bf7d-113">Configuration prerequisites</span></span>

* <span data-ttu-id="4bf7d-114">您需要最新版本的命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="4bf7d-115">如需詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="4bf7d-116">開始設定之前，請務必檢閱[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="4bf7d-117">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="4bf7d-118">遵循指示來 [建立 ExpressRoute 線路](howto-circuit-cli.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="4bf7d-119">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="4bf7d-120">請參閱 [設定路由](howto-routing-cli.md) 一文，以取得路由指示。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="4bf7d-121">確定已設定 Azure 私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="4bf7d-122">已開啟您的網路與 Microsoft 之間的 BGP 對等互連，讓您可以啟用端對端連線。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="4bf7d-123">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="4bf7d-124">請遵循指示[為 ExpressRoute 設定虛擬網路閘道](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="4bf7d-125">請務必使用 `--gateway-type ExpressRoute`。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="4bf7d-126">您最多可以將 10 個虛擬網路連結至標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="4bf7d-127">在使用標準 ExpressRoute 電路時，所有虛擬網路都必須位於相同的地理政治區域內。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="4bf7d-128">如果您已啟用 ExpressRoute 進階附加元件，則可連結 ExpressRoute 線路的地理政治區域以外的虛擬網路，或是將大量的虛擬網路連線到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="4bf7d-129">如需有關進階附加元件的詳細資訊，請參閱[常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="4bf7d-130">將相同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="4bf7d-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="4bf7d-131">您可以使用範例，將虛擬網路閘道連線到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="4bf7d-132">執行命令之前，請確定您已建立虛擬網路閘道，並準備好進行連結。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="4bf7d-133">將不同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="4bf7d-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="4bf7d-134">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="4bf7d-135">下圖顯示簡單的圖解，示範多個訂用帳戶共用 ExpressRoute 線路的方式。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="4bf7d-136">大型雲端內的每個較小型雲端，會用來代表屬於組織內不同部門的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="4bf7d-137">組織內的每個部門都可以使用自己的訂用帳戶來部署它們的服務，但可共用單一 ExpressRoute 線路，以連接回內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="4bf7d-138">單一部門 (在此範例中：IT) 可以擁有 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="4bf7d-139">組織內的其他訂用帳戶可以使用 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="4bf7d-140">ExpressRoute 線路擁有者需支付專用線路的連線和頻寬費用。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="4bf7d-141">所有虛擬網路都會共用相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="4bf7d-143">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="4bf7d-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="4bf7d-144">「線路擁有者」是 ExpressRoute 線路資源的已授權「進階使用者」。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="4bf7d-145">線路擁有者能夠建立可由「線路使用者」兌換的授權。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="4bf7d-146">線路使用者是虛擬網路閘道的擁有者，與 ExpressRoute 線路位於不同的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="4bf7d-147">線路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="4bf7d-148">線路擁有者能夠隨時修改及撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="4bf7d-149">撤銷授權時，在存取權遭到撤銷的訂用帳戶中，所有連結連線均會遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="4bf7d-150">線路擁有者作業</span><span class="sxs-lookup"><span data-stu-id="4bf7d-150">Circuit Owner operations</span></span>

<span data-ttu-id="4bf7d-151">**建立授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-151">**To create an authorization**</span></span>

<span data-ttu-id="4bf7d-152">線路擁有者會建立授權，這會建立授權金鑰讓線路使用者可用以將其虛擬網路閘道連線到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="4bf7d-153">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="4bf7d-154">下列範例示範如何建立授權：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="4bf7d-155">回應包含授權金鑰和狀態：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="4bf7d-156">**檢閱授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-156">**To review authorizations**</span></span>

<span data-ttu-id="4bf7d-157">線路擁有者可以透過執行下列範例，檢閱特定線路上發出的所有授權：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="4bf7d-158">**新增授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-158">**To add authorizations**</span></span>

<span data-ttu-id="4bf7d-159">線路擁有者可以使用下列範例來新增授權：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="4bf7d-160">**刪除授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-160">**To delete authorizations**</span></span>

<span data-ttu-id="4bf7d-161">線路擁有者可以透過執行下列範例來撤銷/刪除使用者的授權：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="4bf7d-162">線路使用者作業</span><span class="sxs-lookup"><span data-stu-id="4bf7d-162">Circuit User operations</span></span>

<span data-ttu-id="4bf7d-163">線路使用者需要具備對等識別碼以及線路擁有者所提供的授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="4bf7d-164">授權金鑰是 GUID。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="4bf7d-165">**兌換連線授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="4bf7d-166">線路使用者可以執行下列範例來兌換連結授權：</span><span class="sxs-lookup"><span data-stu-id="4bf7d-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="4bf7d-167">**釋出連線授權**</span><span class="sxs-lookup"><span data-stu-id="4bf7d-167">**To release a connection authorization**</span></span>

<span data-ttu-id="4bf7d-168">您可以藉由刪除將 ExpressRoute 線路連結到虛擬網路的連線來釋出授權。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bf7d-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bf7d-169">Next steps</span></span>

<span data-ttu-id="4bf7d-170">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="4bf7d-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>