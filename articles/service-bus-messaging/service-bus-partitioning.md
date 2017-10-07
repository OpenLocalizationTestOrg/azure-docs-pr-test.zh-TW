---
title: "aaaCreate 分割 Azure 服務匯流排佇列和主題 |Microsoft 文件"
description: "描述如何 toopartition Service Bus 佇列和主題，使用多個訊息仲介。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>分割的佇列和主題
Azure 的服務匯流排會運用多個訊息代理人 tooprocess 訊息和多個訊息存放 toostore 訊息。 傳統的佇列或主題由單一訊息代理程式處理並儲存在一個訊息存放區中。 服務匯流排*分割*啟用佇列和主題，或*傳訊實體*，toobe 分割到多個訊息代理程式和訊息存放區。 Hello 磁碟分割實體的整體輸送量這表示不再受限於單一訊息代理程式或訊息存放區的 hello 效能。 此外，即使訊息存放區暫時中斷也不會讓分割的佇列或主題無法使用。 分割的佇列和主題可以包含所有進階的服務匯流排功能，例如支援交易和工作階段。

如需服務匯流排內部項目資訊，請參閱 hello [Service Bus 架構][ Service Bus architecture]發行項。

在標準和進階傳訊中，依預設，在所有佇列和主題上建立實體時會啟用分割。 您可以建立標準傳訊層實體而不要分割，但進階命名空間中的佇列和主題永遠會分割。無法停用此選項。 

不可能 toochange hello 資料分割上現有的佇列或主題 Standard 或 Premium 層中的選項，您可以只 hello 時設定選項建立 hello 實體。

## <a name="how-it-works"></a>運作方式

每個分割的佇列或主題都包含多個片段。 每個片段儲存在不同的訊息存放區中，並由不同的訊息代理人處理。 當訊息傳送 tooa 分割的佇列或主題時，服務匯流排會指派 hello 訊息 tooone 的 hello 片段。 hello 選取項目由隨機服務匯流排，或者可以指定使用 hello 寄件者資料分割索引鍵。

當用戶端想 tooreceive 將訊息從資料分割的佇列或訂閱 tooa 分割主題，從服務匯流排查詢訊息的所有片段時，然後傳回 hello 取自任何 hello 訊息存放區 toohello 收件者的第一個訊息。 服務匯流排快取 hello 其他的訊息並傳回它們收到其他時接收要求。 接收用戶端並不知道 hello 資料分割;hello 面對用戶端行為的分割的佇列或主題 (例如 read、 complete、 defer、 deadletter、 預先提取) 是相同的 toohello 行為的一般實體。

傳送訊息給分割的佇列或主題，或從該處接收訊息時，不需要額外成本。

## <a name="enable-partitioning"></a>啟用分割

toouse 分割佇列和主題與 Azure 服務匯流排，使用 hello Azure SDK 版本 2.2 或更新版本，或指定`api-version=2013-10`在您的 HTTP 要求。

### <a name="standard"></a>標準

在 hello 標準通訊層，您可以建立服務匯流排佇列和主題 1、 2、 3、 4 或 5 GB 大小 （hello 預設為 1 GB）。 啟用分割，服務匯流排會建立您指定每個 GB 的 hello 實體 16 的複本 （16 個磁碟分割）。 因此，如果您建立大小為 5 GB 的佇列時，16 個磁碟分割與 hello 佇列大小上限會變成 (5 \* 16) = 80 GB。 您可以看到 hello 磁碟分割的佇列或主題的大小上限藉由查看其項目上 hello [Azure 入口網站][Azure portal]，在 hello**概觀**刀鋒視窗，該實體。

### <a name="premium"></a>進階

在 Premium 層命名空間中，您可以建立服務匯流排佇列和主題 1、 2、 3、 4、 5、 10、 20、 40、 80 GB 的大小 （hello 預設為 1 GB）。 由於依預設會啟用分割，服務匯流排會為每個實體建立兩個資料分割。 您可以看到 hello 磁碟分割的佇列或主題的大小上限藉由查看其項目上 hello [Azure 入口網站][Azure portal]，在 hello**概觀**刀鋒視窗，該實體。

