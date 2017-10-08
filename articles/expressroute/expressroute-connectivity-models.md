---
title: "ExpressRoute 的連線模型： 透過網路服務提供者、 交換，與乙太網路提供者連線 tooMicrosoft Azure |Microsoft 文件"
description: "本文說明 hello 不同的 hello 客戶網路和 Microsoft Azure、 Office 365 和 Dynamics 365 服務之間的連接模式。 客戶可以使用 MPLS 提供者、雲端 Exchange 和乙太網路提供者。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a><span data-ttu-id="94217-104">ExpressRoute 連線模型</span><span class="sxs-lookup"><span data-stu-id="94217-104">ExpressRoute connectivity models</span></span>
<span data-ttu-id="94217-105">您可以建立您的內部部署網路與 hello Microsoft 雲端之間的連線以三個不同的方式， [CloudExchange 共](#CloudExchange)，[點對點乙太網路連線](#Ethernet)，和[Any-any (IPVPN) 連線](#IPVPN)。</span><span class="sxs-lookup"><span data-stu-id="94217-105">You can create a connection between your on-premises network and hello Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span></span> <span data-ttu-id="94217-106">連線提供者可以提供一或多個連線模型。</span><span class="sxs-lookup"><span data-stu-id="94217-106">Connectivity providers can offer one or more connectivity models.</span></span> <span data-ttu-id="94217-107">您可以使用最適合您連接提供者 toopick hello 模型。</span><span class="sxs-lookup"><span data-stu-id="94217-107">You can work with your connectivity provider toopick hello model that works best for you.</span></span>
<br><br>

![ExpressRoute 連線模型圖表](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <span data-ttu-id="94217-109"><a name="CloudExchange"></a>共置於雲端 Exchange</span><span class="sxs-lookup"><span data-stu-id="94217-109"><a name="CloudExchange"></a>Co-located at a cloud exchange</span></span>
<span data-ttu-id="94217-110">如果您同時位於雲端交換設備，您可以排序虛擬交叉連線 toohello 透過 hello 代管提供者的乙太網路交換的 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="94217-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections toohello Microsoft cloud through hello co-location provider’s Ethernet exchange.</span></span> <span data-ttu-id="94217-111">代管提供者可以提供第 2 層交叉連線或受管理第 3 層交叉連線 hello Microsoft 雲端基礎結構在 hello 共置設備之間。</span><span class="sxs-lookup"><span data-stu-id="94217-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in hello co-location facility and hello Microsoft cloud.</span></span>

## <span data-ttu-id="94217-112"><a name="Ethernet"></a>點對點乙太網路連線</span><span class="sxs-lookup"><span data-stu-id="94217-112"><a name="Ethernet"></a>Point-to-point Ethernet connections</span></span>
<span data-ttu-id="94217-113">您可以透過點對點乙太網路連結連接您在內部部署資料中心/辦公室 toohello Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="94217-113">You can connect your on-premises datacenters/offices toohello Microsoft cloud through point-to-point Ethernet links.</span></span> <span data-ttu-id="94217-114">點對點乙太網路提供者可以提供第 2 層連線，或管理您的站台與 hello Microsoft 雲端之間的第 3 層連線。</span><span class="sxs-lookup"><span data-stu-id="94217-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and hello Microsoft cloud.</span></span>

## <span data-ttu-id="94217-115"><a name="IPVPN"></a>任意點對任意點 (IPVPN) 網路</span><span class="sxs-lookup"><span data-stu-id="94217-115"><a name="IPVPN"></a>Any-to-any (IPVPN) networks</span></span>
<span data-ttu-id="94217-116">您可以整合您的 WAN 與 hello Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="94217-116">You can integrate your WAN with hello Microsoft cloud.</span></span> <span data-ttu-id="94217-117">IPVPN 提供者 (通常是 MPLS VPN) 在您的分公司與資料中心之間提供任意點對任意點連線。</span><span class="sxs-lookup"><span data-stu-id="94217-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span></span> <span data-ttu-id="94217-118">hello Microsoft 雲端可以互連的 tooyour WAN toomake 它看起來就像任何其他分公司。</span><span class="sxs-lookup"><span data-stu-id="94217-118">hello Microsoft cloud can be interconnected tooyour WAN toomake it look just like any other branch office.</span></span> <span data-ttu-id="94217-119">WAN 提供者通常會提供受管理的第 3 層連線能力。</span><span class="sxs-lookup"><span data-stu-id="94217-119">WAN providers typically offer managed Layer 3 connectivity.</span></span> <span data-ttu-id="94217-120">ExpressRoute 功能和功能是 hello 的所有相同的所有連接模型上方。</span><span class="sxs-lookup"><span data-stu-id="94217-120">ExpressRoute capabilities and features are all identical across all of hello above connectivity models.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="94217-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94217-121">Next steps</span></span>
* <span data-ttu-id="94217-122">了解 ExpressRoute 連線和路由網域。</span><span class="sxs-lookup"><span data-stu-id="94217-122">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="94217-123">請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="94217-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="94217-124">了解 ExpressRoute 功能。</span><span class="sxs-lookup"><span data-stu-id="94217-124">Learn about ExpressRoute features.</span></span> <span data-ttu-id="94217-125">請參閱 hello [ExpressRoute 技術概觀](expressroute-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="94217-125">See hello [ExpressRoute Technical Overview](expressroute-introduction.md)</span></span>
* <span data-ttu-id="94217-126">尋找服務提供者。</span><span class="sxs-lookup"><span data-stu-id="94217-126">Find a service provider.</span></span> <span data-ttu-id="94217-127">請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="94217-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="94217-128">請確定符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="94217-128">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="94217-129">請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="94217-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="94217-130">請參閱 toohello 需求[路由](expressroute-routing.md)， [NAT](expressroute-nat.md)，和[QoS](expressroute-qos.md)。</span><span class="sxs-lookup"><span data-stu-id="94217-130">Refer toohello requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="94217-131">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="94217-131">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="94217-132">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="94217-132">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="94217-133">設定路由</span><span class="sxs-lookup"><span data-stu-id="94217-133">Configure routing</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="94217-134">連結的 VNet tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="94217-134">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
