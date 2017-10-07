---
title: "服務匯流排 aaaAzure 配對命名空間 |Microsoft 文件"
description: "配對的命名空間實作詳細資料和成本"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>配對命名空間實作詳細資料和成本影響
hello [PairNamespaceAsync] [ PairNamespaceAsync]方法，使用[SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions]執行個體，請執行可見的工作您的身分。 因為有成本考量使用 hello 功能時，所以這些工作，讓您在發生時加以預期 hello 行為的有用 toounderstand。 hello API 會代替您遵循自動行為 hello:

* 建立待處理項目佇列。
* 建立[MessageSender] [ MessageSender]交談 tooqueues 或主題的物件。
* 當訊息實體變得無法使用時，會傳送 ping 訊息 toohello 實體中嘗試 toodetect 時該實體再度恢復使用。
* 選擇性地建立一組 「 訊息幫浦 」 移動訊息從 hello 待處理項目佇列 toohello 主要佇列。
* 協調關閉/錯誤的主要和次要的 hello [MessagingFactory] [ MessagingFactory]執行個體。

在高層級，hello 功能的運作方式如下： hello 主要實體狀況良好時，就會發生任何行為變更。 當 hello [FailoverInterval] [ FailoverInterval]期間結束，並可 hello 主要實體看見任何成功傳送之後非暫時性[MessagingException] [MessagingException]或[TimeoutException][TimeoutException]，就會發生下列行為的 hello:

1. 傳送作業 toohello 主要實體會停用，直到可以順利傳遞 ping 為止，hello 系統 ping hello 主要實體。
2. 已選取隨機待處理項目佇列。
3. [BrokeredMessage] [ BrokeredMessage]物件是路由的 toohello 選擇待處理項目佇列。
4. 如果選擇待處理項目佇列傳送作業 toohello 失敗，該佇列提取從 hello 循環，並選取新的佇列。 所有的寄件者在 hello [MessagingFactory] [ MessagingFactory] hello 失敗的了解的執行個體。

下列數據的 hello 會描述 hello 順序。 首先，hello 寄件者會傳送訊息。

![配對的命名空間][0]

在失敗 toosend toohello 主要佇列，hello 寄件者會開始傳送訊息 tooa 隨機選擇的待處理項目佇列。 同時，它會開始進行 ping 工作。

![配對的命名空間][1]

此時 hello 訊息仍然在 hello 次要佇列，而尚未傳遞 toohello 主要佇列。 Hello 主要佇列恢復狀況良好後, 至少其中一個處理序應執行虹吸 hello。 hello 虹吸 hello 訊息從傳送所有 hello 各種待處理項目佇列 toohello 適當的目的地實體 （佇列和主題）。

![配對的命名空間][2]

本主題的 hello 其餘部分將討論 hello 的這些作業的運作方式的特定詳細資料。

## <a name="creation-of-backlog-queues"></a>建立待處理項目佇列
hello [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions]傳遞 toohello 物件[PairNamespaceAsync] [ PairNamespaceAsync]方法表示 hello待處理項目數目排入佇列，您想 toouse。 每個待處理項目佇列然後建立以 hello 下列屬性明確設定 (所有其他值都會設 toohello [QueueDescription] [ QueueDescription]預設值):

| Path | [primary namespace]/x-servicebus-transfer/[index]，其中 [index] 是 [0, BacklogQueueCount) 中的值 |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 分鐘 |
| EnableDeadLetteringOnMessageExpiration |true |
| EnableBatchedOperations |true |

例如，命名空間建立 hello 第一次的待處理項目佇列**contoso**名為`contoso/x-servicebus-transfer/0`。

當建立 hello 佇列，hello 程式碼會先檢查 toosee 如果存在這類的佇列。 如果 hello 佇列不存在，則會建立 hello 佇列。 hello 程式碼並不會清除 「 額外的 」 待處理項目佇列。 具體來說，如果 hello 應用程式與 hello 主要命名空間**contoso**要求五個待處理項目佇列但 hello 路徑的待處理項目佇列`contoso/x-servicebus-transfer/7`存在，仍會出現額外的積存佇列，而不是。 hello 系統會明確地允許多餘的待處理項目佇列 tooexist，不會使用。 Hello 命名空間擁有者，會負責清除任何未使用/不需要待處理項目佇列。 這項決策的 hello 原因是服務匯流排無法知道您的命名空間中的所有 hello 佇列都存在目的為何。 此外，如果佇列存在 hello 給定名稱，但不符合 hello 假設[QueueDescription][QueueDescription]，則原因取決於您自己的變更 hello 預設行為。 不保證修改 toohello 待處理項目佇列的程式碼。 徹底請確定 tootest 您的變更。

