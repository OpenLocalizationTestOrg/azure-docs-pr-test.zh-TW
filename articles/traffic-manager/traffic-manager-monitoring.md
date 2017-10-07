---
title: "aaaAzure Traffic Manager 端點監視 |Microsoft 文件"
description: "這篇文章可協助您了解 Traffic Manager 會使用端點監視和自動端點容錯移轉 toohelp Azure 客戶部署高可用性應用程式"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>流量管理員端點監視

Azure 流量管理員包含內建的端點監視和自動端點容錯移轉。 這項功能可協助您提供彈性 tooendpoint 失敗，包括 Azure 區域失敗的高可用性應用程式。

## <a name="configure-endpoint-monitoring"></a>設定端點監視

tooconfigure 端點監視，您必須指定下列設定，在您的 Traffic Manager 設定檔的 hello:

* **通訊協定**。 選擇 HTTP、 HTTPS 或 TCP 做為 Traffic Manager 會使用探查端點 toocheck 時的 hello 通訊協定其健全狀況。 HTTPS 監視不會驗證您的 SSL 憑證是否有效-它只會檢查該 hello 的憑證。
* **連接埠**。 選擇 hello hello 要求使用的連接埠。
* **路徑**。 此組態設定是僅適用於 hello HTTP 和 HTTPS 通訊協定，其指定 hello 路徑設定為必要項目。 提供這項設定 hello TCP 監視通訊協定將導致錯誤。 TCP 通訊協定，可讓 hello 相對路徑和 hello hello 網頁或檔案的名稱 hello 監視存取該 hello。 正斜線 （/） 是 hello 相對路徑的有效項目。 這個值表示該 hello 檔案是在 hello 根目錄 （預設值）。
* **探查間隔**。 這個值會指定流量管理員探查代理程式檢查端點健康情況的頻率。 您可以指定以下兩個值：30 秒 (一般探查) 和 10 秒 (快速探查)。 如果未不提供任何值，則 hello 設定檔設定 tooa 預設值為 30 秒。 請瀏覽 hello [Traffic Manager 定價](https://azure.microsoft.com/pricing/details/traffic-manager)頁面 toolearn 更多關於快速探查定價。
* **容許的失敗次數**。 這個值會指定在將該端點標示為狀況不良之前，流量管理員探查代理程式可以容許多少次失敗。 此值必須介於 0 到 9 的範圍內。 值為 0，表示單一的監視失敗可能會導致該端點 toobe，標示為狀況不良。 如果未不指定任何值，它會使用 hello 預設值為 3。
* **監視逾時**。 此屬性指定時間 hello 探查代理程式應該考慮之前，先等候健全狀況檢查探查傳送 toohello 端點時，請檢查失敗，Traffic Manager 的 hello 的數量。 如果 hello 探查間隔設 too30 秒，則您可以設定介於 5 到 10 秒的 hello 逾時值。 如果未指定任何值，它會使用預設值 10 秒。 如果 hello 探查間隔設 too10 秒，則您可以設定介於 5 到 9 秒 hello 逾時值。 如果未指定任何逾時值，它會使用預設值 9 秒。

![流量管理員端點監視](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**圖 1：流量管理員端點監視**

## <a name="how-endpoint-monitoring-works"></a>端點監視的運作方式

如果 hello 監視通訊協定設定為 HTTP 或 HTTPS，hello Traffic Manager 探查代理程式就會建立使用 hello 通訊協定、 連接埠和相對路徑指定之 GET 要求 toohello 端點。 如果它獲得 200-OK 回應，則該端點視為狀況良好。 如果 hello 回應不同的值，或指定的 hello 逾時期限內收到任何回應，然後 hello Traffic Manager 探查代理程式重試根據 toohello 所容許之失敗的數目設定 （沒有重試完成若此設定為 0）. 如果 hello 連續失敗次數大於 hello 所容許之失敗的數目設定值，該端點會標示為狀況不良。 

如果 hello 監視通訊協定是 TCP，hello Traffic Manager 探查代理程式會初始化使用指定的 hello 連接埠 TCP 連線要求。 如果 hello 端點回應 toohello 要求回應 tooestablish hello，透過連線，健全狀況檢查會標示為成功，並且 hello Traffic Manager 探查代理程式會重設 hello TCP 連線。 如果 hello 回應不同的值，或者內沒有收到任何回應 hello 逾時期間指定，hello Traffic Manager 探查代理程式重試根據 toohello 所容許之失敗的數字 （沒有重試所做的設定如果這項設定為 0）。 如果 hello 連續失敗次數大於 hello 所容許之失敗的數目設定值，然後該端點會標示為狀況不良。

在所有情況下，Traffic Manager 探查從多個位置以及 hello 連續失敗判斷發生在每個區域。 這也表示端點會收到健全狀況探查從 Traffic Manager 以更高的頻率比 hello 設定用於探查間隔。

>[!NOTE]
>HTTP 或 HTTPS 通訊協定的監視，hello 端點端上常見的作法是 tooimplement 應用程式中-例如，/health.aspx 的自訂頁面。 使用此路徑進行監視，您可以執行應用程式特定的檢查，例如檢查效能計數器或驗證資料庫可用性。 根據這些自訂的檢查，hello 頁面傳回適當的 HTTP 狀態碼。

流量管理員設定檔中的所有端點都共用監視設定。 如果您需要 toouse 不同的不同端點監視設定，您可以建立[巢狀 流量管理員設定檔](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings)。

## <a name="endpoint-and-profile-status"></a>端點和設定檔狀態

您可以啟用和停用流量管理員設定檔和端點。 不過，端點狀態中的變更也可能是因為流量管理員自動設定和程序的結果所導致。

### <a name="endpoint-status"></a>端點狀態

您可以啟用或停用特定端點。 hello 基礎服務，可能仍會處於狀況良好，不會影響。 變更 hello 端點狀態控制項 hello hello Traffic Manager 設定檔中的 hello 端點的可用性。 停用端點狀態時，Traffic Manager 不會檢查其健全狀況和 hello 端點並未包含在 DNS 回應。

### <a name="profile-status"></a>設定檔狀態

使用 hello 設定檔的狀態設定，您可以啟用或停用特定的設定檔。 端點狀態會影響單一端點，而設定檔狀態會影響 hello 整個設定檔，包括所有端點。 當您停用設定檔時，hello 端點不會檢查健全狀況，而且沒有端點會包含在 DNS 回應。 [NXDOMAIN](https://tools.ietf.org/html/rfc2308) hello DNS 查詢會傳回回應碼。

### <a name="endpoint-monitor-status"></a>端點監視狀態

端點監視狀態會顯示 hello hello 端點狀態的 Traffic Manager 產生的值。 您無法手動變更此設定。 hello 端點監視狀態是 hello 結果的端點監視的組合，hello 設定的端點狀態。 下表中的 hello 顯示 hello 的端點監視狀態的可能值：

| 設定檔狀態 | 端點狀態 | 端點監視狀態 | 注意事項 |
| --- | --- | --- | --- |
| 已停用 |已啟用 |非使用中 |hello 設定檔已停用。 雖然 hello 端點狀態為啟用，但是 hello 設定檔狀態 （已停用） 的優先順序較高。 不會監視「已停用」設定檔中的端點。 Hello DNS 查詢會傳回 NXDOMAIN 回應碼。 |
| &lt;any&gt; |已停用 |已停用 |hello 端點已停用。 不會監視「已停用」的端點。 hello 端點並未包含在 DNS 回應中，因此，不會接收流量。 |
| 已啟用 |已啟用 |線上 |hello 端點受到監視且狀況良好。 端點包含於 DNS 回應中，因此可接收流量。 |
| 已啟用 |已啟用 |已降級 |端點監視健全狀況檢查失敗。 hello 端點不包含在 DNS 回應中，而且不會接收流量。 <br>例外狀況 toothis 是所有端點會都降級，如果在此情況下所有這些皆視為 toobe hello 查詢回應中傳回）。</br>|
| 已啟用 |已啟用 |正在檢查端點 |hello 端點受到監視，但尚未尚未收到 hello hello 第一次探查的結果。 CheckingEndpoint 是新增或啟用 hello 設定檔中的端點之後，通常會發生的暫時狀態。 處於此狀態的端點會包含於 DNS 回應中，因此可接收流量。 |
| 已啟用 |已啟用 |已停止 |hello 雲端服務或 web 應用程式 hello 端點點 toois 未執行。 請檢查 hello 雲端服務或 web 應用程式設定。 此情形也如果 hello 端點的類型巢狀的端點和 hello 子系的設定檔已停用或非使用中。 <br>「已停止」狀態的端點不會受到監視。 它未包含於 DNS 回應中，因此不會接收流量。 例外狀況 toothis 是如果會降級的所有端點，在此情況下全部都將會被視為 toobe hello 查詢回應中傳回。</br>|

如需如何計算巢狀端點的端點監視狀態詳細資訊，請參閱[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。

### <a name="profile-monitor-status"></a>設定檔監視狀態

hello 設定檔監視狀態是設定 hello 設定檔狀態和 hello 所有端點的端點監視狀態值的組合。 hello 下表將描述 hello 可能的值：

| 設定檔狀態 (依設定) | 端點監視狀態 | 設定檔監視狀態 | 注意事項 |
| --- | --- | --- | --- |
| 已停用 |&lt;任何&gt;或未定義端點的設定檔。 |已停用 |hello 設定檔已停用。 |
| 已啟用 |至少一個端點的 hello 狀態會降低。 |已降級 |檢閱 hello 個別的端點狀態值 toodetermine 哪些端點需要進一步注意。 |
| 已啟用 |至少一個端點的 hello 狀態為 Online。 沒有狀態為「已降級」的端點。 |線上 |hello 服務正在接收流量。 不需要採取任何動作。 |
| 已啟用 |至少一個端點的 hello 狀態為 CheckingEndpoint。 沒有狀態為「線上」或「已降級」的端點。 |正在檢查端點 |建立或啟用設定檔時，就會發生此轉換狀態。 hello 端點健全狀況正在檢查的 hello 第一次。 |
| 已啟用 |hello 狀態的 hello 設定檔中的所有端點已停用或已停止，或 hello 設定檔沒有任何已定義的端點。 |非使用中 |沒有端點是作用中，但仍處於啟用狀態 hello 設定檔。 |

## <a name="endpoint-failover-and-recovery"></a>端點容錯移轉和復原

Traffic Manager 會定期檢查 hello 健全狀況的每個端點，包括狀況不良的端點。 當端點變成狀況良好時，流量管理員會偵測到此狀況，並且將它恢復至輪替。

端點是狀況不良，出現任何 hello 下列事件：
- 如果 hello 監視通訊協定是 HTTP 或 HTTPS:
    - 收到非 200 回應 (包括不同的 2xx 碼或 301/302 重新導向)。
- 如果 hello 監視通訊協定是 TCP: 
    - 除了 ACK 或 SYN ACK 收到回應 toohello 同步處理要求中傳送回應 Traffic Manager tooattempt 由連線建立。
- 逾時。 
- 任何其他連線問題導致無法連線到 hello 端點中。

如需疑難排解失敗檢查的詳細資訊，請參閱 [疑難排解 Azure 流量管理員上的已降級狀態](traffic-manager-troubleshooting-degraded.md)。 

hello 下列時間表在圖 2 是 hello 監視具有下列設定的 hello 的流量管理員端點的程序的詳細的說明： 監視通訊協定為 HTTP、 探查間隔為 30 秒，容許的失敗次數為 3，逾時值10 秒，而且 DNS TTL 為 30 秒。

![流量管理員端點容錯移轉和容錯回復順序](./media/traffic-manager-monitoring/timeline.png)

**圖 2：流量管理員端點容錯移轉和復原順序**

1. **GET**。 針對每個端點，hello Traffic Manager 監視系統會 hello hello 監視設定中指定的路徑上，執行 GET 要求。
2. **200 OK**。 hello 監視系統必須要有 10 秒內傳回 HTTP 200 OK 訊息 toobe。 當它收到此回應時，會辨識 hello 服務可供使用。
3. **每次檢查之間間隔 30 秒**。 hello 端點健全狀況檢查重複每隔 30 秒。
4. **服務無法使用**。 hello 服務變為無法使用。 Traffic Manager 將不會知道直到 hello 下一步的健全狀況檢查。
5. **監視路徑嘗試 tooaccess hello**。 hello 監視系統執行 GET 要求，但未收到 hello 10 秒逾時期限之內回應 （或者，-200 回應可能會收到）。 接著每隔 30 秒執行一次，再嘗試三次。 如果其中一個 hello 嘗試成功，會重設 hello 嘗試次數。
6. **狀態設定 tooDegraded**。 在第四個連續失敗之後，監視系統的 hello 會標示為 「 降級 hello 無法使用的端點狀態。
7. **流量是轉接的 tooother 端點**。 hello Traffic Manager DNS 名稱伺服器更新，Traffic Manager 不會再傳回 hello 端點回應 tooDNS 查詢中。 新的連接會導向的 tooother，可用的端點。 不過，先前包含此端點的 DNS 回應仍可能由遞迴 DNS 伺服器和 DNS 用戶端所快取。 用戶端繼續 toouse hello 端點，直到 hello DNS 快取到期為止。 Hello DNS 快取過期，因為用戶端提出新的 DNS 查詢，並會導向的 toodifferent 端點。 hello 快取持續時間是由在 hello Traffic Manager 設定檔，例如，30 秒的 hello TTL 設定所控制。
8. **健全狀況檢查繼續**。 Traffic Manager 降級狀態時，會繼續 toocheck hello hello 端點健全狀況。 Traffic Manager 偵測到 hello 端點傳回 toohealth 時。
9. **服務重新上線**。 hello 服務變為無法使用。 hello 端點會保留在 Traffic Manager 降級狀態，直到 hello 監視系統執行其下一步的健全狀況檢查。
10. **流量 tooservice 繼續**。 流量管理員傳送 GET 要求，並收到 200 OK 狀態回應。 hello 服務傳回 tooa 狀況良好狀態。 hello Traffic Manager 名稱伺服器會更新，而開始 toohand 出 hello 服務的 DNS 回應中的 DNS 名稱。 過期的快取的 DNS 回應傳回其他端點，以及與現有的連接已終止 tooother 端點，流量會傳回 toohello 端點。

    > [!NOTE]
    > Traffic Manager 會在 hello DNS 層級運作，因為它無法影響現有連線 tooany 端點。 它會導向端點 （無論是已變更的設定檔設定，或是在容錯移轉或容錯回復期間） 之間的流量，Traffic Manager 會指示新的連線 tooavailable 端點。 不過，其他端點可能會繼續 tooreceive 流量透過現有的連線，直到這些工作階段已終止。 tooenable 流量 toodrain 從現有的連接，應用程式應該限制 hello 與每個端點使用的工作階段持續時間。

## <a name="traffic-routing-methods"></a>流量路由方法

當端點已降級狀態時，它不會再傳回回應 tooDNS 查詢中。 而是選擇並傳回替代端點。 設定 hello 設定檔中的 hello 流量路由方法會判斷如何選擇 hello 替代端點。

* **優先順序**。 端點會形成優先順序清單。 一律傳回 hello 第一個可用的端點上 hello 清單。 如果端點狀態的效能降低，則會傳回 hello 下一個可用的端點。
* **加權**。 任何可用的端點會選擇隨機根據其指派加權和其他可用端點 hello hello 加權。
* **效能**。 hello 端點最接近 toohello 終端使用者就會傳回。 如果無法使用該端點，端點會隨機選擇從所有 hello 其他可用端點。 選擇隨機的端點，可避免 hello 下一步 最靠近的端點變得負載過重時可能發生的階層式失敗。 您可以使用[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region)來設定效能流量路由的替代容錯移轉計劃。
* **地理**。 hello 端點對應 tooserve hello 地理位置根據 hello 查詢要求會傳回的 IP。 如果無法使用該端點，另一個端點不會選取的 toofailover，因為地理位置可以是對應的唯一 tooone 端點，在設定檔 (更多詳細資料位於 hello[常見問題集](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method))。 最佳作法是，使用地理路由時，我們建議客戶 toouse 巢狀 Traffic Manager 設定檔與一個以上的端點為 hello hello 設定檔的端點。

如需詳細資訊，請參閱 [流量管理員流量路由方法](traffic-manager-routing-methods.md)。

> [!NOTE]
> 符合資格的所有端點都有降級會發生一個例外狀況 toonormal 流量路由行為。 Traffic Manager 可讓 「 盡力 」 嘗試和*回應所有 hello 降級狀態端點實際上都會處於線上狀態*。 這是偏好的 toohello 替代方式，就是 toonot hello DNS 回應中傳回任何端點。 「已停用」或「已停止」端點不會受到監視，因此，不會將它們視為符合流量資格。
>
> 這種狀況，通常被因為 hello 服務的設定不正確例如：
>
> * 存取控制清單 [ACL] 封鎖 hello Traffic Manager 的健康情況檢查。
> * 監視連接埠或通訊協定 hello 流量管理員設定檔中的 hello 的不適當的設定。
>
> hello 的後果這種行為是，如果未正確設定 Traffic Manager 的健康情況檢查，它可能會顯示與 hello 流量路由一樣 Traffic Manager*是*正常運作。 不過，在此情況下，不會發生影響整體應用程式可用性的端點容錯移轉。 很重要的 toocheck hello 設定檔，顯示線上狀態，無法降級狀態。 線上的狀態，表示該 hello 健康情況檢查依照預期方式運作的 Traffic Manager。

如需疑難排解無法進行健康狀態檢查的詳細資訊，請參閱[疑難排解 Azure 流量管理員上的已降級狀態](traffic-manager-troubleshooting-degraded.md)。



## <a name="next-steps"></a>後續步驟

了解 [流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)

深入了解 hello[流量路由方法](traffic-manager-routing-methods.md)流量管理員支援

了解如何太[建立 Traffic Manager 設定檔](traffic-manager-manage-profiles.md)

[疑難排解流量管理員端點上的已降級狀態](traffic-manager-troubleshooting-degraded.md)
