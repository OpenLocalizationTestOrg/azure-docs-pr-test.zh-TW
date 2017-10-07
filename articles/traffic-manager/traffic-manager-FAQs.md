---
title: "aaaAzure Traffic Manager 的常見問題集 |Microsoft 文件"
description: "本文提供的解答 toofrequently 常見問題關於流量管理員"
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
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>流量管理員常見問題集 (FAQ)

## <a name="traffic-manager-basics"></a>流量管理員基本概念

### <a name="what-ip-address-does-traffic-manager-use"></a>「流量管理員」使用什麼 IP 位址？

中所述[Traffic Manager 的運作方式](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works)，Traffic Manager 會在 hello DNS 層級運作。 它會傳送 DNS 回應 toodirect 用戶端 toohello 適當的服務端點。 用戶端然後 toohello 服務端點直接連接，未透過 Traffic Manager。

因此，Traffic Manager 不針對用戶端 tooconnect 來提供端點或 IP 位址。 因此，如果您想要您的服務靜態 IP 位址，，必須設定在 hello 服務，不在 Traffic Manager 中。

### <a name="does-traffic-manager-support-sticky-sessions"></a>流量管理員是否支援「黏性」工作階段？

中所述[Traffic Manager 的運作方式](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works)，Traffic Manager 會在 hello DNS 層級運作。 它會使用 DNS 回應 toodirect 用戶端 toohello 適當的服務端點。 用戶端連接直接，未透過 Traffic Manager toohello 服務端點。 因此，Traffic Manager 不會看到 hello HTTP hello 用戶端和伺服器之間傳輸 hello。

此外，hello DNS 查詢流量管理員所收到 hello 來源 IP 位址所屬 toohello 遞迴 DNS 服務，不使用用戶端 hello。 因此，Traffic Manager 沒有方式 tootrack 個別用戶端，而且無法實作 '自黏' 工作階段。 這項限制是常見 tooall DNS 為基礎的流量管理系統而非特定 tooTraffic 管理員。

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>我在使用流量管理員時為何看到 HTTP 錯誤？

中所述[Traffic Manager 的運作方式](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works)，Traffic Manager 會在 hello DNS 層級運作。 它會使用 DNS 回應 toodirect 用戶端 toohello 適當的服務端點。 用戶端然後 toohello 服務端點直接連接，未透過 Traffic Manager。 流量管理員看不到用戶端與伺服器之間的 HTTP 流量。 因此，您看到的任何 HTTP 錯誤必定來自您的應用程式。 Hello 用戶端 tooconnect toohello 應用程式，所有的 DNS 解析步驟都已完成。 這包括 Traffic Manager 對應用程式流量 hello 任何互動。

進一步調查因此應該專注於 hello 應用程式中。

從用戶端 hello 瀏覽器傳送 hello HTTP 主機標頭是 hello 最常見的問題的來源。 請確定 hello 應用程式設定的 tooaccept hello 正確的主機標頭 hello 您使用的網域名稱。 如需使用端點 hello Azure 應用程式服務，請參閱[使用 Traffic Manager 的 Azure App Service 中設定 web 應用程式的自訂網域名稱](../app-service-web/web-sites-traffic-manager-custom-domain-name.md)。

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>使用 Traffic Manager 的 hello 效能影響為何？

中所述[Traffic Manager 的運作方式](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works)，Traffic Manager 會在 hello DNS 層級運作。 因為用戶端直接連接 tooyour 服務端點，所以沒有建立 hello 連接之後，使用流量管理員時所產生效能影響。

