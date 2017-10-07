---
title: "aaaWhat 是 Traffic Manager |Microsoft 文件"
description: "本文將協助您了解流量管理員為何，以及它是否 hello 右流量路由適合您的應用程式"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>流量管理員概觀

Microsoft Azure Traffic Manager 可讓您 toocontrol hello 使用者流量分散的服務端點的不同資料中心內。 流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。 您也可以將流量管理員使用於外部、非 Azure 端點。

Traffic Manager 會使用 hello 網域名稱系統 (DNS) toodirect 用戶端要求 toohello 最適當的端點和 hello 健全狀況的 hello 端點的流量路由方法為基礎。 Traffic Manager 所提供的範圍[流量路由方法](traffic-manager-routing-methods.md)和[端點監視選項](traffic-manager-monitoring.md)toosuit 不同的應用程式需求和自動容錯移轉模式。 Traffic Manager 是彈性 toofailure，包括整個 Azure 地區的 hello 失敗。

## <a name="traffic-manager-benefits"></a>流量管理員的優點

流量管理員可協助您：

* **提高重要應用程式的可用性**

    流量管理員藉由監視端點，以及在端點停止運作時提供自動容錯移轉功能，為重要的應用程式提供高可用性。

* **提升高效能應用程式的回應能力**

    Azure 可讓您 toorun 雲端服務或網站在 hello 世界各地位於資料中心。 Traffic Manager 可以改善應用程式回應與 hello 網路延遲最小 hello 用戶端導向流量 toohello 端點。

* **在不需要停機的情況下執行服務維護**

    您可以在您的應用程式執行規劃的維護作業，而不需要停機。 Hello 維護進行中時，traffic Manager 將導向流量 tooalternative 端點。

* **結合內部部署和雲端應用程式**

    Traffic Manager 支援的外部，非 Azure 端點，讓它 toobe 搭配混合式雲端和內部部署，包括 hello 「 高載到雲端，""移轉到雲端，」 和 「 容錯移轉到雲端 」 案例。

* **大型複雜部署的流量分配**

    使用[巢狀 流量管理員設定檔](traffic-manager-nested-profiles.md)、 流量路由方法可以結合的 toocreate 複雜和彈性的規則 toosupport hello 需要的較大且較為複雜的部署。

## <a name="how-traffic-manager-works"></a>流量管理員的運作方式

Azure Traffic Manager 可讓您的流量 toocontrol hello 分配在應用程式端點。 端點是裝載於 Azure 內部或外部的任何網際網路對向服務。

流量管理員提供兩大優點︰

1. 根據數個 tooone 流量分散[流量路由方法](traffic-manager-routing-methods.md)
2. [連續監視端點健康狀態](traffic-manager-monitoring.md) 以及在端點失敗時自動容錯移轉

當用戶端嘗試 tooconnect tooa 服務時，它必須先解決 hello 的 hello 服務 tooan IP 位址的 DNS 名稱。 hello 用戶端接著會連線 toothat IP 位址 tooaccess hello 服務。

**hello 最重要的點 toounderstand 是 Traffic Manager 可在 hello DNS 層級。**  Traffic Manager 會使用 DNS toodirect 用戶端 toospecific 服務端點的 hello 流量路由方法的 hello 規則為基礎。 用戶端連線 toohello 選取端點**直接**。 流量管理員不是 Proxy 或閘道。 Traffic Manager 不會看到 hello hello 用戶端與 hello 服務之間傳送的流量。

### <a name="traffic-manager-example"></a>流量管理員範例

Contoso Corp 開發出新的合作夥伴入口網站。 此入口網站中的 hello URL 為 https://partners.contoso.com/login.aspx。 hello 應用程式裝載於 Azure 的三個區域。 tooimprove 可用性和全域效能最大化時，它們使用 Traffic Manager toodistribute 用戶端流量 toohello 最接近可用端點。

tooachieve 此組態中，完成下列步驟的 hello:

1. 部署三個服務執行個體。 這些部署的 hello DNS 名稱為 'contoso us.cloudapp.net'、 'contoso eu.cloudapp.net' 和 'contoso asia.cloudapp.net'。
2. 建立名為 'contoso.trafficmanager.net'，Traffic Manager 設定檔，並且設定該 toouse hello 「 效能 」 流量路由方法 hello 三個端點之間。
* 設定其虛名網域名稱、 'partners.contoso.com'、 toopoint too'contoso.trafficmanager.net'，使用 DNS CNAME 記錄。

![流量管理員 DNS 組態][1]

> [!NOTE]
> 使用虛名網域與 Azure 流量管理員時，您必須使用 CNAME toopoint 您虛名網域名稱 tooyour Traffic Manager 網域名稱。 DNS 標準不允許您網域的 toocreate 在 hello 'apex' CNAME （或根）。 因此，您無法建立 'contoso.com' 的 CNAME (有時稱為「裸」網域)。 您只能為 'contoso.com' 下的網域建立 CNAME，例如 'www.contoso.com'。 這項限制 toowork，建議您使用簡單 HTTP 要求重新導向 toodirect 'contoso.com' tooan 替代名稱，例如 'www.contoso.com'。

