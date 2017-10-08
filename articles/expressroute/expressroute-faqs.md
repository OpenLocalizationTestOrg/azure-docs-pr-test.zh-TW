---
title: "aaaAzure ExpressRoute 常見問題集 |Microsoft 文件"
description: "hello ExpressRoute 常見問題集包含支援的 Azure 服務、 成本、 資料和連線、 SLA、 提供者和位置、 頻寬和其他技術詳細資料的相關資訊。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>ExpressRoute 常見問題集

## <a name="what-is-expressroute"></a>什麼是 ExpressRoute？

ExpressRoute 這項 Azure 服務可讓您在 Microsoft 資料中心和內部部署或共置設備中的基礎結構之間建立私人連線。 ExpressRoute 連線不會經過 hello 公用網際網路，並提供較高的安全性、 可靠性和速度降低延遲比一般連線透過網際網路 hello。

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>使用 ExpressRoute 和私人網路連線的 hello 優點有哪些？

ExpressRoute 連線不會經過 hello 公用網際網路。 它們提供更高的安全性、 可靠性和速度，比透過 hello 網際網路的一般連線較低且一致的延遲。 在某些情況下，使用 ExpressRoute 連線 tootransfer 資料之間的內部的裝置，Azure 會產生顯著的成本優勢。

### <a name="where-is-hello-service-available"></a>其中是 hello 服務可用？

請參閱以下頁面，以取得服務位置和可用性： [ExpressRoute 合作夥伴和位置](expressroute-locations.md)。

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>如果我並未與其中一個 hello ExpressRoute 電信業合作夥伴建立合作關係，如何使用 ExpressRoute tooconnect tooMicrosoft？

您可以選取一個地區性貨運公司，並進入乙太網路連線 tooone 的 hello 支援 exchange 提供者位置。 您接著可以使用 Microsoft hello 提供者位置互連。 檢查 hello 的最後一個區段[ExpressRoute 合作夥伴和位置](expressroute-locations.md)toosee 您服務提供者是否有任何 hello exchange 位置。 然後，您可以訂購 hello 服務提供者 tooconnect tooAzure 透過 ExpressRoute 電路。

### <a name="how-much-does-expressroute-cost"></a>ExpressRoute 需要多少錢？

如需價格資訊，請查看 [價格詳細資訊](https://azure.microsoft.com/pricing/details/expressroute/) 。

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>如果我支付給定頻寬的 ExpressRoute 電路並 hello 我從我的網路服務提供者購買的 VPN 連線 toobe 擁有 hello 相同的速度嗎？

否。 您可以從服務提供者購買任何速度的 VPN 連線。 不過，連線 tooAzure 是您購買的有限的 toohello ExpressRoute 電路頻寬。

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>如果我支付給定頻寬的 ExpressRoute 電路，我是否必須 hello 能力 tooburst toohigher 速度必要時註冊？

是。 ExpressRoute 電路都已設定的 tooallow tooburst tootwo 時間 hello 您無需額外成本提高現有頻寬限制。 如果它們支援這項功能，請洽詢您的服務提供者 toosee。

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>我可以使用 hello 同時私用的相同網路與虛擬網路與其他 Azure 服務的連線嗎？

是。 ExpressRoute 電路一旦設定完成，可讓您虛擬網路內的 tooaccess 服務和其他 Azure 服務同時。 您透過 toovirtual 網路 hello 私用對等互連路徑和 tooother 服務透過 hello 公用互連路徑。

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute 是否提供服務等級協定 (SLA)？

如需資訊，請參閱 hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/)頁面。

## <a name="supported-services"></a>支援的服務

ExpressRoute 針對各種服務類型支援[三種路由網域](expressroute-circuit-peerings.md)。

### <a name="private-peering"></a>私人對等互連

* 包括所有虛擬機器和雲端服務在內的虛擬網路

### <a name="public-peering"></a>公用對等互連

