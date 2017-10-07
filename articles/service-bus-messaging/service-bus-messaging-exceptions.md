---
title: "aaaAzure 服務匯流排訊息例外狀況 |Microsoft 文件"
description: "服務匯流排傳訊例外狀況和建議的動作清單。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>服務匯流排傳訊例外狀況
本文列出一些 hello Microsoft Azure 服務匯流排所產生的例外狀況訊息處理應用程式開發介面。 這個參考是主體 toochange，因此稍後回來查看更新。

## <a name="exception-categories"></a>例外狀況類別
hello 訊息 Api 產生可以分為下列類別目錄的 hello 的例外狀況，以及相關聯的 hello 動作中，您可以採取 tootry toofix 它們。 請注意，hello 的意義和例外狀況的原因可以根據 hello 訊息實體 （佇列/主題或事件中心） 類型不同：

1. 使用者程式碼撰寫錯誤 ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)、[System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx)、[System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx)、[System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx))。 一般動作： 嘗試 toofix hello 程式碼，再繼續進行。
2. 設定/組態錯誤 ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception)、[System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx))。 一般動作：檢閱您的組態並視需要進行變更。
3. 暫時性例外狀況 ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception)、[Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)、[Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception))。 一般動作： hello 作業重試一次，或通知使用者。
4. 其他例外狀況 ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx)、[System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)、[Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception)、[Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception))。 一般動作： 特定 toohello 例外狀況類型。請參閱 toohello hello 之後 > 一節中的資料表。 

## <a name="exception-types"></a>例外狀況類型
hello 下表列出訊息的例外狀況類型，其原因和附註您可以採取建議的動作。

