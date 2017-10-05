---
title: "確認連線：Azure ExpressRoute 疑難排解指南 | Microsoft Docs"
description: "此頁面提供 ExpressRoute 路線的端對端連線確認和疑難排解的指示。"
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
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="29bbc-103">確認 ExpressRoute 連線</span><span class="sxs-lookup"><span data-stu-id="29bbc-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="29bbc-104">ExpressRoute 透過連線提供者所提供的私人連線將內部部署網路擴充至 Microsoft 雲端，涉及三個不同的網路區域：</span><span class="sxs-lookup"><span data-stu-id="29bbc-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="29bbc-105">客戶網路</span><span class="sxs-lookup"><span data-stu-id="29bbc-105">Customer Network</span></span>
-   <span data-ttu-id="29bbc-106">提供者網路</span><span class="sxs-lookup"><span data-stu-id="29bbc-106">Provider Network</span></span>
-   <span data-ttu-id="29bbc-107">Microsoft 資料中心</span><span class="sxs-lookup"><span data-stu-id="29bbc-107">Microsoft Datacenter</span></span>

<span data-ttu-id="29bbc-108">本文件的目的是協助使用者識別連線有沒有問題、在哪一個區域，藉此尋找適當的小組來解決問題。</span><span class="sxs-lookup"><span data-stu-id="29bbc-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="29bbc-109">如果需要 Microsoft 支援服務解決問題，請利用 [Microsoft 支援服務][Support]開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="29bbc-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29bbc-110">本文件旨在協助診斷並修正簡單的問題。</span><span class="sxs-lookup"><span data-stu-id="29bbc-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="29bbc-111">它無法取代 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="29bbc-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="29bbc-112">如果無法使用本文提供的指引來解決問題，請利用 [Microsoft 支援服務][Support]開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="29bbc-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="29bbc-113">概觀</span><span class="sxs-lookup"><span data-stu-id="29bbc-113">Overview</span></span>
<span data-ttu-id="29bbc-114">下圖顯示使用 ExpressRoute 從客戶網路連至 Microsoft 網路的邏輯連線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="29bbc-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="29bbc-115">[![1]][1]</span></span>

