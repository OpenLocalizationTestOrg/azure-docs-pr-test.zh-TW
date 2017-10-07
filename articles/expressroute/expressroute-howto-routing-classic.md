---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： Azure： 傳統 |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="b8f03-104">建立和修改 ExpressRoute 線路的對等互連 (傳統)</span><span class="sxs-lookup"><span data-stu-id="b8f03-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8f03-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b8f03-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="b8f03-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8f03-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="b8f03-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8f03-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="b8f03-108">視訊 - 私用對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="b8f03-109">視訊 - 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="b8f03-110">視訊 - Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="b8f03-111">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="b8f03-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="b8f03-112">本文將引導您完成 hello 步驟 toocreate 並管理使用 PowerShell 和 hello 傳統部署模型的 ExpressRoute 電路的路由組態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="b8f03-113">下列的 hello 步驟也會顯示您 toocheck hello 狀態更新，或刪除和取消佈建的 ExpressRoute 電路的互連的方式。</span><span class="sxs-lookup"><span data-stu-id="b8f03-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="b8f03-114">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="b8f03-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="b8f03-115">組態必要條件</span><span class="sxs-lookup"><span data-stu-id="b8f03-115">Configuration prerequisites</span></span>
* <span data-ttu-id="b8f03-116">您將需要 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="b8f03-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="b8f03-117">如需詳細資訊，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b8f03-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="b8f03-118">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="b8f03-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="b8f03-119">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="b8f03-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="b8f03-120">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)和有 hello 電路啟用您的連線提供者，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="b8f03-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="b8f03-121">hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet 如下所述的佈建並啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8f03-122">這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。</span><span class="sxs-lookup"><span data-stu-id="b8f03-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="b8f03-123">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="b8f03-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="b8f03-124">您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。</span><span class="sxs-lookup"><span data-stu-id="b8f03-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="b8f03-125">您可以依自己選擇的任何順序設定對等。</span><span class="sxs-lookup"><span data-stu-id="b8f03-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="b8f03-126">不過，您必須確定您完成每個對等互連一次一個的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b8f03-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="b8f03-127">登入 tooyour Azure 帳戶，然後選取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b8f03-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="b8f03-128">使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="b8f03-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="b8f03-129">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8f03-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="b8f03-130">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8f03-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="b8f03-131">如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8f03-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="b8f03-132">接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b8f03-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="b8f03-133">Azure 私用對等</span><span class="sxs-lookup"><span data-stu-id="b8f03-133">Azure private peering</span></span>
<span data-ttu-id="b8f03-134">本節提供 toocreate，如何取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定的指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="b8f03-135">toocreate Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="b8f03-136">**匯入 ExpressRoute hello PowerShell 模組。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="b8f03-137">您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。</span><span class="sxs-lookup"><span data-stu-id="b8f03-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="b8f03-138">Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8f03-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="b8f03-139">**建立 ExpressRoute 線路。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="b8f03-140">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="b8f03-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="b8f03-141">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="b8f03-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="b8f03-142">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="b8f03-143">不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="b8f03-144">**請檢查已佈建 hello ExpressRoute 電路 tooensure。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="b8f03-145">如果佈建及也啟用 hello ExpressRoute 循環，您必須先檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="b8f03-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="b8f03-146">請參閱以下的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b8f03-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="b8f03-147">請確定 hello 循環顯示已佈建與已啟用。</span><span class="sxs-lookup"><span data-stu-id="b8f03-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="b8f03-148">如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="b8f03-149">**設定 Azure 私用對等互連 hello 循環。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="b8f03-150">請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="b8f03-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="b8f03-151">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="b8f03-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="b8f03-152">這不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="b8f03-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="b8f03-153">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="b8f03-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="b8f03-154">這不能在保留給虛擬網路的任何位址空間中。</span><span class="sxs-lookup"><span data-stu-id="b8f03-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="b8f03-155">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="b8f03-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="b8f03-156">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="b8f03-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="b8f03-157">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-157">AS number for peering.</span></span> <span data-ttu-id="b8f03-158">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="b8f03-159">您可以將私用 AS 編號用於此對等。</span><span class="sxs-lookup"><span data-stu-id="b8f03-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="b8f03-160">請確定您不是使用 65515。</span><span class="sxs-lookup"><span data-stu-id="b8f03-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="b8f03-161">MD5 雜湊，如果您選擇其中一個 toouse。</span><span class="sxs-lookup"><span data-stu-id="b8f03-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="b8f03-162">**這是選擇性的**。</span><span class="sxs-lookup"><span data-stu-id="b8f03-162">**This is optional**.</span></span>
     
    <span data-ttu-id="b8f03-163">您可以執行下列 cmdlet tooconfigure 為您的電路 Azure 私人互連的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8f03-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="b8f03-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="b8f03-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="b8f03-165">如果您選擇 toouse MD5 雜湊，您可以使用下列的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8f03-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="b8f03-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="b8f03-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="b8f03-167">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="b8f03-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="b8f03-168">tooview Azure 私用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8f03-168">tooview Azure private peering details</span></span>
