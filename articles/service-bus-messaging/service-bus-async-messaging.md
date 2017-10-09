---
title: "aaaService 匯流排非同步傳訊 |Microsoft 文件"
description: "「Azure 服務匯流排」非同步傳訊說明。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>非同步傳訊模式和高可用性

有各種不同的方式可以實作非同步傳訊。 「Azure 服務匯流排」利用佇列、主題及訂用帳戶來支援透過儲存和轉送機制進行的非同步處理。 在正常 （同步） 作業中，您可以傳送訊息 tooqueues 和主題，並從佇列和訂閱接收訊息。 您撰寫的應用程式依存於這些實體永遠可用。 Hello 實體健全狀況變更時，由於 tooa 各種不同的情況下，您需要的方式 tooprovide 能夠滿足大多數需求的容量減少的實體。

應用程式通常使用非同步傳訊模式 tooenable 一些通訊案例。 您可以建置應用程式即使 hello 服務未執行用戶端可以傳送訊息 tooservices。 對於遇到大量通訊的應用程式，佇列可協助提供位置 toobuffer 通訊載入層級 hello。 最後，您可以取得簡單但有效率的負載平衡器 toodistribute 訊息在多部電腦。

在這些實體的任何順序 toomaintain 可用性，請考慮不同的方法，這些實體可以出現在長期訊息系統無法使用的數字。 一般而言，我們看到 hello 實體會變成無法使用 tooapplications hello 遵循不同的方式在我們寫入：

* 無法 toosend 訊息。
* 無法 tooreceive 訊息。
* 無法 toomanage 實體 （建立、 擷取、 更新或刪除實體）。
* 無法 toocontact hello 服務。

針對每個這些失敗情況，不同的失敗模式會讓某個層級的容量減少應用程式 toocontinue tooperform 工作。 例如，可傳送訊息但不會收到訊息的系統仍可以接收來自客戶的訂單，但無法處理這些訂單。 本主題討論可能發生的潛在問題，以及如何減輕這些問題。 服務匯流排已導入了一些您必須選擇加入，這與本主題也討論的 hello 規則 hello 控管使用這些選擇加入防護功能。

## <a name="reliability-in-service-bus"></a>服務匯流排的可靠性
有數種方式 toohandle 訊息和實體問題，而且都有控管 hello 適當使用這些防護功能的指導方針。 toounderstand hello 指導方針，您必須先了解什麼可以在服務匯流排失敗。 Toohello 設計 Azure 的系統，因為所有的這些問題通常 toobe 存留較短。 在高層級，hello 的不可用不同的原因如下：

* 從服務匯流排所依賴的外部系統節流。 從與儲存體和運算資源的互動進行節流。
* 服務匯流排所依賴系統的問題。 例如，指定的儲存體部份可能會發生問題。
* 單一子系統上的服務匯流排失敗。 在此情況下，計算節點可以進入不一致的狀態，且必須重新啟動本身，造成所有的實體做 tooload 平衡 tooother 節點。 這又會導致短期內的訊息處理速度緩慢。
* Azure 資料中心內的服務匯流排失敗。 這是在 hello 系統是無法連線到數分鐘或幾個小時的 「 災難性失敗 」。

> [!NOTE]
> hello 詞彙**儲存體**可代表 Azure 儲存體和 SQL Azure。
> 
> 

對於這些問題，服務匯流排有數種緩和措施。 hello 下列各節會討論每個問題，以及其各別的防護功能。

### <a name="throttling"></a>節流
使用服務匯流排，節流可達到協同合作的訊息速率管理。 每個個別的服務匯流排節點都容納許多實體。 每個實體 CPU、 記憶體、 存放裝置，和其他方面的 hello 系統提出需求。 當上述任何面向偵測到超出所定義臨界值的使用量時，服務匯流排可以拒絕指定的要求。 hello 呼叫端會收到[ServerBusyException] [ ServerBusyException]和 10 秒後的重試。

做為防護功能，hello 程式碼必須讀取 hello 錯誤並停止 hello 訊息的任何重試至少 10 秒。 Hello 錯誤可能會發生跨 hello 客戶應用程式項目，因為它預期每個都能獨立執行 hello 重試邏輯。 hello 程式碼可以降低啟用佇列或主題上的分割區會進行節流處理 hello 機率。

### <a name="issue-for-an-azure-dependency"></a>Azure 相依性問題
Azure 中的其他元件可能會不時出現服務問題。 例如，當服務匯流排使用的系統正在升級時，該系統可能會暫時經歷降低的功能。 這些類型的問題，服務匯流排定期 toowork 調查並實作防護功能。 這些緩和措施的確會出現副作用。 例如，toohandle 暫時性問題的儲存體、 服務匯流排實作系統，可讓訊息傳送作業 toowork 一致的方式。 Hello 緩和 toohello 本質，因為傳送的訊息可以佔用 too15 分鐘 tooappear hello 受影響的佇列或訂閱中，並準備好可供接收作業。 一般而言，大部分實體不會發生這個問題。 不過，在 Azure 中的服務匯流排中給定實體的 hello 數目，此防護功能有時需要的服務匯流排客戶的小型子集。

