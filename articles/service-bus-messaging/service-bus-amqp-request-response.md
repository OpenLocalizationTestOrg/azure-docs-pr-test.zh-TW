---
title: "Azure 服務匯流排要求-回應為基礎的作業中 aaaAMQP 1.0 |Microsoft 文件"
description: "Microsoft Azure 服務匯流排要求/回應架構作業的清單。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>Microsoft Azure 服務匯流排中的 AMQP 1.0：要求/回應架構作業

本主題會定義 Microsoft Azure 服務匯流排要求/回應架構作業 hello 清單。 這項資訊根據 hello AMQP 管理版本 1.0 工作草稿。  
  
詳細的有線等級 AMQP 1.0 通訊協定指引，其中說明如何實作服務匯流排，和 hello OASIS AMQP 技術規格為基礎，請參閱 hello [Azure 服務匯流排和事件中心的通訊協定指南中的 AMQP 1.0](service-bus-amqp-protocol-guide.md)。  
  
## <a name="concepts"></a>概念  
  
### <a name="entity-description"></a>實體描述  

實體描述是指 Service Bus tooeither [QueueDescription 類別](/dotnet/api/microsoft.servicebus.messaging.queuedescription)， [TopicDescription 類別](/dotnet/api/microsoft.servicebus.messaging.topicdescription)，或[SubscriptionDescription 類別](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription)物件。  
  
### <a name="brokered-message"></a>代理訊息  

表示服務匯流排，也就是對應的 tooan AMQP 訊息中的訊息。 hello 對應定義於 hello[服務匯流排 AMQP 通訊協定指南](service-bus-amqp-protocol-guide.md)。  
  
## <a name="attach-tooentity-management-node"></a>附加 tooentity 管理節點  

這份文件中所述的所有 hello 作業會遵循要求/回應模式，已設定領域的 tooan 實體，但需要附加 tooan 實體管理節點。  
  
### <a name="create-link-for-sending-requests"></a>建立傳送要求的連結  

建立傳送要求的連結 toohello 管理節點。  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>建立接收回應的連結  

建立接收回應從 hello 管理節點的連結。  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>傳輸要求訊息  

傳輸要求訊息。  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>接收回應訊息  

接收來自 hello 回應連結 hello 回應訊息。  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
hello 回應訊息處於下列表單的 hello:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>服務匯流排實體位址  

必須處理服務匯流排實體，如下所示︰  
  
|實體類型|位址|範例|  
|-----------------|-------------|-------------|  
|佇列|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|主題|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|訂用帳戶|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>訊息作業  
  
### <a name="message-renew-lock"></a>訊息更新鎖定  

延伸 hello 鎖定訊息的 hello hello 實體描述中指定的時間。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
 以下列項目 hello 含有對應的 amqp 值區段必須包含 hello 要求訊息內文：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|UUID 的陣列|是|訊息鎖定權杖 toorenew。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗。|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
以下列項目 hello 含有對應的 amqp 值區段必須包含 hello 回應訊息內文：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|到期日|時間戳記的陣列|是|訊息鎖定權杖新到期對應 toohello 要求鎖定權杖。|  
  
### <a name="peek-message"></a>查看訊息  

查看訊息而不用鎖定。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|long|是|從哪些 toostart 查看的序號。|  
|`message-count`|int|是|訊息 toopeek 的數目上限。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 有多個訊息<br /><br /> 0xcc︰沒有內容 – 沒有其他訊息|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|上限|對應的清單|是|當中每個對應都代表一則訊息的訊息清單。|  
  
hello 對應表示訊息必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|訊息|位元組的陣列|是|AMQP 1.0 連線編碼訊息。|  
  
### <a name="schedule-message"></a>排程訊息  

排程訊息。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|上限|對應的清單|是|當中每個對應都代表一則訊息的訊息清單。|  
  
hello 對應表示訊息必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|message-id|字串|是|`amqpMessage.Properties.MessageId` 為字串|  
|session-id|string|是|`amqpMessage.Properties.GroupId as string`|  
|partition-key|字串|是|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|訊息|位元組的陣列|是|AMQP 1.0 連線編碼訊息。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗。|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|長整數的陣列|是|排定訊息的序號。 序號是使用的 toocancel。|  
  
### <a name="cancel-scheduled-message"></a>取消排定的訊息  

取消排定的訊息。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|長整數的陣列|是|排定的訊息 toocancel 順序編號。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗。|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|長整數的陣列|是|排定訊息的序號。 序號是使用的 toocancel。|  
  
## <a name="session-operations"></a>工作階段作業  
  
### <a name="session-renew-lock"></a>工作階段更新鎖定  

延伸 hello 鎖定訊息的 hello hello 實體描述中指定的時間。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|session-id|string|是|工作階段識別碼。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 有多個訊息<br /><br /> 0xcc︰沒有內容 – 沒有其他訊息|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|expiration|timestamp|是|新的到期日。|  
  
### <a name="peek-session-message"></a>查看工作階段訊息  

