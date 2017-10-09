---
title: "虛擬網路 tooan ExpressRoute 電路的連結： CLI: Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路 hello Resource Manager 部署模型和 CLI 所使用的方式。"
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
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="05560-103">連接使用 CLI 的虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="05560-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="05560-104">這篇文章可協助您使用 CLI 的虛擬網路 (Vnet) tooAzure ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="05560-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="05560-105">使用 Azure CLI toolink hello 虛擬網路必須使用 hello Resource Manager 部署模型來建立。</span><span class="sxs-lookup"><span data-stu-id="05560-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="05560-106">它們可以在 hello 是相同的訂用帳戶或其他訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="05560-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="05560-107">如果您想 toouse 不同方法 tooconnect 您 VNet tooan ExpressRoute 循環，您可以從下列清單中的 hello 選取一個發行項：</span><span class="sxs-lookup"><span data-stu-id="05560-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05560-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="05560-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="05560-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05560-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="05560-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05560-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="05560-111">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="05560-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="05560-112">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="05560-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="05560-113">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="05560-113">Configuration prerequisites</span></span>

* <span data-ttu-id="05560-114">您需要 hello hello 命令列介面 (CLI) 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="05560-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="05560-115">如需詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="05560-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="05560-116">您需要 tooreview hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="05560-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="05560-117">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="05560-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="05560-118">請依照下列指示 hello 太[建立 ExpressRoute 電路](howto-circuit-cli.md)和已啟用連線提供者的 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="05560-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="05560-119">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="05560-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="05560-120">請參閱 hello[設定路由](howto-routing-cli.md)路由指示的發行項。</span><span class="sxs-lookup"><span data-stu-id="05560-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="05560-121">確定已設定 Azure 私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="05560-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="05560-122">hello BGP 對等互連網路與 Microsoft 之間必須啟動，讓您可以啟用端對端連線。</span><span class="sxs-lookup"><span data-stu-id="05560-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="05560-123">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="05560-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="05560-124">請依照下列指示 hello 太[設定 expressroute 的虛擬網路閘道](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。</span><span class="sxs-lookup"><span data-stu-id="05560-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="05560-125">要確定 toouse `--gateway-type ExpressRoute`。</span><span class="sxs-lookup"><span data-stu-id="05560-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="05560-126">您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="05560-127">所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="05560-128">如果您啟用 hello ExpressRoute premium 附加元件，您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目。</span><span class="sxs-lookup"><span data-stu-id="05560-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="05560-129">如需 hello premium 附加元件的詳細資訊，請參閱 hello[常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="05560-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="05560-130">連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路</span><span class="sxs-lookup"><span data-stu-id="05560-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="05560-131">您可以藉由使用 hello 範例連接虛擬網路閘道 tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="05560-132">請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="05560-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="05560-133">在不同的訂用帳戶 tooa 電路的虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="05560-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="05560-134">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="05560-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="05560-135">hello 下圖顯示簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05560-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="05560-136">Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05560-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="05560-137">每個 hello hello 組織內的部門可以使用自己的訂用帳戶部署其服務-但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="05560-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="05560-138">單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="05560-139">Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="05560-140">Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。</span><span class="sxs-lookup"><span data-stu-id="05560-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="05560-141">所有虛擬網路共用 hello 相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="05560-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="05560-143">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="05560-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="05560-144">hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。</span><span class="sxs-lookup"><span data-stu-id="05560-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="05560-145">hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。</span><span class="sxs-lookup"><span data-stu-id="05560-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="05560-146">循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="05560-147">線路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="05560-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="05560-148">hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="05560-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="05560-149">授權撤銷時，所有連結連線將會都刪除從 hello 訂用帳戶已撤銷其存取權。</span><span class="sxs-lookup"><span data-stu-id="05560-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="05560-150">線路擁有者作業</span><span class="sxs-lookup"><span data-stu-id="05560-150">Circuit Owner operations</span></span>

<span data-ttu-id="05560-151">**toocreate 授權**</span><span class="sxs-lookup"><span data-stu-id="05560-151">**toocreate an authorization**</span></span>

<span data-ttu-id="05560-152">hello 電路擁有者建立授權，可建立的授權金鑰，可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="05560-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="05560-153">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="05560-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="05560-154">下列範例會示範如何 hello toocreate 授權：</span><span class="sxs-lookup"><span data-stu-id="05560-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="05560-155">hello 回應包含 hello 授權金鑰和狀態：</span><span class="sxs-lookup"><span data-stu-id="05560-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="05560-156">**tooreview 授權**</span><span class="sxs-lookup"><span data-stu-id="05560-156">**tooreview authorizations**</span></span>

<span data-ttu-id="05560-157">hello 電路擁有者可以檢閱執行 hello 下列範例針對特定電路來發出的所有授權：</span><span class="sxs-lookup"><span data-stu-id="05560-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="05560-158">**tooadd 授權**</span><span class="sxs-lookup"><span data-stu-id="05560-158">**tooadd authorizations**</span></span>

<span data-ttu-id="05560-159">hello 電路擁有者可以使用下列範例中的 hello 來新增授權：</span><span class="sxs-lookup"><span data-stu-id="05560-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="05560-160">**toodelete 授權**</span><span class="sxs-lookup"><span data-stu-id="05560-160">**toodelete authorizations**</span></span>

<span data-ttu-id="05560-161">hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="05560-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="05560-162">線路使用者作業</span><span class="sxs-lookup"><span data-stu-id="05560-162">Circuit User operations</span></span>

<span data-ttu-id="05560-163">hello 循環使用者需要 hello 對等識別碼與 hello 電路擁有者從授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="05560-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="05560-164">hello 授權金鑰是 GUID。</span><span class="sxs-lookup"><span data-stu-id="05560-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="05560-165">**tooredeem 連線授權**</span><span class="sxs-lookup"><span data-stu-id="05560-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="05560-166">hello 循環使用者可以執行下列範例 tooredeem hello 連結授權：</span><span class="sxs-lookup"><span data-stu-id="05560-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="05560-167">**toorelease 連線授權**</span><span class="sxs-lookup"><span data-stu-id="05560-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="05560-168">您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。</span><span class="sxs-lookup"><span data-stu-id="05560-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05560-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05560-169">Next steps</span></span>

<span data-ttu-id="05560-170">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="05560-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