### <a name="how-clients-connect-using-traffic-manager"></a>用戶端連接如何使用流量管理員

當用戶端要求 hello 頁面 https://partners.contoso.com/login.aspx 從 hello 上述範例中，繼續進行，hello 用戶端會執行下列步驟 tooresolve hello DNS 名稱的 hello，並建立連接：

![使用流量管理員建立連接][2]

1. 傳送 DNS 查詢 tooits 設定遞迴 DNS 服務 tooresolve hello 名稱 'partners.contoso.com' hello 用戶端。 遞迴 DNS 服務 (有時稱為「本機 DNS」服務) 不直接裝載 DNS 網域。 相反地，hello 用戶端 off-loads hello 工作的連絡 hello 各種授權的 DNS 服務 hello 所需的網際網路 tooresolve DNS 名稱。
2. tooresolve hello DNS 名稱，hello 遞迴 DNS 服務尋找 hello 'contoso.com' 網域 hello 名稱伺服器。 然後，它會連絡這些名稱伺服器 toorequest hello 'partners.contoso.com' DNS 記錄。 hello contoso.com 的 DNS 伺服器會傳回指向 toocontoso.trafficmanager.net hello CNAME 記錄。
3. 接下來，hello 遞迴 DNS 服務會尋找 hello 名稱伺服器 hello 'trafficmanager.net' 網域中所提供的 hello Azure Traffic Manager 服務。 它接著會傳送 hello 'contoso.trafficmanager.net' DNS 記錄 toothose 要求 DNS 伺服器。
4. hello Traffic Manager 名稱伺服器接收 hello 要求。 它們會根據下列項目來選擇端點︰

    - 每個端點設定的 hello 狀態 （已停用的端點不會傳回）
    - hello 的每個端點，由 hello Traffic Manager 健全狀況所決定的目前健全狀況檢查。 如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。
    - hello 選擇流量路由方法。 如需詳細資訊，請參閱[流量管理員路由方法](traffic-manager-routing-methods.md)。

5. 選擇 hello 端點會傳回其他 DNS CNAME 記錄。 在此例子中，我們假設傳回 contoso us.cloudapp.net。
6. 接下來，hello 遞迴 DNS 服務尋找 hello 'cloudapp.net' 網域 hello 名稱伺服器。 它會連絡這些名稱伺服器 toorequest hello 'contoso us.cloudapp.net' DNS 記錄。 會傳回包含 hello hello 美國為基礎的服務端點的 IP 位址的 DNS 'A' 記錄。
7. hello 遞迴 DNS 服務會合併 hello 結果，並傳回單一的 DNS 回應 toohello 用戶端。
8. hello 用戶端收到 hello 的 DNS 結果，並連接 toohello IP 位址。 hello 用戶端連線直接，未透過 Traffic Manager toohello 應用程式服務端點。 因為這是 HTTPS 端點，hello 用戶端執行 hello 必要的 SSL/TLS 信號交換，，然後提出 HTTP GET 要求 hello ' / login.aspx' 頁面。

hello 遞迴 DNS 服務會快取收到 hello DNS 回應。 hello hello 用戶端裝置上的 DNS 解析程式也會快取 hello 結果。 快取可讓後續的 DNS 查詢 toobe 來使用 hello 快取中的資料，而非其他的名稱伺服器查詢更快速地回應。 hello hello 快取持續時間取決於每個 DNS 記錄 hello '-存留時間' (TTL) 屬性。 較短的值造成更快的快取過期，因此多個往返 toohello Traffic Manager 名稱伺服器。 較長的值，表示可能需要較長的 toodirect 流量從失敗的端點。 Traffic Manager 可讓您 tooconfigure hello TTL 用於 Traffic Manager DNS 回應 toobe 為 0 秒，最高為 2,147,483,647 秒 (hello 與相容的最大範圍[RFC 1035](https://www.ietf.org/rfc/rfc1035.txt))，讓您 toochoose hello 值最佳平衡 hello 應用程式的需求。

## <a name="pricing"></a>價格

如需定價資訊，請參閱[流量管理員定價](https://azure.microsoft.com/pricing/details/traffic-manager/)。

## <a name="faq"></a>常見問題集

如需流量管理員的常見問題集，請參閱[流量管理員常見問題集](traffic-manager-FAQs.md)

## <a name="next-steps"></a>後續步驟

深入了解「流量管理員」的 [端點監視和自動容錯移轉](traffic-manager-monitoring.md)。

深入了解「流量管理員」的 [流量路由方法](traffic-manager-routing-methods.md)。

深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

