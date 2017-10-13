---
title: "aaaAzure ExpressRoute 線路和路由網域 |Microsoft 文件"
description: "此頁面會提供 ExpressRoute 線路和 hello 路由網域的概觀。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a><span data-ttu-id="09685-103">ExpressRoute 線路和路由網域</span><span class="sxs-lookup"><span data-stu-id="09685-103">ExpressRoute circuits and routing domains</span></span>
 <span data-ttu-id="09685-104">您必須訂購*ExpressRoute 電路*tooconnect 您在內部部署基礎結構 tooMicrosoft，透過連線服務提供者。</span><span class="sxs-lookup"><span data-stu-id="09685-104">You must order an *ExpressRoute circuit* tooconnect your on-premises infrastructure tooMicrosoft through a connectivity provider.</span></span> <span data-ttu-id="09685-105">hello 圖提供您的 WAN 與 Microsoft 之間連線的邏輯表示法。</span><span class="sxs-lookup"><span data-stu-id="09685-105">hello figure below provides a logical representation of connectivity between your WAN and Microsoft.</span></span>

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a><span data-ttu-id="09685-106">ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="09685-106">ExpressRoute circuits</span></span>
<span data-ttu-id="09685-107">*ExpressRoute 線路* 代表內部部署基礎結構與 Microsoft 雲端服務之間透過連線提供者的邏輯連線。</span><span class="sxs-lookup"><span data-stu-id="09685-107">An *ExpressRoute circuit* represents a logical connection between your on-premises infrastructure and Microsoft cloud services through a connectivity provider.</span></span> <span data-ttu-id="09685-108">您可以訂購多條 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="09685-108">You can order multiple ExpressRoute circuits.</span></span> <span data-ttu-id="09685-109">每個 expressroute 電路可以在 hello 相同或不同區域，而且可以透過不同的連接提供者的連接的 tooyour 內部部署。</span><span class="sxs-lookup"><span data-stu-id="09685-109">Each circuit can be in hello same or different regions, and can be connected tooyour premises through different connectivity providers.</span></span> 

<span data-ttu-id="09685-110">ExpressRoute 電路並對應 tooany 實際的實體。</span><span class="sxs-lookup"><span data-stu-id="09685-110">ExpressRoute circuits do not map tooany physical entities.</span></span> <span data-ttu-id="09685-111">線路由一個稱為服務金鑰 (s 金鑰) 的標準 GUID 唯一識別。</span><span class="sxs-lookup"><span data-stu-id="09685-111">A circuit is uniquely identified by a standard GUID called as a service key (s-key).</span></span> <span data-ttu-id="09685-112">hello 服務金鑰是唯一 Microsoft、 hello 連線服務提供者與您之間交換資訊 hello。</span><span class="sxs-lookup"><span data-stu-id="09685-112">hello service key is hello only piece of information exchanged between Microsoft, hello connectivity provider, and you.</span></span> <span data-ttu-id="09685-113">hello s 鍵不是基於安全的密碼。</span><span class="sxs-lookup"><span data-stu-id="09685-113">hello s-key is not a secret for security purposes.</span></span> <span data-ttu-id="09685-114">沒有 1:1 之間的對應的 ExpressRoute 電路並 hello s 鍵。</span><span class="sxs-lookup"><span data-stu-id="09685-114">There is a 1:1 mapping between an ExpressRoute circuit and hello s-key.</span></span>

