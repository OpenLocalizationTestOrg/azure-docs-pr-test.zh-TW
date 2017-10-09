---
title: "最佳化 ExpressRoute 路由：Azure | Microsoft Docs"
description: "此頁面提供有關如何 toooptimize 路由，當您有多個 ExpressRoute 電路的連接 Microsoft 和您的公司網路。"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>最佳化 ExpressRoute 路由
當您有多個 ExpressRoute 電路時，您會有一個以上的路徑 tooconnect tooMicrosoft。 如此一來，次佳的路由可能會發生-也就是您的流量可能需要較長的路徑 tooreach Microsoft 和 Microsoft tooyour 網路。 hello 長 hello 網路路徑，hello 較高的 hello 延遲。 延遲對於應用程式效能和使用者體驗有直接的影響。 這篇文章會說明這個問題，並說明如何使用路由 toooptimize hello 標準路由技術。

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>次佳的客戶 tooMicrosoft 從路由
讓我們仔細查看 hello 路由問題所範例。 假設您有兩個 hello 美國，一部位於洛杉磯，另一個在紐約辦公室。 您的辦公室是在廣域網路 (WAN) 上連線，該網路可以是您自己的骨幹網路或服務提供者的 IP VPN。 您有兩個 ExpressRoute 電路，分別位於美國西部和美國東部 hello WAN 上也連接。 很明顯地，您有兩個路徑 tooconnect toohello Microsoft 網路。 現在假設您在美國西部和美國東部均有 Azure 部署 (例如 Azure App Service)。 您的意圖是 tooconnect Los Angeles tooAzure 美國西部使用者和使用者在紐約 tooAzure 美國東部中的因為您的服務系統管理員會通告每個 office access 中 hello 附近的最佳體驗的 Azure 服務。 不幸的是，hello 計劃適用於用於 hello 東部 coast 使用者，但不適用於 hello 西岸使用者。 hello hello 問題原因是下列 hello。 在每個 ExpressRoute 電路，我們會通告 tooyou Azure 美國東部 (23.100.0.0/16) 中的 hello 前置詞和 Azure 美國西部 (13.100.0.0/16) 中的 hello 前置詞都。 如果您不知道的前置詞是從哪一個區域，您不能 tootreat 它以不同的方式。 您的 WAN 網路可能會認為這兩個 hello 前置詞是美國西部比接近 tooUS 東部而且因此美國東部路由這兩種 office 使用者 toohello ExpressRoute 電路。 Hello 結束時，您必須在 hello 洛杉磯分公司中的許多不滿意使用者。

