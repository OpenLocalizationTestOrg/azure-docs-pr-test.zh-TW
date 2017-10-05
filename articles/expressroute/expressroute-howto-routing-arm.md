---
title: "如何設定 ExpressRoute 線路的路由 (對等互連)：Resource Manager：PowerShell：Azure | Microsoft Docs"
description: "本文將逐步引導您為 ExpressRoute 線路建立和佈建私用、公用及 Microsoft 對等。 本文也示範如何檢查狀態、更新或刪除線路的對等。"
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="046be-104">使用 PowerShell 建立和修改 ExpressRoute 線路的對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="046be-105">本文將協助您使用 PowerShell，在 Resource Manager 部署模型中建立和管理 ExpressRoute 線路的路由設定。</span><span class="sxs-lookup"><span data-stu-id="046be-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="046be-106">您還可以檢查狀態、更新，或是刪除與取消佈建 ExpressRoute 線路的對等互連。</span><span class="sxs-lookup"><span data-stu-id="046be-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="046be-107">如果您想要對線路使用不同的方法，可選取下列清單中的文章：</span><span class="sxs-lookup"><span data-stu-id="046be-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="046be-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="046be-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="046be-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="046be-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="046be-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="046be-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="046be-111">視訊 - 私用對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="046be-112">視訊 - 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="046be-113">視訊 - Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="046be-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="046be-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="046be-115">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="046be-115">Configuration prerequisites</span></span>

