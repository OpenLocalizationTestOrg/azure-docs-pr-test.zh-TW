hello 下表列出配額資訊特定 tooService Bus 訊息。 服務匯流排的其他配額和定價資訊，請參閱 hello[服務匯流排定價](https://azure.microsoft.com/pricing/details/service-bus/)概觀。

| 配額名稱 | Scope | 類型 | 超出時的行為 | 值 |
| --- | --- | --- | --- | --- |
| 每個 Azure 訂用帳戶的基本/標準命名空間數目上限 |命名空間 |靜態 |其他基本 / 標準的命名空間的後續要求將會拒絕的 hello 入口網站。 |100|
| 每個 Azure 訂用帳戶的進階命名空間數目上限 |命名空間 |靜態 |其他 premium 命名空間的後續要求將會拒絕的 hello 入口網站。 |10 |
| 佇列/主題大小 |實體 |在建立 hello 佇列/主題時定義。 |內送訊息將會遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |1、2、3、4 或 5 GB。<br /><br />如果[分割](../articles/service-bus-messaging/service-bus-partitioning.md)已啟用，hello 佇列/主題大小上限是 80 GB。 |
| 命名空間上的並行連線數目 |命名空間 |靜態 |其他連接的後續要求將遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 REST 作業不會計入並行 TCP 連線內。 |NetMessaging: 1,000<br /><br />AMQP: 5,000 |
| 佇列/主題/訂用帳戶實體上的並行接收要求數目 |實體 |靜態 |後續接收會拒絕要求，而且呼叫程式碼的 hello 程式會收到例外狀況。 這個配額會套用 toohello 結合的並行連線數目的所有子主題訂閱接收作業。 |5,000 |
| 每個服務命名空間的主題/佇列數目 |全系統 |靜態 |建立新主題或佇列 hello 服務命名空間上的後續要求將遭到拒絕。 如此一來，如果透過 hello 設定[Azure 入口網站][Azure portal]，將會產生錯誤訊息。 如果從 hello 管理 API 呼叫，就會收到例外狀況所呼叫的程式碼的 hello。 |10,000<br /><br />hello 主題和佇列服務命名空間中的總數目必須小於或等於 too10，000。<br/>這是不適用 tooPremium 分割的所有實體。 |
| 每個服務命名空間的分割主題/佇列數目 |全系統 |靜態 |建立新分割的主題或佇列 hello 服務命名空間上的後續要求將遭到拒絕。 如此一來，如果透過 hello 設定[Azure 入口網站][Azure portal]，將會產生錯誤訊息。 如果呼叫 hello 管理 API，從**QuotaExceededException**程式 hello 呼叫程式碼將會收到例外狀況。 |基本層和標準層 - 100<br />[進階](../articles/service-bus-messaging/service-bus-premium-messaging.md) - 1,000 (每個傳訊單位)<br/><br />每個磁碟分割的佇列或主題會計入 hello 配額的每個命名空間的 10,000 個實體。 |
| 任何傳訊實體路徑的大小上限︰佇列或主題 |實體 |靜態 |- |260 個字元 |
| 任何傳訊實體名稱的大小上限︰命名空間、訂用帳戶或訂用帳戶規則 |實體 |靜態 |- |50 個字元 |
| 佇列/主題/訂用帳戶實體的訊息大小 |全系統 |靜態 |超出這些配額的內送訊息將會遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |訊息大小上限︰256KB ([標準層](../articles/service-bus-messaging/service-bus-premium-messaging.md)) / 1MB ([進階層](../articles/service-bus-messaging/service-bus-premium-messaging.md))。 <br /><br />**請注意**toosystem 額外負荷，因為這項限制通常是稍微少。<br /><br />標頭大小上限︰64KB<br /><br />屬性包中的標頭屬性數目上限︰**byte/int.MaxValue**<br /><br />屬性包中的屬性大小上限︰沒有明確限制。 受限於標頭大小上限。 |
| 佇列/主題/訂用帳戶實體的訊息屬性大小 |全系統 |靜態 |已產生 **SerializationException** 例外狀況。 |每個屬性的訊息屬性大小上限為 32K。 所有屬性的累計大小不得超過 64K。 這適用於整個 toohello hello 標頭[BrokeredMessage](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.aspx)，其具有使用者屬性，以及系統屬性 (例如[SequenceNumber](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.sequencenumber.aspx)，[標籤](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.label.aspx)， [MessageId](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.messageid.aspx)等等)。 |
| 每個主題的訂用帳戶數目 |全系統 |靜態 |建立其他訂閱 hello 主題的後續要求將遭到拒絕。 如此一來，如果透過 hello 入口網站設定，將會顯示錯誤訊息。 如果已從 hello 管理 API 呼叫將會收到例外狀況，所呼叫的程式碼的 hello。 |2,000 |
| 每個主題的 SQL 篩選器數目 |全系統 |靜態 |建立 hello 主題上的其他篩選的後續要求將遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |2,000 |
| 每個主題的相互關聯篩選器數目 |全系統 |靜態 |建立 hello 主題上的其他篩選的後續要求將遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |100,000 |
| SQL 篩選器/動作的大小 |全系統 |靜態 |建立其他篩選的後續要求將遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |篩選條件字串的長度上限︰1024 (1K)。<br /><br />規則動作字串的長度上限︰1024 (1K)。<br /><br />每個規則動作的運算式數目上限︰32。 |
| 每個命名空間、佇列或主題的 [SharedAccessAuthorizationRule](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sharedaccessauthorizationrule.aspx) 規則數目 |實體、命名空間 |靜態 |建立其他規則的後續要求將遭到拒絕，並由 hello 呼叫程式碼將會收到例外狀況。 |規則數目上限︰12。 <br /><br /> 服務匯流排命名空間所設定的規則適用於 tooall 佇列和主題，該命名空間中。 |

[Azure portal]: https://portal.azure.com