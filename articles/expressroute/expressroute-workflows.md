---
title: "設定 ExpressRoute 線路的工作流程 | Microsoft Docs"
description: "此頁面會引導您完成設定 ExpressRoute 線路的工作流程"
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="dd778-103">ExpressRoute 工作流程線路佈建和線路狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="dd778-104">這個頁面以高階觀點引導您完成服務佈建和路由設定的工作流程。</span><span class="sxs-lookup"><span data-stu-id="dd778-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="dd778-105">下圖和對應的步驟顯示佈建端對端 ExpressRoute 線路所必須執行的工作。</span><span class="sxs-lookup"><span data-stu-id="dd778-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="dd778-106">使用 PowerShell 來設定 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="dd778-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="dd778-107">如需更多詳細資料，請依照 [建立 ExpressRoute 線路](expressroute-howto-circuit-classic.md) 一文中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="dd778-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="dd778-108">向服務提供者訂購連線能力。</span><span class="sxs-lookup"><span data-stu-id="dd778-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="dd778-109">此過程視情況而異。</span><span class="sxs-lookup"><span data-stu-id="dd778-109">This process varies.</span></span> <span data-ttu-id="dd778-110">如需有關如何訂購連線能力的詳細資訊，請連絡連線提供者。</span><span class="sxs-lookup"><span data-stu-id="dd778-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="dd778-111">請透過 PowerShell 驗證 ExpressRoute 線路佈建狀態，以確定線路已佈建成功。</span><span class="sxs-lookup"><span data-stu-id="dd778-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="dd778-112">設定路由網域。</span><span class="sxs-lookup"><span data-stu-id="dd778-112">Configure routing domains.</span></span> <span data-ttu-id="dd778-113">如果連線提供者為您管理第 3 層，他們會為您的線路設定路由。</span><span class="sxs-lookup"><span data-stu-id="dd778-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="dd778-114">如果連線提供者只提供第 2 層服務，您必須根據[路由需求](expressroute-routing.md)和[路由組態](expressroute-howto-routing-classic.md)頁面所述的指導方針來設定路由。</span><span class="sxs-lookup"><span data-stu-id="dd778-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="dd778-115">啟用 Azure 私用對等 - 您必須啟用此對等，才能連接到部署在虛擬網路內的 VM / 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="dd778-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="dd778-116">啟用 Azure 公用對等 - 如果您想要連接到裝載於公用 IP 位址的 Azure 服務，則必須啟用 Azure 公用對等。</span><span class="sxs-lookup"><span data-stu-id="dd778-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="dd778-117">如果您已選擇啟用 Azure 私用對等的預設路由，則這是存取 Azure 資源的條件。</span><span class="sxs-lookup"><span data-stu-id="dd778-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="dd778-118">啟用 Microsoft 對等 - 您必須啟用此對等，才能存取 Office 365 和 Dynamics 365。</span><span class="sxs-lookup"><span data-stu-id="dd778-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="dd778-119">必須確定您使用個別的 Proxy / 邊緣來連接到 Microsoft，而不是您用於網際網路的 Proxy / 邊緣。</span><span class="sxs-lookup"><span data-stu-id="dd778-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="dd778-120">ExpressRoute 和網際網路使用相同的邊緣會導致路由不對稱，並造成網路連線中斷。</span><span class="sxs-lookup"><span data-stu-id="dd778-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="dd778-121">將虛擬網路連結到 ExpressRoute 線路 - 您可以將虛擬網路連結到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="dd778-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="dd778-122">請依照指示 [連結 VNet](expressroute-howto-linkvnet-arm.md) 到您的線路。</span><span class="sxs-lookup"><span data-stu-id="dd778-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="dd778-123">這些 VNet 可以與 ExpressRoute 線路位於相同的 Azure 訂用帳戶中，也可以在不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="dd778-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="dd778-124">ExpressRoute 線路佈建狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="dd778-125">每個 ExpressRoute 線路有兩種狀態：</span><span class="sxs-lookup"><span data-stu-id="dd778-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="dd778-126">服務提供者佈建狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-126">Service provider provisioning state</span></span>
* <span data-ttu-id="dd778-127">狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-127">Status</span></span>