如需 hello Premium 傳訊層的資料分割的詳細資訊，請參閱[服務匯流排 Premium 和 Standard 傳訊層](service-bus-premium-messaging.md)。 

### <a name="create-a-partitioned-entity"></a>建立分割實體

有數種方式 toocreate 磁碟分割佇列或主題。 當您從應用程式建立 hello 佇列或主題時，您可以啟用依分別設定 hello hello 佇列或主題分割[QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning]或[TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning]屬性太**true**。 這些屬性必須設定在 hello hello 佇列的時間，或建立主題。 如先前所述，它是不可能 toochange 這些屬性上的現有的佇列或主題。 例如：

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

或者，您可以建立磁碟分割的佇列或主題在 hello [Azure 入口網站][ Azure portal]或 Visual Studio 中。 當您在 hello 入口網站中建立的佇列或主題時，hello**啟用資料分割**hello 佇列或主題中的選項**建立**預設會核取刀鋒視窗。 您可以只停用的標準層實體; 中的這個選項在 hello 永遠啟用 Premium 層資料分割。 在 Visual Studio 中，按一下 [hello**啟用分割**核取方塊在 hello**新佇列**或**新主題**] 對話方塊。

## <a name="use-of-partition-keys"></a>分割索引鍵的用途
當訊息列入分割的佇列或主題時，會檢查服務匯流排 hello 存在資料分割索引鍵。 如果找到，就會選取該索引鍵為基礎的 hello 片段。 如果找不到資料分割索引鍵，就會選取內部演算法為基礎的 hello 片段。

### <a name="using-a-partition-key"></a>使用分割區索引鍵
某些情況下，例如工作階段或交易，需要訊息 toobe 儲存在特定的片段中。 所有這些情況下需要 hello 使用資料分割索引鍵。 所有訊息相同的資料分割索引鍵會指派該使用 hello toohello 相同片段。 如果 hello 片段暫時無法使用時，服務匯流排會傳回錯誤。

根據 hello 的案例，不同的訊息屬性會用做資料分割索引鍵：

**SessionId**： 若訊息已 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId]設定屬性，則服務匯流排會使用這個屬性為 hello 資料分割索引鍵。 如此一來，所有的訊息，toohello 屬於相同的工作階段由處理 hello 相同訊息代理程式。 這可讓服務匯流排 tooguarantee 訊息排序以及 hello 的工作階段狀態的一致性。

**PartitionKey**： 若訊息已 hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey]屬性，但不是 hello [BrokeredMessage.SessionId] [BrokeredMessage.SessionId]設定屬性，則服務匯流排也使用 hello [PartitionKey] [ PartitionKey] hello 資料分割索引鍵屬性。 如果 hello 訊息有兩個 hello [SessionId] [ SessionId]和 hello [PartitionKey] [ PartitionKey]屬性集，這兩個屬性必須相同。 如果 hello [PartitionKey] [ PartitionKey]屬性設定為比 hello tooa 不同值[SessionId] [ SessionId]屬性，服務匯流排會傳回不正確作業的例外狀況。 hello [PartitionKey] [ PartitionKey]應該使用屬性，如果傳送端傳送非工作階段感知的交易訊息。 hello 分割金鑰可確保，在交易內傳送的所有訊息都由 hello 相同訊息代理人。

**MessageId**： 如果 hello 佇列或主題有 hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection]屬性設定太**true**和 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId]或[BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey]屬性未設定，則 hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId]屬性做為 hello 資料分割索引鍵。 （請注意，hello Microsoft.NET 和 AMQP 程式庫自動指派訊息識別碼 hello 傳送應用程式並不會）。在此情況下，所有副本都由相同訊息的都 hello 都 hello 相同訊息代理程式。 這可讓服務匯流排 toodetect，並排除重覆的訊息。 如果 hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection]屬性未設定太**true**，Service Bus 不會考慮 hello [MessageId][ MessageId]做為資料分割索引鍵的屬性。

