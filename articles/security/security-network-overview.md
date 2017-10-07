---
title: "aaaNetwork 安全性概念和 Azure 中的需求 |Microsoft 文件"
description: " 這篇文章方便您 toounderstand 什麼 Microsoft Azure 有 toooffer hello 網路安全性區域中。 我們提供的核心網路的安全性概念和需求的基本說明，且在 Azure 上的資訊 toooffer 中每個區域。 "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Azure 網路安全性概觀
Microsoft Azure 包括強固的網路基礎結構 toosupport 應用程式和服務連線需求。 在 Azure 中，位於內部部署之間的資源之間的網路連線可與 Azure 託管資源和 tooand 從 hello 網際網路和 Azure。

這篇文章的 hello 目標是 toomake 輕鬆您 toounderstand 什麼 Microsoft Azure 有 toooffer hello 區域中的網路安全性。 這裡我們提供核心網路安全性概念和需求的基本說明。 此外，我們也會提供您有關 Azure 中每個區域有 toooffer，以及連結 toohelp 獲得更深層的了解的感興趣的區域。

Azure 網路安全性概觀本文著重於 hello 下列區域：

* Azure 網路
* 網路存取控制
* 安全遠端存取和跨單位連線
* Availability
* 名稱解析
* DMZ 架構
* 監視與威脅偵測


## <a name="azure-networking"></a>Azure 網路
虛擬機器需要遠端連線。 toosupport 該需求，Azure 需要連接的虛擬機器 toobe tooan Azure 虛擬網路。 Azure 虛擬網路是建立在 hello Azure 的實體網路網狀架構之上一個邏輯結構。 每個邏輯 Azure 虛擬網路都會與其他所有 Azure 虛擬網路隔離。 這有助於確保您的部署中的網路流量不是可存取 tooother Microsoft Azure 客戶。

深入了解：

