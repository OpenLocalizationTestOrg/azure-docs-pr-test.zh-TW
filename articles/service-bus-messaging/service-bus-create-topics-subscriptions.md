---
title: "aaaCreate 應用程式使用 Azure 服務匯流排主題和訂用帳戶 |Microsoft 文件"
description: "簡介 toohello 發行-訂閱所提供服務匯流排主題和訂閱的能力。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>建立使用服務匯流排主題和訂用帳戶的應用程式
Azure 服務匯流排支援一套以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。 這篇文章會根據所提供的 hello 資訊[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)簡單介紹 toohello 發佈/訂閱功能所提供的服務匯流排主題。

## <a name="evolving-retail-scenario"></a>不斷演變的零售案例
本文會繼續使用中的 hello 零售案例[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)。 前文提過，將個別銷售點 (POS) 終端機的銷售資料必須路由的 tooan 庫存管理系統使用該資料 toodetermine toobe 補充存貨。 每個 POS 終端機報告其銷售資料，藉由傳送訊息 toohello **DataCollectionQueue**佇列，其中一直等到收到 hello 庫存管理系統，如下所示：

![服務匯流排 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

此案例中，新的需求已的 tooevolve 加入 toohello 系統： hello 店主想 toobe 無法 toomonitor hello 存放區執行即時的方式。

tooaddress 這項需求，hello 系統必須 「 竊聽 」 hello 銷售資料流。 我們仍然希望傳送嗨 POS 終端機 toobe 傳送 toohello 庫存管理系統做為前，每個訊息，但我們想要每則訊息，我們可以使用 toopresent hello 儀表板檢視 toohello 存放區擁有者的另一個複本。

在任何情況下，您需要由多個合作對象，每個訊息 toobe 中，您可以使用服務匯流排*主題*。 主題提供發佈/訂閱的模式，其中每個發佈的訊息可提供 tooone 或多個訂閱註冊 hello 主題。 相較之下，佇列是由單一取用者收到每則訊息。

訊息會傳送 hello tooa 主題相同方式進行傳送 tooa 佇列。 不過，訊息不會從接收 hello 主題直接;它們會從訂閱接收。 您可以將訂用帳戶 tooa 主題視為虛擬佇列，可接收 toothat 主題傳送 hello 訊息複本。 從訂閱接收訊息方式與從佇列收到 hello 相同。

返回 toohello 零售案例，主題，會取代 hello 佇列，並加入訂用帳戶，可以使用哪些 hello 庫存管理系統元件。 hello 系統現在會顯示，如下所示：

![服務匯流排 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

這裡 hello 組態執行方式 toohello 先前佇列架構設計。 也就是說，傳送 toohello 主題的訊息會路由的 toohello**清查**訂用帳戶，從哪些 hello**庫存管理系統**會使用它們。

順序 toosupport hello 管理儀表板中，我們建立第二個訂閱 hello 主題如下所示：

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

使用此設定時，所做每則訊息將 hello POS 終端機可用 tooboth hello**儀表板**和**清查**訂用帳戶。

## <a name="show-me-hello-code"></a>我想 hello 程式碼
hello 文章[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)描述如何 toosign 的 Azure 帳戶，建立服務命名空間。 hello 最簡單方式 tooreference 服務匯流排相依性為 tooinstall hello Service Bus [Nuget 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)。 您也可以尋找 hello 服務匯流排程式庫做為 hello Azure SDK 的一部分。 hello 下載將會位於 hello [Azure SDK 下載頁面](https://azure.microsoft.com/downloads/)。

### <a name="create-hello-topic-and-subscriptions"></a>建立 hello 主題和訂閱
管理 Service Bus 訊息實體 （佇列和發佈/訂閱主題） 都是透過 hello 作業[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)類別。 適當的認證所需的順序 toocreate **NamespaceManager**針對特定的命名空間的執行個體。 服務匯流排會使用以[共用存取簽章 (SAS)](service-bus-sas.md) 為基礎的安全性模型。 hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider)類別代表與內建的 factory 方法傳回某些已知權杖提供者的安全性權杖提供者。 我們將使用[CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_)方法 toohold hello SAS 認證。 hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello hello 服務匯流排命名空間和 hello 權杖提供者的基底地址，然後建構執行個體。

hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)類別會提供方法 toocreate、 列舉和刪除訊息實體。 hello 程式碼，如下所示顯示如何 hello **NamespaceManager**執行個體是已建立並使用 toocreate hello **DataCollectionTopic**主題。

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

請注意，有多載的 hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) hello 主題的 tooset 屬性可讓您的方法。 例如，您可以設定 hello 預設存留時間 (TTL) 值傳送 toohello 主題的訊息。 接下來，新增 hello**清查**和**儀表板**訂用帳戶。

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>傳送訊息 toohello 主題
對於服務匯流排實體上的執行階段作業 (例如，傳送和接收訊息)，應用程式必須先建立 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) 物件。 類似 toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager)類別，hello **MessagingFactory**從 hello hello 服務命名空間和 hello 權杖提供者的基底地址建立執行個體。

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