<span data-ttu-id="29bbc-116">在上圖中，數字指出重要的網路點。</span><span class="sxs-lookup"><span data-stu-id="29bbc-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="29bbc-117">本文提及不同網路點會附上其圖中的編號。</span><span class="sxs-lookup"><span data-stu-id="29bbc-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="29bbc-118">網路點 3 和 4 可能互換 (第 2 層裝置)，取決於 ExpressRoute 連線模型 (雲端 Exchange 共置、點對點乙太網路連線、或任何對任何 (IPVPN))。</span><span class="sxs-lookup"><span data-stu-id="29bbc-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="29bbc-119">圖中的重要網路點分別是︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="29bbc-120">客戶計算裝置 (例如，伺服器或電腦)</span><span class="sxs-lookup"><span data-stu-id="29bbc-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="29bbc-121">CE︰客戶邊緣路由器</span><span class="sxs-lookup"><span data-stu-id="29bbc-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="29bbc-122">PE (面對 CE)︰面對客戶邊緣路由器的提供者邊緣路由器/交換器。</span><span class="sxs-lookup"><span data-stu-id="29bbc-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="29bbc-123">在本文件中稱為 PE-CE。</span><span class="sxs-lookup"><span data-stu-id="29bbc-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="29bbc-124">PE (面對 MSEE)︰面對 MSEE 的提供者邊緣路由器/交換器。</span><span class="sxs-lookup"><span data-stu-id="29bbc-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="29bbc-125">在本文件中稱為 PE-MSEE。</span><span class="sxs-lookup"><span data-stu-id="29bbc-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="29bbc-126">MSEE：Microsoft Enterprise Edge (MSEE) ExpressRoute 路由器</span><span class="sxs-lookup"><span data-stu-id="29bbc-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="29bbc-127">虛擬網路 (VNet) 閘道器</span><span class="sxs-lookup"><span data-stu-id="29bbc-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="29bbc-128">Azure VNet 上的計算裝置</span><span class="sxs-lookup"><span data-stu-id="29bbc-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="29bbc-129">如果使用雲端 Exchange 共置或點對點乙太網路連線的連線模型，客戶邊緣路由器 (2) 會建立與 MSEE (5) 的 BGP 對等互連。</span><span class="sxs-lookup"><span data-stu-id="29bbc-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="29bbc-130">網路點 3 和 4 仍會存在，但會化做透明的第 2 層裝置。</span><span class="sxs-lookup"><span data-stu-id="29bbc-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="29bbc-131">如果使用任何對任何 (IPVPN) 連線模型，PE (面對 MSEE)(4) 會建立與 MSEE (5) 的 BGP 對等互連。</span><span class="sxs-lookup"><span data-stu-id="29bbc-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="29bbc-132">然後，路由會透過 IPVPN 服務網路提供者的網路傳播回客戶網路。</span><span class="sxs-lookup"><span data-stu-id="29bbc-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-133">為了讓 ExpressRoute 有高可用性，Microsoft 需要在 MSEE (5) 和 PE-MSEE (4) 之間有一組備援的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="29bbc-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="29bbc-134">我們也鼓勵您在客戶網路和 PE-CE 之間有一組備援的網路路徑。</span><span class="sxs-lookup"><span data-stu-id="29bbc-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="29bbc-135">不過，在任何對任何 (IPVPN) 連線模型中，單一 CE 裝置 (2) 可能會連線到一或多個 PE (3)。</span><span class="sxs-lookup"><span data-stu-id="29bbc-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="29bbc-136">若要確認 ExpressRoute 路線，需要下列步驟 (附網路點編號)︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="29bbc-137">確認路線的佈建和狀態 (5)</span><span class="sxs-lookup"><span data-stu-id="29bbc-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="29bbc-138">確認至少已設定一個 ExpressRoute 對等互連 (5)</span><span class="sxs-lookup"><span data-stu-id="29bbc-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="29bbc-139">確認 Microsoft 與服務之間的提供者之間的 ARP (4 和 5 之間的連結)</span><span class="sxs-lookup"><span data-stu-id="29bbc-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="29bbc-140">確認 BGP 和 MSEE 上的路由 (BGP 在4 到 5 之間，如果連接 VNet 則在 5 至 6 之間) </span><span class="sxs-lookup"><span data-stu-id="29bbc-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="29bbc-141">檢查流量統計資料 (通過 5 的流量)</span><span class="sxs-lookup"><span data-stu-id="29bbc-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="29bbc-142">未來將加入更多確認和檢查，請每個月回來查看！</span><span class="sxs-lookup"><span data-stu-id="29bbc-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="29bbc-143">確認路線的佈建和狀態</span><span class="sxs-lookup"><span data-stu-id="29bbc-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="29bbc-144">不論是何種連線模型，皆必須建立 ExpressRoute 路線，系統才會為佈建的路線產生服務機碼。</span><span class="sxs-lookup"><span data-stu-id="29bbc-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="29bbc-145">佈建 ExpressRoute 路線會在 PE-MSEE (4) 和 MSEE (5) 之間建立備援的第 2 層連線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="29bbc-146">如需有關如何建立、修改、佈建、確認 ExpressRoute 路線的詳細資訊，請參閱[建立和修改 ExpressRoute 路線][CreateCircuit]一文。</span><span class="sxs-lookup"><span data-stu-id="29bbc-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="29bbc-147">服務機碼可唯一識別 ExpressRoute 路線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="29bbc-148">本文中所述的 Powershell 命令大多需要有這個機碼。</span><span class="sxs-lookup"><span data-stu-id="29bbc-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="29bbc-149">此外，如果您需 Microsoft 或 ExpressRoute 合作夥伴協助進行問題的疑難排解，請提供服務機碼以利輕易識別路線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="29bbc-150">透過 Azure 入口網站進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-150">Verification via the Azure portal</span></span>
<span data-ttu-id="29bbc-151">在 Azure 入口網站中，選取功能表左欄中的 ![2][2]，然後選取 ExpressRoute 路線，便可以檢查 ExpressRoute 路線狀態。</span><span class="sxs-lookup"><span data-stu-id="29bbc-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="29bbc-152">選取 [所有資源] 底下列出的 ExpressRoute 路線，會開啟 ExpressRoute 路線刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29bbc-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="29bbc-153">在刀鋒視窗的 ![3][3] 區段中，會列出ExpressRoute 的基本資料，如以下螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="29bbc-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="29bbc-154">![4][4]</span></span>    

