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
# <a name="about-virtual-network-gateways-for-expressroute"></a>關於 ExpressRoute 的虛擬網路閘道
使用虛擬網路閘道 toosend Azure 虛擬網路與內部部署位置之間的網路流量。 當您設定 ExpressRoute 連線時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。

當您建立虛擬網路閘道時，需要指定數個設定。 其中一個所需的 hello 設定指定是否將使用 hello 閘道 ExpressRoute 或站對站 VPN 流量。 在 hello Resource Manager 部署模型，hello 設定是 '-gatewaytype 的授權 '。

當私用連接上傳送網路流量時，您會使用 hello 'ExpressRoute' 的閘道類型。 這也是參考的 tooas ExpressRoute 閘道。 當網路流量會傳送跨加密 hello 公用網際網路，您使用 hello 'Vpn' 的閘道類型。 這是參考的 tooas VPN 閘道。 站對站、點對站和 VNet 對 VNet 連線都使用 VPN 閘道。

對於每種閘道類型，每個虛擬網路只能有一個虛擬網路閘道。 例如，您可以有一個使用 -GatewayType Vpn 的虛擬網路閘道，以及一個使用 -GatewayType ExpressRoute 的虛擬網路閘道。 本文著重在 hello ExpressRoute 的虛擬網路閘道。

## <a name="gwsku"></a>閘道 SKU
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

如果您想 tooupgrade 閘道 tooa 更強大了在大部分情況下，您可以使用的閘道 SKU，hello ' 調整 AzureRmVirtualNetworkGateway' PowerShell cmdlet。 這適用於升級 tooStandard 和高效能的分散式 Sku。 不過，tooupgrade toohello UltraPerformance SKU，您將需要 toorecreate hello 閘道。

### <a name="aggthroughput"></a>依閘道 SKU 列出的估計彙總輸送量
hello 下表顯示 hello 閘道類型和 hello 估計的彙總輸送量。 此表格適用於 tooboth hello 資源管理員和傳統部署模型。

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> 應用程式輸送量取決於多個因素，例如 hello 端對端延遲，和流量 hello 號碼流動 hello 應用程式隨即開啟。 在 hello 資料表代表 hello 上限 hello 應用程式可以 theorectically hello 數字達到理想的環境中。 
> 
>

## <a name="resources"></a>REST API 和 PowerShell Cmdlet
其他技術資源及虛擬網路閘道組態使用 REST Api 和 PowerShell 指令程式時的特定語法需求，請參閱下列頁面的 hello:

| **傳統** | **資源管理員** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [REST API](https://msdn.microsoft.com/library/jj154113.aspx) |[REST API](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>後續步驟
如需有關可用連線組態的詳細資訊，請參閱 [ExpressRoute 概觀](expressroute-introduction.md) 。 