| **例外狀況類型** | **描述/原因/範例** | **建議的動作** | **自動/立即重試附註** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |hello 伺服器未回應要求的 toohello hello 內的作業指定時間所控制的[OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout)。 hello 伺服器可能已完成 hello 要求的作業。 這種情形到期 toonetwork 或其他基礎結構延遲。 |檢查一致性的 hello 系統狀態，並視需要重試。 請參閱 [逾時例外狀況](#timeoutexception)。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |hello 要求 hello 伺服器或服務中不允許使用者操作。 請參閱 hello 例外狀況訊息，如需詳細資訊。 例如，[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)將會產生這個例外狀況，如果在收到 hello 訊息[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式。 |請檢查 hello 程式碼和 hello 文件。 請確定 hello 要求作業無效。 |重試將無助益。 |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |嘗試進行 tooinvoke 已經關閉、 中止或處置的物件上的作業。 在罕見的情況下，hello 環境交易已經過處置。 |請檢查 hello 程式碼，並確定它不會叫用已處置的物件上的作業。 |重試將無助益。 |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)物件無法取得驗證權杖、 hello 權杖無效，或 hello token 未包含 hello 宣告需要的 tooperform hello 作業。 |請確定 hello 權杖提供者會透過 hello 正確的值。 請檢查 hello hello 存取控制服務組態。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |一或多個引數提供 toohello 方法均為無效。<br /> hello URI 提供太[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__)包含路徑區段。<br /> hello URI 配置太提供[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__)無效。 <br />hello 屬性值大於 32 KB。 |請檢查 hello 呼叫程式碼，並確定 hello 引數正確。 |重試將無助益。 |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |與 hello 作業相關聯的實體不存在或已遭刪除。 |請確定 hello 實體存在。 |重試將無助益。 |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |嘗試 tooreceive 訊息與特定的序號。 找不到此訊息。 |請確定沒有已收到 hello 訊息。 如果 hello 訊息已成為無效，請檢查 hello 無效信件佇列 toosee。 |重試將無助益。 |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |用戶端不是能 tooestablish 連接 tooService 匯流排。 |請確定 hello 提供主機名稱正確，且 hello 主機可連接。 |如果有間歇性的連線問題，重試也許有幫助。 |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |服務不能 tooprocess hello 要求這一次。 |用戶端可以等候一段時間，然後重試 hello 作業。 |用戶端可以在特定間隔後重試。 如果重試產生不同的例外狀況，請檢查該例外狀況的重試行為。 |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Hello 訊息相關聯的鎖定權杖已過期，或找不到 hello 鎖定權杖。 |處置 hello 訊息。 |重試將無助益。 |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |與此工作階段相關聯的鎖定遺失。 |中止 hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession)物件。 |重試將無助益。 |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |泛型訊息可能會在下列情況下的 hello 擲回的例外狀況：<br /> 嘗試 toocreate [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)使用所屬 tooa 不同的實體類型 （例如，主題） 的路徑或名稱。<br />  嘗試進行 toosend 訊息超過 256 KB。 hello 伺服器或服務處理 hello 要求時發生錯誤。 請 hello 例外狀況訊息，如需詳細資訊，參閱。 這通常是暫時性例外狀況。 |檢查 hello 程式碼，確保可序列化的物件會針對 hello 訊息內文 （或使用自訂序列化程式）。 請檢查 hello 和說明文件的 hello 支援實值類型的 hello 屬性只有使用支援型別。 檢查 hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient)屬性。 如果是**true**，您可以重試 hello 作業。 |重試行為未定義，而且可能沒有幫助。 |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |嘗試 toocreate 實體已由該服務命名空間中的另一個實體的名稱。 |刪除現有實體的 hello 或選擇 hello 實體 toobe 建立不同的名稱。 |重試將無助益。 |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |hello 訊息實體已達到其允許大小上限，或已超過 hello 連線 tooa 命名空間的最大數目。 |Hello 實體中建立空間，請從 hello 實體接收訊息或它的子佇列。 請參閱 [QuotaExceededException](#quotaexceededexception)。 |如果同時 hello 中已移除訊息，可能有助於重試。 |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |如果您嘗試 toocreate 無效的規則動作，服務匯流排會傳回這個例外狀況。 服務匯流排會附加此例外狀況 tooa 成為無效訊息，如果發生錯誤時正在處理該訊息的 hello 規則動作。 |請檢查 hello 規則動作的正確性。 |重試將無助益。 |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |服務匯流排會傳回這個例外狀況，如果您嘗試 toocreate 無效的篩選。 服務匯流排會附加此例外狀況 tooa 成為無效訊息，如果處理該訊息的 hello 篩選時發生錯誤。 |核取 hello 篩選條件的正確性。 |重試將無助益。 |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |嘗試的 tooaccept 由另一個用戶端目前鎖定的工作階段與特定的工作階段識別碼，但 hello 工作階段。 |請確定其他用戶端才能解除鎖定 hello 工作階段。 |如果已釋放 hello 工作階段中暫時 hello，可能有助於重試。 |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |太多的作業是 hello 交易的一部分。 |減少 hello 次數的作業，此交易的一部分。 |重試將無助益。 |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |在停用的實體上要求執行階段作業。 |啟動 hello 實體。 |如果已啟用 hello 實體 hello 過渡版中，可能有助於重試。 |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |如果您傳送的訊息 tooa 主題預先篩選已啟用，而且 hello 篩選器皆不符合，服務匯流排會傳回這個例外狀況。 |確定至少有一個篩選相符。 |重試將無助益。 |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |訊息內容超過 hello 256 KB 的限制。 請注意該 hello 256 KB 的限制是 hello 總訊息大小，也可以包含系統屬性和任何.NET 負擔。 |減少 hello 大小 hello 訊息內容，然後重試 hello 作業。 |重試將無助益。 |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |hello 環境交易 (*Transaction.Current*) 無效。 其可能已完成或中止。 內部例外狀況可能會提供其他資訊。 | |重試將無助益。 |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |交易處於不確定，請嘗試執行作業，或嘗試 toocommit hello 交易和 hello 交易才會變成有疑問。 |您的應用程式必須處理 （做為特殊案例），此例外狀況，如 hello 交易可能已經被認可。 |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 指出已超過某特定實體的配額。

### <a name="queues-and-topics"></a>佇列和主題
佇列和主題，這通常是 hello hello 佇列大小。 hello 錯誤訊息屬性將會包含進一步的詳細資訊，如 hello 下列範例所示：

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

hello 訊息，說明該 hello 主題超過其大小的限制，在此案例 1 GB （hello 預設大小限制）。 

### <a name="namespaces"></a>命名空間

命名空間， [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception)可能表示應用程式已超過 hello 連線 tooa 命名空間的數目上限。 例如：

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>常見的原因
有兩個常見的原因造成此錯誤： hello 寄不出信件佇列與非正常運作的訊息接收者。

1. **寄不出的信件佇列**toocomplete 訊息失敗的讀取器和 hello 訊息 hello 鎖定過期時傳回 toohello 佇列/主題。 這種情況 hello 讀取器遇到例外狀況，所以無法呼叫[BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx)。 讀取訊息 10 次之後，它會根據預設移動 toohello 寄不出的信件佇列。 此行為由 hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx)屬性且具有預設值是 10。 當訊息以免 hello 寄不出信件佇列中，它們會佔用空間。
   
    tooresolve hello 問題，請從 hello 寄不出信件佇列，當您讀取且完整的 hello 訊息會從任何其他佇列。 hello [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx)類別也包含[FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx)方法 toohelp 格式 hello 寄不出信件佇列路徑。
