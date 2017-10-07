---
title: "aaaAzure 網路安全性最佳作法 |Microsoft 文件"
description: "本文提供使用內建 Azure 功能的一些網路安全性最佳作法。"
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Azure 網路安全性最佳作法
Microsoft Azure 可讓您 tooconnect 虛擬機器和應用裝置 tooother 已連線到網路裝置放在 Azure 虛擬網路上。 Azure 虛擬網路是虛擬網路建構，可讓您 tooconnect 虛擬網路介面卡 tooa 虛擬網路 tooallow TCP 架構之間的通訊啟用網路裝置。 Azure 虛擬機器連線的 tooan Azure 虛擬網路都能 tooconnect toodevices hello 相同 Azure 虛擬網路，不同 Azure 虛擬網路，hello 網際網路上，或甚至在內部部署網路上。

本文將討論 Azure 網路安全性最佳作法的集合。 這些最佳作法衍生自 Azure 網路的經驗，而且 hello 經驗的客戶想自己。

針對每個最佳作法，我們會說明︰

* 哪些 hello 最佳作法是
* 為什麼要 tooenable 該最佳作法
* 如果您無法 tooenable hello 最佳作法，可能 hello 結果
* 可能的替代方式 toohello 最佳作法
* 如何了解 tooenable hello 最佳作法

此 Azure 網路安全性最佳做法文章根據共識意見，Azure 平台功能和功能集，存在於 hello 撰寫本文時的時間。 隨時間變更的意見和技術，且這篇文章會定期 tooreflect 上更新這些變更。

本文討論的 Azure 網路安全性最佳作法包括︰

* 以邏輯方式分割子網路
* 控制路由行為
* 啟用強制通道
* 使用虛擬網路應用裝置
* 部署 DMZ 進行安全性分區
* 避免暴露 toohello 網際網路具有專用的 WAN 連結
* 將執行時間和效能最佳化
* 使用全域負載平衡
* 停用虛擬機器的 RDP 存取 tooAzure
* 啟用 Azure 資訊安全中心
* 將資料中心擴充至 Azure

## <a name="logically-segment-subnets"></a>以邏輯方式分割子網路
[Azure 虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)會在內部部署網路上的類似 tooa LAN。 hello Azure 虛擬網路概念是，您建立單一私人 IP 位址空間型的網路您可以將所有您[Azure 虛擬機器](https://azure.microsoft.com/services/virtual-machines/)。 hello 類別 A (10.0.0.0/8)，類別 B (172.16.0.0/12) 和類別 C (192.168.0.0/16) 範圍位於 hello 私人 IP 位址空間可用。

類似 toowhat 您不要在內部，您會想 toosegment hello 較大的位址空間至子網路。 您可以使用[CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)基礎子網路原則 toocreate > 您子網路。

子網路間路由動作會自動發生，而且您不需要 toomanually 設定路由表。 不過，hello 預設設定為您建立 hello Azure 虛擬網路的 hello 子網路之間沒有網路存取控制項。 在訂單 toocreate 網路存取控制之間的子網路，您將需要 tooput hello 子網路之間的項目。

其中一項 hello 您可以使用這項工作的 tooaccomplish[網路安全性群組](../virtual-network/virtual-networks-nsg.md)(NSG)。 Nsg 是簡單的可設定狀態之封包檢查使用 hello 5 個 tuple （hello 來源 IP、 來源連接埠、 目的地 IP、 目的地連接埠和第 4 層通訊協定） 的裝置會很接近 toocreate 允許/拒絕規則的網路流量。 您可以允許或拒絕流量 tooand 來自單一 IP 位址、 tooand 從多個 IP 位址或甚至 tooand 從整個子網路。

使用 Nsg，子網路之間的網路存取控制可讓您將屬於 toohello tooput 資源相同的安全性區域或在他們自己的子網路中的角色。 例如，簡單的 3 層式應用程式具有 Web 層、應用程式邏輯層和資料庫層。 您放入自己的子網路都屬於 tooeach 的這些層的虛擬機器。 然後，您要使用 Nsg toocontrol hello 子網路之間的流量：

* Web 層的虛擬機器只可以起始連接 toohello 應用程式邏輯機器，並可以只接受來自 hello 網際網路連線
* 應用程式邏輯的虛擬機器可以僅開始與資料庫層的連接，而且只可接受來自 hello web 層連接
* 資料庫在階層虛擬機器無法初始連線與自己的子網路之外的任何項目，並可以只接受來自 hello 應用程式邏輯層連線

更多關於網路安全性群組，您可以如何使用這些 toologically 區段 toolearn 您的 Azure 虛擬網路，請閱讀 hello 文章[什麼是網路安全性群組](../virtual-network/virtual-networks-nsg.md)(NSG)。

## <a name="control-routing-behavior"></a>控制路由行為
當您將虛擬機器放在 Azure 虛擬網路上時，您會發現該 hello 虛擬機器可以連接 tooany 其他虛擬機器上 hello 相同 Azure 虛擬網路，即使 hello 其他虛擬機器位於不同子網路。 hello 為什麼這是通訊的可能的原因是通訊的之路由的集合系統預設會啟用，可讓這種類型。 這些預設路由允許 hello 上的虛擬機器相同 Azure 虛擬網路 tooinitiate 連線，以及以 hello 網際網路 （適用於輸出通訊 toohello 網際網路只)。

