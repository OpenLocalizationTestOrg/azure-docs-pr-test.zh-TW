---
title: "Azure 服務匯流排訊息工作階段 | Microsoft Docs"
description: "使用工作階段處理 Azure 服務匯流排訊息的序列。"
services: service-bus-messaging
documentationcenter: 
author: clemensv
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/02/2018
ms.author: sethm
ms.openlocfilehash: 16f641c7b6fdd1d6730d2ae229c93ce4a33b9492
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="message-sessions-first-in-first-out-fifo"></a>訊息工作階段： 第一次先進先出 (FIFO) 

Microsoft Azure 服務匯流排工作階段讓聯合和已排序的未繫結的相關訊息序列的處理。 若要實現 FIFO 保證 Service Bus 中的，使用工作階段。 服務匯流排對於訊息之間關係的本質並無任何規範，而且也不會定義特殊的模型來判斷訊息序列開頭或結尾的位置。

任何寄件者可以建立當提交訊息至佇列或主題藉由設定工作階段[SessionId](/dotnet/api/microsoft.azure.servicebus.message.sessionid#Microsoft_Azure_ServiceBus_Message_SessionId)某些應用程式定義的識別項的唯一工作階段的屬性。 在 AMQP 1.0 通訊協定層級，這個值會對應至「群組識別碼」屬性。

在工作階段感知的佇列或訂用帳戶中，工作階段會在至少有一個訊息具備工作階段的 [SessionId](/dotnet/api/microsoft.azure.servicebus.message.sessionid#Microsoft_Azure_ServiceBus_Message_SessionId) 時變成存在。 一旦工作階段存在之後，就不會有針對工作階段到期或消失時定義的時間或 API。 理論上，今日可接收工作階段的訊息，一年內的下一個訊息，而且如果 **SessionId** 相符，則從服務匯流排的觀點來看，工作階段是一樣。

一般而言，不過，應用程式的其中一組相關的訊息開始和結束清除概念。 服務匯流排未設定任何特定的規則。

如何描述傳輸檔案的序列範例是將第一個訊息的 **Label** 屬性設為 **start**、針對中繼訊息設為 **content**，然後針對最後一個訊息設為 **end**。 計算內容訊息的相對位置與目前訊息*SequenceNumber*從差異**啟動**訊息*SequenceNumber*。

服務匯流排中的工作階段功能會啟用特定的接收作業，在 C# 和 Java API 中的形式為 [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession)。 您可以透過 Azure Resource Manager 來設定佇列或訂用帳戶上的 [requiresSession](/azure/templates/microsoft.servicebus/namespaces/queues#property-values) 屬性，或者在入口網站中設定旗標，藉以啟用此功能。 在您嘗試使用相關的 API 作業之前，必須先執行此動作。

在入口網站中，設定以下的核取方塊的旗標：

![][2]

適用於工作階段的 API 會存在於佇列和訂用帳戶用戶端上。 沒有命令式模型，可控制何時收到工作階段和訊息，並處理常式為基礎的模型，類似於*OnMessage*，會隱藏複雜度管理接收迴圈。

## <a name="session-features"></a>工作階段功能

工作階段提供並行分離的交錯的訊息資料流時保留，並保證排序的傳遞。

![][1]

[MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) 接收者會由接受工作階段的用戶端所建立。 用戶端呼叫[QueueClient.AcceptMessageSession](/dotnet/api/microsoft.servicebus.messaging.queueclient.acceptmessagesession#Microsoft_ServiceBus_Messaging_QueueClient_AcceptMessageSession)或[QueueClient.AcceptMessageSessionAsync](/dotnet/api/microsoft.servicebus.messaging.queueclient.acceptmessagesessionasync#Microsoft_ServiceBus_Messaging_QueueClient_AcceptMessageSessionAsync) C# 中。 在回應式回呼模型中，它會註冊工作階段處理常式，如稍後所討論。

當[MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession)物件會接受並時它由用戶端，該用戶端會保留與該工作階段的所有訊息上的獨佔鎖定[SessionId](/en-us/dotnet/api/microsoft.servicebus.messaging.messagesession.sessionid#Microsoft_ServiceBus_Messaging_MessageSession_SessionId)存在於佇列或訂閱，並也在與所有訊息上**SessionId** ，仍會到達持有工作階段。

釋放鎖定時**關閉**或**CloseAsync**呼叫時，或在應用程式是無法執行關閉作業的情況下則鎖定會逾時。 工作階段鎖定應被視為類似檔案上的獨佔鎖定，這表示只要應用程式不再需要工作階段和 (或) 不預期會有任何後續訊息時，就應儘速關閉該工作階段。

當多個並行接收者從佇列提取時，就會將屬於特殊工作階段的訊息分派給目前保有該工作階段之鎖定的特定接收者。 透過該作業，位於一個佇列或訂用帳戶中的交錯式訊息資料流就會被完全分離信號到不同的接收者，而那些接收者也可以存留於不同的用戶端機器上，因為鎖定管理會發生於服務匯流排內部的服務端。

不過，佇列仍然是佇列：不會有隨機存取。 如果多個並行接收者會等候接受特定的工作階段，或是等候來自特定工作階段的訊息，而且屬於尚未宣告任何接收者之工作階段的佇列頂端有一個訊息，則會保留傳遞，直到工作階段接收者宣告該工作階段為止。

上圖顯示三個並行工作階段接收者，它們全都必須針對每個接收者主動從佇列中獲取訊息以取得進展。 與先前的工作階段`SessionId`= 4 有沒有作用中主控的用戶端，這表示任何訊息會傳送給任何人，直到該訊息已由新的建立，主控工作階段接收者。

儘管那樣似乎會變成限制，但是，單一接收者處理序可以輕鬆地處理許多並行工作階段，特別當它們是以完全非同步的程式碼撰寫的；同時應付數十個並行工作階段，可利用回呼模型有效地自動執行。

用於處理許多並行工作階段的策略 (其中每個工作階段只會偶爾收到訊息) 是針對處理常式，在一段閒置時間之後卸除該工作階段，並且在因下一個工作階段送達而接受工作階段時繼續處理。

工作階段接收者所保留的工作階段鎖定是對於「查看鎖定」安置模式所使用之訊息鎖定的保護傘。 接收者不能同時有兩個「在途中」的訊息，而是必須依序處理訊息。 只有在已完成先前的訊息或使其成為失效信件時才能取得新訊息。 放棄訊息會導致下一個接收作業再次提供相同的訊息。

## <a name="message-session-state"></a>訊息工作階段狀態

在高延展性、高可用性的雲端系統中處理工作流程時，與特定工作階段相關聯的工作流程處理常式必須能夠從非預期的失敗中復原，同時也能在與工作開始之處不同的處理序或機器上，繼續執行部分完成的工作。

工作階段狀態設施會在訊息代理程式內部，為訊息工作階段啟用應用程式定義的註釋，因此，相對於該工作階段所記錄的處理狀態會在新的處理器取得該工作階段時立即變成可用狀態。

從服務匯流排的觀點而言，訊息工作階段狀態是一個不透明的二進位物件，其可保存一個訊息大小的資料，針對服務匯流排標準為 256 KB，針對服務匯流排進階則是 1 MB。 相對於工作階段的處理狀態可以保留在工作階段狀態內部，或者工作階段狀態可以指向某個保留這類資訊的儲存體位置或資料庫記錄。

管理工作階段狀態的 API ([SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) 和 [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)) 可在 C# 和 Java API 中的 [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) 物件上找到。 先前未設定任何工作階段狀態的工作階段會針對 **GetState** 傳回 **null** 參考。 使用 [SetState(null)](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) 來完成清除先前設定的工作階段狀態。

佇列或訂用帳戶中所有現有的工作階段都可使用 Java API 中的 **SessionBrowser** 方法，以及 .NET 用戶端中 [QueueClient](/dotnet/api/microsoft.azure.servicebus.queueclient) 和 [SubscriptionClient](/dotnet/api/microsoft.azure.servicebus.subscriptionclient) 上的 [GetMessageSessions](/dotnet/api/microsoft.servicebus.messaging.queueclient.getmessagesessions#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessions) 來列舉。

保留於佇列或訂用帳戶中的工作階段狀態會計入該實體的儲存體配額。 使用工作階段完成應用程式時，接著會建議應用程式清除其保留狀態以避免產生外部管理成本。

## <a name="next-steps"></a>後續步驟

- 使用 .NET 標準程式庫，從服務匯流排佇列傳送及接收以工作階段為基礎之訊息的[完整範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/GettingStarted/Microsoft.Azure.ServiceBus/BasicSendReceiveUsingQueueClient) \(英文\)。
- 使用 .NET Framework 用戶端來處理工作階段感知訊息的[範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/Sessions) \(英文\)。 

若要深入了解服務匯流排傳訊，請參閱下列主題：

* [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
* [服務匯流排佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)
* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [如何使用服務匯流排主題和訂用帳戶](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[1]: ./media/message-sessions/sessions.png
[2]: ./media/message-sessions/queue-sessions.png