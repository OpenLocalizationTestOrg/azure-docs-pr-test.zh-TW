---
title: "設定 ExpressRoute 電路 aaaWorkflows |Microsoft 文件"
description: "此頁面會引導您完成設定 ExpressRoute 電路和對等互連的 hello 工作流程"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="a85f3-103">ExpressRoute 工作流程線路佈建和線路狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="a85f3-104">此頁面會引導您透過 hello 服務佈建和以高層級的路由設定工作流程。</span><span class="sxs-lookup"><span data-stu-id="a85f3-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="a85f3-105">hello 圖和相對應的步驟會顯示 hello 工作必須遵循順序 toohave ExpressRoute 循環佈建的端對端。</span><span class="sxs-lookup"><span data-stu-id="a85f3-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="a85f3-106">使用 PowerShell tooconfigure ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="a85f3-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="a85f3-107">遵循指示進行 hello hello[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)文件以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a85f3-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="a85f3-108">順序從 hello 服務提供者的連線。</span><span class="sxs-lookup"><span data-stu-id="a85f3-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="a85f3-109">此過程視情況而異。</span><span class="sxs-lookup"><span data-stu-id="a85f3-109">This process varies.</span></span> <span data-ttu-id="a85f3-110">如需有關如何連絡您的連線服務提供者 tooorder 連線。</span><span class="sxs-lookup"><span data-stu-id="a85f3-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="a85f3-111">請確定，hello 循環已佈建已順利驗證 hello ExpressRoute 循環佈建透過 PowerShell 的狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="a85f3-112">設定路由網域。</span><span class="sxs-lookup"><span data-stu-id="a85f3-112">Configure routing domains.</span></span> <span data-ttu-id="a85f3-113">如果連線提供者為您管理第 3 層，他們會為您的線路設定路由。</span><span class="sxs-lookup"><span data-stu-id="a85f3-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="a85f3-114">如果您連線服務提供者只提供第 2 層服務，您必須設定每 hello 中所述的指導方針路由[路由需求](expressroute-routing.md)和[路由組態](expressroute-howto-routing-classic.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="a85f3-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="a85f3-115">啟用 Azure 私人互連-您必須啟用此對等互連 tooconnect tooVMs / 雲端服務部署在虛擬網路內。</span><span class="sxs-lookup"><span data-stu-id="a85f3-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="a85f3-116">啟用 Azure 公用對等互連-您必須啟用 Azure 公用對等互連如果您想 tooconnect tooAzure 服務裝載於公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a85f3-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="a85f3-117">如果您選擇的 Azure 私人互連的 tooenable 預設路由，這是需求 tooaccess Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a85f3-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="a85f3-118">啟用 Microsoft 對等互連-您必須啟用 Office 365 和 Dynamics 365 這個 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="a85f3-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="a85f3-119">您必須確定您使用不同的 proxy 邊緣 tooconnect tooMicrosoft 比 hello 您用於 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="a85f3-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="a85f3-120">使用的 hello hello 網際網路和 ExpressRoute 的相同邊緣會導致非對稱路由，而導致您網路的連線中斷。</span><span class="sxs-lookup"><span data-stu-id="a85f3-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="a85f3-121">連結虛擬網路 tooExpressRoute 電路-您可以將虛擬網路 tooyour ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="a85f3-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a85f3-122">請依照下列指示[toolink Vnet](expressroute-howto-linkvnet-arm.md) tooyour 循環。</span><span class="sxs-lookup"><span data-stu-id="a85f3-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="a85f3-123">這些 Vnet 可以在 hello 相同 Azure 訂用帳戶 hello ExpressRoute 循環，或可以位於不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a85f3-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="a85f3-124">ExpressRoute 線路佈建狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="a85f3-125">每個 ExpressRoute 線路有兩種狀態：</span><span class="sxs-lookup"><span data-stu-id="a85f3-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="a85f3-126">服務提供者佈建狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-126">Service provider provisioning state</span></span>
* <span data-ttu-id="a85f3-127">狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-127">Status</span></span>

<span data-ttu-id="a85f3-128">Status 代表 Microsoft 的佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="a85f3-129">這個屬性是設定 tooEnabled，當您建立 Expressroute 電路</span><span class="sxs-lookup"><span data-stu-id="a85f3-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="a85f3-130">hello 連線提供者佈建狀態代表 hello hello 連線提供者端的狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="a85f3-131">可能是 *NotProvisioned*、*Provisioning* 或 *Provisioned*。</span><span class="sxs-lookup"><span data-stu-id="a85f3-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="a85f3-132">hello ExpressRoute 電路必須位於已佈建狀態，以便您 toobe 無法 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="a85f3-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="a85f3-133">ExpressRoute 線路的可能狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="a85f3-134">此區段會列出 hello 的 ExpressRoute 電路的可能狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="a85f3-135">**在建立時**</span><span class="sxs-lookup"><span data-stu-id="a85f3-135">**At creation time**</span></span>

<span data-ttu-id="a85f3-136">您會看見 hello ExpressRoute 電路 hello 下列狀態，只要您在執行 hello PowerShell cmdlet toocreate hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="a85f3-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="a85f3-137">**當連線服務提供者處於 hello 的佈建 hello 循環的程序**</span><span class="sxs-lookup"><span data-stu-id="a85f3-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="a85f3-138">您會看到 hello ExpressRoute 電路 hello 下列狀態，只要您在傳遞 hello 服務金鑰 toohello 連線服務提供者，並在開始佈建程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="a85f3-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="a85f3-139">**當連線服務提供者已完成佈建程序的 hello**</span><span class="sxs-lookup"><span data-stu-id="a85f3-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="a85f3-140">您會看到 hello hello 下列狀態，只要 hello 連線服務提供者已完成 hello 佈建程序中的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="a85f3-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="a85f3-141">佈建並啟用僅限 hello 狀態 hello 循環可在適用於您 toobe 無法 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="a85f3-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="a85f3-142">如果您使用第 2 層提供者，則只有當線路處於此狀態下，您才能設定路由。</span><span class="sxs-lookup"><span data-stu-id="a85f3-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="a85f3-143">**當連線服務提供者正在取消佈建 hello 循環**</span><span class="sxs-lookup"><span data-stu-id="a85f3-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="a85f3-144">如果您要求 hello 服務提供者 toodeprovision hello ExpressRoute 循環，您會看到 hello 循環設定 toohello 遵循 hello 服務提供者完成 hello 解除佈建程序之後的狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="a85f3-145">您可以選擇 toore 啟用它，如果需要或是執行 PowerShell 指令程式 toodelete hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a85f3-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a85f3-146">如果您執行 hello PowerShell cmdlet toodelete hello 循環 hello ServiceProviderProvisioningState 時佈建 」 或 「 已佈建 hello 作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a85f3-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="a85f3-147">請先使用您的連線提供者 toodeprovision hello ExpressRoute 循環，然後刪除 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a85f3-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="a85f3-148">Microsoft 將持續 toobill hello 循環，直到您執行 hello PowerShell cmdlet toodelete hello 循環。</span><span class="sxs-lookup"><span data-stu-id="a85f3-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="a85f3-149">路由工作階段組態狀態</span><span class="sxs-lookup"><span data-stu-id="a85f3-149">Routing session configuration state</span></span>
<span data-ttu-id="a85f3-150">hello BGP 佈建狀態可讓您得知是否已經啟用 hello Microsoft edge hello BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a85f3-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="a85f3-151">hello 狀態必須啟用您 toobe 無法 toouse hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="a85f3-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="a85f3-152">它是特別為 Microsoft 對等互連重要 toocheck hello BGP 工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="a85f3-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="a85f3-153">在加法 toohello BGP 佈建狀態，則呼叫另一個狀態*公告公用首碼狀態*。</span><span class="sxs-lookup"><span data-stu-id="a85f3-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="a85f3-154">hello 公告公用首碼狀態必須是在*設定*狀態，而同時向上 hello BGP 工作階段 toobe 以及您路由 toowork 端對端。</span><span class="sxs-lookup"><span data-stu-id="a85f3-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="a85f3-155">如果 hello 公告公用首碼狀態會設 tooa*驗證所需*狀態時，未啟用 hello BGP 工作階段，如 hello 公告前置詞不符合 hello 中 hello 路由所登錄的任何數字。</span><span class="sxs-lookup"><span data-stu-id="a85f3-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a85f3-156">Hello 公告公用首碼狀態是否在*進行手動驗證*狀態時，您必須開啟支援票證給[Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)並提供您自己沿著通告 hello IP 位址的辨識項hello 相關聯自發系統編號。</span><span class="sxs-lookup"><span data-stu-id="a85f3-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a85f3-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a85f3-157">Next steps</span></span>
* <span data-ttu-id="a85f3-158">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="a85f3-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="a85f3-159">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="a85f3-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="a85f3-160">設定路由</span><span class="sxs-lookup"><span data-stu-id="a85f3-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="a85f3-161">連結的 VNet tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="a85f3-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

