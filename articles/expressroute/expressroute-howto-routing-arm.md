---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： 資源管理員： PowerShell: Azure |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="a56c1-104">使用 PowerShell 建立和修改 ExpressRoute 線路的對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="a56c1-105">這篇文章可協助您建立及管理在 hello 資源管理員部署模型中使用 PowerShell 的 ExpressRoute 電路的路由組態。</span><span class="sxs-lookup"><span data-stu-id="a56c1-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="a56c1-106">您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="a56c1-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="a56c1-107">如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：</span><span class="sxs-lookup"><span data-stu-id="a56c1-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a56c1-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a56c1-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="a56c1-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a56c1-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="a56c1-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a56c1-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="a56c1-111">視訊 - 私用對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="a56c1-112">視訊 - 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="a56c1-113">視訊 - Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="a56c1-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="a56c1-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="a56c1-115">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="a56c1-115">Configuration prerequisites</span></span>

* <span data-ttu-id="a56c1-116">您將需要 hello 的 hello Azure 資源管理員 PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="a56c1-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="a56c1-117">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="a56c1-118">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="a56c1-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="a56c1-119">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="a56c1-120">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="a56c1-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="a56c1-121">hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet，在本文中的佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="a56c1-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="a56c1-122">這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。</span><span class="sxs-lookup"><span data-stu-id="a56c1-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="a56c1-123">如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="a56c1-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a56c1-124">我們目前不會進行通告透過 hello 服務管理入口網站的服務提供者所設定的對等互連。</span><span class="sxs-lookup"><span data-stu-id="a56c1-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="a56c1-125">我們正努力在近期推出這項功能。</span><span class="sxs-lookup"><span data-stu-id="a56c1-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="a56c1-126">設定 BGP 對等互連之前，請洽詢您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="a56c1-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="a56c1-127">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="a56c1-128">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="a56c1-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="a56c1-129">不過，您必須確定您完成每個對等互連一次一個的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a56c1-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="a56c1-130">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="a56c1-130">Azure private peering</span></span>

<span data-ttu-id="a56c1-131">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。</span><span class="sxs-lookup"><span data-stu-id="a56c1-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="a56c1-132">toocreate Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="a56c1-133">匯入 ExpressRoute hello PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="a56c1-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="a56c1-134">您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a56c1-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="a56c1-135">您必須以系統管理員身分 toorun PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a56c1-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="a56c1-136">匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="a56c1-137">您也可以匯入選取的模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="a56c1-138">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="a56c1-139">選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="a56c1-140">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="a56c1-141">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="a56c1-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="a56c1-142">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="a56c1-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="a56c1-143">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="a56c1-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="a56c1-144">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="a56c1-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="a56c1-145">請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。</span><span class="sxs-lookup"><span data-stu-id="a56c1-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="a56c1-146">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="a56c1-147">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="a56c1-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="a56c1-148">設定 Azure 私用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a56c1-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="a56c1-149">請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="a56c1-150">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="a56c1-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="a56c1-151">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="a56c1-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="a56c1-152">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="a56c1-153">hello 子網路不能保留的虛擬網路的任何位址空間的一部分。</span><span class="sxs-lookup"><span data-stu-id="a56c1-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="a56c1-154">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="a56c1-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="a56c1-155">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="a56c1-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="a56c1-156">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-156">AS number for peering.</span></span> <span data-ttu-id="a56c1-157">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="a56c1-158">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="a56c1-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="a56c1-159">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="a56c1-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="a56c1-160">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="a56c1-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="a56c1-161">使用下列範例 tooconfigure Azure 私用對等互連，為您的電路的 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="a56c1-162">如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="a56c1-163">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="a56c1-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="a56c1-164">tooview Azure 私用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="a56c1-164">tooview Azure private peering details</span></span>

<span data-ttu-id="a56c1-165">您可以使用下列範例中的 hello，以取得設定的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="a56c1-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="a56c1-166">tooupdate Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="a56c1-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="a56c1-167">您可以更新使用下列範例中的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="a56c1-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="a56c1-168">在此範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="a56c1-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="a56c1-169">toodelete Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-169">toodelete Azure private peering</span></span>

<span data-ttu-id="a56c1-170">您可以執行下列範例中的 hello 來移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="a56c1-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="a56c1-171">您必須確定所有虛擬網路，然後再執行此範例會從 hello ExpressRoute 電路取消連結。</span><span class="sxs-lookup"><span data-stu-id="a56c1-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="a56c1-172">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="a56c1-172">Azure public peering</span></span>

