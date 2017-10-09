---
title: "aaaWhat 是 Azure 轉送和為什麼使用概觀 |Microsoft 文件"
description: "Azure 轉送的概觀"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>什麼是 Azure 轉送？

hello Azure 轉送服務可方便您混合式應用程式藉由啟用您 toosecurely 公開 （expose） 服務，位於公司的企業網路 toohello 公用雲端，而不需要 tooopen 防火牆連線，或需要具侵入性變更 tooa公司網路基礎結構。 轉送支援各種不同的傳輸通訊協定和 Web 服務標準。

hello 轉送服務支援傳統單向、 要求/回應，以及對等流量。 它也支援網際網路領域 tooenable 發行/訂閱案例和雙向通訊端通訊上的事件發佈，以提高的點對點效率。 

在 hello 轉送資料的傳輸模式，在內部部署服務會 toohello 轉送服務連接透過輸出連接埠，並建立繫結的通訊 tooa 特定會合位址的雙向通訊端。 然後 hello 用戶端可以與 hello 在內部部署服務上通訊，藉由傳送 hello 會合位址為目標的流量 toohello 轉送服務。 hello 轉送服務然後 「 轉送 」 資料 toohello 在內部部署服務，透過雙向通訊端專用的 tooeach 用戶端。 hello 用戶端不需要直接連線 toohello 在內部部署服務，就不需要的 tooknow hello 服務位於何處，而且 hello 在內部部署服務並不需要任何輸入連接埠 hello 防火牆上開啟。

hello 金鑰功能所轉送提供雙向、 緩衝通訊跨網路界限與 TCP 類似的節流設定、 端點的探索、 連線狀態，並依據項目重疊端點安全性。 hello 轉送功能，如 VPN 的網路層級整合技術的不同，該轉送中可能會在單一電腦上已設定領域的 tooa 單一應用程式端點 VPN 技術時更具侵入性因為它是倚賴改變 hello 網路環境.

Azure 轉送有兩項功能︰

1. [混合式連線](#hybrid-connections)-啟用多平台案例的使用 hello 開啟標準 web 通訊端。
2. [WCF 轉送](#wcf-relays)-使用 Windows Communication Foundation (WCF) tooenable 遠端程序呼叫。 WCF 轉送是 hello 舊版轉送提供許多客戶已經使用其 WCF 程式設計模型。

混合式連線和 WCF 轉送可讓公司的企業網路中存在的安全連線 tooassets。 Hello 下表中所述，使用其他 hello 哪一個是取決於您的特定需求：

|  | WCF 轉送 | 混合式連線 |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **標準型開放式通訊協定** | |x |
| **多個 RPC 程式設計模型** | |x |

## <a name="hybrid-connections"></a>混合式連線

hello [Azure 轉送混合式連線](relay-hybrid-connections-protocol.md)功能是安全、 開放通訊協定的演進 hello 現有的轉送功能，可以在任何平台上，並具備基本的 WebSocket 功能，任何語言中實作的明確包含常用的 web 瀏覽器中的 hello WebSocket API。 混合式連線是以 HTTP 和 Websocket 為基礎。

### <a name="service-history"></a>服務歷程記錄

混合式連線取代了 hello 前者，同樣名為建置 hello Azure 服務匯流排的 WCF 轉送的 「 BizTalk 服務 」 功能。 hello 新混合式連接的功能，補充 hello 現有的 WCF 轉送功能，而這些兩個服務的功能存在 hello Azure 轉送服務並存。 它們共用通用的閘道，但有不同的實作方式。

## <a name="wcf-relays"></a>WCF 轉送

hello WCF 轉送適用於 hello 完整.NET Framework (NETFX) 和 wcf。 您起始 hello 在內部部署服務與使用 WCF 「 轉送 」 繫結套件 hello 轉送服務之間的連線。 Hello 幕後 hello 轉送繫結對應 toonew 傳輸繫結項目設計 toocreate WCF 通道元件與 hello 雲端中的服務匯流排整合。

## <a name="architecture-processing-of-incoming-relay-requests"></a>架構：處理內送轉送要求
當用戶端傳送要求 toohello [Azure 轉送](/azure/service-bus-relay/)hello Azure 負載平衡器服務將其路由傳送的 hello 閘道節點 tooany。 如果 hello 要求是接聽的要求，hello 的 gateway 節點會建立新的轉送。 如果連線要求 tooa 特定轉送 hello 要求，hello 的 gateway 節點會轉送 hello 連線要求 toohello 閘道節點擁有 hello 轉送。 hello 閘道節點擁有 hello 轉送傳送 rendezvous 要求 toohello 接聽用戶端，要求 hello 接聽程式 toocreate 暫時通道 toohello 閘道節點已收到 hello 連線要求。

建立 hello 轉送連線時，hello 用戶端可以交換訊息，透過用於 hello rendezvous hello 閘道節點。

![處理內送 WCF 轉送要求](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>後續步驟

* [轉送常見問題集](relay-faq.md)
* [建立命名空間](relay-create-namespace-portal.md)
* [開始使用 .NET](relay-hybrid-connections-dotnet-get-started.md)
* [開始使用 Node](relay-hybrid-connections-node-get-started.md)