<span data-ttu-id="b8f03-169">就可以使用下列 cmdlet 的 hello 設定詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8f03-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="b8f03-170">tooupdate Azure 私用對等組態</span><span class="sxs-lookup"><span data-stu-id="b8f03-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="b8f03-171">您可以更新使用下列 cmdlet 的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="b8f03-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="b8f03-172">在 hello 下列範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="b8f03-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="b8f03-173">toodelete Azure 私人互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-173">toodelete Azure private peering</span></span>
<span data-ttu-id="b8f03-174">您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定。</span><span class="sxs-lookup"><span data-stu-id="b8f03-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="b8f03-175">您必須確定執行這個指令程式之前，所有虛擬網路是從 hello ExpressRoute 電路取消連結。</span><span class="sxs-lookup"><span data-stu-id="b8f03-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="b8f03-176">Azure 公用對等</span><span class="sxs-lookup"><span data-stu-id="b8f03-176">Azure public peering</span></span>
<span data-ttu-id="b8f03-177">本節提供 toocreate，如何取得、 更新及刪除 hello Azure ExpressRoute 循環的公用對等設定的指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="b8f03-178">toocreate Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="b8f03-179">**匯入 ExpressRoute hello PowerShell 模組。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="b8f03-180">您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。</span><span class="sxs-lookup"><span data-stu-id="b8f03-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="b8f03-181">Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8f03-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="b8f03-182">**建立 ExpressRoute 線路**</span><span class="sxs-lookup"><span data-stu-id="b8f03-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="b8f03-183">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="b8f03-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="b8f03-184">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable Azure 公用對等互連。</span><span class="sxs-lookup"><span data-stu-id="b8f03-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="b8f03-185">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="b8f03-186">不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="b8f03-187">**檢查已佈建 ExpressRoute 循環 tooensure**</span><span class="sxs-lookup"><span data-stu-id="b8f03-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="b8f03-188">如果佈建及也啟用 hello ExpressRoute 循環，您必須先檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="b8f03-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="b8f03-189">請參閱以下的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b8f03-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="b8f03-190">請確定 hello 循環顯示已佈建與已啟用。</span><span class="sxs-lookup"><span data-stu-id="b8f03-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="b8f03-191">如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="b8f03-192">**設定 Azure 公用對等互連 hello 循環**</span><span class="sxs-lookup"><span data-stu-id="b8f03-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="b8f03-193">確定您擁有 hello 繼續接下來，下列資訊。</span><span class="sxs-lookup"><span data-stu-id="b8f03-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="b8f03-194">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="b8f03-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="b8f03-195">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="b8f03-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="b8f03-196">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="b8f03-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="b8f03-197">這必須是有效的公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="b8f03-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="b8f03-198">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="b8f03-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="b8f03-199">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="b8f03-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="b8f03-200">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-200">AS number for peering.</span></span> <span data-ttu-id="b8f03-201">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="b8f03-202">MD5 雜湊，如果您選擇其中一個 toouse。</span><span class="sxs-lookup"><span data-stu-id="b8f03-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="b8f03-203">**這是選擇性的**。</span><span class="sxs-lookup"><span data-stu-id="b8f03-203">**This is optional**.</span></span>
     
    <span data-ttu-id="b8f03-204">您可以執行下列 cmdlet tooconfigure 為您的電路 Azure 公用對等的 hello</span><span class="sxs-lookup"><span data-stu-id="b8f03-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="b8f03-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="b8f03-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="b8f03-206">如果您選擇 toouse MD5 雜湊，您可以使用下列的 hello cmdlet</span><span class="sxs-lookup"><span data-stu-id="b8f03-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="b8f03-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="b8f03-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="b8f03-208">請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。</span><span class="sxs-lookup"><span data-stu-id="b8f03-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="b8f03-209">tooview Azure 公用對等互連的詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8f03-209">tooview Azure public peering details</span></span>
