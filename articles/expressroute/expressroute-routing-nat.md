---
title: "適用於 Azure ExpressRoute 的 NAT | Microsoft Docs"
description: "此頁面提供用來設定和管理 ExpressRoute 循環路由的詳細需求。"
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>適用於 ExpressRoute 的 NAT

使用 ExpressRoute tooconnect tooMicrosoft 雲端服務，您將需要 tooset 註冊和管理路由。 有些連線提供者會以受管理的服務形式提供路由的設定和管理。 如果提供了這項服務，請洽詢您的連線提供者 toosee。 如果沒有，您必須遵守下列需求的 toohello。 

請參閱 toohello[線路和路由網域](expressroute-circuit-peerings.md)hello 路由的說明文章需要 toobe 的工作階段中 toofacilitate 連線設定。

> [!NOTE]
> Microsoft 不支援任何高可用性組態的路由器備援通訊協定 (如 HSRP、VRRP)。 我們依賴每個對等互連的一組備援 BGP 工作階段來取得高可用性。
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>用於對等互連的 IP 位址

您需要 tooreserve 幾個區塊的 IP 位址 tooconfigure 路由在網路與 Microsoft 的企業邊緣 (MSEEs) 路由器之間。 本節提供一份需求，並描述 hello 規則必須如何取得及使用這些 IP 位址。

### <a name="ip-addresses-used-for-azure-private-peering"></a>用於 Azure 私人對等互連的 IP 位址

您可以使用私人 IP 位址或公用 IP 位址 tooconfigure hello 對等互連。 hello 可用來設定路由的位址範圍不得與 Azure 中的位址範圍使用 toocreate 虛擬網路重疊。 