### <a name="service-bus-failure-on-a-single-subsystem"></a>單一子系統上的服務匯流排失敗
任何應用程式，情況可能會造成不一致的服務匯流排 toobecome 的內部元件。 當服務匯流排偵測到此時，它會收集資料 hello 應用程式 tooaid 診斷發生了什麼事。 一旦 hello 資料收集，hello 應用程式是在重新啟動嘗試 tooreturn 它 tooa 一致的狀態。 此程序會相當快速，而結果中實體無法向上 tooa toobe 幾分鐘的時間，但一般停機時間較短。

在這些情況下，hello 用戶端應用程式會產生[System.TimeoutException] [ System.TimeoutException]或[MessagingException] [ MessagingException]例外狀況。 服務匯流排包含自動化用戶端重試邏輯的 hello 形式問題防護功能。 一旦 hello 重試期間已用完，且不會傳送 hello 訊息，您可以瀏覽使用其他功能，例如[配對命名空間][paired namespaces]。 配對的命名空間有其他需要的注意事項 (請見該文章中的討論)。

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Azure 資料中心內的服務匯流排失敗
hello Azure 資料中心失敗的最可能的原因是服務匯流排或相依系統的升級部署失敗。 因為 hello 平台日趨成熟，已大幅降低 hello 可能性，這種類型的失敗。 資料中心失敗的可能發生的原因包括下列 hello:

* 電力中斷 (電源和供電失效)。
* 連線 (用戶端與 Azure 之間的網際網路中斷)。

在這兩種情況下，自然或二災害 hello 問題原因。 toowork 解決這個問題，請確定您仍然可以傳送訊息，您可以使用[配對命名空間][ paired namespaces] tooenable 時 hello 主要位置運作正常之後，訊息傳送的 toobe tooa 第二個位置。 如需詳細資訊，請參閱[將應用程式與服務匯流排中斷和災難隔絕的最佳做法 (英文)][Best practices for insulating applications against Service Bus outages and disasters]。

## <a name="paired-namespaces"></a>配對的命名空間
hello[配對命名空間][ paired namespaces]功能支援案例中無法使用服務匯流排實體或資料中心內的部署。 雖然這個事件不常發生，分散式的系統仍然必須準備 toohandle 最糟的情況。 通常會因為服務匯流排所依賴的某個元素遇到短期問題而發生此事件。 toomaintain 應用程式可用性中斷，在服務匯流排使用者可以使用兩個不同的命名空間，最好是在不同的資料中心，toohost 其訊息實體。 hello 本節其餘部分會使用下列詞彙的 hello:

* 主要命名空間： hello 命名空間與您的應用程式互動，傳送和接收作業。
* 次要命名空間： hello 做為備份 toohello 主要命名空間的命名空間。 應用程式邏輯不會與此命名空間互動。
* 容錯移轉間隔： hello 數量時間 tooaccept 正常失敗之前 hello 應用程式切換 hello 主要命名空間 toohello 次要命名空間中。

配對的命名空間支援「傳送可用性」。 傳送可用性會保留 hello 能力 toosend 訊息。 toouse 傳送可用性，您的應用程式必須符合下列需求的 hello:

1. 訊息只會收到 hello 主要命名空間。
2. 給定的佇列或主題傳送的訊息 tooa 可能到達順序。
3. 工作階段內的訊息可能不會按順序抵達。 這是工作階段的正常功能毀損。 這表示您的應用程式會使用訊息工作階段 toologically 分組。
4. Hello 主要命名空間只會保留工作階段狀態。
5. hello 主要佇列可以上線，而 hello 次要佇列傳遞所有訊息到 hello 主要佇列之前開始接受訊息。

hello 下列各節討論 hello Api、 hello 應用程式開發介面中實作方式，以及顯示範例程式碼使用 hello 功能。 請注意，這項功能有相關聯的計費暗示。

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>hello MessagingFactory.PairNamespaceAsync API
hello 配對的命名空間功能包括 hello [PairNamespaceAsync] [ PairNamespaceAsync]方法上 hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [Microsoft.ServiceBus.Messaging.MessagingFactory]類別：

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Hello 工作完成時，hello 命名空間配對也是完成並準備 tooact 時任何[MessageReceiver][MessageReceiver]， [QueueClient] [ QueueClient]，或[TopicClient] [ TopicClient]建立以 hello [MessagingFactory] [ MessagingFactory]執行個體。 [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]是 hello hello 基底類別不同型別的配對，可用之[MessagingFactory] [MessagingFactory]物件。 目前，hello 衍生類別只是一個名為[SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions]，它會實作 hello 傳送可用性需求。 [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] 有一組建立在彼此之上的建構函式。 查看 hello 建構函式以 hello 大部分的參數，您可以了解 hello 行為 hello 其他建構函式。

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

