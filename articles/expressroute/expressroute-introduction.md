---
title: "ExpressRoute 概觀：透過私人連線將內部部署網路延伸至 Azure | Microsoft Docs"
description: "此「ExpressRoute 技術概觀」說明 ExpressRoute 連線如何透過私人連線，將內部部署網路延伸至 Azure。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 7390462d79506e63989baadac2b2cee00eef325d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="expressroute-overview"></a><span data-ttu-id="04644-103">ExpressRoute 概欟</span><span class="sxs-lookup"><span data-stu-id="04644-103">ExpressRoute overview</span></span>
<span data-ttu-id="04644-104">Microsoft Azure ExpressRoute 可讓您透過連線提供者所提供的私人連線，將內部部署網路延伸至 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="04644-104">Microsoft Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="04644-105">透過 ExpressRoute，您可以建立 Microsoft 雲端服務的連線，例如 Microsoft Azure、Office 365 和 Dynamics 365。</span><span class="sxs-lookup"><span data-stu-id="04644-105">With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and Dynamics 365.</span></span>

<span data-ttu-id="04644-106">從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。</span><span class="sxs-lookup"><span data-stu-id="04644-106">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span> <span data-ttu-id="04644-107">ExpressRoute 連線不會經過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="04644-107">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="04644-108">相較於一般網際網路連線，這可讓 ExpressRoute 連線提供更可靠、更快速、延遲更短和更安全的連線。</span><span class="sxs-lookup"><span data-stu-id="04644-108">This allows ExpressRoute connections to offer more reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet.</span></span> <span data-ttu-id="04644-109">如需如何使用 ExpressRoute 將您的網路連接至 Microsoft 的詳細資訊，請參閱 [ExpressRoute 連線模型](expressroute-connectivity-models.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-109">For information on how to connect your network to Microsoft using ExpressRoute, see [ExpressRoute connectivity models](expressroute-connectivity-models.md).</span></span>

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a><span data-ttu-id="04644-110">主要權益</span><span class="sxs-lookup"><span data-stu-id="04644-110">Key benefits</span></span>

* <span data-ttu-id="04644-111">內部部署網路與 Microsoft Cloud 之間透過連線提供者的第 3 層連線能力。</span><span class="sxs-lookup"><span data-stu-id="04644-111">Layer 3 connectivity between your on-premises network and the Microsoft Cloud through a connectivity provider.</span></span> <span data-ttu-id="04644-112">從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或透過乙太網路交換經由虛擬交叉連接，都可以進行連線。</span><span class="sxs-lookup"><span data-stu-id="04644-112">Connectivity can be from an any-to-any (IPVPN) network, a point-to-point Ethernet connection, or through a virtual cross-connection via an Ethernet exchange.</span></span>
* <span data-ttu-id="04644-113">跨地理政治區域中的所有區域連接到 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="04644-113">Connectivity to Microsoft cloud services across all regions in the geopolitical region.</span></span>
* <span data-ttu-id="04644-114">透過 ExpressRoute Premium 附加元件從全球連線到所有區域的 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="04644-114">Global connectivity to Microsoft services across all regions with ExpressRoute premium add-on.</span></span>
* <span data-ttu-id="04644-115">網路與 Microsoft 之間透過業界標準通訊協定 (BGP) 的動態路由。</span><span class="sxs-lookup"><span data-stu-id="04644-115">Dynamic routing between your network and Microsoft over industry standard protocols (BGP).</span></span>
* <span data-ttu-id="04644-116">每個對等位置有內建的備援性，可靠性更高。</span><span class="sxs-lookup"><span data-stu-id="04644-116">Built-in redundancy in every peering location for higher reliability.</span></span>
* <span data-ttu-id="04644-117">連線執行時間 [SLA](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="04644-117">Connection uptime [SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>
* <span data-ttu-id="04644-118">商務用 Skype 的 QoS 支援。</span><span class="sxs-lookup"><span data-stu-id="04644-118">QoS support for Skype for Business.</span></span>

<span data-ttu-id="04644-119">如需詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-119">For more information, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

## <a name="features"></a><span data-ttu-id="04644-120">特性</span><span class="sxs-lookup"><span data-stu-id="04644-120">Features</span></span>

### <a name="layer-3-connectivity"></a><span data-ttu-id="04644-121">第 3 層連線能力</span><span class="sxs-lookup"><span data-stu-id="04644-121">Layer 3 connectivity</span></span>
<span data-ttu-id="04644-122">Microsoft 採用業界標準動態路由通訊協定 (BGP)，在您的內部部署網路、Azure 中的執行個體和 Microsoft 公用位址之間交換路由。</span><span class="sxs-lookup"><span data-stu-id="04644-122">Microsoft uses industry standard dynamic routing protocol (BGP) to exchange routes between your on-premises network, your instances in Azure, and Microsoft public addresses.</span></span>  <span data-ttu-id="04644-123">我們會針對不同的流量設定檔，與您的網路建立多個 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="04644-123">We establish multiple BGP sessions with your network for different traffic profiles.</span></span> <span data-ttu-id="04644-124">如需詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="04644-124">More details can be found in the [ExpressRoute circuit and routing domains](expressroute-circuit-peerings.md) article.</span></span>

### <a name="redundancy"></a><span data-ttu-id="04644-125">備援性</span><span class="sxs-lookup"><span data-stu-id="04644-125">Redundancy</span></span>
<span data-ttu-id="04644-126">每個 ExpressRoute 線路有兩條連線，從連線提供者 / 您的網路邊緣連接到兩個 Microsoft Enterprise 邊緣路由器 (MSEE) 。</span><span class="sxs-lookup"><span data-stu-id="04644-126">Each ExpressRoute circuit consists of two connections to two Microsoft Enterprise edge routers (MSEEs) from the connectivity provider / your network edge.</span></span> <span data-ttu-id="04644-127">Microsoft 需要有來自連線提供者/您這端的雙重 BGP 連線 – 每個連線皆各自連線至每個 MSEE。</span><span class="sxs-lookup"><span data-stu-id="04644-127">Microsoft requires dual BGP connection from the connectivity provider / your side – one to each MSEE.</span></span> <span data-ttu-id="04644-128">您可以選擇不要在您這端部署備援裝置 / 乙太網路線路。</span><span class="sxs-lookup"><span data-stu-id="04644-128">You may choose not to deploy redundant devices / Ethernet circuits at your end.</span></span> <span data-ttu-id="04644-129">不過，連線提供者會使用備援裝置，確保以備援方式將您的連線交給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="04644-129">However, connectivity providers use redundant devices to ensure that your connections are handed off to Microsoft in a redundant manner.</span></span> <span data-ttu-id="04644-130">備援第 3 層連線組態是我們的 [SLA](https://azure.microsoft.com/support/legal/sla/) 生效的條件。</span><span class="sxs-lookup"><span data-stu-id="04644-130">A redundant Layer 3 connectivity configuration is a requirement for our [SLA](https://azure.microsoft.com/support/legal/sla/) to be valid.</span></span>

### <a name="connectivity-to-microsoft-cloud-services"></a><span data-ttu-id="04644-131">連線到 Microsoft 雲端服務</span><span class="sxs-lookup"><span data-stu-id="04644-131">Connectivity to Microsoft cloud services</span></span>
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

<span data-ttu-id="04644-132">透過 ExpressRoute 連線可存取下列服務：</span><span class="sxs-lookup"><span data-stu-id="04644-132">ExpressRoute connections enable access to the following services:</span></span>

* <span data-ttu-id="04644-133">Microsoft Azure 服務</span><span class="sxs-lookup"><span data-stu-id="04644-133">Microsoft Azure services</span></span>
* <span data-ttu-id="04644-134">Microsoft Office 365 服務</span><span class="sxs-lookup"><span data-stu-id="04644-134">Microsoft Office 365 services</span></span>
* <span data-ttu-id="04644-135">Microsoft Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="04644-135">Microsoft Dynamics 365</span></span>

<span data-ttu-id="04644-136">您可以瀏覽 [ExpressRoute 常見問題集](expressroute-faqs.md) 頁面，取得透過 ExpressRoute 所支援的服務的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="04644-136">You can visit the [ExpressRoute FAQ](expressroute-faqs.md) page for a detailed list of services supported over ExpressRoute.</span></span>

### <a name="connectivity-to-all-regions-within-a-geopolitical-region"></a><span data-ttu-id="04644-137">連線到地理政治區域內的所有區域</span><span class="sxs-lookup"><span data-stu-id="04644-137">Connectivity to all regions within a geopolitical region</span></span>
<span data-ttu-id="04644-138">您可以在我們的其中一個 [對等位置](expressroute-locations.md) 中連接到 Microsoft，就能夠存取地理政治區域內的所有區域。</span><span class="sxs-lookup"><span data-stu-id="04644-138">You can connect to Microsoft in one of our [peering locations](expressroute-locations.md) and have access to all regions within the geopolitical region.</span></span> 

<span data-ttu-id="04644-139">例如，如果您在阿姆斯特丹透過 ExpressRoute 連線至 Microsoft，您就能夠存取在北歐和西歐託管的所有 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="04644-139">For example, if you connected to Microsoft in Amsterdam through ExpressRoute, you have access to all Microsoft cloud services hosted in Northern Europe and Western Europe.</span></span> <span data-ttu-id="04644-140">如需地理政治地區、相關聯的 Microsoft 雲端區域和對應的 ExpressRoute 對等位置的概觀，請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)一文。</span><span class="sxs-lookup"><span data-stu-id="04644-140">See the [ExpressRoute partners and peering locations](expressroute-locations.md) article for an overview of the geopolitical regions, associated Microsoft cloud regions, and corresponding ExpressRoute peering locations.</span></span>

### <a name="global-connectivity-with-expressroute-premium-add-on"></a><span data-ttu-id="04644-141">使用 ExpressRoute Premium 附加元件從全球連線</span><span class="sxs-lookup"><span data-stu-id="04644-141">Global connectivity with ExpressRoute premium add-on</span></span>
<span data-ttu-id="04644-142">您可以啟用 ExpressRoute Premium 附加功能，將連線能力延伸到跨越地理政治的界限。</span><span class="sxs-lookup"><span data-stu-id="04644-142">You can enable the ExpressRoute premium add-on feature to extend connectivity across geopolitical boundaries.</span></span> <span data-ttu-id="04644-143">例如，如果您在阿姆斯特丹透過 ExpressRoute 連接到 Microsoft，您就能夠存取全球所有區域裝載的所有 Microsoft 雲端服務 (不包括國家雲端)。</span><span class="sxs-lookup"><span data-stu-id="04644-143">For example, if you are connected to Microsoft in Amsterdam through ExpressRoute, you will have access to all Microsoft cloud services hosted in all regions across the world (national clouds are excluded).</span></span> <span data-ttu-id="04644-144">就像存取北歐和西歐區域一樣，您也可以存取部署在南美洲或澳大利亞的服務。</span><span class="sxs-lookup"><span data-stu-id="04644-144">You can access services deployed in South America or Australia the same way you access the North and West Europe regions.</span></span>

### <a name="rich-connectivity-partner-ecosystem"></a><span data-ttu-id="04644-145">豐富的連線合作夥伴生態系統</span><span class="sxs-lookup"><span data-stu-id="04644-145">Rich connectivity partner ecosystem</span></span>
<span data-ttu-id="04644-146">ExpressRoute 的連線提供者和 SI 合作夥伴生態系統持續成長茁壯。</span><span class="sxs-lookup"><span data-stu-id="04644-146">ExpressRoute has a constantly growing ecosystem of connectivity providers and SI partners.</span></span> <span data-ttu-id="04644-147">如需最新資訊，請參閱 [ExpressRoute 提供者和位置](expressroute-locations.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="04644-147">You can refer to the [ExpressRoute providers and locations](expressroute-locations.md) article for the latest information.</span></span>

### <a name="connectivity-to-national-clouds"></a><span data-ttu-id="04644-148">連線到國家雲端</span><span class="sxs-lookup"><span data-stu-id="04644-148">Connectivity to national clouds</span></span>
<span data-ttu-id="04644-149">Microsoft 為特殊的地理政治地區和客戶群提供隔離的雲端環境。</span><span class="sxs-lookup"><span data-stu-id="04644-149">Microsoft operates isolated cloud environments for special geopolitical regions and customer segments.</span></span> <span data-ttu-id="04644-150">如需國家雲端和提供者的清單，請參閱 [ExpressRoute 提供者和位置](expressroute-locations.md) 頁面。</span><span class="sxs-lookup"><span data-stu-id="04644-150">Refer to the [ExpressRoute providers and locations](expressroute-locations.md) page for a list of national clouds and providers.</span></span>

### <a name="bandwidth-options"></a><span data-ttu-id="04644-151">頻寬選項</span><span class="sxs-lookup"><span data-stu-id="04644-151">Bandwidth options</span></span>
<span data-ttu-id="04644-152">您可以購買各種頻寬的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="04644-152">You can purchase ExpressRoute circuits for a wide range of bandwidths.</span></span> <span data-ttu-id="04644-153">支援的頻寬如下所列。</span><span class="sxs-lookup"><span data-stu-id="04644-153">Supported bandwidths are listed below.</span></span> <span data-ttu-id="04644-154">請務必洽詢您的連線提供者，以判斷他們支援的頻寬清單。</span><span class="sxs-lookup"><span data-stu-id="04644-154">Be sure to check with your connectivity provider to determine the list of supported bandwidths they provide.</span></span>

* <span data-ttu-id="04644-155">50 Mbps</span><span class="sxs-lookup"><span data-stu-id="04644-155">50 Mbps</span></span>
* <span data-ttu-id="04644-156">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="04644-156">100 Mbps</span></span>
* <span data-ttu-id="04644-157">200 Mbps</span><span class="sxs-lookup"><span data-stu-id="04644-157">200 Mbps</span></span>
* <span data-ttu-id="04644-158">500 Mbps</span><span class="sxs-lookup"><span data-stu-id="04644-158">500 Mbps</span></span>
* <span data-ttu-id="04644-159">1 Gbps</span><span class="sxs-lookup"><span data-stu-id="04644-159">1 Gbps</span></span>
* <span data-ttu-id="04644-160">2 Gbps</span><span class="sxs-lookup"><span data-stu-id="04644-160">2 Gbps</span></span>
* <span data-ttu-id="04644-161">5 Gbps</span><span class="sxs-lookup"><span data-stu-id="04644-161">5 Gbps</span></span>
* <span data-ttu-id="04644-162">10 Gbps</span><span class="sxs-lookup"><span data-stu-id="04644-162">10 Gbps</span></span>

### <a name="dynamic-scaling-of-bandwidth"></a><span data-ttu-id="04644-163">動態調整頻寬</span><span class="sxs-lookup"><span data-stu-id="04644-163">Dynamic scaling of bandwidth</span></span>
<span data-ttu-id="04644-164">您可以在不中斷連線的情況下﹐增加 ExpressRoute 線路頻寬 (盡最大努力)。</span><span class="sxs-lookup"><span data-stu-id="04644-164">You can increase the ExpressRoute circuit bandwidth (on a best effort basis) without having to tear down your connections.</span></span> 

### <a name="flexible-billing-models"></a><span data-ttu-id="04644-165">彈性的計費模型</span><span class="sxs-lookup"><span data-stu-id="04644-165">Flexible billing models</span></span>
<span data-ttu-id="04644-166">您可以挑選最適合的計費模型。</span><span class="sxs-lookup"><span data-stu-id="04644-166">You can pick a billing model that works best for you.</span></span> <span data-ttu-id="04644-167">請從下列計費模型中選擇。</span><span class="sxs-lookup"><span data-stu-id="04644-167">Choose between the billing models listed below.</span></span> <span data-ttu-id="04644-168">如需詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-168">For more information, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

* <span data-ttu-id="04644-169">**無限制資料**。</span><span class="sxs-lookup"><span data-stu-id="04644-169">**Unlimited data**.</span></span> <span data-ttu-id="04644-170">ExpressRoute 線路按月計費，所有輸入和輸出資料傳輸已免費包括在內。</span><span class="sxs-lookup"><span data-stu-id="04644-170">The ExpressRoute circuit is charged based on a monthly fee, and all inbound and outbound data transfer is included free of charge.</span></span> 
* <span data-ttu-id="04644-171">**已計量資料**。</span><span class="sxs-lookup"><span data-stu-id="04644-171">**Metered data**.</span></span> <span data-ttu-id="04644-172">ExpressRoute 線路按月計費。</span><span class="sxs-lookup"><span data-stu-id="04644-172">The ExpressRoute circuit is charged based on a monthly fee.</span></span> <span data-ttu-id="04644-173">所有輸入資料傳輸都免費。</span><span class="sxs-lookup"><span data-stu-id="04644-173">All inbound data transfer is free of charge.</span></span> <span data-ttu-id="04644-174">輸出資料傳輸依每 GB 資料傳輸計費。</span><span class="sxs-lookup"><span data-stu-id="04644-174">Outbound data transfer is charged per GB of data transfer.</span></span> <span data-ttu-id="04644-175">資料傳輸費率依區域而不同。</span><span class="sxs-lookup"><span data-stu-id="04644-175">Data transfer rates vary by region.</span></span>
* <span data-ttu-id="04644-176">**ExpressRoute Premium 附加元件**。</span><span class="sxs-lookup"><span data-stu-id="04644-176">**ExpressRoute premium add-on**.</span></span> <span data-ttu-id="04644-177">ExpressRoute Premium 是 ExpressRoute 線路上的附加元件。</span><span class="sxs-lookup"><span data-stu-id="04644-177">The ExpressRoute premium is an add-on over the ExpressRoute circuit.</span></span> <span data-ttu-id="04644-178">ExpressRoute Premium 附加元件提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="04644-178">The ExpressRoute premium add-on provides the following capabilities:</span></span> 
  * <span data-ttu-id="04644-179">Azure 公用和 Azure 私用對等的路由限制從 4,000 個路由提高到 10,000 個路由。</span><span class="sxs-lookup"><span data-stu-id="04644-179">Increased route limits for Azure public and Azure private peering from 4,000 routes to 10,000 routes.</span></span>
  * <span data-ttu-id="04644-180">從全球連線到服務。</span><span class="sxs-lookup"><span data-stu-id="04644-180">Global connectivity for services.</span></span> <span data-ttu-id="04644-181">任何區域中建立的 ExpressRoute 線路 (不包括國家雲端) 能夠存取全球其他任何區域的資源。</span><span class="sxs-lookup"><span data-stu-id="04644-181">An ExpressRoute circuit created in any region (excluding national clouds) will have access to resources across any other region in the world.</span></span> <span data-ttu-id="04644-182">例如，透過在美國矽谷佈建的 ExpressRoute 線路，可存取在西歐建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="04644-182">For example, a virtual network created in West Europe can be accessed through an ExpressRoute circuit provisioned in Silicon Valley.</span></span>
  * <span data-ttu-id="04644-183">每個 ExpressRoute 線路的 VNet 連結數目已從原本 10 個放寬限制，視線路的頻寬而定。</span><span class="sxs-lookup"><span data-stu-id="04644-183">Increased number of VNet links per ExpressRoute circuit from 10 to a larger limit, depending on the bandwidth of the circuit.</span></span>

## <a name="faq"></a><span data-ttu-id="04644-184">常見問題集</span><span class="sxs-lookup"><span data-stu-id="04644-184">FAQ</span></span>

<span data-ttu-id="04644-185">如需有關 ExpressRoute 的常見問題，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-185">For frequently asked questions about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04644-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04644-186">Next steps</span></span>

* <span data-ttu-id="04644-187">深入了解 [ExpressRoute 連線模型](expressroute-connectivity-models.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-187">Learn about [ExpressRoute connectivity models](expressroute-connectivity-models.md).</span></span>
* <span data-ttu-id="04644-188">了解 ExpressRoute 連線和路由網域。</span><span class="sxs-lookup"><span data-stu-id="04644-188">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="04644-189">請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-189">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="04644-190">尋找服務提供者。</span><span class="sxs-lookup"><span data-stu-id="04644-190">Find a service provider.</span></span> <span data-ttu-id="04644-191">請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-191">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="04644-192">請確定符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="04644-192">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="04644-193">請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-193">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="04644-194">請參閱[路由](expressroute-routing.md)、[NAT](expressroute-nat.md) 和 [QoS](expressroute-qos.md) 的需求。</span><span class="sxs-lookup"><span data-stu-id="04644-194">Refer to the requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="04644-195">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="04644-195">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="04644-196">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="04644-196">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="04644-197">設定 ExpressRoute 線路的對等互連</span><span class="sxs-lookup"><span data-stu-id="04644-197">Configure peering for an ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="04644-198">將虛擬網路連線到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="04644-198">Connect a virtual network to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
* <span data-ttu-id="04644-199">深入了解 Azure 的一些其他重要[網路功能](../networking/networking-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="04644-199">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>
