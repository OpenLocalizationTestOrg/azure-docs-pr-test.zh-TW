---
title: "ExpressRoute 電路的 aaaNAT 需求 |Microsoft 文件"
description: "此頁面提供為 ExpressRoute 線路設定和管理 NAT 的詳細需求。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>ExpressRoute NAT 需求
使用 ExpressRoute tooconnect tooMicrosoft 雲端服務，您將需要 tooset 註冊和管理 Nat。 有些連線提供者會以受管理的服務來支援設定和管理路由。 如果他們提供這類服務，請洽詢您的連線提供者 toosee。 如果沒有，您必須遵守 toohello 底下所述的需求。 

檢閱 hello [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)頁面 tooget 概觀 hello 各種路由網域。 toomeet hello 公用 IP 位址需求的公用 Azure 和 Microsoft 對等互連，我們建議您將 NAT 設定您的網路和 Microsoft 之間。 本節提供您需要 tooset 向上 hello NAT 基礎結構的詳細的描述。

## <a name="nat-requirements-for-azure-public-peering"></a>Azure 公用對等的 NAT 需求
hello Azure 公用互連路徑可讓您 tooconnect tooall 裝載的服務在 Azure 中透過其公用 IP 位址。 其中包括服務列在 hello [ExpessRoute 常見問題集](expressroute-faqs.md)與任何由 Isv Microsoft Azure 上裝載的服務。 

> [!IMPORTANT]
> 服務連線 tooMicrosoft Azure 公用對等互連一律從起始您的網路到 hello Microsoft 網路。 因此，工作階段無法透過 ExpressRoute 起始從 Microsoft Azure 服務 tooyour 網路。 如果嘗試傳送封包 toothese 通告 Ip 將會使用 hello 網際網路，而不是 ExpressRoute。
> 

在公用對等互連流量 tooMicrosoft Azure 必須是公用 IPv4 位址進入 hello Microsoft 網路之前 SNATed toovalid。 hello 圖提供高層級的 hello NAT 如何無法設定上述需求 toomeet hello 圖片。

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>NAT IP 集區和路由通告
您必須確定流量輸入 hello Azure 公用互連路徑具有有效的公用 IPv4 位址。 Microsoft 必須能夠 toovalidate hello 擁有權的 hello 對區域的路由網際網路登錄 (RIR) 或網際網路路由登錄 (IRR) IPv4 NAT 位址集區。 檢查將會執行根據 hello 為號碼正在使用所以而 hello hello NAT 使用的 IP 位址 請參閱 toohello [ExpressRoute 路由需求](expressroute-routing.md)路由所登錄的詳細資訊的頁面。

沒有任何限制 hello 透過此對等互連通告 hello NAT IP 首碼長度。 您必須監視 hello NAT 集區，並確保您不耗盡的 NAT 工作階段。

> [!IMPORTANT]
> hello NAT IP 集區通告 tooMicrosoft 不得公告的 toohello 網際網路。 這會中斷連線 tooother Microsoft 服務。
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Microsoft 對等的 NAT 需求
hello Microsoft 對等互連路徑可讓您透過 hello Azure 公用互連路徑連接 tooMicrosoft 不支援的雲端服務。 服務的 hello 清單包含 Office 365 服務，例如 Exchange Online、 SharePoint Online、 商務和 Dynamics 365 Skype。 Microsoft 會預期在 hello Microsoft 對等互連 toosupport 雙向連線。 流量 tooMicrosoft 雲端服務必須是公用 IPv4 位址進入 hello Microsoft 網路之前 SNATed toovalid。 從 Microsoft 雲端服務的流量 tooyour 網路必須是您的網際網路邊緣 tooprevent SNATed[對稱路由](expressroute-asymmetric-routing.md)。 hello 圖會提供如何 hello NAT 應該是 Microsoft 對等互連的安裝程式的高階圖片。

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>源自於您的網路目的地 tooMicrosoft 流量
* 您必須確定流量輸入 hello Microsoft 對等互連路徑具有有效的公用 IPv4 位址。 Microsoft 必須能夠 toovalidate hello 的擁有者 hello IPv4 NAT 位址集區針對 hello 區域路由網際網路登錄 (RIR) 或網際網路路由登錄 (IRR)。 檢查將會執行根據 hello 為號碼正在使用所以而 hello hello NAT 使用的 IP 位址 請參閱 toohello [ExpressRoute 路由需求](expressroute-routing.md)路由所登錄的詳細資訊的頁面。
* IP 位址用於 hello Azure 公用對等設定，且其他 ExpressRoute 電路必須通告的 tooMicrosoft 透過 hello BGP 工作階段。 沒有任何限制 hello 透過此對等互連通告 hello NAT IP 首碼長度。
  
  > [!IMPORTANT]
  > hello NAT IP 集區通告 tooMicrosoft 不得公告的 toohello 網際網路。 這會中斷連線 tooother Microsoft 服務。
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>來自 Microsoft 預定的 tooyour 網路流量
* 某些情況下需要 Microsoft tooinitiate 連線 tooservice 端點裝載您的網路內。 Hello 案例的典型範例就是從 Office 365 網路中託管的連線能力 tooADFS 伺服器。 在這種情況下，您必須從您的網路遺漏適當的前置詞到 hello Microsoft 對等互連。 
* 您必須在服務端點的網際網路邊緣 hello SNAT Microsoft 流量網路 tooprevent 內[對稱路由](expressroute-asymmetric-routing.md)。 一律會透過 ExpressRoute 傳送具有一個目的地 IP 且符合透過 ExpressRoute 接收之路由的要求**和回覆**。 非對稱的路由存在，如果透過 hello 網際網路以 hello 收到 hello 要求透過 ExpressRoute 傳送的回覆。 SNATing hello 連入 Microsoft 流量在 hello 網際網路邊緣強制回覆流量後 toohello 網際網路邊緣，解決 hello 問題。

![非對稱式路由與 ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>後續步驟
* 請參閱 toohello 需求[路由](expressroute-routing.md)和[QoS](expressroute-qos.md)。
* 如需工作流程資訊，請參閱 [ExpressRoute 線路佈建工作流程和線路狀態](expressroute-workflows.md)。
* 設定 ExpressRoute 連線。
  
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-classic.md)
  * [設定路由](expressroute-howto-routing-classic.md)
  * [連結的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)