這些參數具有下列意義 hello:

* *secondaryNamespaceManager*： 初始化[NamespaceManager] [ NamespaceManager]例項而言 hello 次要命名空間的 hello [PairNamespaceAsync][ PairNamespaceAsync]方法可以使用 tooset hello 次要命名空間。 hello 命名空間管理員是使用的 tooobtain hello hello 命名空間和 toomake 確定存在所需的 hello 待處理項目佇列中的佇列清單。 如果這些佇列不存在，則會加以建立。 [NamespaceManager] [ NamespaceManager]需要 hello 能力 toocreate hello 的語彙基元**管理**宣告。
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] hello 次要命名空間的執行個體。 hello [MessagingFactory] [ MessagingFactory]物件是使用的 toosend，而如果 hello [EnableSyphon] [ EnableSyphon]屬性設定太**，則為 true**，從 hello 待處理項目佇列接收訊息。
* *backlogQueueCount*： 排入佇列，toocreate hello 待處理項目數目。 此值必須至少為 1。 當傳送訊息 toohello 待處理項目，會隨機選擇其中一個佇列。 如果您設定 hello 值 too1，只有一個佇列可以曾經使用。 當發生這種情況，hello 積存佇列產生錯誤時 hello 用戶端不能 tootry 不同的積存佇列，並可能會失敗 toosend 您的訊息。 我們建議您設定此值 toosome 較大值和預設 hello 值 too10。 您可以變更此 tooa 較高或較低的值，視資料量而定每天傳送您的應用程式。 每個積存佇列可以阻擋 too5 GB 的訊息。
* *failoverInterval*: hello 一段期間將會接受 hello 主要命名空間上的失敗之前切換 toohello 次要命名空間中的任何單一實體的時間。 容錯移轉會以逐一實體的方式進行。 單一命名空間中的實體經常留存在服務匯流排中的不同節點。 某一個實體失敗不表示另一個實體也失敗。 您可以將此值太[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello 您第一次、 非暫時性失敗後立即次要。 Hello 容錯移轉計時器觸發程序的失敗是否有任何[MessagingException] [ MessagingException]中的 hello [IsTransient] [ IsTransient]屬性為 false，或[System.TimeoutException][System.TimeoutException]。 其他例外狀況，例如[UnauthorizedAccessException] [ UnauthorizedAccessException]並不會造成容錯移轉，因為它們表示該 hello 用戶端設定不正確。 A [ServerBusyException] [ ServerBusyException]不會致使容錯移轉由於 hello 正確模式為 toowait 10 秒，然後傳送 hello 訊息一次。
* *enableSyphon*： 表示此特殊的配對應該也會虹吸 hello 次要命名空間後 toohello 主要命名空間中的訊息。 一般情況下，傳送訊息的應用程式應該將此值太**false**; 接收訊息的應用程式應將此值設定太**true**。 hello 原因是，經常有較少的訊息接收端可比傳送的訊息。 根據 hello 接收者數目，您可以選擇 toohave 單一應用程式執行個體控制代碼 hello 虹吸工作。 使用許多接收端會牽涉到每個待處理項目佇列的計費。

toouse hello 程式碼，請建立主要[MessagingFactory] [ MessagingFactory]執行個體，次要[MessagingFactory] [ MessagingFactory]執行個體，次要資料庫[NamespaceManager] [ NamespaceManager]執行個體，和[SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions]執行個體。 hello 呼叫很簡單，如下所示 hello:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

當 hello hello 所傳回工作[PairNamespaceAsync] [ PairNamespaceAsync]方法完成、 設定和準備 toouse 的所有內容。 Hello 工作傳回前，您可能尚未完成所有 hello 背景工作所需的 hello 配對 toowork 權限。 如此一來，您不應開始傳送訊息，直到 hello 工作傳回。 如果發生任何失敗，例如認證錯誤或失敗 toocreate hello 待處理項目佇列 hello 工作完成之後將會擲回這些例外狀況。 一旦傳回 hello 工作，確認已找到 hello 佇列，或藉由檢查 hello 建立[BacklogQueueCount] [ BacklogQueueCount]屬性您[SendAvailabilityPairedNamespaceOptions][ SendAvailabilityPairedNamespaceOptions]執行個體。 Hello 前面程式碼，該作業會出現，如下所示：

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>後續步驟
現在，您學到的非同步傳訊服務匯流排中的 hello 基本概念，閱讀更多詳細資料[配對命名空間][paired namespaces]。

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
