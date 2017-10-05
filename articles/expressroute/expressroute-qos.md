---
title: "適用於 ExpressRoute 的 QoS 需求 |Microsoft Docs"
description: "此頁面提供用來設定和管理適用於 ExpressRoute 循環之 QoS 的詳細需求。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="7c63d-103">ExpressRoute QoS 需求</span><span class="sxs-lookup"><span data-stu-id="7c63d-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="7c63d-104">商務用 Skype 具有各種工作負載，其所要求的 QoS 處理方式各有差異。</span><span class="sxs-lookup"><span data-stu-id="7c63d-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="7c63d-105">如果您打算透過 ExpressRoute 取用語音服務，應遵守以下所述的需求。</span><span class="sxs-lookup"><span data-stu-id="7c63d-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="7c63d-106">QoS 需求僅適用於 Microsoft 對等項目。</span><span class="sxs-lookup"><span data-stu-id="7c63d-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="7c63d-107">在 Azure 公用對等和 Azure 私用對等上收到的網路流量的 DSCP 值將會重設為 0。</span><span class="sxs-lookup"><span data-stu-id="7c63d-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="7c63d-108">下表提供一份商務用 Skype 所使用的 DSCP 標示清單。</span><span class="sxs-lookup"><span data-stu-id="7c63d-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="7c63d-109">如需詳細資訊，請參閱 [管理適用於商務用 Skype 的 QoS](https://technet.microsoft.com/library/gg405409.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="7c63d-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="7c63d-110">**傳輸類別**</span><span class="sxs-lookup"><span data-stu-id="7c63d-110">**Traffic Class**</span></span> | <span data-ttu-id="7c63d-111">**處理方式 (DSCP 標示)**</span><span class="sxs-lookup"><span data-stu-id="7c63d-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="7c63d-112">**商務用 Skype 的工作負載**</span><span class="sxs-lookup"><span data-stu-id="7c63d-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c63d-113">**語音**</span><span class="sxs-lookup"><span data-stu-id="7c63d-113">**Voice**</span></span> |<span data-ttu-id="7c63d-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="7c63d-114">EF (46)</span></span> |<span data-ttu-id="7c63d-115">Skype / Lync 語音</span><span class="sxs-lookup"><span data-stu-id="7c63d-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="7c63d-116">**互動式**</span><span class="sxs-lookup"><span data-stu-id="7c63d-116">**Interactive**</span></span> |<span data-ttu-id="7c63d-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="7c63d-117">AF41 (34)</span></span> |<span data-ttu-id="7c63d-118">影片、VBSS</span><span class="sxs-lookup"><span data-stu-id="7c63d-118">Video, VBSS</span></span> |
| <span data-ttu-id="7c63d-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="7c63d-119">AF21 (18)</span></span> |<span data-ttu-id="7c63d-120">APP 共用</span><span class="sxs-lookup"><span data-stu-id="7c63d-120">App sharing</span></span> | |
| <span data-ttu-id="7c63d-121">**預設值**</span><span class="sxs-lookup"><span data-stu-id="7c63d-121">**Default**</span></span> |<span data-ttu-id="7c63d-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="7c63d-122">AF11 (10)</span></span> |<span data-ttu-id="7c63d-123">檔案傳輸</span><span class="sxs-lookup"><span data-stu-id="7c63d-123">File transfer</span></span> |
| <span data-ttu-id="7c63d-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="7c63d-124">CS0 (0)</span></span> |<span data-ttu-id="7c63d-125">任何其他項目</span><span class="sxs-lookup"><span data-stu-id="7c63d-125">Anything else</span></span> | |

* <span data-ttu-id="7c63d-126">您應將工作負載分類，並標記正確的 DSCP 值。</span><span class="sxs-lookup"><span data-stu-id="7c63d-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="7c63d-127">遵循 [這裡](https://technet.microsoft.com/library/gg405409.aspx) 所提供的指引，以了解如何在您的網路中設定 DSCP 標示。</span><span class="sxs-lookup"><span data-stu-id="7c63d-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="7c63d-128">您應在網路中設定並支援多個 QoS 佇列。</span><span class="sxs-lookup"><span data-stu-id="7c63d-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="7c63d-129">語音必須是獨立的類別，並可接收 RFC 3246 中指定的 EF 處理方式。</span><span class="sxs-lookup"><span data-stu-id="7c63d-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="7c63d-130">您可以決定適用於每個流量類別的佇列機制、壅塞偵測原則和頻寬配置。</span><span class="sxs-lookup"><span data-stu-id="7c63d-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="7c63d-131">但是必須保留適用於商務用 Skype 工作負載的 DSCP 標示。</span><span class="sxs-lookup"><span data-stu-id="7c63d-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="7c63d-132">如果您使用以上未列出的 DSCP 標示 (例如 AF31 (26))，就必須先將此 DSCP 值重寫為 0，才能將封包傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="7c63d-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="7c63d-133">Microsoft 只會傳送使用上表所列之 DSCP 值標記的封包。</span><span class="sxs-lookup"><span data-stu-id="7c63d-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c63d-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c63d-134">Next steps</span></span>
* <span data-ttu-id="7c63d-135">請參閱[路由](expressroute-routing.md)和 [NAT](expressroute-nat.md) 的需求。</span><span class="sxs-lookup"><span data-stu-id="7c63d-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="7c63d-136">請參閱下列連結，以設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="7c63d-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="7c63d-137">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="7c63d-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="7c63d-138">設定路由</span><span class="sxs-lookup"><span data-stu-id="7c63d-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="7c63d-139">將 VNet 連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="7c63d-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

