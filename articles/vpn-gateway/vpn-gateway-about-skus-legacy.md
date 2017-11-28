---
title: "aaaLegacy Azure 虛擬網路閘道 Sku |Microsoft 文件"
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
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="500ec-103">使用虛擬網路閘道 SKU (舊版 SKU)</span><span class="sxs-lookup"><span data-stu-id="500ec-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="500ec-104">本文章包含 hello 舊版 （舊） 虛擬網路閘道 Sku 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="500ec-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="500ec-105">hello 舊版部署模型已經建立的 VPN 閘道中仍可運作的 Sku。</span><span class="sxs-lookup"><span data-stu-id="500ec-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="500ec-106">傳統 VPN 閘道繼續 toouse hello 舊版 Sku，現有的閘道，以及新的閘道。</span><span class="sxs-lookup"><span data-stu-id="500ec-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="500ec-107">在建立新的資源管理員 VPN 閘道時，使用 hello 新的閘道 Sku。</span><span class="sxs-lookup"><span data-stu-id="500ec-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="500ec-108">如需 hello 新 Sku，請參閱[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="500ec-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="500ec-109"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="500ec-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="500ec-110"><a name="agg"></a>依 SKU 列出的估計彙總輸送量</span><span class="sxs-lookup"><span data-stu-id="500ec-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="500ec-111"><a name="config"></a>依 SKU 和 VPN 類型列出的支援組態</span><span class="sxs-lookup"><span data-stu-id="500ec-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="500ec-112"><a name="resize"></a>調整閘道的大小 (變更閘道 SKU)</span><span class="sxs-lookup"><span data-stu-id="500ec-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="500ec-113">您可以調整大小 hello 內的閘道 SKU 相同 SKU 系列。</span><span class="sxs-lookup"><span data-stu-id="500ec-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="500ec-114">例如，如果您有標準 SKU，您可以調整 tooa HighPerformance SKU。</span><span class="sxs-lookup"><span data-stu-id="500ec-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="500ec-115">您不可以調整您的 VPN 閘道之間 hello 舊的 Sku 和 hello 新 SKU 系列。</span><span class="sxs-lookup"><span data-stu-id="500ec-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="500ec-116">例如，您無法從標準 SKU tooa VpnGw2 SKU 移。</span><span class="sxs-lookup"><span data-stu-id="500ec-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="500ec-117">tooresize hello 傳統部署模型，下列命令使用 hello 閘道 SKU:</span><span class="sxs-lookup"><span data-stu-id="500ec-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="500ec-118">tooresize 閘道 SKU hello Resource Manager 部署模型，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="500ec-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="500ec-119"><a name="migrate"></a>移轉 toohello 新的閘道 Sku</span><span class="sxs-lookup"><span data-stu-id="500ec-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="500ec-120">如果您正在使用 hello Resource Manager 部署模型，您可以移轉 toohello 新的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="500ec-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="500ec-121">如果您正在使用 hello 傳統部署模型，您無法移轉 toohello 新 Sku 和必須改為繼續 toouse hello 舊版 Sku。</span><span class="sxs-lookup"><span data-stu-id="500ec-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="500ec-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="500ec-122">Next steps</span></span>

<span data-ttu-id="500ec-123">如需有關 hello 新的閘道 Sku，請參閱[閘道 Sku](vpn-gateway-about-vpngateways.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="500ec-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="500ec-124">如需組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="500ec-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>