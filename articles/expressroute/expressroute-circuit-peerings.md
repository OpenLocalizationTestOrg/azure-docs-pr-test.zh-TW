---
title: "aaaAzure ExpressRoute 線路和路由網域 |Microsoft 文件"
description: "此頁面會提供 ExpressRoute 線路和 hello 路由網域的概觀。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>ExpressRoute 線路和路由網域
 您必須訂購*ExpressRoute 電路*tooconnect 您在內部部署基礎結構 tooMicrosoft，透過連線服務提供者。 hello 圖提供您的 WAN 與 Microsoft 之間連線的邏輯表示法。

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>ExpressRoute 線路
*ExpressRoute 線路* 代表內部部署基礎結構與 Microsoft 雲端服務之間透過連線提供者的邏輯連線。 您可以訂購多條 ExpressRoute 線路。 每個 expressroute 電路可以在 hello 相同或不同區域，而且可以透過不同的連接提供者的連接的 tooyour 內部部署。 

ExpressRoute 電路並對應 tooany 實際的實體。 線路由一個稱為服務金鑰 (s 金鑰) 的標準 GUID 唯一識別。 hello 服務金鑰是唯一 Microsoft、 hello 連線服務提供者與您之間交換資訊 hello。 hello s 鍵不是基於安全的密碼。 沒有 1:1 之間的對應的 ExpressRoute 電路並 hello s 鍵。

ExpressRoute 電路可以有向上 toothree 獨立的對等互連： Azure 的公用、 Azure 私人和 Microsoft。 每個對等為一組獨立的 BGP 工作階段，每個都重複設定，以確保較高的可用性。 ExpressRoute 線路與路由網域之間存在 1:N (1 <= N <= 3) 對應。 每個 ExpressRoute 電路可以啟用任何一個、兩個或全部三個對等。

每個 expressroute 電路具有固定的頻寬 （50 Mbps、 100 Mbps、 200 Mbps、 500 Mbps、 1 Gbps、 10 Gbps），而且是對應的 tooa 連線服務提供者和對等互連位置。 您選取的 hello 頻寬會共用所有的 hello 對等互連 hello 循環之間。 

### <a name="quotas-limits-and-limitations"></a>配額和限制
每個 ExpressRoute 線路會套用預設的配額和限制。 請參閱 toohello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)頁面以取得最新配額的資訊。

## <a name="expressroute-routing-domains"></a>ExpressRoute 路由網域
ExpressRoute 線路有多個相關聯的路由網域：Azure 公用、Azure 私用和 Microsoft。 每一個 hello 路由網域都設定相同的路由器對上 (主動 / 主動或載入共用組態) 的高可用性。 Azure 服務都會分類成*Azure 公用*和*Azure 私用*toorepresent hello IP 定址配置。

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>私人對等互連
Azure 計算服務，也就是虛擬機器 (IaaS) 和虛擬網路內部署的雲端服務 (PaaS)，可以透過 hello 私用對等網域連接。 hello 私用對等網域被視為 toobe 核心網路的受信任的擴充至 Microsoft Azure。 您可以在核心網路與 Azure 虛擬網路 (VNet) 之間設定雙向連線。 此對等互連，可讓您連接 toovirtual 機器和雲端服務，直接在其私人 IP 位址。  

您可以連接多個虛擬網路 toohello 私用對等網域。 檢閱 hello[常見問題集頁面](expressroute-faqs.md)有關限制和限制的資訊。 您可以瀏覽 hello [Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)頁面以取得有關限制的最新狀態資訊。  請參閱 toohello[路由](expressroute-routing.md)路由組態的詳細資訊的頁面。

### <a name="public-peering"></a>公用對等互連
公用 IP 位址上提供如 Azure 儲存體、SQL Database 和網站等服務。 您可以私下連接 tooservices 裝載於公用 IP 位址，包括您的雲端服務，透過 hello 公用對等互連路由網域的 Vip。 您可以連接 hello 公用對等網域 tooyour 周邊網路，並連接 tooall Azure 服務，您不需要 tooconnect 透過 WAN 從其公用 IP 位址上的 hello 網際網路。 

