---
title: "aaaAzure 網路 |Microsoft 文件"
description: "深入了解 Azure 網路服務和功能。"
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Azure 網路

Azure 提供各種不同的網路功能，它們可以合併或分開使用。 按一下任何下列主要功能 toolearn 深入了解它們的 hello:
- [Azure 資源之間的連線](#connectivity): hello 雲端中的安全的私人虛擬網路中的 Azure 連接資源。
- [網際網路連線](#internet-connectivity): hello 網際網路上通訊 tooand 從 Azure 資源。
- [在內部部署連線](#on-premises-connectivity)： 透過 hello 網際網路，透過虛擬私人網路 (VPN) 或透過專用的連接 tooAzure 連線在內部部署網路 tooAzure 資源。
- [負載平衡及流量的方向](#load-balancing)： 在負載平衡流量 tooservers hello 相同的位置和直接流量 tooservers 在不同的位置。
- [安全性](#security)︰篩選網路子網路或個別虛擬機器 (VM) 之間的網路流量。
- [路由](#routing)︰在您的 Azure 和內部部署資源之間使用預設路由或完全控制路由。
- [管理能力](#manageability)︰監視和管理您的 Azure 網路資源。
- [部署和設定工具](#tools)： 使用網頁型入口網站或跨平台命令列工具 toodeploy 並設定網路資源。

## <a name="Connectivity"></a>Azure 資源之間的連線

Azure 資源 (例如虛擬機器、雲端服務、 虛擬機器擴展集和 Azure App Service Environment) 可透過 Azure 虛擬網路 (VNet) 和彼此進行私下通訊。 VNet 是 hello 專用的 Azure 雲端 tooyour 邏輯隔離[訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json)。 您可以在每個 Azure 訂用帳戶和 Azure [區域](https://azure.microsoft.com/regions)內實作多個 VNet。 每個 VNet 會與其他 VNet 隔離。 對於每個 VNet，您可以︰

- 使用公用和私人 (RFC 1918) 位址指定自訂私人 IP 位址空間。 Azure 資源連接的 toohello VNet 私人 IP 位址會從指派 hello 您指派的位址空間。
- 區段 hello VNet 到一個或多個子網路，並配置 hello VNet 位址空間 tooeach 子網路的一部分。
- 使用 Azure 提供名稱解析，或指定您自己的 DNS 伺服器以供資源連接 tooa VNet。

深入了解 hello Azure 虛擬網路服務，讀取 hello toolearn[虛擬網路概觀](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。 您可以連接的 Vnet tooeach 其他，啟用資源彼此連接 tooeither VNet toocommunicate 跨 Vnet。 您可以使用一個或兩個下列選項 tooconnect Vnet tooeach 其他 hello:

- **對等互連：**可讓資源連線 toodifferent Azure Vnet 內 hello 相同 Azure 地區 toocommunicate 彼此。 hello 頻寬和延遲在 hello Vnet 是 hello 相同好像 hello 資源連線的 toohello 相同的 VNet。 深入了解對等互連，toolearn 讀取 hello[虛擬網路對等互連概觀](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **VPN 閘道：**啟用資源彼此連線中不同的 Azure 地區 toocommunicate toodifferent Azure Vnet。 VNet 之間的流量流經 Azure VPN 閘道。 Vnet 之間的頻寬是有限的 toohello 頻寬 hello 閘道。 深入了解 Vnet 連接 VPN 閘道，讀取 hello toolearn[跨區域設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

## <a name="internet-connectivity"></a>網際網路連線

所有 Azure 資源連接的 tooa VNet 有預設的傳出連線 toohello 網際網路。 hello 資源的 hello 私用 IP 位址是來源網路位址轉譯 (SNAT) tooa 公用 IP 位址的 hello Azure 基礎結構。 深入了解輸出的網際網路連線，讀取 hello toolearn[了解 Azure 中的輸出連線](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

toocommunicate 輸入網際網路而不需要 SNAT，資源必須指派的公用 IP 位址的 hello 網際網路或 toocommunicate 輸出的 toohello tooAzure 資源。 更多關於公用 IP 位址，讀取 hello toolearn[公用 IP 位址](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

## <a name="on-premises-connectivity"></a>內部部署連線

您可以透過 VPN 連線或直接的私人連線，在您的 VNet 中安全地存取資源。 toosend Azure 虛擬網路與內部部署網路之間的網路流量，您必須建立虛擬網路閘道。 您設定的連線，VPN 或 ExpressRoute hello 閘道 toocreate hello 類型的設定。

您可以連接您在內部部署網路 tooa VNet hello 下列選項的任意組合：

**點對站 (透過 SSTP 的 VPN)**

hello 下列圖片顯示多部電腦與 VNet 之間的不同點 toosite 連線：

![點對站](./media/networking-overview/point-to-site.png)

在單一電腦與 VNet 之間會建立此連線。 這種連接類型是如果您剛開始使用 Azure 或開發人員，很好的因為您需要少量或沒有變更 tooyour 現有的網路。 這也是從會議或住家等遠端位置連線時的便利方式。 點對站連線通常搭配 hello 透過站對站連線相同的虛擬網路閘道。 hello 連線會使用透過 hello 網際網路 hello 電腦與 hello VNet 之間 hello SSTP 通訊協定 tooprovide 加密通訊。 點對站 VPN 的 hello 延遲是無法預測的因為 hello 流量會周遊 hello 網際網路。

**站對站 (IPsec/IKE VPN 通道)**

![網站間](./media/networking-overview/site-to-site.png)

內部部署的 VPN 裝置與 Azure VPN 閘道之間會建立此連線。 這種連接類型可讓您授權 tooaccess hello VNet 任何內部部署資源。 hello 連接是透過 hello 網際網路在內部部署裝置與 hello Azure VPN 閘道之間提供加密的通訊的 IPSec/IKE VPN。 您可以連接多個內部部署站台 toohello 相同的 VPN 閘道。 hello 內部部署 VPN 裝置會在每個站台必須執行對外公用 IP 位址不是 NAT 後方。 站對站連線的 hello 延遲是無法預測的因為 hello 流量會周遊 hello 網際網路。

**ExpressRoute (專用的私人連線)**

![ExpressRoute](./media/networking-overview/expressroute.png)

您的網路與 Azure 之間會透過 ExpressRoute 合作夥伴建立此類型的連線。 此連線是私人連線。 流量不會周遊 hello 網際網路。 ExpressRoute 連線的 hello 延遲是可預測，，因為流量不會周遊 hello 網際網路。 ExpressRoute 可以結合站對站連線。

深入了解所有 hello 先前連線的選項，讀取 hello toolearn[連線拓撲圖表](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

## <a name="load-balancing"></a>負載平衡和流量方向

Microsoft Azure 提供多個服務，可管理分配網路流量和負載平衡的方式。 您可以使用任何 hello 單獨或一起下列功能：

**DNS 負載平衡**

hello Azure 流量管理員服務提供通用 DNS 負載平衡。 Traffic Manager 會回應 tooclients hello IP 位址設為狀況良好的端點，並根據 hello 下列路由方式的其中一個：
- **地理：**的用戶端導向 toospecific 端點 (Azure、 外部或巢狀) 會根據其 DNS 查詢是來自哪一個地理位置上。 在必須知道用戶端所在的地理區域並根據此位置進行路由的情況下，適合採取此方式。 例如，遵守資料主權規定、內容和使用者經驗的當地語系化，以及測量來自不同區域的流量。
- **效能：** hello IP 位址傳回 toohello 用戶端是 hello 「 最靠近 」 toohello 用戶端。 hello '靠近' 的端點不一定是最接近地理距離的測量。 相反地，這個方法會判斷 hello 最靠近的端點，藉由測量網路延遲。 Traffic Manager 會維護網際網路延遲表格 tootrack hello 來回時間 IP 位址範圍與每個 Azure 資料中心之間。
- **優先順序：**流量會導向的 toohello 主要 （最高優先權） 端點。 如果 hello 主要端點無法使用，Traffic Manager 路由 hello 流量 toohello 第二個端點。 如果無法使用這兩個 hello 主要和次要端點，則 hello 流量會傳送 toohello，第三個，依此類推。 Hello 端點的可用性會根據設定 hello 狀態 （啟用或停用） 和 hello 持續的端點監視。
- **加權循環配置資源：**針對每個要求，流量管理員會隨機選擇可用的端點。 選擇端點的 hello 機率根據 hello 權重 tooall 可用的端點。 相同加權跨甚至流量發佈中的所有端點結果使用 hello。 在特定端點上使用高或較低的加權值會導致傳回頻率 hello DNS 回應中的這些端點 toobe。

hello 下列圖片顯示 web 應用程式導向 tooa Web 應用程式端點的要求。 端點也可以是其他 Azure 服務，例如 VM 和雲端服務。

![流量管理員](./media/networking-overview/traffic-manager.png)

hello 用戶端會直接連接 toothat 端點。 Azure Traffic Manager 會偵測端點會處於狀況不良，然後重新導向用戶端 tooa 不同的狀況良好端點。 更多關於流量管理員 中，讀取 hello toolearn [Azure Traffic Manager 概觀](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

**應用程式負載平衡**

hello Azure 應用程式閘道服務做為服務提供應用程式傳遞控制站 (ADC)。 應用程式閘道提供各種層 7 (HTTP/HTTPS) 負載平衡功能對於您的應用程式，包括 web 應用程式防火牆 tooprotect 入侵的弱點可能會與 web 應用程式。 應用程式閘道也可讓您 toooptimize web 伺服陣列產能卸載 CPU 運算密集 SSL 終止 toohello 應用程式閘道。 

其他 7 層路由功能包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 背後的單一應用程式閘道的多個網站。 應用程式閘道可以設定為連結網際網路的閘道、內部專用閘道或兩者混合。 應用程式閘道完全由 Azure 管理、可調整且可用性極高。 它提供一組豐富的診斷和記錄功能，很好管理。 深入了解應用程式閘道，讀取 hello toolearn[應用程式閘道概觀](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

hello 下圖顯示的 URL 路徑為基礎的路由與應用程式閘道：

![應用程式閘道](./media/networking-overview/application-gateway.png)

**網路負載平衡**

hello Azure 負載平衡器提供高效能、 低延遲第 4 層負載平衡所有 UDP 和 TCP 通訊協定。 它會管理輸入及輸出連線。 您可以設定公用和內部負載平衡端點。 您可以定義規則 toomap 輸入連線 tooback 後端集區目的地使用 TCP 和 HTTP 健全狀況探查選項 toomanage 服務可用性。 深入了解負載平衡器，讀取 hello toolearn[負載平衡器概觀](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

hello 下列圖片顯示網際網路對向多層式應用程式，它會利用這兩個外部和內部負載平衡器：

![負載平衡器](./media/networking-overview/load-balancer.png)

## <a name="security"></a>安全性

您可以篩選從 Azure 資源，使用下列選項的 hello 流量 tooand:

- **網路：**您可以實作 Azure 網路的安全性群組 (Nsg) toofilter 傳入和傳出流量 tooAzure 資源。 每個 NSG 可包含一或多個輸入和輸出規則。 每個規則指定 hello 來源 IP 位址、 目的地 IP 位址、 連接埠和通訊協定流量的篩選。 Nsg 可以套用的 tooindividual 子網路和個別的 Vm。 深入了解 Nsg，讀取 hello toolearn[網路安全性群組概觀](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **應用程式︰**同時使用應用程式閘道和 Web 應用程式防火牆，可保護您的應用程式以防範漏洞和攻擊。 常見的範例包括 SQL 插入式攻擊、跨網站指令碼和格式不正確的標頭。 應用程式閘道會篩選掉此流量，使它無法到達您的 Web 伺服器。 您都可以 tooconfigure 您想要啟用哪些規則。 hello 能力 tooconfigure SSL 交涉原則會提供 tooallow 特定原則 toobe 停用。 深入了解 hello web 應用程式防火牆讀取 hello toolearn [Web 應用程式防火牆](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

如果您需要 Azure 不提供，或想 toouse 網路應用程式使用內部部署的網路功能，可以實作在 Vm 中的 hello 產品，並將它們連接 tooyour VNet。 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)包含數個不同的 Vm 網路應用程式，您可以使用預先設定。 這些預先設定的 Vm 是通常參照的 tooas 網路虛擬裝置 (NVA)。 NVA 已搭載防火牆和 WAN 最佳化等應用程式。

## <a name="routing"></a>路由

Azure 會建立預設啟用在彼此任何 VNet toocommunicate 資源連線的 tooany 子網路的路由表。 您可以實作，或這兩個下列類型的路由 toooverride hello hello Azure 建立的預設路由：
- **使用者定義：**您可以建立自訂的路由表控制流量所在 toofor 路由的路由與每個子網路。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **邊界閘道通訊協定 (BGP):**如果您使用 Azure VPN 閘道或 ExpressRoute 連接的 VNet tooyour 在內部部署網路連接，您可以將傳播 BGP 路由 tooyour Vnet。 BGP 是 hello 標準路由通訊協定常用 hello 網際網路 tooexchange 路由和連線資訊中兩個或多個網路之間。 使用 Azure 虛擬網路，BGP 啟用 hello Azure VPN 閘道與內部部署 VPN 裝置 hello 內容中時呼叫的 BGP 對等或鄰近項目，tooexchange 「 路由 」 通知 hello 可用性和這些前置詞的連線兩個閘道透過 hello 閘道或路由器涉及的 toogo。 BGP 也可以啟用傳輸多個網路之間路由傳播路由的 BGP 閘道會從一個 BGP 對等 tooall 學習其他 BGP 對等節點。 toolearn 深入了解 BGP，請參閱 hello [BGP 與 Azure VPN 閘道概觀](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

## <a name="manageability"></a>可管理性

Azure 提供 hello 下列工具 toomonitor 和管理網路功能：
- **活動記錄：**所有 Azure 資源有提供作業資訊的活動記錄檔位置，就會有作業的狀態，以及起始 hello 作業的使用者。 深入了解活動記錄檔讀取 hello toolearn[活動記錄概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **診斷記錄檔：**周期和即時事件所建立的網路資源和登入 Azure 儲存體帳戶、 傳送 tooan Azure 事件中心，或傳送 tooAzure 記錄分析。 診斷記錄檔提供深入了解 toohello 健全狀況的資源。 負載平衡器 (網際網路對向)、網路安全性群組、路由和應用程式閘道均提供診斷記錄。 深入了解診斷記錄檔，讀取 hello toolearn[診斷記錄檔概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **計量：**計量是在一段時間內所收集到關於資源的效能測量數據和計數器。 度量可以是使用的 tootrigger 警示根據臨界值。 目前有針對應用程式閘道的計量。 深入了解度量，讀取 hello toolearn[度量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **疑難排解：**有直接在 hello Azure 入口網站中存取疑難排解資訊。 hello 資訊可協助診斷 ExpressRoute、 與 VPN 閘道，應用程式閘道、 網路安全性記錄檔、 路由、 DNS、 負載平衡器，Traffic Manager 的常見問題。
- **角色型存取控制 (RBAC)：**使用角色型存取控制 (RBAC)，控制誰可以建立和管理網路資源。 深入了解 RBAC 閱讀 hello[開始使用 RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。 
- **封包擷取：** hello 服務會提供 Azure 網路監看員 hello 能力 toorun 透過內 hello VM 擴充功能的 VM 的封包擷取。 Linux 和 Windows VM 均提供此功能。 深入了解讀取 hello 的封包擷取 toolearn[封包擷取概觀](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **請確認 IP 流量：**網路監看員可讓您的 Azure VM 之間的遠端資源 toodetermine tooverify IP 流量是否允許或拒絕封包。 這項功能提供的系統管理員 hello 能力 tooquickly 診斷連線問題。 深入了解 tooverify IP 流動的方式，toolearn 讀取 hello [IP 流量確認概觀](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **VPN 連線問題疑難排解：** hello VPN 網路監看員的疑難排解功能提供 hello 能力 tooquery 連接或閘道，並確認 hello hello 資源健全狀況。 更多關於疑難排解 VPN 連線，讀取 hello toolearn [VPN 連接的疑難排解概觀](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **檢視網路拓樸：**檢視網路監看員的 VNet 中的 hello 網路資源的圖形表示法。 深入了解檢視網路拓撲，讀取 hello toolearn[拓撲概觀](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。

## <a name="tools"></a>部署和設定工具

您可以使用部署和設定 Azure 網路功能資源任何 hello 下列工具：

- **Azure 入口網站︰**在瀏覽器中執行的圖形化使用者介面。 開啟 hello [Azure 入口網站](http://portal.azure.com)。
- **Azure PowerShell：**從 Windows 電腦管理 Azure 的命令列工具。 進一步了解 Azure PowerShell 讀取 hello [Azure PowerShell 概觀](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **Azure 命令列介面 (CLI)：**從 Linux、macOS 或 Windows 電腦管理 Azure 的命令列工具。 深入了解所讀取的 hello hello Azure CLI [Azure CLI 概觀](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- **Azure 資源管理員範本：**定義 hello 基礎結構和設定 Azure 解決方案中的檔案 （以 JSON 格式）。 透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。 深入了解撰寫範本，讀取 hello toolearn[建立範本的最佳做法](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。 您可以部署範本，以 hello Azure 入口網站，CLI 或 PowerShell。 tooget 立即，開始使用範本將部署其中一種 hello 許多預先設定的範本在 hello [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/?term=network)程式庫。 

## <a name="pricing"></a>價格

部分的 hello Azure 網路服務有一筆費用，有些則是可用。 檢視 hello[虛擬網路](https://azure.microsoft.com/pricing/details/virtual-network)， [VPN 閘道](https://azure.microsoft.com/pricing/details/vpn-gateway)，[應用程式閘道](https://azure.microsoft.com/en-us/pricing/details/application-gateway/)，[負載平衡器](https://azure.microsoft.com/pricing/details/load-balancer)， [網路監看員](https://azure.microsoft.com/pricing/details/network-watcher)， [DNS](https://azure.microsoft.com/pricing/details/dns)， [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager)和[ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute)定價的詳細資訊的頁面。

## <a name="next-steps"></a>後續步驟

- 建立第一個 VNet 和 hello hello 中的步驟，以連接少數的 Vm tooit[建立第一個虛擬網路](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- Hello hello 中的步驟，以連接您的電腦 tooa VNet[設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
- 負載平衡網際網路流量 toopublic 伺服器 hello 中的 hello 步驟[建立網際網路對向負載平衡器](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json)發行項。
