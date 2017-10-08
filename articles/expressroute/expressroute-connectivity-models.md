---
title: "ExpressRoute 的連線模型： 透過網路服務提供者、 交換，與乙太網路提供者連線 tooMicrosoft Azure |Microsoft 文件"
description: "本文說明 hello 不同的 hello 客戶網路和 Microsoft Azure、 Office 365 和 Dynamics 365 服務之間的連接模式。 客戶可以使用 MPLS 提供者、雲端 Exchange 和乙太網路提供者。"
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
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>ExpressRoute 連線模型
您可以建立您的內部部署網路與 hello Microsoft 雲端之間的連線以三個不同的方式， [CloudExchange 共](#CloudExchange)，[點對點乙太網路連線](#Ethernet)，和[Any-any (IPVPN) 連線](#IPVPN)。 連線提供者可以提供一或多個連線模型。 您可以使用最適合您連接提供者 toopick hello 模型。
<br><br>

![ExpressRoute 連線模型圖表](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>共置於雲端 Exchange
如果您同時位於雲端交換設備，您可以排序虛擬交叉連線 toohello 透過 hello 代管提供者的乙太網路交換的 Microsoft 雲端。 代管提供者可以提供第 2 層交叉連線或受管理第 3 層交叉連線 hello Microsoft 雲端基礎結構在 hello 共置設備之間。

## <a name="Ethernet"></a>點對點乙太網路連線
您可以透過點對點乙太網路連結連接您在內部部署資料中心/辦公室 toohello Microsoft 雲端。 點對點乙太網路提供者可以提供第 2 層連線，或管理您的站台與 hello Microsoft 雲端之間的第 3 層連線。

## <a name="IPVPN"></a>任意點對任意點 (IPVPN) 網路
您可以整合您的 WAN 與 hello Microsoft 雲端。 IPVPN 提供者 (通常是 MPLS VPN) 在您的分公司與資料中心之間提供任意點對任意點連線。 hello Microsoft 雲端可以互連的 tooyour WAN toomake 它看起來就像任何其他分公司。 WAN 提供者通常會提供受管理的第 3 層連線能力。 ExpressRoute 功能和功能是 hello 的所有相同的所有連接模型上方。 

## <a name="next-steps"></a>後續步驟
* 了解 ExpressRoute 連線和路由網域。 請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。
* 了解 ExpressRoute 功能。 請參閱 hello [ExpressRoute 技術概觀](expressroute-introduction.md)
* 尋找服務提供者。 請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。
* 請確定符合所有必要條件。 請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。
* 請參閱 toohello 需求[路由](expressroute-routing.md)， [NAT](expressroute-nat.md)，和[QoS](expressroute-qos.md)。
* 設定 ExpressRoute 連線。
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md)
  * [設定路由](expressroute-howto-routing-portal-resource-manager.md)
  * [連結的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-portal-resource-manager.md)
