---
title: "使用 Azure Service Bus 佇列的 aaaWrite 應用程式 |Microsoft 文件"
description: "如何 toowrite 簡單佇列為基礎的應用程式使用 Azure 服務匯流排。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>建立使用服務匯流排佇列的應用程式
本主題描述服務匯流排佇列，並顯示如何 toowrite 的簡單佇列架構應用程式會使用服務匯流排。

請考慮下列案例： hello world 的零售銷售資料從個別 Point-of-Sale (POS) 終端機必須路由傳送 tooan 庫存管理系統時，所用 hello 資料 toodetermine toobe 補充存貨。 此解決方案會使用服務匯流排訊息 hello 之間的通訊 hello 終端機和 hello 庫存管理系統，hello 遵循圖所示：

![服務匯流排佇列影像 1](./media/service-bus-create-queues/IC657161.gif)

每個 POS 終端機報告其銷售資料，藉由傳送訊息 toohello **DataCollectionQueue**。 這些訊息會維持此佇列，直到擷取 hello 庫存管理系統。 此模式通常稱為*非同步傳訊*，因為 hello POS 終端機無須 toowait hello 庫存管理系統 toocontinue 處理的回覆。

## <a name="why-queuing"></a>為何使用佇列？
我們會審視此應用程式的必要的 tooset hello 程式碼之前，請考慮在此案例中而不需 hello POS 終端機使用佇列的 hello 優點溝通直接 （同步） toohello 庫存管理系統。

### <a name="temporal-decoupling"></a>暫時分離
使用 hello 非同步訊息模式中，產生者和消費者不需要線上 toobe hello 在相同的時間。 hello 訊息基礎結構會可靠地儲存訊息直到 hello 取用方準備 tooreceive 它們。 這表示 hello hello 分散式應用程式元件可以被中斷連線，或是主動;例如，為了進行維護，或因為 tooa 元件損毀，而不會影響 hello 整個系統。 此外，hello 取用應用程式可能只有線上 toobe hello 一天的特定時間。 例如，在此零售案例中，hello 庫存管理系統可能只有 toocome 線上 hello hello 營業日結束後。

### <a name="load-leveling"></a>負載調節
在許多應用程式系統負載會隨著時間改變，而每一單位的工作所需的 hello 處理時間則通常不變。 調解訊息產生者和具有佇列表示 hello 消費性應用程式 （hello 背景工作角色） 的消費者只有 toobe 佈建的 tooservice 平均負載而不是高峰負載。 hello hello 佇列深度會成長，而且合約為 hello 連入負載而有所不同。 這與基礎結構需要的 tooservice hello 應用程式負載而考慮 toohello 數量可直接節省金錢。

![服務匯流排佇列影像 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>負載平衡
為 hello 負載增加，多個背景工作處理序可以是加入的 tooread hello 背景工作佇列中。 只有其中一個 hello 背景工作處理序處理每個訊息。 此外，此提取為基礎的負載平衡能充分利用 hello 背景工作電腦即使 hello 背景工作電腦不同而考慮 tooprocessing 電源，因為它們會在他們自己的最大速率提取訊息。 此模式通常稱為 hello 競爭取用者模式。

![服務匯流排佇列影像 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>鬆散結合
使用訊息佇列 toointermediate 訊息產生者和消費者提供 hello 元件之間的內建鬆散結合。 因為產生者和消費者不知道彼此的存在，取用者可以在 hello 生產者影響的情況下升級。 此外，而不會影響 hello 現有端點的 hello 訊息拓撲能持續改進。 當我們談到發佈/訂閱時，會討論更多這部分的內容。

## <a name="show-me-hello-code"></a>我想 hello 程式碼
hello 之後 > 一節顯示如何 toouse Service Bus toobuild 此應用程式。

### <a name="sign-up-for-an-azure-account"></a>註冊 Azure 帳戶
您需要使用服務匯流排的順序 toostart 中的 Azure 帳戶。 如果您沒有此帳戶，可以在[這裡](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)註冊免費帳戶。

### <a name="create-a-namespace"></a>建立命名空間
當您有訂用帳戶後，便可[建立服務命名空間](service-bus-create-namespace-portal.md)。 每個命名空間會作為一組服務匯流排實體的範圍容器。 請為所有服務匯流排帳戶的新命名空間指定唯一名稱。 

### <a name="install-hello-nuget-package"></a>安裝 hello NuGet 封裝
toouse hello 服務匯流排命名空間，應用程式必須參考 hello 服務匯流排組件，也就是 Microsoft.ServiceBus.dll。 您可以找到此組件的 hello Microsoft Azure SDK，且可在 hello hello 下載[Azure SDK 下載頁面](https://azure.microsoft.com/downloads/)。 不過，hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)是最簡單方式 tooget hello hello 服務匯流排 API 和 tooconfigure hello 服務匯流排相依性的所有應用程式。

### <a name="create-hello-queue"></a>建立 hello 佇列
管理 Service Bus 訊息實體 （佇列和發佈/訂閱主題） 都是透過 hello 作業[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)類別。 服務匯流排會使用以[共用存取簽章 (SAS)](service-bus-sas.md) 為基礎的安全性模型。 hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)類別代表與內建的 factory 方法傳回某些已知權杖提供者的安全性權杖提供者。 我們將使用[CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_)方法 toohold hello SAS 認證。 hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) hello hello 服務匯流排命名空間和 hello 權杖提供者的基底地址，然後建構執行個體。

hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)類別會提供方法 toocreate、 列舉和刪除訊息實體。 hello 程式碼，如下所示顯示如何 hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)執行個體是已建立並使用 toocreate hello **DataCollectionQueue**佇列。

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

