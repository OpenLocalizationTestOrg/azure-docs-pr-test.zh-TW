---
title: "ExpressRoute 連線模型：透過網路服務提供者、Exchange 和乙太網路提供者連接到 Microsoft Azure | Microsoft Docs"
description: "本文說明在客戶網路與 Microsoft Azure、Office 365 和 Dynamics 365 服務之間的各種連線模式。 客戶可以使用 MPLS 提供者、雲端 Exchange 和乙太網路提供者。"
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
ms.openlocfilehash: 00f97da2189491103c461b49ac82feb92d8f4b9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-connectivity-models"></a><span data-ttu-id="1856d-104">ExpressRoute 連線模型</span><span class="sxs-lookup"><span data-stu-id="1856d-104">ExpressRoute connectivity models</span></span>
<span data-ttu-id="1856d-105">有三種方法可以在內部部署網路與 Microsoft Cloud 之間建立連線：[CloudExchange 共置](#CloudExchange)、[點對點乙太網路連線](#Ethernet)和[任意點對任意點 (IPVPN) 連線](#IPVPN)。</span><span class="sxs-lookup"><span data-stu-id="1856d-105">You can create a connection between your on-premises network and the Microsoft cloud in three different ways, [CloudExchange Co-location](#CloudExchange), [Point-to-point Ethernet Connection](#Ethernet), and [Any-to-any (IPVPN) Connection](#IPVPN).</span></span> <span data-ttu-id="1856d-106">連線提供者可以提供一或多個連線模型。</span><span class="sxs-lookup"><span data-stu-id="1856d-106">Connectivity providers can offer one or more connectivity models.</span></span> <span data-ttu-id="1856d-107">您可以洽詢連線提供者來選擇最適合您的模型。</span><span class="sxs-lookup"><span data-stu-id="1856d-107">You can work with your connectivity provider to pick the model that works best for you.</span></span>
<br><br>

![ExpressRoute 連線模型圖表](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <span data-ttu-id="1856d-109"><a name="CloudExchange"></a>共置於雲端 Exchange</span><span class="sxs-lookup"><span data-stu-id="1856d-109"><a name="CloudExchange"></a>Co-located at a cloud exchange</span></span>
<span data-ttu-id="1856d-110">如果您共置於具有雲端交換的設施中，您可以訂購虛擬交叉連接，透過共置提供者的乙太網路交換而連接至 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="1856d-110">If you are co-located in a facility with a cloud exchange, you can order virtual cross-connections to the Microsoft cloud through the co-location provider’s Ethernet exchange.</span></span> <span data-ttu-id="1856d-111">共置提供者可以在您於共置設施中的基礎結構與 Microsoft 雲端之間，提供第 2 層交叉連接或受管理的第 3 層交叉連接。</span><span class="sxs-lookup"><span data-stu-id="1856d-111">Co-location providers can offer either Layer 2 cross-connections, or managed Layer 3 cross-connections between your infrastructure in the co-location facility and the Microsoft cloud.</span></span>

## <span data-ttu-id="1856d-112"><a name="Ethernet"></a>點對點乙太網路連線</span><span class="sxs-lookup"><span data-stu-id="1856d-112"><a name="Ethernet"></a>Point-to-point Ethernet connections</span></span>
<span data-ttu-id="1856d-113">您可以透過點對點乙太網路連結，將內部部署資料中心/辦公室連接到 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="1856d-113">You can connect your on-premises datacenters/offices to the Microsoft cloud through point-to-point Ethernet links.</span></span> <span data-ttu-id="1856d-114">點對點乙太網路提供者可以在您的網路與 Microsoft 雲端之間，提供第 2 層連線或受管理的第 3 層連線。</span><span class="sxs-lookup"><span data-stu-id="1856d-114">Point-to-point Ethernet providers can offer Layer 2 connections, or managed Layer 3 connections between your site and the Microsoft cloud.</span></span>

## <span data-ttu-id="1856d-115"><a name="IPVPN"></a>任意點對任意點 (IPVPN) 網路</span><span class="sxs-lookup"><span data-stu-id="1856d-115"><a name="IPVPN"></a>Any-to-any (IPVPN) networks</span></span>
<span data-ttu-id="1856d-116">您可以整合 WAN 與 Microsoft 雲端。</span><span class="sxs-lookup"><span data-stu-id="1856d-116">You can integrate your WAN with the Microsoft cloud.</span></span> <span data-ttu-id="1856d-117">IPVPN 提供者 (通常是 MPLS VPN) 在您的分公司與資料中心之間提供任意點對任意點連線。</span><span class="sxs-lookup"><span data-stu-id="1856d-117">IPVPN providers (typically MPLS VPN) offer any-to-any connectivity between your branch offices and datacenters.</span></span> <span data-ttu-id="1856d-118">Microsoft 雲端可以相互連接到您的 WAN，看起來就像任何其他分公司一樣。</span><span class="sxs-lookup"><span data-stu-id="1856d-118">The Microsoft cloud can be interconnected to your WAN to make it look just like any other branch office.</span></span> <span data-ttu-id="1856d-119">WAN 提供者通常會提供受管理的第 3 層連線能力。</span><span class="sxs-lookup"><span data-stu-id="1856d-119">WAN providers typically offer managed Layer 3 connectivity.</span></span> <span data-ttu-id="1856d-120">在上述所有連線模型中，ExpressRoute 功能與特性完全相同。</span><span class="sxs-lookup"><span data-stu-id="1856d-120">ExpressRoute capabilities and features are all identical across all of the above connectivity models.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1856d-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1856d-121">Next steps</span></span>
* <span data-ttu-id="1856d-122">了解 ExpressRoute 連線和路由網域。</span><span class="sxs-lookup"><span data-stu-id="1856d-122">Learn about ExpressRoute connections and routing domains.</span></span> <span data-ttu-id="1856d-123">請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。</span><span class="sxs-lookup"><span data-stu-id="1856d-123">See [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="1856d-124">了解 ExpressRoute 功能。</span><span class="sxs-lookup"><span data-stu-id="1856d-124">Learn about ExpressRoute features.</span></span> <span data-ttu-id="1856d-125">請參閱 [ExpressRoute 技術概觀](expressroute-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1856d-125">See the [ExpressRoute Technical Overview](expressroute-introduction.md)</span></span>
* <span data-ttu-id="1856d-126">尋找服務提供者。</span><span class="sxs-lookup"><span data-stu-id="1856d-126">Find a service provider.</span></span> <span data-ttu-id="1856d-127">請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="1856d-127">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="1856d-128">請確定符合所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="1856d-128">Ensure that all prerequisites are met.</span></span> <span data-ttu-id="1856d-129">請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="1856d-129">See [ExpressRoute prerequisites](expressroute-prerequisites.md).</span></span>
* <span data-ttu-id="1856d-130">請參閱[路由](expressroute-routing.md)、[NAT](expressroute-nat.md) 和 [QoS](expressroute-qos.md) 的需求。</span><span class="sxs-lookup"><span data-stu-id="1856d-130">Refer to the requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="1856d-131">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="1856d-131">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="1856d-132">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="1856d-132">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
  * [<span data-ttu-id="1856d-133">設定路由</span><span class="sxs-lookup"><span data-stu-id="1856d-133">Configure routing</span></span>](expressroute-howto-routing-portal-resource-manager.md)
  * [<span data-ttu-id="1856d-134">將 VNet 連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="1856d-134">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)