* Power BI
* Dynamics 365 for Finance and Operations (先前稱為 Dynamics AX Online)
* 大部分的 hello Azure 服務，以下列幾個例外狀況的 hello:
  * CDN
  * Visual Studio Team Services 負載測試 
  * 多因素驗證
  * 流量管理員

### <a name="microsoft-peering"></a>Microsoft 對等互連

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 Customer Engagement 應用程式 (先前稱為 CRM Online)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service

## <a name="data-and-connections"></a>資料與連線

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>有我可以使用 ExpressRoute 傳輸的資料的 hello 數量的限制嗎？

我們未上的資料傳輸的 hello 量設定限制。 請參閱太[定價詳細資料](https://azure.microsoft.com/pricing/details/expressroute/)如需頻寬費率的資訊。

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>ExpressRoute 支援的連線速度為何？

支援的頻寬優惠：

50 Mbps、100 Mbps、200 Mbps、500 Mbps、1 Gbps、2 Gbps、5 Gbps、10 Gbps

### <a name="which-service-providers-are-available"></a>可以使用的服務提供者有哪些？

請參閱[ExpressRoute 合作夥伴和位置](expressroute-locations.md)hello 清單服務提供者和位置。

## <a name="technical-details"></a>技術詳細資訊

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Hello 連線我在內部部署位置 tooAzure 的技術需求為何？

請參閱 [ExpressRoute 必要條件頁面](expressroute-prerequisites.md)以取得相關需求。

### <a name="are-connections-tooexpressroute-redundant"></a>會連線 tooExpressRoute 備援嗎？

是。 每個 ExpressRoute 電路都有一組備援的交叉連線設定 tooprovide 高可用性。

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>如果我的其中一個 ExpressRoute 連結失敗，連線是否就會中斷？

您不會中斷連線，如果一個的 hello 交叉連線會失敗。 備援連線是網路的可用 toosupport hello 負載。 此外，您就可以在不同對等互連位置 tooachieve 失敗恢復建立多個電路。

### <a name="onep2plink"></a>如果我不在雲端交換共我的服務提供者提供點對點連線，需要 tooorder 兩個實體之間的連線我的內部部署網路和 Microsoft？

如果您的服務提供者可以建立兩個乙太網路的虛擬電路 hello 實體連線，您只需要一個實體連線。 hello 實體連線 （例如，光纖） 已終止圖層上 1 (L1) 裝置 （請參閱 hello 映像）。 hello 兩個乙太網路的虛擬電路都會加上不同的 VLAN Id，一個 hello 主要循環，另一個用於次要的 hello。 這些 VLAN 識別碼採用 xxxnnnnn hello 外部 802.1 q 乙太網路標頭。 hello 內部 802.1 q 乙太網路標頭 （未顯示） 是特定的對應的 tooa [ExpressRoute 路由網域](expressroute-circuit-peerings.md)。

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>我可以將其中一個我使用 ExpressRoute 的 Vlan tooAzure 延伸嗎？

否。 我們不支援至 Azure 的第 2 層連線擴充程式。

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>我的訂用帳戶是否可以有多個 ExpressRoute 電路？

是。 您的訂用帳戶可以有多個 ExpressRoute 電路。 hello 預設限制是設 too10。 如有需要您可以連絡 Microsoft 支援服務 tooincrease hello 限制。

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>我可以使用其他服務提供者的 ExpressRoute 電路嗎？

是。 您可以使用許多服務提供者的 ExpressRoute 電路。 每個 ExpressRoute 線路只會與一個服務提供者產生關聯。 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>可以有多個 ExpressRoute 電路 hello 中相同的位置？

是。 您可以有多個 ExpressRoute 電路，與 hello 相同或不同的服務提供者在 hello 相同的位置。 不過，您無法連結多個 ExpressRoute 電路 toohello 相同虛擬 hello 從網路相同的位置。

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>我要如何連接我的虛擬網路 tooan ExpressRoute 電路

hello 基本步驟如下：

* 建立 ExpressRoute 電路並 hello 服務提供者啟用它。
* 您或 hello 提供者，必須設定 hello BGP 對等 (s)。
* 連結 hello 虛擬網路 toohello ExpressRoute 電路。

如需詳細資訊，請參閱 [ExpressRoute 工作流程線路佈建和線路狀態](expressroute-workflows.md)。

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>我的 ExpressRoute 電路是否有連線範圍？

是。 hello [ExpressRoute 合作夥伴和位置](expressroute-locations.md)文章提供概觀 hello 連線界限的 ExpressRoute 電路。 ExpressRoute 循環的連線能力是有限的 tooa 單一地理政治區域。 連線可以是展開的 toocross 地緣政治區域啟用 hello ExpressRoute premium 功能。

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>可以將連結 toomore 比一個虛擬網路 tooan ExpressRoute 電路嗎？

是。 您可以在擁有 too10 標準的 ExpressRoute 電路的虛擬網路連線和向上 too100 [premium ExpressRoute 電路](#expressroute-premium)。 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>我有多個含有虛擬網路的 Azure 訂用帳戶。 中的個別訂閱 tooa 單一 ExpressRoute 電路的虛擬網路可以連接嗎？

是。 您可以向上 too10 授權其他 Azure 訂用帳戶 toouse 單一 ExpressRoute 電路。 藉由啟用 hello ExpressRoute 高階功能，可以提高此限制。

如需詳細資訊，請參閱[在多個訂用帳戶中共用 ExpressRoute 線路](expressroute-howto-linkvnet-arm.md)。

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>已隔離的相同電路的虛擬網路連接的 toohello 彼此嗎？

否。 從路由的檢視方塊的所有虛擬網路連結 toohello 相同 ExpressRoute 電路屬於 hello 相同路由網域，而且不會互相隔離。 如果您需要路由隔離，您會需要 toocreate 不同的 ExpressRoute 電路。

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>可以有一個虛擬網路連接 toomore 比一個 ExpressRoute 電路嗎？

是。 您可以連結具有向上 toofour ExpressRoute 電路的單一虛擬網路。 它們必須透過 4 個不同的 [ExpressRoute 位置](expressroute-locations.md)來訂購。

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>可以存取網際網路 hello 從我的虛擬網路連接的 tooExpressRoute 電路嗎？

是。 如果您不具有公告預設路由 (0.0.0.0/0) 或網際網路路由首碼，透過 hello BGP 工作階段，您可以從虛擬網路連結 tooan ExpressRoute 電路連接 toohello 網際網路。

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>我可以封鎖網際網路連線 toovirtual 網路連線的 tooExpressRoute 電路嗎？

是。 您可以公告預設路由 (0.0.0.0/0) tooblock 所有的網際網路連線 toovirtual 機器虛擬網路中部署和路由傳送所有流量透過 hello ExpressRoute 電路。

如果您通告預設路由，我們會強制流量 tooservices 提供透過公用互連 （例如 Azure 儲存體和 SQL 資料庫） 的回復 tooyour 內部部署。 您必須 tooconfigure 您路由器 tooreturn 的流量有 tooAzure 透過 hello 公用互連路徑或 hello 網際網路。

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>可以虛擬網路連結的 toohello 相同 ExpressRoute 電路溝通 tooeach 其他嗎？

是。 虛擬機器部署在虛擬網路連接 toohello 相同 ExpressRoute 電路可與對方進行通訊。

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>我是否可以將虛擬網路的站對站連線與 ExpressRoute 搭配使用?

是。 ExpressRoute 可與站對站 VPN 並存。

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>可以移動的虛擬網路從站對站 / 點對站組態 toouse ExpressRoute 嗎？

是。 您將虛擬網路中有 toocreate ExpressRoute 閘道。 沒有與 hello 程序相關聯的短暫停機時間。

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>為什麼會有相關聯的虛擬網路上的 hello ExpressRoute 閘道的公用 IP 位址？

hello 公用 IP 位址用於只使用內部的管理。 這個公用 IP 位址不是公開的 toohello 網際網路，並不會構成安全性風險的虛擬網路。

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>怎麼 tooconnect tooAzure 儲存體需要透過 ExpressRoute？

您必須建立 ExpressRoute 電路，並設定公用對等互連的路由。

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>有我可以公告的路由的 hello 數目的限制嗎？

是。 我們接受 too4000 用於私人互連的路由前置詞和 200 每一個用於公用互連，Microsoft 對等互連。 您可以增加此 too10，000 路由用於私人互連，如果您啟用 hello ExpressRoute 高階功能。

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>有我可以透過 hello BGP 工作階段公告的 IP 範圍的限制嗎？

我們不接受在 hello 公用的私人首碼 (RFC1918) 與 Microsoft 對等互連 BGP 工作階段。

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>如果我超出 hello BGP 限制，會發生什麼情況？

BGP 工作階段將會被刪除。 一旦 hello 首碼數量低於 hello 限制，它們會被重設。

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>什麼是的 hello ExpressRoute BGP 保存的時間？ 可調整此保留時間嗎？

hello 保留時間是 180。 每隔 60 秒，就會傳送 hello 保持連線訊息。 這些被固定 hello Microsoft 端，無法變更設定。 很可能您 tooconfigure 不同計時器，並將據此交涉 hello BGP 工作階段參數。

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>我通告 hello 預設路由 (0.0.0.0/0) toomy 虛擬網路之後，我無法啟動我的 Azure Vm 上執行的 Windows。 如何 tooI 修正這個問題？

下列步驟的 hello 協助辨識 hello 啟用要求的 Azure:

1. 建立 hello 公用對等 ExpressRoute 電路。
2. 執行 DNS 查閱和尋找 hello IP 位址**kms.core.windows.net**
3. hello 金鑰管理服務必須辨識該 hello 啟用要求來自 Azure 與實行 hello 要求。 執行下列三個工作的 hello 的其中一個：

   * 您在內部部署網路上路由傳送嗨流量預定 hello 您在步驟 2 後 tooAzure 透過 hello 公用對等互連中取得的 IP 位址。
   * 具有您 NSP 提供者線 pin hello 流量後的 tooAzure 透過 hello 公用對等互連。
   * 建立使用者定義的路由有網際網路的下一個躍點，該點 hello IP，並將它套用 toohello 子網路，這些虛擬機器的所在。

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>可以變更 hello 頻寬的 ExpressRoute 電路嗎？

是，您可以嘗試 tooincrease hello 頻寬的 ExpressRoute 循環中 hello Azure 入口網站或 PowerShell。 如果您的電路建立所在的 hello 實體連接埠上有可用的容量，您的變更將會成功。 

如果您的變更失敗，表示可能是沒有剩餘的 hello 目前的連接埠足夠容量，而且您需要 toocreate 新的 ExpressRoute 電路與 hello 較高的頻寬，或在該位置沒有任何額外的容量，在此情況下您將無法tooincrease hello 頻寬。 

您也必須 toofollow 與您的連線提供者 tooensure 他們更新其網路 toosupport hello 頻寬增加內 hello 節流。 您無法，不過，減少 hello 頻寬的 ExpressRoute 電路。 您擁有 toocreate 新的 ExpressRoute 電路擁有較低頻寬，並且刪除 hello 舊循環。

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>如何變更 hello 頻寬的 ExpressRoute 電路？

您可以更新 hello 使用 hello REST API 或 PowerShell cmdlet 的 hello ExpressRoute 電路頻寬。

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>什麼是 ExpressRoute Premium？

ExpressRoute premium 是 hello 的集合下列功能：

* 增加路由的資料表限制，從 4000 路由 too10，000 用於私人互連的路由。
* 增加可以是連線的 toohello ExpressRoute 電路的 Vnet 數目 （預設值為 10）。 如需詳細資訊，請參閱 hello [ExpressRoute 限制](#limits)資料表。
* 連線 tooOffice 365 和 Dynamics 365。
* 全域 hello Microsoft 核心網路上的連線。 您現在可將某一個地緣政治區域中的 VNet 與另一個區域中的 ExpressRoute 線路連結。<br>
    **範例：**

    *  您可以連結在西歐 tooan 在美國矽谷建立 ExpressRoute 電路建立 VNet。 
    *  在 hello 公用對等互連，其他地緣政治區域前置詞已公告，您可以從在美國矽谷電路連接到，比方說，在西歐 SQL Azure。


### <a name="limits"></a>多少 Vnet 可以將連結 tooan ExpressRoute 電路如果啟用 ExpressRoute premium？

hello 下列表格顯示 hello ExpressRoute 限制和每個 ExpressRoute 電路的 Vnet 的 hello 數目：

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>我要如何啟用 ExpressRoute Premium？

ExpressRoute 高階功能時啟用 hello 功能時，可以啟用，而且可以藉由更新 hello 循環狀態關機。 您可以在電路建立時，啟用 ExpressRoute premium 或可以呼叫 hello REST API / PowerShell cmdlet。

### <a name="how-do-i-disable-expressroute-premium"></a>我要如何停用 ExpressRoute Premium？

您可以藉由呼叫 hello REST API 或 PowerShell cmdlet 來停用 ExpressRoute premium。 您必須確定您已停用 ExpressRoute premium 之前可能向您連線需求 toomeet hello 的預設限制。 如果您的使用率縮放比例超出 hello 預設限制，hello 要求 toodisable ExpressRoute 高階將會失敗。

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>可以我挑選並選擇 hello 我想要從 hello premium 功能集的功能嗎？

否。 您無法挑選 hello 功能。 當您開啟 ExpressRoute Premium 時，我們便會將所有功能啟用。

### <a name="how-much-does-expressroute-premium-cost"></a>ExpressRoute Premium 需要多少錢？

請參閱太[定價詳細資料](https://azure.microsoft.com/pricing/details/expressroute/)成本。

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>請勿我支付 ExpressRoute premium 除了 toostandard ExpressRoute 費用嗎？

是。 ExpressRoute premium 費用 適用於 ExpressRoute 電路費用和 hello 連線服務提供者所需的費用。

## <a name="expressroute-for-office-365-and-dynamics-365"></a>Office 365 和 Dynamics 365 的 ExpressRoute

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>如何建立 ExpressRoute 電路 tooconnect tooOffice 365 服務和 Dynamics 365？

1. 檢閱 hello [ExpressRoute 必要條件頁面](expressroute-prerequisites.md)toomake 確定您符合 hello 需求。
2. 符合您的連線需要 tooensure，檢閱 hello 的服務提供者和位置清單中 hello [ExpressRoute 合作夥伴和位置](expressroute-locations.md)發行項。
3. 透過檢閱 [Office 365 的網路規劃和效能調整](http://aka.ms/tune/)來計劃您的容量需求。
4. Hello 工作流程 tooset 連線設定中所列步驟 hello [ExpressRoute 循環佈建和循環狀態的工作流程](expressroute-workflows.md)。

> [!IMPORTANT]
> 請確定您已設定連線 tooOffice 365 服務和 Dynamics 365 時啟用 ExpressRoute premium 附加元件。
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>我需要 tooenable Azure 公用對等互連 tooconnect tooOffice 365 服務和 Dynamics 365？

否，您只需要 tooenable Microsoft 對等互連。 驗證流量 tooAzure AD 會傳送到 Microsoft 對等互連。 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>可以連線 tooOffice 365 服務和 Dynamics 365 支援我現有的 ExpressRoute 電路嗎？

是。 您現有的 ExpressRoute 電路可以設定的 toosupport 連線 tooOffice 365 服務。 請確定您有足夠的容量 tooconnect tooOffice 365 服務，且您已啟用高階的附加元件。 [Office 365 的網路規劃和效能調整](http://aka.ms/tune/)可協助您規劃連線需求。 另請參閱 [建立和修改 ExpressRoute 電路](expressroute-howto-circuit-classic.md)。

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>透過 ExpressRoute 連線可以存取哪些 Office 365 服務？

請參閱太[Office 365 Url 與 IP 位址範圍](http://aka.ms/o365endpoints)服務透過 ExpressRoute 受到支援的最新清單的頁面。

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>適用於 Office 365 服務和 Dynamics 365 的 ExpressRoute 費用是多少？

Office 365 服務和 Dynamics 365 需要啟用 premium 附加元件 toobe。 請參閱 hello[定價詳細資料頁面](https://azure.microsoft.com/pricing/details/expressroute/)成本。

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>哪些區域支援 ExpressRoute for Office 365？

如需相關資訊，請參閱 [ExpressRoute 合作夥伴和位置](expressroute-locations.md)。

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>我可以存取 Office 365 透過 hello 網際網路，即使我的組織已設定 ExpressRoute 嗎？

是。 即使已針對您的網路設定 ExpressRoute，是透過 hello 網際網路，連線到 office 365 的服務端點。 如果您是透過 ExpressRoute 設定的 tooconnect tooOffice 365 服務的位置中，您會透過 ExpressRoute 進行連線。

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>我是否可以透過 Azure 美國政府 ExpressRoute 電路存取 Office 365 US Government Community (GCC) 服務？

是。 Office 365 GCC 服務端點都可以透過 hello Azure 美國政府 ExpressRoute 連線。 不過，您第一次需要 tooopen 支援票證 hello 想 tooadvertise tooMicrosoft 的 Azure 入口網站 tooprovide hello 前置詞。 解決 hello 支援票證後，將會建立連線 tooOffice 365 GCC 服務。 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>是否可透過 ExpressRoute 連線存取 Dynamics 365 for Operations (先前稱為 Dynamics AX Online)？

是。 [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) 是裝載於 Azure 上。 您可以啟用您的 ExpressRoute 電路 tooconnect tooit 上 Azure 公用對等。

## <a name="route-filters-for-microsoft-peering"></a>Microsoft 對等互連的路由篩選

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>開啟 Microsoft 對等互連 hello 第一次，會看到哪些路由？

您不會看到任何路由。 您有 tooattach 路由篩選 tooyour 電路 toostart 前置詞通告。 如需指示，請參閱[針對 Microsoft 對等互連設定路由篩選](how-to-routefilter-powershell.md)。

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>我已開啟的 Microsoft 對等互連，而且現在我嘗試 tooselect Exchange Online，但是它會讓我我不是授權的 toodo 錯誤它。

當使用路由篩選時，任何客戶都可開啟 Microsoft 對等互連。 不過，使用 Office 365 服務，您仍然需要 tooget 由 Office 365 授權。

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>需要透過 Microsoft 對等互連開啟 Dynamics 365 tooget 授權嗎？

否，您不需要 Dynamics 365 的授權。 您不需授權就可建立規則和選取 Dynamics 365 社群。

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>我已經有 Microsoft 對等互連，該如何利用路由篩選？

您可以建立路由篩選器，您想 toouse，並將選取的 hello 服務 hello 篩選 tooyour Microsoft 對等互連。 如需指示，請參閱[針對 Microsoft 對等互連設定路由篩選](how-to-routefilter-powershell.md)。

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>我有 Microsoft 對等互連的位置，現在我試著 tooenable 它在其他位置並沒有看到任何前置詞。

* Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。

* Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。 根據預設，您不會看見任何首碼。
