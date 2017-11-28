---
title: "aaaAbout ExpressRoute 的虛擬網路閘道 |Microsoft 文件"
description: "了解 ExpressRoute 的虛擬網路閘道。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="9bcef-103">關於 ExpressRoute 的虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="9bcef-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="9bcef-104">使用虛擬網路閘道 toosend Azure 虛擬網路與內部部署位置之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="9bcef-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="9bcef-105">當您設定 ExpressRoute 連線時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。</span><span class="sxs-lookup"><span data-stu-id="9bcef-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="9bcef-106">當您建立虛擬網路閘道時，需要指定數個設定。</span><span class="sxs-lookup"><span data-stu-id="9bcef-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="9bcef-107">其中一個所需的 hello 設定指定是否將使用 hello 閘道 ExpressRoute 或站對站 VPN 流量。</span><span class="sxs-lookup"><span data-stu-id="9bcef-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="9bcef-108">在 hello Resource Manager 部署模型，hello 設定是 '-gatewaytype 的授權 '。</span><span class="sxs-lookup"><span data-stu-id="9bcef-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="9bcef-109">當私用連接上傳送網路流量時，您會使用 hello 'ExpressRoute' 的閘道類型。</span><span class="sxs-lookup"><span data-stu-id="9bcef-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="9bcef-110">這也是參考的 tooas ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="9bcef-111">當網路流量會傳送跨加密 hello 公用網際網路，您使用 hello 'Vpn' 的閘道類型。</span><span class="sxs-lookup"><span data-stu-id="9bcef-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="9bcef-112">這是參考的 tooas VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="9bcef-113">站對站、點對站和 VNet 對 VNet 連線都使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="9bcef-114">對於每種閘道類型，每個虛擬網路只能有一個虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="9bcef-115">例如，您可以有一個使用 -GatewayType Vpn 的虛擬網路閘道，以及一個使用 -GatewayType ExpressRoute 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="9bcef-116">本文著重在 hello ExpressRoute 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="9bcef-117"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="9bcef-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="9bcef-118">如果您想 tooupgrade 閘道 tooa 更強大了在大部分情況下，您可以使用的閘道 SKU，hello ' 調整 AzureRmVirtualNetworkGateway' PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9bcef-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="9bcef-119">這適用於升級 tooStandard 和高效能的分散式 Sku。</span><span class="sxs-lookup"><span data-stu-id="9bcef-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="9bcef-120">不過，tooupgrade toohello UltraPerformance SKU，您將需要 toorecreate hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="9bcef-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="9bcef-121"><a name="aggthroughput"></a>依閘道 SKU 列出的估計彙總輸送量</span><span class="sxs-lookup"><span data-stu-id="9bcef-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="9bcef-122">hello 下表顯示 hello 閘道類型和 hello 估計的彙總輸送量。</span><span class="sxs-lookup"><span data-stu-id="9bcef-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="9bcef-123">此表格適用於 tooboth hello 資源管理員和傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="9bcef-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="9bcef-124">應用程式輸送量取決於多個因素，例如 hello 端對端延遲，和流量 hello 號碼流動 hello 應用程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="9bcef-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="9bcef-125">在 hello 資料表代表 hello 上限 hello 應用程式可以 theorectically hello 數字達到理想的環境中。</span><span class="sxs-lookup"><span data-stu-id="9bcef-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="9bcef-126"><a name="resources"></a>REST API 和 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9bcef-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="9bcef-127">其他技術資源及虛擬網路閘道組態使用 REST Api 和 PowerShell 指令程式時的特定語法需求，請參閱下列頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bcef-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="9bcef-128">**傳統**</span><span class="sxs-lookup"><span data-stu-id="9bcef-128">**Classic**</span></span> | <span data-ttu-id="9bcef-129">**資源管理員**</span><span class="sxs-lookup"><span data-stu-id="9bcef-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="9bcef-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bcef-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="9bcef-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bcef-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="9bcef-132">REST API</span><span class="sxs-lookup"><span data-stu-id="9bcef-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="9bcef-133">REST API</span><span class="sxs-lookup"><span data-stu-id="9bcef-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="9bcef-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bcef-134">Next steps</span></span>
<span data-ttu-id="9bcef-135">如需有關可用連線組態的詳細資訊，請參閱 [ExpressRoute 概觀](expressroute-introduction.md) 。</span><span class="sxs-lookup"><span data-stu-id="9bcef-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

