---
title: "確認連線：Azure ExpressRoute 疑難排解指南 | Microsoft Docs"
description: "此頁面提供疑難排解與驗證結束 tooend 連線，ExpressRoute 電路的指示。"
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="5f52a-103">確認 ExpressRoute 連線</span><span class="sxs-lookup"><span data-stu-id="5f52a-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="5f52a-104">ExpressRoute，擴充到 hello Microsoft 雲端的內部部署網路，透過連線服務提供者來實現的私用連接，牽涉到下列三個不同的網路區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="5f52a-105">客戶網路</span><span class="sxs-lookup"><span data-stu-id="5f52a-105">Customer Network</span></span>
-   <span data-ttu-id="5f52a-106">提供者網路</span><span class="sxs-lookup"><span data-stu-id="5f52a-106">Provider Network</span></span>
-   <span data-ttu-id="5f52a-107">Microsoft 資料中心</span><span class="sxs-lookup"><span data-stu-id="5f52a-107">Microsoft Datacenter</span></span>

<span data-ttu-id="5f52a-108">本文件的 hello 目的是 toohelp 使用者 tooidentify 位置 （或即使） 有連線問題存在，而且內的區域，藉此 tooseek 協助從適當的團隊 tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="5f52a-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="5f52a-109">如果 Microsoft 支援，則需要的 tooresolve 發生問題，開啟支援票證給[Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f52a-110">本文件是預定的 toohelp 診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="5f52a-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="5f52a-111">它不是預期的 toobe Microsoft 支援的取代項目。</span><span class="sxs-lookup"><span data-stu-id="5f52a-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="5f52a-112">開啟支援票證給[Microsoft 支援服務][ Support]如果您是使用所提供的 hello 指引無法 toosolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="5f52a-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="5f52a-113">概觀</span><span class="sxs-lookup"><span data-stu-id="5f52a-113">Overview</span></span>
<span data-ttu-id="5f52a-114">hello 下列圖表顯示 hello 邏輯客戶網路 tooMicrosoft 網路使用 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="5f52a-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="5f52a-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="5f52a-115">[![1]][1]</span></span>

