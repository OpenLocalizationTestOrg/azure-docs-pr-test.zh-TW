---
title: "建立和修改 ExpressRoute 線路：PowerShell：Azure Resource Manager | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建 ExpressRoute 電路。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="0ba53-103">使用 PowerShell 建立和修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="0ba53-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ba53-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0ba53-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="0ba53-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ba53-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="0ba53-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ba53-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="0ba53-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0ba53-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="0ba53-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="0ba53-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="0ba53-109">本文說明如何 toocreate Azure ExpressRoute 電路使用 PowerShell cmdlet 和 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0ba53-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0ba53-110">本文也會顯示 hello 電路 toocheck hello 狀態如何更新，或刪除，並取消佈建它。</span><span class="sxs-lookup"><span data-stu-id="0ba53-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0ba53-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="0ba53-111">Before you begin</span></span>
* <span data-ttu-id="0ba53-112">安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="0ba53-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="0ba53-113">如需詳細資訊，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0ba53-114">檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="0ba53-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="0ba53-115">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="0ba53-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="0ba53-116">1.登入 tooyour Azure 帳戶並選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0ba53-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="0ba53-117">toobegin 您的設定，登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ba53-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="0ba53-118">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0ba53-119">核取 hello 訂閱 hello 帳戶：</span><span class="sxs-lookup"><span data-stu-id="0ba53-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="0ba53-120">選取您想的 toocreate ExpressRoute 電路的 hello 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="0ba53-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="0ba53-121">2.取得支援的提供者、 位置及頻寬 hello 清單</span><span class="sxs-lookup"><span data-stu-id="0ba53-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="0ba53-122">建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="0ba53-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="0ba53-123">hello PowerShell cmdlet **Get AzureRmExpressRouteServiceProvider**傳回這項資訊在稍後步驟中，您將使用：</span><span class="sxs-lookup"><span data-stu-id="0ba53-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="0ba53-124">請檢查 toosee，如果您連線服務提供者已列於此處。</span><span class="sxs-lookup"><span data-stu-id="0ba53-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="0ba53-125">記下 hello 下列資訊。</span><span class="sxs-lookup"><span data-stu-id="0ba53-125">Make a note of hello following information.</span></span> <span data-ttu-id="0ba53-126">稍後當您建立線路時，將會需要用到它。</span><span class="sxs-lookup"><span data-stu-id="0ba53-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="0ba53-127">名稱</span><span class="sxs-lookup"><span data-stu-id="0ba53-127">Name</span></span>
* <span data-ttu-id="0ba53-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="0ba53-128">PeeringLocations</span></span>
* <span data-ttu-id="0ba53-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="0ba53-129">BandwidthsOffered</span></span>

