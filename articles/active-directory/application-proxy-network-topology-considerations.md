---
title: "使用 Azure Active Directory 應用程式 Proxy 時，aaaNetwork 拓撲考量 |Microsoft 文件"
description: "涵蓋使用 Azure AD 應用程式 Proxy 時的網路拓撲考量。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量

本文說明使用 Azure Active Directory 應用程式 Proxy 遠端發佈及存取您的應用程式時的網路拓撲考量。

## <a name="traffic-flow"></a>流量

透過 Azure AD Application Proxy 發行應用程式時，從 hello 使用者 toohello 應用程式的流量會流經共有三個連接：

1. hello 使用者連接在 Azure 上的 toohello Azure AD Application Proxy 服務公用端點
2. hello 應用程式 Proxy 服務連接 toohello 應用程式 Proxy 連接器
3. hello 應用程式 Proxy 連接器連接 toohello 目標應用程式

![顯示從使用者 tootarget 應用程式的流量圖表](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>租用戶位置與應用程式 Proxy 服務

當您註冊 Azure AD 租用戶時，hello 區域，您的租用戶由您指定的 hello 國家/地區決定。 當您啟用應用程式 Proxy 時，選擇或建立 hello 中相同租用戶的 hello 應用程式 Proxy 服務執行個體與您的 Azure AD 租用戶或最接近區域 tooit hello 的區域。

比方說，如果您的 Azure AD 租用戶的區域是 hello 歐盟 (EU)，所有的應用程式 Proxy 連接器會使用服務執行個體 hello EU 中的 Azure 資料中心。 當您的使用者存取已發行的應用程式時，其流量會經歷 hello 應用程式 Proxy 服務執行個體，在這個位置。

## <a name="considerations-for-reducing-latency"></a>降低延遲的考量

所有 Proxy 解決方案都會在您的網路連線中造成延遲。 不論哪一個 proxy 或 VPN 解決方案選擇做為遠端存取解決方案，它一律包含一組啟用 hello 連接 tooinside 您的公司網路的伺服器。

組織通常包含其周邊網路中的伺服器端點。 使用 Azure AD Application Proxy，不過，流量流經 hello 雲端中的 hello proxy 服務時 hello 連接器位於公司網路。 不需要周邊網路。

hello 下一節包含的其他建議 toohelp 減少延遲更進一步。 

### <a name="connector-placement"></a>連接器放置

應用程式 Proxy 為您的租用戶位置選擇 hello 位置執行個體。 不過，您取得 toodecide tooinstall hello 連接器，讓您在 hello 電源 toodefine hello 延遲特性的網路流量。

Hello 應用程式 Proxy 服務設定，請詢問下列問題的 hello:

* Hello 應用程式位於何處？
* 在哪裡？ 大部分使用者都可以存取位於 hello 應用程式
* Hello 應用程式 Proxy 執行個體位於何處？
* 您已經有設定，例如 Azure ExpressRoute 或類似的 VPN 專用的網路連線 tooAzure 資料中心嗎？

hello 連接器 toocommunicate 使用 Azure 和您的應用程式 （步驟 2 和 3 在 hello 流量圖表），因此 hello hello 連接器會影響這些兩個連線的 hello 延遲的位置。 時評估 hello 放置 hello 連接器，請遵循點注意 hello:

* 如果您想 toouse Kerberos 限制委派 (KCD) 的單一登入，然後 hello 連接器必須的視野 tooa 資料中心。 此外，hello 連接器伺服器必須加入 toobe 網域。  
* 有疑問，hello 連接器接近 toohello 應用程式的安裝。

### <a name="general-approach-toominimize-latency"></a>一般方法 toominimize 延遲

您可以延遲降至最低 hello hello 端對端傳輸的最佳化每個網路連線。 可以將每個連線最佳化，方法為︰

* 減少 hello hello 兩端 hello 躍點的距離。
* 選擇 hello 正確網路 tootraverse。 比方說，是私人網路，而不是 hello 周遊公用網際網路可能更快，因為 toodedicated 連結。

如果您有 Azure 與您的公司網路之間的 VPN 或 ExpressRoute 專用的連結時，您可能會想 toouse 的。

## <a name="focus-your-optimization-strategy"></a>專注於最佳化策略

還有一些您可以執行您的使用者與 hello 應用程式 Proxy 服務之間的 toocontrol hello 連線。 使用者可以從家用網路、咖啡廳或不同的國家/地區存取您的應用程式。 相反地，您可以最佳化 hello 連線從 hello 應用程式 Proxy 服務 toohello 應用程式 Proxy 連接器 toohello 應用程式。 請考慮納入 hello 遵循您的環境中的模式。

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>模式 1: Put hello 連接器關閉 toohello 應用程式

位置 hello 連接器關閉 toohello 目標應用程式在 hello 客戶網路中。 因為 hello 連接器和應用程式關閉這項設定最小化在 hello 拓撲圖表中的步驟 3。 

如果您的連接器需要的視野 toohello 網域控制站，這個模式是有利的。 大部分的客戶會使用此模式，因為它非常適合大部分情節。 此模式也可以結合 hello 連接器 hello 服務之間的模式 2 toooptimize 流量。

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>模式 2︰利用 ExpressRoute 與公用對等互連

如果您有使用公用對等互連設定 ExpressRoute，您可以使用 hello 更快的 ExpressRoute 連線應用程式 Proxy 與 hello 連接器之間的流量。 hello 連接器是仍在網路上，關閉 toohello 應用程式。

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>模式 3︰利用具有私人對等互連的 ExpressRoute

如果有專用的 VPN 或 ExpressRoute 在 Azure 和公司網路之間設定私人對等互連，您會有另一個選項。 在此組態中，通常會被視為 hello 公司網路的延伸模組的 hello Azure 中的虛擬網路。 因此您可以安裝 hello 連接器在 hello Azure 資料中心，且仍能滿足 hello 低延遲要求的 hello 連接器-應用程式的連接。

延遲不會受到危害，因為流量會流經專用的連接。 您也可以改善應用程式 Proxy 服務的連接器延遲，因為 hello 連接器安裝在 Azure 資料中心關閉 tooyour Azure AD 租用戶位置。

![顯示安裝在 Azure 資料中心內之連接器的圖表](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>其他方法

雖然這篇文章的 hello 焦點是連接器放置，您也可以變更 hello 放置 hello 應用程式 tooget 較佳延遲的特性。

有愈來愈多的組織將其網路移至託管環境。 這樣可讓他們 tooplace 自己也其公司的網路的一部分，它仍然是 hello 網域內的託管環境中的應用程式。 在此情況下，hello hello 前幾節中討論的模式可以是 toohello 套用新的應用程式位置。 如果您正在考慮此選項，請參閱 [AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)。

此外，請考慮組織使用的連接器[連接器群組](active-directory-application-proxy-connectors.md)tootarget 應用程式中不同的位置和網路。 

## <a name="common-use-cases"></a>一般使用案例

在本節中，我們將逐步解說幾個常見案例。 假設該 hello Azure AD 租用戶 （和 proxy 因此為服務端點） 位於 hello United States (US)。 hello 考量討論這些使用案例也適用於 tooother 區域周圍 hello 地球。

這些情況下，我們將每個連線稱為「躍點」，並將它們編號以便於討論︰

- **1 個躍點**： 使用者 toohello 應用程式 Proxy 服務
- **2 個躍點**： 應用程式 Proxy 服務 toohello 應用程式 Proxy 連接器
- **3 個躍點**： 應用程式 Proxy 連接器 toohello 目標應用程式 

### <a name="use-case-1"></a>使用案例 1

**案例：** hello 應用程式是在組織網路中 hello US，與 hello 中的使用者相同的區域。 沒有 ExpressRoute 或 VPN hello Azure 資料中心與 hello 公司網路之間不存在。

**建議：**遵循模式 1，hello 上一節所述。 如需改良的延遲，請視需要考慮使用 ExpressRoute。

這是簡單的模式。 您可以最佳化躍點 3 放入 hello 連接器附近 hello 應用程式。 這是也合理的選擇，因為 hello 連接器通常會隨的視野 toohello 應用程式和 toohello datacenter tooperform KCD 作業。

![顯示的使用者、 proxy、 連接器和應用程式都位於 hello 我們的圖表](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>使用案例 2

**案例：** hello 應用程式是在組織網路中 hello US，與全域分散的使用者。 沒有 ExpressRoute 或 VPN hello Azure 資料中心與 hello 公司網路之間不存在。

**建議：**遵循模式 1，hello 上一節所述。 

同樣地，hello 常見的模式是 toooptimize 躍點 3，位置靠近 hello 應用程式的 hello 連接器。 躍點 3 不通常昂貴，如果它是所有內 hello 相同區域。 不過，躍點 1 可能更耗費資源，根據位置 hello 使用者，因為 hello 世界各地的使用者必須存取在 hello 美國 hello 應用程式 Proxy 執行個體。 值得注意的是，就散佈於全球的使用者而言，任何 Proxy 解決方案會有相似特性。

![顯示使用者全域擴展，但 hello proxy、 連接器和應用程式會位於 hello 我們的圖表](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>使用案例 3

**案例：** hello 應用程式是在組織網路中 hello 我們。 使用公用對等 ExpressRoute Azure 與 hello 公司網路之間不存在。

**建議：**遵循模式 1 和 2，hello 上一節所述。

首先，將關閉，可能 toohello 應用程式的 hello 連接器。 然後，hello 系統會自動會使用 ExpressRoute 的躍點 2。 

如果 hello ExpressRoute 連結使用公用對等互連，hello hello proxy 與 hello 連接器之間的流量流程透過該連結。 躍點 2 具有最佳化延遲。

![ExpressRoute 顯示 hello proxy 之間連接器的圖表](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>使用案例 4

**案例：** hello 應用程式是在組織網路中 hello 我們。 Azure 與 hello 公司網路之間不存在與私用對等 ExpressRoute。

**建議：**遵循模式 3，hello 上一節所述。

置於 hello Azure 資料中心會透過 ExpressRoute 私用對等體的連接的 toohello 公司網路中的 hello 連接器。 

hello 連接器可以放在 hello Azure 資料中心。 Hello 連接器仍然會有的視野 toohello 應用程式和 hello 資料中心透過 hello 私人網路，因為躍點 3 會維持最佳化。 此外，躍點 2 已進一步最佳化。

![顯示 hello 連接器中的 Azure 資料中心和 ExpressRoute hello 連接器與應用程式之間的圖表](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>使用案例 5

**案例：** hello 應用程式是在組織網路中含有 hello 應用程式 Proxy 執行個體和大部分的使用者在 hello hello EU，我們。

**建議：**附近 hello 應用程式的地方 hello 連接器。 因為美國使用者存取應用程式 Proxy 執行個體時所發生 toobe hello 中的相同的區域，躍點 1 不是太高成本。 躍點 3 已最佳化。 請考慮使用 ExpressRoute toooptimize 躍點 2。 

![顯示使用者和 proxy hello 美國、 hello 連接器與 hello EU 中的應用程式中的圖表](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

您也可以考慮在此情況下使用另一個變體。 如果 hello 組織中的大部分使用者都位於 hello 我們，機率是會以確認您的網路延伸 toohello 我們也。 Hello 連接器置於 hello 美國，並使用專用的 hello 公司內部網路列 toohello 應用程式在 hello EU。 如此一來，躍點 2 和躍點 3 便已最佳化。

![顯示 hello US、 hello EU 中應用程式中的使用者、 proxy 和連接器的圖表](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>後續步驟

- [啟用應用程式 Proxy](active-directory-application-proxy-enable.md)
- [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
- [啟用條件式存取](active-directory-application-proxy-conditional-access.md)
- [使用應用程式 Proxy 疑難排解您遇到的問題](active-directory-application-proxy-troubleshoot.md)
