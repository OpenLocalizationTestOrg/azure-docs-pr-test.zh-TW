---
title: "ExpressRoute 線路的 NAT 需求 | Microsoft Docs"
description: "此頁面提供為 ExpressRoute 線路設定和管理 NAT 的詳細需求。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: d3de566ff2825ef0c41d88d4a86157dc23d9f46b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-nat-requirements"></a><span data-ttu-id="6a126-103">ExpressRoute NAT 需求</span><span class="sxs-lookup"><span data-stu-id="6a126-103">ExpressRoute NAT requirements</span></span>
<span data-ttu-id="6a126-104">若要使用 ExpressRoute 連線到 Microsoft 雲端服務，您必須設定和管理 NAT。</span><span class="sxs-lookup"><span data-stu-id="6a126-104">To connect to Microsoft cloud services using ExpressRoute, you’ll need to set up and manage NATs.</span></span> <span data-ttu-id="6a126-105">有些連線提供者會以受管理的服務來支援設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="6a126-105">Some connectivity providers offer setting up and managing NAT as a managed service.</span></span> <span data-ttu-id="6a126-106">請洽詢您的連線服務提供者，以查看他們是否提供這類服務。</span><span class="sxs-lookup"><span data-stu-id="6a126-106">Check with your connectivity provider to see if they offer such a service.</span></span> <span data-ttu-id="6a126-107">如果沒有，您必須遵守以下所述的需求。</span><span class="sxs-lookup"><span data-stu-id="6a126-107">If not, you must adhere to the requirements described below.</span></span> 

<span data-ttu-id="6a126-108">如需不同路由網域的概觀，請檢閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="6a126-108">Review the [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) page to get an overview of the various routing domains.</span></span> <span data-ttu-id="6a126-109">為了符合 Azure 公用和 Microsoft 對等的公用 IP 位址需求，建議在您的網路與 Microsoft 之間設定 NAT。</span><span class="sxs-lookup"><span data-stu-id="6a126-109">To meet the public IP address requirements for Azure public and Microsoft peering, we recommend that you set up NAT between your network and Microsoft.</span></span> <span data-ttu-id="6a126-110">本節提供您需要設定的 NAT 基礎結構的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="6a126-110">This section provides a detailed description of the NAT infrastructure you need to set up.</span></span>

## <a name="nat-requirements-for-azure-public-peering"></a><span data-ttu-id="6a126-111">Azure 公用對等的 NAT 需求</span><span class="sxs-lookup"><span data-stu-id="6a126-111">NAT requirements for Azure public peering</span></span>
<span data-ttu-id="6a126-112">Azure 公用對等路徑可讓您連接到裝載於 Azure 中的所有服務的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6a126-112">The Azure public peering path enables you to connect to all services hosted in Azure over their public IP addresses.</span></span> <span data-ttu-id="6a126-113">其中包括 [ExpessRoute 常見問題集](expressroute-faqs.md) 列出的服務，以及由 ISV 裝載於 Microsoft Azure 上的任何服務。</span><span class="sxs-lookup"><span data-stu-id="6a126-113">These include services listed in the [ExpessRoute FAQ](expressroute-faqs.md) and any services hosted by ISVs on Microsoft Azure.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6a126-114">連線到公用對等的 Microsoft Azure 服務時，一律是從您的網路出發到 Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="6a126-114">Connectivity to Microsoft Azure services on public peering is always initiated from your network into the Microsoft network.</span></span> <span data-ttu-id="6a126-115">因此，無法透過 ExpressRoute 從 Microsoft Azure 服務將工作階段起始到您的網路。</span><span class="sxs-lookup"><span data-stu-id="6a126-115">Therefore, sessions cannot be initiated from Microsoft Azure services to your network over ExpressRoute.</span></span> <span data-ttu-id="6a126-116">若已嘗試這麼做，傳送至這些通知 IP 的封包將使用網際網路，而不是 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="6a126-116">If attempted, packets sent to these advertised IPs will use the internet instead of ExpressRoute.</span></span>
> 