Traffic Manager 會與在 hello DNS 層級的應用程式整合，因為它需要插入 hello DNS 解析鏈結至其他 DNS 查閱 toobe。 hello 影響的 Traffic Manager DNS 解析時間是最小。 Traffic Manager 會使用全域網路的名稱伺服器，並使用[任一傳播](https://en.wikipedia.org/wiki/Anycast)網路 tooensure DNS 查詢都路由的 toohello 最接近可用的名稱伺服器。 此外，DNS 回應的快取表示 hello 使用 Traffic Manager 會產生其他 DNS 延遲套用只 tooa 分數的工作階段。

hello 效能方法路由流量 toohello 最接近的可用端點。 hello 最後結果就是該 hello 這個方法與相關聯的整體效能影響應該很小。 應該會增加任何的 DNS 延遲位移較低的網路延遲 toohello 端點。

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>我可以搭配「流量管理員」使用哪些應用程式通訊協定？

中所述[Traffic Manager 的運作方式](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works)，Traffic Manager 會在 hello DNS 層級運作。 Hello DNS 查閱完成之後，用戶端連線 toohello 應用程式端點直接，未透過 Traffic Manager。 因此，hello 連線可以使用任何應用程式通訊協定。 如果您選取 TCP 作為 hello 監視通訊協定，Traffic Manager 的端點健全狀況監視，才可以不使用任何應用程式通訊協定。 如果您選擇使用應用程式通訊協定驗證 toohave hello 健全狀況，hello 端點需要 toobe 無法 toorespond tooeither HTTP 或 HTTPS GET 要求。

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>我是否可以在流量管理員中使用「裸」網域名稱？

否。 hello DNS 標準不允許 Cname tooco-存在 hello 其他 DNS 記錄，具有相同名稱。 hello apex （或根） 的 DNS 區域一定會包含兩個預先存在的 DNS 記錄。hello SOA 和 hello 權威 NS 記錄。 這表示無法在 hello 區域的 apex 建立 CNAME 記錄，而不會違反 hello DNS 標準。

Traffic Manager 會需要 DNS CNAME 記錄 toomap hello 虛名 DNS 名稱。 例如，您將對應 www.contoso.com toohello Traffic Manager 設定檔 DNS 名稱 contoso.trafficmanager.net。 此外，hello Traffic Manager 設定檔會傳回第二個的 DNS CNAME tooindicate hello 用戶端應該連接至哪一個端點。

toowork 解決此問題，我們建議使用 hello naked 網域名稱 tooa 不同的 URL，然後可以使用 Traffic Manager 從 HTTP 重新導向 toodirect 流量。 例如，hello naked 網域 'contoso.com' 可以重新導向使用者 toohello CNAME 'www.contoso.com' 指向 toohello Traffic Manager DNS 名稱。

我們的功能待處理項目中追蹤了對「流量管理員」中裸網域的完整支援。 您可以[在我們的社群意見反應站投票](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly)，以表達您支持這項功能要求。

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>處理 DNS 查詢時，就 Traffic Manager 考慮 hello 用戶端的子網路位址嗎？ 
否，目前 Traffic Manager 會考慮只 hello 來源 IP 位址的 hello DNS 查詢收到，地理和效能的路由方法執行查詢時，通常是 hello DNS 解讀器，hello IP 位址。  
具體來說， [RFC 7871 – 用戶端在 DNS 查詢中的子網路](https://tools.ietf.org/html/rfc7871)提供[DNS (EDNS0) 的延伸模組機制](https://tools.ietf.org/html/rfc2671)其可以從解析程式支援它 tooDNS 伺服器傳遞 hello 用戶端的子網路位址是目前不支援在 Traffic Manager 中。 您可以透過我們的[社群意見反應站 (英文)](https://feedback.azure.com/forums/217313-networking) 來表達您支持這項功能要求。


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>什麼是 DNS TTL，以及它如何影響我的使用者？

DNS 查詢會落在 Traffic Manager，它會設定稱為 「 存留時間 (TTL) 的 hello 回應中的值。 這個值，其單位是以秒為單位，表示 tooDNS 上的解析程式下游多久 toocache 此回應。 雖然 DNS 解析程式不會保證 toocache 此結果中，快取它可讓他們關閉 hello life tooTraffic Manager DNS 伺服器的快取 toorespond tooany 後續查詢。 這會影響 hello 回應，如下所示：
- 較高的 TTL 會減少 hello 進入 hello Traffic Manager DNS 伺服器，因為提供的查詢數目為可計費的使用量，可以降低 hello 成本客戶的查詢數目。
- 較高的 TTL 可能會減少 hello 花的時間 toodo DNS 查閱。
- 較高的 TTL 也表示您的資料不會反映 hello 最新健全狀況，Traffic Manager 已取得資訊透過其探查的代理程式。

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>如何最高或最低可設定 Traffic Manager 回應 hello TTL？

您可以設定，在每個設定檔層級，hello DNS TTL toobe 做為 0 秒，最高為 2,147,483,647 秒 (hello 與相容的最大範圍[RFC 1035](https://www.ietf.org/rfc/rfc1035.txt ))。 0 表示下游的 DNS 解析程式不會快取查詢回應所有查詢都是 TTL 預期 tooreach hello Traffic Manager DNS 伺服器來進行解析。

## <a name="traffic-manager-geographic-traffic-routing-method"></a>流量管理員地理流量路由方法

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>地理路由派上用場的使用案例有哪些？ 
地理路由類型可用在任何案例中是 Azure 客戶需要的地方 toodistinguish 使用者根據地理區域。 例如，使用 hello 地理流量路由方式，您就能給予使用者從特定區域以外的其他區域的不同的使用者體驗。 另一個例子是符合本機資料主權規定，要求特定區域的使用者只能由該區域中的端點提供服務。

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Traffic Manager 所支援的地理路由 hello 區域有哪些？ 
您可以找到 hello Traffic Manager 時使用的國家/地區階層[這裡](traffic-manager-geographic-regions.md)。 此頁面會保留最新狀態的任何變更，而您也以程式設計方式可以擷取使用 hello hello 相同資訊[Azure Traffic Manager REST API](https://docs.microsoft.com/rest/api/trafficmanager/)。 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>流量管理員如何判斷使用者從何處執行查詢？ 
Traffic Manager 會查看 hello 來源 IP hello 查詢 （這可能是執行 hello 查詢代表 hello 使用者的本機 DNS 解析程式），並使用內部 IP tooregion 對應 toodetermine hello 位置。 此對應會更新變更的 hello 持續 tooaccount 網際網路。 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>這樣會保證 Traffic Manager 可以正確判斷 hello 確切地理位置中每個案例的 hello 使用者嗎？
否，Traffic Manager 無法保證我們推斷 hello 來源 IP 位址的 DNS 查詢從該 hello 地理區域永遠都會將對應 toohello 使用者的位置，因為 toohello 下列原因： 

- 首先，hello 先前常見問題集所述，hello 我們看到是 DNS 解析程式執行代表 hello 使用者 hello 查閱的來源 IP 位址。 Hello hello 使用者地理位置的良好 proxy hello hello DNS 解析程式的地理位置時，它也可以是不同定 hello DNS 解析程式服務和 hello 特定 DNS 解析程式服務的客戶已選擇 hello 耗用量toouse。 例如，位於馬來西亞客戶可以指定他們的裝置設定使用中新加坡其 DNS 伺服器可能會收到一個 DNS 解析程式服務中挑選 toohandle hello 查詢解析度，該使用者/裝置。 案例中，Traffic Manager 只能看見 hello 解析程式的 IP 位址，對應 toohello 新加坡位置。 此外，請參閱之前有關用戶端的子網路位址的常見問題集支援此頁面的 hello。

- 第二，Traffic Manager 會使用內部對應 toodo hello IP 位址 toogeographic 區域轉譯。 雖然此對應會驗證並更新持續 tooincrease 上其精確度和帳戶 hello 發展的本質 hello 網際網路，仍有 hello 可能性，我們的資訊不是所有的 hello 地理位置的精確表示hello IP 位址。


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>沒有實際位於端點需要 toobe hello hello 與相同的區域一個設定為地理路由？ 
否，hello hello 端點位置都會加入所在區域可以是對應的 tooit 沒有限制。 例如，美國中部 Azure 區域中的端點可以有來自印度導向 tooit 的所有使用者。

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>可以將指定的地理區域 tooendpoints 不是設定檔中的設定 toodo 地理路由？ 

是，如果不地理 hello 路由方式的設定檔，您可以使用 hello [Azure Traffic Manager REST API](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign 地理區域 tooendpoints 該設定檔中的。 在非地理路由類型設定檔的 hello 情況下，會忽略此設定。 如果您在稍後變更這類的設定檔 toogeographic 路由類型，Traffic Manager 可以使用這些對應。


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>為什麼我會收到錯誤時的現有的設定檔 tooGeographic toochange hello 路由方法？

在具有地理路由的設定檔的所有 hello 端點都需要 toohave 至少一個區域對應 tooit。 tooconvert 現有的設定檔 toogeographic 路由類型，您必須先 tooassociate 地理區域 tooall 其端點使用 hello [Azure Traffic Manager REST API](https://docs.microsoft.com/rest/api/trafficmanager/)之前變更 hello 路由輸入 toogeographic。 如果使用入口網站中，第一次刪除 hello 端點，變更 hello 設定檔 toogeographic hello 路由方法，然後新增 hello 端點，以及其地理區域的對應。 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>為什麼強烈建議客戶建立巢狀設定檔，而不是在啟用地理路由的設定檔下新增端點？ 

區域可以指派設定檔中的一個 tooonly 端點如果它使用地理路由類型。 如果該端點不是子連接的設定檔 tooit，具有的巢狀型別，如果該端點會處於狀況不良，Traffic Manager 會持續 toosend 流量 tooit 自 hello 不傳送任何流量不好的替代方式。 流量管理員 」 會執行不容錯移轉 tooanother 端點，即使 hello 區域指派 「 父 」 的 hello 區域指派 toohello 端點發生 （例如，如果擁有區域西班牙的端點，變成狀況不良，我們將無法容錯移轉 tooanother 狀況不良具有 hello 區域歐洲的端點指派 tooit）。 這是 tooensure Traffic Manager 方面 hello 地理界限的客戶的安裝程式在其設定檔。 tooget hello 優點容錯移轉 tooanother 端點當端點變成狀況不良時，建議您使用地理區域，指派 toonested 具有多個端點中，而不是個別端點的設定檔。 如此一來，如果中巢狀的 hello 子項設定檔失敗，流量的端點可以容錯移轉 tooanother 端點內 hello 相同巢狀化子系設定檔。

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>有支援這種路由類型的 hello API 版本的任何限制嗎？

可以，只有 2017年-03-01 的 API 版本和更新版本支援 hello 地理路由類型。 任何較舊的應用程式開發介面版本無法使用的 toocreated 的地理路由類型的設定檔或指派 tooendpoints 地理區域。 如果較舊的 API 版本使用的 tooretrieve 從 Azure 訂用帳戶的設定檔，不會傳回任何設定檔的地理路由類型。 此外，使用舊版 API 時，傳回的任何設定檔如果有已指派地理區域的端點，則不會顯示其地理區域指派。



## <a name="traffic-manager-endpoints"></a>流量管理員端點

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>可以將流量管理員用於來自多個訂用帳戶的端點嗎？

來自多個訂用帳戶的端點不能與 Azure Web 應用程式搭配使用。 Azure Web Apps 規定 Web Apps 使用的任何自訂網域名稱只能在單一訂用帳戶內使用。 它不是從多個訂閱 hello 與可能 toouse Web 應用程式相同的網域名稱。

對於其他端點型別，就可能 toouse Traffic Manager 具有一個以上的訂用帳戶的端點。 資源管理員 中，從任何訂用帳戶的端點可以加入 tooTraffic 管理員 中，只要設定 hello Traffic Manager 設定檔的 hello 使用者擁有讀取權限 toohello 端點。 使用 [Azure Resource Manager 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)可以授與這些權限。


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>我可以使用流量管理員來設定雲端服務「預備」位置嗎？

是。 雲端服務「預備」位置可在流量管理員中設定為外部端點。 健康情況檢查仍會收費 hello Azure 端點速率。 正在使用中的 hello 外部端點的型別，因為變更 toohello 基礎服務不會收取自動。 與外部端點，hello 雲端服務已停止或刪除時，無法偵測 Traffic Manager。 因此，hello Traffic Manager 會持續健全狀況檢查的計費 hello 端點已停用或刪除為止。

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>流量管理員是否支援 IPv6 端點？

流量管理員目前不提供 IPv6 定址的名稱伺服器。 不過，Traffic Manager 仍可以使用 IPv6 連接 tooIPv6 端點的用戶端。 用戶端不會進行 DNS 要求直接 tooTraffic 管理員。 相反地，hello 用戶端會使用遞迴 DNS 服務。 僅支援 IPv6 的用戶端傳送要求透過 IPv6 toohello 遞迴 DNS 服務。 然後 hello 遞迴服務應能 toocontact hello Traffic Manager 名稱伺服器使用 IPv4。

Traffic Manager 的回應 hello 端點 hello DNS 名稱。 toosupport IPv6 端點 DNS AAAA 記錄指標 hello 端點 DNS 名稱 toohello IPv6 位址必須存在。 流量管理員健康情況檢查僅支援 IPv4 位址。 hello 服務必須在 hello tooexpose IPv4 端點相同的 DNS 名稱。

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>可以使用 Traffic Manager hello 中的多個 Web 應用程式使用相同的區域？

通常，Traffic Manager 會使用的 toodirect 流量 tooapplications 部署在不同的區域。 不過，它也可用位置的應用程式有多個部署 hello 中相同的區域。 hello Azure Traffic Manager 端點不允許多個 Web 應用程式端點 hello 從相同的 Azure 區域 toobe 加入 toohello 相同 Traffic Manager 設定檔。

##  <a name="traffic-manager-endpoint-monitoring"></a>流量管理員端點監視

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>為 Traffic Manager 彈性 tooAzure 區域失敗？

Traffic Manager 是高度可用的應用程式在 Azure 中的 hello 傳遞的重要元件。
toodeliver 高可用性，Traffic Manager 必須有過高的層級的可用性和彈性 tooregional 失敗。

根據設計，Traffic Manager 元件是彈性 tooa 完全失敗的任何 Azure 區域。 此彈性適用於 tooall Traffic Manager 元件： hello DNS 名稱伺服器、 hello API、 hello 儲存層和 hello 端點監視服務。

在整個 Azure 地區中斷的罕見事件中 hello，Traffic Manager 通常是預期的 toocontinue toofunction。 部署多個 Azure 區域中的應用程式可以依賴 Traffic Manager toodirect 流量 tooan 可用其應用程式執行個體。

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>資源群組位置 hello 選擇如何影響 Traffic Manager？

流量管理員是單一全域服務。 不是區域性。 hello 所選擇的資源群組位置可讓部署該資源群組中沒有差異 tooTraffic 管理員設定檔。

Azure 資源管理員需要所有的資源群組 toospecify 位置，這會決定部署資源的資源群組中的 hello 預設位置。 當您建立流量管理員設定檔時，它會建立在資源群組中。 所有的 Traffic Manager 設定檔使用**全域**作為其位置，覆寫 hello 資源群組的預設值。

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>我要如何判斷 hello 的每個端點的目前健全狀況？

hello 目前監視的每個端點的狀態，在加法 toohello 整體的設定檔，會顯示在 hello Azure 入口網站。 這項資訊也可以使用透過 hello 流量監視[REST API](https://msdn.microsoft.com/library/azure/mt163667.aspx)， [PowerShell cmdlet](https://msdn.microsoft.com/library/mt125941.aspx)，和[跨平台 Azure CLI](../cli-install-nodejs.md)。

Azure 不提供過去端點相關的歷程記錄資訊的相關變更 tooendpoint 健全狀況的健全狀況或 hello 能力 tooraise 警示。

### <a name="can-i-monitor-https-endpoints"></a>我可以監視 HTTPS 端點嗎？

是。 流量管理員支援透過 HTTPS 探查。 設定**HTTPS**做為 hello 監視設定中的 hello 通訊協定。

流量管理員無法提供任何憑證驗證，包括：

* 不會驗證伺服器端憑證
* 不支援 SNI 伺服器端憑證
* 不支援用戶端憑證

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>即使我的應用程式不支援 HTTP 或 HTTPS 也可以使用流量管理員嗎？

是。 您可以指定 TCP 通訊協定和 Traffic Manager 監視的 hello 可以起始 TCP 連線，或等候 hello 端點的回應。 如果 hello 端點回覆 toohello 連線要求與回應 tooestablish hello 連接，hello 逾時時間內期間，則該端點會標示為狀況良好。

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>使用 TCP 監視時從 hello 端點需要哪些特定回應？

使用 TCP 監視時，Traffic Manager 會開始傳送 SYN 三向 TCP 交握要求在 tooendpoint hello 指定的連接埠。 接著會等待一段時間 （如 hello 逾時設定中指定） 的回應 hello 端點。 如果 hello 端點回應 toohello SYN SYN ACK 回應 hello 監視設定，在指定的 hello 逾時期間內要求，則該端點視為狀況良好。 收到 hello SYN ACK 回應時，如果 hello Traffic Manager 重設回與 RST 回應 hello 連線。

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>流量管理員將我的使用者從狀況不良的端點移開時間有多快？

Traffic Manager 所提供多項設定，可協助您 toocontrol hello 容錯移轉行為，您的 Traffic Manager 設定檔，如下所示：
- 您可以指定 hello 更頻繁地藉由設定 Traffic Manager 探查 hello 端點 hello 探查間隔，在 10 秒。 這可確保能夠立即偵測到狀況不良的任何端點。 
- 您可以指定 toowait 健全狀況檢查要求之前逾時的時間長度 （最小逾時值是 5 秒）。
- 您可以指定 hello 端點標示為狀況不良之前，可能會發生多少次失敗。 這個值可以是下限為 0，第一個的健康情況檢查在哪一個案例的 hello 端點標示為狀況不良時失敗的 hello。 不過，使用 hello 所容許之失敗次數的 hello 最小值為 0 可能會導致 tooendpoints 取得離輪替循環，因為 tooany 的探查 hello 時間可能會發生的暫時性問題。
- 您可以指定為 0 的 hello DNS 回應 toobe hello 存留時間 (TTL)。 這麼做會表示的 DNS 解析程式無法快取 hello 回應，每個新的查詢會取得包含最新健全狀況資訊 hello 回應該 hello Traffic Manager 有。

透過使用這些設定，Traffic Manager 可以提供容錯移轉在 10 秒後端點會處於狀況不良，並針對 hello 對應的設定檔進行 DNS 查詢。

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>如何為設定檔中不同的端點指定不同監視設定？

流量管理員監視設定是在各個設定檔層級。 如果您需要 toouse 不同的監視設定為只能有一個端點時，可以透過讓該端點，如[巢狀設定檔](traffic-manager-nested-profiles.md)其監視的設定會與不同 hello 父系設定檔。

### <a name="what-host-header-do-endpoint-health-checks-use"></a>端點健全狀況檢查使用哪一個主機標頭？

流量管理員在 HTTP 和 HTTPS 的健康狀態檢查中使用主機標頭。 hello Traffic Manager 所使用的主機標頭是 hello hello hello 設定檔中設定的端點目標名稱。 無法從 hello 目標屬性分別指定 hello hello 主機標頭中使用的值。

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>從中 hello 健康情況檢查源自 hello IP 位址有哪些？

hello 下列清單包含要從中 Traffic Manager 的健康情況檢查可能源自 hello IP 位址。 您可以使用此清單 tooensure，來自這些 IP 位址的連入連線可以在 hello 端點 toocheck 其健全狀況狀態。

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>多少健全狀況檢查 toomy 端點應該會有從 Traffic Manager？

hello 數目 Traffic Manager 健全狀況檢查到達您的端點取決於下列 hello:
- hello hello 監視間隔為設定的值 （較小的間隔表示在任何給定的時間期間內登陸在您的端點上的更多要求）。
- hello 位置 hello 健康情況檢查產生 （hello IP 位址與其中預期這些檢查會列在 hello 前面常見問題集） 的位置數目。

## <a name="traffic-manager-nested-profiles"></a>流量管理員巢狀設定檔

### <a name="how-do-i-configure-nested-profiles"></a>如何設定巢狀設定檔？

巢狀 流量管理員設定檔可以使用這兩個 hello Azure 資源管理員來設定和 hello 傳統 Azure REST Api，Azure PowerShell cmdlet 和跨平台 Azure CLI 命令。 它們也支援透過 hello 新版 Azure 入口網站。 它們不支援 hello 傳統入口網站中。

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>流量管理員支援幾層巢狀結構？

您可以巢狀深度 too10 層級上的設定檔。 不允許使用「迴圈」。

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>可以我混合其他端點類型巢狀的子系的設定檔，請在 hello 相同 Traffic Manager 設定檔嗎？

是。 對於在設定檔內如何結合不同類型的端點，並沒有任何限制。

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Hello 計費模型如何套用的巢狀設定檔？

使用巢狀設定檔並沒有計價上的負面影響。

流量管理員計費有兩個要素︰端點健康狀態檢查和數百萬個 DNS 查詢

* 端點健康情況檢查︰當子設定檔被設定為父設定檔中的端點時，並不會針對該子設定檔收費。 監視的 hello 子項設定檔中的 hello 端點在 hello 計費一般方式。
* DNS 查詢：每個查詢只計算一次。 針對傳回端點的子項設定檔從父設定檔的查詢會計算針對 hello 父系設定檔。

完整的詳細資訊，請參閱 hello [Traffic Manager 定價頁面](https://azure.microsoft.com/pricing/details/traffic-manager/)。

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>巢狀設定檔是否會對效能造成影響？

沒有。 使用巢狀設定檔不會影響效能。

hello Traffic Manager 名稱伺服器在內部周遊 hello 設定檔的階層，在處理每個 DNS 查詢。 DNS 查詢 tooa 父系設定檔可以接收與端點的 DNS 回應中的子項設定檔。 不論您使用單一設定檔或巢狀設定檔，都只會使用單一 CNAME 記錄。 沒有任何需要 toocreate hello 階層中每個設定檔的 CNAME 記錄。

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Traffic Manager 如何計算 hello 的父系設定檔中的巢狀端點的健全狀況？

hello 父系設定檔不會直接執行 hello 子系上的健康情況檢查。 相反地，hello hello 子項設定檔的端點健全狀況是使用的 toocalculate hello hello 子項設定檔的整體健全狀況。 這項資訊會傳播 hello 巢狀設定檔階層 toodetermine hello 健全狀況的巢狀的 hello 端點。 hello 父系設定檔會使用此彙總健全狀況 toodetermine 是否 hello 流量可以成為導向的 toohello 子系。

hello 下表描述 hello 行為流量管理員 」 的健全狀況檢查有巢狀的端點。

| 子設定檔監視狀態 | 父端點監視狀態 | 注意事項 |
| --- | --- | --- |
| 已停用。 hello 子系的設定檔已停用。 |已停止 |停止 hello 父系端點狀態，不會停用。 hello 停用狀態保留來指出您已停用 hello 父系設定檔中的 hello 端點。 |
| 已降級。 至少有一個子設定檔端點的狀態為「已降級」。 |Online: hello hello 子系的設定檔中的線上端點數目至少為 hello MinChildEndpoints 的值。<BR>CheckingEndpoint: hello hello 子項設定檔中的線上 」 加上 CheckingEndpoint 端點數目至少為 hello MinChildEndpoints 的值。<BR>已降級︰其他情況。 |流量會路由的 tooan CheckingEndpoint 狀態的端點。 如果 MinChildEndpoints 設定太高，則 hello 端點一定會降級。 |
| 線上。 至少有一個子設定檔端點處於「線上」狀態。 沒有端點處於 hello 降級 」 狀態。 |請參閱上方。 | |
| CheckingEndpoints。 至少有一個子設定檔端點是 'CheckingEndpoint'。 沒有端點是「線上」或「已降級」。 |同上。 | |
| 非使用中。 所有子設定檔端點不是「已停用」就是「已停止」，或者此設定檔沒有任何端點 |已停止 | |

## <a name="next-steps"></a>後續步驟：
- 深入了解「流量管理員」的 [端點監視和自動容錯移轉](../traffic-manager/traffic-manager-monitoring.md)。
- 深入了解「流量管理員」的 [流量路由方法](../traffic-manager/traffic-manager-routing-methods.md)。