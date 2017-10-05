---
title: "建立使用 Azure 服務匯流排主題和訂用帳戶的應用程式 | Microsoft Docs"
description: "介紹服務匯流排主題和訂用帳戶所提供的發佈/訂閱功能。"
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
ms.openlocfilehash: eb01120ce9578f716e5381c107faa93f0b36e358
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>建立使用服務匯流排主題和訂用帳戶的應用程式
Azure 服務匯流排支援一套以雲端為基礎、訊息導向的中介軟體技術，包括可靠的訊息佇列和持久的發佈/訂閱訊息。 本文是根據[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)所提供的資訊撰寫而成，並簡介服務匯流排主題所提供的發佈/訂閱功能。

## <a name="evolving-retail-scenario"></a>不斷演變的零售案例
本文會繼續運用[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中的零售案例。 請回想一下先前提過的，個別銷售點 (POS) 終端機的銷售資料，必須路由傳送至庫存管理系統，讓系統使用該資料來判斷何時必須補充庫存。 每個 POS 終端機會將訊息傳送至 **DataCollectionQueue** 佇列，藉此回報其銷售資料，訊息會在佇列中持續保留，直到庫存管理系統收到為止，如下所示：

![服務匯流排 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

為了進一步演變此案例，我們已將新的要求加入至系統：商店老闆想要能夠即時監視商店的銷售業績。

為了滿足這項要求，系統必須「支開」銷售資料流。 我們還是需要 POS 終端機傳送的每則訊息像之前一樣，傳送至庫存管理系統，但我們想要每則訊息的另一個複本，以便對商店老闆呈現儀表板檢視。

在任何類似情況下，如果需要每則訊息是由多方取用，您可以使用服務匯流排「主題」。 主題提供發佈/訂閱模式，亦即每則發佈的訊息會提供給向主題註冊的一或多個訂用帳戶。 相較之下，佇列是由單一取用者收到每則訊息。

訊息傳送至主題的方式會與傳送至佇列的方式相同。 不過，訊息不是直接從主題處接收；而是從訂用帳戶接收的。 您可以將主題的訂用帳戶視為虛擬佇列，可接收已傳送到該主題的訊息複本。 從訂用帳戶接收訊息的方式與從佇列接收訊息的方式相同。

回到零售案例中，主題會取代佇列，而新增的訂用帳戶將可由庫存管理系統元件使用。 系統現在看起來會像下面這樣：

![服務匯流排 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

這裡的組態會與先前以佇列為基礎的設計的運作方式完全相同。 也就是傳送至主題的訊息，會路由傳送至 **Inventory** 訂用帳戶，然後由**庫存管理系統**從中取用。

為了支援管理儀表板，我們在主題上建立了第二個訂用帳戶，如下所示：

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

在此組態中，來自 POS 終端機的每則訊息皆會提供給 **Dashboard** 和 **Inventory** 訂用帳戶。

## <a name="show-me-the-code"></a>示範程式碼
[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)文章中說明如何註冊 Azure 帳戶，並建立服務命名空間。 參考服務匯流排相依性的最簡單方式是，安裝服務匯流排 [Nuget 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus/)。 您也可以在 Azure SDK 中找到服務匯流排程式庫。 您可以在 [Azure SDK 下載頁面](https://azure.microsoft.com/downloads/)中下載。

### <a name="create-the-topic-and-subscriptions"></a>建立主題和訂用帳戶
服務匯流排傳訊實體的管理作業 (佇列和發佈/訂閱主題) 是透過 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別來執行。 需要有適當的認證，才能建立特定命名空間的 **NamespaceManager** 執行個體。 服務匯流排會使用以[共用存取簽章 (SAS)](service-bus-sas.md) 為基礎的安全性模型。 [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) 類別代表安全性權杖提供者，其具有內建 Factory 方法，可傳回部分已知的權杖提供者。 我們將使用 [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) 方法來保存 SAS 認證。 接著使用服務匯流排命名空間和權杖提供者的基底位址建構 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 執行個體。

[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別提供用以建立、列舉及刪除傳訊實體的方法。 此處的程式碼會示範如何建立 **NamespaceManager** 執行個體，並用來建立 **DataCollectionTopic** 主題。

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

請注意，您可使用 [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) 方法的多載來設定主題的屬性。 例如，您可以為傳送到主題的訊息，設定預設的存留時間 (TTL) 值。 接下來，新增 **Inventory** 和 **Dashboard** 訂用帳戶。

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-to-the-topic"></a>將訊息傳送到主題
對於服務匯流排實體上的執行階段作業 (例如，傳送和接收訊息)，應用程式必須先建立 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) 物件。 **MessagingFactory** 執行個體類似於 [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) 類別，是從服務命名空間和權杖提供者的基底位址建立的。

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

傳送至 (和接收自) 服務匯流排主題的訊息是 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 類別的執行個體。 此類別包含一組標準屬性 (例如 [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) 和 [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive))、一個用來保存應用程式屬性的字典，以及任意應用程式資料的主體。 應用程式可以傳入任何可序列化物件來設定主體 (以下範例傳入 **SalesData** 物件代表 POS 終端機的銷售資料)，藉此利用 [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) 將物件序列化。 或者，也可以提供 [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) 物件。

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

將訊息傳送至主題的最簡單方式是使用 [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_)，直接從 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 執行個體建立 [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) 物件：

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
與使用佇列類似，您可以使用 [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) 物件 (可使用 [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_) 從 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 直接建立)，接收來自訂用帳戶的訊息。 您可以使用兩種不同接收模式的其中之一 (**ReceiveAndDelete** 和 **PeekLock**)，如[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中所述。

請注意，當您建立訂用帳戶的 **MessageReceiver** 時，*entityPath* 參數的形式會是 `topicPath/subscriptions/subscriptionName`。 因此，若要為 **DataCollectionTopic** 主題的 **Inventory** 訂用帳戶建立 **MessageReceiver**，*entityPath* 必須設為 `DataCollectionTopic/subscriptions/Inventory`。 程式碼看起來會像下面這樣：

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
到目前為止，此案例中傳送至主題的所有訊息，都會提供給所有已註冊的訂用帳戶。 請注意「都會提供」這幾個字。 雖然服務匯流排訂用帳戶可看見所有傳送至主題的訊息，但您只能將部分訊息複製到虛擬訂用帳戶佇列。 這項工作可透過訂用帳戶「篩選」來進行。 當您建立訂用帳戶時，可以用 SQL92 樣式的述詞形式，提供依訊息屬性運作的篩選運算式，這之中包括系統屬性 (例如 [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) 和應用程式屬性 (例如上一個範例中的 **StoreName**)。

若要演變案例來說明這點，要將第二間商店加入我們的零售案例。 兩間商店的所有 POS 終端機的銷售資料，還是必須路由傳送至集中的庫存管理系統，但使用儀表板工具的店經理只注意到商店的銷售業績。 您可以用訂用帳戶篩選來達到此目的。 請注意，當 POS 終端機發佈訊息時，會在訊息上設定 **StoreName** 應用程式屬性。 假設有兩間商店，例如 **Redmond** 和 **Seattle**，Redmond 商店中的 POS 終端機將其銷售資料訊息戳記了 **StoreName** 等於 **Redmond**，而 Seattle 商店的 POS 終端機則使用 **StoreName** 等於 **Seattle**。 Redmond 商店的店經理只想要查看其 POS 終端機的資料。 系統看起來會像下面這樣：

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

若要設定此路由傳送，您必須建立 **Dashboard** 訂用帳戶，如下所示：

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

使用此[訂用帳戶篩選](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)時，只有 **StoreName** 屬性設定為 **Redmond** 的訊息才會複製到 **Dashboard** 訂用帳戶的虛擬佇列。 但還有更多其他訂用帳戶篩選。 除了能夠在訊息傳遞到訂用帳戶的虛擬佇列時修改訊息屬性外，應用程式還可以在每個訂用帳戶中擁有多個篩選規則。

## <a name="summary"></a>摘要
在[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)中所有使用佇列的原因說明，具體上也適用於使用主題的原因：

* 暫時分離 – 訊息產生者和取用者不需要同時在線上。
* 負載調節 – 由主題舒緩負載尖峰，因而可針對平均負載 (而非尖峰負載) 來佈建取用應用程式。
* 負載平衡 – 類似於佇列，您可以有多個競爭取用者接聽單一訂用帳戶，並將每則訊息遞交給其中一個取用者，進而平衡負載。
* 鬆散結合 – 您可以在不影響現有端點的情況下發展傳訊網路；例如，新增訂用帳戶或變更主題的篩選，以接納新的取用者。

## <a name="next-steps"></a>後續步驟

請參閱[建立使用服務匯流排佇列的應用程式](service-bus-create-queues.md)，了解如何在 POS 零售案例中使用佇列的相關資訊。

