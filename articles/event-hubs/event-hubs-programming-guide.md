---
title: "Azure 事件中心的 aaaProgramming 指南 |Microsoft 文件"
description: "使用 Azure.NET SDK hello Azure 事件中心撰寫的程式碼。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>事件中樞程式設計指南

這篇文章會討論一些常見的案例中撰寫程式碼使用 Azure 事件中樞與 hello Azure.NET SDK。 它假設使用者對事件中樞已有初步了解。 事件中心概念的概觀，請參閱 hello[事件中心概觀](event-hubs-what-is-event-hubs.md)。

## <a name="event-publishers"></a>事件發佈者

您傳送事件 tooan 事件中心使用 HTTP POST 或透過 AMQP 1.0 連線。 hello 選擇的哪一個 toouse 和時機取決於要定址的 hello 特定案例。 AMQP 1.0 連線是以服務匯流排中的代理連線形式計量，其較適合經常出現大量訊息且需要低延遲的案例，因為它們可提供持續的傳訊通道。

您建立和管理事件中心使用 hello [NamespaceManager][]類別。 當使用 hello.NET managed Api 時，hello 主要會建構如發佈資料 tooEvent 集線器是 hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient)和[EventData][]類別。 [EventHubClient][]提供 hello 的事件傳送 toohello 事件中心的 AMQP 通訊通道。 hello [EventData][]類別代表事件，並為使用的 toopublish 訊息 tooan 事件中樞。 這個類別包含 hello 本文、 一些中繼資料及 hello 事件的標頭資訊。 其他屬性會加入 toohello [EventData][]物件通過事件中心。

## <a name="get-started"></a>開始使用

支援事件中樞的 hello.NET 類別被提供 hello Microsoft.ServiceBus.dll 組件中。 最簡單的方式 tooreference hello 服務匯流排 API 和 tooconfigure hello hello 服務匯流排相依性的所有應用程式都為 toodownload hello[服務匯流排 NuGet 封裝](https://www.nuget.org/packages/WindowsAzure.ServiceBus)。 或者，您可以使用 hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) Visual Studio 中。 toodo 因此，發出下列命令在 hello hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)視窗：

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>建立事件中心
您可以使用 hello [NamespaceManager][]類別 toocreate 事件中心。 例如：

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

在大部分情況下，建議您使用 hello [CreateEventHubIfNotExists][]方法 tooavoid hello 服務重新啟動時產生例外狀況。 例如：

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

所有事件中心建立作業，包括[CreateEventHubIfNotExists][]，需要**管理**hello 相關的命名空間的權限。 如果您想 toolimit hello 權限的發行者或取用者應用程式，您可以避免這些建立作業呼叫在實際執行程式碼中，當您使用有限權限的認證。

hello [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription)類別包含有關事件中心，包括 hello 授權規則、 hello 訊息保留間隔、 資料分割識別碼、 狀態和路徑的詳細資料。 事件中心上，您可以使用此類別 tooupdate hello 中繼資料。

## <a name="create-an-event-hubs-client"></a>建立事件中樞用戶端
hello 與事件中心互動的主要類別是[Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]。 這個類別提供傳送者和接收者功能。 您可以具現化這個類別使用 hello[建立](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create)方法 hello 下列範例所示。

```csharp
var client = EventHubClient.Create(description.Path);
```

這個方法會使用 hello 服務匯流排連接資訊在 hello App.config 檔案中，在 hello `appSettings` > 一節。 如需範例的 hello `appSettings` XML 使用 toostore hello 服務匯流排連接資訊，請參閱 hello 文件以 hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_)方法。

另一個選項是 toocreate hello 用戶端從連接字串。 此選項可以使用 Azure 背景工作角色時，因為 hello 字串存放 hello hello 背景工作的組態屬性。 例如：

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

hello 連接字串會在相同的格式出現在 hello 先前方法的 hello App.config 檔案中的 hello:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

最後，它也是可能 toocreate [EventHubClient][]物件從[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory)執行個體，如下列範例中的 hello 中所示。

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

它是額外的重要 toonote [EventHubClient][]從傳訊 factory 執行個體建立的物件將會重複使用 hello 相同基礎 TCP 連線。 因此，這些物件對用戶端的輸送量將受到限制。 hello[建立](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_)方法重複使用單一傳訊 factory。 如果您與單一傳送者之間需要大量輸送量，可以建立多個訊息處理站，並從每個傳訊處理站建立一個 [EventHubClient][] 物件。

## <a name="send-events-tooan-event-hub"></a>傳送事件 tooan 事件中樞
您藉由建立傳送事件 tooan 事件中心[EventData][]執行個體，並將它傳送嗨透過[傳送](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_)方法。 這個方法會採用單一[EventData][]例項參數，並以同步方式傳送 tooan 事件中心。