<span data-ttu-id="0ba53-130">您現在準備好 toocreate ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="0ba53-131">3.建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="0ba53-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="0ba53-132">若您還沒有資源群組，您必須在建立 ExpressRoute 線路之前建立一個。</span><span class="sxs-lookup"><span data-stu-id="0ba53-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="0ba53-133">您可以藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="0ba53-134">hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。</span><span class="sxs-lookup"><span data-stu-id="0ba53-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="0ba53-135">如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。</span><span class="sxs-lookup"><span data-stu-id="0ba53-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="0ba53-136">hello 下面是新的服務金鑰的要求範例：</span><span class="sxs-lookup"><span data-stu-id="0ba53-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="0ba53-137">請確定您指定正確 SKU 層 hello 和 SKU 系列：</span><span class="sxs-lookup"><span data-stu-id="0ba53-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="0ba53-138">SKU 層會判斷 ExpressRoute 標準或 ExpressRoute 高階附加元件是否啟用。</span><span class="sxs-lookup"><span data-stu-id="0ba53-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="0ba53-139">您可以指定*標準*tooget hello 標準 SKU 或*Premium* hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="0ba53-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="0ba53-140">SKU 系列決定 hello 計費的型別。</span><span class="sxs-lookup"><span data-stu-id="0ba53-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="0ba53-141">您可以指定 [Metereddata] 以採用計量付費數據傳輸方案，選取 [Unlimiteddata] 以採用無限行動數據方案。</span><span class="sxs-lookup"><span data-stu-id="0ba53-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="0ba53-142">您可以變更從 hello 計費類型*Metereddata*太*Unlimiteddata*，但是您無法變更 hello 類型從*Unlimiteddata*太*Metereddata*.</span><span class="sxs-lookup"><span data-stu-id="0ba53-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ba53-143">ExpressRoute 電路將計費 hello 發出服務金鑰的時間。</span><span class="sxs-lookup"><span data-stu-id="0ba53-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="0ba53-144">請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。</span><span class="sxs-lookup"><span data-stu-id="0ba53-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="0ba53-145">hello 回應包含 hello 服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="0ba53-145">hello response contains hello service key.</span></span> <span data-ttu-id="0ba53-146">您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：</span><span class="sxs-lookup"><span data-stu-id="0ba53-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="0ba53-147">4.列出所有 ExpressRoute 循環</span><span class="sxs-lookup"><span data-stu-id="0ba53-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="0ba53-148">一份所有 hello 您建立 ExpressRoute 電路 tooget 執行 hello **Get AzureRmExpressRouteCircuit**命令：</span><span class="sxs-lookup"><span data-stu-id="0ba53-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="0ba53-149">hello 回應看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-149">hello response will look similar toohello following example:</span></span>

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="0ba53-150">您可以擷取這項資訊在任何時候使用 hello `Get-AzureRmExpressRouteCircuit` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0ba53-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="0ba53-151">進行呼叫不含任何參數的 hello 列出 hello 的所有電路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="0ba53-152">您的服務金鑰將會列在 hello *ServiceKey*欄位：</span><span class="sxs-lookup"><span data-stu-id="0ba53-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="0ba53-153">hello 回應看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-153">hello response will look similar toohello following example:</span></span>

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="0ba53-154">您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：</span><span class="sxs-lookup"><span data-stu-id="0ba53-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="0ba53-155">5.佈建傳送嗨服務金鑰 tooyour 連線服務提供者</span><span class="sxs-lookup"><span data-stu-id="0ba53-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="0ba53-156">*ServiceProviderProvisioningState*提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0ba53-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="0ba53-157">狀態提供 hello Microsoft 戶端 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="0ba53-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="0ba53-158">如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。</span><span class="sxs-lookup"><span data-stu-id="0ba53-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="0ba53-159">當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="0ba53-160">hello 循環會變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：</span><span class="sxs-lookup"><span data-stu-id="0ba53-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="0ba53-161">您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="0ba53-162">6.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="0ba53-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="0ba53-163">檢查 hello 狀態和 hello 循環索引鍵 hello 狀態，可讓您了解您的提供者已啟用您的循環時間。</span><span class="sxs-lookup"><span data-stu-id="0ba53-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="0ba53-164">在設定 hello 循環之後， *ServiceProviderProvisioningState*會顯示為*已佈建*hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0ba53-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="0ba53-165">hello 回應看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-165">hello response will look similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="0ba53-166">7.建立路由組態</span><span class="sxs-lookup"><span data-stu-id="0ba53-166">7. Create your routing configuration</span></span>
<span data-ttu-id="0ba53-167">如需逐步指示，請參閱 hello [ExpressRoute 電路的路由組態](expressroute-howto-routing-arm.md)文章 toocreate 和修改循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="0ba53-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ba53-168">這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。</span><span class="sxs-lookup"><span data-stu-id="0ba53-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="0ba53-169">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="0ba53-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="0ba53-170">8.連結虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="0ba53-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="0ba53-171">接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="0ba53-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="0ba53-172">使用 hello[連結虛擬網路 tooExpressRoute 電路](expressroute-howto-linkvnet-arm.md)處理 hello Resource Manager 部署模型時，發行項。</span><span class="sxs-lookup"><span data-stu-id="0ba53-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="0ba53-173">取得 hello 狀態的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="0ba53-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="0ba53-174">您可以擷取這項資訊在任何時候使用 hello **Get AzureRmExpressRouteCircuit** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0ba53-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="0ba53-175">進行呼叫不含任何參數的 hello 列出 hello 的所有電路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="0ba53-176">hello 回應將類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-176">hello response will be similar toohello following example:</span></span>

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


<span data-ttu-id="0ba53-177">您可以取得有關特定的 ExpressRoute 電路並 hello 資源群組名稱和循環名稱傳遞為參數 toohello 呼叫：</span><span class="sxs-lookup"><span data-stu-id="0ba53-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="0ba53-178">hello 回應看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-178">hello response will look similar toohello following example:</span></span>

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