<span data-ttu-id="09685-115">ExpressRoute 電路可以有向上 toothree 獨立的對等互連： Azure 的公用、 Azure 私人和 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="09685-115">An ExpressRoute circuit can have up toothree independent peerings: Azure public, Azure private, and Microsoft.</span></span> <span data-ttu-id="09685-116">每個對等為一組獨立的 BGP 工作階段，每個都重複設定，以確保較高的可用性。</span><span class="sxs-lookup"><span data-stu-id="09685-116">Each peering is a pair of independent BGP sessions each of them configured redundantly for high availability.</span></span> <span data-ttu-id="09685-117">ExpressRoute 線路與路由網域之間存在 1:N (1 <= N <= 3) 對應。</span><span class="sxs-lookup"><span data-stu-id="09685-117">There is a 1:N (1 <= N <= 3) mapping between an ExpressRoute circuit and routing domains.</span></span> <span data-ttu-id="09685-118">每個 ExpressRoute 電路可以啟用任何一個、兩個或全部三個對等。</span><span class="sxs-lookup"><span data-stu-id="09685-118">An ExpressRoute circuit can have any one, two, or all three peerings enabled per ExpressRoute circuit.</span></span>

<span data-ttu-id="09685-119">每個 expressroute 電路具有固定的頻寬 （50 Mbps、 100 Mbps、 200 Mbps、 500 Mbps、 1 Gbps、 10 Gbps），而且是對應的 tooa 連線服務提供者和對等互連位置。</span><span class="sxs-lookup"><span data-stu-id="09685-119">Each circuit has a fixed bandwidth (50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 10 Gbps) and is mapped tooa connectivity provider and a peering location.</span></span> <span data-ttu-id="09685-120">您選取的 hello 頻寬會共用所有的 hello 對等互連 hello 循環之間。</span><span class="sxs-lookup"><span data-stu-id="09685-120">hello bandwidth you select is shared across all hello peerings for hello circuit.</span></span> 

### <a name="quotas-limits-and-limitations"></a><span data-ttu-id="09685-121">配額和限制</span><span class="sxs-lookup"><span data-stu-id="09685-121">Quotas, limits, and limitations</span></span>
<span data-ttu-id="09685-122">每個 ExpressRoute 線路會套用預設的配額和限制。</span><span class="sxs-lookup"><span data-stu-id="09685-122">Default quotas and limits apply for every ExpressRoute circuit.</span></span> <span data-ttu-id="09685-123">請參閱 toohello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)頁面以取得最新配額的資訊。</span><span class="sxs-lookup"><span data-stu-id="09685-123">Refer toohello [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md) page for up-to-date information on quotas.</span></span>

## <a name="expressroute-routing-domains"></a><span data-ttu-id="09685-124">ExpressRoute 路由網域</span><span class="sxs-lookup"><span data-stu-id="09685-124">ExpressRoute routing domains</span></span>
<span data-ttu-id="09685-125">ExpressRoute 線路有多個相關聯的路由網域：Azure 公用、Azure 私用和 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="09685-125">An ExpressRoute circuit has multiple routing domains associated with it: Azure public, Azure private, and Microsoft.</span></span> <span data-ttu-id="09685-126">每一個 hello 路由網域都設定相同的路由器對上 (主動 / 主動或載入共用組態) 的高可用性。</span><span class="sxs-lookup"><span data-stu-id="09685-126">Each of hello routing domains is configured identically on a pair of routers (in active-active or load sharing configuration) for high availability.</span></span> <span data-ttu-id="09685-127">Azure 服務都會分類成*Azure 公用*和*Azure 私用*toorepresent hello IP 定址配置。</span><span class="sxs-lookup"><span data-stu-id="09685-127">Azure services are categorized as *Azure public* and *Azure private* toorepresent hello IP addressing schemes.</span></span>

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a><span data-ttu-id="09685-128">私人對等互連</span><span class="sxs-lookup"><span data-stu-id="09685-128">Private peering</span></span>
<span data-ttu-id="09685-129">Azure 計算服務，也就是虛擬機器 (IaaS) 和虛擬網路內部署的雲端服務 (PaaS)，可以透過 hello 私用對等網域連接。</span><span class="sxs-lookup"><span data-stu-id="09685-129">Azure compute services, namely virtual machines (IaaS) and cloud services (PaaS), that are deployed within a virtual network can be connected through hello private peering domain.</span></span> <span data-ttu-id="09685-130">hello 私用對等網域被視為 toobe 核心網路的受信任的擴充至 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="09685-130">hello private peering domain is considered toobe a trusted extension of your core network into Microsoft Azure.</span></span> <span data-ttu-id="09685-131">您可以在核心網路與 Azure 虛擬網路 (VNet) 之間設定雙向連線。</span><span class="sxs-lookup"><span data-stu-id="09685-131">You can set up bi-directional connectivity between your core network and Azure virtual networks (VNets).</span></span> <span data-ttu-id="09685-132">此對等互連，可讓您連接 toovirtual 機器和雲端服務，直接在其私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09685-132">This peering lets you connect toovirtual machines and cloud services directly on their private IP addresses.</span></span>  

