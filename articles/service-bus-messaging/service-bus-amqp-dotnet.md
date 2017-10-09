---
title: "使用.NET 和 AMQP 1.0 匯流排 aaaService |Microsoft 文件"
description: "搭配使用 .NET 的 Azure 服務匯流排與 AMQP"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>搭配使用 .NET 的服務匯流排與 AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>下載服務匯流排 SDK hello

Hello 服務匯流排 SDK 版本 2.1 或更新版本中使用 AMQP 1.0 支援。 您可以確保您的 hello 服務匯流排的位元從下載最新版本的 hello [NuGet][NuGet]。

## <a name="configuring-net-applications-toouse-amqp-10"></a>設定.NET 應用程式 toouse AMQP 1.0

根據預設，hello 服務匯流排.NET 用戶端程式庫會與 hello 使用專用的 SOAP 架構通訊協定的服務匯流排服務通訊。 toouse AMQP 1.0 而不是 hello 預設通訊協定需要明確設定於 hello 服務匯流排連接字串，hello 下一節中所述。 除了這項變更之外，在使用 AMQP 1.0 時，應用程式程式碼會維持不變。

在 hello 目前版本中，有一些使用 AMQP 時，不支援的 API 功能。 這些不支援的功能列稍後在 hello 區段[不支援的功能、 限制和行為的差異](#unsupported-features-restrictions-and-behavioral-differences)。 有些進階組態設定的 hello 也具有不同的意義，使用 AMQP 時。

### <a name="configuration-using-appconfig"></a>使用 App.config 進行設定

它是應用程式 toouse hello App.config 組態檔 toostore 設定好的作法。 服務匯流排應用程式，您可以使用 App.config toostore hello 服務匯流排連接字串。 範例 App.config 檔案如下所示：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

hello 值 hello`Microsoft.ServiceBus.ConnectionString`設定是為使用的 tooconfigure hello 連接 tooService 匯流排 hello 服務匯流排連接字串。 hello 格式如下所示：

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

其中`[namespace]`和`SharedAccessKey`取自 hello [Azure 入口網站][ Azure portal]當您建立服務匯流排命名空間。 如需詳細資訊，請參閱[建立服務匯流排命名空間使用 hello Azure 入口網站][Create a Service Bus namespace using hello Azure portal]。

使用 AMQP 時，附加與 hello 連接字串`;TransportType=Amqp`。 這個標記法指示 hello 用戶端程式庫 toomake 其連線 tooService 匯流排使用 AMQP 1.0。

## <a name="message-serialization"></a>訊息序列化

Hello 預設序列化行為 hello.NET 用戶端程式庫時使用 hello 預設通訊協定，為 toouse hello [DataContractSerializer] [ DataContractSerializer]輸入 tooserialize [BrokeredMessage] [ BrokeredMessage] hello 用戶端程式庫和 hello 服務匯流排服務之間傳輸的執行個體。 Hello 用戶端程式庫使用 hello AMQP 傳輸模式時，會使用 hello AMQP 類型系統的 hello 序列化[代理的訊息][ BrokeredMessage]至 AMQP 訊息。 此序列化讓 hello 訊息 toobe 接收和解譯接收的應用程式可能在不同的平台，例如，使用 hello JMS API tooaccess 服務匯流排的 Java 應用程式上執行。

當您建構[BrokeredMessage] [ BrokeredMessage]執行個體，您可以提供.NET 物件當做參數 toohello 建構函式 tooserve，作為 hello hello 訊息主體。 物件可以是對應的 tooAMQP 基本型別，hello 主體會序列化至 AMQP 資料類型。 如果 hello 物件無法直接對應至 AMQP 基本類型。也就是使用 hello 序列化 hello 應用程式，然後在 hello 物件定義的自訂類型[DataContractSerializer][DataContractSerializer]，和 AMQP 資料訊息中傳送嗨序列化位元組。

toofacilitate 互通性與非.NET 用戶端，使用可直接序列化至 AMQP 類型以供 hello hello 訊息本文，.NET 型別。 hello 下表詳細說明這些類型和 hello 對應對應 toohello AMQP 類型系統。

| .NET 主體物件類型 | 對應的 AMQP 類型 | AMQP 主體區段類型 |
| --- | --- | --- |
| 布林 |布林值 |AMQP 值 |
| byte |ubyte |AMQP 值 |
| ushort |ushort |AMQP 值 |
| uint |uint |AMQP 值 |
| ulong |ulong |AMQP 值 |
| sbyte |byte |AMQP 值 |
| short |short |AMQP 值 |
| int |int |AMQP 值 |
| long |long |AMQP 值 |
| float |float |AMQP 值 |
| double |double |AMQP 值 |
| decimal |decimal128 |AMQP 值 |
| char |char |AMQP 值 |
| DateTime |timestamp |AMQP 值 |
| Guid |uuid |AMQP 值 |
| byte[] |binary |AMQP 值 |
| string |string |AMQP 值 |
| System.Collections.IList |list |AMQP 值： hello 集合中包含的項目只能在此資料表中定義的。 |
| System.Array |array |AMQP 值： hello 集合中包含的項目只能在此資料表中定義的。 |
| System.Collections.IDictionary |map |AMQP 值： hello 集合中包含的項目只能在此資料表中定義的。注意： 只有字串索引鍵支援。 |
| Uri |描述字串 （請參閱下表中的 hello） |AMQP 值 |
| Datetimeoffset |描述的 long （請參閱下表中的 hello） |AMQP 值 |
| 時間範圍 |描述的 long （請參閱下列 hello） |AMQP 值 |
| Stream |binary |AMQP 資料 (可能有多個)。 hello 資料區段包含 hello 未經處理位元組讀取 hello 資料流物件。 |
| 其他物件 |binary |AMQP 資料 (可能有多個)。 包含序列化 hello 二進位的 hello DataContractSerializer 或 hello 應用程式所提供的序列化程式所使用的 hello 物件。 |

| .NET 類型 | 對應的 AMQP 描述類型 | 注意事項 |
| --- | --- | --- |
| Uri |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>不支援的功能、限制和行為差異

hello 遵循 hello 服務匯流排.NET API 的功能目前不支援使用 AMQP 時：

* 交易
* 透過傳輸目的地傳送

另外還有一些小差異中的 hello 服務匯流排.NET API 的 hello 行為時，使用 AMQP 比較的 toohello 預設通訊協定：

* hello [OperationTimeout] [ OperationTimeout]屬性會被忽略。
* `MessageReceiver.Receive(TimeSpan.Zero)` 會實作為 `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`。
* 完成訊息的鎖定權杖只能夠由開始收到 hello 訊息的 hello 訊息接收者。

## <a name="controlling-amqp-protocol-settings"></a>控制 AMQP 通訊協定設定

hello [.NET Api](/dotnet/api/)公開數個設定 toocontrol hello hello AMQP 通訊協定的行為：

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**： 控制項 hello 套用的初始信用額度 tooa 連結。 hello 預設值為 0。
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**： 在連接開啟時間 hello 交涉期間提供的控制項 hello AMQP 框架大小上限。 hello 預設值為 65,536 位元組。
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**： 如果傳輸可以批次進行，這個值會決定用於傳送處置 hello 最大延遲。 預設由傳送者/接收者繼承。 個別的傳送者/接收者可以覆寫，而不是 20 毫秒 hello 預設。
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**︰控制是否透過 SSL 連線建立 AMQP 連線。 hello 預設值是**true**。

## <a name="next-steps"></a>後續步驟

更準備 toolearn 嗎？ 請造訪下列連結查看 hello:

* [服務匯流排 AMQP 概觀]
* [適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]
* [Windows Server 服務匯流排中的 AMQP]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[服務匯流排 AMQP 概觀]: service-bus-amqp-overview.md
[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