<span data-ttu-id="29bbc-155">在 ExpressRoute [基本資料] 中，[路線狀態] 指出 Microsoft 端路線的狀態。</span><span class="sxs-lookup"><span data-stu-id="29bbc-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="29bbc-156">[提供者狀態] 指出在服務提供者端是否「已佈建/未佈建」路線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="29bbc-157">[路線狀態] 必須是 [已啟用]，且[提供者狀態] 必須是 [已佈建]，ExpressRoute 路線才能運作。</span><span class="sxs-lookup"><span data-stu-id="29bbc-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-158">如果 [路線狀態] 未啟用，請連絡 [Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29bbc-159">如果 [提供者狀態] 是未佈建，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="29bbc-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="29bbc-160">透過 PowerShell 進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-160">Verification via PowerShell</span></span>
<span data-ttu-id="29bbc-161">若要列出資源群組中的所有 ExpressRoute 路線，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="29bbc-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="29bbc-162">您可以透過 Azure 入口網站取得您的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="29bbc-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="29bbc-163">請參閱本文之前的文章段落，並記下範例螢幕擷取畫面中列出的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="29bbc-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="29bbc-164">若要選取資源群組中的特定 ExpressRoute 路線，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="29bbc-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="29bbc-165">範例回應：</span><span class="sxs-lookup"><span data-stu-id="29bbc-165">A sample response is:</span></span>

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