![ExpressRoute 案例 1 問題-次佳的客戶 tooMicrosoft 從路由](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>解決方法︰使用 BGP 社群
toooptimize 路由傳送給這兩個辦公室的使用者，您需要的前置詞會從 Azure 美國西部和取自 Azure 美國東部 tooknow。 我們使用 [BGP 社群值](expressroute-routing.md)來編碼這項資訊。 我們已指派唯一的 BGP 社群值 tooeach Azure 地區，例如："12076:51004" 適用於美國東部，"12076:51006" 適用於美國西部。 您現在知道哪個前置詞來自哪個 Azure 區域，即可設定應優先使用哪個 ExpressRoute 線路。 因為我們使用 hello BGP tooexchange 路由資訊時，您可以使用 BGP 的本機喜好設定 tooinfluence 路由。 在本例中，您可以指定本機喜好設定值 too13.100.0.0/16 中比在美國東部、 美國西部和同樣地，本機喜好設定值 too23.100.0.0/16 比位於美國西部的美國東部。 此設定可確保，這兩個路徑 tooMicrosoft 可用時，您的使用者在洛杉磯會接受在美國西部 tooconnect tooAzure 美國西部 hello ExpressRoute 電路而紐約使用者接受 hello ExpressRoute 在美國東部 tooAzure 美國東部. 這兩端的路由均已最佳化。 

![ExpressRoute 案例 1 解決方案 - 使用 BGP 社群](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> hello 相同的技巧，使用本機的喜好設定，可以套用的 toorouting 從客戶 tooAzure 虛擬網路。 我們不標記已從 Azure tooyour 網路公告的 BGP 社群值 toohello 前置詞。 不過，因為您知道哪一個虛擬網路部署的關閉 toowhich 的辦公室，您可以設定您的路由器據以 tooprefer 一個 ExpressRoute 電路 tooanother。
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>次佳路由從 Microsoft toocustomer
以下是另一個範例中，從 Microsoft 的連線會使用較長的路徑 tooreach 您的網路。 在此情況下，您可在 [混合式環境](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx)中使用內部部署 Exchange 伺服器和 Exchange Online。 您的辦公室可連接的 tooa WAN。 您會通告內部部署伺服器中的 hello 兩個 ExpressRoute 電路透過您的辦公室 tooMicrosoft hello 前置詞。 Exchange Online 將會起始連線 toohello 在內部部署伺服器，例如信箱移轉的情況下。 很遺憾，hello 連接 tooyour 洛杉磯分公司路由的 toohello 美國東部的 ExpressRoute 電路之前周遊整個 continent 後 toohello 西岸 hello。 hello hello 問題的原因是類似 toohello 第一個。 沒有任何提示，hello Microsoft 網路無法分辨哪些客戶前置詞是關閉的 tooUS 東部和哪一種關閉 tooUS 西。 發生在洛杉磯 toopick hello 錯誤的路徑 tooyour office。

![ExpressRoute 案例 2 的次佳路由從 Microsoft toocustomer](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>解決方案︰使用 AS PATH 前置
有兩個方案 toohello 問題。 hello 第一次是只要通告內部首碼 Los Angeles 辦公室 177.2.0.0/31，hello ExpressRoute 電路位於美國西部上，並在內部紐約辦公室 177.2.0.2/31，在美國東部 hello ExpressRoute 電路的前置詞。 如此一來，是您分公司的 Microsoft tooconnect tooeach 只能有一個路徑。 沒有模稜兩可的狀況，而且路由已最佳化。 與這個設計中，您會需要 toothink 有關容錯移轉策略。 Hello hello 路徑 tooMicrosoft 透過 ExpressRoute 的事件已中斷，您需要 toomake 確定 Exchange Online 可以仍然連接 tooyour 在內部部署伺服器。 

hello 第二個方案是您繼續這兩個 ExpressRoute 電路的 hello 首碼 tooadvertise，除了您提供的前置詞是您分公司的關閉 toowhich 的提示。 因為我們支援 BGP AS 路徑前面加上，您可以設定 hello AS 路徑前置詞 tooinfluence 器路由工具。 在此範例中，您可以延長為美國東部 172.2.0.0/31 hello AS 路徑，讓我們會偏好 hello ExpressRoute 電路位於美國西部的流量 （如網路會認為 hello 路徑 toothis 前置詞是短 hello 西） 針對此前置詞。 同樣地您會增加 172.2.0.2/31 位於美國西部的 hello AS 路徑，讓我們將會偏好在美國東部 hello ExpressRoute 電路。 這兩個辦公室的路由均已最佳化。 採用這個設計，如果一個 ExpressRoute 路線已中斷，Exchange Online 仍可透過另一個 ExpressRoute 線路和您的 WAN 來觸達您。 

> [!IMPORTANT]
> 我們移除私用，因為 Microsoft 對等互連收到 hello 前置詞的 hello AS 路徑中的數字。 您需要 tooappend 公用 AS 號碼 hello AS 路徑 tooinfluence 路由傳送中的 Microsoft 對等互連。
> 
> 

![ExpressRoute 案例 2 解決方案 - 使用 AS PATH 前置](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> 雖然此處指定的 hello 範例之 Microsoft 軟體和公用對等互連，我們支援 hello hello 私用對等互連的相同功能。 此外，hello AS 路徑前面加上在中運作單一 ExpressRoute 電路，tooinfluence hello hello 主要和次要路徑的選取項目。
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>虛擬網路之間的次佳化路由
透過 ExpressRoute，您可以啟用虛擬網路 tooVirtual 網路 （也稱為 「 VNet 」） 將它們連結 tooan ExpressRoute 電路的通訊。 當您連結它們 toomultiple ExpressRoute 電路時，次佳的路由可能會發生 hello Vnet 之間。 我們來看一個範例。 您有兩個 ExpressRoute 線路，一個在美國西部，一個在美國東部。 而在這兩個區域中，您各有兩個 VNet。 一個 VNet 中部署您的 web 伺服器，並在應用程式伺服器 hello 其他。 如需備援，您連結 hello 的每個區域 tooboth hello 本機 ExpressRoute 電路的兩個 Vnet 和 hello 遠端的 ExpressRoute 電路。 可以是如下所示，從每個 VNet 有兩個路徑 toohello 另一個 VNet。 hello Vnet 不知道哪一個 ExpressRoute 電路位於本機，以及哪一個是遠端。 因此一樣等成本-多重路徑 (ECMP) 路由 tooload 平衡間 VNet 流量，某些流量都有 hello 較長的路徑，因此會路由在 hello 遠端 ExpressRoute 循環。

![ExpressRoute 案例 3 - 虛擬網路之間的次佳化路由](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>解決方案： 指派加權高 toolocal 連接
hello 方案很簡單。 因為知道 hello Vnet 和 hello 電路位置，您可以告訴我們應該最好每個 VNet 的路徑。 特別針對此範例中，您指派較高權數 toohello 本機連接比 toohello 遠端連線 (請參閱 hello 組態範例[這裡](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection))。 當 VNet 收到 hello hello 前置詞上多個連接，它會與 hello 最高權數 toosend 流量目的該前置詞偏好 hello 連線其他 VNet。

![ExpressRoute 案例 3 方案-指派加權高 toolocal 連線](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> 您也可以決定路由從 VNet tooyour 在內部部署網路，如果您有多個 ExpressRoute 電路，藉由設定 hello 權數的連接，而不是套用 AS 路徑前面加上 hello 上面的第二個案例中所述的技術。 每個前置詞，我們將一律探討 hello 連接加權 hello AS 路徑長度之前決定時如何 toosend 流量。
>
>