<span data-ttu-id="b8f03-210">就可以使用下列 cmdlet 的 hello 設定詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8f03-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="b8f03-211">tooupdate Azure 公用對等組態</span><span class="sxs-lookup"><span data-stu-id="b8f03-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="b8f03-212">您可以使用下列 cmdlet 的 hello hello 設定的任何部分，更新</span><span class="sxs-lookup"><span data-stu-id="b8f03-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="b8f03-213">正在從在上面範例中的 hello 200 too600 更新 hello hello 循環的 VLAN ID。</span><span class="sxs-lookup"><span data-stu-id="b8f03-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="b8f03-214">toodelete Azure 公用對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-214">toodelete Azure public peering</span></span>
<span data-ttu-id="b8f03-215">您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定</span><span class="sxs-lookup"><span data-stu-id="b8f03-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="b8f03-216">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-216">Microsoft peering</span></span>
<span data-ttu-id="b8f03-217">本節提供 toocreate，如何取得、 更新及刪除 ExpressRoute 循環的 hello Microsoft 對等組態指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="b8f03-218">toocreate Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="b8f03-219">**匯入 ExpressRoute hello PowerShell 模組。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="b8f03-220">您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。</span><span class="sxs-lookup"><span data-stu-id="b8f03-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="b8f03-221">Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8f03-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="b8f03-222">**建立 ExpressRoute 線路**</span><span class="sxs-lookup"><span data-stu-id="b8f03-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="b8f03-223">請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="b8f03-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="b8f03-224">如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。</span><span class="sxs-lookup"><span data-stu-id="b8f03-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="b8f03-225">在此情況下，您不需要 toofollow hello 下一節中所列的指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="b8f03-226">不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="b8f03-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="b8f03-227">**檢查已佈建 ExpressRoute 循環 tooensure**</span><span class="sxs-lookup"><span data-stu-id="b8f03-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="b8f03-228">您必須先簽 toosee hello ExpressRoute 循環是否處於 已佈建且已啟用的狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="b8f03-229">請確定 hello 循環顯示已佈建與已啟用。</span><span class="sxs-lookup"><span data-stu-id="b8f03-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="b8f03-230">如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。</span><span class="sxs-lookup"><span data-stu-id="b8f03-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="b8f03-231">**設定 Microsoft 對等互連 hello 循環**</span><span class="sxs-lookup"><span data-stu-id="b8f03-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="b8f03-232">請確定您擁有 hello 下列資訊才能繼續。</span><span class="sxs-lookup"><span data-stu-id="b8f03-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="b8f03-233">/ 30 子網路 hello 主要連結。</span><span class="sxs-lookup"><span data-stu-id="b8f03-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="b8f03-234">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="b8f03-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="b8f03-235">/ 30 hello 次要連結的子網路。</span><span class="sxs-lookup"><span data-stu-id="b8f03-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="b8f03-236">這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。</span><span class="sxs-lookup"><span data-stu-id="b8f03-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="b8f03-237">有效的 VLAN ID tooestablish 此對等。</span><span class="sxs-lookup"><span data-stu-id="b8f03-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="b8f03-238">請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="b8f03-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="b8f03-239">對等的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-239">AS number for peering.</span></span> <span data-ttu-id="b8f03-240">您可以使用 2 位元組和 4 位元組 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="b8f03-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="b8f03-241">通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8f03-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="b8f03-242">只接受公用 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="b8f03-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="b8f03-243">如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="b8f03-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="b8f03-244">這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。</span><span class="sxs-lookup"><span data-stu-id="b8f03-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="b8f03-245">客戶 ASN： 如果您通告不是數字的已註冊的 toohello 對等互連的前置詞，您可以指定 hello 為其所註冊的數字 toowhich。</span><span class="sxs-lookup"><span data-stu-id="b8f03-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="b8f03-246">**這是選擇性的**。</span><span class="sxs-lookup"><span data-stu-id="b8f03-246">**This is optional**.</span></span>
   * <span data-ttu-id="b8f03-247">路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。</span><span class="sxs-lookup"><span data-stu-id="b8f03-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="b8f03-248">MD5 雜湊，如果您選擇其中一個 toouse。</span><span class="sxs-lookup"><span data-stu-id="b8f03-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="b8f03-249">**這是選擇性。**</span><span class="sxs-lookup"><span data-stu-id="b8f03-249">**This is optional.**</span></span>
     
    <span data-ttu-id="b8f03-250">您可以執行下列 cmdlet tooconfigure Microsoft pering 為您的電路的 hello</span><span class="sxs-lookup"><span data-stu-id="b8f03-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="b8f03-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="b8f03-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="b8f03-252">tooview Microsoft 對等詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8f03-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="b8f03-253">就可以使用下列 cmdlet 的 hello 設定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b8f03-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="b8f03-254">tooupdate Microsoft 對等組態</span><span class="sxs-lookup"><span data-stu-id="b8f03-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="b8f03-255">您可以更新使用下列 cmdlet 的 hello hello 設定的任何部分。</span><span class="sxs-lookup"><span data-stu-id="b8f03-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="b8f03-256">toodelete Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="b8f03-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="b8f03-257">您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定。</span><span class="sxs-lookup"><span data-stu-id="b8f03-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="b8f03-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8f03-258">Next steps</span></span>
<span data-ttu-id="b8f03-259">下一步[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f03-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="b8f03-260">如需有關工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f03-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="b8f03-261">如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f03-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