<span data-ttu-id="dd778-128">Status 代表 Microsoft 的佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="dd778-129">這個屬性會在您建立 Expressroute 循環時設定為 [Enabled]</span><span class="sxs-lookup"><span data-stu-id="dd778-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="dd778-130">連線提供者佈建狀態代表連線提供者那端的狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="dd778-131">可能是 *NotProvisioned*、*Provisioning* 或 *Provisioned*。</span><span class="sxs-lookup"><span data-stu-id="dd778-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="dd778-132">ExpressRoute 線路必須處於 Provisioned 狀態，才可供您使用。</span><span class="sxs-lookup"><span data-stu-id="dd778-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="dd778-133">ExpressRoute 線路的可能狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="dd778-134">本節列出 ExpressRoute 線路的可能狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="dd778-135">**在建立時**</span><span class="sxs-lookup"><span data-stu-id="dd778-135">**At creation time**</span></span>

<span data-ttu-id="dd778-136">執行 PowerShell Cmdlet 建立 ExpressRoute 線路後，您很快就會看到 ExpressRoute 線路處於下列狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="dd778-137">**當連線提供者正在佈建線路時**</span><span class="sxs-lookup"><span data-stu-id="dd778-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="dd778-138">當您將服務金鑰傳遞給連線提供者且他們也啟動佈建程序時，您快很就會看到 ExpressRoute 線路處於下列狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="dd778-139">**當連線提供者完成佈建程序時**</span><span class="sxs-lookup"><span data-stu-id="dd778-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="dd778-140">當連線提供者完成佈建程序後，您快很就會看到 ExpressRoute 線路處於下列狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="dd778-141">線路只能處於 Provisioned 和 Enabled 狀態下，才可供您使用。</span><span class="sxs-lookup"><span data-stu-id="dd778-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="dd778-142">如果您使用第 2 層提供者，則只有當線路處於此狀態下，您才能設定路由。</span><span class="sxs-lookup"><span data-stu-id="dd778-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="dd778-143">**當連線提供者正在取消佈建循環時**</span><span class="sxs-lookup"><span data-stu-id="dd778-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="dd778-144">如果您要求服務提供者取消佈建 ExpressRoute 循環，則當服務提供者完成取消佈建程序後，您將會看到已將循環設定為下列狀態。</span><span class="sxs-lookup"><span data-stu-id="dd778-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="dd778-145">如有需要，您可以選擇重新啟用線路，或執行 PowerShell Cmdlet 刪除線路。</span><span class="sxs-lookup"><span data-stu-id="dd778-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="dd778-146">如果您在 ServiceProviderProvisioningState 為 Provisioning 或 Provisioned 時執行 PowerShell Cmdlet 來刪除循環，作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="dd778-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="dd778-147">請和您的連線提供者合作，先取消佈建 ExpressRoute 循環，然後再刪除循環。</span><span class="sxs-lookup"><span data-stu-id="dd778-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="dd778-148">Microsoft 將持續收取循環費用，直到您執行 PowerShell Cmdlet 來取消循環為止。</span><span class="sxs-lookup"><span data-stu-id="dd778-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="dd778-149">路由工作階段組態狀態</span><span class="sxs-lookup"><span data-stu-id="dd778-149">Routing session configuration state</span></span>
<span data-ttu-id="dd778-150">BGP 佈建狀態可讓您知道 Microsoft 邊緣是否已啟用 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="dd778-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="dd778-151">必須是已啟用的狀態，您才能使用對等。</span><span class="sxs-lookup"><span data-stu-id="dd778-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="dd778-152">務必檢查 BGP 工作階段狀態，特別是 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="dd778-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="dd778-153">除了 BGP 佈建狀態，還有另一個狀態稱為 *已公告公用首碼狀態*。</span><span class="sxs-lookup"><span data-stu-id="dd778-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="dd778-154">已公告公用首碼狀態必須是 *已設定* 狀態，BGP 工作階段才能啟動，路由也才能端對端運作。</span><span class="sxs-lookup"><span data-stu-id="dd778-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="dd778-155">如果已公告公用首碼狀態設為 *需要驗證* 狀態，則不會啟用 BGP 工作階段，因為已公告的首碼不符合任何路由登錄中的 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="dd778-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="dd778-156">如果公告的公用首碼狀態是 *手動驗證* 狀態，您必須向 [Microsoft 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 開啟支援票證，並提供您擁有公告的 IP 位址的證明，以及相關聯的自發系統編號。</span><span class="sxs-lookup"><span data-stu-id="dd778-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dd778-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd778-157">Next steps</span></span>
* <span data-ttu-id="dd778-158">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="dd778-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="dd778-159">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="dd778-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="dd778-160">設定路由</span><span class="sxs-lookup"><span data-stu-id="dd778-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="dd778-161">將 VNet 連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="dd778-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