<span data-ttu-id="5f52a-116">在之前圖表 hello，hello 數字會表示金鑰的網路點。</span><span class="sxs-lookup"><span data-stu-id="5f52a-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="5f52a-117">hello 網路點通常透過這份文件所參考其相關的數字。</span><span class="sxs-lookup"><span data-stu-id="5f52a-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="5f52a-118">依據 hello ExpressRoute 連線能力模型 （雲端 Exchange 代管、 點對點乙太網路連線或 Any-any (IPVPN)） hello 網路點 3 和 4 可能參數 （第 2 層的裝置）。</span><span class="sxs-lookup"><span data-stu-id="5f52a-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="5f52a-119">hello 所述的索引鍵的網路點如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f52a-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="5f52a-120">客戶計算裝置 (例如，伺服器或電腦)</span><span class="sxs-lookup"><span data-stu-id="5f52a-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="5f52a-121">CE︰客戶邊緣路由器</span><span class="sxs-lookup"><span data-stu-id="5f52a-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="5f52a-122">PE (面對 CE)︰面對客戶邊緣路由器的提供者邊緣路由器/交換器。</span><span class="sxs-lookup"><span data-stu-id="5f52a-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="5f52a-123">指 tooas PE CEs 本文件中。</span><span class="sxs-lookup"><span data-stu-id="5f52a-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="5f52a-124">PE (面對 MSEE)︰面對 MSEE 的提供者邊緣路由器/交換器。</span><span class="sxs-lookup"><span data-stu-id="5f52a-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="5f52a-125">指 tooas PE MSEEs 本文件中。</span><span class="sxs-lookup"><span data-stu-id="5f52a-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="5f52a-126">MSEE：Microsoft Enterprise Edge (MSEE) ExpressRoute 路由器</span><span class="sxs-lookup"><span data-stu-id="5f52a-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="5f52a-127">虛擬網路 (VNet) 閘道器</span><span class="sxs-lookup"><span data-stu-id="5f52a-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="5f52a-128">計算 hello Azure VNet 上的裝置</span><span class="sxs-lookup"><span data-stu-id="5f52a-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="5f52a-129">如果使用 hello 雲端 Exchange 代管或點對點乙太網路連線的連線模型，hello 客戶邊緣路由器 (2) 會建立 BGP 對等與 MSEEs (5)。</span><span class="sxs-lookup"><span data-stu-id="5f52a-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5f52a-130">網路點 3 和 4 仍會存在，但會化做透明的第 2 層裝置。</span><span class="sxs-lookup"><span data-stu-id="5f52a-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="5f52a-131">如果使用 hello Any-any (IPVPN) 連接模型，則 hello PEs （MSEE 面對） (4) 會建立 BGP 對等與 MSEEs (5)。</span><span class="sxs-lookup"><span data-stu-id="5f52a-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5f52a-132">路由會再傳播後 toohello 客戶網路透過 hello IPVPN 服務提供者網路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-133">為了讓 ExpressRoute 有高可用性，Microsoft 需要在 MSEE (5) 和 PE-MSEE (4) 之間有一組備援的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5f52a-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="5f52a-134">我們也鼓勵您在客戶網路和 PE-CE 之間有一組備援的網路路徑。</span><span class="sxs-lookup"><span data-stu-id="5f52a-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="5f52a-135">不過，在任何-any (IPVPN) 連線模型中，單一的 CE 裝置 (2) 可能是連線的 tooone 或更多的 PEs (3)。</span><span class="sxs-lookup"><span data-stu-id="5f52a-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="5f52a-136">toovalidate ExpressRoute 電路，hello 遵循步驟涵蓋 （有相關聯的 hello 數字指示 hello 網路點）：</span><span class="sxs-lookup"><span data-stu-id="5f52a-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="5f52a-137">確認路線的佈建和狀態 (5)</span><span class="sxs-lookup"><span data-stu-id="5f52a-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="5f52a-138">確認至少已設定一個 ExpressRoute 對等互連 (5)</span><span class="sxs-lookup"><span data-stu-id="5f52a-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="5f52a-139">驗證 ARP 之間 Microsoft 和 hello 服務提供者 （介於 4 到 5 之間的連結）</span><span class="sxs-lookup"><span data-stu-id="5f52a-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="5f52a-140">驗證 BGP 和上 hello MSEE (4 too5 和 5 too6 如果 VNet 連接之間的 BGP) 路由</span><span class="sxs-lookup"><span data-stu-id="5f52a-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="5f52a-141">核取 hello 流量統計資料 （流量通過 5）</span><span class="sxs-lookup"><span data-stu-id="5f52a-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="5f52a-142">多個驗證和檢查將會加入 hello 未來，查看每個月 ！</span><span class="sxs-lookup"><span data-stu-id="5f52a-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="5f52a-143">確認路線的佈建和狀態</span><span class="sxs-lookup"><span data-stu-id="5f52a-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="5f52a-144">Hello 連接模型，不論 ExpressRoute 電路會具有 toobe 建立，因此服務產生循環的佈建金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f52a-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="5f52a-145">佈建 ExpressRoute 路線會在 PE-MSEE (4) 和 MSEE (5) 之間建立備援的第 2 層連線。</span><span class="sxs-lookup"><span data-stu-id="5f52a-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="5f52a-146">如需有關 toocreate，如何修改、 佈建，以及確認 ExpressRoute 電路的詳細資訊，請參閱 hello 文章[建立及修改 ExpressRoute 電路][CreateCircuit]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="5f52a-147">服務機碼可唯一識別 ExpressRoute 路線。</span><span class="sxs-lookup"><span data-stu-id="5f52a-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="5f52a-148">大部分的這份文件中所述的 hello powershell 命令需要此金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f52a-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="5f52a-149">此外，您需要協助來自 Microsoft 或 ExpressRoute 合作夥伴 tootroubleshoot ExpressRoute 問題，提供 hello 服務金鑰 tooreadily 識別 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="5f52a-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5f52a-150">透過 hello Azure 入口網站的驗證</span><span class="sxs-lookup"><span data-stu-id="5f52a-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="5f52a-151">在 hello Azure 入口網站，可以檢查的 ExpressRoute 電路的 hello 狀態選取![2][2] hello 在左提要欄位的功能表，然後選取 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5f52a-152">選取 ExpressRoute 電路列出 [所有資源] 下會開啟 hello ExpressRoute 電路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5f52a-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5f52a-153">在 hello ![3][3]區段 hello 刀鋒視窗中，hello ExpressRoute essentials 列出 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="5f52a-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5f52a-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="5f52a-154">![4][4]</span></span>    

