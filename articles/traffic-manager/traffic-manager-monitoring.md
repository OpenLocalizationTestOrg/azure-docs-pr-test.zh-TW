---
title: "Azure 流量管理員端點監視 | Microsoft Docs"
description: "本文有助於您了解流量管理員如何使用端點監視和自動端點容錯移轉，以協助 Azure 客戶部署高可用性應用程式"
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
ms.openlocfilehash: 3b30aa04854b779c25582abafc0f9ebba65b71ba
ms.sourcegitcommit: bd0d3ae20773fc87b19dd7f9542f3960211495f9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>流量管理員端點監視

Azure 流量管理員包含內建的端點監視和自動端點容錯移轉。 此功能可協助您提供能夠從端點故障中恢復的高可用性應用程 式，包括 Azure 區域失敗。

## <a name="configure-endpoint-monitoring"></a>設定端點監視

若要設定端點監視，您必須在流量管理員設定檔中指定下列設定︰

* **通訊協定**。 選擇 HTTP、HTTPS 或 TCP 作為通訊協定，流量管理員會在探查端點以檢查其健康情況時使用。 HTTPS 監視不會驗證您的 SSL 憑證是否有效，它只會檢查該憑證是否存在。
* **連接埠**。 選擇要求所使用的連接埠。
* **路徑**。 組態設定僅適用於 HTTP 和 HTTPS 通訊協定，這些通訊協定需要指定路徑設定。 為 TCP 監視通訊協定提供這項設定會導致錯誤。 對於 TCP 通訊協定，提供監視存取之網頁或檔案的相對路徑和名稱。 正斜線 (/) 是相對路徑的有效項目。 這個值表示檔案位於根目錄 (預設值)。
* **探查間隔**。 這個值會指定流量管理員探查代理程式檢查端點健康情況的頻率。 您可以指定以下兩個值：30 秒 (一般探查) 和 10 秒 (快速探查)。 如果沒有提供任何值，設定檔會設定為預設值 30 秒。 請瀏覽[流量管理員定價](https://azure.microsoft.com/pricing/details/traffic-manager)分頁以深入了解快速探查定價的詳細資訊。
* **容許的失敗次數**。 這個值會指定在將該端點標示為狀況不良之前，流量管理員探查代理程式可以容許多少次失敗。 此值必須介於 0 到 9 的範圍內。 值為 0 表示單一監視失敗就會導致將該端點標示為狀況不良。 如果未指定任何值，它會使用預設值 3。
* **監視逾時**。 此屬性會指定流量管理員探查代理程式在健康情況檢查探查傳送至端點時，將該檢查視為失敗之前應該等待的時間量。 如果探查間隔設定為 30 秒，則您可以設定介於 5 到 10 秒的逾時值。 如果未指定任何值，它會使用預設值 10 秒。 如果探查間隔設定為 10 秒，則您可以設定介於 5 到 9 秒的逾時值。 如果未指定任何逾時值，它會使用預設值 9 秒。

![流量管理員端點監視](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**圖 1：流量管理員端點監視**

## <a name="how-endpoint-monitoring-works"></a>端點監視的運作方式

如果監視通訊協定設定為 HTTP 或 HTTPS，流量管理員探查代理程式會使用通訊協定、連接埠以及指定的相對路徑，向端點提出 GET 要求。 如果它獲得 200-OK 回應，則該端點視為狀況良好。 如果回應是不同的值，或者，如果在指定的逾時期間內未收到回應，則流量管理員探查代理程式會根據「容許的失敗次數」設定重新嘗試 (如果此設定為 0 則不會重新嘗試）。 如果連續失敗次數大於「容許的失敗次數」設定，則該端點會標示為狀況不良。 

如果監視通訊協定是 TCP，流量管理員探查代理程式會使用指定的連接埠初始化 TCP 連線要求。 如果端點以建立連線的回應來回覆要求，該健康情況檢查會標示為成功，且流量管理員探查代理程式會重設 TCP 連線。 如果回應是不同的值，或者，如果在指定的逾時期間內未收到回應，流量管理員探查代理程式會根據「容許的失敗次數」設定重新嘗試 (如果此設定為 0 則不會重新嘗試）。 如果連續失敗次數大於「容許的失敗次數」設定，則該端點會標示為狀況不良。

在所有情況下，流量管理員會從多個位置探查，連續失敗判斷會在每個區域內發生。 這也表示端點收到來自流量管理員之健康情況檢查探查的頻率，會比用於探查間隔的設定更高。

>[!NOTE]
>對於 HTTP 或 HTTPS 監視通訊協定，端點端上常見的做法是在您的應用程式內實作自訂分頁，例如，/health.aspx。 使用此路徑進行監視，您可以執行應用程式特定的檢查，例如檢查效能計數器或驗證資料庫可用性。 根據這些自訂檢查，頁面會傳回適當的 HTTP 狀態碼。

流量管理員設定檔中的所有端點都共用監視設定。 如果您需要對不同端點使用不同的監視設定，您可以建立[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings)。

## <a name="endpoint-and-profile-status"></a>端點和設定檔狀態

您可以啟用和停用流量管理員設定檔和端點。 不過，端點狀態中的變更也可能是因為流量管理員自動設定和程序的結果所導致。

### <a name="endpoint-status"></a>端點狀態

您可以啟用或停用特定端點。 基礎服務可能仍然狀況良好，不受影響。 變更端點狀態可控制流量管理員設定檔中端點的可用性。 當端點狀態為「已停用」時，流量管理員不會檢查其健全狀況，而且端點不會包含於 DNS 回應中。

### <a name="profile-status"></a>設定檔狀態

使用設定檔狀態設定，您可以啟用或停用特定的設定檔。 儘管端點狀態只會影響單一端點，設定檔狀態仍會影響整個設定檔，包括所有端點。 當您停用設定檔時，不會檢查端點的健全狀況，而且 DNS 回應中不會包含任何端點。 會針對 DNS 查詢傳回 [NXDOMAIN](https://tools.ietf.org/html/rfc2308) 回應碼。

### <a name="endpoint-monitor-status"></a>端點監視狀態

端點監視狀態是流量管理員所產生的值，會顯示端點的狀態。 您無法手動變更此設定。 端點監視狀態是端點監視的結果以及設定端點狀態的組合。 下表顯示端點監視狀態的可能值：

| 設定檔狀態 | 端點狀態 | 端點監視狀態 | 注意事項 |
| --- | --- | --- | --- |
| 已停用 |已啟用 |非使用中 |已停用設定檔。 儘管端點狀態為「已啟用」，但會優先採用設定檔狀態 (「已停用」)。 不會監視「已停用」設定檔中的端點。 會針對 DNS 查詢傳回 NXDOMAIN 回應碼。 |
| &lt;any&gt; |已停用 |已停用 |已停用端點。 不會監視「已停用」的端點。 端點未包含於 DNS 回應中，因此不會接收流量。 |
| 已啟用 |已啟用 |線上 |端點受到監視且狀況良好。 端點包含於 DNS 回應中，因此可接收流量。 |
| 已啟用 |已啟用 |已降級 |端點監視健全狀況檢查失敗。 端點未包含於 DNS 回應中，因此不會接收流量。 <br>例外狀況是如果所有端點都降級，如果發生這種情況，則所有端點會被視為要在查詢回應中傳回。</br>|
| 已啟用 |已啟用 |正在檢查端點 |端點受到監視，但尚未收到第一次探查的結果。 CheckingEndpoint 是暫時性狀態，其通常會在新增或啟用設定檔中的端點之後立即發生。 處於此狀態的端點會包含於 DNS 回應中，因此可接收流量。 |
| 已啟用 |已啟用 |已停止 |端點指向的雲端服務或 Web 應用程式並未執行。 請檢查雲端服務或 Web 應用程式設定。 如果端點是巢狀端點類型，且子系設定檔已停用或非使用中，也會發生這種情況。 <br>「已停止」狀態的端點不會受到監視。 它未包含於 DNS 回應中，因此不會接收流量。 例外狀況是如果所有端點都降級，如果發生這種情況，則所有端點會被視為要在查詢回應中傳回。</br>|

如需如何計算巢狀端點的端點監視狀態詳細資訊，請參閱[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。

### <a name="profile-monitor-status"></a>設定檔監視狀態

設定檔監視狀態是所有端點的端點監視狀態值，以及設定之設定檔狀態所形成的組合。 下表說明可能的值︰

| 設定檔狀態 (依設定) | 端點監視狀態 | 設定檔監視狀態 | 注意事項 |
| --- | --- | --- | --- |
| 已停用 |&lt;任何&gt;或未定義端點的設定檔。 |已停用 |已停用設定檔。 |
| 已啟用 |至少有一個端點的狀態為「已降級」。 |已降級 |檢閱個別端點狀態值，以判斷哪些端點需要進一步注意。 |
| 已啟用 |至少有一個端點的狀態為「線上」。 沒有狀態為「已降級」的端點。 |線上 |服務正在接收流量。 不需要採取任何動作。 |
| 已啟用 |至少有一個端點的狀態為「正在檢查端點」。 沒有狀態為「線上」或「已降級」的端點。 |正在檢查端點 |建立或啟用設定檔時，就會發生此轉換狀態。 正在初次檢查端點健康情況。 |
| 已啟用 |設定檔中的所有端點狀態為「已停用」或「已停止」，或者設定檔並未定義任何端點。 |非使用中 |沒有作用中的端點，但設定檔仍為「已啟用」。 |

## <a name="endpoint-failover-and-recovery"></a>端點容錯移轉和復原

流量管理員會定期檢查每個端點的健康狀態，包括狀況不良的端點健康情況。 當端點變成狀況良好時，流量管理員會偵測到此狀況，並且將它恢復至輪替。

發生下列任何一種狀況時，端點為狀況不良：
- 如果監視通訊協定是 HTTP 或 HTTPS：
    - 收到非 200 回應 (包括不同的 2xx 碼或 301/302 重新導向)。
- 如果監視通訊協定是 TCP： 
    - 在流量管理員傳送給 SYNC 要求以嘗試連線建立的回應中，收到 ACK 或 SYN-ACK 以外的回應。
- 逾時。 
- 導致無法連線到端點的任何其他連線問題。

如需疑難排解失敗檢查的詳細資訊，請參閱 [疑難排解 Azure 流量管理員上的已降級狀態](traffic-manager-troubleshooting-degraded.md)。 

圖 2 中的下列時間軸是流量管理員端點之監視處理序的詳細說明，具有以下設定：監視通訊協定為 HTTP、探查間隔為 30 秒、容許的失敗次數為 3 次、逾時值為 10 秒，以及 DNS TTL 為 30 秒。

![流量管理員端點容錯移轉和容錯回復順序](./media/traffic-manager-monitoring/timeline.png)

**圖 2：流量管理員端點容錯移轉和復原順序**

1. **GET**。 對於每個端點而言，流量管理員監視系統會對監視設定中指定的路徑執行 GET 要求。
2. **200 OK**。 監視系統預期在 10 秒鐘內應該傳回 HTTP 200 OK 訊息。 收到此回應時，就能確認服務可供使用。
3. **每次檢查之間間隔 30 秒**。 每隔 30 秒重複進行端點健康狀態檢查。
4. **服務無法使用**。 服務變為無法使用。 流量管理員要直到下次健全狀況檢查時才會知道。
5. **嘗試存取監視路徑**。 監視系統執行 GET 要求，但沒有在 10 秒鐘的逾時期限內收到回應 (反而可能收到非 200 的回應)。 接著每隔 30 秒執行一次，再嘗試三次。 如果其中一次嘗試成功，會重設嘗試次數。
6. **將狀態設為已降級**。 在第四次連續失敗之後，監視系統會將無法使用的端點狀態標示為「已降級」。
7. **流量轉向其他端點**。 流量管理員 DNS 名稱伺服器已更新，而流量管理員在回應 DNS 查詢時不再傳回端點。 新的連接會導向至其他可用的端點。 不過，先前包含此端點的 DNS 回應仍可能由遞迴 DNS 伺服器和 DNS 用戶端所快取。 用戶端會繼續使用端點，直到 DNS 快取過期為止。 當 DNS 快取過期時，用戶端會提出新的 DNS 查詢，並導向至不同的端點。 快取持續時間是由流量管理員設定檔中的 TTL 設定所控制，例如 30 秒。
8. **健全狀況檢查繼續**。 儘管端點處於「已降級」狀態，流量管理員還是會繼續檢查它的健全狀況。 當端點恢復成狀況良好的狀態時，流量管理員會偵測到此情況。
9. **服務重新上線**。 服務變為可供使用。 端點會在流量管理員中維持「已降級」狀態，直到監視系統執行下一次健全狀況檢查為止。
10. **服務的流量恢復**。 流量管理員傳送 GET 要求，並收到 200 OK 狀態回應。 此服務已恢復狀況良好的狀態。 流量管理員名稱伺服器會更新，並會開始在 DNS 回應中送出服務的 DNS 名稱。 當傳回其他端點的快取 DNS 回應過期時，以及當其他端點的現有連接終止時，流量將再次回到端點。

    > [!NOTE]
    > 由於流量管理員是在 DNS 層級運作，所以無法影響任何端點的現有連接。 在引導端點之間的流量時 (透過變更設定檔設定，或是在容錯移轉或容錯回復期間)，流量管理員會將新的連接導向至可用的端點。 不過，其他端點可透過現有的連接繼續接收流量，直到這些工作階段終止為止。 若要將現有連接的流量排出，應用程式應該限制每個端點使用的工作階段持續時間。

## <a name="traffic-routing-methods"></a>流量路由方法

當端點狀態為「已降級」，它不會再傳回以回應 DNS 查詢。 而是選擇並傳回替代端點。 設定檔中設定的流量路由方法會決定如何選擇替代端點。

* **優先順序**。 端點會形成優先順序清單。 永遠傳回清單上第一個可用的端點。 如果端點狀態為「已降級」，則會傳回下一個可用的端點。
* **加權**。 根據指派的加權和其他可用端點的加權，隨機選擇任何可用的端點。
* **效能**。 會傳回最接近使用者的端點。 如果該端點無法使用，流量管理員會將流量移至最接近的下一個 Azure 區域中的端點。 您可以使用[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region)來設定效能流量路由的替代容錯移轉計劃。
* **地理**。 會傳回根據查詢要求 IP，對地理位置提供服務的已對應端點。 如果該端點無法使用，則不會選取要容錯移轉的另一個端點，因為地理位置只能對應至設定檔中的一個端點 (更多詳細資料位於[常見問題集](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method))。 使用地理路由時的最佳做法是，建議客戶使用具有多個端點作為設定檔端點的巢狀流量管理員設定檔。

如需詳細資訊，請參閱 [流量管理員流量路由方法](traffic-manager-routing-methods.md)。

> [!NOTE]
> 當所有合格的端點狀態為「已降級」時，正常的流量路由行為會發生例外狀況。 流量管理員會「竭盡所能」進行嘗試，且「彷彿所有已降級狀態的端點實際上是處於線上狀態一樣地回應」 。 此行為比在 DNS 回應中不傳回任何端點的另一種做法更好。 「已停用」或「已停止」端點不會受到監視，因此，不會將它們視為符合流量資格。
>
> 這種情況通常是因為服務組態不正確所造成的，例如：
>
> * 存取控制清單 [ACL] 封鎖流量管理員健康情況檢查。
> * 流量管理員設定檔中監視連接埠或通訊協定的設定不正確。
>
> 此行為的結果是當流量管理員健康狀態檢查未正確設定時，從流量路由傳送看起來，流量管理員似乎運作正常。 不過，在此情況下，不會發生影響整體應用程式可用性的端點容錯移轉。 請務必檢查設定檔會顯示為「線上」狀態，而不是「已降級」狀態。 「線上」狀態表示流量管理員的健康狀態檢查如預期般地運作。

如需疑難排解無法進行健康狀態檢查的詳細資訊，請參閱[疑難排解 Azure 流量管理員上的已降級狀態](traffic-manager-troubleshooting-degraded.md)。



## <a name="next-steps"></a>後續步驟

了解 [流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)

深入了解流量管理員支援的 [流量路由方法](traffic-manager-routing-methods.md)

了解如何 [建立流量管理員設定檔](traffic-manager-manage-profiles.md)

[疑難排解流量管理員端點上的已降級狀態](traffic-manager-troubleshooting-degraded.md)