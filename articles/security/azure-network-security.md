---
title: "網路安全性 aaaAzure |Microsoft 文件"
description: "深入了解雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可以自動 toomeet hello 需求的應用程式或企業上下調整的服務。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Azure 網路安全性

我們知道安全性是 hello 定域機組中的其中一個工作，而且重要，您會看到 Azure 安全性的精確且即時資訊。 Tootake 利用 Azure 的各種安全性工具和功能的其中一個 hello 最佳原因 toouse Azure 應用程式與服務。 這些工具和功能可協助使其可能 toocreate 安全解決方案在 hello Azure 平台上。

Microsoft Azure 提供客戶資料的機密性、完整性和可用性，同時也能釐清責任。 toohelp 您進一步了解 hello 控制項集合的網路安全性在 Microsoft Azure 內實作從 hello 客戶的觀點來看，本文中，「 Azure 網路安全性 」 寫入 tooprovide hello 網路安全性查看全方位使用 Microsoft Azure 中可用的控制項。

本文的適用 tooinform 您有關 hello 各種不同的網路控制，您可以在 Azure 中設定的部署的 hello 解決方案 tooenhance hello 安全性。 如果您想要在 Microsoft 中沒有 toosecure hello 網路網狀架構的 hello Azure 平台本身，請參閱 hello Azure 的安全性 > 一節中 hello [Microsoft 信任中心](https://www.microsoft.com/trustcenter/security/azure-security)。

## <a name="azure-platform"></a>Azure 平台

Azure 是一個公用雲端服務平台，支援廣泛的作業系統、程式設計語言、架構、工具、資料庫及裝置等選擇。  它可以透過 Docker 整合執行 Linux 容器；使用 JavaScript、Python、.NET、PHP、Java 及 Node.js 建置應用程式；為 iOS、Android 及 Windows 裝置建置後端。 Azure 雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您建置，或 IT 資產移轉至公用雲端服務提供者、 您依賴該組織的能力 tooprotect 應用程式和資料與 hello 服務 」 和 「 hello 」 控制項提供您雲端架構的 toomanage hello 安全性資產。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供可設定的安全性選項和 hello 能力 toocontrol 的廣泛集合它們可讓您可以自訂的組織部署的安全性 toomeet hello 獨特需求。

## <a name="abstract"></a>摘要

Microsoft 公用雲端服務提供超大規模的服務和基礎結構、企業級的功能，以及許多混合式連線選項。 您可以選擇 tooaccess 透過 hello 網際網路或 Azure ExpressRoute，後者提供私人網路連線與這些服務。 hello Microsoft Azure 平台可讓您 tooseamlessly 將您的基礎結構延伸至 hello 雲端並建立多層式架構。 另外，協力廠商可以提供安全性服務和虛擬設備，以啟用增強的功能。

Azure 的網路服務設計可將彈性、可用性、復原、安全性和完整性最大化。 這份技術白皮書提供的 Azure hello 網路功能的詳細資訊以及有關客戶如何使用 Azure 的原生安全性功能 toohelp 保護他們的資訊資產。

hello 適用於本白皮書的對象包括：

- 尋求 Azure 中可用和支援安全性解決方案的技術管理員、網路管理員和開發人員。

-   Sme 或想 tooget 的高階概觀的商務程序主管 hello Azure 網路技術和服務的相關討論 hello Azure 公用雲端中的網路安全性中。

## <a name="azure-networking-big-picture"></a>Azure 網路服務概觀
Microsoft Azure 包括強固的網路基礎結構 toosupport 應用程式和服務連線需求。 在 Azure 中，位於內部部署之間的資源之間的網路連線可與 Azure 託管資源和 tooand 從 hello 網際網路和 Azure。

![Azure 網路服務概觀](media/azure-network-security/azure-network-security-fig-1.png)

hello [Azure 網路基礎結構](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines)可讓您 toosecurely 連接的 Azure 資源 tooeach 其他與虛擬網路 (Vnet)。 VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是隔離的邏輯 hello Azure 雲端專用的網路 tooyour 訂用帳戶。 您可以連接的 Vnet tooyour 在內部部署網路。

Azure 支援專用 WAN 連結連線 tooyour 在內部部署網路和 Azure 虛擬網路與[ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)。 hello Azure 與您的站台之間的連結使用專用的連接，不會通過 hello 公用網際網路。 如果多個資料中心中執行 Azure 應用程式，您可以使用[Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute 以聰明的方式跨 hello 應用程式的執行個體的使用者要求。 您也可以路由傳送流量 tooservices 不在 Azure 中執行時可從 hello 網際網路存取。

## <a name="enterprise-view-of-azure-networking-components"></a>Azure 網路元件的企業觀點
Azure 有許多相關 toonetwork 安全性的討論區的網路元件。 我們將描述這些網路功能元件，並專注於 hello 安全性問題的相關的 toothem。

> [!Note]
> 並非所有 Azure 網路方面詳述 – 我們討論只包括在中規劃和設計安全的網路基礎結構服務和您在 Azure 中部署的應用程式周圍考慮 toobe 關鍵。

本文中會涵蓋 hello 遵循 Azure 網路的企業功能：

-   基本網路連線

-   混合式連線

-   安全性控制

-   網路驗證

### <a name="basic-network-connectivity"></a>基本網路連線

hello [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)服務可讓您 toosecurely 連接的 Azure 資源 tooeach 其他虛擬網路 (VNet)。 VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是隔離的邏輯 hello Azure 網路基礎結構專用 tooyour 訂用帳戶。 您也可以連接的 Vnet tooeach 其他和 tooyour 在內部部署網路使用站對站 Vpn 和專用[WAN 連結](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)。

![基本網路連線](media/azure-network-security/azure-network-security-fig-2.png)

以了解您在 Azure 中使用 Vm toohost 伺服器 hello，hello 問題是，這些 Vm tooa 網路的連線方式。 hello 解決辦法就是 Vm 連接 tooan [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)。

Azure 虛擬網路 」 就像 hello 虛擬網路，您使用您自己的虛擬化平台解決方案，例如 Microsoft HYPER-V 或 VMware 在內部部署。

#### <a name="intra-vnet-connectivity"></a>VNet 內部連線

您可以連接的 Vnet tooeach 其他，啟用資源彼此連接 tooeither VNet toocommunicate 跨 Vnet。 您可以使用一個或兩個下列選項 tooconnect Vnet tooeach 其他 hello:

- **對等互連：**可讓資源連線 toodifferent Azure Vnet hello 內相同的 Azure 位置 toocommunicate 彼此。 hello 頻寬和延遲在 hello VNet 是 hello 相同好像 hello 資源連線的 toohello 相同的 VNet。 深入了解對等互連，toolearn 讀取[虛擬網路對等互連](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)。

 ![對等互連](media/azure-network-security/azure-network-security-fig-3.png)

- **VNet 對 VNet 連線：**可讓資源連線 toodifferent Azure VNet 內 hello 相同，或不同的 Azure 位置。 不同於對等互連，VNet 之間的頻寬有限，因為流量必須通過 Azure VPN 閘道。

![VNet 對 VNet 連線](media/azure-network-security/azure-network-security-fig-4.png)


深入了解 Vnet 連線 VNet 對 VNet 連線後，讀取 hello toolearn[設定 VNet 對 VNet 連線文章](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json)。

#### <a name="azure-virtual-network-capabilities"></a>Azure 虛擬網路功能：

如您所見，Azure 虛擬網路會提供虛擬機器 tooconnect toohello 網路，使其可以連線安全的方式 tooother 網路資源。 不過，基本連線能力是只 hello 開頭。 hello hello Azure 虛擬網路服務的下列功能會公開 hello Azure 虛擬網路之安全性特性：

-   隔離

-   網際網路連線

-   Azure 資源連線

-   VNet 連線

-   內部部署連線能力

-   流量篩選

-   路由

**隔離**

VNet 會彼此[隔離](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)。 您可以建立個別的開發、 測試和生產環境使用 hello 相同的 Vnet [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)位址區塊。 相反地，您可以建立多個使用不同 CIDR 位址區塊的 VNet 並將這些網路連接在一起。 您可以將 VNet 分成多個子網路。

Azure 提供的 Vm 的內部名稱解析和[雲端服務](https://azure.microsoft.com/services/cloud-services/)角色執行個體連接 tooa VNet。 您可以選擇性地設定 VNet toouse 您自己的 DNS 伺服器，而不是使用 Azure 的內部名稱解析。

您可以在每個 Azure [訂用帳戶](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json)和 Azure [區域](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json)內實作多個 VNet。 每個 VNet 會與其他 VNet 隔離。 對於每個 VNet，您可以︰

-   使用公用和私人 (RFC 1918) 位址指定自訂私人 IP 位址空間。 Azure 會將資源連接的 toohello VNet 私人 IP 位址指派從 hello 位址空間，您指派。

-   區段 hello VNet 到一個或多個子網路，並配置 hello VNet 位址空間 tooeach 子網路的一部分。

-   使用 Azure 提供名稱解析，或指定您自己的 DNS 伺服器以供資源連接 tooa VNet。 深入了解讀取 hello 的 Vnet 中的名稱解析 toolearn [Vm 和雲端服務的名稱解析](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances)。

**網際網路連線**

所有[Azure 虛擬機器 (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/)和雲端服務角色執行個體連接的 tooa VNet 已存取 toohello 網際網路，根據預設。 視需要您也可以啟用輸入的存取 toospecific 資源。(VM) 和雲端服務角色執行個體連接的 tooa VNet 已存取 toohello 網際網路，根據預設。 視需要您也可以啟用輸入的存取 toospecific 資源。

所有資源連線的 tooa VNet 都有預設的傳出連線 toohello 網際網路。 hello 資源的 hello 私用 IP 位址是來源網路位址轉譯 (SNAT) tooa 公用 IP 位址的 hello Azure 基礎結構。 您可以透過實作自訂路由和流量篩選變更 hello 預設連線。 深入了解輸出的網際網路連線，讀取 hello toolearn[了解 Azure 中的輸出連線](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json)。

toocommunicate 輸入網際網路而不需要 SNAT，資源必須指派的公用 IP 位址的 hello 網際網路或 toocommunicate 輸出的 toohello tooAzure 資源。 更多關於公用 IP 位址，讀取 hello toolearn[公用 IP 位址](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address)。

**Azure 資源連線能力**

[Azure 資源](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)為雲端服務和 Vm 可以連接的 toohello 相同的 VNet。 hello 資源可以連接 tooeach 其他使用私人 IP 位址，即使它們位於不同子網路。 Azure 預設之間提供路由子網路、 Vnet，與在內部部署網路，因此您不需要 tooconfigure，管理路由。

您可以連接數個 Azure 資源 tooa VNet，例如虛擬機器 (VM)、 雲端服務、 應用程式服務環境和虛擬機器規模集。 Vm 連接 tooa VNet 中的子網路的網路介面 (NIC)。 深入了解 Nic，讀取 hello toolearn[網路介面](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface)。

**VNet 連線能力**

[Vnet](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)可以是連線的 tooeach 其他，讓資源連線 tooany VNet toocommunicate 與任何其他 VNet 上的任何資源。

您可以連接的 Vnet tooeach 其他，啟用資源彼此連接 tooeither VNet toocommunicate 跨 Vnet。 您可以使用一個或兩個下列選項 tooconnect Vnet tooeach 其他 hello:

- **對等互連：**可讓資源連線 toodifferent Azure Vnet hello 內相同的 Azure 位置 toocommunicate 彼此。 hello 頻寬和延遲 hello Vnet 是 hello 與相同連接的 toohello hello 資源一樣在相同 VNet.toolearn 深入了解對等互連，讀取 hello[虛擬網路對等互連](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)。

- **VNet 對 VNet 連線：**可讓資源連線 toodifferent Azure VNet 內 hello 相同，或不同的 Azure 位置。 不同於對等互連，VNet 之間的頻寬有限，因為流量必須通過 Azure VPN 閘道。 toolearn 深入了解 Vnet 連線 VNet 對 VNet 連線。 toolearn 詳細資訊，讀取 hello[設定 VNet 對 VNet 連線](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json)。

**內部部署連線能力**

可以連接的 Vnet 太[內部](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)透過網路與 Azure 之間的私人網路連線或透過站對站 VPN 連線透過網際網路 hello 網路。

您可以連接您在內部部署網路 tooa VNet hello 下列選項的任意組合：

- **點對站虛擬私人網路 (VPN):**單一的電腦已連線的 tooyour 網路與 hello VNet 之間建立。 這種連接類型是如果您剛開始使用 Azure 或開發人員，很好的因為您需要少量或沒有變更 tooyour 現有的網路。 hello 連線會使用透過 hello 網際網路 hello PC 與 hello VNet 之間 hello SSTP 通訊協定 tooprovide 加密通訊。 因為 hello 流量會周遊 hello 網際網路，則無法預測的點對站 vpn 的 hello 延遲。

- **站對站 VPN：**建立於 VPN 裝置與 Azure VPN 閘道之間。 這種連接類型可讓您授權 tooaccess VNet 任何內部部署資源。 hello 連接是透過 hello 網際網路在內部部署裝置與 hello Azure VPN 閘道之間提供加密的通訊的 IPsec/IKE VPN。 因為 hello 流量會周遊 hello 網際網路，則無法預測 hello 站對站連線的延遲。

- **Azure ExpressRoute：**透過 ExpressRoute 合作夥伴，建立於您的網路與 Azure 之間。 此連線是私人連線。 流量不會周遊 hello 網際網路。 ExpressRoute 連線的 hello 延遲是可預測的因為流量不會周遊 hello 網際網路。 深入了解所有 hello 先前連線的選項，讀取 hello toolearn[連線拓撲圖表](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json)。

**流量篩選**

可以依照來源 IP 位址和連接埠、目的地 IP 位址和連接埠以及通訊協定，對 VM 和雲端服務角色執行個體[網路流量](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)進行輸入及輸出的篩選。

您可以篩選使用 hello 下列選項之一或兩者的子網路之間的網路流量：

- **網路安全性群組 (NSG):**每個 NSG 可以包含多個傳入和傳出的安全性規則可讓您依來源和目的地 IP 位址、 連接埠和通訊協定的 toofilter 流量。 您可以套用 NSG tooeach NIC 的 VM 中。 您也可以套用 NSG toohello 子網路的 NIC，或其他 Azure 資源，連線到。 深入了解 Nsg，讀取 hello toolearn[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)。

- **虛擬網路設備：**虛擬網路設備是執行軟體的 VM，該軟體可執行網路功能 (例如防火牆)。 Hello Azure Marketplace 中檢視可用 NVAs 的清單。 此外，也可取得提供 WAN 最佳化和其他網路流量功能的 NVA。 NVA 通常使用於使用者定義或 BGP 路由。 您也可以使用 Vnet 之間 NVA toofilter 流量。

**路由**

您可以透過設定自己的路由，或使用透過網路閘道的 BGP 路由，選擇性地覆寫 Azure 的預設路由。

Azure 會建立可讓資源連線的 tooany 子網路中任何 VNet toocommunicate 彼此，預設路由表。 您可以實作，或這兩個下列選項 toooverride hello hello Azure 建立的預設路由：

- **使用者定義的路由：**您可以建立自訂的路由表控制流量所在 toofor 路由的路由與每個子網路。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)。

- **BGP 路由：**如果您使用 Azure VPN 閘道或 ExpressRoute 連接的 VNet tooyour 在內部部署網路連接，您可以將傳播 BGP 路由 tooyour Vnet。

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>混合式網際網路連線： tooan 在內部部署網路連線
您可以連接您在內部部署網路 tooa VNet hello 下列選項的任意組合：

-   網際網路連線

-   點對站 VPN (P2S VPN)

-   站對站 VPN (S2S VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>網際網路連線

如其名所示，網際網路連線將您的工作負載可從 hello 網際網路，讓您公開不同的公用端點 tooworkloads 留存 hello 虛擬網路。 這些工作負載可以使用公開[網際網路對向負載平衡器](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)或直接指派公用 IP 位址 toohello VM。 如此一來，它就可能會對任何項目上 hello 網際網路 toobe 無法 tooreach 該虛擬機器，提供主機防火牆後面，[網路安全性群組 (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)，和[使用者定義的路由](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)是否允許toohappen。

在此案例中，可以公開 （expose） 需要 toobe 公用 toohello 網際網路的應用程式，是無法 tooconnect tooit 從任何位置，或從特定位置視您的工作負載的 hello 組態而定。

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>點對站 VPN 或站對站 VPN
這些兩個落入 hello 相同類別目錄。 它們都需要您的 VNet toohave VPN 閘道，而且您可以連接 VPN 用戶端用於您的工作站，一部分 hello tooit[點對站組態](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)或者您可以設定在內部[部署VPN裝置](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe 無法 tooterminate 站對站 VPN。 如此一來，在內部部署裝置可以連線 tooresources hello VNet 內。

點對站 (P2S) 設定可讓您建立的安全連線從個別的用戶端電腦 tooa 虛擬網路。 P2S 是透過 SSTP (安全通訊端通道通訊協定) 的 VPN 連線。

![點對站 VPN](media/azure-network-security/azure-network-security-fig-5.png)

當您想 tooconnect tooyour VNet 從遠端位置，例如從家裡或會議中心，或是當您只有一些需要 tooconnect tooa 虛擬網路的用戶端時，適合使用點對站連線。

P2S 連線不需要 VPN 裝置或公眾對應 IP 位址即可運作。 您建立從 hello 用戶端電腦的 hello VPN 連線。 因此，P2S 不建議的方式 tooconnect tooAzure 以防您需要從許多在內部部署裝置和電腦 tooyour Azure 網路的持續連線。

![站對站 VPN](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> 如需有關點對站連線的詳細資訊，請參閱 hello[點對站 FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal)。

站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。

這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。 此連接將超過 hello 網際網路和可讓您太 「 通道 」 內加密的連結，您的網路與 Azure 之間的資訊。 站對站 VPN 是安全成熟的技術，各種規模的企業已部署數十年。 使用 [IPsec 通道模式](https://technet.microsoft.com/library/cc786385.aspx)可執行通道加密。

雖然站台對站 VPN 是受信任、 可靠且已建立的技術，hello 通道內的流量並周遊 hello 網際網路。 此外，頻寬是相對較受條件約束的 tooa 最大值 200 Mbps。

如果您需要跨單位連線的例外安全性或效能層級，建議您對跨單位連線使用 Azure ExpressRoute。 ExpressRoute 是內部部署位置或 Exchange 主機服務提供者之間專用的 WAN 連結。 因為這是電信公司連線，您的資料不會通過 hello 網際網路，因此不公開的 toohello 固有的網際網路通訊的潛在風險。

> [!Note]
> 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways)。

#### <a name="dedicated-wan-link"></a>專用的 WAN 連結
Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至透過專用私人連接透過連線服務提供者來實現 hello Azure。

ExpressRoute 連線不會經過 hello 公用網際網路。 這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。

![ 專用的 WAN 連結](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> 如需詳細資訊 tooconnect 使用 ExpressRoute，您網路 tooMicrosoft 看到[ExpressRoute 的連線模型](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways)和[ExpressRoute 技術概觀](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)。

做為 hello 站對站 VPN 選項 ExpressRoute 也可讓您不一定只有一個 VNet 的 tooconnect tooresources。 事實上，根據 hello SKU，您可以連接 too10 Vnet。 如果您擁有 hello [premium add-on](https://docs.microsoft.com/azure/expressroute/expressroute-faqs)，連線 tooup too100 Vnet 都有可能，根據頻寬。 深入了解喜歡哪一點這些類型的連接查詢，讀取 toolearn[連線拓撲圖表](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json)。

### <a name="security-controls"></a>安全性控制
Azure 虛擬網路可提供與其他虛擬網路隔離的安全、邏輯網路，並支援您在內部部署網路上使用的許多安全性控制。 客戶建立自己的結構，使用： 子網路，他們使用他們自己的私人 IP 位址範圍、 設定路由表、 網路安全性群組，存取控制清單 (Acl)、 閘道和虛擬應用裝置 toorun 其 hello 雲端中的工作負載。

hello 以下是您可以使用您的 Azure 虛擬網路的安全性控制：

-   網路存取控制

-   使用者定義的路由

-   網路安全性設備

-   應用程式閘道

-   Azure Web 應用程式防火牆

-   網路可用性控制

#### <a name="network-access-controls"></a>網路存取控制
雖然 hello Azure 虛擬網路 (VNet) 的 Azure 網路模型的 hello 基石，提供隔離和保護 hello[網路安全性群組群組 (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) hello 使用 tooenforce 及控制網路流量的主要工具在 hello 網路層級的規則。

![ 網路存取控制](media/azure-network-security/azure-network-security-fig-8.png)


您可以藉由允許或拒絕虛擬網路，客戶透過跨單位連線的網路上的系統中的 hello 工作負載之間的通訊控制的存取，或直接網際網路通訊。

在 hello 圖表 Vnet 和 Nsg 位於 Nsg、 UDR 和網路的虛擬應用裝置可以是使用的 toocreate 安全性界限 tooprotect hello 應用程式部署在受保護的 hello 網路中的 hello Azure 的整體安全性堆疊中特定圖層中。

Nsg 使用 5 tuple tooevaluate 流量 （及 hello NSG hello 規則設定中所使用）：

-   [來源和目的地 IP 位址](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [來源和目的地連接埠](https://technet.microsoft.com/library/dd197515)

-   通訊協定：[傳輸控制通訊協定 (TCP)](https://technet.microsoft.com/library/cc940037.aspx) 或[使用者資料包通訊協定 (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

這表示您可以控制存取單一 VM 與群組之間的 Vm 或單一 VM tooanother 單一 VM，或整個子網路之間。 同樣地，請記住，這是簡單的具狀態封包篩選，而不是完整的封包檢查。 網路安全性群組中沒有通訊協定驗證或網路層級 IDS 或 IPS 功能。

NSG 隨附一些您應該注意的內建規則。 它們是：

-   **允許特定的虛擬網路內的所有流量：** hello 上的所有 Vm 相同 Azure 虛擬網路可以彼此都通訊。

-   **允許 Azure 負載平衡 tooinbound:** 這個規則允許來自任意來源位址 tooany 目的地位址的流量 hello Azure 負載平衡器。

-   **拒絕所有輸入：** 此規則會封鎖從 hello 您明確允許的網際網路傳送的所有流量。

-   **允許所有流量輸出 toohello 網際網路：**此規則可讓 Vm tooinitiate 連線 toohello 網際網路。 若不想使用起始這些連線，您需要 toocreate 規則 tooblock 這些連線，或強制執行強制通道。

#### <a name="system-routes-and-user-defined-routes"></a>系統路由和使用者定義的路由

當您在 Azure 中新增虛擬機器 (Vm) tooa 虛擬網路 (VNet) 時，您會注意到 hello Vm 會自動無法 toocommunicate 彼此 hello 網路上。 您不需要 toospecify 閘道，即使 hello Vm 位於不同的子網路。

hello 也適用於來自 hello Vm toohello 通訊公用網際網路，以及混合式連線從 Azure tooyour 擁有資料中心已存在時，甚至 tooyour 與內部網路。

![系統路由](media/azure-network-security/azure-network-security-fig-9.png)

這個流量可能是通訊的因為 Azure 會使用一系列的系統路由 toodefine IP 流量流動的方式。 系統路由控制 hello hello 下列案例中的通訊流程：

-   從 hello 相同子網路。

-   從 VNet 中的子網路 tooanother。

-   從 Vm toohello 網際網路。

-   從透過 VPN 閘道 VNet tooanother VNet。

-   從 VNet tooanother 透過對等互連的 VNet 的 VNet ([服務鏈結](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview))。

-   從透過 VPN 閘道的 VNet tooyour 在內部部署網路。

許多企業都有嚴格的安全性，以及需要的所有網路封包 tooenforce 特定內部檢查相容性需求原則。 Azure 提供的機制稱為[強制通道](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling)，路由傳送來自 hello tooon 內部部署 Vm 流量，或藉由建立自訂路由[邊界閘道通訊協定 (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp)透過公告ExpressRoute 或 VPN。

Azure 中的強制通道會透過虛擬網路使用者定義路由 (UDR) 進行設定。 重新導向流量 tooan 內部部署站台以預設路由 toohello Azure VPN 閘道。

hello 下節列出 hello 目前限制的 hello 路由表和路由的 Azure 虛擬網路：

-   每個虛擬網路的子網路皆有內建的系統路由表。 hello 系統路由表具有下列三個路由群組的 hello:

 -  **區域的 VNet 路由：**直接 toohello Vm 中的目的地 hello 相同虛擬網路

 - **內部部署路由：** toohello Azure VPN 閘道

 -  **預設路由：**直接 toohello 網際網路。 目的地的封包 toohello 私人 IP 位址未涵蓋的 hello 前兩個路由會卸除。

-   Hello 版本中的使用者定義的路由，您可建立路由表 tooadd 預設路由，並再將關聯 hello 路由表 tooyour VNet 子網路 tooenable 強制通道這些子網路上。

-   您在 hello 跨單位本機站台連線的 toohello 虛擬網路之間需要 tooset 「 預設網站 」。

-   強制通道必須與具有動態路由 VPN 閘道 (非靜態閘道) 的 VNet 相關聯。

- 未設定這項機制，透過 ExpressRoute 強制通道，但相反地，會啟用透過 ExpressRoute BGP hello 將預設路由通告對等互連工作階段。

> [!Note]
> 如需詳細資訊，請參閱 hello [ExpressRoute 文件](https://azure.microsoft.com/documentation/services/expressroute/)如需詳細資訊。

#### <a name="network-security-appliances"></a>網路安全性設備
雖然網路安全性群組和使用者定義的路由可以提供特定量值在 hello 的網路安全性的網路傳輸層 hello [OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，將要 toobe 情況下您想要或需要 tooenablehello 網路堆疊的較高層級的安全性。 在這類情況下，建議您部署 Azure 合作夥伴所提供的虛擬網路安全性應用裝置。

![網路安全性設備](./media/azure-network-security/azure-network-security-fig-10.png)

Azure 網路的安全性設備卻改善 VNet 安全性和網路功能，而且這是可從許多廠商透過 hello [Azure Marketplace](https://azuremarketplace.microsoft.com)。 這些虛擬的安全性應用裝置可以是已部署的 tooprovide:

-   高可用性的防火牆

-   入侵預防

-   入侵偵測

-   Web 應用程式防火牆 (WAF)

-   WAN 最佳化

-   路由

-   負載平衡

-   VPN

-   憑證管理

-   Active Directory

-   多重要素驗證

#### <a name="application-gateway"></a>應用程式閘道

[Microsoft Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)是專用的虛擬設備，它會以服務形式提供應用程式傳遞控制器 (ADC)。

 ![應用程式閘道](./media/azure-network-security/azure-network-security-fig-11.png)

應用程式閘道可讓您 toooptimize web 伺服陣列效能和可用性卸載 CPU 密集 SSL 終止 toohello 應用程式閘道 （SSL 卸載）。 它也提供其他第 7 層路由功能，包括：

-   傳入流量的循環配置資源散發

-   Cookie 型工作階段同質

-   URL 路徑型路由

-   能力 toohost 單一應用程式閘道背後的多個網站


A [web 應用程式防火牆 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)也會提供 hello 應用程式閘道的一部分。 這會提供保護 tooweb 應用程式，從一般 web 弱點和破解。 應用程式閘道可以設定為網際網路對向閘道、內部專用閘道或兩者混合。

可以在偵測或預防模式中執行應用程式閘道 WAF。 常見的使用案例是系統管理員 toorun 偵測模式 tooobserve 流量的惡意模式中。 一旦偵測到潛在的弱點，開啟 tooprevention 模式會封鎖可疑的連入流量。

 ![應用程式閘道](./media/azure-network-security/azure-network-security-fig-12.png)

此外，應用程式閘道 WAF 可協助您監視 web 應用程式使用即時 WAF 記錄與整合攻擊[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)和[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)tootrack WAF 警示並輕鬆地監視趨勢。

hello JSON 格式化的記錄檔會直接進入 toohello 客戶儲存體帳戶。 您可以完全掌控這些記錄，而且可以套用自己的保留原則。

您也可以使用 [Azure 記錄整合](https://aka.ms/AzLog)，將這些記錄內嵌至自己的分析系統中。 WAF 記錄檔也會與整合[Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite)因此您可以使用 OMS 記錄分析 tooexecute 複雜的更細緻的查詢。

#### <a name="azure-web-application-firewall-waf"></a>Azure Web 應用程式防火牆 (WAF)

Web 應用程式也日益利用一般的已知的弱點，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和會出現在 hello 其他攻擊的惡意攻擊的目標[OWASP 前 10 個](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)。 防止 hello 應用程式中的這類攻擊需要嚴格的維護、 修補和監視 hello 應用程式拓撲的多個層級。

 ![Azure Web 應用程式防火牆 (WAF)](./media/azure-network-security/azure-network-security-fig-13.png)

集中式 [Web 應用程式防火牆 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) 可以防禦 Web 攻擊並簡化安全性管理，而不需要變更任何應用程式。

WAF 方案也可以回應 tooa 更快的安全性威脅的修補與保護每個個別的 web 應用程式的中央位置的已知的弱點。 現有的應用程式閘道可以輕鬆地是轉換的 tooa web 應用程式啟用防火牆應用程式閘道。

#### <a name="network-availability-controls"></a>網路可用性控制

有不同的選項 toodistribute 網路流量使用 Microsoft Azure。 這些選項的運作方式彼此間會有差異，其具備不同的功能組合並支援不同的案例。 它們每個都可單獨使用，或組合在一起。

下列是 hello 網路可用性控制：

-   Azure Load Balancer

-   應用程式閘道

-   流量管理員

**Azure Load Balancer**

Tooyour 應用程式提供高可用性和網路效能。 這是 Layer 4 (TCP、UDP) 負載平衡器，可將連入流量分配到負載平衡集中所定義服務的狀況良好執行個體。

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Azure Load Balancer 可以設定為：

-   負載平衡連入網際網路流量 toovirtual 機器。 這個組態稱為 [網際網路面向的負載平衡](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)。

-   平衡虛擬網路中的虛擬機器之間、雲端服務中的虛擬機器之間，或內部部署電腦與跨單位部署虛擬網路中的虛擬機器之間的流量負載。 這個組態稱為 [內部負載平衡](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)。

-   將外部流量 tooa 特定虛擬機器。

Hello 雲端中的所有資源都必須公開的 IP 位址 toobe hello 網際網路從可以連線。 在 Azure 中的 hello 雲端基礎結構會使用其資源的非路由的 IP 位址。 Azure 會使用公用 IP 位址 toocommunicate toohello 網際網路的網路位址轉譯 (NAT)。

 **應用程式閘道**

 在 hello 應用程式層級 (hello OSI 網路參考堆疊中的圖層 7) 運作的應用程式閘道。 它會充當反向 proxy 服務時，終止 hello 用戶端連線，並轉送要求 tooback 端端點。

 **流量管理員**

Microsoft Azure Traffic Manager 可讓您 toocontrol hello 使用者流量分散的服務端點的不同資料中心內。 流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。 您也可以將流量管理員使用於外部、非 Azure 端點。

Traffic Manager 會使用 hello 網域名稱系統 (DNS) toodirect 用戶端要求 toohello 最適當的端點，根據[流量路由方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)和 hello hello 端點健全狀況。 Traffic Manager 所提供的流量路由方法 toosuit 不同的應用程式的需求，端點健全狀況範圍[監視](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)，以及自動容錯移轉。 Traffic Manager 是彈性 toofailure，包括整個 Azure 地區的 hello 失敗。

Azure Traffic Manager 可讓您的流量 toocontrol hello 分配在應用程式端點。 端點是裝載於 Azure 內部或外部的任何網際網路對向服務。

流量管理員提供兩大優點︰

-   根據數個 tooone 流量分散[流量路由方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)。

-   [連續監視端點健康狀態](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)以及在端點失敗時自動容錯移轉。

當用戶端嘗試 tooconnect tooa 服務時，它必須先解決 hello 的 hello 服務 tooan IP 位址的 DNS 名稱。 hello 用戶端接著會連線 toothat IP 位址 tooaccess hello 服務。 Traffic Manager 會使用 DNS toodirect 用戶端 toospecific 服務端點的 hello 流量路由方法的 hello 規則為基礎。 用戶端直接連接 toohello 選取端點。 流量管理員不是 Proxy 或閘道。 Traffic Manager 不會看到 hello hello 用戶端與 hello 服務之間傳送的流量。

### <a name="azure-network-validation"></a>Azure 網路驗證

Hello Azure 網路的 tooensure 正在運作，因為它已設定且可在完成驗證，azure 網路驗證會使用 hello 服務和功能可用 toomonitor hello 網路。 使用 Azure 網路監看員，您可以存取的記錄和診斷功能，讓您深入資訊 toounderstand 您的網路效能和健全狀況。 這些功能可透過入口網站、Power Shell、CLI、Rest API 和 SDK 存取。

Azure 操作的安全性是指 toohello 服務、 控制項和功能可用 toousers 保護其資料、 應用程式，以及其他 Microsoft Azure 中的資產。 Azure 操作安全性是建置在結合 hello 知識透過唯一 tooMicrosoft，包括 Microsoft 安全性開發週期 (SDL)，Microsoft 回應資訊安全中心 hello hello 各種功能的架構程式及深層 hello 網路安全性威脅大環境的認知。

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure 網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure 儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Azure Resource Manager

hello 人員和操作 Microsoft Azure 的程序有或許 hello 最重要的安全性功能 hello 平台。 這一節說明 Microsoft 的全域資料中心基礎結構中，可協助您增強及維護安全性、持續性和隱私權的功能。

許多元件 – 也許虛擬機器、 儲存體帳戶和虛擬網路或 web 應用程式、 資料庫、 資料庫伺服器和協力廠商服務的 hello 基礎結構，您的應用程式通常由所組成。 您看不到這些元件作為個別的實體，而是看到它們作為單一實體相關且彼此相依的組件。 您想 toodeploy、 管理和監視這些群組。 Azure 資源管理員可讓您與您的方案中的 hello 資源 toowork 為群組。

您可以部署、 更新或刪除您的解決方案是單一的協調作業，在 hello 的所有資源。 您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。 資源管理員提供安全性、 稽核和標記功能 toohelp 部署後管理您的資源。

**使用資源管理員的 hello 優點**

Resource Manager 會提供數個優點：

-   您可以部署、 管理及監視您的方案 hello 的所有資源群組，而非個別處理這些資源。

-   重複，您可以部署整個 hello 開發生命週期方案，並確保一致的狀態以部署您的資源。

-   您可以透過宣告式範本而非指令碼來管理基礎結構。

-   您可以定義 hello 資源，因此它們部署在 hello 正確的順序之間的相依性。

-   因為角色型存取控制 (RBAC) 原生整合至 hello 管理平台，您可以套用存取控制 tooall 服務資源群組中。

-   您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。

-   您可以檢視共用標籤之資源群組的成本，以釐清您的組織的計費方式。

> [!Note]
> 資源管理員提供新的方式 toodeploy 和管理您的方案。 如果您使用 hello 舊版部署模型而且想 toolearn 有關 hello 變更，請參閱[了解資源管理員部署和傳統部署](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)。

## <a name="azure-network-logging-and-monitoring"></a>Azure 網路記錄和監視

Azure 提供許多工具 toomonitor、 防止、 偵測及回應 toonetwork 安全性事件。 Hello 最有力工具可用 tooyou 此區域中的部分包括：

-   網路監看員

-   網路資源層級監視

-   Log Analytics

### <a name="network-watcher"></a>網路監看員

[網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)-提供以案例為基礎監視使用中網路監看員的 hello 功能。 這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。 案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。

 ![網路監看員](./media/azure-network-security/azure-network-security-fig-15.png)

網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。

網路監看員目前具有下列功能的 hello:

#### <a name="topology"></a>拓撲

[拓撲](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview)會傳回虛擬網路中的網路資源之圖形。 hello 圖描繪 hello 資源 toorepresent hello 結束 tooend 網路連線之間的 hello 互連。 在 hello 入口網站拓撲傳回 hello 資源物件根據虛擬網路為基礎。 即使在 hello 資源群組將不會顯示，但會由 hello 網路監看員區域以外的 hello 資源間的線條顯示 hello 關聯性。 傳回在 hello 入口網站檢視中的 hello 資源是 hello 網路元件是圖形化的子集。 toosee hello 的完整清單網路資源，您可以使用[PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell)或[REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest)。

因為傳回的資源 hello 它們之間的連線是在兩個關聯性建立模型。

- **內含項目** - 虛擬網路包含其中含有 NIC 的子網路。

- **相關聯** - NIC 與 VM 相關聯。

#### <a name="variable-packet-capture"></a>變數封包擷取

網路監看員[變數的封包擷取](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview)可讓您 toocreate 封包擷取工作階段 tootrack 流量 tooand 從虛擬機器。 封包擷取協助 toodiagnose 網路異常這兩個被動和 proactivity。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。

封包擷取是透過網路監看員從遠端啟動的虛擬機器擴充功能。 這項功能可以減輕工作 hello 負擔 hello 預期虛擬機器上，以節省寶貴的時間手動執行封包擷取。 透過 hello 入口網站、 PowerShell、 CLI 或 REST API，可以觸發封包擷取。 觸發封包擷取方式的其中一個範例是使用虛擬機器警示。

#### <a name="ip-flow-verify"></a>IP 流量驗證

[IP 流量確認](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview)檢查封包允許或拒絕 tooor 從 5 個 tuple 資訊為基礎的虛擬機器。 這些資訊包括方向、通訊協定、本機 IP、遠端 IP、本機連接埠和遠端連接埠。 如果安全性群組遭拒絕 hello 封包，會傳回 hello 拒絕 hello 封包的 hello 規則名稱。 這項功能時可以選擇任何來源或目的地 IP，協助系統管理員快速診斷中的連線問題或 toohello 網際網路來回或 toohello 在內部部署環境。

IP 流量驗證是以虛擬機器的網路介面作為目標。 根據設定的 hello 設定 tooor 該網路介面，然後驗證流量。 這項功能可用於確認從虛擬機器的輸入或輸出流量 tooor 時，是否要封鎖網路安全性群組中的規則。

#### <a name="next-hop"></a>下一個躍點

決定 hello[下一個躍點](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview)hello Azure 網路網狀架構中路由傳送封包，讓您 toodiagnose 任何錯誤設定使用者定義的路由。 從 VM 的流量會傳送 tooa 根據 hello 與 NIC 相關聯的有效路由的目的地 下一個躍點取得下一個躍點類型 hello 和封包的 IP 位址從特定虛擬機器與 nic。 這可協助 toodetermine 如果 hello 封包會被導向的 toohello 目的地，或為正在黑色 hello 流量書背。

下一個躍點也會傳回 hello 與 hello 下一個躍點相關聯的路由表。 如果 hello 路由定義為使用者定義的路由，請查詢下一個躍點，將會傳回該路由。 否則，下一個躍點會傳回「系統路由」。

#### <a name="security-group-view"></a>安全性群組檢視

取得在 VM 套用的 hello 有效且套用安全性規則。 網路安全性群組會在子網路層級或 NIC 層級產生關聯。 當關聯的子網路層級，它會套用 hello 子網路中的 tooall hello VM 執行個體。 網路[安全性群組檢視](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview)會傳回所有設定的 hello Nsg 與 NIC 和子網路層級提供深入了解 hello 組態的虛擬機器關聯的規則。 此外，hello 有效的安全性規則會傳回每個 VM 中的 hello Nic。 使用 [網路安全性群組] 檢視，您就可以評估 VM 的網路弱點，例如開啟的連接埠。 您也可以驗證您的網路安全性群組是否正常運作根據如果[hello 之間的比較設定和 hello 有效的安全性規則](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell)。

#### <a name="nsg-flow-logging"></a>NSG 流量記錄

 網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。 hello 流程是由 5-tuple 資訊 – 來源 IP、 目的地 IP、 來源連接埠，目的地連接埠和通訊協定定義。

[網路安全性小組流程記錄](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview)是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>虛擬網路閘道和連線疑難排解

網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。 這些功能的其中之一便是資源疑難排解。 [資源疑難排解](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)可透過 PowerShell、CLI 或 REST API 來呼叫。 呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。

本節會帶領您完成疑難排解資源的目前可用的 hello 不同的管理工作。

-   [針對虛擬網路閘道進行疑難排解](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [針對連線進行疑難排解](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>網路訂用帳戶限制

[訂用帳戶限制的網路](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)您提供的每個訂用帳戶中針對 hello 的可用資源的最大數目的區域中的 hello 網路資源的 hello 使用量的詳細資料。

#### <a name="configuring-diagnostics-log"></a>設定診斷記錄

網路監看員提供[診斷記錄](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)檢視。 此檢視包含所有支援診斷記錄的網路資源。 從這個檢視中，您可以方便且快速地啟用和停用網路資源。

### <a name="network-resource-level-monitoring"></a>網路資源層級監視

下列功能的 hello 可供資源層級的監視：

#### <a name="audit-log"></a>稽核記錄檔

Hello 的網路組態的一部分執行的作業記錄。 這些稽核記錄檔是基本 tooestablish 各種符合。 這些記錄檔可以在 hello Azure 入口網站中檢視，或使用 Microsoft 工具，例如 Power BI 或協力廠商工具來擷取。 稽核記錄檔皆可透過 hello 入口網站、 PowerShell、 CLI 和 Rest API。

> [!Note]
> 如需稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit)。
針對所有網路資源所進行的作業都會有稽核記錄。


#### <a name="metrics"></a>度量

計量是在一段時間內所收集到的效能測量數據和計數器。 計量目前適用於應用程式閘道。 度量可以是使用的 tootrigger 警示臨界值為基礎。 預設的 azure 應用程式閘道監視它的後端集區中的所有資源 hello 健全狀況，並自動移除任何從 hello 集區被視為狀況不良的資源。 應用程式閘道會繼續 toomonitor hello 狀況不良的執行個體，並將其加入回 toohello 狀況良好的後端集區，當它們變成可用，而且回應 toohealth 探查。 應用程式閘道會傳送 hello 健全狀況探查 hello 與 hello 後端 HTTP 設定中定義的相同連接埠。 此組態可確保該 hello 探查測試的 hello 相同連接埠，客戶就會使用 tooconnect toohello 後端。

> [!Note]
> 請參閱[應用程式閘道診斷](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview)tooview 度量可以列印文件的是，請使用的 toocreate 警示。

#### <a name="diagnostic-logs"></a>診斷記錄檔

定期和即時事件建立的網路資源，登入傳送 tooan 事件中心 」 或 「 記錄分析的儲存體帳戶。 這些記錄檔提供深入了解資源的 hello 健全狀況。 您可以在 Power BI 和 Log Analytics 等工具中檢視這些記錄。 toolearn tooview 診斷記錄檔的瀏覽[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)。

診斷記錄適用於[負載平衡器](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log)、[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)、路由和[應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)。

網路監看員提供診斷記錄檢視。 此檢視包含所有支援診斷記錄的網路資源。 從這個檢視中，您可以方便且快速地啟用和停用網路資源。

### <a name="log-analytics"></a>Log Analytics

[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)是中的服務[Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) ，監視您的雲端和內部部署環境 toomaintain 其可用性及效能。 它會收集您的雲端和內部部署環境和其他監視工具 tooprovide 分析資源所產生的跨多個來源資料。

記錄分析會提供下列用於監視您的網路解決方案的 hello:

-   網路效能監視器 (NPM)

-   Azure 應用程式閘道分析

-   Azure 網路安全性群組分析

#### <a name="network-performance-monitor-npm"></a>網路效能監視器 (NPM)
hello[網路效能監視器](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor)管理解決方案是網路監視會監視 hello 健全狀況、 可用性和網路連線能力的解決方案。

它是使用的 toomonitor 之間的連線：

-   公用雲端與內部部署環境

-   資料中心與使用者地點 (分公司)

-   裝載各種多層式應用程式的子網路。


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Log Analytics 中的 Azure 應用程式閘道分析

應用程式閘道可支援下列記錄檔的 hello:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

應用程式閘道可支援下列度量的 hello:

-   5 分鐘輸送量

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Log Analytics 中的 Azure 網路安全性群組分析

hello 下列記錄檔支援[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:**包含哪些 nsg 規則會套用的 tooVMs 和 MAC 位址為基礎的執行個體角色的項目。 hello 狀態，這些規則會收集每隔 60 秒。

- **NetworkSecurityGroupRuleCounter:**包含項目多少次每個 NSG 規則會套用的 toodeny 或允許流量。

## <a name="next-steps"></a>後續步驟
閱讀一些有深度的安全性主題，以深入了解安全性：

-   [網路安全性群組 (NSG) 的 Log Analytics](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [該磁碟機 hello 雲端中斷網路創新](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [網路交換器軟體提供 hello Microsoft 全域雲端 SONiC: hello](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Microsoft 建置其快速且可靠全域網路的方式](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [點燃網路創新](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
