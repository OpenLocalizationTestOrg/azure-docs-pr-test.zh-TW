---
title: "改善效能，使用 Azure Service Bus aaaBest 作法 |Microsoft 文件"
description: "描述如何 toouse 交換時，服務匯流排 toooptimize 效能代理訊息。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>使用服務匯流排傳訊的效能改進最佳作法

本文說明如何 toouse [Azure 服務匯流排傳訊](https://azure.microsoft.com/services/service-bus/)toooptimize 效能時交換代理訊息。 hello 本主題的第一個部分說明 hello 不同的機制，提供 toohelp 增加效能。 hello 第二個部分提供指引 toouse Service Bus 可以提供的方式如何 hello 在指定案例最佳效能。

本主題中，整個 hello 詞彙 「 用戶端 」 是指 tooany 實體存取服務匯流排。 用戶端可以擔任傳送者或接收者的 hello 角色。 hello 詞彙 「 寄件者 」 用於服務匯流排佇列或主題用戶端傳送的郵件 tooa 服務匯流排佇列或主題。 hello 詞彙 「 接收者 」 是指 tooa 服務匯流排佇列或訂閱用戶端會接收來自服務匯流排佇列或訂閱訊息。

下列各節介紹數個服務匯流排使用 toohelp 提升效能的概念。

## <a name="protocols"></a>通訊協定
服務匯流排可讓用戶端 toosend 和接收訊息，透過三種通訊協定之一：

1. 進階訊息佇列通訊協定 (AMQP)
2. 服務匯流排傳訊通訊協定 (SBMP)
3. HTTP

AMQP 和 SBMP 會更有效率，因為它們會維護 hello 連接 tooService 匯流排，只要存在 hello 訊息 factory。 它也會實作批次處理和預先擷取作業。 除非明確所述，本主題中的所有內容會都假設 hello 使用 AMQP 或 SBMP。

## <a name="reusing-factories-and-clients"></a>重複使用處理站和用戶端
服務匯流排用戶端物件，例如 [QueueClient][QueueClient] 或 [MessageSender][MessageSender]，會透過也提供內部連接管理的 [MessagingFactory][MessagingFactory] 物件來建立。 您應該關閉訊息中心或佇列、 主題及訂閱用戶端傳送訊息，並再重新建立它們時傳送嗨下一個訊息之後。 關閉訊息中心刪除 hello 連接 toohello 服務匯流排服務，並重新建立 hello 處理站時，建立新的連接。 建立連接，您可以避免重複使用昂貴的作業 hello 相同的處理站和用戶端物件的多個作業。 您可以安全地使用 hello [QueueClient] [ QueueClient]物件以傳送訊息，從並行的非同步作業和多個執行緒。 

## <a name="concurrent-operations"></a>並行作業
執行作業 (傳送、接收、刪除等等) 需要一點時間。 此時根據 hello 服務匯流排服務包括 hello 處理 hello 作業的加法 toohello 延遲 hello 要求與 hello 回覆中。 tooincrease hello 數字，每次的作業，必須同時執行作業。 您可以利用數個不同方式執行這項操作：

* **非同步作業**: hello 用戶端所執行的非同步作業排程的作業。 hello 前一個要求完成之前，會發出 hello 下一個要求。 hello 下列是非同步傳送作業的範例：
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  非同步接收作業的範例如下：
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **多個中心**： 所有用戶端 （傳送者在加法 tooreceivers） 所建立的 hello 相同 factory 共用一個 TCP 連線。 hello 最大訊息輸送量受限於 hello 可以透過此 TCP 連線的作業數目。 可以透過單一中心取得的 hello 輸送量與 TCP 來回行程時間和訊息大小的極大的不同。 tooobtain 更高的輸送量速率，您應該使用多個訊息中心。

## <a name="receive-mode"></a>接收模式
建立佇列或訂用帳戶用戶端時，您可以指定接收模式：「查看鎖定」或「接收與刪除」。 hello 預設接收模式是[PeekLock][PeekLock]。 以這種模式操作時，hello 用戶端傳送要求 tooreceive 訊息從服務匯流排。 Hello 用戶端收到 hello 訊息後，它會傳送要求 toocomplete hello 訊息。

當太設定 hello 接收模式[ReceiveAndDelete][ReceiveAndDelete]，這兩個步驟會結合在單一要求中。 這可減少 hello 總次數的作業，並可改善 hello 整體訊息輸送量。 此效能提升伴隨 hello 風險的遺失訊息。

服務匯流排不支援接收和刪除作業的交易。 此外，查看並鎖定語意的案例所需的任何在哪一個 hello 用戶端想要 toodefer 或[寄不出信件](service-bus-dead-letter-queues.md)訊息。

## <a name="client-side-batching"></a>用戶端批次處理
用戶端批次處理可讓佇列或主題用戶端 toodelay hello 訊息傳送的一段時間的時間。 如果 hello 用戶端會傳送其他訊息，此期間內，它將以單一批次的 hello 訊息傳輸。 用戶端批次處理也會導致佇列或訂閱的用戶端 toobatch 多個**完成**結合為單一要求的要求。 批次處理僅適用於非同步**傳送**及**完成**作業。 同步作業會立即傳送 toohello 服務匯流排服務。 查看或接收作業不會進行批次處理，也不會跨用戶端進行。

根據預設，用戶端使用的批次間隔為 20 毫秒。 您可以變更設定 hello hello 批次間隔[BatchFlushInterval] [ BatchFlushInterval]屬性，才能建立 hello 訊息 factory。 這個設定會影響此處理站所建立的所有用戶端。

toodisable 批次處理，設定 hello [BatchFlushInterval] [ BatchFlushInterval]屬性太**TimeSpan.Zero**。 例如：

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

批次處理不會影響 hello 可計費訊息作業數目，並僅供 hello 服務匯流排用戶端通訊協定。 hello HTTP 通訊協定不支援批次處理。

## <a name="batching-store-access"></a>批次處理存放區存取
tooincrease hello 輸送量佇列、 主題或訂用帳戶的服務匯流排批次多個訊息時就會將寫入 tooits 內部存放區。 如果啟用佇列或主題，會進行批次處理訊息寫入到 hello 存放區。 如果啟用佇列或訂閱，會進行批次處理從 hello 存放區刪除訊息。 如果實體啟用批次存放區存取時，服務匯流排會延遲對於向上 too20ms 所實體存放區寫入作業。 此間隔期間發生的其他存放區作業會加入 toohello 批次。 批次處理的存放區存取只會影響**傳送**和**完成**作業；接收作業不會受到影響。 批次處理的存放區存取是實體上的屬性。 批次處理會在啟用批次處理存放區存取的所有實體進行。

建立新佇列、主題或訂用帳戶時，預設會啟用批次處理的存放區存取。 toodisable 批次存放區存取，集合 hello [EnableBatchedOperations] [ EnableBatchedOperations]屬性太**false**之前建立 hello 的實體。 例如：

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

批次存放區存取並不會影響 hello 可計費訊息作業數目，而且是佇列、 主題或訂用帳戶的屬性。 它是獨立的 hello 接收模式和 hello 使用用戶端與 hello 服務匯流排服務之間的通訊協定。

## <a name="prefetching"></a>預先擷取
執行接收作業時，預先擷取可讓 hello 佇列或訂閱用戶端 tooload 額外的訊息從 hello 服務。 hello 用戶端會將這些訊息儲存在本機快取。 hello hello 快取大小由 hello [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount]或[SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount]屬性。 啟用預先擷取的每個用戶端會維護自己的快取。 快取不會跨用戶端共用。 如果 hello 用戶端起始接收作業，而且其快取是空的 hello 服務會傳輸一批訊息。 hello hello 批次大小等於 hello hello 快取或 256 KB 的大小，以較小。 如果 hello 用戶端起始接收作業 hello 快取包含一則訊息，hello 訊息是來自 hello 快取中。

當訊息預先提取，hello 服務鎖定 hello 預先擷取的訊息。 如此一來，hello 預先擷取的訊息無法接收不同的接收者。 如果 hello 接收者 hello 鎖定到期之前，無法完成 hello 訊息，hello 訊息會變成可用 tooother 接收者。 預先提取的 hello hello 訊息副本會保留在 hello 快取。 hello 接收器，以便取用 hello 過期快取嘗試 toocomplete 該訊息時，複製將會收到例外狀況。 根據預設，hello 訊息鎖定 60 秒之後到期。 這個值可以是擴充的 too5 分鐘。 過期的訊息 tooprevent hello 耗用量，hello 快取大小一律應小於 hello 可供用戶端 hello 鎖定逾時間隔內的訊息數目。

使用 60 秒的 hello 預設鎖定到期時，理想值[SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount]上限的 20 倍 hello 會處理所有接收者 hello factory 的速度。 例如，中心建立 3 個接收者，而且每個接收者可以處理 too10 每秒的訊息。 hello 預先擷取計數不應該超過 20 X 3 X 10 = 600。 根據預設， [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount]是集 too0，表示從 hello 服務擷取任何額外的訊息。

預先擷取訊息會增加 hello 的佇列或訂閱的整體輸送量，因為它可以減少 hello 訊息作業或來回行程的整體數目。 擷取 hello 第一則訊息，不過，將會延長 （因為 toohello 增加訊息大小）。 接收預先擷取的訊息將會比較快，因為 hello 用戶端已下載這些訊息。

hello 伺服器會檢查訊息的 hello 存留時間 (TTL) 屬性，在 hello 伺服器會傳送 hello 訊息 toohello 用戶端 hello 階段。 hello 用戶端收到 hello 訊息時，不會檢查 hello 訊息的 TTL 屬性。 相反地，即使 hello 訊息 TTL 已通過由 hello 用戶端快取的 hello 訊息時，可以收到 hello 訊息。

預先擷取不會影響 hello 可計費訊息作業數目，並僅供 hello 服務匯流排用戶端通訊協定。 hello HTTP 通訊協定不支援預先擷取。 同步和非同步接收作業皆可使用預先擷取。

## <a name="express-queues-and-topics"></a>快速佇列和主題

快速實體啟用高輸送量和低的延遲案例，而且只支援 hello 標準通訊層。 所建立的實體[Premium 命名空間](service-bus-premium-messaging.md)不支援 hello express 的選項。 使用快速實體時，如果 tooa 佇列或主題時，會將訊息傳送 hello 訊息不立即會儲存在 hello 訊息存放區。 相反地，它會快取在記憶體中。 如果訊息保留在佇列中的 hello 超過幾秒鐘，它會自動寫入 toostable 存放裝置，藉此保護到期 tooan 中斷不會遺失。 寫入記憶體快取的 hello 訊息會增加輸送量並降低延遲，因為沒有存取 toostable 傳送的 hello 時間 hello 訊息儲存。 在幾秒鐘內耗用的訊息不會寫入 toohello 訊息存放區。 hello 下列範例會建立快速主題。

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

如果包含不可遺失的重要資訊的訊息傳送 tooan 快速實體，hello 寄件者可以強制執行服務匯流排 tooimmediately 保存 hello 訊息 toostable 存放裝置設定 hello [ForcePersistence] [ForcePersistence]屬性太**true**。

> [!NOTE]
> 快速實體並不支援交易。

## <a name="use-of-partitioned-queues-or-topics"></a>使用分割的佇列或主題
就內部而言，Service Bus 使用相同的節點和訊息存放區 tooprocess hello 和儲存訊息實體 （佇列或主題） 的所有訊息。 磁碟分割的佇列或主題上 hello，換句話說，都會分散到多個節點和訊息存放區。 分割的佇列和主題不僅會產生比一般佇列和主題更高的輸送量，也會展現較優異的可用性。 toocreate 的資料分割的實體集 hello [EnablePartitioning] [ EnablePartitioning]屬性太**true**hello 下列範例所示。 如需分割實體的詳細資訊，請參閱[分割的傳訊實體][Partitioned messaging entities]。

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>使用多個佇列

如果不可能 toouse 分割的佇列或主題或 hello 預期負載無法處理的單一磁碟分割的佇列或主題，您必須使用多個訊息實體。 當使用多個實體，建立專用的用戶端，每個實體，而不是使用 hello 相同用戶端的所有實體。

## <a name="development-and-testing-features"></a>開發與測試功能

服務匯流排有一項專門用於開發的功能，此功能**永遠不應該用在生產組態**：[TopicDescription.EnableFilteringMessagesBeforePublishing][]。

當新的規則或篩選器加入 toohello 主題時，您可以使用[TopicDescription.EnableFilteringMessagesBeforePublishing][] hello 新的篩選條件運算式的 tooverify 是否正常運作。

## <a name="scenarios"></a>案例
hello 下列各節描述一般傳訊案例，並簡述慣用的 hello 服務匯流排設定。 輸送量速率會分類為小型 (小於 1 則訊息/秒)、中型 (1 則訊息/秒或更多但小於 100 則訊息/秒) 和高型 (100 則訊息/秒或更多)。 hello 的用戶端數目可分為小 （5 或更少），「 中 」 (5 個以上但小於或等於 too20)，和大 （超過 20）。

### <a name="high-throughput-queue"></a>高輸送量佇列
目標： 在單一佇列的 hello 輸送量最大化。 hello 傳送者和接收者數目很小。

* 使用分割的佇列以改善效能和可用性。
* tooincrease hello 整體傳送速率，到 hello 佇列，請使用多個訊息 factory toocreate 寄件者。 對每個傳送者使用非同步作業或多個執行緒。
* 整體 tooincrease hello 從 hello 佇列接收速率，請使用多個訊息 factory toocreate 接收者。
* 使用非同步作業 tootake 利用用戶端批次處理。
* 設定批次處理間隔 too50ms tooreduce hello 數量的服務匯流排用戶端通訊協定傳送 hello。 如果使用多個傳送者，請增加批次處理間隔 too100ms hello。
* 讓批次處理的存放區存取保持啟用。 這會增加整體的 hello 訊息可以寫入 hello 佇列的速率。
* 設定 hello 預先擷取計數 too20 時間 hello 處理速率上限的所有接收者處理站。 這會減少 hello 服務匯流排用戶端通訊協定傳輸數目。

### <a name="multiple-high-throughput-queues"></a>多個高輸送量佇列
目標：最大化多個佇列的整體輸送量。 個別佇列的 hello 輸送量為中或大。

tooobtain 橫跨多個佇列的最大輸送量，使用 hello 設定概述 toomaximize hello 單一佇列輸送量。 此外，使用不同的處理站 toocreate 的用戶端傳送或接收來自不同的佇列。

### <a name="low-latency-queue"></a>低延遲性佇列
目標：最小化佇列或主題的端對端延遲。 hello 傳送者和接收者數目很小。 hello 佇列的 hello 輸送量為小或中度。

* 使用分割的佇列以改善可用性。
* 停用用戶端批次處理。 hello 用戶端會立即傳送訊息。
* 停用批次處理的存放區存取。 hello 服務會立即寫入 hello 訊息 toohello 存放區。
* 如果使用單一用戶端，設定 hello 預先擷取計數 too20 時間 hello 處理速度的 hello 接收器。 如果多個訊息到達 hello 佇列 hello 在相同時間，hello 服務匯流排用戶端通訊協定傳送 hello 的所有項目相同的時間。 Hello 用戶端收到 hello 下一個訊息時，該訊息會已經在 hello 本機快取。 hello 快取應該很小。
* 如果使用多個用戶端，設定 hello 預先擷取計數 too0。 如此一來，hello 第二個用戶端可以接收 hello 第二個訊息時 hello 第一個用戶端仍在處理 hello 第一則訊息。

### <a name="queue-with-a-large-number-of-senders"></a>具有大量傳送者的佇列
目標：最大化具有大量傳送者之佇列或主題的輸送量。 每個傳送者都會以中等速率傳送訊息。 hello 接收者數目很小。

服務匯流排可讓向上 too1000 並行連線 tooa 訊息實體 (5000 個使用 AMQP)。 在 hello 命名空間層級，會強制執行這項限制，佇列/主題/訂閱會受限於 hello 每個命名空間的並行連線限制。 對佇列而言，這個數目是在傳送者和接收者之間共用的。 如果所有的 1000 個連接所需的寄件者，您應該以主題和單一訂閱取代 hello 佇列。 主題會接受 too1000 寄件者，並行連線，而 hello 訂用帳戶接受接收者其他 1000 個並行連接。 如果需要超過 1000 個並行的寄件者，hello 寄件者應該傳送訊息 toohello 透過 HTTP 的服務匯流排通訊協定。

toomaximize 輸送量，請勿遵循 hello:

* 使用分割的佇列以改善效能和可用性。
* 如果每個傳送者都位於不同的處理序中，每個處理序僅使用單一處理站。
* 使用非同步作業 tootake 利用用戶端批次處理。
* 使用 hello 毫秒預設批次處理間隔的 20 毫秒 tooreduce hello 服務匯流排用戶端通訊協定傳輸數目。
* 讓批次處理的存放區存取保持啟用。 這會增加整體的 hello 的訊息可以寫入的速率 hello 佇列或主題。
* 設定 hello 預先擷取計數 too20 時間 hello 處理速率上限的所有接收者處理站。 這會減少 hello 服務匯流排用戶端通訊協定傳輸數目。

### <a name="queue-with-a-large-number-of-receivers"></a>具有大量接收者的佇列
目標： 最大化 hello 接收的佇列或訂閱具有大量接收者的速率。 每個接收者皆以中等速率接收訊息。 hello 寄件者數目很小。

服務匯流排可讓向上 too1000 並行連線 tooan 實體。 如果佇列需要超過 1000 個接收者，您應該以主題和多個訂閱取代 hello 佇列。 每個訂用帳戶可以支援 too1000 並行連線。 或者，接收者可以存取透過 HTTP 通訊協定 hello hello 佇列。

toomaximize 輸送量，請勿遵循 hello:

* 使用分割的佇列以改善效能和可用性。
* 如果每個接收者都位於不同的處理序中，每個處理序僅使用單一處理站。
* 接收者可以使用同步或非同步作業。 指定的 hello 中度的接收設定個別接收者的速率，用戶端批次處理完成的要求不會影響接收者輸送量。
* 讓批次處理的存放區存取保持啟用。 這會減少 hello hello 實體的整體負載。 它也會減少 hello，可以將訊息寫入 hello 佇列或主題的整體速率。
* 設定 hello 預先擷取計數 tooa 小的值 (例如，PrefetchCount = 10)。 這樣可以避免接收者在其他接收者具有大量快取的訊息時閒置。

### <a name="topic-with-a-small-number-of-subscriptions"></a>具有少量訂用帳戶的主題
目標： 具有少量訂閱的主題的 hello 輸送量最大化。 收到的訊息是許多訂閱，這表示 hello 結合接收所有訂閱的速度大於 hello 傳送速率。 hello 寄件者數目很小。 每個訂閱接收者的 hello 數目很小。

toomaximize 輸送量，請勿遵循 hello:

* 使用分割的主題以改善效能和可用性。
* tooincrease hello 整體傳送速率，到 hello 主題，請使用多個訊息 factory toocreate 寄件者。 對每個傳送者使用非同步作業或多個執行緒。
* 整體 tooincrease hello 從訂閱接收速率，請使用多個訊息 factory toocreate 接收者。 對每個接收者使用非同步作業或多個執行緒。
* 使用非同步作業 tootake 利用用戶端批次處理。
* 使用 hello 毫秒預設批次處理間隔的 20 毫秒 tooreduce hello 服務匯流排用戶端通訊協定傳輸數目。
* 讓批次處理的存放區存取保持啟用。 這會增加整體的 hello 訊息可以寫入 hello 主題速率。
* 設定 hello 預先擷取計數 too20 時間 hello 處理速率上限的所有接收者處理站。 這會減少 hello 服務匯流排用戶端通訊協定傳輸數目。

### <a name="topic-with-a-large-number-of-subscriptions"></a>具有大量訂用帳戶的主題
目標： 具有大量訂閱的主題的 hello 輸送量最大化。 收到的訊息是許多訂閱，這表示 hello 結合接收所有訂閱的速度會遠大於 hello 傳送速率。 hello 寄件者數目很小。 每個訂閱接收者的 hello 數目很小。

如果所有的訊息路由的 tooall 訂用帳戶具有大量訂閱的主題通常會呈現低的整體輸送量。 這被因為 hello 事實收到許多次，每個訊息，並包含在主題中的所有訊息，以及所有其訂用帳戶會儲存在 hello 相同存放區。 它會假設 hello 寄件者數目和每個訂閱的接收者數目很小。 服務匯流排支援向上 too2，每個主題 000 訂用帳戶。

toomaximize 輸送量，請勿遵循 hello:

* 使用分割的主題以改善效能和可用性。
* 使用非同步作業 tootake 利用用戶端批次處理。
* 使用 hello 毫秒預設批次處理間隔的 20 毫秒 tooreduce hello 服務匯流排用戶端通訊協定傳輸數目。
* 讓批次處理的存放區存取保持啟用。 這會增加整體的 hello 訊息可以寫入 hello 主題速率。
* 設定速率 hello 預期收到 hello 預先擷取計數 too20 時間，以秒為單位。 這會減少 hello 服務匯流排用戶端通訊協定傳輸數目。

## <a name="next-steps"></a>後續步驟
toolearn 有關 Service Bus 效能最佳化的詳細資訊請參閱[分割訊息實體][Partitioned messaging entities]。

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