<span data-ttu-id="09685-133">您可以連接多個虛擬網路 toohello 私用對等網域。</span><span class="sxs-lookup"><span data-stu-id="09685-133">You can connect more than one virtual network toohello private peering domain.</span></span> <span data-ttu-id="09685-134">檢閱 hello[常見問題集頁面](expressroute-faqs.md)有關限制和限制的資訊。</span><span class="sxs-lookup"><span data-stu-id="09685-134">Review hello [FAQ page](expressroute-faqs.md) for information on limits and limitations.</span></span> <span data-ttu-id="09685-135">您可以瀏覽 hello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)頁面以取得有關限制的最新狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="09685-135">You can visit hello [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md) page for up-to-date information on limits.</span></span>  <span data-ttu-id="09685-136">請參閱 toohello[路由](expressroute-routing.md)路由組態的詳細資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="09685-136">Refer toohello [Routing](expressroute-routing.md) page for detailed information on routing configuration.</span></span>

### <a name="public-peering"></a><span data-ttu-id="09685-137">公用對等互連</span><span class="sxs-lookup"><span data-stu-id="09685-137">Public peering</span></span>
<span data-ttu-id="09685-138">公用 IP 位址上提供如 Azure 儲存體、SQL Database 和網站等服務。</span><span class="sxs-lookup"><span data-stu-id="09685-138">Services such as Azure Storage, SQL databases, and Websites are offered on public IP addresses.</span></span> <span data-ttu-id="09685-139">您可以私下連接 tooservices 裝載於公用 IP 位址，包括您的雲端服務，透過 hello 公用對等互連路由網域的 Vip。</span><span class="sxs-lookup"><span data-stu-id="09685-139">You can privately connect tooservices hosted on public IP addresses, including VIPs of your cloud services, through hello public peering routing domain.</span></span> <span data-ttu-id="09685-140">您可以連接 hello 公用對等網域 tooyour 周邊網路，並連接 tooall Azure 服務，您不需要 tooconnect 透過 WAN 從其公用 IP 位址上的 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="09685-140">You can connect hello public peering domain tooyour DMZ and connect tooall Azure services on their public IP addresses from your WAN without having tooconnect through hello internet.</span></span> 

