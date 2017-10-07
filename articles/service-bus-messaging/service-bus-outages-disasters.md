---
title: "aaaInsulating Azure 服務匯流排應用程式，避免中斷和嚴重損壞 |Microsoft 文件"
description: "描述您可以使用 tooprotect 應用程式，避免潛在的服務匯流排中斷的技術。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>將應用程式與服務匯流排中斷和災難隔絕的最佳做法
關鍵任務應用程式必須持續作業，即使在未計劃的中斷或災害 hello 存在。 本主題描述您可以使用 tooprotect 服務匯流排應用程式，避免造成服務中斷或災害的技術。

中斷的定義是作為 Azure 服務匯流排 hello 暫時無法使用。 hello 中斷可能會影響服務匯流排的某些元件，例如訊息存放區或甚至 hello 整個資料中心。 已修正 hello 問題之後，服務匯流排再次變為無法使用。 中斷通常不會導致訊息或其他資料遺失。 元件失敗的範例是 hello 無法使用特定的訊息存放區。 在全資料中心中斷的範例是停電 hello 資料中心，或錯誤的資料中心網路交換器。 中斷可能持續數分鐘 tooa 幾天。

災害的定義是服務匯流排擴充單元或資料中心的 hello 永久遺失。 hello 資料中心可能會或可能不會變成可用一次。 災害通常會造成部分或所有訊息或其他資料遺失。 災害的範例包括火災、水災或地震。

## <a name="current-architecture"></a>目前架構
服務匯流排也使用 tooqueues 或主題傳送的多個訊息存放區 toostore 訊息。 非資料分割的佇列或主題會指派 tooone 訊息存放區。 如果此訊息存放區無法使用，該佇列或主題上的所有作業都會失敗。

所有服務匯流排訊息實體 (佇列、主題、轉送) 都位於附屬於資料中心的服務命名空間中。 Service Bus 不會啟用自動複寫地理資料，也不允許命名空間 toospan 多個資料中心。

## <a name="protecting-against-acs-outages"></a>保護 ACS 免於中斷
如果您使用 ACS 認證，ACS 會無法使用，用戶端也無法再取得權杖。 在 ACS 中斷 hello 時擁有權杖的用戶端可以繼續 toouse 服務匯流排，直到 hello 權杖到期。 hello 權杖存留期為 3 小時。

tooprotect ACS 免於中斷，請使用共用存取簽章 (SAS) 權杖。 在此情況下，hello 用戶端直接與 Service Bus 驗證與秘密金鑰簽署自行產生的語彙基元。 呼叫 tooACS 不再需要。 如需有關 SAS 權杖的詳細資訊，請參閱[服務匯流排驗證][Service Bus authentication]。

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>保護佇列和主題免於發生訊息存放區失敗
非資料分割的佇列或主題會指派 tooone 訊息存放區。 如果此訊息存放區無法使用，該佇列或主題上的所有作業都會失敗。 A 進行資料分割的佇列，請在 hello 另一方面，包含多個片段。 每個片段都儲存在不同的訊息存放區。 當訊息傳送 tooa 分割的佇列或主題時，服務匯流排會指派 hello 訊息 tooone 的 hello 片段。 Hello 對應的訊息存放區無法使用時，服務匯流排盡可能寫入 hello 訊息 tooa 不同的片段。 如需分割實體的詳細資訊，請參閱[分割的傳訊實體][Partitioned messaging entities]。

## <a name="protecting-against-datacenter-outages-or-disasters"></a>保護資料中心免於中斷或災害
tooallow 兩個資料中心之間的容錯移轉，您可以在每個資料中心內建立服務匯流排服務命名空間。 例如，hello 服務匯流排服務命名空間**contosoPrimary.servicebus.windows.net**可能位於 hello 美國北部/中部地區，以及**contosoSecondary.servicebus.windows.net**可能位於 hello 美國南部/中部地區。 如果服務匯流排訊息實體必須保持在 hello 出現在資料中心中斷中存取，您可以在兩個命名空間中建立該實體。

如需詳細資訊，請參閱 「 Azure 資料中心中的服務匯流排失敗 」 一節中的 hello[非同步訊息模式和高可用性][Asynchronous messaging patterns and high availability]。

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>保護轉送端點免於發生資料中心中斷或災害
轉送端點的地理複寫可讓您公開轉送端點 toobe 在 hello 存在的服務匯流排中斷連線的服務。 tooachieve 異地複寫，hello 服務必須在不同的命名空間中建立兩個轉送端點。 hello 命名空間必須位於不同的資料中心和 hello 兩個端點必須具有不同的名稱。 比方說，主要端點在 **contosoPrimary.servicebus.windows.net/myPrimaryService** 之下達到，而其次要的對應項目可以在 **contosoSecondary.servicebus.windows.net/mySecondaryService** 之下達到。

hello 服務接著會接聽這兩個端點，並且需要透過任一端點的 hello 服務叫用用戶端。 用戶端應用程式隨機挑選其中一個 hello 轉送，因為 hello 主要端點，並傳送其要求 toohello 主動端點。 如果 hello 作業失敗並出現錯誤代碼，此失敗表示該 hello 轉送端點無法使用。 hello 應用程式會開啟通道 toohello 備份端點，並重新發出 hello 要求。 在該點作用中的 hello 和 hello 備份端點會互換角色： hello 用戶端應用程式將視 hello 舊的主動端點 toobe hello 新的備份端點，而舊備份端點 toobe hello hello 新的主動端點。 如果兩個傳送作業失敗，hello 角色 hello 兩個實體都維持不變，則會傳回錯誤。

