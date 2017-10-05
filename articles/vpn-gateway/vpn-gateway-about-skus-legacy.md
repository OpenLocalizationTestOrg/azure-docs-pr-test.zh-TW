---
title: "傳統 Azure 虛擬網路閘道 SKU | Microsoft Docs"
description: "舊式虛擬網路閘道 SKU。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="5be9e-103">使用虛擬網路閘道 SKU (舊版 SKU)</span><span class="sxs-lookup"><span data-stu-id="5be9e-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="5be9e-104">此文章包含舊版虛擬網路閘道 SKU 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5be9e-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="5be9e-105">舊版 SKU 仍然可以在針對 VPN 閘道建立的兩個部署模型中運作。</span><span class="sxs-lookup"><span data-stu-id="5be9e-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="5be9e-106">傳統 VPN 閘道仍繼續針對現有閘道以及新閘道使用舊版 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="5be9e-107">在建立新的資源管理員 VPN 閘道時，請使用新的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="5be9e-108">如需最新 SKU 的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="5be9e-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="5be9e-109"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="5be9e-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="5be9e-110"><a name="agg"></a>依 SKU 列出的估計彙總輸送量</span><span class="sxs-lookup"><span data-stu-id="5be9e-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="5be9e-111"><a name="config"></a>依 SKU 和 VPN 類型列出的支援組態</span><span class="sxs-lookup"><span data-stu-id="5be9e-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="5be9e-112"><a name="resize"></a>調整閘道的大小 (變更閘道 SKU)</span><span class="sxs-lookup"><span data-stu-id="5be9e-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="5be9e-113">您可以調整相同 SKU 系列內的閘道 SKU 大小。</span><span class="sxs-lookup"><span data-stu-id="5be9e-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="5be9e-114">例如，如果您有標準 SKU，則可以調整為高效能 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="5be9e-115">您無法調整舊 SKU 與新 SKU 系列之間的 VPN 閘道大小。</span><span class="sxs-lookup"><span data-stu-id="5be9e-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="5be9e-116">例如，您不能從標準 SKU 變成 VpnGw2 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="5be9e-117">若要調整傳統部署模型的閘道 SKU 大小，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5be9e-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="5be9e-118">若要調整資源管理員部署模型的閘道 SKU 大小，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5be9e-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="5be9e-119"><a name="migrate"></a>移轉到新的閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="5be9e-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="5be9e-120">如果您使用的是資源管理員部署模型，則可以移轉到新的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="5be9e-121">如果您使用的是傳統部署模型，則無法移轉到新的 SKU，而必須改為繼續使用舊版 SKU。</span><span class="sxs-lookup"><span data-stu-id="5be9e-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5be9e-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5be9e-122">Next steps</span></span>

<span data-ttu-id="5be9e-123">如需新式閘道 SKU 的相關資訊，請參閱[閘道 SKU](vpn-gateway-about-vpngateways.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="5be9e-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="5be9e-124">如需組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="5be9e-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>