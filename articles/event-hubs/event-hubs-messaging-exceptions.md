---
title: "訊息例外狀況的 aaaAzure 事件中心 |Microsoft 文件"
description: "Azure 事件中樞傳訊例外狀況和建議的動作清單。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>事件中樞傳訊例外狀況
本文列出一些 hello hello Azure 服務匯流排所產生的例外狀況的訊息應用程式開發介面，其中包含事件中心。 這個參考是主體 toochange，因此稍後回來查看更新。

## <a name="exception-categories"></a>例外狀況類別
hello 事件中心 Api 產生可以分為下列類別目錄的 hello 的例外狀況，以及相關聯的 hello 動作中，您可以採取 tootry toofix 它們。

1. 使用者程式碼撰寫錯誤：[System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)、[System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx)、[System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx)、[System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)。 一般動作： 嘗試 toofix hello 程式碼，再繼續進行。
2. 設定/組態錯誤：[Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception)、[Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception)、[System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)。 一般動作：檢閱您的組態並視需要進行變更。
3. 暫時性例外狀況：[Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception)、[Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception)、[Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception)、[Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)。 一般動作： hello 作業重試一次，或通知使用者。
4. 其他例外狀況：[System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx)、[System.TimeoutException](#timeoutexception)、[Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception)、[Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)。 一般動作： 特定 toohello 例外狀況類型。請參閱 toohello hello 之後 > 一節中的資料表。 

## <a name="exception-types"></a>例外狀況類型
hello 下表列出訊息的例外狀況類型，其原因和附註您可以採取建議的動作。

| **例外狀況類型** | **描述/原因/範例** | **建議的動作** | **自動/立即重試附註** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |hello 伺服器未回應要求的 toohello hello 內的作業指定的時間，這由[OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout)。 hello 伺服器可能已完成 hello 要求的作業。 這種情形到期 toonetwork 或其他基礎結構延遲。 |檢查一致性的 hello 系統狀態，並視需要重試。<br /> 請參閱 [TimeoutException](#timeoutexception)。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |hello 要求 hello 伺服器或服務中不允許使用者操作。 請參閱 hello 例外狀況訊息，如需詳細資訊。 例如，[完成](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)會產生這個例外狀況，如果在收到 hello 訊息[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)模式。 |請檢查 hello 程式碼和 hello 文件。 請確定 hello 要求作業無效。 |重試將無助益。 |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |嘗試進行 tooinvoke 已經關閉、 中止或處置的物件上的作業。 在罕見的情況下，hello 環境交易已經過處置。 |請檢查 hello 程式碼，並確定它不會叫用已處置的物件上的作業。 |重試將無助益。 |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)物件無法取得驗證權杖、 hello 權杖無效，或 hello token 未包含 hello 宣告需要的 tooperform hello 作業。 |請確定 hello 權杖提供者會透過 hello 正確的值。 請檢查 hello hello 存取控制服務組態。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |一或多個引數提供 toohello 方法均為無效。 hello URI 提供太[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__)包含路徑區段。 hello URI 配置太提供[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__)無效。 hello 屬性值大於 32 KB。 |請檢查 hello 呼叫程式碼，並確定 hello 引數正確。 |重試將無助益。 |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |與 hello 作業相關聯的實體不存在或已遭刪除。 |請確定 hello 實體存在。 |重試將無助益。 |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |嘗試 tooreceive 訊息與特定的序號。 找不到此訊息。 |請確定沒有已收到 hello 訊息。 如果 hello 訊息已成為無效，請檢查 hello 無效信件佇列 toosee。 |重試將無助益。 |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |用戶端不是能 tooestablish 連接 tooEvent 中樞。 |請確定 hello 提供主機名稱正確，且 hello 主機可連接。 |如果有間歇性的連線問題，重試也許有幫助。 |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |服務不能 tooprocess hello 要求這一次。 |用戶端可以等候一段時間，然後重試 hello 作業。 <br /> 請參閱 [ServerBusyException](#serverbusyexception)。 |用戶端可以在特定間隔後重試。 如果重試產生不同的例外狀況，請檢查該例外狀況的重試行為。 |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Hello 訊息相關聯的鎖定權杖已過期，或找不到 hello 鎖定權杖。 |處置 hello 訊息。 |重試將無助益。 |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |與此工作階段相關聯的鎖定遺失。 | 中止 hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession)物件。 |重試將無助益。 |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |泛型訊息可能會在下列情況下的 hello 擲回的例外狀況： 嘗試 toocreate [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient)使用所屬 tooa 不同的實體類型 （例如，主題） 的路徑或名稱。 嘗試進行 toosend 訊息超過 256 KB。 hello 伺服器或服務處理 hello 要求時發生錯誤。 請 hello 例外狀況訊息，如需詳細資訊，參閱。 這通常是暫時性例外狀況。 |檢查 hello 程式碼，確保可序列化的物件會針對 hello 訊息內文 （或使用自訂序列化程式）。 請檢查 hello 和說明文件的 hello 支援實值類型的 hello 屬性只有使用支援型別。 檢查 hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient)屬性。 如果是**true**，您可以重試 hello 作業。 |重試行為未定義，而且可能沒有幫助。 |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |嘗試 toocreate 實體已由該服務命名空間中的另一個實體的名稱。 |刪除現有實體的 hello 或選擇 hello 實體 toobe 建立不同的名稱。 |重試將無助益。 |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |hello 訊息實體已達到其最大容許大小。 如果在每個取用者群組層級的 hello 的數目上限接收器 （其為 5） 已開啟，也可能會發生。 |Hello 實體中建立空間，請從 hello 實體接收訊息或它的子佇列。 <br /> 請參閱 [QuotaExceededException](#quotaexceededexception) |如果同時 hello 中已移除訊息，可能有助於重試。 |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |嘗試的 tooaccept 由另一個用戶端目前鎖定的工作階段與特定的工作階段識別碼，但 hello 工作階段。 |請確定其他用戶端才能解除鎖定 hello 工作階段。 |如果已釋放 hello 工作階段中暫時 hello，可能有助於重試。 |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |太多的作業是 hello 交易的一部分。 |減少 hello 次數的作業，此交易的一部分。 |重試將無助益。 |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |在停用的實體上要求執行階段作業。 |啟動 hello 實體。 |如果已啟用 hello 實體 hello 過渡版中，可能有助於重試。 |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | 訊息內容超過 hello 256k 限制。 請注意該 hello 256k 限制是 hello 總訊息大小，也可以包含系統屬性和任何.NET 負擔。 |減少 hello 大小 hello 訊息內容，然後重試 hello 作業。 |重試將無助益。 |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |hello 環境交易 (*Transaction.Current*) 無效。 其可能已完成或中止。 內部例外狀況可能會提供其他資訊。 | |重試將無助益。 |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |交易處於不確定，請嘗試執行作業，或嘗試 toocommit hello 交易和 hello 交易才會變成有疑問。 |您的應用程式必須處理 （做為特殊案例），此例外狀況，如 hello 交易可能已經被認可。 |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 指出已超過某特定實體的配額。

這種情況在每個取用者群組層級已經開啟 hello 接收者 (5) 的數目上限。

### <a name="event-hubs"></a>事件中樞
每一個事件中樞都有 20 個用戶群組的限制。 當您嘗試 toocreate 更多時，您會收到[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception)。 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)表示使用者啟動的作業花費的時間超過 hello 作業逾時。 

事件中心 hello 逾時已指定做為部分 hello 連接字串，或透過[ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder)。 hello 錯誤訊息本身可能不盡相同，但它一律包含 hello hello 目前作業指定的逾時值。 

### <a name="common-causes"></a>常見的原因
這個錯誤有兩個常見的原因︰設定不正確或暫時性服務錯誤。

1. **不正確的設定**hello 作業逾時可能會太小 hello 操作條件。 hello hello hello client SDK 作業逾時的預設值為 60 秒。 檢查您的程式碼有 hello 值 toosee 設定 toosomething 太小。 請注意 hello 條件的 hello 網路和 CPU 使用量可能會影響 hello 花費的時間的特定作業 toocomplete，因此 hello 作業逾時不應該設定 tooa 非常小的值。
2. **暫時性服務錯誤**有時候 hello 事件中心服務可能會遇到延遲處理要求，例如高流量的期間。 在這種情況下，您可以重試您的作業的延遲之後，直到 hello 操作成功。 如果 hello 相同的作業仍失敗多次嘗試之後，請瀏覽 hello [Azure 服務狀態的站台](https://azure.microsoft.com/status/)toosee 是否有任何已知的服務中斷。

## <a name="serverbusyexception"></a>ServerBusyException

[Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) 或 [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) 表示伺服器已超載。 此例外狀況有兩個相關的錯誤碼。

### <a name="error-code-50002"></a>錯誤碼 50002

此錯誤會因為兩個原因其中之一而發生：

1. hello 負載未平均分佈的所有資料分割上 hello 事件中心和一個分割區點擊 hello 本機輸送量單位限制。
    
    解決方式： Hello 分割區散發策略的修訂，或嘗試[EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_)可以幫助。

2. hello 事件中樞命名空間沒有足夠的輸送量單位 (您可以檢查 hello**度量**刀鋒視窗中的事件中樞命名空間 刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)tooconfirm)。 請注意，hello 入口網站會顯示彙總 （1 分鐘） 的詳細資訊，我們會測量即時 – hello 輸送量，所以只是估計值。

    解決方法： 增加 hello 輸送量單位 hello 命名空間上的可以幫助。 您可以在 hello 入口網站，在 hello**標尺**刀鋒視窗中的 hello 事件中樞命名空間 刀鋒視窗。

### <a name="error-code-50001"></a>錯誤碼 50001

此錯誤應該很少會發生。 它會發生在 CPU 上執行您的命名空間的程式碼的 hello 容器不足 – 不能超過幾秒鐘的時間之前 hello 事件中心負載平衡器開始。


## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)