2. **收件者停止** ：收件者停止接收佇列或訂用帳戶的訊息。 hello 方式 tooidentify 這是在 hello toolook [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx)屬性，其中顯示 hello 完整分解的 hello 訊息。 如果 hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx)屬性為高或不斷增長，則 hello 訊息未以最快速度正在寫入讀取。

### <a name="event-hubs"></a>事件中樞
每一個事件中樞都有 20 個用戶群組的限制。 當您嘗試 toocreate 更多時，您會收到[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception)。 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)表示使用者啟動的作業花費的時間超過 hello 作業逾時。 

您應該檢查 hello hello 值[ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit)屬性，以達到這個限制可能也會導致[TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)。

### <a name="queues-and-topics"></a>佇列和主題
指定 hello 逾時的佇列和主題，有兩種 hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout)屬性，為一部分的 hello 連接字串，或透過[ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). hello 錯誤訊息本身可能不盡相同，但它一律包含 hello hello 目前作業指定的逾時值。 

### <a name="event-hubs"></a>事件中樞
事件中心 hello 逾時已指定做為部分 hello 連接字串，或透過[ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder)。 hello 錯誤訊息本身可能不盡相同，但它一律包含 hello hello 目前作業指定的逾時值。 

### <a name="common-causes"></a>常見的原因
這個錯誤有兩個常見的原因︰設定不正確或暫時性服務錯誤。

1. **不正確的設定**hello 作業逾時可能會太小 hello 操作條件。 hello hello hello client SDK 作業逾時的預設值為 60 秒。 檢查您的程式碼有 hello 值 toosee 設定 toosomething 太小。 請注意 hello 條件的 hello 網路和 CPU 使用量可能會影響 hello 花費的時間的特定作業 toocomplete，因此 hello 作業逾時不應該設定 tooa 非常小的值。
2. **暫時性服務錯誤**有時候 hello 服務匯流排服務可能會遇到延遲處理要求，例如高流量的期間。 在這種情況下，您可以重試您的作業的延遲之後，直到 hello 操作成功。 如果 hello 相同的作業仍失敗多次嘗試之後，請瀏覽 hello [Azure 服務狀態的站台](https://azure.microsoft.com/status/)toosee 是否有任何已知的服務中斷。

## <a name="next-steps"></a>後續步驟

Hello 完整的服務匯流排.NET API 參考，請參閱 hello [Azure.NET 應用程式開發介面參考](/dotnet/api/overview/azure/servicebus)。

深入了解 toolearn [Service Bus](https://azure.microsoft.com/services/service-bus/)，請參閱下列主題中的 hello。

* [服務匯流排訊息概觀](service-bus-messaging-overview.md)
* [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
* [服務匯流排架構](service-bus-architecture.md)

