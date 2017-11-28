---
title: "aaaAzure ExpressRoute 常見問題集 |Microsoft 文件"
description: "hello ExpressRoute 常見問題集包含支援的 Azure 服務、 成本、 資料和連線、 SLA、 提供者和位置、 頻寬和其他技術詳細資料的相關資訊。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a><span data-ttu-id="e797c-103">ExpressRoute 常見問題集</span><span class="sxs-lookup"><span data-stu-id="e797c-103">ExpressRoute FAQ</span></span>

## <a name="what-is-expressroute"></a><span data-ttu-id="e797c-104">什麼是 ExpressRoute？</span><span class="sxs-lookup"><span data-stu-id="e797c-104">What is ExpressRoute?</span></span>

<span data-ttu-id="e797c-105">ExpressRoute 這項 Azure 服務可讓您在 Microsoft 資料中心和內部部署或共置設備中的基礎結構之間建立私人連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-105">ExpressRoute is an Azure service that lets you create private connections between Microsoft datacenters and infrastructure that’s on your premises or in a colocation facility.</span></span> <span data-ttu-id="e797c-106">ExpressRoute 連線不會經過 hello 公用網際網路，並提供較高的安全性、 可靠性和速度降低延遲比一般連線透過網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="e797c-106">ExpressRoute connections do not go over hello public Internet, and offer higher security, reliability, and speeds with lower latencies than typical connections over hello Internet.</span></span>

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a><span data-ttu-id="e797c-107">使用 ExpressRoute 和私人網路連線的 hello 優點有哪些？</span><span class="sxs-lookup"><span data-stu-id="e797c-107">What are hello benefits of using ExpressRoute and private network connections?</span></span>

<span data-ttu-id="e797c-108">ExpressRoute 連線不會經過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="e797c-108">ExpressRoute connections do not go over hello public Internet.</span></span> <span data-ttu-id="e797c-109">它們提供更高的安全性、 可靠性和速度，比透過 hello 網際網路的一般連線較低且一致的延遲。</span><span class="sxs-lookup"><span data-stu-id="e797c-109">They offer higher security, reliability, and speeds, with lower and consistent latencies than typical connections over hello Internet.</span></span> <span data-ttu-id="e797c-110">在某些情況下，使用 ExpressRoute 連線 tootransfer 資料之間的內部的裝置，Azure 會產生顯著的成本優勢。</span><span class="sxs-lookup"><span data-stu-id="e797c-110">In some cases, using ExpressRoute connections tootransfer data between on-premises devices and Azure can yield significant cost benefits.</span></span>

### <a name="where-is-hello-service-available"></a><span data-ttu-id="e797c-111">其中是 hello 服務可用？</span><span class="sxs-lookup"><span data-stu-id="e797c-111">Where is hello service available?</span></span>

<span data-ttu-id="e797c-112">請參閱以下頁面，以取得服務位置和可用性： [ExpressRoute 合作夥伴和位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-112">See this page for service location and availability: [ExpressRoute partners and locations](expressroute-locations.md).</span></span>

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a><span data-ttu-id="e797c-113">如果我並未與其中一個 hello ExpressRoute 電信業合作夥伴建立合作關係，如何使用 ExpressRoute tooconnect tooMicrosoft？</span><span class="sxs-lookup"><span data-stu-id="e797c-113">How can I use ExpressRoute tooconnect tooMicrosoft if I don’t have partnerships with one of hello ExpressRoute-carrier partners?</span></span>

<span data-ttu-id="e797c-114">您可以選取一個地區性貨運公司，並進入乙太網路連線 tooone 的 hello 支援 exchange 提供者位置。</span><span class="sxs-lookup"><span data-stu-id="e797c-114">You can select a regional carrier and land Ethernet connections tooone of hello supported exchange provider locations.</span></span> <span data-ttu-id="e797c-115">您接著可以使用 Microsoft hello 提供者位置互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-115">You can then peer with Microsoft at hello provider location.</span></span> <span data-ttu-id="e797c-116">檢查 hello 的最後一個區段[ExpressRoute 合作夥伴和位置](expressroute-locations.md)toosee 您服務提供者是否有任何 hello exchange 位置。</span><span class="sxs-lookup"><span data-stu-id="e797c-116">Check hello last section of [ExpressRoute partners and locations](expressroute-locations.md) toosee if your service provider is present in any of hello exchange locations.</span></span> <span data-ttu-id="e797c-117">然後，您可以訂購 hello 服務提供者 tooconnect tooAzure 透過 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-117">You can then order an ExpressRoute circuit through hello service provider tooconnect tooAzure.</span></span>

### <a name="how-much-does-expressroute-cost"></a><span data-ttu-id="e797c-118">ExpressRoute 需要多少錢？</span><span class="sxs-lookup"><span data-stu-id="e797c-118">How much does ExpressRoute cost?</span></span>

<span data-ttu-id="e797c-119">如需價格資訊，請查看 [價格詳細資訊](https://azure.microsoft.com/pricing/details/expressroute/) 。</span><span class="sxs-lookup"><span data-stu-id="e797c-119">Check [pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for pricing information.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a><span data-ttu-id="e797c-120">如果我支付給定頻寬的 ExpressRoute 電路並 hello 我從我的網路服務提供者購買的 VPN 連線 toobe 擁有 hello 相同的速度嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-120">If I pay for an ExpressRoute circuit of a given bandwidth, does hello VPN connection I purchase from my network service provider have toobe hello same speed?</span></span>

<span data-ttu-id="e797c-121">否。</span><span class="sxs-lookup"><span data-stu-id="e797c-121">No.</span></span> <span data-ttu-id="e797c-122">您可以從服務提供者購買任何速度的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-122">You can purchase a VPN connection of any speed from your service provider.</span></span> <span data-ttu-id="e797c-123">不過，連線 tooAzure 是您購買的有限的 toohello ExpressRoute 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="e797c-123">However, your connection tooAzure is limited toohello ExpressRoute circuit bandwidth that you purchase.</span></span>

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a><span data-ttu-id="e797c-124">如果我支付給定頻寬的 ExpressRoute 電路，我是否必須 hello 能力 tooburst toohigher 速度必要時註冊？</span><span class="sxs-lookup"><span data-stu-id="e797c-124">If I pay for an ExpressRoute circuit of a given bandwidth, do I have hello ability tooburst up toohigher speeds if necessary?</span></span>

<span data-ttu-id="e797c-125">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-125">Yes.</span></span> <span data-ttu-id="e797c-126">ExpressRoute 電路都已設定的 tooallow tooburst tootwo 時間 hello 您無需額外成本提高現有頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="e797c-126">ExpressRoute circuits are configured tooallow you tooburst up tootwo times hello bandwidth limit you procured for no additional cost.</span></span> <span data-ttu-id="e797c-127">如果它們支援這項功能，請洽詢您的服務提供者 toosee。</span><span class="sxs-lookup"><span data-stu-id="e797c-127">Check with your service provider toosee if they support this capability.</span></span>

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a><span data-ttu-id="e797c-128">我可以使用 hello 同時私用的相同網路與虛擬網路與其他 Azure 服務的連線嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-128">Can I use hello same private network connection with virtual network and other Azure services simultaneously?</span></span>

<span data-ttu-id="e797c-129">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-129">Yes.</span></span> <span data-ttu-id="e797c-130">ExpressRoute 電路一旦設定完成，可讓您虛擬網路內的 tooaccess 服務和其他 Azure 服務同時。</span><span class="sxs-lookup"><span data-stu-id="e797c-130">An ExpressRoute circuit, once set up, allows you tooaccess services within a virtual network and other Azure services simultaneously.</span></span> <span data-ttu-id="e797c-131">您透過 toovirtual 網路 hello 私用對等互連路徑和 tooother 服務透過 hello 公用互連路徑。</span><span class="sxs-lookup"><span data-stu-id="e797c-131">You connect toovirtual networks over hello private peering path, and tooother services over hello public peering path.</span></span>

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a><span data-ttu-id="e797c-132">ExpressRoute 是否提供服務等級協定 (SLA)？</span><span class="sxs-lookup"><span data-stu-id="e797c-132">Does ExpressRoute offer a Service Level Agreement (SLA)?</span></span>

<span data-ttu-id="e797c-133">如需資訊，請參閱 hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/)頁面。</span><span class="sxs-lookup"><span data-stu-id="e797c-133">For information, see hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) page.</span></span>

