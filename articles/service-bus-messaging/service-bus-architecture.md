---
title: "aaaAzure Service Bus 訊息處理架構概觀 |Microsoft 文件"
description: "描述 Azure 服務匯流排 hello 訊息處理架構。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>服務匯流排架構
本文說明的 Azure 服務匯流排 hello 訊息處理的架構。

## <a name="service-bus-scale-units"></a>服務匯流排縮放單位
服務匯流排依 *縮放單位*組織。 擴充單元是部署單位，並包含所有的元件所需執行的 hello 服務。 每個區域都會部署一或多個服務匯流排縮放單位。

服務匯流排命名空間是對應的 tooa 擴充單元。 hello 縮放單位會處理所有類型的服務匯流排實體 （佇列、 主題、 訂用帳戶）。 服務匯流排擴充單元包含下列元件的 hello:

* **一組閘道器節點。** 閘道節點會驗證傳入要求。 每個閘道器節點都有一個公用 IP 位址。
* **一組訊息代理程式節點。** 訊息代理程式節點會處理關於訊息實體的要求。
* **一個閘道器存放區。** hello 閘道存放區會保留此縮放單位會定義每個實體的 hello 資料。 SQL Azure 資料庫最上層，則實作 hello 閘道存放區。
* **多個訊息存放區。** 訊息存放區保留所有佇列、 主題和訂用帳戶在此縮放單位中定義的 hello 的訊息。 它也包含所有訂用帳戶資料。 除非[分割訊息實體](service-bus-partitioning.md)已啟用，佇列或主題是對應的 tooone 訊息存放區。 訂用帳戶會儲存在 hello 相同的訊息存放區做為其父主題。 除了服務匯流排[進階傳訊](service-bus-premium-messaging.md)，SQL Azure 資料庫上實作 hello 訊息存放區。

## <a name="containers"></a>容器
每個訊息實體都會指派給特定的容器。 容器是這個容器使用一個訊息存放區 toostore 所有相關資料的邏輯建構。 每個容器會指派 tooa 訊息代理人節點。 通常，容器較訊息代理程式節點多。 因此，每個訊息代理程式節點會載入多個容器。 容器 tooa 傳訊代理程式節點的 hello 發佈組織同樣會載入所有的訊息代理程式節點。 如果 hello hello 負載模式變更 （例如，一個 hello 容器取得非常忙碌），或訊息代理程式節點會變成暫時無法使用，容器會重新分配 hello 訊息代理程式節點。

## <a name="processing-of-incoming-messaging-requests"></a>處理內送訊息要求
當用戶端傳送要求 tooService 匯流排時，hello Azure 負載平衡器將其路由傳送 hello 閘道節點的 tooany。 hello 的 gateway 節點授權 hello 要求。 Hello 要求動作訊息實體 （佇列、 主題、 訂用帳戶），如果 hello 的 gateway 節點查閱 hello 閘道存放區中的 hello 實體，並判斷哪些訊息存放區 hello 中實體所在。 接著會尋找哪一個訊息代理人節點目前正在服務此容器，以及傳送嗨要求 toothat 訊息代理人節點。 hello 訊息代理人節點處理 hello 要求，並更新 hello hello 容器存放區中的實體狀態。 hello 訊息代理人節點，然後會傳送 hello 回應後 toohello 閘道 節點，該發行的 hello 原始要求傳送給適當的回應後 toohello 用戶端。

![處理內送訊息要求](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>後續步驟
既然您已閱讀 Service Bus 架構的概觀，請造訪下列連結以取得詳細資訊的 hello:

* [服務匯流排訊息概觀](service-bus-messaging-overview.md)
* [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
* [使用服務匯流排佇列的佇列訊息解決方案](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