<span data-ttu-id="6a126-117">以公用對等的 Microsoft Azure 為目的地的流量，必須由 SNAT 轉譯成有效的公用 IPv4 位址，才能進入 Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="6a126-117">Traffic destined to Microsoft Azure on public peering must be SNATed to valid public IPv4 addresses before they enter the Microsoft network.</span></span> <span data-ttu-id="6a126-118">下圖提供如何設定 NAT 以符合上述需求的高階圖片。</span><span class="sxs-lookup"><span data-stu-id="6a126-118">The figure below provides a high-level picture of how the NAT could be set up to meet the above requirement.</span></span>

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a><span data-ttu-id="6a126-119">NAT IP 集區和路由通告</span><span class="sxs-lookup"><span data-stu-id="6a126-119">NAT IP pool and route advertisements</span></span>
<span data-ttu-id="6a126-120">您必須確定流量進入的 Azure 公用對等路徑具備有效的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="6a126-120">You must ensure that traffic is entering the Azure public peering path with valid public IPv4 address.</span></span> <span data-ttu-id="6a126-121">Microsoft 必須能夠向區域路由網際網路登錄 (RIR) 和網際網路路由登錄 (IRR) 驗證 IPv4 NAT 位址集區的擁有權。</span><span class="sxs-lookup"><span data-stu-id="6a126-121">Microsoft must be able to validate the ownership of the IPv4 NAT address pool against a regional routing Internet registry (RIR) or an Internet routing registry (IRR).</span></span> <span data-ttu-id="6a126-122">將會根據所比對的 AS 編號和用於 NAT 的 IP 位址執行檢查。</span><span class="sxs-lookup"><span data-stu-id="6a126-122">A check will be performed based on the AS number being peered with and the IP addresses used for the NAT.</span></span> <span data-ttu-id="6a126-123">如需路由登錄的詳細資訊，請參閱 [ExpressRoute 路由需求](expressroute-routing.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="6a126-123">Refer to the [ExpressRoute routing requirements](expressroute-routing.md) page for information on routing registries.</span></span>

<span data-ttu-id="6a126-124">透過此對等公告的 NAT IP 首碼長度沒有限制。</span><span class="sxs-lookup"><span data-stu-id="6a126-124">There are no restrictions on the length of the NAT IP prefix advertised through this peering.</span></span> <span data-ttu-id="6a126-125">您必須監視 NAT 集區，確保您未耗盡 NAT 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6a126-125">You must monitor the NAT pool and ensure that you are not starved of NAT sessions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a126-126">向 Microsoft 公告的 NAT IP 集區不得向網際網路公告。</span><span class="sxs-lookup"><span data-stu-id="6a126-126">The NAT IP pool advertised to Microsoft must not be advertised to the Internet.</span></span> <span data-ttu-id="6a126-127">這樣會中斷其他 Microsoft 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="6a126-127">This will break connectivity to other Microsoft services.</span></span>
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a><span data-ttu-id="6a126-128">Microsoft 對等的 NAT 需求</span><span class="sxs-lookup"><span data-stu-id="6a126-128">NAT requirements for Microsoft peering</span></span>
<span data-ttu-id="6a126-129">Microsoft 對等路徑可讓您連接到不支援透過 Azure 公用對等路徑存取的 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6a126-129">The Microsoft peering path lets you connect to Microsoft cloud services that are not supported through the Azure public peering path.</span></span> <span data-ttu-id="6a126-130">服務清單包括 Office 365 服務，例如 Exchange Online、SharePoint Online、商務用 Skype 和 Dynamics 365。</span><span class="sxs-lookup"><span data-stu-id="6a126-130">The list of services includes Office 365 services, such as Exchange Online, SharePoint Online, Skype for Business, and Dynamics 365.</span></span> <span data-ttu-id="6a126-131">Microsoft 預計在 Microsoft 對等上支援雙向連線能力。</span><span class="sxs-lookup"><span data-stu-id="6a126-131">Microsoft expects to support bi-directional connectivity on the Microsoft peering.</span></span> <span data-ttu-id="6a126-132">以 Microsoft 雲端服務為目的地的流量，必須由 SNAT 轉譯成有效的公用 IPv4 位址，才能進入 Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="6a126-132">Traffic destined to Microsoft cloud services must be SNATed to valid public IPv4 addresses before they enter the Microsoft network.</span></span> <span data-ttu-id="6a126-133">從 Microsoft 雲端服務送到您的網路的流量，必須在網際網路邊緣經過 SNAT 轉譯，才可防止[非對稱式路由](expressroute-asymmetric-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="6a126-133">Traffic destined to your network from Microsoft cloud services must be SNATed at your Internet edge to prevent [asymmetric routing](expressroute-asymmetric-routing.md).</span></span> <span data-ttu-id="6a126-134">下圖提供如何為 Microsoft 對等設定 NAT 的高階圖片。</span><span class="sxs-lookup"><span data-stu-id="6a126-134">The figure below provides a high-level picture of how the NAT should be setup for Microsoft peering.</span></span>

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-to-microsoft"></a><span data-ttu-id="6a126-135">從您的網路出發到 Microsoft 的流量</span><span class="sxs-lookup"><span data-stu-id="6a126-135">Traffic originating from your network destined to Microsoft</span></span>
* <span data-ttu-id="6a126-136">您必須確定流量進入的 Microsoft 對等路徑具備有效的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="6a126-136">You must ensure that traffic is entering the Microsoft peering path with a valid public IPv4 address.</span></span> <span data-ttu-id="6a126-137">Microsoft 必須能夠向區域路由網際網路登錄 (RIR) 和網際網路路由登錄 (IRR) 驗證 IPv4 NAT 位址集區的擁有者。</span><span class="sxs-lookup"><span data-stu-id="6a126-137">Microsoft must be able to validate the owner of the IPv4 NAT address pool against the regional routing internet registry (RIR) or an internet routing registry (IRR).</span></span> <span data-ttu-id="6a126-138">將會根據所比對的 AS 編號和用於 NAT 的 IP 位址執行檢查。</span><span class="sxs-lookup"><span data-stu-id="6a126-138">A check will be performed based on the AS number being peered with and the IP addresses used for the NAT.</span></span> <span data-ttu-id="6a126-139">如需路由登錄的詳細資訊，請參閱 [ExpressRoute 路由需求](expressroute-routing.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="6a126-139">Refer to the [ExpressRoute routing requirements](expressroute-routing.md) page for information on routing registries.</span></span>
* <span data-ttu-id="6a126-140">用於 Azure 公用對等設定和其他 ExpressRoute 線路的 IP 位址，不得透過 BGP 工作階段向 Microsoft 公告。</span><span class="sxs-lookup"><span data-stu-id="6a126-140">IP addresses used for the Azure public peering setup and other ExpressRoute circuits must not be advertised to Microsoft through the BGP session.</span></span> <span data-ttu-id="6a126-141">透過此對等公告的 NAT IP 首碼長度沒有限制。</span><span class="sxs-lookup"><span data-stu-id="6a126-141">There is no restriction on the length of the NAT IP prefix advertised through this peering.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="6a126-142">向 Microsoft 公告的 NAT IP 集區不得向網際網路公告。</span><span class="sxs-lookup"><span data-stu-id="6a126-142">The NAT IP pool advertised to Microsoft must not be advertised to the Internet.</span></span> <span data-ttu-id="6a126-143">這樣會中斷其他 Microsoft 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="6a126-143">This will break connectivity to other Microsoft services.</span></span>
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-to-your-network"></a><span data-ttu-id="6a126-144">從 Microsoft 出發到您的網路的流量</span><span class="sxs-lookup"><span data-stu-id="6a126-144">Traffic originating from Microsoft destined to your network</span></span>
* <span data-ttu-id="6a126-145">在某些情況下，需要由 Microsoft 對您網路中裝載的服務端點起始連線。</span><span class="sxs-lookup"><span data-stu-id="6a126-145">Certain scenarios require Microsoft to initiate connectivity to service endpoints hosted within your network.</span></span> <span data-ttu-id="6a126-146">常見的例子就是從 Office 365 連接到您網路中裝載的 ADFS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6a126-146">A typical example of the scenario would be connectivity to ADFS servers hosted in your network from Office 365.</span></span> <span data-ttu-id="6a126-147">在這種情況下，必須將您網路中適當的首碼透露給 Microsoft 對等。</span><span class="sxs-lookup"><span data-stu-id="6a126-147">In such cases, you must leak appropriate prefixes from your network into the Microsoft peering.</span></span> 
* <span data-ttu-id="6a126-148">您必須在網際網路邊緣進行 Microsoft 流量的 SNAT 轉譯，才可防止[非對稱式路由](expressroute-asymmetric-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="6a126-148">You must SNAT Microsoft traffic at the Internet edge for service endpoints within your network to prevent [asymmetric routing](expressroute-asymmetric-routing.md).</span></span> <span data-ttu-id="6a126-149">一律會透過 ExpressRoute 傳送具有一個目的地 IP 且符合透過 ExpressRoute 接收之路由的要求**和回覆**。</span><span class="sxs-lookup"><span data-stu-id="6a126-149">Requests **and replies** with a destination IP that match a route received via ExpressRoute will always be sent via ExpressRoute.</span></span> <span data-ttu-id="6a126-150">如果要求是透過網際網路收到，而回覆是透過 ExpressRoute 傳送，則存在非對稱式路由。</span><span class="sxs-lookup"><span data-stu-id="6a126-150">Asymmetric routing exists if the request is received via the Internet with the reply sent via ExpressRoute.</span></span> <span data-ttu-id="6a126-151">在網際網路邊緣進行 Microsoft 流量的 SNAT 轉譯，可強制回覆流量回到網際網路邊緣，進而解決問題。</span><span class="sxs-lookup"><span data-stu-id="6a126-151">SNATing the incoming Microsoft traffic at the Internet edge forces reply traffic back to the Internet edge, resolving the problem.</span></span>

![非對稱式路由與 ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a><span data-ttu-id="6a126-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a126-153">Next steps</span></span>
* <span data-ttu-id="6a126-154">請參閱[路由](expressroute-routing.md)和 [QoS](expressroute-qos.md) 的需求。</span><span class="sxs-lookup"><span data-stu-id="6a126-154">Refer to the requirements for [Routing](expressroute-routing.md) and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="6a126-155">如需工作流程資訊，請參閱 [ExpressRoute 線路佈建工作流程和線路狀態](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="6a126-155">For workflow information, see [ExpressRoute circuit provisioning workflows and circuit states](expressroute-workflows.md).</span></span>
* <span data-ttu-id="6a126-156">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="6a126-156">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="6a126-157">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="6a126-157">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="6a126-158">設定路由</span><span class="sxs-lookup"><span data-stu-id="6a126-158">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="6a126-159">將 VNet 連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="6a126-159">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