連線一律會從您的 WAN tooMicrosoft Azure 起始服務。 Microsoft Azure 服務不會無法 tooinitiate 您透過此路由網域的網路連線。 啟用公用對等互連時，才能夠 tooconnect tooall Azure 服務。 我們不允許您 tooselectively 挑選服務，我們會通告的路由。 您可以檢閱我們通告 tooyou 透過 hello 此對等的前置詞的 hello 清單[Microsoft Azure Datacenter IP 範圍](http://www.microsoft.com/download/details.aspx?id=41653)頁面。 hello 頁面會每週更新。

您可以定義自訂的路由篩選您的網路 tooconsume 只有 hello 路由您需要內。 請參閱 toohello[路由](expressroute-routing.md)路由組態的詳細資訊的頁面。 

請參閱 hello[常見問題集頁面](expressroute-faqs.md)如需有關支援透過 hello 公用對等互連路由網域的服務。 

### <a name="microsoft-peering"></a>Microsoft 對等互連
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

連線 tooall 其他 Microsoft online services （例如 Office 365 服務） 會透過 hello Microsoft 對等互連。 我們啟用您 WAN 和 Microsoft 雲端服務之間透過 hello Microsoft 對等互連的路由網域的雙向連線。 您必須連接 tooMicrosoft 雲端服務僅透過由您或您連線服務提供者所擁有的公用 IP 位址，您必須遵守 tooall hello 定義規則。 請參閱 hello [ExpressRoute 必要條件](expressroute-prerequisites.md)頁面以取得詳細的資訊。

請參閱 hello[常見問題集頁面](expressroute-faqs.md)的更多有關支援的服務、 成本與組態詳細資料。 請參閱 hello [ExpressRoute 位置](expressroute-locations.md)hello 清單上的 Microsoft 對等互連支援供應項目連線提供者的資訊的頁面。

## <a name="routing-domain-comparison"></a>路由網域的比較
hello 表比較 hello 三個路由網域。

|  | **私人對等互連** | **公用對等互連** | **Microsoft 對等互連** |
| --- | --- | --- | --- |
| **每個對等支援的前置詞數目最大值** |預設為 4000，ExpressRoute Premium 中為 10000 |200 |200 |
| **支援的 IP 位址範圍** |您的 WAN 內任何有效的 IPv4 位址。 |您或您的連線提供者所擁有的公用 IPv4 位址。 |您或您的連線提供者所擁有的公用 IPv4 位址。 |
| **AS 編號需求** |私密和公用 AS 編號。 您必須擁有 hello 公用如果您選擇其中一個 toouse 的數字。 |私密和公用 AS 編號。 不過，您必須證明公用 IP 位址的擁有權。 |私密和公用 AS 編號。 不過，您必須證明公用 IP 位址的擁有權。 |
| **路由介面 IP 位址** |RFC1918 和公用 IP 位址 |公用 IP 位址已註冊的 tooyou 路由登錄中。 |公用 IP 位址已註冊的 tooyou 路由登錄中。 |
| **MD5 雜湊支援** |是 |是 |是 |

您可以選擇一或多個路由網域的 hello tooenable ExpressRoute 電路的一部分。 您可以選擇 toohave 所有 hello 路由網域打 hello 相同的 VPN，如果您想 toocombine 為單一路由網域。 您也可以將它們放在不同的路由網域，類似 toohello 圖表上。 hello 建議設定是該私人互連已連接直接 toohello 核心網路，而且 hello 公用及 Microsoft 對等互連連結是連接的 tooyour 周邊網路。

如果您選擇 toohave 所有三個對等互連工作階段，您必須有三組 BGP 工作階段 （每個對等互連類型的一組）。 hello BGP 工作階段組可提供高度可用的連結。 如果您透過第 2 層連線提供者來連線，則要負責設定和管理路由。 您可以進一步檢閱 hello[工作流程](expressroute-workflows.md)設定 ExpressRoute。

## <a name="next-steps"></a>後續步驟
* 尋找服務提供者。 請參閱 [ExpressRoute 服務提供者和位置](expressroute-locations.md)。
* 請確定符合所有必要條件。 請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。
* 設定 ExpressRoute 連線。
  * [建立和管理 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md)
  * [設定 ExpressRoute 線路的路由 (對等戶連)](expressroute-howto-routing-portal-resource-manager.md)