查看工作階段訊息而不用鎖定。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|long|是|從哪些 toostart 查看的序號。|  
|message-count|int|是|訊息 toopeek 的數目上限。|  
|session-id|string|是|工作階段識別碼。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 有多個訊息<br /><br /> 0xcc︰沒有內容 – 沒有其他訊息|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|上限|對應的清單|是|當中每個對應都代表一則訊息的訊息清單。|  
  
 hello 對應表示訊息必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|訊息|位元組的陣列|是|AMQP 1.0 連線編碼訊息。|  
  
### <a name="set-session-state"></a>設定工作階段狀態  

設定 hello 工作階段狀態。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|session-id|string|是|工作階段識別碼。|  
|session-state|位元組的陣列|是|不透明的二進位資料。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
### <a name="get-session-state"></a>取得工作階段狀態  

取得工作階段的 hello 狀態。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|session-id|string|是|工作階段識別碼。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|session-state|位元組的陣列|是|不透明的二進位資料。|  
  
### <a name="enumerate-sessions"></a>列舉工作階段  

列舉訊息實體上的工作階段。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|是|篩選 tooinclude 唯一工作階段指定的時間之後更新。|  
|skip|int|是|略過工作階段數。|  
|top|int|是|工作階段數上限。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 有多個訊息<br /><br /> 0xcc︰沒有內容 – 沒有其他訊息|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|skip|int|是|如果狀態碼為 200 所略過的工作階段數。|  
|sessions-ids|字串的陣列|是|如果狀態碼為 200 的工作階段識別碼陣列。|  
  
## <a name="rule-operations"></a>規則作業  
  
### <a name="add-rule"></a>新增規則  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|rule-name|字串|是|規則名稱，不包括訂用帳戶和主題名稱。|  
|rule-description|map|是|如下一節中指定的規則描述。|  
  
hello**規則描述**地圖必須包含下列項目，hello 其中**sql 篩選**和**相互關聯篩選**互斥：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|是|`sql-filter`hello 下一節中所指定。|  
|correlation-filter|map|是|`correlation-filter`hello 下一節中所指定。|  
|sql-rule-action|map|是|`sql-rule-action`hello 下一節中所指定。|  
  
hello sql 篩選地圖必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|expression|字串|是|Sql 篩選運算式。|  
  
hello**相互關聯篩選**地圖必須包含至少其中一個 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|correlation-id|字串|否||  
|message-id|字串|否||  
|to|字串|否||  
|reply-to|string|否||  
|標籤|string|否||  
|session-id|string|否||  
|reply-to-session-id|string|否||  
|Content-Type|字串|否||  
|properties|map|否|對應 tooService 匯流排[BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)。|  
  
hello **sql 規則動作**地圖必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|expression|字串|是|Sql 動作運算式。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
### <a name="remove-rule"></a>移除規則  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|rule-name|字串|是|規則名稱，不包括訂用帳戶和主題名稱。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
## <a name="deferred-message-operations"></a>延遲的訊息作業  
  
### <a name="receive-by-sequence-number"></a>依照序號接收  

依序號接收延遲的訊息。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|長整數的陣列|是|序號。|  
|receiver-settle-mode|ubyte|是|AMQP 核心 1.0 版中所指定的「收件者支付」模式。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|  
  
hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|上限|對應的清單|是|當中每個對應都代表一則訊息的訊息清單。|  
  
hello 對應表示訊息必須包含下列項目 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|是|如果 `receiver-settle-mode` 為 1 則鎖定權杖。|  
|訊息|位元組的陣列|是|AMQP 1.0 連線編碼訊息。|  
  
### <a name="update-disposition-status"></a>更新配置狀態  

更新 hello 配置狀態延後的訊息。  
  
#### <a name="request"></a>要求  

hello 要求訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|operation|字串|是|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|否|作業伺服器逾時以毫秒為單位。|  
  
hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|是|完成<br /><br /> 放棄<br /><br /> 暫止|  
|lock-tokens|UUID 的陣列|是|訊息鎖定權杖 tooupdate 配置狀態。|  
|deadletter-reason|字串|否|如果設定太配置狀態可能會設定**暫停**。|  
|deadletter-description|字串|否|如果設定太配置狀態可能會設定**暫停**。|  
|properties-to-modify|map|否|清單中的服務匯流排代理訊息屬性 toomodify。|  
  
#### <a name="response"></a>Response  

hello 回應訊息必須包含下列應用程式屬性的 hello:  
  
|Key|值類型|必要|值內容|  
|---------|----------------|--------------|--------------------|  
|StatusCode|int|是|HTTP 回應碼 [RFC2616]<br /><br /> 200：確定 – 成功，否則失敗|  
|statusDescription|字串|否|Hello 狀態的描述。|

## <a name="next-steps"></a>後續步驟

深入了解 AMQP 和 Service Bus toolearn 請造訪下列連結查看 hello:

* [服務匯流排 AMQP 概觀]
* [適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]
* [Windows Server 服務匯流排中的 AMQP]

[服務匯流排 AMQP 概觀]: service-bus-amqp-overview.md
[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.asp