---
title: "aaaAzure 服務匯流排 Premium 和 Standard 傳訊定價層概觀 |Microsoft 文件"
description: "服務匯流排進階和標準傳訊層級"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>服務匯流排進階和標準傳訊層級

服務匯流排傳訊 (包含佇列和主題等實體) 結合雲端級別的企業傳訊功能與豐富的發佈-訂閱語意。 Service Bus 訊息作為 hello 通訊骨幹許多複雜的雲端解決方案。

hello *Premium*的 Service Bus 訊息層位址周圍小數位數、 效能和可用性的關鍵任務應用程式的一般客戶要求。 雖然 hello 功能集幾乎完全相同，但這些兩個 Service Bus 訊息層是設計的 tooserve 不同使用案例。

高層級的一些差異會在下表中的 hello 反白顯示。

| 進階 | 標準 |
| --- | --- |
| 高輸送量 |變動輸送量 |
| 可預測的效能 |變動延遲 |
| 固定價格 |隨用隨付變動價格 |
| 增加和減少的能力 tooscale 工作負載 |N/A |
| 向上 too1 MB 的訊息大小 |向上 too256 KB 的訊息大小 |

**Service Bus 高階訊息**提供資源隔離層級 hello CPU 和記憶體，以便在隔離狀態執行的每個客戶工作負載。 此資源容器稱為「傳訊單位」 。 每個進階命名空間都會被配置至少一個傳訊單位。 您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。 單一的工作負載或實體可以跨越多個傳訊單位，可在將變更 hello 傳訊單位數目，雖然計費是 24 小時或每日速率費用。 hello 結果是您 Service Bus 為基礎的解決方案的效能可預測且可重複。

此效能不僅更可預測並可取得，而且還更快速。 服務匯流排進階傳訊基礎 hello 儲存引擎中導入[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)。 使用進階傳訊，尖峰效能的速度比具有 hello 標準層。

## <a name="premium-messaging-technical-differences"></a>進階傳訊技術差異

hello 下列各節討論 Premium 和 Standard 傳訊層之間有一些差異。

### <a name="partitioned-queues-and-topics"></a>分割的佇列和主題

進階傳訊支援分割的佇列和主題；事實上這些實體一律會進行分割 (且無法停用)。 不過，Premium 分割佇列和主題不會運作 hello 相同的方式為 hello 標準和基本層的服務匯流排傳訊。 進階訊息未使用 SQL 做為資料存放區，且不再具有 hello 與共用的平台相關聯的可能的資源競爭。 如此一來，資料分割不是必要的 tooimprove 效能。 此外，已從標準傳訊 too2 資料分割在 Premium 中 16 個資料分割變更 hello 分割區計數。 擁有兩個資料分割可確保可用性，並是更適當的數字的 hello Premium 執行階段環境。 

使用進階傳訊，當您指定的實體與 hello 大小[MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes)，，大小被分割同樣 hello 2 的磁碟分割，不同於[標準分割實體](service-bus-partitioning.md#standard)中的 hello總大小是 16 hello 指定大小的時間。 

如需分割的詳細資訊，請參閱[分割的佇列和主題](service-bus-partitioning.md)。

### <a name="express-entities"></a>快速實體

因為進階傳訊是在完全隔離的執行階段環境中執行，所以在進階命名空間中並不支援快速實體。 如需 hello express 功能的詳細資訊，請參閱 hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress)屬性。

如果您有下執行標準的訊息，且想 tooport 它 toohello Premium 層的程式碼，請確定 hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress)屬性設定太**false** (hello 預設值)。

## <a name="get-started-with-premium-messaging"></a>開始使用進階傳訊

開始使用進階傳訊相當簡單，但 hello 程序類似 toothat 的傳訊標準。 首先[建立命名空間](service-bus-create-namespace-portal.md)。 請務必選取 [定價層] 之下的 [進階]。

![create-premium-namespace][create-premium-namespace]

您也可以[使用 Azure Resource Manager 範本建立進階命名空間](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/)。


## <a name="next-steps"></a>後續步驟

toolearn 有關 Service Bus 訊息的詳細資訊，請參閱下列主題中的 hello。

* [Azure 服務匯流排進階傳訊簡介 (部落格文章)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure 服務匯流排進階傳訊簡介 (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [服務匯流排訊息概觀](service-bus-messaging-overview.md)
* [如何 toouse 服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
