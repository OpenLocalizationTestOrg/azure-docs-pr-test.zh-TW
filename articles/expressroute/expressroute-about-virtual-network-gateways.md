---
title: "關於 ExpressRoute 虛擬網路閘道 | Microsoft Docs"
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
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="e7c08-103">關於 ExpressRoute 的虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="e7c08-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="e7c08-104">虛擬網路閘道可用來傳送 Azure 虛擬網路和內部部署位置之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="e7c08-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="e7c08-105">當您設定 ExpressRoute 連線時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。</span><span class="sxs-lookup"><span data-stu-id="e7c08-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="e7c08-106">當您建立虛擬網路閘道時，需要指定數個設定。</span><span class="sxs-lookup"><span data-stu-id="e7c08-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="e7c08-107">其中一個必要設定會指定是否要對 ExpressRoute 或站對站 VPN 閘道流量使用閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="e7c08-108">在 Resource Manager 部署模型中，此設定是「-GatewayType」。</span><span class="sxs-lookup"><span data-stu-id="e7c08-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="e7c08-109">如果網路流量是在私人連線上傳送，則使用的閘道類型為「ExpressRoute」。</span><span class="sxs-lookup"><span data-stu-id="e7c08-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="e7c08-110">也稱為 ExpressRoute 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="e7c08-111">如果網路流量是透過公用網際網路加密傳送，則使用的閘道類型為「Vpn」。</span><span class="sxs-lookup"><span data-stu-id="e7c08-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="e7c08-112">稱之為 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="e7c08-113">站對站、點對站和 VNet 對 VNet 連線都使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="e7c08-114">對於每種閘道類型，每個虛擬網路只能有一個虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="e7c08-115">例如，您可以有一個使用 -GatewayType Vpn 的虛擬網路閘道，以及一個使用 -GatewayType ExpressRoute 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="e7c08-116">本文著重於 ExpressRoute 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="e7c08-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="e7c08-117"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="e7c08-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="e7c08-118">如果您想要將閘道器升級至更強大的閘道 SKU，在大部分情況下，您可以使用 'Resize-AzureRmVirtualNetworkGateway' PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7c08-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="e7c08-119">這適用於升級至 Standard 和 HighPerformance SKU。</span><span class="sxs-lookup"><span data-stu-id="e7c08-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="e7c08-120">不過，若要升級至 UltraPerformance SKU，您必須重新建立閘道器。</span><span class="sxs-lookup"><span data-stu-id="e7c08-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="e7c08-121"><a name="aggthroughput"></a>依閘道 SKU 列出的估計彙總輸送量</span><span class="sxs-lookup"><span data-stu-id="e7c08-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="e7c08-122">下表顯示閘道類型和預估的彙總輸送量。</span><span class="sxs-lookup"><span data-stu-id="e7c08-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="e7c08-123">此資料表適用於資源管理員與傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="e7c08-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="e7c08-124">應用程式輸送量取決於多項因素，例如端對端延遲以及應用程式開啟之流量的數目。</span><span class="sxs-lookup"><span data-stu-id="e7c08-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="e7c08-125">表格中的數字代表應用程式在理想的環境中，理論上可以達成的最高上限。</span><span class="sxs-lookup"><span data-stu-id="e7c08-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="e7c08-126"><a name="resources"></a>REST API 和 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e7c08-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="e7c08-127">如需將 REST API 和 PowerShell Cmdlet 使用於虛擬網路閘道組態時的其他技術資源和特定語法需求，請參閱下列頁面︰</span><span class="sxs-lookup"><span data-stu-id="e7c08-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="e7c08-128">**傳統**</span><span class="sxs-lookup"><span data-stu-id="e7c08-128">**Classic**</span></span> | <span data-ttu-id="e7c08-129">**資源管理員**</span><span class="sxs-lookup"><span data-stu-id="e7c08-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="e7c08-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7c08-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="e7c08-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7c08-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="e7c08-132">REST API</span><span class="sxs-lookup"><span data-stu-id="e7c08-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="e7c08-133">REST API</span><span class="sxs-lookup"><span data-stu-id="e7c08-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="e7c08-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7c08-134">Next steps</span></span>
<span data-ttu-id="e7c08-135">如需有關可用連線組態的詳細資訊，請參閱 [ExpressRoute 概觀](expressroute-introduction.md) 。</span><span class="sxs-lookup"><span data-stu-id="e7c08-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

