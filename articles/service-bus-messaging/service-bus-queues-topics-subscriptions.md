---
title: "Azure Service Bus 訊息佇列、 主題和訂用帳戶的 aaaOverview |Microsoft 文件"
description: "服務匯流排訊息實體的概觀。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>服務匯流排佇列、主題和訂用帳戶

Microsoft Azure 服務匯流排支援一組以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。 這些 「 代理 」 訊息功能可以被視為低耦合訊息支援發行-訂閱的功能、 時態解除結合及負載平衡案例使用 hello 服務匯流排傳訊網狀架構。 低耦合通訊有許多優點︰例如，用戶端和伺服器可視需要連接並以非同步方式執行其作業。

hello 訊息實體所構成訊息功能，在 Service Bus 中的 hello 核心是 hello 的佇列、 主題和訂閱和規則/動作。

## <a name="queues"></a>佇列

佇列提供*先進先出*(FIFO) 訊息傳遞 tooone 或更多的競爭取用者。 也就是說，訊息是通常預期的 toobe 接收和處理由 hello 接收者 hello 順序，在其中加入 toohello 佇列，以及每個訊息是接收並處理一個訊息取用者。 使用佇列的主要優點是 tooachieve 「 時間解除結合 」 的應用程式元件。 換句話說，hello 產生者 （傳送者） 和消費者 （接收者） 不需要 toobe 傳送和接收訊息在 hello 相同的時間，因為訊息長期儲存 hello 佇列中。 此外，hello 生產者沒有 toowait hello 消費者的回覆順序 toocontinue tooprocess 中，以及傳送訊息。

相關的優點是 「 負載調節 」 這可讓產生者和消費者 toosend 和接收訊息至不同的費率。 在許多應用程式，hello 系統負載會隨著時間;不過，所需每個工作單位的 hello 處理時間通常不變。 調解訊息產生者和消費者與佇列表示耗用僅應用程式的 hello toobe 佈建的 toobe 無法 toohandle 平均負載而非尖峰負載。 hello 深度 hello 佇列成長，且合約會隨著 hello 連入負載而改變。 這與基礎結構需要的 tooservice hello 應用程式負載而考慮 toohello 數量可直接節省金錢。 為 hello 負載增加，多個背景工作處理序可以是加入的 tooread hello 佇列中。 只有其中一個 hello 背景工作處理序處理每個訊息。 此外，此提取為基礎的負載平衡能充分利用 hello 背景工作電腦即使 hello 背景工作電腦不同而考慮 tooprocessing 電源，因為它們會在他們自己的最大速率提取訊息。 此模式通常稱為 hello 「 競爭消費者 」 模式。

使用訊息產生者與取用者之間的佇列 toointermediate 提供 hello 元件之間的固有鬆散結合。 因為產生者和消費者不知道彼此的存在，取用者可以在 hello 生產者影響的情況下升級。

建立佇列是一個多步驟的程序。 執行管理作業，如 Service Bus 訊息實體 （佇列和主題） 透過 hello [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)類別，建構藉由提供基底位址 hello Service Bus hello命名空間和 hello 使用者認證。 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)提供方法 toocreate 列舉和刪除訊息實體。 在建立之後[Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) hello SAS 名稱和金鑰，以及服務命名空間管理來自物件的物件，您可以使用 hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_)方法 toocreate hello 佇列。 例如：

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

然後您可以建立佇列物件和訊息 factory 以 hello 服務匯流排 URI 做為引數。 例如：

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

然後，您可以傳送郵件 toohello 佇列。 例如，如果您有呼叫代理訊息清單`MessageList`，hello 程式碼會顯示類似 toohello 下列：

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

您再從佇列接收訊息 hello，如下所示：

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

在 hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式，hello 接收作業是單發式的也就是服務匯流排收到 hello 要求時，它會標示為正在使用的 hello 訊息，並傳回它 toohello 應用程式。 **ReceiveAndDelete**模式是 hello 簡單的模式，最適合用於中的 hello 應用程式可以容許不處理中失敗的 hello 事件訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 因為服務匯流排會標示為正在使用，當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，將會遺失已的 hello 訊息取用先前 toohello 損毀。

在[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式，hello 接收作業變成兩階段，讓它不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到 hello 要求時，它找到 hello 耗用下一個訊息 toobe、 tooprevent 將它鎖定，接收其他取用者，然後傳回 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)上收到 hello 訊息。 當服務匯流排會看見 hello**完成**呼叫時，它會將標示為正在使用的 hello 訊息。

如果 hello 應用程式無法 tooprocess hello 訊息，因為某些原因，它可以呼叫 hello[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)收到 hello 訊息上的方法 (而不是[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete))。 這可讓服務匯流排 toounlock hello 訊息，並讓它再次接收可用 toobe、 由 hello 相同的消費者或其他競爭消費者。 其次，那里已逾時與鎖定相關聯 hello 和 hello 應用程式如果無法 tooprocess hello 訊息 hello 鎖定逾時到期前 （例如，如果 hello 應用程式當機），則服務匯流排解除鎖定 hello 訊息，並使其可用 toobe接收一次 (基本上執行[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)作業依預設)。

