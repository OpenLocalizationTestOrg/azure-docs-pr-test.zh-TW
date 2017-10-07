---
title: "Azure 服務匯流排中處理交易的 aaaOverview |Microsoft 文件"
description: "Azure 服務匯流排不可部分完成交易和傳送方式概觀"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>服務匯流排交易處理概觀
這篇文章討論 Azure 服務匯流排 hello 交易功能。 大部分的 hello 討論說明 hello[不可部分完成交易與服務匯流排範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)。 這篇文章是有限的 tooan 概觀交易處理和 hello*透過傳送*Service bus，hello 不可部分完成交易的範例是在範圍更大且更複雜的功能。

## <a name="transactions-in-service-bus"></a>服務匯流排中的交易
[交易](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions)會將兩個以上的作業一起分組到「執行範圍」。 本質上，屬於 tooa 假設的作業群組的所有作業成功或失敗共同，必須確定在這種交易。 在這一方面交易做為一個單位，通常會參考的 tooas*不可部份完成性*。 

服務匯流排是交易訊息代理人，並確保其訊息存放區之所有內部作業的交易完整性。 所有傳輸的服務匯流排內的訊息，例如移動訊息 tooa[寄不出的信件佇列](service-bus-dead-letter-queues.md)或[自動轉送](service-bus-auto-forwarding.md)個實體之間的訊息，為交易式。 這麼一來，如果服務匯流排接受訊息，表示訊息已經儲存並標上序號。 從那時起，Service Bus 中的任何訊息傳輸會協調的作業，跨實體，而將兩者都不會導致 tooloss （來源成功和失敗的目標） 或 tooduplication （來源成功與失敗目標） 的 hello 訊息。

服務匯流排支援針對單一訊息實體 （佇列、 主題、 訂用帳戶） hello 範圍內的交易的分組作業。 例如，您可以將來自數個訊息 tooone 佇列傳送的交易範圍內，而 hello 訊息才會認可的 toohello 佇列記錄 hello 交易成功完成時。

## <a name="operations-within-a-transaction-scope"></a>交易範圍內的作業
可以在交易範圍內執行的 hello 作業如下所示：

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)、[MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)、[TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**：Send、SendAsync、SendBatch、SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**：Complete、CompleteAsync、Abandon、AbandonAsync、Deadletter、DeadletterAsync、Defer、DeferAsync、RenewLock、RenewLockAsync 

接收作業並不包含在內，因為它會假設 hello 應用程式會取得使用 hello 訊息[ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式中的，在某些接收迴圈或[OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_)回呼，以及只然後開啟交易範圍處理 hello 訊息。

hello hello 訊息 （完成，放棄，寄不出的信件、 延遲） 的配置就會發生在 hello 範圍，以及依存於，hello hello 交易的整體結果。

## <a name="transfers-and-send-via"></a>傳輸和「傳送方式」
tooenable 和資料的佇列 tooa 處理器，然後 tooanother 佇列的交易移，服務匯流排支援*傳輸*。 在傳送作業中，寄件者先傳送訊息 tooa 「 傳送佇列 」 和 hello 傳輸佇列立即移 hello 訊息 toohello 適合使用的 hello 強固相同傳輸實作 hello 自動轉送功能相依的目的地佇列上。 hello 訊息永遠不會認可的 toohello 傳輸佇列的記錄檔，它會變成可見 hello 傳輸佇列的取用者的方式。

hello hello 寄件者的輸入訊息來源 hello 傳輸佇列本身時，此交易式功能的 hello 電源就顯而易見。 換句話說，服務匯流排可以傳送 hello 訊息 toohello 目的地佇列"via"hello 傳輸佇列中，執行完成時 (或延遲，或寄不出信件) 在 hello 輸入訊息中，所有在一個不可部分完成的作業中的作業。 

### <a name="see-it-in-code"></a>透過程式碼查看
tooset 總這類傳輸，您會建立訊息寄件者為目標 hello 透過 hello 傳輸佇列的目的地佇列。 您也要有從相同佇列提取訊息的收件者。 例如：

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

然後簡單交易是使用這些項目，如 hello 下列範例所示：

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>後續步驟

請參閱下列文章中的服務匯流排佇列的詳細資訊的 hello:

* [使用自動轉寄鏈結服務匯流排實體](service-bus-auto-forwarding.md)
* [自動轉寄範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [使用服務匯流排的不可部分完成交易範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [比較 Azure 佇列和服務匯流排佇列](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [如何 toouse 服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)