雖然 hello 預設系統路由可用於許多部署案例，但是會的想 toocustomize hello 路由設定為您的部署。 這些自訂項目可讓您 tooconfigure hello 下一個躍點位址 tooreach 特定的目的地。

建議您在部署虛擬網路安全性應用裝置時設定「使用者定義的路由」，我們將在更新版的最佳作法中進行討論。

> [!NOTE]
> 使用者定義的路由不需要與 hello 預設系統路由會在大部分情況下運作。
>
>

您可以進一步了解使用者定義的路由和如何 tooconfigure 它們藉由讀取 hello 文章[什麼是使用者定義的路由與 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。

## <a name="enable-forced-tunneling"></a>啟用強制通道
toobetter 了解強制通道，就很有用的 toounderstand 哪些 「 分割通道 」 是。
hello 的分割通道的最常見範例是看過的 VPN 連線。 假設您建立 VPN 連線，從旅館房間 tooyour 公司網路。 這個連接可讓您 tooconnect tooresources 您公司網路上和您公司網路上的所有通訊 tooresources 都經由 hello VPN 通道。

當您想 tooconnect tooresources hello 網際網路上的時，發生什麼事？ 啟用分割通道時，這些連線會直接移 toohello 網際網路，並不能透過 hello VPN 通道。 某些安全性專家考慮這個 toobe 潛在的風險，因此建議，停用分割通道，所有連線，針對 hello 網際網路以及針對 公司資源，經由 hello VPN 通道。 hello 優點，這麼做的是網際網路然後強制 hello 公司網路安全性裝置，而不是 hello 情況下，如果 hello VPN 用戶端連線 toohello 網際網路之外 hello VPN 通道透過該連線 toohello。

現在讓我們將此備份 toovirtual 機器 Azure 虛擬網路上。 Azure 虛擬網路的 hello 預設路由可讓虛擬機器 tooinitiate 流量 toohello 網際網路。 這太可代表安全性風險，這些傳出的連接可能會增加虛擬機器的 hello 受攻擊面並利用這些攻擊者。
基於這個理由，當您的 Azure 虛擬網路與內部部署網路之間有跨單位連線時，建議您在虛擬機器上啟用強制通道。 我們稍後會在這份 Azure 網路最佳作法文件中討論跨單位的連線能力。

如果沒有跨單位連線，請確定您的網路安全性群組 （稍早所討論） 或 Azure 利用虛擬網路的安全性設備 （接下來會討論） tooprevent 輸出連線 toohello 網際網路從 Azure 虛擬機器。

深入了解 toolearn 強制通道和如何 tooenable，請閱讀 hello 文章[設定強制通道使用 PowerShell 和 Azure 資源管理員](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md)。

## <a name="use-virtual-network-appliances"></a>使用虛擬網路應用裝置
雖然網路安全性群組和使用者定義路由可以提供特定量值在 hello 的網路安全性的網路傳輸層 hello [OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，將要 toobe 情況下，您會想要或需要 tooenable在高 hello 堆疊層級安全性。 在這類情況下，建議您部署 Azure 合作夥伴所提供的虛擬網路安全性應用裝置。

Azure 網路安全性應用裝置可透過網路層級控制項所提供的內容來提供大幅增強的安全性層級。 提供虛擬網路的安全性設備卻 hello 網路安全性功能包括：

* 防火牆
* 入侵偵測/入侵預防
* 弱點管理
* 應用程式控制
* 以網路為基礎的異常偵測
* Web 篩選
* 防毒
* 殭屍網路防護

如果您需要的網路安全性層級高於您可以利用網路層級存取控制項取得的層級，則建議您調查並部署 Azure 虛擬網路安全性應用裝置。

toolearn 有關哪些 Azure 虛擬網路的安全性設備卻可供使用，以及它們的能力，請瀏覽 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) ，並搜尋 「 安全性 」 和 「 網路安全性 」。

## <a name="deploy-dmzs-for-security-zoning"></a>部署 DMZ 進行安全性分區
周邊網路或 「 周邊網路 」 是實體或邏輯網路區段，且為設計 tooprovide 額外的 資產與 hello 網際網路之間的安全性。 hello DMZ hello 目的是 tooplace 特製化網路存取控制裝置 hello hello DMZ 網路的邊緣，以便允許過去 hello 網路安全性裝置，並在您的 Azure 虛擬網路所需的流量。

Dmz 很實用是因為您可以專注於您網路存取控制管理 中，監視、 記錄和報告 hello 裝置 hello Azure 虛擬網路的邊緣。 在此您通常會啟用 DDoS 預防、入侵偵測/入侵預防系統 (IDS/IPS)、防火牆規則和原則、Web 篩選、網路反惡意程式碼等。 hello 網路安全性裝置 hello 網際網路和 Azure 虛擬網路之間的位置，並會在這兩個網路介面。

雖然這是 hello 基本設計的周邊網路時，有許多不同的周邊網路設計，例如背對背式三主目錄，多重主目錄，和其他人。

我們建議您考慮部署 DMZ tooenhance hello 層級的網路安全性，您的 Azure 資源的高安全性部署中所有的。

深入了解 Dmz 和如何 toodeploy 它們在 Azure 中，請閱讀 hello 文章 toolearn [Microsoft 雲端服務和網路安全性](../best-practices-network-security.md)。

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>避免暴露 toohello 網際網路具有專用的 WAN 連結
許多組織已選擇 hello 混合式 IT 的路由。 在混合式 IT 中，其中某些 hello 公司的資訊資產是在 Azure 中，則其他人保持內部部署。 在許多情況下，服務的某些元件會在 Azure 中執行，而其他元件則維持在內部部署上。

在 hello 混合式 IT 案例，通常沒有某種類型的跨單位連線。 這個跨單位連線允許 hello 公司 tooconnect 其內部部署網路 tooAzure 虛擬網路。 可用的跨單位連線解決方案有兩個︰

* 站對站 VPN
* ExpressRoute

[站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) 代表您的內部部署網路和 Azure 虛擬網路之間的虛擬私人連線。 此連接將超過 hello 網際網路和可讓您太 「 通道 」 內加密的連結，您的網路與 Azure 之間的資訊。 站對站 VPN 是安全成熟的技術，各種規模的企業已部署數十年。 使用 [IPsec 通道模式](https://technet.microsoft.com/library/cc786385.aspx)可執行通道加密。

雖然站台對站 VPN 是受信任、 可靠且已建立的技術，hello 通道內的流量並周遊 hello 網際網路。 此外，頻寬是相對較受條件約束的 tooa 最大值為 200Mbps 有關。

如果您需要跨單位連線的例外安全性或效能層級，建議您對跨單位連線使用 Azure ExpressRoute。 ExpressRoute 是內部部署位置或 Exchange 主機服務提供者之間專用的 WAN 連結。 因為這是電信公司連線，您的資料不會通過 hello 網際網路，因此不公開的 toohello 固有的網際網路通訊的潛在風險。

toolearn 深入了解 Azure ExpressRoute 的運作方式以及如何 toodeploy，請閱讀 hello 文章[ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)。

## <a name="optimize-uptime-and-performance"></a>將執行時間和效能最佳化
機密性、 完整性和可用性 (CIA) 由今天的最具影響力的安全性模型的 hello 三角理論所組成。 是加密和隱私權相關的機密性、 完整性是確保資料不會變更未經授權的人員，並確保獲得授權的個人都能 tooaccess hello 資訊他們獲授權的可用性是tooaccess。 上述任何一個區域失敗都代表可能破壞安全性。

可用性可被視為與執行時間和效能有關。 如果服務已關閉，便無法存取資訊。 如果效能是做為 toomake hello 資料無法使用，因此不佳，則我們可以考慮 hello 資料 toobe 無法存取。 因此，從安全性觀點來看，我們需要 toodo 任何我們可以 toomake 確定我們的服務有最佳的執行時間和效能。
受歡迎且有效的方法使用 tooenhance 可用性和效能是 toouse 負載平衡。 負載平衡是將網路流量分散於服務中各伺服器的方法。 例如，如果您有前端網頁伺服器做為服務一部分時，您可以使用負載平衡 toodistribute hello 流量，跨多個前端網頁伺服器。

此分佈的流量會增加可用性，因為其中 hello web 伺服器變成無法使用，如果 hello 負載平衡器將會停止傳送流量 toothat 伺服器以及仍保持線上狀態的重新導向流量 toohello 伺服器。 負載平衡，也有助於效能，因為 hello 處理器、 網路和記憶體額外負荷來服務要求會分散到所有 hello 負載平衡的伺服器。

建議您儘可能為您的服務採用適當的負載平衡。 我們將其適當性 hello 下列各節中。
在 hello Azure 虛擬網路層級，Azure 會提供三個主要的負載平衡選項：

* 以 HTTP 為基礎的負載平衡
* 外部負載平衡
* 內部負載平衡

## <a name="http-based-load-balancing"></a>以 HTTP 為基礎的負載平衡
以 HTTP 為基礎的負載平衡基底來判斷哪些伺服器 toosend 連線使用 hello HTTP 通訊協定的特性。 Azure 有 hello 名稱的應用程式閘道會使用 HTTP 負載平衡器。

建議您在下列情況使用 Azure 應用程式閘道︰

* 需要要求的應用程式從 hello 相同的使用者/用戶端工作階段 tooreach hello 相同後端的虛擬機器。 此情況的範例為：購物車應用程式和網頁郵件伺服器。
* 應用程式想 toofree web 伺服器陣列，從 SSL 終止額外負荷是藉由運用應用程式閘道[SSL 卸載](https://f5.com/glossary/ssl-offloading)功能。
* 應用程式，例如內容傳遞網路，是需要的 hello 長時間執行相同的 TCP 連線 toobe 路由或負載平衡的 toodifferent 後端伺服器上的多個 HTTP 要求。

toolearn 進一步了解 Azure 應用程式閘道的運作方式及如何使用它在您部署中，請閱讀 hello 文章[應用程式閘道概觀](../application-gateway/application-gateway-introduction.md)。

## <a name="external-load-balancing"></a>外部負載平衡
外部負載平衡發生時從 hello 網際網路的連入連線位於 Azure 虛擬網路中伺服器之間平衡負載。 hello Azure 外部負載平衡器可以提供這項功能，而且我們建議您使用它時您不需要 hello 黏性工作階段或 SSL 卸載。

相較之下 tooHTTP 為依據負載平衡，hello 外部負載平衡器會使用 hello 網路傳輸層級 hello OSI 網路模型 toomake 決策哪些伺服器 tooload 平衡連線上的資訊。

我們建議您使用外部負載平衡只要有[無狀態應用程式](http://whatis.techtarget.com/definition/stateless-app)接受來自網際網路的 hello 連入要求。

toolearn 進一步了解 hello Azure 外部負載平衡器的運作方式及部署，請閱讀 hello 文章[開始建立網際網路對向負載平衡器資源管理員 中使用 PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)。

## <a name="internal-load-balancing"></a>內部負載平衡
內部負載平衡非常類似 tooexternal 負載平衡及使用 hello 相同機制 tooload 平衡連線 toohello 伺服器後盾。 hello 只差異是該 hello 負載平衡器在此情況下會接受來自不在 hello 網際網路的虛擬機器的連線。 在大部分情況下，在 Azure 虛擬網路上的裝置起始 hello 連線可接受的負載平衡。

我們建議您使用內部負載平衡的實例將受益於這項功能，例如當您需要 tooload 平衡連線 tooSQL 伺服器或內部的 web 伺服器。

toolearn 進一步了解 Azure 內部的負載平衡的運作方式及部署，請閱讀 hello 文章[開始建立使用 PowerShell 內部負載平衡器](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer)。

## <a name="use-global-load-balancing"></a>使用全域負載平衡
公用雲端運算可讓您 toodeploy 全域分散式元件位於資料中心擁有 hello world 應用程式。 這是在 Microsoft Azure 上可能因 tooAzure 的全域資料中心存在。 相較之下 toohello 負載平衡技術之前所述，全域負載平衡可可能 toomake 服務即使整個資料中心可能會變成無法使用。

您可以利用 [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)在 Azure 中取得這種類型的全域負載平衡。 便可能 tooload 平衡 traffic Manager 可連線 tooyour 服務根據 hello hello 使用者位置。

比方說，如果 hello 使用者正在要求從 hello EU tooyour 服務，hello 連線是位於 EU 資料中心的導向的 tooyour 服務 」。 Traffic Manager 全域負載平衡可協助 tooimprove 效能的這個部分因為連接 toohello 最接近的資料中心的速度比連接 toodatacenters 遠的。

在 hello 可用性方面，全域負載平衡可確保您的服務就可以使用，即使整個資料中心應該變成無法使用。

例如，如果 Azure 資料中心應該變成無法使用 tooenvironmental 原因或到期金額 toooutages （例如區域網路失敗），連線 tooyour 服務將為重新路由到 toohello 最接近的線上資料中心。 運用您可以在流量管理員中建立的 DNS 原則來完成此全域負載平衡。

我們建議您在任何雲端解決方案您開發的多個區域都有四處分散的範圍，而且需要 hello 最高層級的執行時間可能使用 Traffic Manager。

更多有關 Azure Traffic Manager toolearn 和如何 toodeploy，請閱讀 hello 文章[什麼是 Traffic Manager](../traffic-manager/traffic-manager-overview.md)。

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>停用虛擬機器的 RDP/SSH 存取 tooAzure
它是可能 tooreach Azure 虛擬機器使用 hello[遠端桌面通訊協定](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol)(RDP) 和 hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) (SSH) 通訊協定。 這些通訊協定使其可能 toomanage 虛擬機器從遠端位置，且是在資料中心運算的標準。

hello 潛在安全性問題 hello 網際網路上使用這些通訊協定是攻擊者可以使用各種[暴力](https://en.wikipedia.org/wiki/Brute-force_attack)技術 toogain 存取 tooAzure 虛擬機器。 一旦 hello 攻擊者可以存取，他們可以作為您的虛擬機器的啟動點危害您的 Azure 虛擬網路上的其他機器，或甚至攻擊 Azure 外的網路的裝置。

因為這個緣故，我們建議您停用直接 RDP 和 SSH 存取 tooyour Azure 虛擬機器從 hello 網際網路。 從 hello 已停用網際網路存取的直接 RDP 和 SSH 之後，您會有其他選項，您可以使用 tooaccess 這些虛擬機器的遠端管理：

* 點對站 VPN
* 站對站 VPN
* ExpressRoute

[點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) 是遠端存取 VPN 用戶端/伺服器連線的另一種說法。 點對站 VPN 可讓單一使用者 tooconnect tooan Azure 虛擬網路透過 hello 網際網路。 之後建立 hello 點對站連線，hello 使用者將能夠 toouse RDP 或 SSH tooconnect tooany 虛擬機器位於 hello Azure 虛擬網路，hello 使用者連接 toovia 點對站 VPN。 這是假設該 hello 使用者已獲得授權的 tooreach 這些虛擬機器。

點對站 VPN 會比直接 RDP 或 SSH 的連接更安全的因為 hello 使用者 tooauthenticate 兩次之前連接 tooa 虛擬機器。 首先，hello 使用者需求 tooauthenticate （和授權） tooestablish hello 點對站 VPN 連線。第二，hello 使用者需求 tooauthenticate （和授權） tooestablish hello RDP 或 SSH 工作階段。

A[站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)透過 hello 網際網路連線的整個網路 tooanother 網路。 您可以使用站對站 VPN tooconnect 您在內部部署網路 tooan Azure 虛擬網路。 如果您部署的站對站 VPN 時，在內部部署網路上的使用者將能夠 tooconnect toovirtual 機器 Azure 虛擬網路上的使用 hello RDP 或 SSH 通訊協定超過 hello 站對站 VPN 連線，並不需要您 tooallow 直接 RDP 或 SSH透過 hello 網際網路存取。

您也可以使用專用的 WAN 連結 tooprovide 功能類似 toohello 站對站 VPN。 hello 主要差異是 1。 hello 專用的 WAN 連結不會周遊 hello 網際網路和 2。 專用的 WAN 連結通常比較穩定且效能較好。 Azure 會提供專用的 WAN 連結方案中的 hello 表單[ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/)。

## <a name="enable-azure-security-center"></a>啟用 Azure 資訊安全中心
Azure 資訊安全中心可協助您防止、 偵測，並回應 toothreats，，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

Azure 資訊安全中心藉由下列方式來協助您最佳化和監視網路安全性︰

* 提供網路安全性建議
* 監視網路安全性組態的 hello 狀態
* 提醒您 toonetwork 基礎威脅這兩個在 hello 端點和網路層級

強烈建議您在所有的 Azure 部署上啟用 Azure 資訊安全中心。

深入了解 Azure 資訊安全中心，以及如何 tooenable 它為您的部署，請閱讀 hello 文章 toolearn[簡介 tooAzure 資訊安全中心](../security-center/security-center-intro.md)。

## <a name="securely-extend-your-datacenter-into-azure"></a>安全地將資料中心擴充至 Azure
許多企業 IT 組織會想要 tooexpand hello 雲端，而不是增加其內部部署資料中心。 此擴充到 hello 公用雲端代表現有的 IT 基礎結構的擴充功能。 藉由運用跨單位連線選項很可能 tootreat 只是另一個子網路上您內部部署為 Azure 虛擬網路的網路基礎結構。

不過，有很多的規劃，而且需要 toobe 的設計問題解決之後第一個。 這是特別重要 hello 網路安全性區域中。 其中一個最佳方式 toounderstand hello 接近此種設計的方式是 toosee 範例。

Microsoft 已建立 hello[資料中心擴充功能參考架構圖表](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content)以及支援附屬 toohelp 您了解這類的資料中心延伸模組的樣子。 這提供您可以使用 tooplan 並設計安全的企業資料中心延伸 toohello 定域機組的範例參考實作。 我們建議您檢閱此文件 tooget 了解的 hello 的安全解決方案的重要元件。

toolearn 深入了解如何 toosecurely 您資料中心擴充至 Azure，請觀看 hello[擴充資料中心 tooMicrosoft Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA)。
