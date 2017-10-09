---
title: "aaaAzure Storage queues 和 Service Bus 佇列-比較和對比 |Microsoft 文件"
description: "分析 Azure 所提供之兩種佇列類型之間的差異和相似性。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>儲存體佇列和服務匯流排佇列 - 異同比較
本文將分析 hello 兩個 Microsoft Azure 目前所提供的佇列類型之間 hello 差異和相似性： 儲存體佇列和服務匯流排佇列。 使用這項資訊，您可以比較和對比 hello 各項技術，是無法 toomake 更明智的決定哪一種最佳的解決方案需符合您的需求。

## <a name="introduction"></a>簡介
Azure 支援兩種佇列機制：**儲存體佇列**和**服務匯流排佇列**。

**儲存體佇列**，這屬於 hello [Azure 儲存體](https://azure.microsoft.com/services/storage/)基礎結構功能的簡單的 REST 架構 GET/PUT/PEEK 介面，提供可靠且持續的傳訊內部及服務之間。

**服務匯流排佇列**是較廣泛 [Azure 傳訊](https://azure.microsoft.com/services/service-bus/)基礎結構的一部分，支援佇列處理和發佈/訂閱，以及更進階的整合模式。 如需有關 Service Bus 佇列/主題/訂閱的詳細資訊，請參閱 hello[的服務匯流排概觀](service-bus-messaging-overview.md)。

雖然這兩種佇列技術同時存在，不過儲存體佇列較早引進，作為建置在 Azure 儲存體服務之上的專用佇列儲存體機制。 服務匯流排佇列建立在更廣泛的 「 訊息 」 基礎結構設計 toointegrate 應用程式或應用程式元件，可能會跨越多個通訊協定、 資料合約、 信任網域及/或網路環境的 hello 之上。

## <a name="technology-selection-considerations"></a>技術選擇考量
儲存體佇列和服務匯流排佇列是 hello 訊息佇列服務目前在 Microsoft Azure 提供的實作。 每個具有稍有不同的功能集，這表示您可以選擇其中一個或 hello，或兩者都使用，根據特定的方案或解決您的商務/技術問題的 hello 需求而定。

在決定哪一種佇列技術適合給定方案的 hello 目的時，方案架構設計人員和開發人員應該考慮下列 hello 建議。 如需詳細資訊，請參閱 hello 下一節。

身為方案架構設計人員/開發人員，您應該在下列情況下**考慮使用儲存體佇列**：

* 您的應用程式必須儲存超過 80 GB 的訊息在佇列中，其中 hello 訊息的存留期短於 7 天。
* 您的應用程式處理 hello 佇列內訊息想 tootrack 進度。 這是適用於處理訊息的 hello 工作者當機。 後續工作者可以接著會使用該資訊 toocontinue，從 hello 先前工作者停止的地方。
* 您需要伺服器端記錄所有 hello 針對佇列執行的交易。

身為方案架構設計人員/開發人員，您應該在下列情況下**考慮使用服務匯流排佇列**：

* 您的方案必須能夠 tooreceive 而不需要 toopoll hello 佇列的訊息。 使用服務匯流排，這可以透過 hello 使用 hello 長時間輪詢接收作業使用 hello 以 TCP 為基礎的通訊協定服務匯流排支援。
* 您的方案需要 hello 佇列 tooprovide 保證第一個在-後進先出 (FIFO) 排序的傳遞。
* 您想要在 Azure 中和在 Windows Server (私人雲端) 上有相稱體驗。 如需詳細資訊，請參閱 [Windows Server 的服務匯流排](https://msdn.microsoft.com/library/dn282144.aspx)。
* 您的方案必須能夠 toosupport 自動重複偵測。
* 您想要以平行的長時間執行資料流您應用程式 tooprocess 訊息 (訊息會與使用 hello 以資料流相關聯[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) hello 訊息上的屬性)。 在此模型中，hello 取用應用程式的每個節點競爭資料流，做為相對於 toomessages。 當資料流提供 tooa 耗用節點時，hello 節點可以檢查 hello hello 使用交易的應用程式資料流狀態的狀態。
* 從佇列傳送或接收多個訊息時，您的方案需要交易行為和不可部分完成性。
* hello 應用程式特定工作負載的 hello 存留時間 (TTL) 特性可能會超過 hello 7 天的期限。
* 您的應用程式會處理訊息可能會超過 64 KB，但將不太可能會接近 hello 256 KB 的限制。
* 在處理需求 tooprovide 角色型存取模型 toohello 佇列，以及不同的權限的傳送者和接收者。
* 您的佇列大小不會成長超過 80 GB。
* 您想 toouse hello AMQP 1.0 標準型訊息通訊協定。 如需 AMQP 的詳細資訊，請參閱[服務匯流排 AMQP 概觀](service-bus-amqp-overview.md)。
* 您可以想像方式與從佇列架構的點對點通訊 tooa 訊息交換模式，可讓緊密整合其他接收者 （訂戶），其中每個收到的部分或所有的獨立複本最終移轉toohello 佇列傳送訊息。 hello 後者是指 Service Bus 原本提供的 toohello 發佈/訂閱功能。
* 您的訊息方案必須能夠 toosupport hello 」 在大部分-一次 」 傳遞保證，而 hello 需要在您 toobuild hello 其他基礎結構元件。
* 您可以像是 toobe 無法 toopublish 和取用訊息批次。

## <a name="comparing-storage-queues-and-service-bus-queues"></a>比較儲存體佇列和服務匯流排佇列
hello 下列各節中的 hello 資料表提供佇列功能的邏輯群組，並可讓您一眼比較可用的儲存體佇列和服務匯流排佇列的 hello 功能。

## <a name="foundational-capabilities"></a>基本功能
本節將比較的一些基本 hello 提供儲存體佇列和服務匯流排佇列的佇列功能。

| 比較準則 | 儲存體佇列 | 服務匯流排佇列 |
| --- | --- | --- |
| 排序保證 |**否** <br/><br>如需詳細資訊，請參閱 hello hello < 其他資訊 > 一節中的第一個附註。</br> |**是 - 先進先出 (FIFO)**<br/><br>（透過使用 hello 訊息工作階段） |
| 傳遞保證 |**至少一次** |**至少一次**<br/><br/>**最多一次** |
| 不可部分完成作業支援 |**否** |**是**<br/><br/> |
| 接收行為 |**非封鎖**<br/><br/>(如果找不到新的訊息，便立即完成) |**含/不含逾時的封鎖**<br/><br/>(提供長期輪詢，或使用 hello ["Comet 技術"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**非封鎖**<br/><br/>(透過 hello 使用.NET API 僅限 managed) |
| 推送型 API |**否** |**是**<br/><br/>[OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) 和 **OnMessage** 工作階段的 .NET API。 |
| 接收模式 |**查看與租用** |**查看與鎖定**<br/><br/>**接收與刪除** |
| 獨佔存取模式 |**以租用為基礎** |**以鎖定為基礎** |
| 租用/鎖定持續時間 |**30 秒 (預設值)**<br/><br/>**7 天 （上限）** (您可以更新或釋放訊息租用使用 hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API。) |**60 秒 (預設值)**<br/><br/>您可以更新訊息鎖定使用 hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock)應用程式開發介面。 |
| 租用/鎖定精確度 |**訊息層級**<br/><br/>(每個訊息可以有不同的逾時值，然後您可以更新視處理 hello 訊息時，使用 hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx)應用程式開發介面) |**佇列層級**<br/><br/>(每個佇列有鎖定套用的有效位數 tooall 的訊息，但您可以更新使用 hello hello 鎖定[RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API。) |
| 批次接收 |**是**<br/><br/>（明確指定訊息計數擷取訊息，向上 tooa 最多 32 個訊息時） |**是**<br/><br/>（隱含啟用預先提取屬性或明確地透過 hello 使用的交易） |
| 批次傳送 |**否** |**是**<br/><br/>（透過 hello 使用的交易或用戶端批次處理） |

### <a name="additional-information"></a>其他資訊
* 儲存體佇列中的訊息通常是先進先出，但有時也不按順序；舉例來說，訊息的可視性逾時期限到期時 (例如，由於處理期間用戶端應用程式損毀所致)。 Hello 訊息 hello 可見度逾時過期時，隨即顯示在另一個工作者 toodequeue hello 佇列上再次它。 此時，hello 最新出現的訊息可能會由於置放 hello 佇列中 （toobe 再度） 之後原本之後加入佇列的訊息。
* hello 保證服務匯流排佇列中的 FIFO 模式需要 hello 傳訊工作階段使用。 在 hello hello 應用程式的事件損毀時處理 hello 中接收的訊息**查看 （& s) 鎖定**模式、 hello 下一次佇列接收者接受訊息工作階段時，它會開始與 hello 失敗訊息之後其存留時間 (TTL) 期限到期。
* 儲存體佇列是設計的 toosupport 標準佇列案例，例如分離應用程式元件 tooincrease 延展性及容錯能力、 進行負載均衡，以及建置程序工作流程。
* 服務匯流排佇列支援 hello*在-至少一次*傳遞保證。 此外，hello*大部分-次*語意可支援使用工作階段狀態 toostore hello 應用程式狀態和使用交易 tooatomically 接收訊息並更新 hello 工作階段狀態。
* 儲存體佇列提供跨佇列、資料表和 BLOB 之統一且一致的程式設計模型，適合開發人員和營運團隊使用。
* 服務匯流排佇列 hello 內容中的單一佇列的本機交易提供支援。
* hello**接收和刪除**Service Bus 所支援的模式提供 hello 能力 tooreduce hello 訊息作業計數 （以及相關聯的成本），但是也會降低的傳遞保證。
* 儲存體佇列訊息提供 hello 能力 tooextend hello 租用的租用。 這可讓 hello 工作者 toomaintain 簡短租用在訊息上。 因此，如果某個工作者當機，hello 訊息就可以快速處理一次由另一個工作者。 此外，背景工作可以擴充 hello 訊息租用，如果需要的 tooprocess 它超過 hello 目前租用的時間。
* 儲存體佇列提供可見性逾時，您可以設定或取消佇列訊息的 hello 佇列時設定。 此外，您可以在執行階段使用不同的租用值來更新訊息和不同的更新值在訊息中 hello 相同佇列。 服務匯流排鎖定逾時定義在 hello 佇列中繼資料。不過，您可以更新 hello 鎖定呼叫 hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock)方法。
* 封鎖接收作業在服務匯流排佇列 hello 最大逾時值是 24 天。 但是，REST 架構的最大逾時值為 55 秒。
* 用戶端批次處理由提供服務匯流排可讓佇列用戶端 toobatch 多個訊息成單一傳送作業。 批次處理僅適用於非同步傳送作業。
* Hello 200TB 上限的儲存體佇列 （當虛擬化帳戶時，此項會更多） 和無限的佇列等功能使得的理想平台 SaaS 提供者。
* 儲存體佇列提供彈性、高效能的委派存取控制機制。

## <a name="advanced-capabilities"></a>進階功能
本節將比較儲存體佇列和服務匯流排佇列所提供的進階功能。

| 比較準則 | 儲存體佇列 | 服務匯流排佇列 |
| --- | --- | --- |
| 排程傳遞 |**是** |**是** |
| 自動處理無效信件 |**否** |**是** |
| 增加佇列存留時間值 |**是**<br/><br/>(經由可視性逾時的就地更新) |**是**<br/><br/>(由專用 API 函式提供) |
| 有害訊息支援 |**是** |**是** |
| 就地更新 |**是** |**是** |
| 伺服器端交易記錄 |**是** |**否** |
| 儲存體度量 |**是**<br/><br/>**分鐘度量**：提供可用性、TPS、API 呼叫計數、錯誤計數等即時度量，全都即時 (每分鐘彙總一次並在生產環境中發生狀況的短短數分鐘內回報)。 如需詳細資訊，請參閱[關於儲存體分析度量](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics)。 |**是**<br/><br/>(透過呼叫 [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues) 來進行大量查詢) |
| 狀態管理 |**否** |**是**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active)、[Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled)、[Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled)、[Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| 訊息自動轉送 |**否** |**是** |
| 清除佇列函式 |**是** |**否** |
| 訊息群組 |**否** |**是**<br/><br/>（透過使用 hello 訊息工作階段） |
| 每個訊息群組的應用程式狀態 |**否** |**是** |
| 重複偵測 |**否** |**是**<br/><br/>（可在 hello 寄件者端設定） |
| 瀏覽訊息群組 |**否** |**是** |
| 依 ID 擷取訊息工作階段 |**否** |**是** |

### <a name="additional-information"></a>其他資訊
* 這兩種佇列技術可讓排程在稍後傳遞訊息 toobe。
* 佇列自動轉送可讓數以千計的佇列 tooauto 轉送其訊息 tooa 單一佇列，從哪一個 hello 接收應用程式會使用 hello 訊息。 您可以使用這個機制 tooachieve 安全性、 控制流程和每個訊息發行者之間隔離儲存區。
* 儲存體佇列支援更新訊息內容。 您可以使用這項功能的狀態資訊和累加進度更新保存至 hello 訊息，以便它可以從 hello 最後一個已知的檢查點，而不用從頭開始處理。 您可以使用服務匯流排佇列啟用 hello 透過 hello 訊息工作階段使用的相同案例。 工作階段 toosave 可讓您和擷取 hello 應用程式處理狀態 (使用[SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_)和[GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState))。
* [無作用 lettering](service-bus-dead-letter-queues.md)，這是唯一支援的服務匯流排佇列，可用於隔離 hello 接收應用程式無法順利處理的訊息或 tooan 時無法送達目的地到期的訊息已過期存留時間 (TTL) 屬性。 hello TTL 值會指定訊息保留的時間長度 hello 佇列中。 使用服務匯流排 hello 訊息將會移動的 tooa hello TTL 期限到期時，呼叫 $DeadLetterQueue 的特殊佇列。
* 在儲存體佇列，當取消佇列訊息 hello 應用程式會檢查 hello toofind 「 有害 」 訊息 **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  hello 訊息屬性。 如果**DequeueCount**大於給定的臨界值，hello 應用程式藉移動 hello 訊息 tooan 應用程式定義信件 」 佇列。
* 儲存體佇列可讓您 tooobtain 所有 hello 交易的詳細資訊記錄 hello 佇列中，針對執行，以及彙總度量資訊。 這兩個選項有助於偵錯和了解應用程式的儲存體佇列使用狀況。 它們也是適用於效能微調您的應用程式，並降低使用佇列的 hello 成本。
* 「 訊息工作階段 」 支援的服務匯流排 hello 概念可讓屬於 tooa 訊息與給定的接收者，接著會建立訊息與其個別的接收者之間的類似工作階段親和性相關聯的特定邏輯群組 toobe。 您可以啟用這項進階功能的服務匯流排所設定的 hello [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId)訊息上的屬性。 接收者可以接聽特定的工作階段識別碼並接收共用指定的 hello 訊息工作階段識別項。
* hello 重複偵測功能會自動支援的服務匯流排佇列中移除重複的訊息傳送 tooa 佇列或主題，根據 hello hello 值[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId)屬性。

## <a name="capacity-and-quotas"></a>容量和配額
本節將比較 Storage queues 和 Service Bus 佇列的 hello 觀點[容量和配額](service-bus-quotas.md)，可能會套用。

| 比較準則 | 儲存體佇列 | 服務匯流排佇列 |
| --- | --- | --- |
| 佇列大小上限 |**500 TB**<br/><br/>(有限的 tooa[單一儲存體帳戶容量](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(在建立佇列時定義和[啟用分割](service-bus-partitioning.md)– 請參閱 < 其他資訊 > 一節 hello) |
| 訊息大小上限 |**64 KB**<br/><br/>(使用 **Base64** 編碼時則為 48 KB)<br/><br/>Azure 支援大型訊息，藉由結合佇列和 blob – 此時，您可以向上 too200GB 單一項目加入佇列。 |**256 KB** 或 **1 MB**<br/><br/>(包括標頭和主體，標頭大小上限：64 KB)。<br/><br/>取決於 hello[服務層](service-bus-premium-messaging.md)。 |
| 訊息 TTL 上限 |**7 天** |**`TimeSpan.Max`** |
| 佇列數目上限 |**無限制** |**10,000**<br/><br/>(每個服務命名空間，可以增加) |
| 並行用戶端數目上限 |**無限制** |**無限制**<br/><br/>（100 的並行連線限制僅適用於 tooTCP 通訊協定為基礎的通訊） |

### <a name="additional-information"></a>其他資訊
* 服務匯流排會強制執行佇列大小限制。 hello 佇列大小上限在建立 hello 佇列時指定，且可以介於 1 到 80 GB 之間的值。 如果達到 hello 設定在建立 hello 佇列的佇列大小值時，其他內送訊息將會遭到拒絕，hello 呼叫程式碼程式會收到例外狀況。 如需服務匯流排中配額的詳細資訊，請參閱[服務匯流排配額](service-bus-quotas.md)。
* 在 hello[標準層](service-bus-premium-messaging.md)，您可以建立服務匯流排佇列 1、 2、 3、 4 或 5 GB 大小 （hello 預設為 1 GB）。 在 hello 優質層次中，您可以建立註冊 too80 GB 大小的佇列。 在標準層中的資料分割啟用 （此為 hello 預設）、 服務匯流排會為您指定每 GB 建立 16 個資料分割。 因此，如果您建立大小為 5 GB 的佇列時，16 個磁碟分割與 hello 佇列大小上限會變成 (5 * 16) = 80 GB。 您可以看到 hello 磁碟分割的佇列或主題的大小上限藉由查看其項目上 hello [Azure 入口網站][Azure portal]。 在 hello Premium 層，只有 2 個資料分割會建立每個佇列。
* 與儲存體佇列，如果 hello hello 訊息的內容不是 XML 安全的則它必須是**Base64**編碼。 如果您**Base64**-編碼 hello 訊息、 hello 使用者裝載可以是 up too48 KB，而不是 64 KB。
* 使用服務匯流排佇列時，儲存在佇列中的每個訊息都包含兩個部分：標頭和主體。 hello hello 訊息的大小總計不得超過 hello hello 服務層所支援的大小上限的訊息。
* 當用戶端與服務匯流排佇列通訊透過 hello TCP 通訊協定時，hello 的並行連線 tooa 單一服務匯流排佇列數目上限是有限的 too100。 這個數目是在傳送者和接收者之間共用的。 如果到達此配額，將會拒絕其他連線的後續要求，程式 hello 呼叫程式碼會收到例外狀況。 這項限制不會加諸連接 toohello 佇列使用 REST API 的用戶端上。
* 如果您需要超過 10,000 個佇列，單一的服務匯流排命名空間中，您可以連絡 hello Azure 支援小組，並要求增加。 超過 10,000 個佇列與服務匯流排 tooscale，您可以建立其他命名空間使用 hello [Azure 入口網站][Azure portal]。

## <a name="management-and-operations"></a>管理和作業
本節將比較儲存體佇列和服務匯流排佇列所提供的 hello 管理功能。

| 比較準則 | 儲存體佇列 | 服務匯流排佇列 |
| --- | --- | --- |
| 管理通訊協定 |**REST 透過 HTTP/HTTPS** |**REST 透過 HTTPS** |
| 執行階段通訊協定 |**REST 透過 HTTP/HTTPS** |**REST 透過 HTTPS**<br/><br/>**AMQP 1.0 標準 (具 TLS 的 TCP)** |
| .NET API |**是**<br/><br/>(.NET 儲存體用戶端 API) |**是**<br/><br/>(.NET 服務匯流排 API) |
| Native C++ |**是** |**是** |
| Java API |**是** |**是** |
| PHP API |**是** |**是** |
| Node.js API |**是** |**是** |
| 任意中繼資料支援 |**是** |**否** |
| 佇列命名規則 |**向上 too63 字元**<br/><br/>(佇列名稱的字母必須是小寫。) |**向上 too260 字元**<br/><br/>(佇列路徑和名稱不區分大小寫。) |
| 取得佇列長度函式 |**是**<br/><br/>（近似值如果訊息超出 hello TTL 過期而不被刪除。） |**是**<br/><br/>(精確的時間點值。) |
| 查看函式 |**是** |**是** |

### <a name="additional-information"></a>其他資訊
* 儲存體佇列可以套用的 toohello 佇列描述的名稱/值組的 hello 表單中的任意屬性提供支援。
* 這兩種佇列技術提供 hello 能力 toopeek 訊息而不需要 toolock it 實作佇列總管/瀏覽器工具時很有用。
* 服務匯流排.NET hello 代理訊息 Api 運用全雙工 TCP 連接來改善效能時比較 tooREST over HTTP，並支援 hello AMQP 1.0 標準通訊協定。
* 儲存體佇列名稱長度可以是 3-63 個字元，而且可以包含小寫字母、數字和連字號。 如需詳細資訊，請參閱[為佇列和中繼資料命名](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata)。
* 服務匯流排佇列名稱可以是 up too260 字元，並具有較不嚴格的命名規則。 服務匯流排佇列名稱可以包含字母、數字、句號、連字號和底線。

## <a name="authentication-and-authorization"></a>驗證和授權
本章節討論 hello 驗證和授權功能支援的儲存體佇列和服務匯流排佇列。

| 比較準則 | 儲存體佇列 | 服務匯流排佇列 |
| --- | --- | --- |
| 驗證 |**對稱金鑰** |**對稱金鑰** |
| 安全性模型 |透過 SAS 權杖進行委派存取。 |SAS |
| 識別提供者同盟 |**否** |**是** |

### <a name="additional-information"></a>其他資訊
* Hello 佇列技術的每個要求 tooeither 必須進行驗證。 不支援具有匿名存取的公用佇列。 使用 [SAS](service-bus-sas.md) 時，您可以發佈唯寫 SAS、唯讀 SAS 或甚至是完整存取 SAS 來解決這種情況。
* hello 驗證配置儲存體佇列牽涉到 hello 使用對稱金鑰，這是雜湊式訊息驗證碼 (HMAC)，提供與 hello sha-256 演算法計算並且編碼為**Base64**字串。 如需 hello 個別通訊協定的詳細資訊，請參閱[hello Azure 儲存體服務驗證](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services)。 服務匯流排佇列支援使用對稱金鑰的類似模型。 如需詳細資訊，請參閱[使用服務匯流排的共用存取簽章驗證](service-bus-sas.md)。

## <a name="conclusion"></a>結論
透過更深入了解 hello 兩項技術，您將會是較明智的佇列技術 toouse 無法 toomake 和時。 hello 當 toouse 儲存體佇列或服務匯流排清楚的佇列的決定取決於許多因素。 這些因素可能主要取決於您的應用程式和其架構 hello 個別需求。 如果您的應用程式已經使用 Microsoft Azure 的 hello 核心功能，您可能會想 toochoose 儲存體佇列，特別是當您需要的基本通訊和傳訊服務或可超過 80 GB 的大小需要佇列之間。

由於服務匯流排佇列提供許多進階功能 (例如工作階段、交易、重複偵測、自動處理無效信件和持久的發佈/訂閱功能)，如果您要建置混合應用程式或您的應用程式額外需要這些功能，則比較適合選擇這種佇列。

## <a name="next-steps"></a>後續步驟
hello 下列文章提供詳細指引和使用儲存體佇列或服務匯流排佇列的相關資訊。

* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [如何 tooUse hello 佇列儲存體服務](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [使用服務匯流排代理傳訊的效能改進最佳作法](service-bus-performance-improvements.md)
* [Azure 服務匯流排的佇列和主題簡介 (部落格文章)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [hello 開發人員指南 tooService 匯流排](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [在 Azure 中使用 hello 佇列服務](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