<span data-ttu-id="5f52a-155">在 hello ExpressRoute Essentials*電路狀態*指出 hello hello Microsoft 端上的 hello 循環狀態。</span><span class="sxs-lookup"><span data-stu-id="5f52a-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="5f52a-156">*提供者狀態*指出是否 hello 電路已*已佈建/未佈建*hello 服務提供者端。</span><span class="sxs-lookup"><span data-stu-id="5f52a-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="5f52a-157">為操作的 ExpressRoute 電路 toobe，hello*電路狀態*必須*啟用*和 hello*提供者狀態*必須是*已佈建*.</span><span class="sxs-lookup"><span data-stu-id="5f52a-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-158">如果 hello*電路狀態*是未啟用，請連絡[Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5f52a-159">如果 hello*提供者狀態*為未佈建，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="5f52a-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5f52a-160">透過 PowerShell 進行確認</span><span class="sxs-lookup"><span data-stu-id="5f52a-160">Verification via PowerShell</span></span>
<span data-ttu-id="5f52a-161">toolist 所有 hello ExpressRoute 電路的資源群組中，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="5f52a-162">您可以透過 hello Azure 入口網站來取得資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="5f52a-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="5f52a-163">請參閱此文件的 hello 先前小節，並注意該 hello 資源群組名稱會列在 hello 範例螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="5f52a-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="5f52a-164">tooselect 特定的 ExpressRoute 電路，在資源群組中，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="5f52a-165">範例回應：</span><span class="sxs-lookup"><span data-stu-id="5f52a-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="5f52a-166">tooconfirm 如果 ExpressRoute 電路是否運作正常，請特別注意 toohello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="5f52a-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="5f52a-167">如果 hello *CircuitProvisioningState*是未啟用，請連絡[Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5f52a-168">如果 hello *ServiceProviderProvisioningState*為未佈建，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="5f52a-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="5f52a-169">透過 PowerShell (傳統) 進行確認</span><span class="sxs-lookup"><span data-stu-id="5f52a-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5f52a-170">toolist 所有 hello ExpressRoute 電路訂用帳戶，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="5f52a-171">tooselect 特定的 ExpressRoute 電路，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="5f52a-172">範例回應：</span><span class="sxs-lookup"><span data-stu-id="5f52a-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5f52a-173">tooconfirm 如果 ExpressRoute 電路是否運作正常，請特別注意 toohello 下列欄位： ServiceProviderProvisioningState： 佈建狀態： 啟用</span><span class="sxs-lookup"><span data-stu-id="5f52a-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-174">如果 hello*狀態*是未啟用，請連絡[Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5f52a-175">如果 hello *ServiceProviderProvisioningState*為未佈建，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="5f52a-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="5f52a-176">確認對等互連組態</span><span class="sxs-lookup"><span data-stu-id="5f52a-176">Validate Peering Configuration</span></span>
<span data-ttu-id="5f52a-177">Hello 服務提供者已完成的 hello 佈建 hello ExpressRoute 循環之後，可以透過 hello MSEE Pr (4) 和 MSEEs (5) 之間的 ExpressRoute 電路建立路由組態。</span><span class="sxs-lookup"><span data-stu-id="5f52a-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="5f52a-178">其中一個、 兩個或三個啟用的路由內容，可以有每個 ExpressRoute 電路： Azure 私用對等互連 （流量 tooprivate 虛擬網路在 Azure 中）、 Azure 公用對等 （在 Azure 中流量 toopublic IP 位址，） 和 Microsoft 對等互連 (流量 tooOffice 365和 Dynamics 365）。</span><span class="sxs-lookup"><span data-stu-id="5f52a-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="5f52a-179">如需有關如何 toocreate 和修改路由組態，請參閱 hello 文章[建立及修改 ExpressRoute 電路的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5f52a-180">透過 hello Azure 入口網站的驗證</span><span class="sxs-lookup"><span data-stu-id="5f52a-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="5f52a-181">Hello ExpressRoute 對等互連是其中的 Azure 入口網站中沒有已知的錯誤*不*如果 hello 服務提供者所設定的 hello 入口網站中顯示。</span><span class="sxs-lookup"><span data-stu-id="5f52a-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="5f52a-182">加入透過 hello 入口網站或 PowerShell ExpressRoute 對等互連*hello 服務提供者設定會覆寫*。</span><span class="sxs-lookup"><span data-stu-id="5f52a-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="5f52a-183">此動作會中斷 hello hello ExpressRoute 電路的路由和需要 hello 支援 hello 服務提供者 toorestore hello 設定並重新建立一般路由。</span><span class="sxs-lookup"><span data-stu-id="5f52a-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="5f52a-184">只能修改 hello ExpressRoute 對等互連，確定該 hello 服務提供者會提供僅第 2 層服務 ！</span><span class="sxs-lookup"><span data-stu-id="5f52a-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5f52a-185">如果第 3 層所提供的 hello 服務提供者和 hello 對等互連是空白的 hello 入口網站中，PowerShell 可以使用的 toosee hello 服務設定提供者設定。</span><span class="sxs-lookup"><span data-stu-id="5f52a-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="5f52a-186">在 hello Azure 入口網站，可以檢查 ExpressRoute 循環的狀態選取![2][2] hello 在左提要欄位的功能表，然後選取 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5f52a-187">選取 ExpressRoute 電路列出 [所有資源] 下會開啟 hello ExpressRoute 電路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5f52a-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5f52a-188">在 hello ![3][3] hello 刀鋒視窗中，hello ExpressRoute hello 下列螢幕擷取畫面所示，會被列 essentials 區段：</span><span class="sxs-lookup"><span data-stu-id="5f52a-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5f52a-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="5f52a-189">![5][5]</span></span>

<span data-ttu-id="5f52a-190">在上述範例中的 hello，記下 Azure 私用對等互連的路由內容會啟用，而不會啟用公用 Azure 和 Microsoft 對等互連的路由內容。</span><span class="sxs-lookup"><span data-stu-id="5f52a-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="5f52a-191">已成功啟用的對等互連內容也會有列出 hello 主要和次要的點對點 （需要 BGP） 子網路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="5f52a-192">hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。</span><span class="sxs-lookup"><span data-stu-id="5f52a-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="5f52a-193">如果未啟用的對等互連，請檢查 hello 主要和次要的子網路指派比對上 PE MSEEs hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5f52a-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="5f52a-194">如果沒有，toochange hello 組態 MSEE 路由器上，請參閱太[建立及修改 ExpressRoute 電路的路由][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5f52a-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5f52a-195">透過 PowerShell 進行確認</span><span class="sxs-lookup"><span data-stu-id="5f52a-195">Verification via PowerShell</span></span>
<span data-ttu-id="5f52a-196">tooget hello Azure 私用對等互連設定詳細資料，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="5f52a-197">以下是已成功設定私人對等互連的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="5f52a-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="5f52a-198">已成功啟用的對等內容，就必須列出 hello 主要和次要的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="5f52a-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="5f52a-199">hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。</span><span class="sxs-lookup"><span data-stu-id="5f52a-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5f52a-200">tooget hello Azure 公用對等互連設定詳細資料，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="5f52a-201">tooget hello Microsoft 對等互連設定詳細資料，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="5f52a-202">如未設定對等互連，會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5f52a-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="5f52a-203">Hello 電路內未設定時 hello 所述的對等 （Azure 公用對等互連，在此範例中） 的範例回應：</span><span class="sxs-lookup"><span data-stu-id="5f52a-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="5f52a-204">如果未啟用的對等互連，檢查上 hello hello 指派的主要和次要子相符項目 hello 組態如果連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-205">也請檢查 hello 更正*VlanId*， *AzureASN*，和*PeerASN* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-206">如果選擇 MD5 雜湊，hello 共用的金鑰應該是相同 MSEE 和 PE MSEE 組上。</span><span class="sxs-lookup"><span data-stu-id="5f52a-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5f52a-207">toochange hello 組態在 hello MSEE 路由器上的參閱太 [建立及修改 ExpressRoute 電路的路由] [CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="5f52a-208">透過 PowerShell (傳統) 進行確認</span><span class="sxs-lookup"><span data-stu-id="5f52a-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5f52a-209">tooget hello Azure 私用對等互連設定詳細資料，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="5f52a-210">以下是已成功設定私人對等互連的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="5f52a-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="5f52a-211">已成功，啟用的對等的內容會有列出 hello 主要和次要對等子網路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="5f52a-212">hello/30 子網路用於 hello MSEEs hello 介面 IP 位址和 PE MSEEs。</span><span class="sxs-lookup"><span data-stu-id="5f52a-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5f52a-213">tooget hello Azure 公用對等互連設定詳細資料，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="5f52a-214">tooget hello Microsoft 對等互連設定詳細資料，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="5f52a-215">如果第 3 層對等互連已 hello 服務提供者所設定，設定透過 hello 入口網站或 PowerShell hello ExpressRoute 對等互連會覆寫 hello 服務提供者設定。</span><span class="sxs-lookup"><span data-stu-id="5f52a-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="5f52a-216">重設 hello 提供者端的對等設定需要 hello hello 服務提供者支援。</span><span class="sxs-lookup"><span data-stu-id="5f52a-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="5f52a-217">只能修改 hello ExpressRoute 對等互連，確定該 hello 服務提供者會提供僅第 2 層服務 ！</span><span class="sxs-lookup"><span data-stu-id="5f52a-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5f52a-218">如果未啟用的對等互連，請檢查 hello 主要和次要對等子網路指派比對 hello 上的設定 hello 如果連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-219">也請檢查 hello 更正*VlanId*， *AzureAsn*，和*PeerAsn* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-220">toochange hello 組態在 hello MSEE 路由器上的參閱太 [建立及修改 ExpressRoute 電路的路由] [CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="5f52a-221">Microsoft 與 hello 服務提供者之間驗證 ARP</span><span class="sxs-lookup"><span data-stu-id="5f52a-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="5f52a-222">本節使用 PowerShell (傳統) 命令。</span><span class="sxs-lookup"><span data-stu-id="5f52a-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5f52a-223">如果您已經使用 PowerShell 的 Azure 資源管理員命令，請確定您有系統管理員/共同管理員存取 toohello 訂閱透過[Azure 傳統入口網站][OldPortal]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="5f52a-224">疑難排解使用 Azure 資源管理員的命令，請參閱 toohello [hello Resource Manager 部署模型中的取得 ARP 表格][ ARP]文件。</span><span class="sxs-lookup"><span data-stu-id="5f52a-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-225">可以使用 tooget ARP hello Azure 入口網站和 Azure 資源管理員 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="5f52a-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5f52a-226">如果發生錯誤與 hello Azure 資源管理員 PowerShell 命令，傳統的 PowerShell 命令應能當做傳統的 PowerShell 命令也會搭配 Azure 資源管理員的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5f52a-227">tooget hello 與 hello 私用對等互連 hello 主要 MSEE 路由器的 ARP 表格，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5f52a-228">Hello 命令，在 hello 成功案例的範例回應：</span><span class="sxs-lookup"><span data-stu-id="5f52a-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="5f52a-229">同樣地，您可以檢查 hello ARP 表格，從在 hello hello MSEE*主要*/*次要*路徑，如*私人*/ *公用*/*Microsoft*對等互連。</span><span class="sxs-lookup"><span data-stu-id="5f52a-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="5f52a-230">hello 下列範例顯示 hello 回應 hello 命令的對等互連的不存在。</span><span class="sxs-lookup"><span data-stu-id="5f52a-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="5f52a-231">如果沒有 hello ARP 表格 hello 介面的 IP 位址對應 tooMAC 位址，檢閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5f52a-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="5f52a-232">如果 hello/30 子網路的 hello 第一個 IP 位址指派 hello 連結之間 hello MSEE PR 並用 MSEE MSEE PR hello 介面上</span><span class="sxs-lookup"><span data-stu-id="5f52a-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="5f52a-233">Azure 一律使用 MSEEs hello 第二個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5f52a-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="5f52a-234">請確認是否 hello 客戶 （C-已標記） 和服務 （S 已標記） 的 VLAN 標記符合二者 MSEE PR 和 MSEE 組。</span><span class="sxs-lookup"><span data-stu-id="5f52a-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="5f52a-235">驗證 BGP 和 hello MSEE 上的路由</span><span class="sxs-lookup"><span data-stu-id="5f52a-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="5f52a-236">本節使用 PowerShell (傳統) 命令。</span><span class="sxs-lookup"><span data-stu-id="5f52a-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5f52a-237">如果您已經使用 PowerShell 的 Azure 資源管理員命令，請確定您有系統管理員/共同管理員存取 toohello 訂閱透過[Azure 傳統入口網站][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="5f52a-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-238">tooget BGP 資訊，這兩個 hello 可以使用 Azure 入口網站和 Azure 資源管理員 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="5f52a-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5f52a-239">如果發生錯誤與 hello Azure 資源管理員 PowerShell 命令，傳統的 PowerShell 命令應能當做傳統的 PowerShell 命令也會搭配 Azure 資源管理員的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="5f52a-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5f52a-240">tooget hello 路由表 （BGP 芳鄰） 摘要特定路由內容，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5f52a-241">以下是回應範例：</span><span class="sxs-lookup"><span data-stu-id="5f52a-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="5f52a-242">Hello 前面範例所示，hello 命令會為有用 toodetermine 的時間長度尚未建立 hello 路由的內容。</span><span class="sxs-lookup"><span data-stu-id="5f52a-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="5f52a-243">它也會指出 hello 對等路由器通告的路由前置詞數目。</span><span class="sxs-lookup"><span data-stu-id="5f52a-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="5f52a-244">如果 hello 狀態為作用中或閒置，請檢查 hello 主要和次要對等子網路指派比對 hello 上的設定 hello 如果連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-245">也請檢查 hello 更正*VlanId*， *AzureAsn*，和*PeerAsn* MSEEs 上使用，且如果這些值對應 toohello hello 上使用的連結 PE MSEE。</span><span class="sxs-lookup"><span data-stu-id="5f52a-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5f52a-246">如果選擇 MD5 雜湊，hello 共用的金鑰應該是相同 MSEE 和 PE MSEE 組上。</span><span class="sxs-lookup"><span data-stu-id="5f52a-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5f52a-247">toochange hello 組態在 hello MSEE 路由器上的參閱太[建立及修改 ExpressRoute 電路的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="5f52a-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5f52a-248">如果一段特定的對等互連，不連線到特定目的地，請檢查 hello 路由表的 hello MSEEs 屬於 toohello 特定對等的內容。</span><span class="sxs-lookup"><span data-stu-id="5f52a-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="5f52a-249">如果 hello 路由表中存在相符的前置詞 （可能是 Nat IP），然後檢查是否有防火牆/NSG Acl hello 路徑上，並允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="5f52a-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="5f52a-250">tooget hello 完整路由表從 MSEE hello*主要*hello 特定路徑*私人*路由內容，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5f52a-251">Hello 命令的範例成功結果是：</span><span class="sxs-lookup"><span data-stu-id="5f52a-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="5f52a-252">同樣地，您可以檢查 hello 路由表，從在 hello hello MSEE*主要*/*次要*路徑，如*私人*/ *公用*/*Microsoft*對等的內容。</span><span class="sxs-lookup"><span data-stu-id="5f52a-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="5f52a-253">hello 下列範例顯示 hello 回應 hello 命令的對等互連的不存在：</span><span class="sxs-lookup"><span data-stu-id="5f52a-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="5f52a-254">核取 hello 流量統計資料</span><span class="sxs-lookup"><span data-stu-id="5f52a-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="5f52a-255">tooget hello 和縮小-結合主要和次要路徑流量統計資料-位元組的對等的內容時，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="5f52a-256">Hello 命令的輸出範例是：</span><span class="sxs-lookup"><span data-stu-id="5f52a-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="5f52a-257">用於不存在，互連 hello 命令的輸出範例是：</span><span class="sxs-lookup"><span data-stu-id="5f52a-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="5f52a-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f52a-258">Next Steps</span></span>
<span data-ttu-id="5f52a-259">詳細的資訊或說明，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="5f52a-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="5f52a-260">[Microsoft 支援服務][Support]</span><span class="sxs-lookup"><span data-stu-id="5f52a-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="5f52a-261">[建立和修改 ExpressRoute 路線][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="5f52a-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="5f52a-262">[建立和修改 ExpressRoute 路線的路由][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5f52a-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "ExpressRoute 邏輯連線"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "所有資源圖示"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "概觀圖示"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute 基本資料螢幕擷取畫面範例"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute 基本資料螢幕擷取畫面範例"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






