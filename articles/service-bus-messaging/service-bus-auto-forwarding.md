---
title: "aaaAuto 轉送 Azure Service Bus 訊息實體 |Microsoft 文件"
description: "如何 toochain 服務匯流排佇列或訂閱 tooanother 佇列或主題。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>使用自動轉寄鏈結服務匯流排實體

服務匯流排 hello*自動轉送*功能可讓您 toochain 佇列或訂閱 tooanother 佇列或主題 hello 屬於相同的命名空間。 啟用自動轉送時，服務匯流排自動移除 hello 第一個佇列或訂閱 （來源） 中放置的訊息，並將它們置於 hello 第二個佇列或主題 （目的地）。 請注意，它仍可能 toosend 訊息 toohello 目的地實體直接。 此外，它不可能 toochain 子佇列，例如無效信件佇列、 tooanother 佇列或主題。

## <a name="using-auto-forwarding"></a>使用自動轉寄
您可以啟用自動轉送設定 hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo]或[SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo]屬性上 hello [QueueDescription] [ QueueDescription]或[SubscriptionDescription] [ SubscriptionDescription] hello 來源，例如 hello 的物件下列範例。

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

hello 目的地實體必須存在於建立 hello 來源實體的 hello 階段。 如果 hello 目的地實體不存在，服務匯流排集的 toocreate hello 來源實體時，就會傳回例外狀況。

您可以使用自動轉送 tooscale 個別的主題。 服務匯流排限制 hello[的特定主題的訂用帳戶數目](service-bus-quotas.md)too2，000。 您可以藉由建立第二層主題來容納其他訂用帳戶。 請注意，即使您未繫結的 hello 服務匯流排訂用帳戶，加入第二層主題的 hello 數目限制可以改善 hello 主題的整體輸送量。

![自動轉寄案例][0]

您也可以使用自動轉送 toodecouple 訊息傳送者和接收者。 例如，請考慮包含三個模組的 ERP 系統︰訂單處理、庫存管理及客戶關係管理。 上述每一個模組會產生加入對應主題中的訊息。 Alice 和 Bob 是銷售人員感興趣 tootheir 客戶與相關聯的所有訊息。 tooreceive 這些訊息，Alice 和 Bob 都建立個人佇列和訂閱 hello 自動轉寄所有郵件 tootheir 佇列的 ERP 主題的每個上。

![自動轉寄案例][1]

如果 Alice 渡假，她個人佇列，而不是 hello ERP 主題，則會填滿。 在此案例中，銷售代表未收到任何訊息，因為無 hello ERP 主題不會達到配額。

## <a name="auto-forwarding-considerations"></a>自動轉寄考量

如果 hello 目的地實體太多的訊息會累積及超過 hello 配額或 hello 目的地實體已停用，hello 來源實體會加入 hello 訊息 tooits[寄不出的信件佇列](service-bus-dead-letter-queues.md)直到 hello 目的地中的空間（或 hello 實體已重新啟用）。 這些訊息會繼續 toolive hello 寄不出信件佇列中，因此您必須明確地接收與處理 hello 寄不出的信件佇列。

當鏈結在一起個別主題 tooobtain 具有多個訂閱的複合主題，建議您有少量的 hello 第一層主題訂閱和許多 hello 第二層主題訂閱。 例如，第一層主題包含 20 個訂閱中的，每個鏈結 tooa 第二層主題包含 200 個訂閱，允許更高的輸送量比第一層主題包含 200 個訂閱，每個鏈結 tooa 第二層主題包含 20 個訂閱.

服務匯流排會針對每一則轉寄的訊息向一個作業計費。 例如，每個傳送訊息 tooa 主題包含 20 個訂閱，設定 tooauto 轉寄訊息 tooanother 佇列或主題，以計費 21 次作業如果第一層的所有訂閱都收到 hello 訊息的複本。

hello hello 訂用帳戶的建立者必須具有 toocreate 鏈結的 tooanother 佇列或主題的訂用帳戶，**管理**hello 來源和 hello 目的地實體的權限。 傳送訊息 toohello 來源主題只需要**傳送**hello 來源主題上的權限。

## <a name="next-steps"></a>後續步驟

如需自動轉送的詳細資訊，請參閱下列參考主題的 hello:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn 進一步了解服務匯流排效能增強功能，請參閱 

* [使用服務匯流排傳訊的效能改進最佳作法](service-bus-performance-improvements.md)
* [分割的傳訊實體][Partitioned messaging entities]。

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