hello[地理複寫具有服務匯流排轉送訊息][ Geo-replication with Service Bus relayed Messages]範例會示範如何將 tooreplicate 轉送。

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>保護佇列和主題免於發生資料中心中斷或災害
針對資料中心中斷時使用代理傳訊 tooachieve 恢復功能，服務匯流排支援兩種方法： *active*和*被動*複寫。 每個方法，如果給定的佇列或主題必須保持可存取在 hello 出現在資料中心中斷，您可以建立它在這兩個命名空間中。 這兩個實體可以具有 hello 相同的名稱。 比方說，主要佇列在 **contosoPrimary.servicebus.windows.net/myQueue** 之下達到，而其次要的對應項目可以在 **contosoSecondary.servicebus.windows.net/myQueue** 之下達到。

如果 hello 應用程式不需要永久的傳送者與接收者通訊，hello 應用程式可以實作長期的用戶端佇列 tooprevent 訊息遺失和 tooshield hello 寄件者的任何暫時性的服務匯流排錯誤。

## <a name="active-replication"></a>主動複寫
主動複寫會針對每個作業使用兩個命名空間中的實體。 將訊息傳送的任何用戶端會傳送 hello 的兩份相同的訊息。 hello 第一次複製傳送 toohello 主要實體 (例如， **contosoPrimary.servicebus.windows.net/sales**)，且 toohello 次要實體會傳送 hello 第二個副本 hello 訊息 (比方說， **contosoSecondary.servicebus.windows.net/sales**)。

用戶端會從這兩個佇列接收訊息。 hello 接收者處理程序 hello 第一個訊息的複本，並隱藏 hello 第二個副本。 toosuppress 重複的訊息，hello 寄件者必須標記每個訊息具有唯一識別碼。 Hello hello 訊息的兩個複本必須標記相同的識別項。 您可以使用 hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId]或[BrokeredMessage.Label] [ BrokeredMessage.Label]屬性或使用自訂屬性 tootag hello訊息。 hello 接收者必須維護它已經收到的訊息清單。

hello[地理複寫使用服務匯流排代理訊息][ Geo-replication with Service Bus Brokered Messages]範例將示範傳訊實體的作用中複寫。

> [!NOTE]
> hello 主動複寫方法會讓 hello 作業數目加倍，因此這種方法可能會導致 toohigher 成本。
> 
> 

## <a name="passive-replication"></a>被動複寫
在 hello 無錯誤的情況下，被動複寫會使用其中一個 hello 兩個訊息實體。 用戶端會傳送 hello 訊息 toohello 主動實體。 如果 hello hello 主動實體作業失敗錯誤碼，指出 hello 主機 hello 主動實體可能會無法使用的資料中心，hello 用戶端會傳送 hello 訊息 toohello 備份實體的複本。 在該點作用中的 hello 和 hello 備份實體會互換角色： hello 傳送用戶端會考慮 hello 舊主動實體 toobe hello 新的備份實體，而且 hello 舊的備份實體 hello 新的主動實體。 如果兩個傳送作業失敗，hello 角色 hello 兩個實體都維持不變，則會傳回錯誤。

用戶端會從這兩個佇列接收訊息。 因為沒有機會該 hello 接收者收到兩份相同訊息、 hello hello 接收者必須抑制重複的訊息。 您可以隱藏重複項目在 hello 方式所述相同的作用中複寫。

一般而言，被動複寫比主動複寫更具經濟效益，因為大部分的情形只會執行一項作業。 延遲、 輸送量和貨幣成本會與相同 toohello 非複寫案例。

使用被動複寫時，在 hello 下列案例訊息可能遺失或收到兩次：

* **訊息延遲或遺失**： 假設 hello 寄件者已成功傳送訊息 m1 toohello 主要佇列，並再 hello 佇列變得無法使用 hello 接收者接收 m1 之前。 hello 寄件者會傳送後續訊息 m2 toohello 次要佇列。 如果 hello 主要佇列暫時無法使用，hello 接收者 hello 佇列再次可用後，就會收到 m1。 萬一發生災害，hello 接收者可能不會收到 m1。
* **重複接收**： 假設該 hello 寄件者傳送訊息 m toohello 主要佇列。 服務匯流排成功處理 m，但失敗 toosend 回應。 Hello 傳送作業逾時之後，hello 寄件者會傳送一份完全相同 m toohello 次要佇列。 如果 hello 接收者可以 tooreceive hello 第一份 m hello 主要佇列變成無法使用之前，hello 接收者收到兩份 m 大約 hello 在相同的時間。 如果 hello 接收者不能 tooreceive hello 第一份 m hello 主要佇列變成無法使用之前，hello 接收者一開始會收到僅 hello 第二個複本 m，但 hello 主要佇列再次可用時就會接收第二份 m。

hello[地理複寫具有服務匯流排代理訊息][ Geo-replication with Service Bus Brokered Messages]範例將示範傳訊實體的被動複寫。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解災害復原，請參閱下列文章：

* [Azure SQL Database 商務持續性][Azure SQL Database Business Continuity]
* [為 Azure 設計有彈性的應用程式][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