請注意，有多載的 hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_)啟用內容的 hello 佇列 toobe 微調的方法。 例如，您可以設定 hello 預設存留時間 (TTL) 值傳送 toohello 佇列的訊息。

### <a name="send-messages-toohello-queue"></a>傳送訊息 toohello 佇列
對於服務匯流排實體上的執行階段作業 (例如，傳送和接收訊息)，應用程式必須先建立 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 物件。 類似 toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)類別，hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)從 hello hello 服務命名空間和 hello 權杖提供者的基底地址建立執行個體。

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

訊息傳送至，並收到來自服務匯流排佇列都是執行個體的 hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)類別。 這個類別所組成的一組標準屬性 (例如[標籤](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)和[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)) 的字典，其中使用的 toohold 應用程式屬性，和任意應用程式資料的主體。 應用程式可以藉由傳遞任何可序列化的物件設定 hello 主體 (hello 下列範例會傳入**SalesData**表示 hello POS 終端機 hello 銷售資料物件)，就會使用 hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello 物件。 或者，也可以提供 [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx) 物件。

hello 我們的案例 hello 中指定佇列中，最簡單的方式 toosend 訊息 tooa **DataCollectionQueue**，是 toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)物件直接從 hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)執行個體。

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>從 hello 佇列接收訊息
tooreceive 從 hello 佇列的訊息，您可以使用[MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver)您直接從 hello 建立物件[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)使用[CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_)。 訊息接收者可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。 hello [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode)建立 hello 訊息接收者時，做為參數 toohello 設定[CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_)呼叫。

當使用 hello **ReceiveAndDelete**模式中，會收到 hello 是單發式作業; 也就是服務匯流排收到 hello 要求時，它會標示為正在使用的 hello 訊息，並傳回它 toohello 應用程式。 **ReceiveAndDelete**模式是 hello 簡單的模式，最適合用於中的 hello 應用程式可以容許 toooccur 失敗時，不處理訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排會標示為正在使用的 hello 訊息，因為當 hello 應用程式重新啟動並開始取用訊息，將會遺失 hello 損毀之前所耗用的 hello 訊息。

在**PeekLock**模式，hello 接收會變成兩階段作業，使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到 hello 要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)上收到 hello 訊息。 當服務匯流排會看見 hello[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)呼叫時，它會將標示為正在使用的 hello 訊息。

可能會有兩種不同的結果。 首先，如果 hello 應用程式無法 tooprocess hello 訊息，因為某些原因，它可以呼叫[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)上收到 hello 訊息 (而不是[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete))。 這會使服務匯流排 toounlock hello 訊息，並讓它再次接收可用 toobe、 由 hello 相同的消費者或其他競爭消費者。 第二，沒有逾時與 hello 鎖定相關聯，而且如果 hello 應用程式無法處理 hello 訊息 hello 鎖定逾時過期之前 （例如，如果 hello 應用程式當機），然後將會解除鎖定 Service Bus hello 訊息，並將其可用 toobe接收一次 (基本上執行[放棄](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)作業依預設)。

請注意，如果 hello 應用程式損毀它處理 hello 訊息之後但在 hello 之前[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)發出要求，hello 訊息將已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為 * At Least Once * 處理。 這表示每則訊息會至少一次處理，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理 hello 應用程式 toodetect 重複的情況需要額外的邏輯。 這可以根據 hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) hello 訊息屬性。 這個屬性的 hello 值傳遞嘗試都維持不變。 這便稱為「剛好一次」處理。

hello 如下所示的程式碼接收和處理訊息，使用 hello **PeekLock**模式中，這是 hello 預設值，如果沒有[ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode)明確提供值。

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>使用 hello 佇列用戶端
hello 本節稍早建立的範例[MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender)和[MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver)物件直接從 hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend 和接收訊息從 hello 佇列分別。 另一個方法是 toouse [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)物件，其支援同時傳送和接收作業中加入 toomore 進階功能，例如工作階段。

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的佇列的基本概念，請參閱[建立使用服務匯流排主題和訂用帳戶的應用程式](service-bus-create-topics-subscriptions.md)toocontinue 使用 hello 發佈/訂閱功能的 Service Bus 主題討論和訂用帳戶。