### <a name="not-using-a-partition-key"></a>不使用分割索引鍵
Hello 沒有資料分割索引鍵，在服務匯流排將發佈中的 hello 分割的佇列或主題的循環配置資源方式 tooall hello 片段的訊息。 如果選擇的 hello 片段無法使用，服務匯流排指派 hello 訊息 tooa 不同的片段。 如此一來，hello 訊息存放區暫時無法使用儘管成功 hello 傳送作業。 不過，您不會封存 hello 保證順序，會提供資料分割索引鍵。

Hello 可用性 （沒有資料分割索引鍵） 與一致性 （使用資料分割索引鍵） 之間的權衡取捨的更深入討論，請參閱[本文](../event-hubs/event-hubs-availability-and-consistency.md)。 這項資訊同樣適用於 toopartitioned 服務匯流排實體和事件中心資料分割。

toogive 服務匯流排足夠時間 tooenqueue hello 訊息至不同的片段，hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] hello 用戶端傳送 hello 訊息所指定的值必須大於 15 秒。 我們建議您設定 hello [OperationTimeout] [ OperationTimeout]屬性 toohello 預設值為 60 秒。

請注意，資料分割索引鍵"pin"訊息 tooa 特定片段。 如果保留此片段的 hello 訊息存放區無法使用時，服務匯流排會傳回錯誤。 在資料分割索引鍵 hello 不存在，服務匯流排可以選擇不同的片段，hello 作業成功。 因此，建議您若非必要請勿提供分割索引鍵。

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>進階主題：搭配交易使用分割的實體
傳送做為交易一部分的訊息必須指定資料分割索引鍵。 這可以是其中一個 hello 下列屬性： [BrokeredMessage.SessionId][BrokeredMessage.SessionId]， [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey]，或[BrokeredMessage.MessageId][BrokeredMessage.MessageId]。 Hello 必須指定相同的交易中傳送的所有訊息都 hello 相同的資料分割索引鍵。 如果您嘗試 toosend 訊息，但在交易內的資料分割索引鍵，服務匯流排傳回無效的作業例外狀況。 如果您嘗試的 toosend 內的多個訊息 hello 相同的交易具有不同的資料分割索引鍵，服務匯流排傳回無效的作業例外狀況。 例如：

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

如果設定了任何 hello 屬性做為資料分割索引鍵，服務匯流排 pin hello 訊息 tooa 特定片段。 無論是否使用交易，都會發生這個行為。 建議您若非必要請勿指定分割索引鍵。

## <a name="using-sessions-with-partitioned-entities"></a>搭配工作階段使用分割的實體
hello 訊息 toosend 異動式訊息 tooa 工作階段感知主題或佇列，必須有 hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId]屬性集。 如果 hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey]也指定屬性，它必須是相同的 toohello [SessionId] [ SessionId]屬性。 如果兩者不同，服務匯流排會傳回無效作業例外狀況。

不同於一般 （非資料分割） 的佇列或主題，它不可能 toouse 單一交易 toosend 多個訊息 toodifferent 工作階段。 如果嘗試這樣做，服務匯流排會傳回無效作業例外狀況。 例如：

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>使用分割實體的自動訊息轉送
服務匯流排支援往返於分割實體或在它們之間自動轉送訊息。 tooenable 自動訊息轉送、 設定 hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] hello 來源佇列或訂閱的屬性。 如果 hello 訊息指定資料分割索引鍵 ([SessionId][SessionId]， [PartitionKey][PartitionKey]，或[MessageId] [ MessageId])，該資料分割索引鍵用於 hello 目的地實體。

