---
title: "流量管理員-aaaAzure 流量路由方式 |Microsoft 文件"
description: "此文章可協助您了解流量管理員使用 hello 不同的流量路由方法"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>流量管理員路由方法

Azure Traffic Manager 支援四個流量路由方法 toodetermine 如何 tooroute 的網路流量 toohello 各種服務端點。 Traffic Manager hello 流量路由方法 tooeach DNS 查詢套用它所接收。 hello 流量路由方法會判斷哪一個端點傳回 hello DNS 回應中。

流量管理員中提供四種流量路由方法：

* **[優先順序](#priority):**選取**優先順序**當您想讓所有流量，toouse 主要服務端點，並提供備份以防主要 hello 備份端點都無法使用。
* **[加權](#weighted):**選取**加權**當您想 toodistribute 流量分配一組的端點，可能是平均或相應 tooweights，您所定義。
* **[效能](#performance):**選取**效能**當您在不同地理位置擁有端點，且您想要依據 hello 最低的網路延遲的終端使用者 toouse hello 「 最靠近 」 端點。
* **[地理](#geographic):**選取**地理**其 DNS 查詢，讓使用者導向的 toospecific 端點 （Azure、 外部、 或巢狀） 的地理位置為基礎所發出。 這讓 Traffic Manager 的客戶 tooenable 的情況下知道使用者的地理區域，和路由，根據重要。 例如，遵守資料主權規定、內容和使用者經驗的當地語系化，以及測量來自不同區域的流量。

所有流量管理員設定檔都支援監視端點健康狀態和自動容錯移轉。 如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。 單一「流量管理員」設定檔只能使用一個流量路由方法。 您可以隨時為您的設定檔選取不同的流量路由方法。 變更會在 1 分鐘內套用，不會造成任何停機時間。 透過使用巢狀「流量管理員」設定檔可以將流量路由方法加以結合。 巢狀結構啟用精密且更有彈性流量路由設定符合 hello 較大且複雜的應用程式的需求。 如需詳細資訊，請參閱 [巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。

## <a name = "priority"></a>優先順序流量路由方法

組織經常希望 tooprovide 可靠性的服務部署一或多個備份的服務，萬一主要服務效能降低。 hello 'Priority' 流量路由方法，可讓 Azure 客戶 tooeasily 實作此容錯移轉模式。

![Azure 流量管理員「優先順序」流量路由方法][1]

hello Traffic Manager 設定檔包含服務端點的優先順序的清單。 根據預設，Traffic Manager 會傳送所有流量 toohello 主要 （最高優先權） 端點。 如果 hello 主要端點無法使用，Traffic Manager 路由 hello 流量 toohello 第二個端點。 如果無法使用這兩個 hello 主要和次要端點，則 hello 流量會傳送 toohello，第三個，依此類推。 Hello 端點的可用性會根據設定 hello 狀態 （啟用或停用） 和 hello 持續的端點監視。

### <a name="configuring-endpoints"></a>設定端點

使用 Azure 資源管理員中，您可以設定每個端點使用 hello 'priority' 屬性的 hello 端點優先順序。 這個屬性的值介於 1 到 1000 之間。 值越低代表優先順序越高。 端點無法共用優先順序值。 設定 hello 屬性是選擇性的。 當省略，則會使用 hello 端點順序為基礎的預設優先權。

##<a name = "weighted"></a>加權流量路由方法
hello '加權' 流量路由方法可讓您 toodistribute 流量平均或 toouse 預先定義的加權。

![Azure 流量管理員「加權」流量路由方法][2]

在 hello 加權流量路由方法中，您可以指派 hello Traffic Manager 設定檔設定中的加權 tooeach 端點。 hello 加權值是從 1 too1000 的整數。 這是選擇性參數。 如果省略，流量管理員會使用預設權數 '1'。

針對每個收到的 DNS 查詢，流量管理員會隨機選擇可用的端點。 選擇端點的 hello 機率根據 hello 權重 tooall 可用的端點。 相同加權跨甚至流量發佈中的所有端點結果使用 hello。 在特定端點上使用高或較低的加權值會導致傳回頻率 hello DNS 回應中的這些端點 toobe。

加權的 hello 方法可讓某些案例中很有用：

* 漸進應用程式升級： 配置某百分比的流量 tooroute tooa 新端點，並逐漸增加時間 too100%中的 hello 流量。
* 應用程式移轉 tooAzure： 建立 Azure 和外部端點的設定檔。 調整 hello 端點 tooprefer hello 新端點的 hello 的權數。
* 雲端高載以取得額外的容量： 快速展開 hello 雲端至內部部署，將它放入 Traffic Manager 設定檔的後面。 當您需要額外容量 hello 雲端中的時，您可以加入或啟用更多端點並指定哪個流量部分會 tooeach 端點。

hello 資源管理員的 Azure 入口網站支援 hello 設定加權的流量路由。  您可以設定使用 hello 資源管理員版本的 Azure PowerShell、 CLI，然而 hello REST Api 的加權。

它是重要 toounderstand DNS 回應所快取的用戶端，並根據 hello 用戶端 hello 遞迴 DNS 伺服器會使用 tooresolve DNS 名稱。 此快取可能會影響加權的流量分配。 用戶端與遞迴 DNS 伺服器的 hello 數目較為大量時，流量發佈如預期般運作。 不過，當用戶端或遞迴 DNS 伺服器的 hello 數目很小，快取可能會大幅扭曲 hello 流量分配。

常見使用案例包括：

* 開發與測試環境
* 應用程式間通訊
* 以較小的使用者群為對象的應用程式，有共同的遞迴 DNS 基礎結構 (例如，透過 Proxy 連接的公司員工)

這些 DNS 快取效果是常見 tooall DNS 為基礎的流量路由系統，不只是 Azure Traffic Manager。 在某些情況下，明確地清除 hello DNS 快取可能會提供因應措施。 在其他情況下，使用替代的流量路由方法可能更為合適。

## <a name = "performance"></a>效能流量路由方法

Hello 地球跨部署在兩個或多個位置的端點，可以增進 hello 路由流量 toohello 位置 '最接近' tooyou 許多應用程式回應能力。 hello 「 效能 」 流量路由方法提供這項功能。

![Azure 流量管理員「效能」流量路由方法][3]

hello '靠近' 的端點不一定是最接近地理距離的測量。 相反地，hello 「 效能 」 流量路由方法會判斷 hello 最靠近的端點，藉由測量網路延遲。 Traffic Manager 會維護網際網路延遲表格 tootrack hello 來回時間 IP 位址範圍與每個 Azure 資料中心之間。

Traffic Manager 會查閱 hello 連入 DNS 要求 hello 網際網路延遲表格中的 hello 來源 IP 位址。 Traffic Manager 會在 hello hello 延遲最低的 IP 位址範圍，則在 hello DNS 回應中傳回該端點的 Azure 資料中心中選擇的可用端點。

如[流量管理員的運作方式](traffic-manager-overview.md#how-traffic-manager-works)中所述，流量管理員不會直接從用戶端接收 DNS 查詢。 相反地，DNS 查詢來自 hello 用戶端會設定的 toouse hello 遞迴 DNS 服務。 因此，hello IP 位址使用 toodetermine hello '最接近' 端點不是 hello 用戶端的 IP 位址，但它是 hello hello 遞迴 DNS 服務 IP 位址。 在實務上，此 IP 位址是好 hello 用戶端 proxy。


Traffic Manager 定期更新 hello 中變更的網際網路延遲表格 tooaccount hello 全域網際網路和新的 Azure 區域。 不過，應用程式的效能而異根據負載的即時變化 hello 網際網路。 效能流量路由不會監視特定服務端點上的負載。 不過，如果端點變得無法使用，流量管理員就不會將它加入 DNS 查詢回應中。


點 toonote:

* 如果您的設定檔包含多個端點 hello 相同的 Azure 區域，然後 Traffic Manager 分散流量平均分散在該區域中的 hello 可用端點。 如果您在某個區域內偏好採用不同的流量分配，您可以使用[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。
* 如果啟用中最接近的 hello 端點的所有 Azure 地區降級，Traffic Manager 會將流量 toohello 端點移 hello 下一個最接近 Azure 區域中。 如果您想 toodefine 慣用的容錯移轉順序，請使用[巢狀 流量管理員設定檔](traffic-manager-nested-profiles.md)。
* 當使用外部端點或巢狀的端點 hello 效能流量路由方式，您會需要 toospecify hello 位置，這些端點。 選擇 hello Azure 地區最接近 tooyour 部署。 這些位置是 hello hello 網際網路延遲表格所支援的值。
* 選擇 hello 端點的 hello 演算法是具決定性的。 重複相同的用戶端會從 hello 的 DNS 查詢導向 toohello 相同的端點。 一般而言，用戶端在漫遊時會使用不同的遞迴 DNS 伺服器。 hello 用戶端可能是路由的 tooa 不同端點。 路由可能也會受到更新 toohello 網際網路延遲表格。 因此，hello 效能流量路由方法不保證會在用戶端一律會路由傳送 toohello 相同的端點。
* 當 hello 網際網路延遲表格變更時，您可能會注意到某些用戶端會導向的 tooa 不同端點。 只要取得最新的延遲資料，此路由變更會更精確。 這些更新是不可或缺的 toomaintain hello 精確度效能流量路由為 hello 持續發展，網際網路。

## <a name = "geographic"></a>地理流量路由方法

Traffic Manager 設定檔可以是地理路由方法，因此使用者會被導向 toospecific 端點 （Azure、 外部或巢狀） 為基礎的地理位置的 DNS 查詢來自設定的 toouse hello。 這讓 Traffic Manager 的客戶 tooenable 的情況下知道使用者的地理區域，和路由，根據重要。 例如，遵守資料主權規定、內容和使用者經驗的當地語系化，以及測量來自不同區域的流量。
地理路由設定檔時，每個端點相關聯的設定檔需要 toohave 指派的地理區域 tooit 一組。 地理區域可以達到下列細微層級 
- 世界 – 任何區域
- 地區分組 – 例如非洲、中東、澳大利亞/太平洋等 
- 國家/地區 – 例如愛爾蘭、秘魯、香港特別行政區等 
- 州/省 – 例如美國加州、澳大利亞昆士蘭、加拿大亞伯達省等 (請注意︰僅澳大利亞、加拿大、英國和美國的州/省才支援此細微層級)。

當區域的一組指派 tooan 端點時，從這些區域的任何要求會取得路由唯一 toothat 端點。 Traffic Manager 會使用 hello DNS 查詢 toodetermine hello 區域的使用者從查詢 – 這通常是 hello IP 位址進行 hello 查詢代表 hello 使用者 hello 本機 DNS 解析程式的 hello 來源 IP 位址。  

![Azure 流量管理員「地理」流量路由方法](./media/traffic-manager-routing-methods/geographic.png)

Traffic Manager 會讀取 hello DNS 查詢 hello 來源 IP 位址，並決定來自哪一個地理區域。 如果沒有這個對應的地理區域 tooit 的端點，它接著會尋找 toosee。 執行此查詢會從最低資料粒度層級 hello （縣/市有支援，否則在 hello 國家 （地區） 層級），並且停止 toohello 最高層級，也就是所有 hello 向上**世界**。 hello 第一個相符項目找到使用這個周遊被指定為 hello 端點 tooreturn hello 查詢回應中。 符合「巢狀」類型端點時，則會根據路由方法，傳回該子設定檔中的端點。 下列點 hello 是適用的 toothis 行為：

- 地理區域地理路由 hello 路由類型時，可以是對應的 Traffic Manager 設定檔中的唯一 tooone 端點。 這可確保使用者路由是具決定性，讓客戶在地理界限必須明確的情況下應付自如。
- 如果在兩個不同的端點的地理對應使用者的地區，Traffic Manager hello 最低的資料粒度選取 hello 端點，並不會考慮從該區域 toohello 要求路由傳送另一個端點。 例如，假設「地理路由」類型設定檔有兩個端點 - 端點 1 和端點 2。 Endpoint1 設定已從愛爾蘭和 Endpoint2 tooreceive 流量從歐洲 tooreceive 流量。 如果要求來自愛爾蘭，永遠是路由的 tooEndpoint1。
- 由於區可以是對應的唯一 tooone 端點，Traffic Manager 會傳回它不論 hello 端點是否為狀況良好。

    >[!IMPORTANT]
    >強烈建議，客戶使用 hello 地理路由方法就會將它將已包含至少兩個在每個端點的子項設定檔的 hello 巢狀型別端點關聯。
- 如果找到端點相符，且該端點處於 hello**已停止**狀態時，Traffic Manager 會傳回為 NODATA 回應。 在此情況下，沒有進一步的查閱高的層級中建立 hello 地理區域的階層。 這個行為也會適用於巢狀的端點類型 hello hello 子系的設定檔時**已停止**或**已停用**狀態。
- 如果端點顯示**已停用**狀態，將不會包含在比對程序的 hello 區域中。 這種行為時，也適用於巢狀的端點類型 hello 端點處於 hello**已停用**狀態。
- 如果查詢的來源地理區域在該設定檔中沒有對應，流量管理員會傳回 NODATA 回應。 因此，強烈建議客戶使用地理路由與一個端點，在理想情況下型別中的巢狀 hello 子項設定檔，與 hello 區域中的至少兩個端點**世界**指派 tooit。 這也可確保會處理任何未對應 tooa 區域的 IP 位址。

如[流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)中所述，流量管理員不會直接從用戶端接收 DNS 查詢。 相反地，DNS 查詢來自 hello 用戶端會設定的 toouse hello 遞迴 DNS 服務。 因此，hello IP 位址使用 toodetermine hello 區域不是 hello 用戶端的 IP 位址，但它是 hello hello 遞迴 DNS 服務 IP 位址。 在實務上，此 IP 位址是好 hello 用戶端 proxy。


## <a name="next-steps"></a>後續步驟

深入了解如何使用 toodevelop 高可用性應用程式[Traffic Manager 端點監視](traffic-manager-monitoring.md)

了解如何太[建立 Traffic Manager 設定檔](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