<span data-ttu-id="09685-141">連線一律會從您的 WAN tooMicrosoft Azure 起始服務。</span><span class="sxs-lookup"><span data-stu-id="09685-141">Connectivity is always initiated from your WAN tooMicrosoft Azure services.</span></span> <span data-ttu-id="09685-142">Microsoft Azure 服務不會無法 tooinitiate 您透過此路由網域的網路連線。</span><span class="sxs-lookup"><span data-stu-id="09685-142">Microsoft Azure services will not be able tooinitiate connections into your network through this routing domain.</span></span> <span data-ttu-id="09685-143">啟用公用對等互連時，才能夠 tooconnect tooall Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="09685-143">Once public peering is enabled, you will be able tooconnect tooall Azure services.</span></span> <span data-ttu-id="09685-144">我們不允許您 tooselectively 挑選服務，我們會通告的路由。</span><span class="sxs-lookup"><span data-stu-id="09685-144">We do not allow you tooselectively pick services for which we advertise routes to.</span></span> <span data-ttu-id="09685-145">您可以檢閱我們通告 tooyou 透過 hello 此對等的前置詞的 hello 清單[Microsoft Azure Datacenter IP 範圍](http://www.microsoft.com/download/details.aspx?id=41653)頁面。</span><span class="sxs-lookup"><span data-stu-id="09685-145">You can review hello list of prefixes we advertise tooyou through this peering on hello [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653) page.</span></span> <span data-ttu-id="09685-146">hello 頁面會每週更新。</span><span class="sxs-lookup"><span data-stu-id="09685-146">hello page is updated weekly.</span></span>

<span data-ttu-id="09685-147">您可以定義自訂的路由篩選您的網路 tooconsume 只有 hello 路由您需要內。</span><span class="sxs-lookup"><span data-stu-id="09685-147">You can define custom route filters within your network tooconsume only hello routes you need.</span></span> <span data-ttu-id="09685-148">請參閱 toohello[路由](expressroute-routing.md)路由組態的詳細資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="09685-148">Refer toohello [Routing](expressroute-routing.md) page for detailed information on routing configuration.</span></span> 

<span data-ttu-id="09685-149">請參閱 hello[常見問題集頁面](expressroute-faqs.md)如需有關支援透過 hello 公用對等互連路由網域的服務。</span><span class="sxs-lookup"><span data-stu-id="09685-149">See hello [FAQ page](expressroute-faqs.md) for more information on services supported through hello public peering routing domain.</span></span> 

### <a name="microsoft-peering"></a><span data-ttu-id="09685-150">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="09685-150">Microsoft peering</span></span>
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

<span data-ttu-id="09685-151">連線 tooall 其他 Microsoft online services （例如 Office 365 服務） 會透過 hello Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="09685-151">Connectivity tooall other Microsoft online services (such as Office 365 services) will be through hello Microsoft peering.</span></span> <span data-ttu-id="09685-152">我們啟用您 WAN 和 Microsoft 雲端服務之間透過 hello Microsoft 對等互連的路由網域的雙向連線。</span><span class="sxs-lookup"><span data-stu-id="09685-152">We enable bi-directional connectivity between your WAN and Microsoft cloud services through hello Microsoft peering routing domain.</span></span> <span data-ttu-id="09685-153">您必須連接 tooMicrosoft 雲端服務僅透過由您或您連線服務提供者所擁有的公用 IP 位址，您必須遵守 tooall hello 定義規則。</span><span class="sxs-lookup"><span data-stu-id="09685-153">You must connect tooMicrosoft cloud services only over public IP addresses that are owned by you or your connectivity provider and you must adhere tooall hello defined rules.</span></span> <span data-ttu-id="09685-154">請參閱 hello [ExpressRoute 必要條件](expressroute-prerequisites.md)頁面以取得詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="09685-154">See hello [ExpressRoute prerequisites](expressroute-prerequisites.md) page for more information.</span></span>

<span data-ttu-id="09685-155">請參閱 hello[常見問題集頁面](expressroute-faqs.md)的更多有關支援的服務、 成本與組態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="09685-155">See hello [FAQ page](expressroute-faqs.md) for more information on services supported, costs, and configuration details.</span></span> <span data-ttu-id="09685-156">請參閱 hello [ExpressRoute 位置](expressroute-locations.md)hello 清單上的 Microsoft 對等互連支援供應項目連線提供者的資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="09685-156">See hello [ExpressRoute Locations](expressroute-locations.md) page for information on hello list of connectivity providers offering Microsoft peering support.</span></span>

## <a name="routing-domain-comparison"></a><span data-ttu-id="09685-157">路由網域的比較</span><span class="sxs-lookup"><span data-stu-id="09685-157">Routing domain comparison</span></span>
<span data-ttu-id="09685-158">hello 表比較 hello 三個路由網域。</span><span class="sxs-lookup"><span data-stu-id="09685-158">hello table below compares hello three routing domains.</span></span>

|  | <span data-ttu-id="09685-159">**私人對等互連**</span><span class="sxs-lookup"><span data-stu-id="09685-159">**Private Peering**</span></span> | <span data-ttu-id="09685-160">**公用對等互連**</span><span class="sxs-lookup"><span data-stu-id="09685-160">**Public Peering**</span></span> | <span data-ttu-id="09685-161">**Microsoft 對等互連**</span><span class="sxs-lookup"><span data-stu-id="09685-161">**Microsoft Peering**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09685-162">**每個對等支援的前置詞數目最大值**</span><span class="sxs-lookup"><span data-stu-id="09685-162">**Max. # prefixes supported per peering**</span></span> |<span data-ttu-id="09685-163">預設為 4000，ExpressRoute Premium 中為 10000</span><span class="sxs-lookup"><span data-stu-id="09685-163">4000 by default, 10,000 with ExpressRoute Premium</span></span> |<span data-ttu-id="09685-164">200</span><span class="sxs-lookup"><span data-stu-id="09685-164">200</span></span> |<span data-ttu-id="09685-165">200</span><span class="sxs-lookup"><span data-stu-id="09685-165">200</span></span> |
| <span data-ttu-id="09685-166">**支援的 IP 位址範圍**</span><span class="sxs-lookup"><span data-stu-id="09685-166">**IP address ranges supported**</span></span> |<span data-ttu-id="09685-167">您的 WAN 內任何有效的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="09685-167">Any valid IPv4 address within your WAN.</span></span> |<span data-ttu-id="09685-168">您或您的連線提供者所擁有的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="09685-168">Public IPv4 addresses owned by you or your connectivity provider.</span></span> |<span data-ttu-id="09685-169">您或您的連線提供者所擁有的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="09685-169">Public IPv4 addresses owned by you or your connectivity provider.</span></span> |
| <span data-ttu-id="09685-170">**AS 編號需求**</span><span class="sxs-lookup"><span data-stu-id="09685-170">**AS Number requirements**</span></span> |<span data-ttu-id="09685-171">私密和公用 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="09685-171">Private and public AS numbers.</span></span> <span data-ttu-id="09685-172">您必須擁有 hello 公用如果您選擇其中一個 toouse 的數字。</span><span class="sxs-lookup"><span data-stu-id="09685-172">You must own hello public AS number if you choose toouse one.</span></span> |<span data-ttu-id="09685-173">私密和公用 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="09685-173">Private and public AS numbers.</span></span> <span data-ttu-id="09685-174">不過，您必須證明公用 IP 位址的擁有權。</span><span class="sxs-lookup"><span data-stu-id="09685-174">However, you must prove ownership of public IP addresses.</span></span> |<span data-ttu-id="09685-175">私密和公用 AS 編號。</span><span class="sxs-lookup"><span data-stu-id="09685-175">Private and public AS numbers.</span></span> <span data-ttu-id="09685-176">不過，您必須證明公用 IP 位址的擁有權。</span><span class="sxs-lookup"><span data-stu-id="09685-176">However, you must prove ownership of public IP addresses.</span></span> |
| <span data-ttu-id="09685-177">**路由介面 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="09685-177">**Routing Interface IP addresses**</span></span> |<span data-ttu-id="09685-178">RFC1918 和公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="09685-178">RFC1918 and public IP addresses</span></span> |<span data-ttu-id="09685-179">公用 IP 位址已註冊的 tooyou 路由登錄中。</span><span class="sxs-lookup"><span data-stu-id="09685-179">Public IP addresses registered tooyou in routing registries.</span></span> |<span data-ttu-id="09685-180">公用 IP 位址已註冊的 tooyou 路由登錄中。</span><span class="sxs-lookup"><span data-stu-id="09685-180">Public IP addresses registered tooyou in routing registries.</span></span> |
| <span data-ttu-id="09685-181">**MD5 雜湊支援**</span><span class="sxs-lookup"><span data-stu-id="09685-181">**MD5 Hash support**</span></span> |<span data-ttu-id="09685-182">是</span><span class="sxs-lookup"><span data-stu-id="09685-182">Yes</span></span> |<span data-ttu-id="09685-183">是</span><span class="sxs-lookup"><span data-stu-id="09685-183">Yes</span></span> |<span data-ttu-id="09685-184">是</span><span class="sxs-lookup"><span data-stu-id="09685-184">Yes</span></span> |

<span data-ttu-id="09685-185">您可以選擇一或多個路由網域的 hello tooenable ExpressRoute 電路的一部分。</span><span class="sxs-lookup"><span data-stu-id="09685-185">You can choose tooenable one or more of hello routing domains as part of your ExpressRoute circuit.</span></span> <span data-ttu-id="09685-186">您可以選擇 toohave 所有 hello 路由網域打 hello 相同的 VPN，如果您想 toocombine 為單一路由網域。</span><span class="sxs-lookup"><span data-stu-id="09685-186">You can choose toohave all hello routing domains put on hello same VPN if you want toocombine them into a single routing domain.</span></span> <span data-ttu-id="09685-187">您也可以將它們放在不同的路由網域，類似 toohello 圖表上。</span><span class="sxs-lookup"><span data-stu-id="09685-187">You can also put them on different routing domains, similar toohello diagram.</span></span> <span data-ttu-id="09685-188">hello 建議設定是該私人互連已連接直接 toohello 核心網路，而且 hello 公用及 Microsoft 對等互連連結是連接的 tooyour 周邊網路。</span><span class="sxs-lookup"><span data-stu-id="09685-188">hello recommended configuration is that private peering is connected directly toohello core network, and hello public and Microsoft peering links are connected tooyour DMZ.</span></span>

<span data-ttu-id="09685-189">如果您選擇 toohave 所有三個對等互連工作階段，您必須有三組 BGP 工作階段 （每個對等互連類型的一組）。</span><span class="sxs-lookup"><span data-stu-id="09685-189">If you choose toohave all three peering sessions, you must have three pairs of BGP sessions (one pair for each peering type).</span></span> <span data-ttu-id="09685-190">hello BGP 工作階段組可提供高度可用的連結。</span><span class="sxs-lookup"><span data-stu-id="09685-190">hello BGP session pairs provide a highly available link.</span></span> <span data-ttu-id="09685-191">如果您透過第 2 層連線提供者來連線，則要負責設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="09685-191">If you are connecting through layer 2 connectivity providers, you will be responsible for configuring and managing routing.</span></span> <span data-ttu-id="09685-192">您可以進一步檢閱 hello[工作流程](expressroute-workflows.md)設定 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="09685-192">You can learn more by reviewing hello [workflows](expressroute-workflows.md) for setting up ExpressRoute.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09685-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09685-193">Next steps</span></span>
* <span data-ttu-id="09685-194">尋找服務提供者。</span><span class="sxs-lookup"><span data-stu-id="09685-194">Find a service provider.</span></span> <span data-ttu-id="09685-195">請參閱 [ExpressRoute 服務提供者和位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="09685-195">See [ExpressRoute service providers and locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="09685-196">請確定符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="09685-196">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="09685-197">請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="09685-197">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="09685-198">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="09685-198">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="09685-199">建立和管理 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="09685-199">Create and manage ExpressRoute circuits</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="09685-200">設定 ExpressRoute 線路的路由 (對等戶連)</span><span class="sxs-lookup"><span data-stu-id="09685-200">Configure routing (peering) for ExpressRoute circuits</span></span>](expressroute-howto-routing-portal-resource-manager.md)