## <a name="considerations-and-guidelines"></a>考量和指導方針
* **高一致性功能**： 如果實體使用的功能，例如工作階段、 重複偵測或明確控制資料分割索引鍵，則 hello 訊息作業永遠是路由的 toospecific 片段。 如果任何 hello 片段遇到高流量或 hello 基礎存放區的狀況不良，這些作業失敗，且可用性會減少。 整體來說，hello 一致性高於仍然很多非資料分割的實體。相對於的 tooall hello 流量為發生問題，流量的子集合。 如需詳細資訊，請參閱這篇[針對可用性和一致性的討論](../event-hubs/event-hubs-availability-and-consistency.md)。
* **管理**： 必須 hello 實體的所有 hello 片段上執行作業，例如 Create、 Update 和 Delete。 如果任何片段的狀況不良，可能會造成這些作業失敗。 Hello Get 作業，例如訊息計數必須彙總資訊來自所有片段。 如果任何片段會處於狀況不良，則會將 hello 實體可用性狀態報告為有限。
* **低的大量訊息案例，**： 對於這類情況，尤其是使用 hello HTTP 通訊協定，您可能必須 tooperform 多個接收作業順序 tooobtain 中所有的 hello 訊息。 接收要求，hello 前端會接收對所有 hello 片段，並快取所有收到的 hello 回應。 在相同的連接會從這個快取中獲益並收到延遲的 hello 後續接收要求會比較低。 不過，如果您有多個連線或使用 HTTP，則會針對每個要求建立新的連接。 在這種情況，則它會登陸 hello 無法確保相同的節點。 如果所有現有的訊息會鎖定，快取中另一個前端 hello 接收作業會傳回**null**。 訊息最後會到期，您可以再次接收它們。 建議使用 HTTP 持續作用。
* **瀏覽窺視訊息**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_)不一定會傳回所指定的 hello 訊息的 hello 數目[MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount)屬性。 這有兩個常見的原因。 其中一個原因是該 hello hello 訊息的集合彙總的大小超過 hello 256 KB 的大小上限。 另一個原因是如果 hello 佇列或主題有 hello [EnablePartitioning 屬性](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning)設定得**true**，資料分割可能沒有足夠的訊息 toocomplete hello 要求的訊息數目。 一般情況下，如果應用程式想 tooreceive 特定數目的訊息，它應該呼叫[PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_)重複直到到達該數目的訊息，或有沒有更多的訊息 toopeek。 如需詳細資訊，包括程式碼範例，請參閱 [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) 或 [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_)。

## <a name="latest-added-features"></a>最新加入的功能
* 分割實體現在支援新增或移除規則。 不同於非分割實體，交易情況下不支援這些作業。 
* AMQP 現在支援傳送和接收訊息 tooand 從資料分割的實體。
* AMQP 現在支援下列作業的 hello:[批次傳送](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__)，[批次接收](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_)，[接收由序號](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_)，[查看](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek)， [更新鎖定](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_)，[排程訊息](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_)，[取消已排程的訊息](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_)，[新增規則](/dotnet/api/microsoft.servicebus.messaging.ruledescription)，[移除規則](/dotnet/api/microsoft.servicebus.messaging.ruledescription)，[工作階段更新鎖定](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock)，[設定工作階段狀態](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_)，[取得工作階段狀態](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState)，和[列舉工作階段](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync)。

## <a name="partitioned-entities-limitations"></a>分割實體限制
目前服務匯流排會加諸下列限制分割的佇列和主題的 hello:

* 資料分割的佇列和主題不支援所傳送的訊息屬於 toodifferent 在單一交易中的工作階段。
* 服務匯流排目前允許 too100 分割佇列或主題，每個命名空間。 每個磁碟分割的佇列或主題會計入 hello 配額的 10,000 個實體，每個命名空間 （不適用 tooPremium 層）。

## <a name="next-steps"></a>後續步驟
請參閱 hello 討論[服務匯流排 AMQP 1.0 支援分割佇列和主題][ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn 更多關於資料分割訊息實體。 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