## <a name="event-serialization"></a>事件序列化
hello [EventData][]類別具有[四個多載建構函式](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_)可接受各種參數，例如物件和序列化程式、 位元組陣列或資料流。 它也是可能 tooinstantiate hello [EventData][]類別並之後設定 hello 內文資料流。 當使用 JSON 與[EventData][]，您可以使用**Encoding.UTF8.GetBytes()** tooretrieve hello 位元組陣列的 JSON 編碼的字串。

## <a name="partition-key"></a>資料分割索引鍵
hello [EventData][]類別具有[PartitionKey][]屬性，可讓 hello 寄件者 toospecify 的值是雜湊 tooproduce 資料分割指派。 使用資料分割索引鍵，以確保所有以相同的金鑰會傳送的 hello hello 事件 toohello hello 事件中心在相同資料分割。 常見的資料分割索引鍵包含使用者工作階段識別碼和唯一的傳送者識別碼。 hello [PartitionKey][]是選擇性屬性，可供使用 hello 時[Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_)或[Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_)方法。 如果您未提供的值[PartitionKey][]，傳送事件是分散式的 toopartitions 使用循環配置資源模型。

### <a name="availability-considerations"></a>可用性考量

使用資料分割索引鍵為選擇性，而且您應該仔細考慮是否 toouse 其中一個。 在許多情況下，如果事件的順序很重要，您最好選擇使用資料分割索引鍵。 當您使用資料分割索引鍵時，這些資料分割必須在單一節點上可供使用，但經過一段時間後，節點有可能會發生中斷，例如在計算節點重新開機及修補時。 因此，如果設定分割區識別碼和因為某種原因，該資料分割變成無法使用，該分割中的嘗試 tooaccess hello 資料將會失敗。 高可用性是最重要的如果未指定資料分割索引鍵，在此情況下的事件將會傳送 toopartitions 使用先前所述的 hello 循環配置資源模型。 在此案例中，您要進行的可用性 （沒有分割區識別碼） 與一致性 （釘選事件 tooa 分割區識別碼） 之間的明確選擇。

另一項考量是對處理事件的延遲進行處理。 在某些情況下可能會更好的 toodrop 資料比 tootry 重試和跟上處理，都可能會造成進一步的下游處理延遲。 例如，股票行情指示器很更好的 toowait 完成的最新資料，但在即時聊天或 VOIP 案例快，您想讓 hello 資料即使它不是完整。

指定的這些可用性考量，在這些情況下您可能會選擇其中一個 hello 下列的錯誤處理策略：

- 停止 (停止讀取事件中樞，直到情況獲得修正)
- 捨棄 (訊息並不重要，將其卸除)
- 重試 (重試 hello 訊息，因為您會看到符合)
- [寄不出信件](../service-bus-messaging/service-bus-dead-letter-queues.md)（佇列或另一個事件中樞 toodead 字母 hello 訊息，您只使用無法處理）

如需詳細資訊和討論 hello 之間的利弊得失可用性和一致性，請參閱[可用性和事件中心的一致性](event-hubs-availability-and-consistency.md)。 

## <a name="batch-event-send-operations"></a>批次事件傳送作業
分批傳送事件能大幅增加輸送量。 hello [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)方法會採用**IEnumerable**型別的參數[EventData][]和傳送 hello 與不可部分完成的作業 toohello 事件中心的整個批次。

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

請注意，單一批次不能超過事件的 hello 256 KB 的限制。 此外，在 hello 批次中的每個訊息會使用 hello 相同的發行者識別。 它是 hello hello 批次的傳送者 tooensure hello 責任不超過 hello 事件大小上限。 如果超過的話，系統會產生用戶端 **Send** 錯誤。

## <a name="send-asynchronously-and-send-at-scale"></a>以非同步方式傳送和大規模傳送
您也可以以非同步方式傳送事件 tooan 事件中心。 以非同步方式傳送可以提高用戶端之後無法 toosend 事件 hello 速率。 這兩個 hello[傳送](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_)和[SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)方法都有非同步版本可傳回[工作](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)物件。 雖然這項技術可以增加輸送量，它也會造成 hello 用戶端 toocontinue toosend 事件即使它已實施節流 hello 事件中心服務，並可能會導致 hello 用戶端發生失敗或遺失的訊息時如果未正確實作。 此外，您可以使用 hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) hello 用戶端 toocontrol 用戶端重試選項上的屬性。

## <a name="create-a-partition-sender"></a>建立資料分割的傳送者
雖然它是最常見 toosend 事件 tooan 事件中樞沒有資料分割索引鍵，在某些情況下您可能想 toosend 事件直接 tooa 給定資料分割。 例如：

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_)傳回[EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender)物件，您可以使用 toopublish 事件 tooa 特定事件中心資料分割。