<span data-ttu-id="a56c1-173">本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。</span><span class="sxs-lookup"><span data-stu-id="a56c1-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="a56c1-174">toocreate Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="a56c1-175">匯入 ExpressRoute hello PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="a56c1-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="a56c1-176">您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a56c1-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="a56c1-177">您必須以系統管理員身分 toorun PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a56c1-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="a56c1-178">匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="a56c1-179">您也可以匯入選取的模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="a56c1-180">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="a56c1-181">選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="a56c1-182">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="a56c1-183">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="a56c1-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="a56c1-184">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="a56c1-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="a56c1-185">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="a56c1-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="a56c1-186">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="a56c1-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="a56c1-187">請檢查已佈建並也啟用 hello ExpressRoute 電路 tooensure。</span><span class="sxs-lookup"><span data-stu-id="a56c1-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="a56c1-188">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="a56c1-189">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="a56c1-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="a56c1-190">設定 Azure 公用對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a56c1-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="a56c1-191">請確定您擁有 hello 繼續接下來，下列資訊。</span><span class="sxs-lookup"><span data-stu-id="a56c1-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="a56c1-192">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="a56c1-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="a56c1-193">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="a56c1-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="a56c1-194">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="a56c1-195">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="a56c1-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="a56c1-196">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="a56c1-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="a56c1-197">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="a56c1-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="a56c1-198">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-198">AS number for peering.</span></span> <span data-ttu-id="a56c1-199">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="a56c1-200">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="a56c1-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="a56c1-201">執行下列範例 tooconfigure Azure 公用對等互連，為您的電路的 hello</span><span class="sxs-lookup"><span data-stu-id="a56c1-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="a56c1-202">如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="a56c1-203">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="a56c1-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="a56c1-204">tooview Azure 公用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="a56c1-204">tooview Azure public peering details</span></span>

<span data-ttu-id="a56c1-205">就可以使用下列 cmdlet 的 hello 設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="a56c1-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="a56c1-206">tooupdate Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="a56c1-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="a56c1-207">您可以更新使用下列範例中的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="a56c1-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="a56c1-208">在此範例中，從 200 too600 正在更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="a56c1-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="a56c1-209">toodelete Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-209">toodelete Azure public peering</span></span>

<span data-ttu-id="a56c1-210">您可以執行下列範例中的 hello 來移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="a56c1-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="a56c1-211">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-211">Microsoft peering</span></span>

<span data-ttu-id="a56c1-212">本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。</span><span class="sxs-lookup"><span data-stu-id="a56c1-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a56c1-213">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="a56c1-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="a56c1-214">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="a56c1-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="a56c1-215">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="a56c1-216">toocreate Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="a56c1-217">匯入 ExpressRoute hello PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="a56c1-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="a56c1-218">您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a56c1-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="a56c1-219">您必須以系統管理員身分 toorun PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a56c1-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="a56c1-220">匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="a56c1-221">您也可以匯入選取的模組 hello 已知的語意版本範圍內。</span><span class="sxs-lookup"><span data-stu-id="a56c1-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="a56c1-222">登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="a56c1-223">選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a56c1-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="a56c1-224">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="a56c1-225">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="a56c1-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="a56c1-226">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="a56c1-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="a56c1-227">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="a56c1-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="a56c1-228">不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。</span><span class="sxs-lookup"><span data-stu-id="a56c1-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="a56c1-229">請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。</span><span class="sxs-lookup"><span data-stu-id="a56c1-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="a56c1-230">下列範例使用 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="a56c1-231">hello 回應是類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="a56c1-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="a56c1-232">設定 Microsoft 對等互連 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a56c1-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="a56c1-233">請確定您擁有 hello 下列資訊才能繼續。</span><span class="sxs-lookup"><span data-stu-id="a56c1-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="a56c1-234">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="a56c1-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="a56c1-235">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="a56c1-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="a56c1-236">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="a56c1-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="a56c1-237">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="a56c1-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="a56c1-238">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="a56c1-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="a56c1-239">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="a56c1-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="a56c1-240">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-240">AS number for peering.</span></span> <span data-ttu-id="a56c1-241">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="a56c1-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="a56c1-242">通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a56c1-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="a56c1-243">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="a56c1-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="a56c1-244">如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="a56c1-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="a56c1-245">這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="a56c1-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="a56c1-246">**選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。</span><span class="sxs-lookup"><span data-stu-id="a56c1-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="a56c1-247">路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。</span><span class="sxs-lookup"><span data-stu-id="a56c1-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="a56c1-248">**選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="a56c1-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="a56c1-249">使用下列範例 tooconfigure Microsoft 對等互連為您的電路的 hello:</span><span class="sxs-lookup"><span data-stu-id="a56c1-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="a56c1-250">tooget Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="a56c1-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="a56c1-251">就可以使用下列範例中的 hello 設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="a56c1-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="a56c1-252">tooupdate Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="a56c1-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="a56c1-253">您可以更新使用下列範例中的 hello hello 設定的任何部分：</span><span class="sxs-lookup"><span data-stu-id="a56c1-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="a56c1-254">toodelete Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="a56c1-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="a56c1-255">您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定：</span><span class="sxs-lookup"><span data-stu-id="a56c1-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="a56c1-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a56c1-256">Next steps</span></span>

<span data-ttu-id="a56c1-257">下一步，[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="a56c1-258">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="a56c1-259">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="a56c1-260">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a56c1-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
