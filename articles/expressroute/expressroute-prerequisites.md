---
title: "採用 Azure ExpressRoute 的必要條件 | Microsoft Docs"
description: "本頁面提供在您可以訂購 Azure ExpressRoute 電路之前必須符合的需求清單。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 8629235511e0dda149ceef6a9c834c3042f64f90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-prerequisites--checklist"></a><span data-ttu-id="93a84-103">ExpressRoute 必要條件和檢查清單</span><span class="sxs-lookup"><span data-stu-id="93a84-103">ExpressRoute prerequisites & checklist</span></span>
<span data-ttu-id="93a84-104">若要使用 ExpressRoute 連線到 Microsoft 雲端服務，您必須確認是否符合以下各節中所列的下列需求。</span><span class="sxs-lookup"><span data-stu-id="93a84-104">To connect to Microsoft cloud services using ExpressRoute, you need to verify that the following requirements listed in the following sections have been met.</span></span>

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a><span data-ttu-id="93a84-105">Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="93a84-105">Azure account</span></span>
* <span data-ttu-id="93a84-106">使用中的有效 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a84-106">A valid and active Microsoft Azure account.</span></span> <span data-ttu-id="93a84-107">需要有此帳戶才能設定 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="93a84-107">This account is required to set up the ExpressRoute circuit.</span></span> <span data-ttu-id="93a84-108">ExpressRoute 循環是 Azure 訂用帳戶內的資源。</span><span class="sxs-lookup"><span data-stu-id="93a84-108">ExpressRoute circuits are resources within Azure subscriptions.</span></span> <span data-ttu-id="93a84-109">即使連線只限於非 Azure Microsoft 雲端服務 (例如 Office 365 服務和 Dynamics 365)，Azure 訂用帳戶還是一項需求。</span><span class="sxs-lookup"><span data-stu-id="93a84-109">An Azure subscription is a requirement even if connectivity is limited to non-Azure Microsoft cloud services, such as Office 365 services and Dynamics 365.</span></span>
* <span data-ttu-id="93a84-110">使用中的 Office 365 訂用帳戶 (如果使用的是 Office 365 服務)。</span><span class="sxs-lookup"><span data-stu-id="93a84-110">An active Office 365 subscription (if using Office 365 services).</span></span> <span data-ttu-id="93a84-111">如需詳細資訊，請參閱本文的 [Office 365 特定需求](#office-365-specific-requirements)一節。</span><span class="sxs-lookup"><span data-stu-id="93a84-111">For more information, see the [Office 365 specific requirements](#office-365-specific-requirements) section of this article.</span></span>

## <a name="connectivity-provider"></a><span data-ttu-id="93a84-112">連線提供者</span><span class="sxs-lookup"><span data-stu-id="93a84-112">Connectivity provider</span></span>

* <span data-ttu-id="93a84-113">您可以與 [ExpressRoute 連線合作夥伴](expressroute-locations.md#partners) 合作來連線到 Microsoft Cloud。</span><span class="sxs-lookup"><span data-stu-id="93a84-113">You can work with an [ExpressRoute connectivity partner](expressroute-locations.md#partners) to connect to the Microsoft cloud.</span></span> <span data-ttu-id="93a84-114">您可以透過 [三種方法](expressroute-introduction.md)在內部部署網路與 Microsoft 之間設定連線。</span><span class="sxs-lookup"><span data-stu-id="93a84-114">You can set up a connection between your on-premises network and Microsoft in [three ways](expressroute-introduction.md).</span></span>
* <span data-ttu-id="93a84-115">如果您的提供者不是 ExpressRoute 連線合作夥伴，您仍可透過 [雲端交換服務提供者](expressroute-locations.md#connectivity-through-exchange-providers)連線到 Microsoft Cloud。</span><span class="sxs-lookup"><span data-stu-id="93a84-115">If your provider is not an ExpressRoute connectivity partner, you can still connect to the Microsoft cloud through a [cloud exchange provider](expressroute-locations.md#connectivity-through-exchange-providers).</span></span>

## <a name="network-requirements"></a><span data-ttu-id="93a84-116">網路需求</span><span class="sxs-lookup"><span data-stu-id="93a84-116">Network requirements</span></span>
* <span data-ttu-id="93a84-117">**備援連線**︰您和您的提供者之間不需要實體連線備援。</span><span class="sxs-lookup"><span data-stu-id="93a84-117">**Redundant connectivity**: there is no redundancy requirement on physical connectivity between you and your provider.</span></span> <span data-ttu-id="93a84-118">Microsoft 不要求您在 Microsoft 路由器和對等路由器之間設定備援 BGP 工作階段，即使您只有 [一個與雲端交換服務的實體連線](expressroute-faqs.md#onep2plink)也是如此。</span><span class="sxs-lookup"><span data-stu-id="93a84-118">Microsoft does require redundant BGP sessions to be set up between Microsoft’s routers and the peering routers, even when you have just [one physical connection to a cloud exchange](expressroute-faqs.md#onep2plink).</span></span>
* <span data-ttu-id="93a84-119">**路由**︰根據您連線到 Microsoft Cloud 的方式，您或您的提供者需要設定及管理用於 [路由網域](expressroute-circuit-peerings.md)的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="93a84-119">**Routing**: depending on how you connect to the Microsoft Cloud, you or your provider need to set up and manage the BGP sessions for [routing domains](expressroute-circuit-peerings.md).</span></span> <span data-ttu-id="93a84-120">某些乙太網路連線服務提供者或雲端交換服務提供者可能會提供 BGP 管理功能做為附加價值服務。</span><span class="sxs-lookup"><span data-stu-id="93a84-120">Some Ethernet connectivity provider or cloud exchange provider may offer BGP management as a value-add service.</span></span>
* <span data-ttu-id="93a84-121">**NAT**：Microsoft 只接受透過 Microsoft 對等互連的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a84-121">**NAT**: Microsoft only accepts public IP addresses through Microsoft peering.</span></span> <span data-ttu-id="93a84-122">如果您在內部部署網路中使用私人 IP 位址，您或您的提供者必須 [使用 NAT](expressroute-nat.md)將私人 IP 位址轉譯成公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a84-122">If you are using private IP addresses in your on-premises network, you or your provider need to translate the private IP addresses to the public IP addresses [using the NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="93a84-123">**QoS**：商務用 Skype 具有各種服務 (例如語音、視訊、文字)，其所要求的 QoS 處理方式各有差異。</span><span class="sxs-lookup"><span data-stu-id="93a84-123">**QoS**: Skype for Business has various services (for example; voice, video, text) that require differentiated QoS treatment.</span></span> <span data-ttu-id="93a84-124">您和您的提供者應該遵循 [QoS 需求](expressroute-qos.md)。</span><span class="sxs-lookup"><span data-stu-id="93a84-124">You and your provider should follow the [QoS requirements](expressroute-qos.md).</span></span>
* <span data-ttu-id="93a84-125">**網路安全性**︰透過 ExpressRoute 連線到 Microsoft Cloud 時，請考慮[網路安全性](../best-practices-network-security.md)。</span><span class="sxs-lookup"><span data-stu-id="93a84-125">**Network Security**: consider [network security](../best-practices-network-security.md) when connecting to the Microsoft Cloud via ExpressRoute.</span></span>

## <a name="office-365"></a><span data-ttu-id="93a84-126">Office 365</span><span class="sxs-lookup"><span data-stu-id="93a84-126">Office 365</span></span>
<span data-ttu-id="93a84-127">如果您打算在 ExpressRoute 上啟用 Office 365，請檢閱下列文件以取得 Office 365 需求的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="93a84-127">If you plan to enable Office 365 on ExpressRoute, review the following documents for more information about Office 365 requirements.</span></span>

* [<span data-ttu-id="93a84-128">ExpressRoute for Office 365 概觀</span><span class="sxs-lookup"><span data-stu-id="93a84-128">Overview of ExpressRoute for Office 365</span></span>](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [<span data-ttu-id="93a84-129">使用 ExpressRoute for Office 365 進行路由</span><span class="sxs-lookup"><span data-stu-id="93a84-129">Routing with ExpressRoute for Office 365</span></span>](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [<span data-ttu-id="93a84-130">Office 365 URL 與 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="93a84-130">Office 365 URLs and IP address ranges</span></span>](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [<span data-ttu-id="93a84-131">Office 365 的網路規劃與效能調整</span><span class="sxs-lookup"><span data-stu-id="93a84-131">Network planning and performance tuning for Office 365</span></span>](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [<span data-ttu-id="93a84-132">網路頻寬計算機和工具</span><span class="sxs-lookup"><span data-stu-id="93a84-132">Network bandwidth calculators and tools</span></span>](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [<span data-ttu-id="93a84-133">整合 Office 365 與內部部署環境</span><span class="sxs-lookup"><span data-stu-id="93a84-133">Office 365 integration with on-premises environments</span></span>](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [<span data-ttu-id="93a84-134">Office 365 上的 ExpressRoute 進階訓練影片</span><span class="sxs-lookup"><span data-stu-id="93a84-134">ExpressRoute on Office 365 advanced training videos</span></span>](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a><span data-ttu-id="93a84-135">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="93a84-135">Dynamics 365</span></span>
<span data-ttu-id="93a84-136">如果您打算在 ExpressRoute 上啟用 Dynamics 365，請檢閱下列文件以取得 Dynamics 365 的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="93a84-136">If you plan to enable Dynamics 365 on ExpressRoute, review the following documents for more information about Dynamics 365</span></span>

* [<span data-ttu-id="93a84-137">Dynamics 365 和 ExpressRoute 白皮書</span><span class="sxs-lookup"><span data-stu-id="93a84-137">Dynamics 365 and ExpressRoute whitepaper</span></span>](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* <span data-ttu-id="93a84-138">[Dynamics 365 URL](https://support.microsoft.com/kb/2655102) 和 [IP 位址範圍](https://support.microsoft.com/kb/2728473)</span><span class="sxs-lookup"><span data-stu-id="93a84-138">[Dynamics 365 URLs](https://support.microsoft.com/kb/2655102) and [IP address ranges](https://support.microsoft.com/kb/2728473)</span></span>

## <a name="next-steps"></a><span data-ttu-id="93a84-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93a84-139">Next steps</span></span>
* <span data-ttu-id="93a84-140">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="93a84-140">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
* <span data-ttu-id="93a84-141">尋找 ExpressRoute 連線提供者。</span><span class="sxs-lookup"><span data-stu-id="93a84-141">Find an ExpressRoute connectivity provider.</span></span> <span data-ttu-id="93a84-142">請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="93a84-142">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="93a84-143">請參閱[路由](expressroute-routing.md)、[NAT](expressroute-nat.md) 和 [QoS](expressroute-qos.md) 的需求。</span><span class="sxs-lookup"><span data-stu-id="93a84-143">Refer to requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="93a84-144">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="93a84-144">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="93a84-145">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="93a84-145">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="93a84-146">設定路由</span><span class="sxs-lookup"><span data-stu-id="93a84-146">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="93a84-147">將 VNet 連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="93a84-147">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)