## <a name="event-consumers"></a>事件取用者
事件中樞有兩個主要的事件取用模型：直接接收者和較高層級的抽象 (如 [EventProcessorHost][])。 直接接收者負責自行協調取用者群組內存取 toopartitions。

### <a name="direct-consumer"></a>直接消費者
hello 最直接的方式 tooread 取用者群組內的資料分割為 toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver)類別。 這個類別的執行個體 toocreate，您必須使用 hello 的執行個體[EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup)類別。 在下列範例的 hello，hello 分割區識別碼時，必須指定建立 hello 接收器 hello 取用者群組。

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

hello [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary)方法有數個多載可加強控制所建立的 hello 讀取器。 這些方法包括位移指定為字串或時間戳記，而且 hello 能力 toospecify 是否 tooinclude hello 在此指定的位移傳回串流處理，還是它之後啟動。 建立 hello 接收者之後，您可以開始接收 hello 傳回物件上的事件。 hello[接收](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary)方法有四個多載，該控制項 hello 接收操作參數，例如批次大小和等待時間。 您可以使用取用者的這些方法 tooincrease hello 輸送量 hello 非同步版本。 例如：

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

尊重 tooa 特定分割區，以在其中傳送 toohello 事件中心的 hello 順序來接收 hello 訊息。 hello 位移是字串語彙基元使用的 tooidentify 資料分割中的訊息。

請注意，消費者群組內的單一資料分割一律不能擁有超過 5 個已連接的並行讀取器。 當讀取器連接或中斷時，他們的工作階段可能會持續作用數分鐘才能 hello 服務辨識它們已中斷連線。 在此期間，重新連接 tooa 磁碟分割可能會失敗。 撰寫直接接收者建立事件中樞的完整範例，請參閱 hello[事件中心直接接收者](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6)範例。

### <a name="event-processor-host"></a>事件處理器主機
hello [EventProcessorHost][]類別處理來自事件中心資料。 Hello.NET 平台上建置事件讀取器時，您應該使用這項實作。 [EventProcessorHost][] 能為事件處理器實作提供安全執行緒、多處理序、安全的執行階段環境，進而提供檢查點和資料分割租用管理。

toouse hello [EventProcessorHost][]類別時，您可以實作[IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor)。 這個介面包含三個方法：

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

toostart 事件處理，具現化[EventProcessorHost][]，事件中心提供 hello 適當的參數。 然後，呼叫[RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister 您[IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) hello 執行階段實作。 此時，hello 主機將會嘗試 tooacquire hello 事件中心採用 「 窮盡 」 演算法中的每個資料分割上的租用。 這些租用將延續一段指定時間，然後必須更新。 為新的節點，背景工作執行個體在此情況下，上線，它們會預訂租約，並且經過一段時間 hello 負載會轉移節點之間為每個嘗試次數 tooacquire 更多租用。

![事件處理器主機](./media/event-hubs-programming-guide/IC759863.png)

經過一段時間後，均衡的局面將會出現。 此動態功能可讓 CPU 型自動調整套用 toobe tooconsumers 向上延展和向下調整。 因為事件中心之間沒有直接的訊息計數概念，平均 CPU 使用率通常是 hello 最佳機制 toomeasure 後端或取用者小數位數。 如果發行者開始的 toopublish 可以處理更多的事件取用者比，取用者上的 hello CPU 增加可以使用的 toocause 自動調整規模上背景工作執行個體計數。

hello [EventProcessorHost][]類別也實作 Azure 儲存體為基礎的檢查點機制。 已使每一個取用者可以判斷先前取用者 hello 哪些 hello 最後一個檢查點位移針對每個資料分割，此機制存放區 hello。 由於資料分割轉換之間透過租約在節點，這是 hello 加速負載移轉的同步處理機制。

## <a name="publisher-revocation"></a>發佈者撤銷
此外 toohello 進階執行階段功能的[EventProcessorHost][]，事件中心也啟用發行者撤銷中順序 tooblock 特定發行者傳送事件 tooan 事件中心。 如果發行者權杖已遭洩漏，或軟體更新造成 toobehave 不當，這些功能會特別有用。 在這些情況下，hello 發行者的身分識別，是其 SAS 權杖的一部分，可能會封鎖從發行事件。

如需有關發行者撤銷及如何 toosend tooEvent 中心為發行者，請參閱 hello[事件中心大規模安全發行](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab)範例。

## <a name="next-steps"></a>後續步驟
toolearn 有關事件中心案例的詳細資訊，請前往下列連結：

* [事件中樞 API 概觀](event-hubs-api-overview.md)
* [何謂事件中樞](event-hubs-what-is-event-hubs.md)
* [事件中樞的可用性和一致性](event-hubs-availability-and-consistency.md)
* [事件處理器主機 API 參考](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
