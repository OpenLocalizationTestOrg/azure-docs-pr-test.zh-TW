---
title: "aaaService 匯流排寄不出信件佇列 |Microsoft 文件"
description: "Azure 服務匯流排寄不出的信件佇列的概觀"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>服務匯流排寄不出的信件佇列的概觀

服務匯流排佇列和主題訂用帳戶提供次要的子佇列，稱為*無效信件佇列* (DLQ)。 hello 寄不出的信件佇列不需要明確建立 toobe，而且不能刪除或其他 managed 的無關的 hello 主要實體。

本文討論 Azure 服務匯流排中的無效信件佇列。 大部分的 hello 討論說明 hello[寄不出的信件佇列範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue)GitHub 上。
 
## <a name="hello-dead-letter-queue"></a>hello 寄不出的信件佇列

hello 的目的 hello 寄不出的信件佇列是 toohold 訊息無法傳遞 tooany 收件者或無法處理的訊息。 可以從 hello DLQ 移除訊息，然後檢查。 應用程式可能會與運算子的說明，請更正問題並再重新送出 hello 訊息、 記錄時發生錯誤，hello 事實和採取更正動作。 

從應用程式開發介面和通訊協定的觀點而言，hello DLQ 是大部分類似 tooany 其他佇列中，不同之處在於只能透過 hello 寄不出信件筆勢 hello 父實體的提交訊息。 此外，存留時間並未遵守，而且您無法從 DLQ 讓訊息寄不出去。 hello 寄不出的信件佇列完全支援查看並鎖定傳遞和交易式作業。

請注意，不會自動清除的 hello DLQ。 訊息保留在 hello DLQ，直到您明確地從 hello DLQ 和呼叫擷取[complete （)](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) hello 寄不出的信件訊息上。

## <a name="moving-messages-toohello-dlq"></a>移動訊息 toohello DLQ

沒有服務匯流排中數個會造成訊息 tooget 推入 toohello 從 DLQ hello 傳訊引擎本身內的活動。 應用程式可以同時明確地移動訊息 toohello DLQ。 

因為 hello broker 會呼叫其內部版的 hello hello broker 取得移動 hello 訊息，當兩個屬性就會加入 toohello 訊息[DeadLetter](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) hello 訊息上的方法：`DeadLetterReason`和`DeadLetterErrorDescription`。

應用程式可以定義自己的程式碼的 hello`DeadLetterReason`屬性，但是 hello 系統集 hello 下列值。

| 條件 | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| 一律 |HeaderSizeExceeded |已經超過這個資料流的 hello 大小配額。 |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing 和 SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |hello 訊息過期，而且已無作用信件。 |
| SubscriptionDescription.RequiresSession |工作階段識別碼為 null。 |啟用工作階段的實體不允許工作階段識別項為 null 的訊息。 |
| ！寄不出的信件佇列 |MaxTransferHopCountExceeded |Null |
| 應用程式明確停止傳送 |應用程式所指定 |應用程式所指定 |

## <a name="exceeding-maxdeliverycount"></a>超過 MaxDeliveryCount
佇列與訂用帳戶各有[QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount)和[SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount)屬性分別; hello 預設值為 10。 每當在鎖定下傳遞的訊息 ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode))，但是已經是明確放棄或 hello 鎖定已過期，hello 訊息[BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount)是遞增。 當[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount)超過[MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount)，hello 訊息是移動的 toohello DLQ，指定 hello`MaxDeliveryCountExceeded`原因碼。

無法停用此行為，但是您可以設定[MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa 數量非常龐大。

## <a name="exceeding-timetolive"></a>超過 TimeToLive
當 hello [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration)或[SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration)屬性設定太**true**(hello 預設值是**false**)，所有的過期訊息會移動的 toohello DLQ，指定 hello`TTLExpiredException`原因碼。

請注意，過期的訊息只會被清除，而且至少一個作用中的接收者 hello 主要佇列或訂閱; 提取時，因此移動 toohello DLQ該行為是預設行為。

## <a name="errors-while-processing-subscription-rules"></a>在處理訂用帳戶規則時發生錯誤
當 hello [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions)屬性已啟用訂用帳戶、 訂用帳戶的 SQL 篩選規則執行時所發生的任何錯誤所擷取的 hello DLQ以及 hello 違規的訊息。

## <a name="application-level-dead-lettering"></a>應用程式層級無效信件處理
在加法 toohello 系統提供信件功能，應用程式可以使用 hello DLQ tooexplicitly 拒絕無法接受訊息。 這可能包括無法正確處理系統問題、 保存格式不正確的裝載的訊息或訊息的驗證失敗時則會使用某些訊息層級安全性配置 tooany 排序到期的訊息。

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>ForwardTo 或 SendVia 案例中寄不出的信件處理

訊息會傳送的 toohello 傳送寄不出信件佇列 hello 下列條件下：

- 訊息會通過 3 個以上[鏈結在一起](service-bus-auto-forwarding.md)的佇列或主題。
- hello 目的地佇列或主題已停用或刪除。
- hello 目的地佇列或主題超過 hello 最大實體大小。

tooretrieve 這些信件訊息中，您可以建立使用 hello 接收者[FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_)公用程式方法。

## <a name="example"></a>範例
下列程式碼片段的 hello 建立訊息接收者。 在 hello 收到 hello 主要佇列的迴圈、 hello 程式碼會擷取與 hello 訊息[Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_)，詢問 hello broker tooinstantly 傳回任何訊息取用，或沒有結果 tooreturn。 如果 hello 程式碼會收到訊息時，它立即放棄，即可遞增 hello `DeliveryCount`。 一旦 hello 系統移 hello 訊息 toohello DLQ，hello 主要佇列是空的做為 hello 迴圈結束[ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_)傳回**null**。

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>後續步驟
請參閱下列文章中的服務匯流排佇列的詳細資訊的 hello:

* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [比較 Azure 佇列和服務匯流排佇列](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