* 您必須為路由介面保留一個 /29 子網路或兩個 /30 子網路。
* 用於路由傳送嗨子網路可以是私人 IP 位址或公用 IP 位址。
* hello 子網路不必須與用於 hello Microsoft 雲端中的 hello 客戶所保留的 hello 範圍發生衝突。
* 如果使用 /29 子網路，它就會分割成兩個 /30 子網路。 
  * 第一次 hello/30 子網路將用於 hello 主要連結和 hello 第二個/30 子網路將用於 hello 次要連結。
  * 針對每個 hello/30 子網路，您必須在路由器上使用 hello/30 子網路的 hello 第一個 IP 位址。 Microsoft 會使用 BGP 工作階段的 hello/30 子網路 tooset hello 第二個 IP 的位址。
  * 您必須設定兩個 BGP 工作階段，如我們[可用性 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 有效。  

#### <a name="example-for-private-peering"></a>私人對等互連範例

如果您選擇 toouse a.b.c.d/29 tooset 向上 hello 對等互連，它會分成兩個的/30 子網路。 Hello 下列範例中，我們將探討如何使用 hello a.b.c.d/29 子網路。 

a.b.c.d/29 會分割 tooa.b.c.d/30 而 a.b.c.d+4/30 和 hello 佈建應用程式開發介面透過 tooMicrosoft 中傳遞。 您將使用 a.b.c.d+1 hello VRF IP 的 hello 主要 PE 和 Microsoft 會耗用 a.b.c.d+2 為 hello VRF IP hello 主要 MSEE 如下。 您將使用 a.b.c.d+5 hello VRF IP hello 次要 PE 和 Microsoft 將使用 a.b.c.d+6 為 hello VRF IP hello 次要 MSEE 如下。

試想一個情況，您在其中選取 192.168.100.128/29 tooset 註冊私用對等互連。 192.168.100.128/29 192.168.100.128 位址包含 too192.168.100.135，在這些：

* 192.168.100.128/30 會指派 toolink1，與使用 192.168.100.129 和 Microsoft 使用 192.168.100.130 的提供者。
* 192.168.100.132/30 會指派 toolink2，與使用 192.168.100.133 和 Microsoft 使用 192.168.100.134 的提供者。

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>用於 Azure 公用與 Microsoft 對等互連的 IP 位址

您必須使用您自己的公用 IP 位址設定 hello BGP 工作階段。 Microsoft 必須能夠 tooverify hello 擁有權的 hello 透過路由網際網路登錄和網際網路路由所登錄的 IP 位址。 

* 您必須使用唯一/29 子網路或兩個的/30 子網路 tooset 向上 hello BGP 對等每個對等互連每個 ExpressRoute 電路 （如果您有多個）。 
* 如果使用 /29 子網路，它就會分割成兩個 /30 子網路。 
  * 第一次 hello/30 子網路將用於 hello 主要連結和 hello 第二個/30 子網路將用於 hello 次要連結。
  * 針對每個 hello/30 子網路，您必須在路由器上使用 hello/30 子網路的 hello 第一個 IP 位址。 Microsoft 會使用 BGP 工作階段的 hello/30 子網路 tooset hello 第二個 IP 的位址。
  * 您必須設定兩個 BGP 工作階段，如我們[可用性 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 有效。

## <a name="public-ip-address-requirement"></a>公用 IP 位址需求

### <a name="private-peering"></a>私人對等互連

您可以選擇 toouse 用於私人互連的公用或私人 IPv4 位址。 我們會提供流量的端對端隔離，因此在私人對等互連的情況下不可能發生位址與其他客戶重疊。 這些位址不是公告的 tooInternet。 

### <a name="public-peering"></a>公用對等互連

hello Azure 公用互連路徑可讓您 tooconnect tooall 裝載的服務在 Azure 中透過其公用 IP 位址。 其中包括服務列在 hello [ExpessRoute 常見問題集](expressroute-faqs.md)與任何由 Isv Microsoft Azure 上裝載的服務。 服務連線 tooMicrosoft Azure 公用對等互連一律從起始您的網路到 hello Microsoft 網路。 Hello 流量預定的 tooMicrosoft 網路，您必須使用公用 IP 位址。

### <a name="microsoft-peering"></a>Microsoft 對等互連

hello Microsoft 對等互連路徑可讓您透過 hello Azure 公用互連路徑連接 tooMicrosoft 不支援的雲端服務。 服務的 hello 清單包含 Office 365 服務，例如 Exchange Online、 SharePoint Online、 商務和 Dynamics 365 Skype。 Microsoft 在 hello Microsoft 對等互連支援雙向連線。 進入 hello Microsoft 網路之前，資料傳輸 tooMicrosoft 雲端服務必須使用有效的公用 IPv4 位址。

請確定您的 IP 位址和 AS 號碼會在下面所列的 hello 登錄的其中一個已註冊的 tooyou。

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> 公用 IP 位址通告透過 ExpressRoute tooMicrosoft 不得公告的 toohello 網際網路。 這可能會中斷連線 tooother Microsoft 服務。 不過，您的網路中伺服器用來與 Microsoft 內部 O365 端點進行通訊的公用 IP 位址可透過 ExpressRoute 公告。 
> 
> 

## <a name="dynamic-route-exchange"></a>動態路由交換

路由交換將會透過 eBGP 通訊協定。 Hello MSEEs 與您的路由器之間建立 EBGP 的工作階段。 不一定需要驗證 BGP 工作階段。 如有必要，也可以設定 MD5 雜湊。 請參閱 hello[設定路由](expressroute-howto-routing-classic.md)和[電路的佈建的工作流程和電路狀態](expressroute-workflows.md)設定 BGP 工作階段的資訊。

## <a name="autonomous-system-numbers"></a>自發系統號碼

Microsoft 將使用 AS 12076 進行 Azure 公用、Azure 私人和 Microsoft 對等互連。 我們已從 65515 too65520 供內部使用保留的 Asn。 同時支援 16 和 32 位元號碼。

資料傳輸對稱沒有任何相關需求。 hello 正向和傳回路徑可能會跨越不同的路由器組。 相同的路由必須從橫跨多個屬於您的循環配對的任一端公告。 路由公制不需要的 toobe 完全相同。

## <a name="route-aggregation-and-prefix-limits"></a>路由彙總與前置詞限制

我們支援註冊 too4000 通告 toous 透過 hello Azure 私用對等的前置詞。 這可以增加總 too10，如果已啟用 hello ExpressRoute premium add-on 000 的前置詞。 我們接受 too200 前置詞，每個公用 Azure 的 BGP 工作階段及 Microsoft 對等互連。 

如果 hello 前置詞數目超過 hello 限制，將會捨棄 hello BGP 工作階段。 我們將接受 hello 私用對等互連連結只預設路由。 提供者必須篩選出預設路由和私人 IP 位址 (RFC 1918) 從 hello 公用 Azure 和 Microsoft 對等互連路徑。 

## <a name="transit-routing-and-cross-region-routing"></a>傳輸路由和跨區域路由

ExpressRoute 不能設定為傳輸路由器。 您會有 toorely 連線的傳輸路由服務提供者。

## <a name="advertising-default-routes"></a>公告預設路由

只有 Azure 私人對等互連工作階段允許預設路由。 在這種情況下，我們會將所有來自 hello 相關聯的虛擬網路 tooyour 網路流量。 通告預設路由至私用對等互連，將會導致 hello 網際網路路徑從 Azure 遭到封鎖。 您必須依賴來自您公司的邊緣 tooroute 流量和 toohello 裝載於 Azure 的網際網路服務。 

 tooenable 連線 tooother Azure 服務和基礎結構服務，您必須確定下列項目 hello 就地有：

* Azure 公用對等互連是啟用的 tooroute 流量 toopublic 端點
* 您可以使用使用者定義路由的 tooallow 網際網路連線的每一個子網路需要網際網路連線能力。

> [!NOTE]
> 公告預設路由會中斷 Windows 和其他 VM 授權啟用。 請依照下列指示[這裡](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)toowork 解決這個問題。
> 
> 

## <a name="support-for-bgp-communities-preview"></a>BGP 社群支援 (預覽)

本節提供 BGP 社群如何搭配 ExpressRoute 使用的概觀。 Microsoft 將通告公用 hello 與 Microsoft 對等互連路徑中加上適當的社群值路由的路由。 hello 這麼做的基本原理，hello 的社群以下將詳述值的詳細資訊。 Microsoft，不過，不支援之任何群體值標記的 tooroutes 通告 tooMicrosoft。

如果您要連接 tooMicrosoft 透過 ExpressRoute，在任何一個的對等互連位置地緣政治區域內，您必須存取 tooall Microsoft 雲端服務 hello 地緣政治界限內的所有區域。 

例如，如果您透過 ExpressRoute 連接 tooMicrosoft 阿姆斯特丹中的，您必須存取 tooall Microsoft 雲端服務裝載於北歐和西歐。 

請參閱 toohello [ExpressRoute 合作夥伴和互連位置](expressroute-locations.md)網頁地緣政治區域及相關聯的 Azure 區域對應 ExpressRoute 對等互連位置的詳細清單。

您可以針對每個地理政治區域購買多個 ExpressRoute 循環。 將多個連線提供極大的好處，高可用性到期 toogeo 備援。 在您有多個 ExpressRoute 電路的情況下，您會收到的 hello 公告相同的前置詞集合 Microsoft 在 hello 公用對等互連，且 Microsoft 對等互連路徑。 這表示您將會有多個路徑可從您的網路連到 Microsoft。 這可能會造成您的網路中進行的次佳路由決策 toobe。 如此一來，您可能會遇到次佳的連線經驗 toodifferent 服務。 

Microsoft 會標記透過公用互連公告的首碼，並裝載於 Microsoft 對等互連以適當的 BGP 社群值，指出 hello 區域 hello 前置詞。 您可以依賴 hello 社群值 toomake 適當路由決策 toooffer[最佳路由 toocustomers](expressroute-optimize-routing.md)。

| **地緣政治區域** | **Microsoft Azure 區域** | **BGP 社群值** |
| --- | --- | --- |
| **北美洲** | | |
| 美國東部 |12076:51004 | |
| 美國東部 2 |12076:51005 | |
| 美國西部 |12076:51006 | |
| 美國西部 2 |12076:51026 | |
| 美國中西部 |12076:51027 | |
| 美國中北部 |12076:51007 | |
| 美國中南部 |12076:51008 | |
| 美國中部 |12076:51009 | |
| 加拿大中部 |12076:51020 | |
| 加拿大東部 |12076:51021 | |
| **南美洲** | | |
| 巴西南部 |12076:51014 | |
| **歐洲** | | |
| 北歐 |12076:51003 | |
| 西歐 |12076:51002 | |
| **亞太地區** | | |
| 東亞 |12076:51010 | |
| 東南亞 |12076:51011 | |
| **日本** | | |
| 日本東部 |12076:51012 | |
| 日本西部 |12076:51013 | |
| **澳大利亞** | | |
| 澳洲東部 |12076:51015 | |
| 澳洲東南部 |12076:51016 | |
| **印度** | | |
| 印度南部 |12076:51019 | |
| 印度西部 |12076:51018 | |
| 印度中部 |12076:51017 | |

所有 microsoft 通告的路由會標記 hello 社群的適當值。 

> [!IMPORTANT]
> 全域前置詞會加上適當的社群值，而且只會在啟用 ExpressRoute 進階附加元件時公告。
> 
> 

除了上述 toohello，Microsoft 將也標記它們屬於 hello 服務為基礎的前置詞。 這適用於只有 toohello Microsoft 對等互連。 hello 下表提供服務 tooBGP 社群值的對應。

| **服務** | **BGP 社群值** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **商務用 Skype** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **其他 Office 365 服務** |12076:5100 |

> [!NOTE]
> Microsoft 不會接受您 hello 路由通告 tooMicrosoft 設定任何 BGP 社群值。
> 
> 

## <a name="next-steps"></a>後續步驟

* 設定 ExpressRoute 連線。
  
  * [建立 ExpressRoute 電路 hello 傳統部署模型](expressroute-howto-circuit-classic.md)或[建立及修改 ExpressRoute 電路使用 Azure 資源管理員](expressroute-howto-circuit-arm.md)
  * [設定路由 hello 傳統部署模型](expressroute-howto-routing-classic.md)或[設定路由 hello Resource Manager 部署模型。](expressroute-howto-routing-arm.md)
  * [連結傳統的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)或[連結的資源管理員 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)

