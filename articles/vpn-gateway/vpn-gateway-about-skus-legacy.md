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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>使用虛擬網路閘道 SKU (舊版 SKU)

本文章包含 hello 舊版 （舊） 虛擬網路閘道 Sku 的相關資訊。 hello 舊版部署模型已經建立的 VPN 閘道中仍可運作的 Sku。 傳統 VPN 閘道繼續 toouse hello 舊版 Sku，現有的閘道，以及新的閘道。 在建立新的資源管理員 VPN 閘道時，使用 hello 新的閘道 Sku。 如需 hello 新 Sku，請參閱[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)。

## <a name="gwsku"></a>閘道 SKU

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>依 SKU 列出的估計彙總輸送量

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>依 SKU 和 VPN 類型列出的支援組態

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>調整閘道的大小 (變更閘道 SKU)

您可以調整大小 hello 內的閘道 SKU 相同 SKU 系列。 例如，如果您有標準 SKU，您可以調整 tooa HighPerformance SKU。 您不可以調整您的 VPN 閘道之間 hello 舊的 Sku 和 hello 新 SKU 系列。 例如，您無法從標準 SKU tooa VpnGw2 SKU 移。 

tooresize hello 傳統部署模型，下列命令使用 hello 閘道 SKU:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize 閘道 SKU hello Resource Manager 部署模型，使用下列命令的 hello:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>移轉 toohello 新的閘道 Sku

如果您正在使用 hello Resource Manager 部署模型，您可以移轉 toohello 新的閘道 SKU。 如果您正在使用 hello 傳統部署模型，您無法移轉 toohello 新 Sku 和必須改為繼續 toouse hello 舊版 Sku。

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>後續步驟

如需有關 hello 新的閘道 Sku，請參閱[閘道 Sku](vpn-gateway-about-vpngateways.md#gwsku)。

如需組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。