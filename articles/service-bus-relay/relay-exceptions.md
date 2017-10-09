---
title: "aaaAzure 轉送例外狀況以及 tooresolve 它們 |Microsoft 文件"
description: "取得 Azure 轉送例外狀況的清單，並建議的動作，您可以採取 toohelp 加以解決。"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Azure 轉送例外狀況

本文列出一些 hello Azure 轉送 Api 可能會產生的例外狀況。 這個參考是主體 toochange，因此稍後回來查看更新。

## <a name="exception-categories"></a>例外狀況類別

hello 轉送 Api 產生，可能會分成下列類別目錄的 hello 的例外狀況。 也列出建議的動作，您可以採取 toohelp 解析 hello 例外狀況。

*   **使用者程式碼撰寫錯誤**：[System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)、[System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx)、[System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx)、[System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)。 

    **一般動作**： 在您繼續之前，請嘗試 toofix hello 程式碼。
*   **設定/組態錯誤**：[System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)。 

    **一般動作**：檢閱您的組態。 如有必要，變更 hello 組態。
*   **暫時性例外狀況**：[Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception)、[Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)、[Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)。 

    **一般動作**: hello 作業重試一次，或通知使用者。
*   **其他例外狀況**：[System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx)、[System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)。 

    **一般動作**： 特定 toohello 例外狀況類型。 請參閱 hello 之後 > 一節中的 hello 資料表。 

## <a name="exception-types"></a>例外狀況類型

hello 下表列出訊息例外狀況類型和其原因。 它也會註您可以採取 toohelp 解析 hello 例外狀況的建議的動作。

| **例外狀況類型** | **說明** | **建議動作** | **自動或立即重試附註** |
| --- | --- | --- | --- |
| [逾時](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |hello 伺服器未回應要求的 toohello hello 內的作業指定的時間，這由[OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout)。 hello 伺服器可能已完成的 hello 要求的作業。 這種情形到期 toonetwork 或其他基礎結構延遲。 |檢查 hello 系統狀態的一致性，並重試，如有必要。 請參閱 [TimeoutException](#timeoutexception)。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [作業無效](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |hello 要求 hello 伺服器或服務中不允許使用者操作。 請參閱 hello 例外狀況訊息，如需詳細資訊。 |請檢查 hello 程式碼和 hello 文件。 請確定該 hello 要求作業無效。 |重試將無助益。 |
| [已取消作業](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |嘗試進行 tooinvoke 已經關閉、 中止或處置的物件上的作業。 在罕見的情況下，hello 環境交易已經過處置。 |請檢查 hello 程式碼，並確定它不會叫用已處置的物件上的作業。 |重試將無助益。 |
| [未經授權的存取](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider)物件無法取得驗證權杖、 hello 權杖無效，或 hello token 未包含 hello 宣告需要的 tooperform hello 作業。 |請確定該 hello 權杖提供者會透過 hello 正確的值。 請檢查 hello hello 存取控制服務組態。 |重試可能有助於在某些情況下。加入重試邏輯 toocode。 |
| [引數例外狀況](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [引數 Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[引數超出範圍](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |發生一個或多個 hello 下列：<br />一或多個引數提供 toohello 方法均為無效。<br /> hello URI 提供太[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create)包含一或多個路徑區段。<br />hello URI 配置太提供[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)或[建立](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create)無效。 <br />hello 屬性值大於 32 KB。 |請檢查 hello 呼叫程式碼，並確定 hello 引數正確。 |重試將無助益。 |
| [伺服器忙碌](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |服務不能 tooprocess hello 要求這一次。 |hello 用戶端可以等候一段時間，然後重試 hello 作業。 |hello 用戶端可能會以特定間隔後重試。 如果重試會導致不同的例外狀況，請檢查該例外狀況的 hello 重試行。 |
| [超過配額](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |hello 訊息實體已達到其最大容許大小。 |Hello 實體中建立空間，請從 hello 實體接收訊息或它的子佇列。 請參閱 [QuotaExceededException](#quotaexceededexception)。 |如果同時 hello 中已移除訊息，可能有助於重試。 |
| [超過訊息大小](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |訊息內容超過 hello 256 KB 的限制。 請注意該 hello 256 KB 的限制是 hello 訊息總大小。 系統屬性和任何 Microsoft.NET 負擔，可以包含 hello 訊息總大小。 |減少 hello 大小 hello 訊息內容，然後重試 hello 作業。 |重試將無助益。 |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) 指出已超過某特定實體的配額。

轉送，這個例外狀況會包裝 hello [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx)，表示該 hello 數目上限的接聽程式已超過為此端點。 這表示在 hello **MaximumListenersPerEndpoint** hello 例外狀況訊息的值。

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)表示使用者啟動的作業花費的時間超過 hello 作業逾時。 

檢查 hello hello 值[ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit)屬性。 達到此限制也會導致 [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)。

若為轉送，您可能會在第一次開啟轉送傳送者連線時收到逾時例外狀況。 這個例外狀況有兩個常見的原因︰

*   hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx)值可能會太小 （如果即使的小數秒數）。
* 在內部部署轉送接聽程式可能會沒有回應 （或它可能會遇到禁止接聽程式接受新用戶端連線的防火牆規則問題），和 hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx)值是不超過約 20 秒。

範例：

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>常見的原因
這個錯誤有兩個常見的原因︰

*   **組態不正確**
    
    hello 作業逾時可能會太小，hello 操作條件。 hello hello hello client SDK 作業逾時的預設值為 60 秒。 您的程式碼中的 hello 值設定 toosomething 太小，請檢查 toosee。 請注意，CPU 使用量和 hello 條件 hello 網路可能會影響 hello 作業 toocomplete 所花費的時間。 它是個不錯的主意不 tooset hello 作業逾時 tooa 非常小的值。
*   **暫時性服務錯誤**

    有時候，hello 轉送服務可能會遇到延遲處理要求。 例如，這可能會在高流量期間發生。 如果發生這種情況，並重試作業的延遲之後，直到 hello 操作是否成功。 如果 hello 相同作業仍會繼續 toofail 多次嘗試之後，請檢查 hello [Azure 服務狀態的站台](https://azure.microsoft.com/status/)toosee 如果那里已知的服務中斷。

## <a name="next-steps"></a>後續步驟
* [Azure 轉送常見問題集](relay-faq.md)
* [建立轉送命名空間](relay-create-namespace-portal.md)
* [開始使用 Azure 轉送和 .NET](relay-hybrid-connections-dotnet-get-started.md)
* [開始使用 Azure 轉送和節點](relay-hybrid-connections-node-get-started.md)

