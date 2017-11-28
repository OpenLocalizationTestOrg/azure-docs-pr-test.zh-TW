---
title: "aaaQoS expressroute 的需求 |Microsoft 文件"
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
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="e3a3b-103">ExpressRoute QoS 需求</span><span class="sxs-lookup"><span data-stu-id="e3a3b-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="e3a3b-104">商務用 Skype 具有各種工作負載，其所要求的 QoS 處理方式各有差異。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="e3a3b-105">如果您計劃 tooconsume 語音服務透過 ExpressRoute，您應遵守 toohello 底下所述的需求。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="e3a3b-106">Toohello Microsoft 對等互連只套用 QoS 需求。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="e3a3b-107">在 Azure 公用對等互連和 Azure 私人互連接收網路流量的 hello DSCP 值將會重設 too0。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="e3a3b-108">hello 下表提供用於商務用 Skype 的 DSCP 標示的清單。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="e3a3b-109">請參閱太[管理商務用 Skype 的 QoS](https://technet.microsoft.com/library/gg405409.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="e3a3b-110">**傳輸類別**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-110">**Traffic Class**</span></span> | <span data-ttu-id="e3a3b-111">**處理方式 (DSCP 標示)**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="e3a3b-112">**商務用 Skype 的工作負載**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3a3b-113">**語音**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-113">**Voice**</span></span> |<span data-ttu-id="e3a3b-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="e3a3b-114">EF (46)</span></span> |<span data-ttu-id="e3a3b-115">Skype / Lync 語音</span><span class="sxs-lookup"><span data-stu-id="e3a3b-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="e3a3b-116">**互動式**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-116">**Interactive**</span></span> |<span data-ttu-id="e3a3b-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="e3a3b-117">AF41 (34)</span></span> |<span data-ttu-id="e3a3b-118">影片、VBSS</span><span class="sxs-lookup"><span data-stu-id="e3a3b-118">Video, VBSS</span></span> |
| <span data-ttu-id="e3a3b-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="e3a3b-119">AF21 (18)</span></span> |<span data-ttu-id="e3a3b-120">APP 共用</span><span class="sxs-lookup"><span data-stu-id="e3a3b-120">App sharing</span></span> | |
| <span data-ttu-id="e3a3b-121">**預設值**</span><span class="sxs-lookup"><span data-stu-id="e3a3b-121">**Default**</span></span> |<span data-ttu-id="e3a3b-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="e3a3b-122">AF11 (10)</span></span> |<span data-ttu-id="e3a3b-123">檔案傳輸</span><span class="sxs-lookup"><span data-stu-id="e3a3b-123">File transfer</span></span> |
| <span data-ttu-id="e3a3b-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="e3a3b-124">CS0 (0)</span></span> |<span data-ttu-id="e3a3b-125">任何其他項目</span><span class="sxs-lookup"><span data-stu-id="e3a3b-125">Anything else</span></span> | |

* <span data-ttu-id="e3a3b-126">您應該分類 hello 工作負載，並將標示 hello 右 DSCP 值。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="e3a3b-127">請遵循所提供的 hello 指引[這裡](https://technet.microsoft.com/library/gg405409.aspx)如何 tooset DSCP 標示您的網路中。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="e3a3b-128">您應在網路中設定並支援多個 QoS 佇列。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="e3a3b-129">語音必須是獨立類別，且收到 hello RFC 3246 中指定的 EF 處理方式。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="e3a3b-130">您可以決定 hello 佇列機制、 壅塞偵測原則和每個流量類別的頻寬配置。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="e3a3b-131">但是，hello DSCP 標示 skype 以商業工作負載必須保留。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="e3a3b-132">如果您使用 DSCP 標示，以上未列出例如 AF31 (26)，您必須重新撰寫此 DSCP 值 too0 傳送 hello 封包 tooMicrosoft 之前。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="e3a3b-133">Microsoft 只會傳送 hello DSCP 值顯示在資料表上方的 hello 以標記的封包。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3a3b-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3a3b-134">Next steps</span></span>
* <span data-ttu-id="e3a3b-135">請參閱 toohello 需求[路由](expressroute-routing.md)和[NAT](expressroute-nat.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="e3a3b-136">請參閱 hello 下列連結 tooconfigure ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="e3a3b-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="e3a3b-137">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="e3a3b-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="e3a3b-138">設定路由</span><span class="sxs-lookup"><span data-stu-id="e3a3b-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="e3a3b-139">連結的 VNet tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="e3a3b-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