<span data-ttu-id="29bbc-166">若要確認 ExpressRoute 路線是否在運作，請特別注意下列欄位︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="29bbc-167">如果 CircuitProvisioningState 不是 enabled，請連絡 [Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29bbc-168">如果 ServiceProviderProvisioningState 不是 provisioned，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="29bbc-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="29bbc-169">透過 PowerShell (傳統) 進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="29bbc-170">若要列出訂用帳戶下的所有 ExpressRoute 路線，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="29bbc-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="29bbc-171">若要選取特定 ExpressRoute 路線，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="29bbc-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="29bbc-172">範例回應：</span><span class="sxs-lookup"><span data-stu-id="29bbc-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29bbc-173">若要確認 ExpressRoute 路線是否在運作，請特別注意下列欄位︰ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span><span class="sxs-lookup"><span data-stu-id="29bbc-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-174">如果 Status 不是 enabled，請連絡 [Microsoft 支援服務][Support]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="29bbc-175">如果 ServiceProviderProvisioningState 不是 provisioned，請連絡您的服務提供者。</span><span class="sxs-lookup"><span data-stu-id="29bbc-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="29bbc-176">確認對等互連組態</span><span class="sxs-lookup"><span data-stu-id="29bbc-176">Validate Peering Configuration</span></span>
<span data-ttu-id="29bbc-177">服務提供者已完成 ExpressRoute 路之線佈建後，可以透過 MSEE-PR (4) 和 MSEE (5) 之間的 ExpressRoute 路線建立路由組態。</span><span class="sxs-lookup"><span data-stu-id="29bbc-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="29bbc-178">每個 ExpressRoute 線路可以啟用一、二或三個路由內容︰Azure 私人對等互連 (送至 Azure 中私人虛擬網路的流量)、Azure 公用對等互連 (送至 Azure 中公用 IP 位址的流量) 及 Microsoft 對等互連 (送至 Office 365 和 Dynamics 365 的流量)。</span><span class="sxs-lookup"><span data-stu-id="29bbc-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="29bbc-179">如需有關如何建立及修改路由組態的詳細資訊，請參閱[建立和修改 ExpressRoute 路線的路由][CreatePeering]一文。</span><span class="sxs-lookup"><span data-stu-id="29bbc-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="29bbc-180">透過 Azure 入口網站進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="29bbc-181">Azure 入口網站中有個已知的錯誤：如果 ExpressRoute 對等互連是由服務提供者設定，在入口網站中「不會」顯示 ExpressRoute 對等互連。</span><span class="sxs-lookup"><span data-stu-id="29bbc-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="29bbc-182">透過入口網站或 PowerShell 新增 ExpressRoute 對等互連，可覆寫服務提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="29bbc-183">這個動作會中斷 ExpressRoute 路線上的路由，且需要服務提供者支援將設定還原並重新建立一般路由。</span><span class="sxs-lookup"><span data-stu-id="29bbc-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="29bbc-184">只有當確定服務提供者僅提供第 2 層服務時，才修改 ExpressRoute 對等互連！</span><span class="sxs-lookup"><span data-stu-id="29bbc-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29bbc-185">如果第 3 層是由服務提供者提供，且入口網站中的對等互連是空白的，可以用 PowerShell 來查看服務提供者所做的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="29bbc-186">在 Azure 入口網站中，選取功能表左欄中的 ![2][2]，然後選取 ExpressRoute 路線，便可以查看 ExpressRoute 路線的狀態。</span><span class="sxs-lookup"><span data-stu-id="29bbc-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="29bbc-187">選取 [所有資源] 底下列出的 ExpressRoute 路線，會開啟 ExpressRoute 路線刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="29bbc-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="29bbc-188">在刀鋒視窗的 ![3][3] 區段中，會列出ExpressRoute 的基本資料，如以下螢幕擷取畫面所示︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="29bbc-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="29bbc-189">![5][5]</span></span>

<span data-ttu-id="29bbc-190">在以上範例中，啟用了 Azure 私人對等互連的路由內容，但沒有啟用 Azure 公用路由內容和 Microsoft 對等互連路由內容。</span><span class="sxs-lookup"><span data-stu-id="29bbc-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="29bbc-191">啟用成功的對等互連內容也會列出主要和次要點對點 (BGP 所需) 子網路。</span><span class="sxs-lookup"><span data-stu-id="29bbc-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="29bbc-192">/30 子網路是用於 MSEE 和 PE-MSEE 的介面 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29bbc-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="29bbc-193">若對等互連沒有啟用，檢查指派的主要和次要子網路是否符合 PE-MSEE 上的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="29bbc-194">如果不符，若要變更 MSEE 路由器上的組態，請參閱[建立和修改 ExpressRoute 路線的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="29bbc-195">透過 PowerShell 進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-195">Verification via PowerShell</span></span>
<span data-ttu-id="29bbc-196">若要取得 Azure 私人對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="29bbc-197">以下是已成功設定私人對等互連的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="29bbc-198">成功啟用的對等互連內容也會列出主要和次要位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="29bbc-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="29bbc-199">/30 子網路是用於 MSEE 和 PE-MSEE 的介面 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29bbc-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="29bbc-200">若要取得 Azure 公用對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="29bbc-201">若要取得 Microsoft 對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="29bbc-202">如未設定對等互連，會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="29bbc-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="29bbc-203">未設定所述對等互連 (在此範例中是 Azure 公用互對等連) 的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="29bbc-204">若對等互連沒有啟用，檢查指派的主要和次要子網路是否符合連結之 PE-MSEE 上的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-205">也請檢查 MSEE 上是否使用正確的 VlanId、AzureASN、PeerASN，以及這些值是否對應至連結的 PE-MSEE 上使用的項目。</span><span class="sxs-lookup"><span data-stu-id="29bbc-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-206">如果選擇 MD5 雜湊，共用的金鑰應該和「MSEE 與 PE-MSEE」對上的金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="29bbc-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="29bbc-207">若要變更 MSEE 路由器上的組態，請參閱 [建立和修改 ExpressRoute 線路的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="29bbc-208">透過 PowerShell (傳統) 進行確認</span><span class="sxs-lookup"><span data-stu-id="29bbc-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="29bbc-209">若要取得 Azure 私人對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="29bbc-210">以下是已成功設定私人對等互連的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="29bbc-211">啟用成功的對等互連內容也會列出主要和次要位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="29bbc-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="29bbc-212">/30 子網路是用於 MSEE 和 PE-MSEE 的介面 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29bbc-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="29bbc-213">若要取得 Azure 公用對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="29bbc-214">若要取得 Microsoft 對等互連的組態詳細資料，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="29bbc-215">如果第 3 層對等互連是由服務提供者設定，透過入口網站或 PowerShell 設定 ExpressRoute 對等互連可覆寫服務提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="29bbc-216">重設提供者端的對等互連設定需要服務提供者的支援。</span><span class="sxs-lookup"><span data-stu-id="29bbc-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="29bbc-217">只有當確定服務提供者僅提供第 2 層服務時，才修改 ExpressRoute 對等互連！</span><span class="sxs-lookup"><span data-stu-id="29bbc-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29bbc-218">若對等互連沒有啟用，檢查指派的主要和次要對等互連子網路是否符合連結之 PE-MSEE 上的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-219">也請檢查 MSEE 上是否使用正確的 VlanId、AzureAsn、PeerAsn，以及這些值是否對應至連結的 PE-MSEE 上使用的項目。</span><span class="sxs-lookup"><span data-stu-id="29bbc-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-220">若要變更 MSEE 路由器上的組態，請參閱 [建立和修改 ExpressRoute 線路的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="29bbc-221">確認 Microsoft 與服務提供者之間的 ARP</span><span class="sxs-lookup"><span data-stu-id="29bbc-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="29bbc-222">本節使用 PowerShell (傳統) 命令。</span><span class="sxs-lookup"><span data-stu-id="29bbc-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="29bbc-223">如果您一向使用 PowerShell 的 Azure Resource Manager 命令，請確定您具有可以在 [Azure 傳統入口網站][OldPortal]存取訂用帳戶的系統管理員/共同管理員存取權。</span><span class="sxs-lookup"><span data-stu-id="29bbc-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="29bbc-224">如需針對使用 Azure Resource Manager 命令進行疑難排解，請參閱[在 Resource Manager 部署模型中取得 ARP 資料表][ARP]文件。</span><span class="sxs-lookup"><span data-stu-id="29bbc-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-225">若要取得 ARP，可以使用 Azure 入口網站和 Azure Resource Manager PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="29bbc-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="29bbc-226">如果使用 Azure Resource Manager PowerShell 命令時發生錯誤，傳統 PowerShell 命令也可以用於 Azure Resource Manager 的 ExpressRoute 路線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="29bbc-227">若要從主要 MSEE 路由器取得 ARP 表格以用於私人對等互連，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29bbc-228">在成功的案例中，命令的回應範例如下︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="29bbc-229">同樣地，您可以查看 Primary/Secondary 路徑中 MSEE 的 ARP 表，用於 Private/Public/Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="29bbc-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="29bbc-230">以下是對等互連不存在時此命令的回應範例。</span><span class="sxs-lookup"><span data-stu-id="29bbc-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="29bbc-231">如果 ARP 表沒有對應到 MAC 位址之介面的 IP 位址，請檢閱下列條件︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="29bbc-232">針對 MSEE-PR 和 MSEE 之間的連結所指派的 /30 子網路的第一個 IP 位址，是用在 MSEE-PR 的介面上。</span><span class="sxs-lookup"><span data-stu-id="29bbc-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="29bbc-233">Azure 一律為 MSEE 使用第二個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29bbc-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="29bbc-234">確認客戶 (C 標籤) 和服務 (S 標籤) VLAN 標籤是否都和「MSEE-PR 與 MSEE」對上的相符。</span><span class="sxs-lookup"><span data-stu-id="29bbc-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="29bbc-235">確認 MSEE 上的 BGP 和路由</span><span class="sxs-lookup"><span data-stu-id="29bbc-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="29bbc-236">本節使用 PowerShell (傳統) 命令。</span><span class="sxs-lookup"><span data-stu-id="29bbc-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="29bbc-237">如果您一向使用 PowerShell 的 Azure Resource Manager 命令，請確定您具有可以在 [Azure 傳統入口網站][OldPortal]存取訂用帳戶的系統管理員/共同管理員存取權。</span><span class="sxs-lookup"><span data-stu-id="29bbc-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-238">若要取得 BGP 資訊，可以使用 Azure 入口網站和 Azure Resource Manager PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="29bbc-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="29bbc-239">如果使用 Azure Resource Manager PowerShell 命令時發生錯誤，傳統 PowerShell 命令也可以用於 Azure Resource Manager 的 ExpressRoute 路線。</span><span class="sxs-lookup"><span data-stu-id="29bbc-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="29bbc-240">若要取得特定路由內容的路由表 (BGP 芳鄰) 摘要，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29bbc-241">以下是回應範例：</span><span class="sxs-lookup"><span data-stu-id="29bbc-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="29bbc-242">如以上範例所示，此命令在判斷路由內容已建立多久時十實用分。</span><span class="sxs-lookup"><span data-stu-id="29bbc-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="29bbc-243">它也會指出對等互連路由器通告的路由前置詞數目。</span><span class="sxs-lookup"><span data-stu-id="29bbc-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="29bbc-244">如果狀態是作用中或閒置，檢查指派的主要和次要對等互連子網路是否符合連結之 PE-MSEE 上的設定。</span><span class="sxs-lookup"><span data-stu-id="29bbc-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-245">也請檢查 MSEE 上是否使用正確的 VlanId、AzureAsn、PeerAsn，以及這些值是否對應至連結的 PE-MSEE 上使用的項目。</span><span class="sxs-lookup"><span data-stu-id="29bbc-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="29bbc-246">如果選擇 MD5 雜湊，共用的金鑰應該和「MSEE 與 PE-MSEE」對上的金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="29bbc-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="29bbc-247">若要變更 MSEE 路由器上的組態，請參閱[建立和修改 ExpressRoute 路線的路由][CreatePeering]。</span><span class="sxs-lookup"><span data-stu-id="29bbc-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="29bbc-248">如果無法透過特定對等互連連線到特定目的地，請確認 MSEE 的路由表屬於該特定對等互連內容。</span><span class="sxs-lookup"><span data-stu-id="29bbc-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="29bbc-249">如果路由表中有符合的前置詞 (可能是 NATed IP)，則請確認路徑上有防火牆/NSG/ACL，且防火牆/NSG/ACL 允許流量。</span><span class="sxs-lookup"><span data-stu-id="29bbc-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="29bbc-250">若要從 Primary 路徑上的 MSEE 取得完整路由用於特定 Private 路由內容，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="29bbc-251">以下是此命令的成功結果範例︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="29bbc-252">同樣地，您可以查看 Primary/Secondary 路徑中 MSEE 的路由表，用於 Private/Public/Microsoft 對等互連內容。</span><span class="sxs-lookup"><span data-stu-id="29bbc-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="29bbc-253">以下是對等互連不存在時此命令的回應範例：</span><span class="sxs-lookup"><span data-stu-id="29bbc-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="29bbc-254">檢查流量統計資料</span><span class="sxs-lookup"><span data-stu-id="29bbc-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="29bbc-255">若要取得對等互連內容的主要和次要路徑的合併流量統計資料，包括進和出的位元組，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="29bbc-256">此命令的輸出範例如下：</span><span class="sxs-lookup"><span data-stu-id="29bbc-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="29bbc-257">對等互連不存在時，命令的輸出範例如下︰</span><span class="sxs-lookup"><span data-stu-id="29bbc-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="29bbc-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29bbc-258">Next Steps</span></span>
<span data-ttu-id="29bbc-259">如需詳細資訊或協助，請看看下列連結：</span><span class="sxs-lookup"><span data-stu-id="29bbc-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="29bbc-260">[Microsoft 支援服務][Support]</span><span class="sxs-lookup"><span data-stu-id="29bbc-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="29bbc-261">[建立和修改 ExpressRoute 路線][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="29bbc-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="29bbc-262">[建立和修改 ExpressRoute 路線的路由][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="29bbc-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="29bbc-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "ExpressRoute 邏輯連線"</span><span class="sxs-lookup"><span data-stu-id="29bbc-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="29bbc-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "所有資源圖示"</span><span class="sxs-lookup"><span data-stu-id="29bbc-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="29bbc-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "概觀圖示"</span><span class="sxs-lookup"><span data-stu-id="29bbc-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="29bbc-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute 基本資料螢幕擷取畫面範例"</span><span class="sxs-lookup"><span data-stu-id="29bbc-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="29bbc-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute 基本資料螢幕擷取畫面範例"</span><span class="sxs-lookup"><span data-stu-id="29bbc-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