<span data-ttu-id="0ba53-179">您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：</span><span class="sxs-lookup"><span data-stu-id="0ba53-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="0ba53-180"><a name="modify"></a>修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="0ba53-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="0ba53-181">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="0ba53-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="0ba53-182">您可以 hello 遵循不中斷的情況：</span><span class="sxs-lookup"><span data-stu-id="0ba53-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="0ba53-183">啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="0ba53-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="0ba53-184">增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。</span><span class="sxs-lookup"><span data-stu-id="0ba53-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="0ba53-185">不支援降級 hello 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="0ba53-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="0ba53-186">變更計量計劃的計量資料 tooUnlimited 資料 hello。</span><span class="sxs-lookup"><span data-stu-id="0ba53-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="0ba53-187">變更計量計劃的資料不支援無限制的資料 tooMetered hello。</span><span class="sxs-lookup"><span data-stu-id="0ba53-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="0ba53-188">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="0ba53-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="0ba53-189">如需有關限制和限制的詳細資訊，請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="0ba53-190">tooenable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="0ba53-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="0ba53-191">您可以使用下列 PowerShell 程式碼片段的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:</span><span class="sxs-lookup"><span data-stu-id="0ba53-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="0ba53-192">hello 電路現在會有 hello ExpressRoute 高階附加元件功能已啟用。</span><span class="sxs-lookup"><span data-stu-id="0ba53-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="0ba53-193">我們將會開始計費您 hello premium 附加元件的功能，儘速 hello 命令已順利執行。</span><span class="sxs-lookup"><span data-stu-id="0ba53-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="0ba53-194">toodisable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="0ba53-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0ba53-195">如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="0ba53-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="0ba53-196">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0ba53-196">Note hello following:</span></span>

* <span data-ttu-id="0ba53-197">您從 premium toostandard 降級之前，您必須確定虛擬網路連結的 hello 數目 toohello 循環為小於 10。</span><span class="sxs-lookup"><span data-stu-id="0ba53-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="0ba53-198">如果您不這樣做，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="0ba53-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="0ba53-199">您必須取消連結其他地理政治區域中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="0ba53-200">如果您不這樣做，更新要求就會失敗，且我們會以進階費率計費。</span><span class="sxs-lookup"><span data-stu-id="0ba53-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="0ba53-201">就私用對等設定而言，路由表必須少於 4000 個路由。</span><span class="sxs-lookup"><span data-stu-id="0ba53-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="0ba53-202">如果您的路由表的大小大於 4000 路由，hello BGP 工作階段卸除，並不會重新啟用，直到 hello 公告的首碼數目，低於 4000。</span><span class="sxs-lookup"><span data-stu-id="0ba53-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="0ba53-203">您可以使用下列 PowerShell cmdlet 的 hello，停用 hello ExpressRoute premium add-on hello 現有循環：</span><span class="sxs-lookup"><span data-stu-id="0ba53-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="0ba53-204">tooupdate hello ExpressRoute 電路頻寬</span><span class="sxs-lookup"><span data-stu-id="0ba53-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="0ba53-205">如需針對您的提供者支援的頻寬選項，請檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="0ba53-206">您可以挑選任何比您現有的循環 hello 大小更大的大小。</span><span class="sxs-lookup"><span data-stu-id="0ba53-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ba53-207">如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="0ba53-208">如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="0ba53-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="0ba53-209">您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。</span><span class="sxs-lookup"><span data-stu-id="0ba53-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="0ba53-210">降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="0ba53-211">決定您需要的大小之後，請使用下列命令 tooresize hello 您的循環：</span><span class="sxs-lookup"><span data-stu-id="0ba53-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="0ba53-212">您的電路將調整大小 hello Microsoft 一邊。</span><span class="sxs-lookup"><span data-stu-id="0ba53-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="0ba53-213">然後您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。</span><span class="sxs-lookup"><span data-stu-id="0ba53-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="0ba53-214">此通知之後，我們將會開始計費您更新的 hello 頻寬選項。</span><span class="sxs-lookup"><span data-stu-id="0ba53-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="0ba53-215">從付費 toounlimited toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="0ba53-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="0ba53-216">您可以使用下列 PowerShell 程式碼片段的 hello 變更 hello 的 ExpressRoute 電路 SKU:</span><span class="sxs-lookup"><span data-stu-id="0ba53-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="0ba53-217">toocontrol 存取 toohello 傳統和資源管理員環境</span><span class="sxs-lookup"><span data-stu-id="0ba53-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="0ba53-218">檢閱中的 hello 指示[從 hello 傳統 toohello Resource Manager 部署模型的移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="0ba53-219">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="0ba53-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="0ba53-220">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0ba53-220">Note hello following:</span></span>

* <span data-ttu-id="0ba53-221">您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0ba53-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="0ba53-222">如果此作業失敗，請檢查 toosee 如果任何虛擬網路連結 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="0ba53-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="0ba53-223">如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。</span><span class="sxs-lookup"><span data-stu-id="0ba53-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="0ba53-224">我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。</span><span class="sxs-lookup"><span data-stu-id="0ba53-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="0ba53-225">如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="0ba53-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="0ba53-226">這會停止計費 hello 循環</span><span class="sxs-lookup"><span data-stu-id="0ba53-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="0ba53-227">若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ba53-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="0ba53-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ba53-228">Next steps</span></span>

<span data-ttu-id="0ba53-229">建立您的循環之後，請確定您執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0ba53-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="0ba53-230">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="0ba53-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="0ba53-231">連結您的虛擬網路 tooyour ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="0ba53-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