## <a name="supported-services"></a><span data-ttu-id="e797c-134">支援的服務</span><span class="sxs-lookup"><span data-stu-id="e797c-134">Supported services</span></span>

<span data-ttu-id="e797c-135">ExpressRoute 針對各種服務類型支援[三種路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-135">ExpressRoute supports [three routing domains](expressroute-circuit-peerings.md) for various types of services.</span></span>

### <a name="private-peering"></a><span data-ttu-id="e797c-136">私人對等互連</span><span class="sxs-lookup"><span data-stu-id="e797c-136">Private peering</span></span>

* <span data-ttu-id="e797c-137">包括所有虛擬機器和雲端服務在內的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e797c-137">Virtual networks, including all virtual machines and cloud services</span></span>

### <a name="public-peering"></a><span data-ttu-id="e797c-138">公用對等互連</span><span class="sxs-lookup"><span data-stu-id="e797c-138">Public peering</span></span>

* <span data-ttu-id="e797c-139">Power BI</span><span class="sxs-lookup"><span data-stu-id="e797c-139">Power BI</span></span>
* <span data-ttu-id="e797c-140">Dynamics 365 for Finance and Operations (先前稱為 Dynamics AX Online)</span><span class="sxs-lookup"><span data-stu-id="e797c-140">Dynamics 365 for Finance and Operations (formerly known as Dynamics AX Online)</span></span>
* <span data-ttu-id="e797c-141">大部分的 hello Azure 服務，以下列幾個例外狀況的 hello:</span><span class="sxs-lookup"><span data-stu-id="e797c-141">Most of hello Azure services, with hello following few exceptions:</span></span>
  * <span data-ttu-id="e797c-142">CDN</span><span class="sxs-lookup"><span data-stu-id="e797c-142">CDN</span></span>
  * <span data-ttu-id="e797c-143">Visual Studio Team Services 負載測試 </span><span class="sxs-lookup"><span data-stu-id="e797c-143">Visual Studio Team Services Load Testing</span></span>
  * <span data-ttu-id="e797c-144">多因素驗證</span><span class="sxs-lookup"><span data-stu-id="e797c-144">Multi-factor Authentication</span></span>
  * <span data-ttu-id="e797c-145">流量管理員</span><span class="sxs-lookup"><span data-stu-id="e797c-145">Traffic Manager</span></span>

### <a name="microsoft-peering"></a><span data-ttu-id="e797c-146">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="e797c-146">Microsoft peering</span></span>

* [<span data-ttu-id="e797c-147">Office 365</span><span class="sxs-lookup"><span data-stu-id="e797c-147">Office 365</span></span>](http://aka.ms/ExpressRouteOffice365)
* <span data-ttu-id="e797c-148">Dynamics 365 Customer Engagement 應用程式 (先前稱為 CRM Online)</span><span class="sxs-lookup"><span data-stu-id="e797c-148">Dynamics 365 Customer Engagement applications (formerly known as CRM Online)</span></span>
  * <span data-ttu-id="e797c-149">Dynamics 365 for Sales</span><span class="sxs-lookup"><span data-stu-id="e797c-149">Dynamics 365 for Sales</span></span>
  * <span data-ttu-id="e797c-150">Dynamics 365 for Customer Service</span><span class="sxs-lookup"><span data-stu-id="e797c-150">Dynamics 365 for Customer Service</span></span>
  * <span data-ttu-id="e797c-151">Dynamics 365 for Field Service</span><span class="sxs-lookup"><span data-stu-id="e797c-151">Dynamics 365 for Field Service</span></span>
  * <span data-ttu-id="e797c-152">Dynamics 365 for Project Service</span><span class="sxs-lookup"><span data-stu-id="e797c-152">Dynamics 365 for Project Service</span></span>

## <a name="data-and-connections"></a><span data-ttu-id="e797c-153">資料與連線</span><span class="sxs-lookup"><span data-stu-id="e797c-153">Data and connections</span></span>

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a><span data-ttu-id="e797c-154">有我可以使用 ExpressRoute 傳輸的資料的 hello 數量的限制嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-154">Are there limits on hello amount of data that I can transfer using ExpressRoute?</span></span>

<span data-ttu-id="e797c-155">我們未上的資料傳輸的 hello 量設定限制。</span><span class="sxs-lookup"><span data-stu-id="e797c-155">We do not set a limit on hello amount of data transfer.</span></span> <span data-ttu-id="e797c-156">請參閱太[定價詳細資料](https://azure.microsoft.com/pricing/details/expressroute/)如需頻寬費率的資訊。</span><span class="sxs-lookup"><span data-stu-id="e797c-156">Refer too[pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for information on bandwidth rates.</span></span>

### <a name="what-connection-speeds-are-supported-by-expressroute"></a><span data-ttu-id="e797c-157">ExpressRoute 支援的連線速度為何？</span><span class="sxs-lookup"><span data-stu-id="e797c-157">What connection speeds are supported by ExpressRoute?</span></span>

<span data-ttu-id="e797c-158">支援的頻寬優惠：</span><span class="sxs-lookup"><span data-stu-id="e797c-158">Supported bandwidth offers:</span></span>

<span data-ttu-id="e797c-159">50 Mbps、100 Mbps、200 Mbps、500 Mbps、1 Gbps、2 Gbps、5 Gbps、10 Gbps</span><span class="sxs-lookup"><span data-stu-id="e797c-159">50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps</span></span>

### <a name="which-service-providers-are-available"></a><span data-ttu-id="e797c-160">可以使用的服務提供者有哪些？</span><span class="sxs-lookup"><span data-stu-id="e797c-160">Which service providers are available?</span></span>

<span data-ttu-id="e797c-161">請參閱[ExpressRoute 合作夥伴和位置](expressroute-locations.md)hello 清單服務提供者和位置。</span><span class="sxs-lookup"><span data-stu-id="e797c-161">See [ExpressRoute partners and locations](expressroute-locations.md) for hello list of service providers and locations.</span></span>

## <a name="technical-details"></a><span data-ttu-id="e797c-162">技術詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e797c-162">Technical details</span></span>

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a><span data-ttu-id="e797c-163">Hello 連線我在內部部署位置 tooAzure 的技術需求為何？</span><span class="sxs-lookup"><span data-stu-id="e797c-163">What are hello technical requirements for connecting my on-premises location tooAzure?</span></span>

<span data-ttu-id="e797c-164">請參閱 [ExpressRoute 必要條件頁面](expressroute-prerequisites.md)以取得相關需求。</span><span class="sxs-lookup"><span data-stu-id="e797c-164">See [ExpressRoute prerequisites page](expressroute-prerequisites.md) for requirements.</span></span>

### <a name="are-connections-tooexpressroute-redundant"></a><span data-ttu-id="e797c-165">會連線 tooExpressRoute 備援嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-165">Are connections tooExpressRoute redundant?</span></span>

<span data-ttu-id="e797c-166">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-166">Yes.</span></span> <span data-ttu-id="e797c-167">每個 ExpressRoute 電路都有一組備援的交叉連線設定 tooprovide 高可用性。</span><span class="sxs-lookup"><span data-stu-id="e797c-167">Each ExpressRoute circuit has a redundant pair of cross connections configured tooprovide high availability.</span></span>

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a><span data-ttu-id="e797c-168">如果我的其中一個 ExpressRoute 連結失敗，連線是否就會中斷？</span><span class="sxs-lookup"><span data-stu-id="e797c-168">Will I lose connectivity if one of my ExpressRoute links fail?</span></span>

<span data-ttu-id="e797c-169">您不會中斷連線，如果一個的 hello 交叉連線會失敗。</span><span class="sxs-lookup"><span data-stu-id="e797c-169">You will not lose connectivity if one of hello cross connections fails.</span></span> <span data-ttu-id="e797c-170">備援連線是網路的可用 toosupport hello 負載。</span><span class="sxs-lookup"><span data-stu-id="e797c-170">A redundant connection is available toosupport hello load of your network.</span></span> <span data-ttu-id="e797c-171">此外，您就可以在不同對等互連位置 tooachieve 失敗恢復建立多個電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-171">You can additionally create multiple circuits in a different peering location tooachieve failure resilience.</span></span>

### <span data-ttu-id="e797c-172"><a name="onep2plink"></a>如果我不在雲端交換共我的服務提供者提供點對點連線，需要 tooorder 兩個實體之間的連線我的內部部署網路和 Microsoft？</span><span class="sxs-lookup"><span data-stu-id="e797c-172"><a name="onep2plink"></a>If I'm not co-located at a cloud exchange and my service provider offers point-to-point connection, do I need tooorder two physical connections between my on-premises network and Microsoft?</span></span>

<span data-ttu-id="e797c-173">如果您的服務提供者可以建立兩個乙太網路的虛擬電路 hello 實體連線，您只需要一個實體連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-173">If your service provider can establish two Ethernet virtual circuits over hello physical connection, you only need one physical connection.</span></span> <span data-ttu-id="e797c-174">hello 實體連線 （例如，光纖） 已終止圖層上 1 (L1) 裝置 （請參閱 hello 映像）。</span><span class="sxs-lookup"><span data-stu-id="e797c-174">hello physical connection (for example, an optical fiber) is terminated on a layer 1 (L1) device (see hello image).</span></span> <span data-ttu-id="e797c-175">hello 兩個乙太網路的虛擬電路都會加上不同的 VLAN Id，一個 hello 主要循環，另一個用於次要的 hello。</span><span class="sxs-lookup"><span data-stu-id="e797c-175">hello two Ethernet virtual circuits are tagged with different VLAN IDs, one for hello primary circuit, and one for hello secondary.</span></span> <span data-ttu-id="e797c-176">這些 VLAN 識別碼採用 xxxnnnnn hello 外部 802.1 q 乙太網路標頭。</span><span class="sxs-lookup"><span data-stu-id="e797c-176">Those VLAN IDs are in hello outer 802.1Q Ethernet header.</span></span> <span data-ttu-id="e797c-177">hello 內部 802.1 q 乙太網路標頭 （未顯示） 是特定的對應的 tooa [ExpressRoute 路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-177">hello inner 802.1Q Ethernet header (not shown) is mapped tooa specific [ExpressRoute routing domain](expressroute-circuit-peerings.md).</span></span>

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a><span data-ttu-id="e797c-178">我可以將其中一個我使用 ExpressRoute 的 Vlan tooAzure 延伸嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-178">Can I extend one of my VLANs tooAzure using ExpressRoute?</span></span>

<span data-ttu-id="e797c-179">否。</span><span class="sxs-lookup"><span data-stu-id="e797c-179">No.</span></span> <span data-ttu-id="e797c-180">我們不支援至 Azure 的第 2 層連線擴充程式。</span><span class="sxs-lookup"><span data-stu-id="e797c-180">We do not support layer 2 connectivity extensions into Azure.</span></span>

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a><span data-ttu-id="e797c-181">我的訂用帳戶是否可以有多個 ExpressRoute 電路？</span><span class="sxs-lookup"><span data-stu-id="e797c-181">Can I have more than one ExpressRoute circuit in my subscription?</span></span>

<span data-ttu-id="e797c-182">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-182">Yes.</span></span> <span data-ttu-id="e797c-183">您的訂用帳戶可以有多個 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-183">You can have more than one ExpressRoute circuit in your subscription.</span></span> <span data-ttu-id="e797c-184">hello 預設限制是設 too10。</span><span class="sxs-lookup"><span data-stu-id="e797c-184">hello default limit is set too10.</span></span> <span data-ttu-id="e797c-185">如有需要您可以連絡 Microsoft 支援服務 tooincrease hello 限制。</span><span class="sxs-lookup"><span data-stu-id="e797c-185">You can contact Microsoft Support tooincrease hello limit, if needed.</span></span>

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a><span data-ttu-id="e797c-186">我可以使用其他服務提供者的 ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-186">Can I have ExpressRoute circuits from different service providers?</span></span>

<span data-ttu-id="e797c-187">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-187">Yes.</span></span> <span data-ttu-id="e797c-188">您可以使用許多服務提供者的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-188">You can have ExpressRoute circuits with many service providers.</span></span> <span data-ttu-id="e797c-189">每個 ExpressRoute 線路只會與一個服務提供者產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e797c-189">Each ExpressRoute circuit is associated with one service provider only.</span></span> 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a><span data-ttu-id="e797c-190">可以有多個 ExpressRoute 電路 hello 中相同的位置？</span><span class="sxs-lookup"><span data-stu-id="e797c-190">Can I have multiple ExpressRoute circuits in hello same location?</span></span>

<span data-ttu-id="e797c-191">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-191">Yes.</span></span> <span data-ttu-id="e797c-192">您可以有多個 ExpressRoute 電路，與 hello 相同或不同的服務提供者在 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e797c-192">You can have multiple ExpressRoute circuits, with hello same or different service providers in hello same location.</span></span> <span data-ttu-id="e797c-193">不過，您無法連結多個 ExpressRoute 電路 toohello 相同虛擬 hello 從網路相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e797c-193">However, you can't link more than one ExpressRoute circuit toohello same virtual network from hello same location.</span></span>

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a><span data-ttu-id="e797c-194">我要如何連接我的虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="e797c-194">How do I connect my virtual networks tooan ExpressRoute circuit</span></span>

<span data-ttu-id="e797c-195">hello 基本步驟如下：</span><span class="sxs-lookup"><span data-stu-id="e797c-195">hello basic steps are:</span></span>

* <span data-ttu-id="e797c-196">建立 ExpressRoute 電路並 hello 服務提供者啟用它。</span><span class="sxs-lookup"><span data-stu-id="e797c-196">Establish an ExpressRoute circuit and have hello service provider enable it.</span></span>
* <span data-ttu-id="e797c-197">您或 hello 提供者，必須設定 hello BGP 對等 (s)。</span><span class="sxs-lookup"><span data-stu-id="e797c-197">You, or hello provider, must configure hello BGP peering(s).</span></span>
* <span data-ttu-id="e797c-198">連結 hello 虛擬網路 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-198">Link hello virtual network toohello ExpressRoute circuit.</span></span>

<span data-ttu-id="e797c-199">如需詳細資訊，請參閱 [ExpressRoute 工作流程線路佈建和線路狀態](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-199">For more information, see [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a><span data-ttu-id="e797c-200">我的 ExpressRoute 電路是否有連線範圍？</span><span class="sxs-lookup"><span data-stu-id="e797c-200">Are there connectivity boundaries for my ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-201">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-201">Yes.</span></span> <span data-ttu-id="e797c-202">hello [ExpressRoute 合作夥伴和位置](expressroute-locations.md)文章提供概觀 hello 連線界限的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-202">hello [ExpressRoute partners and locations](expressroute-locations.md) article provides an overview of hello connectivity boundaries for an ExpressRoute circuit.</span></span> <span data-ttu-id="e797c-203">ExpressRoute 循環的連線能力是有限的 tooa 單一地理政治區域。</span><span class="sxs-lookup"><span data-stu-id="e797c-203">Connectivity for an ExpressRoute circuit is limited tooa single geopolitical region.</span></span> <span data-ttu-id="e797c-204">連線可以是展開的 toocross 地緣政治區域啟用 hello ExpressRoute premium 功能。</span><span class="sxs-lookup"><span data-stu-id="e797c-204">Connectivity can be expanded toocross geopolitical regions by enabling hello ExpressRoute premium feature.</span></span>

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="e797c-205">可以將連結 toomore 比一個虛擬網路 tooan ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-205">Can I link toomore than one virtual network tooan ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-206">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-206">Yes.</span></span> <span data-ttu-id="e797c-207">您可以在擁有 too10 標準的 ExpressRoute 電路的虛擬網路連線和向上 too100 [premium ExpressRoute 電路](#expressroute-premium)。</span><span class="sxs-lookup"><span data-stu-id="e797c-207">You can have up too10 virtual networks connections on a standard ExpressRoute circuit, and up too100 on a [premium ExpressRoute circuit](#expressroute-premium).</span></span> 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a><span data-ttu-id="e797c-208">我有多個含有虛擬網路的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e797c-208">I have multiple Azure subscriptions that contain virtual networks.</span></span> <span data-ttu-id="e797c-209">中的個別訂閱 tooa 單一 ExpressRoute 電路的虛擬網路可以連接嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-209">Can I connect virtual networks that are in separate subscriptions tooa single ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-210">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-210">Yes.</span></span> <span data-ttu-id="e797c-211">您可以向上 too10 授權其他 Azure 訂用帳戶 toouse 單一 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-211">You can authorize up too10 other Azure subscriptions toouse a single ExpressRoute circuit.</span></span> <span data-ttu-id="e797c-212">藉由啟用 hello ExpressRoute 高階功能，可以提高此限制。</span><span class="sxs-lookup"><span data-stu-id="e797c-212">This limit can be increased by enabling hello ExpressRoute premium feature.</span></span>

<span data-ttu-id="e797c-213">如需詳細資訊，請參閱[在多個訂用帳戶中共用 ExpressRoute 線路](expressroute-howto-linkvnet-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-213">For more information, see [Sharing an ExpressRoute circuit across multiple subscriptions](expressroute-howto-linkvnet-arm.md).</span></span>

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a><span data-ttu-id="e797c-214">已隔離的相同電路的虛擬網路連接的 toohello 彼此嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-214">Are virtual networks connected toohello same circuit isolated from each other?</span></span>

<span data-ttu-id="e797c-215">否。</span><span class="sxs-lookup"><span data-stu-id="e797c-215">No.</span></span> <span data-ttu-id="e797c-216">從路由的檢視方塊的所有虛擬網路連結 toohello 相同 ExpressRoute 電路屬於 hello 相同路由網域，而且不會互相隔離。</span><span class="sxs-lookup"><span data-stu-id="e797c-216">From a routing perspective, all virtual networks linked toohello same ExpressRoute circuit are part of hello same routing domain and are not isolated from each other.</span></span> <span data-ttu-id="e797c-217">如果您需要路由隔離，您會需要 toocreate 不同的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-217">If you need route isolation, you need toocreate a separate ExpressRoute circuit.</span></span>

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a><span data-ttu-id="e797c-218">可以有一個虛擬網路連接 toomore 比一個 ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-218">Can I have one virtual network connected toomore than one ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-219">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-219">Yes.</span></span> <span data-ttu-id="e797c-220">您可以連結具有向上 toofour ExpressRoute 電路的單一虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e797c-220">You can link a single virtual network with up toofour ExpressRoute circuits.</span></span> <span data-ttu-id="e797c-221">它們必須透過 4 個不同的 [ExpressRoute 位置](expressroute-locations.md)來訂購。</span><span class="sxs-lookup"><span data-stu-id="e797c-221">They must be ordered through four different [ExpressRoute locations](expressroute-locations.md).</span></span>

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a><span data-ttu-id="e797c-222">可以存取網際網路 hello 從我的虛擬網路連接的 tooExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-222">Can I access hello Internet from my virtual networks connected tooExpressRoute circuits?</span></span>

<span data-ttu-id="e797c-223">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-223">Yes.</span></span> <span data-ttu-id="e797c-224">如果您不具有公告預設路由 (0.0.0.0/0) 或網際網路路由首碼，透過 hello BGP 工作階段，您可以從虛擬網路連結 tooan ExpressRoute 電路連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="e797c-224">If you have not advertised default routes (0.0.0.0/0) or Internet route prefixes through hello BGP session, you can connect toohello Internet from a virtual network linked tooan ExpressRoute circuit.</span></span>

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a><span data-ttu-id="e797c-225">我可以封鎖網際網路連線 toovirtual 網路連線的 tooExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-225">Can I block Internet connectivity toovirtual networks connected tooExpressRoute circuits?</span></span>

<span data-ttu-id="e797c-226">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-226">Yes.</span></span> <span data-ttu-id="e797c-227">您可以公告預設路由 (0.0.0.0/0) tooblock 所有的網際網路連線 toovirtual 機器虛擬網路中部署和路由傳送所有流量透過 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-227">You can advertise default routes (0.0.0.0/0) tooblock all Internet connectivity toovirtual machines deployed within a virtual network and route all traffic out through hello ExpressRoute circuit.</span></span>

<span data-ttu-id="e797c-228">如果您通告預設路由，我們會強制流量 tooservices 提供透過公用互連 （例如 Azure 儲存體和 SQL 資料庫） 的回復 tooyour 內部部署。</span><span class="sxs-lookup"><span data-stu-id="e797c-228">If you advertise default routes, we force traffic tooservices offered over public peering (such as Azure storage and SQL DB) back tooyour premises.</span></span> <span data-ttu-id="e797c-229">您必須 tooconfigure 您路由器 tooreturn 的流量有 tooAzure 透過 hello 公用互連路徑或 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="e797c-229">You will have tooconfigure your routers tooreturn traffic tooAzure through hello public peering path or over hello Internet.</span></span>

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a><span data-ttu-id="e797c-230">可以虛擬網路連結的 toohello 相同 ExpressRoute 電路溝通 tooeach 其他嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-230">Can virtual networks linked toohello same ExpressRoute circuit talk tooeach other?</span></span>

<span data-ttu-id="e797c-231">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-231">Yes.</span></span> <span data-ttu-id="e797c-232">虛擬機器部署在虛擬網路連接 toohello 相同 ExpressRoute 電路可與對方進行通訊。</span><span class="sxs-lookup"><span data-stu-id="e797c-232">Virtual machines deployed in virtual networks connected toohello same ExpressRoute circuit can communicate with each other.</span></span>

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a><span data-ttu-id="e797c-233">我是否可以將虛擬網路的站對站連線與 ExpressRoute 搭配使用?</span><span class="sxs-lookup"><span data-stu-id="e797c-233">Can I use site-to-site connectivity for virtual networks in conjunction with ExpressRoute?</span></span>

<span data-ttu-id="e797c-234">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-234">Yes.</span></span> <span data-ttu-id="e797c-235">ExpressRoute 可與站對站 VPN 並存。</span><span class="sxs-lookup"><span data-stu-id="e797c-235">ExpressRoute can coexist with site-to-site VPNs.</span></span>

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a><span data-ttu-id="e797c-236">可以移動的虛擬網路從站對站 / 點對站組態 toouse ExpressRoute 嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-236">Can I move a virtual network from site-to-site / point-to-site configuration toouse ExpressRoute?</span></span>

<span data-ttu-id="e797c-237">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-237">Yes.</span></span> <span data-ttu-id="e797c-238">您將虛擬網路中有 toocreate ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="e797c-238">You will have toocreate an ExpressRoute gateway within your virtual network.</span></span> <span data-ttu-id="e797c-239">沒有與 hello 程序相關聯的短暫停機時間。</span><span class="sxs-lookup"><span data-stu-id="e797c-239">There is a small downtime associated with hello process.</span></span>

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a><span data-ttu-id="e797c-240">為什麼會有相關聯的虛擬網路上的 hello ExpressRoute 閘道的公用 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="e797c-240">Why is there a public IP address associated with hello ExpressRoute gateway on a virtual network?</span></span>

<span data-ttu-id="e797c-241">hello 公用 IP 位址用於只使用內部的管理。</span><span class="sxs-lookup"><span data-stu-id="e797c-241">hello public IP address is used for internal management only.</span></span> <span data-ttu-id="e797c-242">這個公用 IP 位址不是公開的 toohello 網際網路，並不會構成安全性風險的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e797c-242">This public IP address is not exposed toohello Internet, and does not constitute a security exposure of your virtual network.</span></span>

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a><span data-ttu-id="e797c-243">怎麼 tooconnect tooAzure 儲存體需要透過 ExpressRoute？</span><span class="sxs-lookup"><span data-stu-id="e797c-243">What do I need tooconnect tooAzure storage over ExpressRoute?</span></span>

<span data-ttu-id="e797c-244">您必須建立 ExpressRoute 電路，並設定公用對等互連的路由。</span><span class="sxs-lookup"><span data-stu-id="e797c-244">You must establish an ExpressRoute circuit and configure routes for public peering.</span></span>

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a><span data-ttu-id="e797c-245">有我可以公告的路由的 hello 數目的限制嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-245">Are there limits on hello number of routes I can advertise?</span></span>

<span data-ttu-id="e797c-246">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-246">Yes.</span></span> <span data-ttu-id="e797c-247">我們接受 too4000 用於私人互連的路由前置詞和 200 每一個用於公用互連，Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-247">We accept up too4000 route prefixes for private peering and 200 each for public peering and Microsoft peering.</span></span> <span data-ttu-id="e797c-248">您可以增加此 too10，000 路由用於私人互連，如果您啟用 hello ExpressRoute 高階功能。</span><span class="sxs-lookup"><span data-stu-id="e797c-248">You can increase this too10,000 routes for private peering if you enable hello ExpressRoute premium feature.</span></span>

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a><span data-ttu-id="e797c-249">有我可以透過 hello BGP 工作階段公告的 IP 範圍的限制嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-249">Are there restrictions on IP ranges I can advertise over hello BGP session?</span></span>

<span data-ttu-id="e797c-250">我們不接受在 hello 公用的私人首碼 (RFC1918) 與 Microsoft 對等互連 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e797c-250">We do not accept private prefixes (RFC1918) in hello public and Microsoft peering BGP session.</span></span>

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a><span data-ttu-id="e797c-251">如果我超出 hello BGP 限制，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="e797c-251">What happens if I exceed hello BGP limits?</span></span>

<span data-ttu-id="e797c-252">BGP 工作階段將會被刪除。</span><span class="sxs-lookup"><span data-stu-id="e797c-252">BGP sessions will be dropped.</span></span> <span data-ttu-id="e797c-253">一旦 hello 首碼數量低於 hello 限制，它們會被重設。</span><span class="sxs-lookup"><span data-stu-id="e797c-253">They will be reset once hello prefix count goes below hello limit.</span></span>

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a><span data-ttu-id="e797c-254">什麼是的 hello ExpressRoute BGP 保存的時間？</span><span class="sxs-lookup"><span data-stu-id="e797c-254">What is hello ExpressRoute BGP hold time?</span></span> <span data-ttu-id="e797c-255">可調整此保留時間嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-255">Can it be adjusted?</span></span>

<span data-ttu-id="e797c-256">hello 保留時間是 180。</span><span class="sxs-lookup"><span data-stu-id="e797c-256">hello hold time is 180.</span></span> <span data-ttu-id="e797c-257">每隔 60 秒，就會傳送 hello 保持連線訊息。</span><span class="sxs-lookup"><span data-stu-id="e797c-257">hello keep-alive messages are sent every 60 seconds.</span></span> <span data-ttu-id="e797c-258">這些被固定 hello Microsoft 端，無法變更設定。</span><span class="sxs-lookup"><span data-stu-id="e797c-258">These are fixed settings on hello Microsoft side that cannot be changed.</span></span> <span data-ttu-id="e797c-259">很可能您 tooconfigure 不同計時器，並將據此交涉 hello BGP 工作階段參數。</span><span class="sxs-lookup"><span data-stu-id="e797c-259">It is possible for you tooconfigure different timers, and hello BGP session parameters will be negotiated accordingly.</span></span>

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a><span data-ttu-id="e797c-260">我通告 hello 預設路由 (0.0.0.0/0) toomy 虛擬網路之後，我無法啟動我的 Azure Vm 上執行的 Windows。</span><span class="sxs-lookup"><span data-stu-id="e797c-260">After I advertise hello default route (0.0.0.0/0) toomy virtual networks, I can't activate Windows running on my Azure VMs.</span></span> <span data-ttu-id="e797c-261">如何 tooI 修正這個問題？</span><span class="sxs-lookup"><span data-stu-id="e797c-261">How tooI fix this?</span></span>

<span data-ttu-id="e797c-262">下列步驟的 hello 協助辨識 hello 啟用要求的 Azure:</span><span class="sxs-lookup"><span data-stu-id="e797c-262">hello following steps help Azure recognize hello activation request:</span></span>

1. <span data-ttu-id="e797c-263">建立 hello 公用對等 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-263">Establish hello public peering for your ExpressRoute circuit.</span></span>
2. <span data-ttu-id="e797c-264">執行 DNS 查閱和尋找 hello IP 位址**kms.core.windows.net**</span><span class="sxs-lookup"><span data-stu-id="e797c-264">Perform a DNS lookup and find hello IP address of **kms.core.windows.net**</span></span>
3. <span data-ttu-id="e797c-265">hello 金鑰管理服務必須辨識該 hello 啟用要求來自 Azure 與實行 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="e797c-265">hello Key Management Service must recognize that hello activation request comes from Azure and honor hello request.</span></span> <span data-ttu-id="e797c-266">執行下列三個工作的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="e797c-266">Perform one of hello following three tasks:</span></span>

   * <span data-ttu-id="e797c-267">您在內部部署網路上路由傳送嗨流量預定 hello 您在步驟 2 後 tooAzure 透過 hello 公用對等互連中取得的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e797c-267">On your on-premises network, route hello traffic destined for hello IP address that you obtained in step 2 back tooAzure via hello public peering.</span></span>
   * <span data-ttu-id="e797c-268">具有您 NSP 提供者線 pin hello 流量後的 tooAzure 透過 hello 公用對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-268">Have your NSP provider hair-pin hello traffic back tooAzure via hello public peering.</span></span>
   * <span data-ttu-id="e797c-269">建立使用者定義的路由有網際網路的下一個躍點，該點 hello IP，並將它套用 toohello 子網路，這些虛擬機器的所在。</span><span class="sxs-lookup"><span data-stu-id="e797c-269">Create a user-defined route that points hello IP that has Internet as a next hop, and apply it toohello subnet(s) where these virtual machines are.</span></span>

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="e797c-270">可以變更 hello 頻寬的 ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-270">Can I change hello bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-271">是，您可以嘗試 tooincrease hello 頻寬的 ExpressRoute 循環中 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e797c-271">Yes, you can attempt tooincrease hello bandwidth of your ExpressRoute circuit in hello Azure portal, or by using PowerShell.</span></span> <span data-ttu-id="e797c-272">如果您的電路建立所在的 hello 實體連接埠上有可用的容量，您的變更將會成功。</span><span class="sxs-lookup"><span data-stu-id="e797c-272">If there is capacity available on hello physical port on which your circuit was created, your change succeeds.</span></span> 

<span data-ttu-id="e797c-273">如果您的變更失敗，表示可能是沒有剩餘的 hello 目前的連接埠足夠容量，而且您需要 toocreate 新的 ExpressRoute 電路與 hello 較高的頻寬，或在該位置沒有任何額外的容量，在此情況下您將無法tooincrease hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="e797c-273">If your change fails, it means either there isn’t enough capacity left on hello current port and you need toocreate a new ExpressRoute circuit with hello higher bandwidth, or that there is no additional capacity at that location, in which case you won't be able tooincrease hello bandwidth.</span></span> 

<span data-ttu-id="e797c-274">您也必須 toofollow 與您的連線提供者 tooensure 他們更新其網路 toosupport hello 頻寬增加內 hello 節流。</span><span class="sxs-lookup"><span data-stu-id="e797c-274">You will also have toofollow up with your connectivity provider tooensure that they update hello throttles within their networks toosupport hello bandwidth increase.</span></span> <span data-ttu-id="e797c-275">您無法，不過，減少 hello 頻寬的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="e797c-275">You cannot, however, reduce hello bandwidth of your ExpressRoute circuit.</span></span> <span data-ttu-id="e797c-276">您擁有 toocreate 新的 ExpressRoute 電路擁有較低頻寬，並且刪除 hello 舊循環。</span><span class="sxs-lookup"><span data-stu-id="e797c-276">You have toocreate a new ExpressRoute circuit with lower bandwidth and delete hello old circuit.</span></span>

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a><span data-ttu-id="e797c-277">如何變更 hello 頻寬的 ExpressRoute 電路？</span><span class="sxs-lookup"><span data-stu-id="e797c-277">How do I change hello bandwidth of an ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-278">您可以更新 hello 使用 hello REST API 或 PowerShell cmdlet 的 hello ExpressRoute 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="e797c-278">You can update hello bandwidth of hello ExpressRoute circuit using hello REST API or PowerShell cmdlet.</span></span>

## <a name="expressroute-premium"></a><span data-ttu-id="e797c-279">ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="e797c-279">ExpressRoute premium</span></span>

### <a name="what-is-expressroute-premium"></a><span data-ttu-id="e797c-280">什麼是 ExpressRoute Premium？</span><span class="sxs-lookup"><span data-stu-id="e797c-280">What is ExpressRoute premium?</span></span>

<span data-ttu-id="e797c-281">ExpressRoute premium 是 hello 的集合下列功能：</span><span class="sxs-lookup"><span data-stu-id="e797c-281">ExpressRoute premium is a collection of hello following features:</span></span>

* <span data-ttu-id="e797c-282">增加路由的資料表限制，從 4000 路由 too10，000 用於私人互連的路由。</span><span class="sxs-lookup"><span data-stu-id="e797c-282">Increased routing table limit from 4000 routes too10,000 routes for private peering.</span></span>
* <span data-ttu-id="e797c-283">增加可以是連線的 toohello ExpressRoute 電路的 Vnet 數目 （預設值為 10）。</span><span class="sxs-lookup"><span data-stu-id="e797c-283">Increased number of VNets that can be connected toohello ExpressRoute circuit (default is 10).</span></span> <span data-ttu-id="e797c-284">如需詳細資訊，請參閱 hello [ExpressRoute 限制](#limits)資料表。</span><span class="sxs-lookup"><span data-stu-id="e797c-284">For more information, see hello [ExpressRoute Limits](#limits) table.</span></span>
* <span data-ttu-id="e797c-285">連線 tooOffice 365 和 Dynamics 365。</span><span class="sxs-lookup"><span data-stu-id="e797c-285">Connectivity tooOffice 365 and Dynamics 365.</span></span>
* <span data-ttu-id="e797c-286">全域 hello Microsoft 核心網路上的連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-286">Global connectivity over hello Microsoft core network.</span></span> <span data-ttu-id="e797c-287">您現在可將某一個地緣政治區域中的 VNet 與另一個區域中的 ExpressRoute 線路連結。</span><span class="sxs-lookup"><span data-stu-id="e797c-287">You can now link a VNet in one geopolitical region with an ExpressRoute circuit in another region.</span></span><br>
    <span data-ttu-id="e797c-288">**範例：**</span><span class="sxs-lookup"><span data-stu-id="e797c-288">**Examples:**</span></span>

    *  <span data-ttu-id="e797c-289">您可以連結在西歐 tooan 在美國矽谷建立 ExpressRoute 電路建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="e797c-289">You can link a VNet created in Europe West tooan ExpressRoute circuit created in Silicon Valley.</span></span> 
    *  <span data-ttu-id="e797c-290">在 hello 公用對等互連，其他地緣政治區域前置詞已公告，您可以從在美國矽谷電路連接到，比方說，在西歐 SQL Azure。</span><span class="sxs-lookup"><span data-stu-id="e797c-290">On hello public peering, prefixes from other geopolitical regions are advertised such that you can connect to, for example, SQL Azure in Europe West from a circuit in Silicon Valley.</span></span>


### <span data-ttu-id="e797c-291"><a name="limits"></a>多少 Vnet 可以將連結 tooan ExpressRoute 電路如果啟用 ExpressRoute premium？</span><span class="sxs-lookup"><span data-stu-id="e797c-291"><a name="limits"></a>How many VNets can I link tooan ExpressRoute circuit if I enabled ExpressRoute premium?</span></span>

<span data-ttu-id="e797c-292">hello 下列表格顯示 hello ExpressRoute 限制和每個 ExpressRoute 電路的 Vnet 的 hello 數目：</span><span class="sxs-lookup"><span data-stu-id="e797c-292">hello following tables show hello ExpressRoute limits and hello number of VNets per ExpressRoute circuit:</span></span>

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a><span data-ttu-id="e797c-293">我要如何啟用 ExpressRoute Premium？</span><span class="sxs-lookup"><span data-stu-id="e797c-293">How do I enable ExpressRoute premium?</span></span>

<span data-ttu-id="e797c-294">ExpressRoute 高階功能時啟用 hello 功能時，可以啟用，而且可以藉由更新 hello 循環狀態關機。</span><span class="sxs-lookup"><span data-stu-id="e797c-294">ExpressRoute premium features can be enabled when hello feature is enabled, and can be shut down by updating hello circuit state.</span></span> <span data-ttu-id="e797c-295">您可以在電路建立時，啟用 ExpressRoute premium 或可以呼叫 hello REST API / PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e797c-295">You can enable ExpressRoute premium at circuit creation time, or can call hello REST API / PowerShell cmdlet.</span></span>

### <a name="how-do-i-disable-expressroute-premium"></a><span data-ttu-id="e797c-296">我要如何停用 ExpressRoute Premium？</span><span class="sxs-lookup"><span data-stu-id="e797c-296">How do I disable ExpressRoute premium?</span></span>

<span data-ttu-id="e797c-297">您可以藉由呼叫 hello REST API 或 PowerShell cmdlet 來停用 ExpressRoute premium。</span><span class="sxs-lookup"><span data-stu-id="e797c-297">You can disable ExpressRoute premium by calling hello REST API or PowerShell cmdlet.</span></span> <span data-ttu-id="e797c-298">您必須確定您已停用 ExpressRoute premium 之前可能向您連線需求 toomeet hello 的預設限制。</span><span class="sxs-lookup"><span data-stu-id="e797c-298">You must make sure that you have scaled your connectivity needs toomeet hello default limits before you disable ExpressRoute premium.</span></span> <span data-ttu-id="e797c-299">如果您的使用率縮放比例超出 hello 預設限制，hello 要求 toodisable ExpressRoute 高階將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e797c-299">If your utilization scales beyond hello default limits, hello request toodisable ExpressRoute premium fails.</span></span>

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a><span data-ttu-id="e797c-300">可以我挑選並選擇 hello 我想要從 hello premium 功能集的功能嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-300">Can I pick and choose hello features I want from hello premium feature set?</span></span>

<span data-ttu-id="e797c-301">否。</span><span class="sxs-lookup"><span data-stu-id="e797c-301">No.</span></span> <span data-ttu-id="e797c-302">您無法挑選 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="e797c-302">You can't pick hello features.</span></span> <span data-ttu-id="e797c-303">當您開啟 ExpressRoute Premium 時，我們便會將所有功能啟用。</span><span class="sxs-lookup"><span data-stu-id="e797c-303">We enable all features when you turn on ExpressRoute premium.</span></span>

### <a name="how-much-does-expressroute-premium-cost"></a><span data-ttu-id="e797c-304">ExpressRoute Premium 需要多少錢？</span><span class="sxs-lookup"><span data-stu-id="e797c-304">How much does ExpressRoute premium cost?</span></span>

<span data-ttu-id="e797c-305">請參閱太[定價詳細資料](https://azure.microsoft.com/pricing/details/expressroute/)成本。</span><span class="sxs-lookup"><span data-stu-id="e797c-305">Refer too[pricing details](https://azure.microsoft.com/pricing/details/expressroute/) for cost.</span></span>

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a><span data-ttu-id="e797c-306">請勿我支付 ExpressRoute premium 除了 toostandard ExpressRoute 費用嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-306">Do I pay for ExpressRoute premium in addition toostandard ExpressRoute charges?</span></span>

<span data-ttu-id="e797c-307">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-307">Yes.</span></span> <span data-ttu-id="e797c-308">ExpressRoute premium 費用 適用於 ExpressRoute 電路費用和 hello 連線服務提供者所需的費用。</span><span class="sxs-lookup"><span data-stu-id="e797c-308">ExpressRoute premium charges apply on top of ExpressRoute circuit charges and charges required by hello connectivity provider.</span></span>

## <a name="expressroute-for-office-365-and-dynamics-365"></a><span data-ttu-id="e797c-309">Office 365 和 Dynamics 365 的 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e797c-309">ExpressRoute for Office 365 and Dynamics 365</span></span>

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="e797c-310">如何建立 ExpressRoute 電路 tooconnect tooOffice 365 服務和 Dynamics 365？</span><span class="sxs-lookup"><span data-stu-id="e797c-310">How do I create an ExpressRoute circuit tooconnect tooOffice 365 services and Dynamics 365?</span></span>

1. <span data-ttu-id="e797c-311">檢閱 hello [ExpressRoute 必要條件頁面](expressroute-prerequisites.md)toomake 確定您符合 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="e797c-311">Review hello [ExpressRoute prerequisites page](expressroute-prerequisites.md) toomake sure you meet hello requirements.</span></span>
2. <span data-ttu-id="e797c-312">符合您的連線需要 tooensure，檢閱 hello 的服務提供者和位置清單中 hello [ExpressRoute 合作夥伴和位置](expressroute-locations.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="e797c-312">tooensure that your connectivity needs are met, review hello list of service providers and locations in hello [ExpressRoute partners and locations](expressroute-locations.md) article.</span></span>
3. <span data-ttu-id="e797c-313">透過檢閱 [Office 365 的網路規劃和效能調整](http://aka.ms/tune/)來計劃您的容量需求。</span><span class="sxs-lookup"><span data-stu-id="e797c-313">Plan your capacity requirements by reviewing [Network planning and performance tuning for Office 365](http://aka.ms/tune/).</span></span>
4. <span data-ttu-id="e797c-314">Hello 工作流程 tooset 連線設定中所列步驟 hello [ExpressRoute 循環佈建和循環狀態的工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-314">Follow hello steps listed in hello workflows tooset up connectivity [ExpressRoute workflows for circuit provisioning and circuit states](expressroute-workflows.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e797c-315">請確定您已設定連線 tooOffice 365 服務和 Dynamics 365 時啟用 ExpressRoute premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="e797c-315">Make sure that you have enabled ExpressRoute premium add-on when configuring connectivity tooOffice 365 services and Dynamics 365.</span></span>
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="e797c-316">我需要 tooenable Azure 公用對等互連 tooconnect tooOffice 365 服務和 Dynamics 365？</span><span class="sxs-lookup"><span data-stu-id="e797c-316">Do I need tooenable Azure public peering tooconnect tooOffice 365 services and Dynamics 365?</span></span>

<span data-ttu-id="e797c-317">否，您只需要 tooenable Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-317">No, you only need tooenable Microsoft Peering.</span></span> <span data-ttu-id="e797c-318">驗證流量 tooAzure AD 會傳送到 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-318">Authentication traffic tooAzure AD is sent through Microsoft Peering.</span></span> 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a><span data-ttu-id="e797c-319">可以連線 tooOffice 365 服務和 Dynamics 365 支援我現有的 ExpressRoute 電路嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-319">Can my existing ExpressRoute circuits support connectivity tooOffice 365 services and Dynamics 365?</span></span>

<span data-ttu-id="e797c-320">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-320">Yes.</span></span> <span data-ttu-id="e797c-321">您現有的 ExpressRoute 電路可以設定的 toosupport 連線 tooOffice 365 服務。</span><span class="sxs-lookup"><span data-stu-id="e797c-321">Your existing ExpressRoute circuit can be configured toosupport connectivity tooOffice 365 services.</span></span> <span data-ttu-id="e797c-322">請確定您有足夠的容量 tooconnect tooOffice 365 服務，且您已啟用高階的附加元件。</span><span class="sxs-lookup"><span data-stu-id="e797c-322">Make sure that you have sufficient capacity tooconnect tooOffice 365 services and that you have enabled premium add-on.</span></span> <span data-ttu-id="e797c-323">[Office 365 的網路規劃和效能調整](http://aka.ms/tune/)可協助您規劃連線需求。</span><span class="sxs-lookup"><span data-stu-id="e797c-323">[Network planning and performance tuning for Office 365](http://aka.ms/tune/) helps you plan your connectivity needs.</span></span> <span data-ttu-id="e797c-324">另請參閱 [建立和修改 ExpressRoute 電路](expressroute-howto-circuit-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-324">Also, see [Create and modify an ExpressRoute circuit](expressroute-howto-circuit-classic.md).</span></span>

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="e797c-325">透過 ExpressRoute 連線可以存取哪些 Office 365 服務？</span><span class="sxs-lookup"><span data-stu-id="e797c-325">What Office 365 services can be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="e797c-326">請參閱太[Office 365 Url 與 IP 位址範圍](http://aka.ms/o365endpoints)服務透過 ExpressRoute 受到支援的最新清單的頁面。</span><span class="sxs-lookup"><span data-stu-id="e797c-326">Refer too[Office 365 URLs and IP address ranges](http://aka.ms/o365endpoints) page for an up-to-date list of services supported over ExpressRoute.</span></span>

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a><span data-ttu-id="e797c-327">適用於 Office 365 服務和 Dynamics 365 的 ExpressRoute 費用是多少？</span><span class="sxs-lookup"><span data-stu-id="e797c-327">How much does ExpressRoute for Office 365 services and Dynamics 365 cost?</span></span>

<span data-ttu-id="e797c-328">Office 365 服務和 Dynamics 365 需要啟用 premium 附加元件 toobe。</span><span class="sxs-lookup"><span data-stu-id="e797c-328">Office 365 services and Dynamics 365 require premium add-on toobe enabled.</span></span> <span data-ttu-id="e797c-329">請參閱 hello[定價詳細資料頁面](https://azure.microsoft.com/pricing/details/expressroute/)成本。</span><span class="sxs-lookup"><span data-stu-id="e797c-329">See hello [pricing details page](https://azure.microsoft.com/pricing/details/expressroute/) for costs.</span></span>

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a><span data-ttu-id="e797c-330">哪些區域支援 ExpressRoute for Office 365？</span><span class="sxs-lookup"><span data-stu-id="e797c-330">What regions is ExpressRoute for Office 365 supported in?</span></span>

<span data-ttu-id="e797c-331">如需相關資訊，請參閱 [ExpressRoute 合作夥伴和位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-331">See [ExpressRoute partners and locations](expressroute-locations.md) for information.</span></span>

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a><span data-ttu-id="e797c-332">我可以存取 Office 365 透過 hello 網際網路，即使我的組織已設定 ExpressRoute 嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-332">Can I access Office 365 over hello Internet, even if ExpressRoute was configured for my organization?</span></span>

<span data-ttu-id="e797c-333">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-333">Yes.</span></span> <span data-ttu-id="e797c-334">即使已針對您的網路設定 ExpressRoute，是透過 hello 網際網路，連線到 office 365 的服務端點。</span><span class="sxs-lookup"><span data-stu-id="e797c-334">Office 365 service endpoints are reachable through hello Internet, even though ExpressRoute has been configured for your network.</span></span> <span data-ttu-id="e797c-335">如果您是透過 ExpressRoute 設定的 tooconnect tooOffice 365 服務的位置中，您會透過 ExpressRoute 進行連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-335">If you are in a location that is configured tooconnect tooOffice 365 services through ExpressRoute, you will connect through ExpressRoute.</span></span>

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a><span data-ttu-id="e797c-336">我是否可以透過 Azure 美國政府 ExpressRoute 電路存取 Office 365 US Government Community (GCC) 服務？</span><span class="sxs-lookup"><span data-stu-id="e797c-336">Can I access Office 365 US Government Community (GCC) services over an Azure US Government ExpressRoute circuit?</span></span>

<span data-ttu-id="e797c-337">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-337">Yes.</span></span> <span data-ttu-id="e797c-338">Office 365 GCC 服務端點都可以透過 hello Azure 美國政府 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="e797c-338">Office 365 GCC service endpoints are reachable through hello Azure US Government ExpressRoute.</span></span> <span data-ttu-id="e797c-339">不過，您第一次需要 tooopen 支援票證 hello 想 tooadvertise tooMicrosoft 的 Azure 入口網站 tooprovide hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="e797c-339">However, you first need tooopen a support ticket on hello Azure portal tooprovide hello prefixes you intend tooadvertise tooMicrosoft.</span></span> <span data-ttu-id="e797c-340">解決 hello 支援票證後，將會建立連線 tooOffice 365 GCC 服務。</span><span class="sxs-lookup"><span data-stu-id="e797c-340">Your connectivity tooOffice 365 GCC services will be established after hello support ticket is resolved.</span></span> 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a><span data-ttu-id="e797c-341">是否可透過 ExpressRoute 連線存取 Dynamics 365 for Operations (先前稱為 Dynamics AX Online)？</span><span class="sxs-lookup"><span data-stu-id="e797c-341">Can Dynamics 365 for Operations (formerly known as Dynamics AX Online) be accessed over an ExpressRoute connection?</span></span>

<span data-ttu-id="e797c-342">是。</span><span class="sxs-lookup"><span data-stu-id="e797c-342">Yes.</span></span> <span data-ttu-id="e797c-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) 是裝載於 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="e797c-343">[Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) is hosted on Azure.</span></span> <span data-ttu-id="e797c-344">您可以啟用您的 ExpressRoute 電路 tooconnect tooit 上 Azure 公用對等。</span><span class="sxs-lookup"><span data-stu-id="e797c-344">You can enable Azure public peering on your ExpressRoute circuit tooconnect tooit.</span></span>

## <a name="route-filters-for-microsoft-peering"></a><span data-ttu-id="e797c-345">Microsoft 對等互連的路由篩選</span><span class="sxs-lookup"><span data-stu-id="e797c-345">Route filters for Microsoft peering</span></span>

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a><span data-ttu-id="e797c-346">開啟 Microsoft 對等互連 hello 第一次，會看到哪些路由？</span><span class="sxs-lookup"><span data-stu-id="e797c-346">I am turning on Microsoft peering for hello first time, what routes will I see?</span></span>

<span data-ttu-id="e797c-347">您不會看到任何路由。</span><span class="sxs-lookup"><span data-stu-id="e797c-347">You will not see any routes.</span></span> <span data-ttu-id="e797c-348">您有 tooattach 路由篩選 tooyour 電路 toostart 前置詞通告。</span><span class="sxs-lookup"><span data-stu-id="e797c-348">You have tooattach a route filter tooyour circuit toostart prefix advertisements.</span></span> <span data-ttu-id="e797c-349">如需指示，請參閱[針對 Microsoft 對等互連設定路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-349">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a><span data-ttu-id="e797c-350">我已開啟的 Microsoft 對等互連，而且現在我嘗試 tooselect Exchange Online，但是它會讓我我不是授權的 toodo 錯誤它。</span><span class="sxs-lookup"><span data-stu-id="e797c-350">I turned on Microsoft peering and now I am trying tooselect Exchange Online, but it is giving me an error that I am not authorized toodo it.</span></span>

<span data-ttu-id="e797c-351">當使用路由篩選時，任何客戶都可開啟 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-351">When using route filters, any customer can turn on Microsoft peering.</span></span> <span data-ttu-id="e797c-352">不過，使用 Office 365 服務，您仍然需要 tooget 由 Office 365 授權。</span><span class="sxs-lookup"><span data-stu-id="e797c-352">However, for consuming Office 365 services, you still need tooget authorized by Office 365.</span></span>

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a><span data-ttu-id="e797c-353">需要透過 Microsoft 對等互連開啟 Dynamics 365 tooget 授權嗎？</span><span class="sxs-lookup"><span data-stu-id="e797c-353">Do I need tooget authorization for turning on Dynamics 365 over Microsoft peering?</span></span>

<span data-ttu-id="e797c-354">否，您不需要 Dynamics 365 的授權。</span><span class="sxs-lookup"><span data-stu-id="e797c-354">No, you do not need authorization for Dynamics 365.</span></span> <span data-ttu-id="e797c-355">您不需授權就可建立規則和選取 Dynamics 365 社群。</span><span class="sxs-lookup"><span data-stu-id="e797c-355">You can create a rule and select Dynamics 365 community without authorization.</span></span>

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a><span data-ttu-id="e797c-356">我已經有 Microsoft 對等互連，該如何利用路由篩選？</span><span class="sxs-lookup"><span data-stu-id="e797c-356">I already have Microsoft peering, how can I take advantage of route filters?</span></span>

<span data-ttu-id="e797c-357">您可以建立路由篩選器，您想 toouse，並將選取的 hello 服務 hello 篩選 tooyour Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="e797c-357">You can create a route filter, select hello services you want toouse, and attach hello filter tooyour Microsoft peering.</span></span> <span data-ttu-id="e797c-358">如需指示，請參閱[針對 Microsoft 對等互連設定路由篩選](how-to-routefilter-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="e797c-358">For instructions, see [Configure route filters for Microsoft peering](how-to-routefilter-powershell.md).</span></span>

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a><span data-ttu-id="e797c-359">我有 Microsoft 對等互連的位置，現在我試著 tooenable 它在其他位置並沒有看到任何前置詞。</span><span class="sxs-lookup"><span data-stu-id="e797c-359">I have Microsoft peering at one location, now I am trying tooenable it at another location and I am not seeing any prefixes.</span></span>

* <span data-ttu-id="e797c-360">Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。</span><span class="sxs-lookup"><span data-stu-id="e797c-360">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span>

* <span data-ttu-id="e797c-361">Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="e797c-361">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="e797c-362">根據預設，您不會看見任何首碼。</span><span class="sxs-lookup"><span data-stu-id="e797c-362">You will see no prefixes by default.</span></span>
