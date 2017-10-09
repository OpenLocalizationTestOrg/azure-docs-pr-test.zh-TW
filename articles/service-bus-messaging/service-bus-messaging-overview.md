---
title: "aaaAzure 服務匯流排傳訊概觀 |Microsoft 文件"
description: "描述服務匯流排傳訊與 Azure 轉送"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Service Bus 訊息： hello 雲端中的彈性資料傳遞
Microsoft Azure 服務匯流排是一項可靠的資訊傳遞服務。 此服務的 hello 目的是 toomake 通訊更容易。 當兩個或多個合作對象想 tooexchange 資訊時，他們需要通訊促進。 服務匯流排是一項代理通訊機制或第三方通訊機制。 這是在 hello 現實生活中的類似 tooa 郵遞服務。 郵遞服務很容易 toosend 各種不同的字母和封裝名稱中有各種不同的傳遞保證的任何位置中容易 hello world。

類似 toohello 郵遞服務傳送字母、 Service Bus 是有彈性的資訊傳遞從 hello 寄件者和 hello 收件者。 hello 訊息服務可確保即使 hello 兩個合作對象永遠不會同時上線在相同的時間，或如果不是位於 hello 完全相同的 hello，傳送嗨資訊的時間。 如此一來，訊息是類似 toosending 字母，而非代理通訊是類似 tooplacing 撥打電話 （或電話使用 toobe-之前呼叫等待，呼叫者識別碼，也就是較像代理訊息的方式）。

hello 訊息寄件者也可以要求不同的傳遞特性包括交易、 重複偵測、 以時間為基礎的到期日和批次處理。 這些模式也具備類似郵遞服務的特性：重複傳遞、需要簽名、地址變更或回收。

服務匯流排支援兩種不同的傳訊模式：「Azure 轉送」和「服務匯流排傳訊」。

## <a name="azure-relay"></a>Azure 轉送
hello [WCF 轉送](../service-bus-relay/relay-what-is-it.md)Azure 轉送的元件是集中式 （但高度負載平衡） 服務，可支援各種不同的傳輸通訊協定和 Web 服務標準。 這包括 SOAP、WS-*，甚至是 REST。 hello[轉送服務](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)提供各種不同的轉送連線功能選項，可以協助交涉直接的對等連線時，它會。 服務匯流排最佳化使用 Windows Communication Foundation (WCF)，同時考慮 tooperformance 和可用性，與 hello 的.NET 開發人員，並提供完整存取 tooits 轉送服務，透過 SOAP 和 REST 介面。 這可讓所有 SOAP 或 REST 程式設計環境 toointegrate 具有服務匯流排。

hello 轉送服務支援傳統單向訊息、 要求/回應訊息，以及對等端對端訊息。 它也支援事件發佈在網際網路範圍 tooenable 發行-訂閱案例和雙向通訊端通訊，以提高的點對點效率。 在 hello 轉送訊息模式中，在內部部署服務連接 toohello 轉送服務，透過輸出連接埠，並建立繫結的通訊 tooa 特定會合位址的雙向通訊端。 然後 hello 用戶端可以與 hello 在內部部署服務上通訊，將訊息傳送目標 hello 會合位址 toohello 轉送服務。 hello 轉送服務會接著 「 轉送 」 訊息 toohello 在內部部署服務，透過既 hello 雙向通訊端。 hello 用戶端不需要直接連線 toohello 在內部部署服務，也不是所需的 it tooknow hello 服務位於何處，而且 hello 在內部部署服務並不需要任何輸入連接埠 hello 防火牆上開啟。

您起始 hello 連線在內部部署服務與 hello 轉送服務，使用一組 WCF 「 轉送 」 繫結。 Hello 幕後 hello 轉送繫結對應 tootransport 繫結項目設計 toocreate WCF 通道元件與 hello 雲端中的服務匯流排整合。

WCF 轉送提供許多優點，但是需要 hello 伺服器和用戶端 tooboth 看似在 hello 相同的時間順序 toosend 和接收訊息。 這不是最佳在哪一個 hello 要求可能不是通常存留較久的 HTTP 樣式通訊，或用戶端，只會偶爾連線，例如瀏覽器中，行動應用程式，並依此類推。 代理傳訊支援解耦合通訊，而且有其優勢。用戶端和伺服器可以在需要時連線，並且以非同步方式執行其作業。

## <a name="brokered-messaging"></a>代理傳訊
相較之下 toohello 轉送配置，Service Bus 訊息，或[代理訊息](service-bus-queues-topics-subscriptions.md)可以視為非同步，或 「 暫時分離 」。 產生者 （傳送者） 和消費者 （接收者） 不需要線上 toobe hello 在相同的時間。 hello 訊息基礎結構會可靠地儲存在 「 代理 」 訊息 （如佇列） 直到 hello 取用方準備 tooreceive 它們。 這可讓中斷連接，或是主動; hello 分散式應用程式 toobe hello 元件例如，為了進行維護，或因為 tooa 元件損毀，而不會影響 hello 整個系統。 此外，hello 接收應用程式可能只有線上 toocome hello 天，例如庫存管理系統，只是需要的 toorun hello hello 營業日結束在特定時間。

hello 的 hello Service Bus 代理訊息基礎結構的核心元件是佇列、 主題和訂用帳戶。  hello 主要差異是，主題也支援發行/訂閱功能，可用於複雜內容架構路由和傳遞邏輯，包括傳送 toomultiple 收件者。 這些元件能夠執行新的非同步傳訊案例，例如暫時解耦合、發佈/訂閱，以及負載平衡。 如需這些傳訊實體的詳細資訊，請參閱[服務匯流排佇列、主題及訂閱](service-bus-queues-topics-subscriptions.md)。

Hello WCF 轉送基礎結構，與 hello 代理訊息功能被提供對於 WCF 和.NET Framework 程式設計人員而言，也可以透過 REST。

## <a name="next-steps"></a>後續步驟
toolearn 有關服務匯流排傳訊的詳細資訊，請參閱下列主題中的 hello。

* [服務匯流排基本概念](service-bus-fundamentals-hybrid-solutions.md)
* [服務匯流排佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)
* [如何 toouse 服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [如何 toouse Service Bus 主題和訂閱](service-bus-dotnet-how-to-use-topics-subscriptions.md)