* <span data-ttu-id="046be-116">您需要最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="046be-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="046be-117">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="046be-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="046be-118">開始設定之前，請確定您已經檢閱過[必要條件](expressroute-prerequisites.md)頁面、[路由需求](expressroute-routing.md)頁面和[工作流程](expressroute-workflows.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="046be-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="046be-119">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="046be-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="046be-120">繼續之前，請遵循指示來 [建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="046be-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="046be-121">ExpressRoute 線路必須處於已佈建和已啟用狀態，您才能執行本文中的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="046be-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="046be-122">這些指示只適用於由提供第 2 層連線服務的服務提供者所建立的線路。</span><span class="sxs-lookup"><span data-stu-id="046be-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="046be-123">如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="046be-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="046be-124">我們目前不會透過服務管理入口網站來公告服務提供者所設定的對等。</span><span class="sxs-lookup"><span data-stu-id="046be-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="046be-125">我們正努力在近期推出這項功能。</span><span class="sxs-lookup"><span data-stu-id="046be-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="046be-126">設定 BGP 對等互連之前，請洽詢您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="046be-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="046be-127">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="046be-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="046be-128">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="046be-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="046be-129">不過，您必須確定一次只完成一個對等的設定。</span><span class="sxs-lookup"><span data-stu-id="046be-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="046be-130">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="046be-130">Azure private peering</span></span>

<span data-ttu-id="046be-131">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 私用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="046be-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="046be-132">建立 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="046be-132">To create Azure private peering</span></span>

1. <span data-ttu-id="046be-133">匯入 ExpressRoute 的 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="046be-134">您必須從 [PowerShell 資源庫](http://www.powershellgallery.com/) 安裝最新的 PowerShell 安裝程式並將 Azure Resource Manager 模組匯入至 PowerShell 工作階段，以開始使用 ExpressRoute Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="046be-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="046be-135">您必須以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="046be-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="046be-136">匯入已知語意版本範圍內所有的 AzureRM.* 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="046be-137">您也可以只匯入已知語意版本範圍內選取的模組。</span><span class="sxs-lookup"><span data-stu-id="046be-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="046be-138">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="046be-139">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="046be-140">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="046be-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="046be-141">請遵循指示建立 [ExpressRoute 線路](expressroute-howto-circuit-arm.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="046be-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="046be-142">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="046be-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="046be-143">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="046be-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="046be-144">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="046be-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="046be-145">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="046be-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="046be-146">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="046be-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="046be-147">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="046be-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="046be-148">設定線路的 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="046be-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="046be-149">繼續執行接下來的步驟之前，請確定您有下列項目：</span><span class="sxs-lookup"><span data-stu-id="046be-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="046be-150">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="046be-151">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="046be-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="046be-152">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="046be-153">子網路不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="046be-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="046be-154">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="046be-155">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="046be-156">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-156">AS number for peering.</span></span> <span data-ttu-id="046be-157">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="046be-158">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="046be-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="046be-159">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="046be-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="046be-160">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="046be-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="046be-161">使用下列範例來為線路設定 Azure 私用對等互連：</span><span class="sxs-lookup"><span data-stu-id="046be-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="046be-162">如果您選擇使用 MD5 雜湊，請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="046be-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="046be-163">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="046be-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="046be-164">檢視 Azure 私用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="046be-164">To view Azure private peering details</span></span>

<span data-ttu-id="046be-165">您可以使用下列範例來取得設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="046be-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="046be-166">更新 Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="046be-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="046be-167">您可以使用下列範例來更新設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="046be-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="046be-168">在此範例中，線路的 VLAN ID 從 100 更新為 500。</span><span class="sxs-lookup"><span data-stu-id="046be-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="046be-169">刪除 Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="046be-169">To delete Azure private peering</span></span>

<span data-ttu-id="046be-170">您可以執行下列範例來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="046be-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="046be-171">執行此範例之前，您必須確定所有虛擬網路都已經與 ExpressRoute 線路取消連結。</span><span class="sxs-lookup"><span data-stu-id="046be-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="046be-172">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="046be-172">Azure public peering</span></span>

<span data-ttu-id="046be-173">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Azure 公用對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="046be-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="046be-174">建立 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="046be-174">To create Azure public peering</span></span>

1. <span data-ttu-id="046be-175">匯入 ExpressRoute 的 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="046be-176">您必須從 [PowerShell 資源庫](http://www.powershellgallery.com/) 安裝最新的 PowerShell 安裝程式並將 Azure Resource Manager 模組匯入至 PowerShell 工作階段，以開始使用 ExpressRoute Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="046be-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="046be-177">您必須以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="046be-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="046be-178">匯入已知語意版本範圍內所有的 AzureRM.* 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="046be-179">您也可以只匯入已知語意版本範圍內選取的模組。</span><span class="sxs-lookup"><span data-stu-id="046be-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="046be-180">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="046be-181">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="046be-182">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="046be-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="046be-183">請遵循指示建立 [ExpressRoute 線路](expressroute-howto-circuit-arm.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="046be-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="046be-184">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="046be-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="046be-185">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="046be-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="046be-186">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="046be-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="046be-187">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="046be-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="046be-188">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="046be-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="046be-189">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="046be-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="046be-190">設定線路的 Azure 公用對等。</span><span class="sxs-lookup"><span data-stu-id="046be-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="046be-191">進一步執行之前，請確定您具有下列資訊。</span><span class="sxs-lookup"><span data-stu-id="046be-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="046be-192">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="046be-193">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="046be-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="046be-194">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="046be-195">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="046be-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="046be-196">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="046be-197">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="046be-198">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-198">AS number for peering.</span></span> <span data-ttu-id="046be-199">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="046be-200">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="046be-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="046be-201">執行下列範例來為線路設定 Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="046be-202">如果您選擇使用 MD5 雜湊，請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="046be-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="046be-203">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="046be-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="046be-204">檢視 Azure 公用對等詳細資訊</span><span class="sxs-lookup"><span data-stu-id="046be-204">To view Azure public peering details</span></span>

<span data-ttu-id="046be-205">您可以使用下列 Cmdlet 來取得組態詳細資料：</span><span class="sxs-lookup"><span data-stu-id="046be-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="046be-206">更新 Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="046be-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="046be-207">您可以使用下列範例來更新設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="046be-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="046be-208">在此範例中，線路的 VLAN ID 從 200 更新為 600。</span><span class="sxs-lookup"><span data-stu-id="046be-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="046be-209">刪除 Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="046be-209">To delete Azure public peering</span></span>

<span data-ttu-id="046be-210">您可以執行下列範例來移除對等互連設定：</span><span class="sxs-lookup"><span data-stu-id="046be-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="046be-211">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="046be-211">Microsoft peering</span></span>

<span data-ttu-id="046be-212">本節將協助您為 ExpressRoute 線路建立、取得、更新和刪除 Microsoft 對等互連設定。</span><span class="sxs-lookup"><span data-stu-id="046be-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="046be-213">在 2017 年 8 月 1 日以前設定之 ExpressRoute 線路的 Microsoft 對等互連，會透過 Microsoft 對等互連公告所有服務首碼，即使未定義路由篩選也一樣。</span><span class="sxs-lookup"><span data-stu-id="046be-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="046be-214">在 2017 年 8 月 1 日當日或以後設定之 ExpressRoute 線路的 Microsoft 對等互連，不會公告任何首碼，直到路由篩選連結至線路為止。</span><span class="sxs-lookup"><span data-stu-id="046be-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="046be-215">如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="046be-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="046be-216">建立 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="046be-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="046be-217">匯入 ExpressRoute 的 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="046be-218">您必須從 [PowerShell 資源庫](http://www.powershellgallery.com/) 安裝最新的 PowerShell 安裝程式並將 Azure Resource Manager 模組匯入至 PowerShell 工作階段，以開始使用 ExpressRoute Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="046be-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="046be-219">您必須以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="046be-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="046be-220">匯入已知語意版本範圍內所有的 AzureRM.* 模組。</span><span class="sxs-lookup"><span data-stu-id="046be-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="046be-221">您也可以只匯入已知語意版本範圍內選取的模組。</span><span class="sxs-lookup"><span data-stu-id="046be-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="046be-222">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="046be-223">選取您想要建立 ExpressRoute 線路的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="046be-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="046be-224">建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="046be-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="046be-225">請遵循指示建立 [ExpressRoute 線路](expressroute-howto-circuit-arm.md) ，並由連線提供者佈建它。</span><span class="sxs-lookup"><span data-stu-id="046be-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="046be-226">如果您的連線提供者是提供受管理的第 3 層服務，您可以要求連線提供者為您啟用 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="046be-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="046be-227">在此情況下，您不需要遵循後續幾節所列的指示。</span><span class="sxs-lookup"><span data-stu-id="046be-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="046be-228">不過，如果您的連線提供者不管理路由，請在建立線路之後繼續使用後續步驟進行設定。</span><span class="sxs-lookup"><span data-stu-id="046be-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="046be-229">檢查 ExpressRoute 線路，以確定已佈建且已啟用線路。</span><span class="sxs-lookup"><span data-stu-id="046be-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="046be-230">請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="046be-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="046be-231">回應如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="046be-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="046be-232">設定線路的 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="046be-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="046be-233">繼續之前，請確定您擁有下列資訊。</span><span class="sxs-lookup"><span data-stu-id="046be-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="046be-234">主要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="046be-235">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="046be-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="046be-236">次要連結的 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="046be-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="046be-237">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="046be-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="046be-238">供建立此對等的有效 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="046be-239">請確定線路有沒有其他對等使用相同的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="046be-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="046be-240">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-240">AS number for peering.</span></span> <span data-ttu-id="046be-241">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="046be-242">公告的首碼：您必須提供一份您打算在 BGP 工作階段上公告的所有首碼的清單。</span><span class="sxs-lookup"><span data-stu-id="046be-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="046be-243">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="046be-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="046be-244">如果計劃傳送一組首碼，可以傳送以逗號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="046be-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="046be-245">這些首碼必須在 RIR / IRR 中註冊給您。</span><span class="sxs-lookup"><span data-stu-id="046be-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="046be-246">**選用：**客戶 ASN：如果您要公告的首碼未註冊給對等互連 AS 編號，則可以指定它們所註冊的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="046be-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="046be-247">路由登錄名稱：您可以指定可供註冊 AS 編號和首碼的 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="046be-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="046be-248">**選用：**MD5 雜湊 (如果選擇使用)。</span><span class="sxs-lookup"><span data-stu-id="046be-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="046be-249">使用下列範例來為線路設定 Microsoft 對等互連：</span><span class="sxs-lookup"><span data-stu-id="046be-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="046be-250">取得 Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="046be-250">To get Microsoft peering details</span></span>

<span data-ttu-id="046be-251">您可以使用下列範例來取得設定詳細資料：</span><span class="sxs-lookup"><span data-stu-id="046be-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="046be-252">更新 Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="046be-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="046be-253">您可以使用下列範例來更新設定的任何部分：</span><span class="sxs-lookup"><span data-stu-id="046be-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="046be-254">刪除 Microsoft 對等</span><span class="sxs-lookup"><span data-stu-id="046be-254">To delete Microsoft peering</span></span>

<span data-ttu-id="046be-255">您可以執行下列 Cmdlet 來移除對等組態：</span><span class="sxs-lookup"><span data-stu-id="046be-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="046be-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="046be-256">Next steps</span></span>

<span data-ttu-id="046be-257">下一步， [將 VNet 連結到 ExpressRoute 線路](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="046be-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="046be-258">如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="046be-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="046be-259">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="046be-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="046be-260">如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="046be-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
