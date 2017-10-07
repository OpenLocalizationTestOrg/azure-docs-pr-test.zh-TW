---
title: "ExpressRoute 概觀： 透過私人連線擴充您的內部部署網路 tooAzure |Microsoft 文件"
description: "此 ExpressRoute 技術概觀說明 ExpressRoute 連線運作方式 tooextend 您在內部部署網路 tooAzure 透過私人連線。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>ExpressRoute 概欟
Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的私用連接。 透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 Dynamics 365。

從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。 ExpressRoute 連線不會經過 hello 公用網際網路。 這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。 如需詳細資訊 tooconnect 使用 ExpressRoute，您網路 tooMicrosoft 看到[ExpressRoute 的連線模型](expressroute-connectivity-models.md)。

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>主要權益

* 第 3 層連線在內部部署網路之間透過連線服務提供者的 Microsoft 雲端 hello。 從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或透過乙太網路交換經由虛擬交叉連接，都可以進行連線。
* 連線 tooMicrosoft hello 地緣政治區域中的所有區域的雲端服務。
* ExpressRoute 高階的附加元件的所有區域的全域連線 tooMicrosoft 服務。
* 網路與 Microsoft 之間透過業界標準通訊協定 (BGP) 的動態路由。
* 每個對等位置有內建的備援性，可靠性更高。
* 連線執行時間 [SLA](https://azure.microsoft.com/support/legal/sla/)。
* 商務用 Skype 的 QoS 支援。

如需詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。

## <a name="features"></a>特性

### <a name="layer-3-connectivity"></a>第 3 層連線能力
Microsoft 會使用業界標準動態路由通訊協定 (BGP) tooexchange 路由傳送您的內部部署網路，您的執行個體，在 Azure 中，與 Microsoft 之間的公用位址。  我們會針對不同的流量設定檔，與您的網路建立多個 BGP 工作階段。 更多詳細資料位於 hello [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)發行項。

### <a name="redundancy"></a>備援性
每個 ExpressRoute 電路包含兩個連線 tootwo Microsoft 企業邊緣路由器 (MSEEs) 從 hello 連線服務提供者 / 您網路的邊緣。 Microsoft 會要求從 hello 連線服務提供者的雙重 BGP 連線 / 側邊 – 一個 tooeach MSEE。 您可以選擇不 toodeploy 多餘的裝置 / 乙太網路電路您結尾。 不過，連線提供者會使用備援裝置 tooensure 連線交給 tooMicrosoft 備援的方式。 重複第 3 層連線組態是需求我們[SLA](https://azure.microsoft.com/support/legal/sla/) toobe 有效。

### <a name="connectivity-toomicrosoft-cloud-services"></a>連線 tooMicrosoft 雲端服務
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

ExpressRoute 連線可讓存取 toohello 下列服務：

* Microsoft Azure 服務
* Microsoft Office 365 服務
* Microsoft Dynamics 365

您可以瀏覽 hello [ExpressRoute 常見問題集](expressroute-faqs.md)網頁透過 ExpressRoute 支援之服務的詳細清單。

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>連線 tooall 區域地緣政治區域內
您可以連接其中一種 tooMicrosoft 我們[對等互連位置](expressroute-locations.md)和 hello 地緣政治區域內具有存取 tooall 區域。 

例如，如果您透過 ExpressRoute 連接 tooMicrosoft 中阿姆斯特丹，您會有存取 tooall Microsoft 雲端服務裝載於歐洲北部和西歐。 請參閱 hello [ExpressRoute 合作夥伴和互連位置](expressroute-locations.md)hello 地緣政治區域、 相關聯的 Microsoft 的雲端區域，和對應的 ExpressRoute 對等互連位置的發行項的概觀。

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>使用 ExpressRoute Premium 附加元件從全球連線
您可以跨地理政治界限啟用 hello ExpressRoute premium 附加元件功能 tooextend 連線能力。 例如，如果您是連接的 tooMicrosoft 中透過 ExpressRoute 阿姆斯特丹，您必須裝載在所有區域中的 hello 世界各地存取 tooall Microsoft 雲端服務 （國家 （地區） 的雲端會排除）。 您可以存取服務中存取的相同方式北 hello 南美洲或澳洲 hello 和西歐地區部署。

### <a name="rich-connectivity-partner-ecosystem"></a>豐富的連線合作夥伴生態系統
ExpressRoute 的連線提供者和 SI 合作夥伴生態系統持續成長茁壯。 您可以使用參照 toohello [ExpressRoute 提供者和位置](expressroute-locations.md)文件以 hello 最新資訊取得。

### <a name="connectivity-toonational-clouds"></a>連線 toonational 雲端
Microsoft 為特殊的地理政治地區和客戶群提供隔離的雲端環境。 請參閱 toohello [ExpressRoute 提供者和位置](expressroute-locations.md)網頁的國家 （地區） 的雲端和提供者清單。

### <a name="bandwidth-options"></a>頻寬選項
您可以購買各種頻寬的 ExpressRoute 線路。 支援的頻寬如下所列。 為確定 toocheck 與它們所提供的支援頻寬的連線提供者 toodetermine hello 清單。

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>動態調整頻寬
您可以增加 hello ExpressRoute 電路頻寬 （最大速率來執行），而不需要 tootear 向您的連線。 

### <a name="flexible-billing-models"></a>彈性的計費模型
您可以挑選最適合的計費模型。 下面所列的 hello 計費模型之間的選擇。 如需詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。

* **無限制資料**。 根據每月費用，收取 hello ExpressRoute 循環，也包含免費付費的所有傳入和傳出資料傳輸。 
* **已計量資料**。 hello ExpressRoute 循環會負責根據每月費用。 所有輸入資料傳輸都免費。 輸出資料傳輸依每 GB 資料傳輸計費。 資料傳輸費率依區域而不同。
* **ExpressRoute Premium 附加元件**。 hello ExpressRoute premium 位於 hello ExpressRoute 電路的附加元件。 hello ExpressRoute premium add-on 提供下列功能的 hello: 
  * 增加的路由限制用於 Azure 公用和 Azure 私人互連從 4,000 路由 too10，000 路由。
  * 從全球連線到服務。 （不含國家 （地區） 的雲端） 的任何區域中建立 ExpressRoute 電路必須存取 tooresources 整個 hello 世界中的任何其他區域。 例如，透過在美國矽谷佈建的 ExpressRoute 線路，可存取在西歐建立的虛擬網路。
  * 每個從 10 tooa 較大的限制，根據 hello hello 電路頻寬的 ExpressRoute 電路的 VNet 連結的增加的數目。

## <a name="faq"></a>常見問題集

常見問題集疑問 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。

## <a name="next-steps"></a>後續步驟

* 深入了解 [ExpressRoute 連線模型](expressroute-connectivity-models.md)。
* 了解 ExpressRoute 連線和路由網域。 請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。
* 尋找服務提供者。 請參閱 [ExpressRoute 合作夥伴和對等位置](expressroute-locations.md)。
* 請確定符合所有必要條件。 請參閱 [ExpressRoute 必要條件](expressroute-prerequisites.md)。
* 請參閱 toohello 需求[路由](expressroute-routing.md)， [NAT](expressroute-nat.md)，和[QoS](expressroute-qos.md)。
* 設定 ExpressRoute 連線。
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md)
  * [設定 ExpressRoute 線路的對等互連](expressroute-howto-routing-portal-resource-manager.md)
  * [連接虛擬網路 tooan ExpressRoute 電路](expressroute-howto-linkvnet-portal-resource-manager.md)
* 深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。