* [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>網路存取控制
網路存取控制就是限制從特定裝置或 Azure 虛擬網路內的子網路的連線能力 tooand hello 操作。 hello 的目標網路存取控制是 toolimit 存取 tooyour 虛擬機器和服務 tooapproved 使用者和裝置。 存取控制以在允許或拒絕您的虛擬機器或服務的連線 tooand 決策。

Azure 支援數種類型的網路存取控制，例如︰

* 網路層控制
* 路由控制和強制通道
* 虛擬網路安全性應用裝置

### <a name="network-layer-control"></a>網路層控制
任何安全部署都需要某種程度的網路存取控制。 hello 的目標網路存取控制是 toorestrict 虛擬機器通訊 toohello 必要系統和其他通訊嘗試會遭到封鎖。

如果您需要基本網路層級的存取控制 （根據 IP 位址和 hello TCP 或 UDP 通訊協定），您可以使用網路安全性群組。 網路安全性群組 (NSG) 是基本可設定狀態篩選封包的防火牆，它可讓您 toocontrol 存取權限[5-tuple](https://www.techopedia.com/definition/28190/5-tuple)。 NSG 未提供應用程式層級檢查或已驗證的存取控制。

深入了解：

* [網路安全性群組](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>路由控制和強制通道
在 Azure 虛擬網路上的 hello 能力 toocontrol 路由行為是嚴重的網路安全性和存取控制功能。 路由的設定不正確，如果應用程式和虛擬機器上裝載的服務可能會連線 toounauthorized 裝置，包括系統所擁有和潛在的攻擊者的操作。

Azure 網路支援您的 Azure 虛擬網路上的網路流量 hello 能力 toocustomize hello 路由行為。 這可讓您 tooalter hello 預設路由表項目在 Azure 虛擬網路中。 路由行為的控制可協助您確保來自特定裝置或一組裝置的所有流量，都透過特定位置進入或離開您的虛擬網路。

例如，您在 Azure 虛擬網路上可能會有虛擬網路安全性應用裝置。 您想 toomake 確定從 Azure 虛擬網路的所有流量 tooand 都通過該虛擬的安全性應用裝置。 做法是在 Azure 中設定 [使用者定義的路由](../virtual-network/virtual-networks-udr-overview.md) 。

[強制通道](https://www.petri.com/azure-forced-tunneling)的機制，您可以使用您的服務不 tooensure 允許 tooinitiate 連接 toodevices hello 網際網路上。 請注意，這不同於接受連入連線，然後回應 toothem。 前端網頁伺服器需要從網際網路主機 toorespond toorequests 且允許來自網際網路的流量，因此輸入的 toothese 網頁伺服器和 hello web 伺服器允許 toorespond。

功能不想 tooallow 是前端 web 伺服器 tooinitiate 外送要求。 這類要求可能代表安全性風險，因為這些連接是使用的 toodownload 惡意程式碼。 即使您希望這些前端伺服器 tooinitiate 輸出要求 toohello 網際網路時，您可能會想 tooforce 它們 toogo 透過內部 web proxy，以便您可以利用 URL 篩選和記錄。

相反地，您會想 toouse 強制通道 tooprevent 這。 當您啟用強制通道時，所有連線 toohello 網際網路都強制透過內部部署閘道。 您可以利用「使用者定義的路由」來設定強制通道。

深入了解：

* [什麼是使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>虛擬網路安全性應用裝置
雖然網路安全性群組、 使用者定義路由及強制通道可提供您的 hello hello 網路和傳輸層級的安全性層級[OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，有時可能會想 tooenable 安全性較高的層級與 hello 網路。

例如，您的安全性需求可能包括︰

* 驗證和授權，才能允許存取 tooyour 應用程式
* 入侵偵測和入侵回應
* 高層級通訊協定的應用程式層檢查
* URL 篩選
* 網路層級防毒和反惡意程式碼 
* 反 Bot 保護
* 應用程式存取控制
* （上方 hello DDoS 保護提供 hello Azure 網狀架構本身) 的額外 DDoS 保護

您可以使用 Azure 合作夥伴方案，來存取這些增強的網路安全性功能。 您可以找到 hello 最新的 Azure 合作夥伴網路安全性解決方案瀏覽 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/)並搜尋 「 安全性 」 及 「 網路安全性 」。

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>安全遠端存取和跨單位連線
安裝程式、 設定及管理您的 Azure 資源需要 toobe 從遠端進行。 此外，您可能會想 toodeploy[混合式 IT](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx)元件在內部部署解決方案和 hello Azure 公用雲端中。 這些案例都需要安全遠端存取。

Azure 網路支援下列安全遠端存取案例的 hello:

* 連接個別的工作站 tooan Azure 虛擬網路
* 使用 VPN 連接您在內部部署網路 tooan Azure 虛擬網路
* 使用專用的 WAN 連結連線您的內部部署網路 tooan Azure 虛擬網路
* 連接 Azure 虛擬網路 tooeach 其他

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>連接個別的工作站 tooan Azure 虛擬網路
可能有您想 tooenable 個別開發人員或作業人員 toomanage 虛擬機器和服務在 Azure 中的時間。 例如，您需要存取 tooa Azure 虛擬網路上的虛擬機器，而您的安全性原則不允許 RDP 或 SSH 的遠端存取 tooindividual 虛擬機器。 在此情況下，您可以使用點對站 VPN 連接。

hello 點對站 VPN 連線使用 hello [SSTP VPN](https://technet.microsoft.com/library/cc731352.aspx)通訊協定 tooenable tooset hello 使用者與 hello Azure 虛擬網路之間的私用和安全連線。 Hello VPN 連線建立之後，hello 使用者將能夠 tooRDP 或 hello VPN 透過 SSH 連結至任何 hello Azure 虛擬網路 （假設 hello 使用者可以進行驗證和授權） 上的虛擬機器。

深入了解：

* [設定點對站連線 tooa 虛擬網路，使用 PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>使用 VPN 連接內部部署網路 tooan Azure 虛擬網路
您的整個公司網路或其中 tooan Azure 虛擬網路的一部分，您可能想 tooconnect。 這常見於公司 [將其內部部署資料中心擴充到 Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84)的混合式 IT 案例。 在許多情況下，公司會在 Azure 和內部部署中裝載服務的各個部分 (例如，方案在 Azure 中包括前端 Web 伺服器而在內部部署中包括後端資料庫時)。 這些類型的「跨單位」連線也可更安全地管理 Azure 所在資源，並支援將 Active Directory 網域控制站擴充到 Azure 等案例。

其中一種方式 tooaccomplish 這是 toouse[站對站 VPN](https://www.techopedia.com/definition/30747/site-to-site-vpn)。 站對站 VPN 和點對站 VPN 的 hello 差異為點對站 VPN 連接單一裝置 tooan Azure 虛擬網路，雖然站對站 VPN 連線 （例如您的內部網路） 的整個網路 tooan Azure 虛擬網路. 站對站 Vpn tooan Azure 虛擬網路使用 hello 高度安全 IPsec 通道模式 VPN 通訊協定。

深入了解：

* [建立資源管理員 VNet 使用 hello Azure 入口網站的站對站 VPN 連接](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [規劃與設計 VPN 閘道](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>使用專用的 WAN 連結連線您的內部部署網路 tooan Azure 虛擬網路
點對站和站對站 VPN 連接適用於啟用跨單位連接。 不過，某些組織考慮它們 toohave hello 下列缺點：

* VPN 連線透過網際網路 hello 移動資料，這樣會公開這些連線 toopotential 涉及的安全性問題以透過公用網路移動資料。 此外，無法保證網際網路連接的可靠性和可用性。
* VPN 連線 tooAzure 虛擬網路頻寬限制某些應用程式和目的，您會看到以約 200 Mbps max 出列入考量。

通常需要 hello 高層級的安全性和可用性的跨單位連線的組織使用專用的 WAN 連結 tooconnect tooremote 站台。 Azure 提供 hello 能力 toouse 專用，您可以使用 tooconnect 您在內部部署網路 tooan Azure 虛擬網路的 WAN 連結。 這是透過 Azure ExpressRoute 來啟用。

深入了解：

* [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>連接 Azure 虛擬網路 tooEach 其他
您 toouse 可能會為您部署多個 Azure 虛擬網路。 有許多原因可能會這麼做。 其中一個 hello 原因可能是 toosimplify 管理;另一個可能基於安全性考量。 不論 hello 動機或將資源放在不同的 Azure 虛擬網路上的基本原理，可能是您想在每個 hello 網路 tooconnect 與其他資源時。

其中一個選項以 「 回迴圈 」 時，會針對上一個 Azure 虛擬網路 tooconnect tooservices 另一個 Azure 虛擬網路上的服務透過網際網路 hello。 hello 連接會在一個 Azure 虛擬網路上啟動、 瀏覽 hello 網際網路，，然後返回 toohello 目的地 Azure 虛擬網路。 此選項會顯示 hello 連接 toohello 安全性問題固有 tooany 以網際網路為基礎的通訊。

更好的選項可能 toocreate Azure 虛擬網路至 Azure 虛擬網路的站對站 VPN。 此使用站對站 VPN 的 Azure 虛擬網路至 Azure 虛擬網路 hello 相同[IPsec 通道模式](https://technet.microsoft.com/library/cc786385.aspx)為上述的 hello 跨單位站對站 VPN 連線的通訊協定。

使用 Azure 虛擬網路至 Azure 虛擬網路的站對站 VPN 的 hello 優點是 hello VPN 連線透過 hello Azure 網路網狀架構，而不是透過 hello 網際網路連線建立。 這會提供您一層額外的安全性比透過 hello 網際網路連線的 toosite 對站 Vpn。

深入了解：

* [使用 Azure Resource Manager 和 PowerShell 來設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Availability
可用性是任何安全性程式的重要元件。 如果您的使用者和系統無法存取其功能需要透過 hello tooaccess 網路，hello 服務可以視為入侵。 Azure 有網路技術下列高可用性機制，支援 hello:

* 以 HTTP 為基礎的負載平衡
* 網路層級負載平衡
* 全域負載平衡

負載平衡是設計用機制 tooequally 分散在多個裝置之間的連線。 負載平衡 hello 目標是：

* 當您跨多個裝置載入平衡連線，一或多個 hello 裝置可以變成無法使用，而且 hello hello 剩餘線上裝置上執行的服務可以繼續從 hello 服務 tooserve hello 內容時，提高可用性 –
* 提升效能： 當您跨多個裝置載入平衡連線，單一裝置沒有 tootake hello 處理器叫用。 相反地，hello 處理和記憶體需求提供 hello 內容分成多個裝置。

### <a name="http-based-load-balancing"></a>以 HTTP 為基礎的負載平衡
組織執行的 web 服務通常會想要 toohave 這些 web 服務 toohelp 前面使用以 HTTP 為基礎的負載平衡器可確保適當的層級的效能和高可用性。 相較之下 tootraditional 網路為基礎的負載平衡器、 hello 負載平衡以 HTTP 為基礎的負載平衡器所做的決策根據特性 hello HTTP 通訊協定，不是在 hello 網路和傳輸層通訊協定。

tooprovide 您以 HTTP 為基礎的負載平衡您的 web 型服務，Azure 提供 hello Azure 應用程式閘道。 hello Azure 應用程式閘道支援：

* 以 HTTP 為基礎的負載平衡 – 負載平衡決策依據進行特性特殊 toohello HTTP 通訊協定
* Cookie 架構工作階段親和性 – 這項功能可確保該負載平衡器後方的 hello 伺服器的 tooone 保持不動 hello 用戶端與伺服器之間建立連線。 這樣可確保交易的穩定性。
* SSL 卸載 – 用戶端連接是以建立 hello 負載平衡器，使用 hello HTTPS 加密 hello 用戶端與 hello 負載平衡器之間的工作階段 (SSL /) 通訊協定。 不過，order tooincrease 效能降低，您 hello 選項 toohave hello 和之間有連線 hello 負載平衡器後方 hello 負載平衡器使用 hello （未加密） 的 HTTP 通訊協定的 hello web 伺服器。 這是參考的 tooas"SSL 卸載"，因為 hello hello 負載平衡器後方的網頁伺服器不會遇到 hello 處理器額外負荷涉及使用加密功能，並因此更快速地應該是可以 tooservice 要求。
* URL 為基礎內容的路由 – 這項功能可讓 hello 負載平衡器 toomake 決策 tooforward 連線會根據 hello 目標 URL。 這所提供的彈性大於根據 IP 位址進行負載平衡決策的方案。

深入了解：

* [應用程式閘道概觀](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>網路層級負載平衡
相較之下 tooHTTP 為依據負載平衡，網路層級負載平衡可讓負載平衡 IP 位址和連接埠 （TCP 或 UDP） 編號為基礎的決策。
您可以取得網路層級的負載，使用 hello Azure 負載平衡器平衡在 Azure 中的 hello 的優點。 Hello Azure 負載平衡器的某些關鍵特性包括：

* 根據 IP 位址和連接埠號碼的網路層級負載平衡
* 支援任何應用程式層通訊協定
* 負載平衡 tooAzure 虛擬機器和雲端服務角色執行個體
* 可以用於網際網路面向 (外部負載平衡) 與非網際網路面向 (內部負載平衡) 應用程式和虛擬機器
* 端點監視，也就是使用的 toodetermine，如果任何 hello 負載平衡器後方的 hello 服務已變成無法使用

深入了解：

* [多個虛擬機器或服務之間的網際網路面向負載平衡器](../load-balancer/load-balancer-internet-overview.md)
* [內部負載平衡器概觀](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>全域負載平衡
某些組織會想可能 hello 最高層級的可用性。 這個目標是全域 toohost 應用程式中的其中一種方式 tooreach 分散式資料中心。 應用程式裝載在整個 hello world 位於資料中心，時，可能針對整個地緣政治區域 toobecome 無法使用，最多有 hello 應用程式且正在執行。

此外您藉由裝載在全域散發的資料中心的應用程式取得 toohello 可用性優點，您也可以取得效能優勢。 這些效能優點可透過使用會將 hello 服務 toohello 資料中心內最接近 toohello 裝置 hello 要求提出的要求導向機制。

全域負載平衡可以提供這兩項優點。 在 Azure 中，您可以瞭解 hello 全域負載平衡使用 Azure 流量管理員的優點。

深入了解：

* [什麼是流量管理員？](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>名稱解析
名稱解析是您在 Azure 中裝載之所有服務的重大功能。 從安全性觀點來看，洩露的 hello 名稱解析函式可能會導致 tooan 攻擊者重新導向要求，從站台 tooan 攻擊者的站台。 安全名稱解析是所有雲端裝載服務的需求。

有兩種類型的名稱解析，您需要 tooaddress:

* 內部名稱解析 – Azure 虛擬網路和 (或) 內部部署網路上的服務會使用內部名稱解析。 透過網際網路 hello 便無法存取所使用的內部名稱解析名稱。 為了取得最佳安全性，務必確認您的內部名稱解析配置不是可存取 tooexternal 使用者。
* 外部名稱解析 – 內部部署和 Azure 虛擬網路外部的人員和裝置會使用外部名稱解析。 這些是 hello 名稱可見 toohello 網際網路並是使用的 toodirect 連接 tooyour 雲端式服務。

對於內部名稱解析，您有兩個選項︰

* Azure 虛擬網路 DNS 伺服器 – 建立新的 Azure 虛擬網路時，會建立 DNS 伺服器。 此 DNS 伺服器可以解析 hello 位於 Azure 虛擬網路上的 hello 機器名稱。 此 DNS 伺服器可設定並不受 hello Azure 網狀架構管理員，因此讓它成為安全的名稱解析方案。
* 攜帶您自己的 DNS 伺服器 – 有 hello 選項可讓您的 Azure 虛擬網路上您自己選擇的 DNS 伺服器。 此 DNS 伺服器可能是 Active Directory 整合 DNS 伺服器或專用的 DNS 伺服器方案，您可以從 hello Azure Marketplace 取得 Azure 協力廠商所提供。

深入了解：

* [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)
* [管理虛擬網路 (VNet) 所使用的 DNS 伺服器](../virtual-network/virtual-network-manage-network.md#dns-servers)

對於外部 DNS 解析，您有兩個選項︰

* 在內部部署裝載專屬外部 DNS 伺服器
* 使用服務提供者裝載專屬外部 DNS 伺服器

許多大型組織都會在內部部署裝載其專屬 DNS 伺服器。 因為它們具有 hello 網路專業知識和全域存在 toodo 所以他們可以這麼做。

在大部分情況下，是較佳的 toohost 您的 DNS 名稱解析服務的服務提供者。 這些服務提供者有 hello 網路專業知識與您的名稱解析服務的全域存在 tooensure 非常高可用性。 可用性是重要的 DNS 服務，因為名稱解析服務失敗時，如果沒有人會是能 tooreach 您的網際網路對向服務。

Azure 提供高可用性和高效能外部的 DNS 方案 hello Azure DNS 形式。 這個外部名稱解析方案會利用 hello 全球 Azure DNS 基礎結構。 它可讓您 toohost 您的網域在 Azure 中使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。 Azure 的一部分，它也會繼承 hello 平台內建的 hello 的增強式安全性控制項。

深入了解：

* [Azure DNS 概觀](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>DMZ 架構
許多企業組織使用 Dmz toosegment hello 網際網路與服務之間的網路 toocreate 緩衝區區域。 hello 網路 hello DMZ 部分會被視為低安全性區域和任何高價值資產會放在該網路區段。 通常，您會看到有 hello DMZ 區段與另一個網路介面連接的 tooa 具有網路，虛擬機器和接受來自網際網路的 hello 輸入的連線的服務上的網路介面的網路安全性裝置。

有幾種變化的 DMZ 設計及 hello 決策 toodeploy 周邊網路，然後哪種類型的 DMZ toouse 如果您決定 toouse 其中一個，會根據您的網路安全性需求。

深入了解：

* [Microsoft 雲端服務和網路安全性](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>監視與威脅偵測

Azure 提供的功能 toohelp 您早期偵測、 監視與 hello 能力 toocollect 和檢閱網路流量與此主要區域中。

### <a name="azure-network-watcher"></a>Azure 網路監看員
Azure 網路監看員包含大量的功能，可協助您進行疑難排解，以及提供一組全新的工具 tooassist hello 識別的安全性問題。

[安全性群組檢視](/network-watcher/network-watcher-security-group-view-overview.md)有助於稽核及安全性的相容性的虛擬機器，可以使用的 tooperform 程式設計稽核比較您的組織 tooeffective 規則所定義的每個 Vm 的 hello 基準原則。 這可以協助您識別所有設定漂移。

[封包擷取](/network-watcher/network-watcher-packet-capture-overview.md)可讓您 toocapture 網路流量 tooand 從 hello 虛擬機器。 除了協助可讓您 toocollect 網路統計資料和應用程式的疑難排解 hello 問題封包擷取在十分有用 hello 調查網路入侵。 您也可以使用這項功能，以及 Azure 函式 toostart 網路擷取回應 toospecific Azure 中的警示。

如需有關 Azure 網路監看員 」 和 「 如何在實驗室中測試一些 hello 功能 toostart 看看 hello [Azure 網路監看員監視概觀](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Azure 網路監看員仍處於公開預覽，它可能不會有 hello 相同層級的可用性和可靠性視為一般可用性發行服務。 可能不支援特定功能、可能有限制的功能，且可能無法在所有 Azure 位置提供使用。 Hello 上此服務的可用性與狀態的最新通知，請檢查 hello [Azure 的更新 頁面](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure 資訊安全中心
資訊安全中心可協助您防止、 偵測，並回應 toothreats，，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。 它在您的 Azure 訂用帳戶之間提供整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於大量的安全性解決方案。

Azure 資訊安全中心藉由下列方式來協助您最佳化和監視網路安全性︰

* 提供網路安全性建議
* 監視網路安全性組態的 hello 狀態
* 提醒您 toonetwork 基礎威脅這兩個在 hello 端點和網路層級

深入了解：

* [簡介 tooAzure 資訊安全中心](../security-center/security-center-intro.md)


### <a name="logging"></a>記錄
網路層級的記錄是任何網路安全性案例的重要功能。 在 Azure 中，您可以取得記錄資訊的網路安全性群組 tooget 網路層級的資訊記錄。 使用 NSG 記錄，您可以從下列項目取得資訊︰

* [活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)– 這些記錄是使用的 tooview 所有作業都提交 tooyour Azure 訂用帳戶。 依預設會啟用這些記錄檔，且可用於 hello Azure 入口網站。 它們以前稱為「稽核記錄」或「作業記錄」。
* 事件記錄檔 – 這些記錄檔提供套用哪些 NSG 規則的相關資訊。
* 計數器的記錄檔-這些記錄檔可讓您知道每個 NSG 規則已套用的 toodeny 多少次，或允許流量。

您也可以使用[Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/)、 功能強大的資料視覺效果工具，tooview 和分析這些記錄檔。

深入了解：

* [網路安全性群組 (NSG) 的 Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md)