請注意，在 hello hello 應用程式的事件發生當機之後處理 hello 訊息，但之前 hello**完成**發出要求，hello 訊息已重新傳遞的 toohello 應用程式重新啟動時。 這通常稱為「至少一次」處理機制；也就是說，會至少將每個訊息都處理一次。 不過，在某些情況下 hello 可能傳遞相同的訊息。 如果 hello 案例無法容許重複處理，則需要額外的邏輯在 hello 應用程式 toodetect 重複項目可以根據 hello 達成**MessageId** hello 訊息，會保留屬性所有傳遞嘗試的常數。 這就是所謂的「剛好一次」處理。

## <a name="topics-and-subscriptions"></a>主題和訂用帳戶
在對比 tooqueues，在每個訊息處理由單一消費者，*主題*和*訂閱*-一對多通訊的形式，提供在*發佈/訂閱*模式。 適用於調整 toovery 收件者數目很大，每個已發行的訊息是由可用 tooeach 註冊 hello 主題的訂用帳戶。 Tooa 主題和傳遞的 tooone 或更多相關聯的訂閱，根據您可以將每個訂用帳戶為基礎的篩選規則，會傳送訊息。 hello 訂閱可以使用其他篩選 toorestrict hello 訊息，他們想 tooreceive。 訊息會傳送 tooa 主題在 hello 相同方式會傳送它們 tooa 佇列，但會在收到訊息從 hello 主題直接。 反而會從訂用帳戶接收。 主題訂閱類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。 訊息會從訂閱接收相同 toohello 方法已從佇列接收。

透過比較，hello 訊息傳送功能佇列對應直接 tooa 主題，而其訊息接收功能對應 tooa 訂用帳戶。 除此之外，這表示訂閱支援的 hello 與考慮 tooqueues 本章節稍早描述相同的模式： 競爭消費者、 時間解除結合、 負載調節和負載平衡。

建立主題為類似 toocreating 佇列，hello 前一節中的 hello 範例所示。 建立 hello 服務 URI，然後再使用 hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)類別 toocreate hello 命名空間的用戶端。 然後，您可以建立主題，使用 hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_)方法。 例如：

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

接下來，新增所需的訂用帳戶︰

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

您可以接著建立主題用戶端。 例如：

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

使用 hello 訊息寄件者，您可以傳送和訊息 tooand 收到 hello 主題 hello 上一節中所示。 例如：

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

類似 tooqueues，訊息來自訂用帳戶使用[SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient)物件而非[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)物件。 建立 hello 訂閱用戶端，傳送 hello hello 主題，hello hello 訂用帳戶名稱，名稱和 （選擇性） hello 接收模式做為參數。 例如，以 hello**清查**訂用帳戶：

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>執行和動作
在許多情況下，必須以不同的方式處理具有特定特性的訊息。 tooenable，您可以設定訂閱 toofind 訊息，具有所需的屬性，然後再執行特定修改 toothose 屬性。 服務匯流排訂閱可看見所有傳送 toohello 主題的訊息，而您僅能複製這些訊息 toohello 虛擬訂閱佇列的子集。 使用訂用帳戶篩選器即可達成。 這類修改稱之為「篩選器動作」。 建立訂用帳戶時，您可以提供 hello hello 訊息屬性運作的篩選運算式，兩者 hello 系統屬性 (例如，**標籤**) 和自訂應用程式屬性 (例如， **StoreName**。) hello SQL 篩選運算式是選擇性的在此情況下。SQL 篩選運算式，沒有任何訂用帳戶上所定義的篩選器動作將會執行所有的 hello 訊息，該訂用帳戶。

使用 hello 上述範例中，只有來自 toofilter 訊息**Store1**，您會建立 hello 儀表板訂用帳戶，如下所示：

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

只有具有 hello 訊息的位置，此訂閱篩選`StoreName`屬性設定太`Store1`會複製的 toohello 虛擬佇列 hello`Dashboard`訂用帳戶。

如需可能的篩選值的詳細資訊，請參閱 hello 文件以 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)和[SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)類別。 此外，請參閱 hello[代理訊息： 進階篩選器](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)和[主題篩選](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters)範例。

## <a name="next-steps"></a>後續步驟
Hello 下列進階主題，如需詳細資訊和使用服務匯流排傳訊的範例，請參閱。

* [服務匯流排訊息概觀](service-bus-messaging-overview.md)
* [服務匯流排代理傳訊 .NET 教學課程](service-bus-brokered-tutorial-dotnet.md)
* [服務匯流排代理傳訊 REST 教學課程](service-bus-brokered-tutorial-rest.md)
* [主題篩選器範例](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [代理傳訊︰進階篩選器範例](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