## <a name="custom-messagesender"></a>自訂 MessageSender
傳送時，所有訊息都會都移到內部[MessageSender] [ MessageSender]正常運作時的所有項目運作，以及當項目 」 中斷。 」，將重新導向 toohello 待處理項目佇列的物件 收到非暫時性失敗時，會啟動計時器。 之後[TimeSpan] [ TimeSpan]期間組成 hello [FailoverInterval] [ FailoverInterval]期間沒有成功的訊息傳送的屬性值可供 hello 容錯移轉。 此時，hello 會發生下列狀況的每個實體：

* Ping 工作會執行每個[PingPrimaryInterval] [ PingPrimaryInterval] toocheck hello 實體是否可用。 這項工作中成功後，立即使用 hello 實體的所有用戶端程式碼會開始傳送新訊息 toohello 主要命名空間。
* 未來的要求 toosend toothat 相同的實體，從任何其他傳送者將會導致 hello [BrokeredMessage] [ BrokeredMessage]傳送 toobe 修改 toosit hello 待處理項目佇列中的。 hello 修改某些屬性移除 hello [BrokeredMessage] [ BrokeredMessage]物件，並將它們儲存到其他位置。 hello 下列屬性會被清除並加入新的別名，讓服務匯流排和 hello SDK tooprocess 訊息統一之下：

| 舊屬性名稱 | 新屬性名稱 |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

hello 原始目的地路徑也儲存在 hello 訊息做為 x ms 路徑的屬性。 此設計可讓單一待處理項目佇列中的許多實體 toocoexist 的訊息。 hello 屬性會傳回由 hello 虹吸轉譯。

自訂 hello [MessageSender] [ MessageSender]物件可能會發生問題，當訊息達到 hello 256 KB 的限制，並可供容錯移轉。 自訂 hello [MessageSender] [ MessageSender]物件會儲存所有佇列和主題一起 hello 待處理項目佇列中的訊息。 此物件會將來自許多混雜在 hello 待處理項目佇列的訊息。 toohandle 之間的負載平衡隨機不知道每個其他 hello SDK 的許多用戶端會針對每個挑選一個待處理項目佇列[QueueClient] [ QueueClient]或[TopicClient] [TopicClient]您在程式碼中建立。

## <a name="pings"></a>Ping
Ping 訊息是空白[BrokeredMessage] [ BrokeredMessage]具有其[ContentType] [ ContentType]屬性設定 tooapplication/vnd.ms servicebus-ping和[TimeToLive] [ TimeToLive]值為 1 秒。 此 ping 在 Service Bus 中有一個特性： hello 伺服器永遠不會傳遞 ping 要求的任何呼叫端時[BrokeredMessage][BrokeredMessage]。 因此，您不再需要 toolearn 如何 tooreceive 並忽略這些訊息。 每個實體 （唯一佇列或主題），每個[MessagingFactory] [ MessagingFactory]視為 toobe 無法使用時，將會被 ping 每個用戶端的執行個體。 根據預設，這會每分鐘發生一次。 Ping 訊息會被視為 toobe 一般服務匯流排訊息，而且可能會導致頻寬和訊息的費用。 Hello 用戶端會偵測 hello 系統是可用，如 hello 訊息，會停止。

## <a name="hello-syphon"></a>hello 虹吸
Hello 應用程式中的至少一個可執行程式應主動執行虹吸 hello。 hello 虹吸會執行長時間輪詢接收達 15 分鐘。 當所有實體都都可用，您有 10 個待處理項目佇列 hello 裝載 hello 虹吸呼叫 hello 接收作業 40 次每小時、 每天 960 次，並在 30 天內達到 28800 次應用程式。 當 hello 虹吸主動從 hello 待處理項目 toohello 主要佇列移動訊息時，每個訊息就會發生下列的費用 （訊息大小和頻寬的標準收費適用於所有階段） 的 hello:

1. 傳送 toohello 待處理項目。
2. 收到 hello 待處理項目。
3. 傳送主要 toohello。
4. 接收來自主要 hello。

## <a name="closefault-behavior"></a>關閉/錯誤行為
裝載 hello 虹吸、 一次 hello 主要或次要資料庫的應用程式內[MessagingFactory] [ MessagingFactory]發生錯誤或已關閉而不需要其夥伴也正在發生錯誤/關閉和 hello 虹吸偵測到此狀態hello 虹吸作用。 如果其他 hello [MessagingFactory] [ MessagingFactory]未關閉 hello 虹吸將會在 5 秒內，錯誤 hello 仍開啟[MessagingFactory] [ MessagingFactory].

## <a name="next-steps"></a>後續步驟
如需服務匯流排非同步通訊的詳細討論，請參閱[非同步通訊模式和高可用性][Asynchronous messaging patterns and high availability]。 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