傳送訊息 tooand 收到來自服務匯流排主題是 hello 的執行個體[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)類別。 這個類別所組成的一組標準屬性 (例如[標籤](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)和[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)) 的字典，其中使用的 toohold 應用程式屬性，和任意應用程式資料的主體。 應用程式可以藉由傳遞任何可序列化的物件設定 hello 主體 (hello 下列範例會傳入**SalesData**表示 hello POS 終端機 hello 銷售資料物件)，就會使用 hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello 物件。 或者，也可以提供 [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) 物件。

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

hello 最簡單方式 toosend 訊息 toohello 主題是 toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)物件直接從 hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)執行個體：

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
類似 toousing 佇列、 訂閱，您可以使用從 tooreceive 訊息[MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver)您直接從 hello 建立物件[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)使用[CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_)。 您可以使用其中一個 hello 的兩個不同接收模式 (**ReceiveAndDelete**和**PeekLock**)，如下所述[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)。

請注意，當您建立**MessageReceiver**訂用帳戶，hello *entityPath*參數屬於 hello 表單`topicPath/subscriptions/subscriptionName`。 因此，toocreate **MessageReceiver** hello**清查**訂用帳戶的 hello **DataCollectionTopic**主題*entityPath*必須設定得`DataCollectionTopic/subscriptions/Inventory`。 hello 程式碼如下所示：

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>訂用帳戶篩選
目前為止，在此案例中傳送 toohello 主題的所有訊息都進行可用 tooall 註冊訂用帳戶。 這裡 hello 主要片語 」 可取得。 」 服務匯流排訂閱可看見所有傳送 toohello 主題的訊息，而您可以複製這些訊息 toohello 虛擬訂閱佇列的子集。 這項工作可透過訂用帳戶「篩選」來進行。 當您建立訂閱時，您可以提供 hello 形式 hello hello 訊息屬性上運作的 SQL92 樣式述詞篩選條件運算式，兩者 hello 系統屬性 (例如，[標籤](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) 和 hello 應用程式屬性，例如**StoreName** hello 前一個範例中。

這發展 hello 案例 tooillustrate，第二個存放區是 toobe 加入的 tooour 零售案例。 從兩個存放區的 hello POS 終端機的所有銷售資料仍有 toobe 路由 toohello 集中式庫存管理系統，但使用 hello 儀表板工具的店只有興趣 hello 該存放區的效能。 您可以使用此篩選 tooachieve 訂用帳戶。 請注意，當 hello POS 終端機發佈訊息時，它們將 hello **StoreName** hello 訊息上的應用程式屬性。 指定兩個存放區，例如**Redmond**和**西雅圖**，hello Redmond hello POS 終端機儲存他們的銷售資料訊息使用的戳記**StoreName**太等於**Redmond**，而 hello 西雅圖儲存 POS 終端機使用**StoreName**太等於**西雅圖**。 hello 存放區管理員的 hello Redmond 只儲存想 toosee 來自其 POS 終端機。 hello 系統會顯示，如下所示：

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

設定此路由 tooset，建立 hello**儀表板**訂用帳戶，如下所示：

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

與這個[訂用帳戶篩選](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)，訊息會 hello **StoreName**屬性設定太**Redmond**將會複製的 toohello hello虛擬佇列**儀表板**訂用帳戶。 沒有篩選，不過更多 toosubscription。 傳遞 tooa 訂用帳戶的虛擬佇列，應用程式可以有多個篩選規則，每個訂閱中新增 toohello 能力 toomodify hello 訊息的屬性。

## <a name="summary"></a>摘要
描述所有 hello 原因 toouse 佇列[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)也適用於 tootopics，特別是：

* 時間解除結合 – 訊息產生者和消費者不需要線上 toobe hello 在相同的時間。
* 負載調節 – 尖峰負載平滑 hello 主題啟用取用應用程式 toobe 佈建針對平均負載而非高峰負載。
* 負載平衡 – 類似 tooa 佇列中，您可以有多個接聽單一訂閱，與遞交 hello 取用者，進而達到負載平衡的其中一個 tooonly 每個訊息的競爭取用者。
* 鬆散結合 – 您可以持續改進 hello 訊息而不會影響現有端點; 的網路例如，新增訂閱或變更篩選 tooa 主題 tooallow 新的消費者。

## <a name="next-steps"></a>後續步驟

請參閱[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)toouse 排入佇列中 hello POS 零售案例的相關資訊。

