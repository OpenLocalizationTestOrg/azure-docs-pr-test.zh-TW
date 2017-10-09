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
# <a name="what-is-azure-relay"></a><span data-ttu-id="909a7-103">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="909a7-103">What is Azure Relay?</span></span>

<span data-ttu-id="909a7-104">hello Azure 轉送服務可方便您混合式應用程式藉由啟用您 toosecurely 公開 （expose） 服務，位於公司的企業網路 toohello 公用雲端，而不需要 tooopen 防火牆連線，或需要具侵入性變更 tooa公司網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="909a7-104">hello Azure Relay service facilitates hybrid applications by enabling you toosecurely expose services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or require intrusive changes tooa corporate network infrastructure.</span></span> <span data-ttu-id="909a7-105">轉送支援各種不同的傳輸通訊協定和 Web 服務標準。</span><span class="sxs-lookup"><span data-stu-id="909a7-105">Relay supports a variety of different transport protocols and web services standards.</span></span>

<span data-ttu-id="909a7-106">hello 轉送服務支援傳統單向、 要求/回應，以及對等流量。</span><span class="sxs-lookup"><span data-stu-id="909a7-106">hello relay service supports traditional one-way, request/response, and peer-to-peer traffic.</span></span> <span data-ttu-id="909a7-107">它也支援網際網路領域 tooenable 發行/訂閱案例和雙向通訊端通訊上的事件發佈，以提高的點對點效率。</span><span class="sxs-lookup"><span data-stu-id="909a7-107">It also supports event distribution at internet-scope tooenable publish/subscribe scenarios and bi-directional socket communication for increased point-to-point efficiency.</span></span> 

<span data-ttu-id="909a7-108">在 hello 轉送資料的傳輸模式，在內部部署服務會 toohello 轉送服務連接透過輸出連接埠，並建立繫結的通訊 tooa 特定會合位址的雙向通訊端。</span><span class="sxs-lookup"><span data-stu-id="909a7-108">In hello relayed data transfer pattern, an on-premises service connects toohello relay service through an outbound port and creates a bi-directional socket for communication tied tooa particular rendezvous address.</span></span> <span data-ttu-id="909a7-109">然後 hello 用戶端可以與 hello 在內部部署服務上通訊，藉由傳送 hello 會合位址為目標的流量 toohello 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="909a7-109">hello client can then communicate with hello on-premises service by sending traffic toohello relay service targeting hello rendezvous address.</span></span> <span data-ttu-id="909a7-110">hello 轉送服務然後 「 轉送 」 資料 toohello 在內部部署服務，透過雙向通訊端專用的 tooeach 用戶端。</span><span class="sxs-lookup"><span data-stu-id="909a7-110">hello relay service then "relays" data toohello on-premises service through a bi-directional socket dedicated tooeach client.</span></span> <span data-ttu-id="909a7-111">hello 用戶端不需要直接連線 toohello 在內部部署服務，就不需要的 tooknow hello 服務位於何處，而且 hello 在內部部署服務並不需要任何輸入連接埠 hello 防火牆上開啟。</span><span class="sxs-lookup"><span data-stu-id="909a7-111">hello client does not need a direct connection toohello on-premises service, it is not required tooknow where hello service resides, and hello on-premises service does not need any inbound ports open on hello firewall.</span></span>

<span data-ttu-id="909a7-112">hello 金鑰功能所轉送提供雙向、 緩衝通訊跨網路界限與 TCP 類似的節流設定、 端點的探索、 連線狀態，並依據項目重疊端點安全性。</span><span class="sxs-lookup"><span data-stu-id="909a7-112">hello key capability elements provided by Relay are bi-directional, unbuffered communication across network boundaries with TCP-like throttling, endpoint discovery, connectivity status, and overlaid endpoint security.</span></span> <span data-ttu-id="909a7-113">hello 轉送功能，如 VPN 的網路層級整合技術的不同，該轉送中可能會在單一電腦上已設定領域的 tooa 單一應用程式端點 VPN 技術時更具侵入性因為它是倚賴改變 hello 網路環境.</span><span class="sxs-lookup"><span data-stu-id="909a7-113">hello relay capabilities differ from network-level integration technologies such as VPN, in that relay can be scoped tooa single application endpoint on a single machine, while VPN technology is far more intrusive as it relies on altering hello network environment.</span></span>

<span data-ttu-id="909a7-114">Azure 轉送有兩項功能︰</span><span class="sxs-lookup"><span data-stu-id="909a7-114">Azure Relay has two features:</span></span>

1. <span data-ttu-id="909a7-115">[混合式連線](#hybrid-connections)-啟用多平台案例的使用 hello 開啟標準 web 通訊端。</span><span class="sxs-lookup"><span data-stu-id="909a7-115">[Hybrid Connections](#hybrid-connections) - Uses hello open standard web sockets enabling multi-platform scenarios.</span></span>
2. <span data-ttu-id="909a7-116">[WCF 轉送](#wcf-relays)-使用 Windows Communication Foundation (WCF) tooenable 遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="909a7-116">[WCF Relays](#wcf-relays) - Uses Windows Communication Foundation (WCF) tooenable remote procedure calls.</span></span> <span data-ttu-id="909a7-117">WCF 轉送是 hello 舊版轉送提供許多客戶已經使用其 WCF 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="909a7-117">WCF Relay is hello legacy relay offering that many customers already use with their WCF programming models.</span></span>

<span data-ttu-id="909a7-118">混合式連線和 WCF 轉送可讓公司的企業網路中存在的安全連線 tooassets。</span><span class="sxs-lookup"><span data-stu-id="909a7-118">Hybrid Connections and WCF Relays both enable secure connection tooassets that exist within a corporate enterprise network.</span></span> <span data-ttu-id="909a7-119">Hello 下表中所述，使用其他 hello 哪一個是取決於您的特定需求：</span><span class="sxs-lookup"><span data-stu-id="909a7-119">Use of one over hello other is dependent on your particular needs, as described in hello following table:</span></span>

|  | <span data-ttu-id="909a7-120">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="909a7-120">WCF Relay</span></span> | <span data-ttu-id="909a7-121">混合式連線</span><span class="sxs-lookup"><span data-stu-id="909a7-121">Hybrid Connections</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="909a7-122">**WCF**</span><span class="sxs-lookup"><span data-stu-id="909a7-122">**WCF**</span></span> |<span data-ttu-id="909a7-123">x</span><span class="sxs-lookup"><span data-stu-id="909a7-123">x</span></span> | |
| <span data-ttu-id="909a7-124">**.NET Core**</span><span class="sxs-lookup"><span data-stu-id="909a7-124">**.NET Core**</span></span> | |<span data-ttu-id="909a7-125">x</span><span class="sxs-lookup"><span data-stu-id="909a7-125">x</span></span> |
| <span data-ttu-id="909a7-126">**.NET Framework**</span><span class="sxs-lookup"><span data-stu-id="909a7-126">**.NET Framework**</span></span> |<span data-ttu-id="909a7-127">x</span><span class="sxs-lookup"><span data-stu-id="909a7-127">x</span></span> |<span data-ttu-id="909a7-128">x</span><span class="sxs-lookup"><span data-stu-id="909a7-128">x</span></span> |
| <span data-ttu-id="909a7-129">**JavaScript/NodeJS**</span><span class="sxs-lookup"><span data-stu-id="909a7-129">**JavaScript/NodeJS**</span></span> | |<span data-ttu-id="909a7-130">x</span><span class="sxs-lookup"><span data-stu-id="909a7-130">x</span></span> |
| <span data-ttu-id="909a7-131">**標準型開放式通訊協定**</span><span class="sxs-lookup"><span data-stu-id="909a7-131">**Standards-Based Open Protocol**</span></span> | |<span data-ttu-id="909a7-132">x</span><span class="sxs-lookup"><span data-stu-id="909a7-132">x</span></span> |
| <span data-ttu-id="909a7-133">**多個 RPC 程式設計模型**</span><span class="sxs-lookup"><span data-stu-id="909a7-133">**Multiple RPC Programming Models**</span></span> | |<span data-ttu-id="909a7-134">x</span><span class="sxs-lookup"><span data-stu-id="909a7-134">x</span></span> |

## <a name="hybrid-connections"></a><span data-ttu-id="909a7-135">混合式連線</span><span class="sxs-lookup"><span data-stu-id="909a7-135">Hybrid Connections</span></span>

<span data-ttu-id="909a7-136">hello [Azure 轉送混合式連線](relay-hybrid-connections-protocol.md)功能是安全、 開放通訊協定的演進 hello 現有的轉送功能，可以在任何平台上，並具備基本的 WebSocket 功能，任何語言中實作的明確包含常用的 web 瀏覽器中的 hello WebSocket API。</span><span class="sxs-lookup"><span data-stu-id="909a7-136">hello [Azure Relay Hybrid Connections](relay-hybrid-connections-protocol.md) capability is a secure, open-protocol evolution of hello existing Relay features that can be implemented on any platform and in any language that has a basic WebSocket capability, which explicitly includes hello WebSocket API in common web browsers.</span></span> <span data-ttu-id="909a7-137">混合式連線是以 HTTP 和 Websocket 為基礎。</span><span class="sxs-lookup"><span data-stu-id="909a7-137">Hybrid Connections is based on HTTP and WebSockets.</span></span>

### <a name="service-history"></a><span data-ttu-id="909a7-138">服務歷程記錄</span><span class="sxs-lookup"><span data-stu-id="909a7-138">Service history</span></span>

<span data-ttu-id="909a7-139">混合式連線取代了 hello 前者，同樣名為建置 hello Azure 服務匯流排的 WCF 轉送的 「 BizTalk 服務 」 功能。</span><span class="sxs-lookup"><span data-stu-id="909a7-139">Hybrid Connections supplants hello former, similarly named "BizTalk Services" feature that was built on hello Azure Service Bus WCF Relay.</span></span> <span data-ttu-id="909a7-140">hello 新混合式連接的功能，補充 hello 現有的 WCF 轉送功能，而這些兩個服務的功能存在 hello Azure 轉送服務並存。</span><span class="sxs-lookup"><span data-stu-id="909a7-140">hello new Hybrid Connections capability complements hello existing WCF Relay feature and these two service capabilities exist side-by-side in hello Azure Relay service.</span></span> <span data-ttu-id="909a7-141">它們共用通用的閘道，但有不同的實作方式。</span><span class="sxs-lookup"><span data-stu-id="909a7-141">They share a common gateway, but are otherwise different implementations.</span></span>

## <a name="wcf-relays"></a><span data-ttu-id="909a7-142">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="909a7-142">WCF Relays</span></span>

<span data-ttu-id="909a7-143">hello WCF 轉送適用於 hello 完整.NET Framework (NETFX) 和 wcf。</span><span class="sxs-lookup"><span data-stu-id="909a7-143">hello WCF Relay works for hello full .NET Framework (NETFX) and for WCF.</span></span> <span data-ttu-id="909a7-144">您起始 hello 在內部部署服務與使用 WCF 「 轉送 」 繫結套件 hello 轉送服務之間的連線。</span><span class="sxs-lookup"><span data-stu-id="909a7-144">You initiate hello connection between your on-premises service and hello relay service using a suite of WCF "relay" bindings.</span></span> <span data-ttu-id="909a7-145">Hello 幕後 hello 轉送繫結對應 toonew 傳輸繫結項目設計 toocreate WCF 通道元件與 hello 雲端中的服務匯流排整合。</span><span class="sxs-lookup"><span data-stu-id="909a7-145">Behind hello scenes, hello relay bindings map toonew transport binding elements designed toocreate WCF channel components that integrate with Service Bus in hello cloud.</span></span>

## <a name="architecture-processing-of-incoming-relay-requests"></a><span data-ttu-id="909a7-146">架構：處理內送轉送要求</span><span class="sxs-lookup"><span data-stu-id="909a7-146">Architecture: Processing of incoming relay requests</span></span>
<span data-ttu-id="909a7-147">當用戶端傳送要求 toohello [Azure 轉送](/azure/service-bus-relay/)hello Azure 負載平衡器服務將其路由傳送的 hello 閘道節點 tooany。</span><span class="sxs-lookup"><span data-stu-id="909a7-147">When a client sends a request toohello [Azure Relay](/azure/service-bus-relay/) service, hello Azure load balancer routes it tooany of hello gateway nodes.</span></span> <span data-ttu-id="909a7-148">如果 hello 要求是接聽的要求，hello 的 gateway 節點會建立新的轉送。</span><span class="sxs-lookup"><span data-stu-id="909a7-148">If hello request is a listening request, hello gateway node creates a new relay.</span></span> <span data-ttu-id="909a7-149">如果連線要求 tooa 特定轉送 hello 要求，hello 的 gateway 節點會轉送 hello 連線要求 toohello 閘道節點擁有 hello 轉送。</span><span class="sxs-lookup"><span data-stu-id="909a7-149">If hello request is a connection request tooa specific relay, hello gateway node forwards hello connection request toohello gateway node that owns hello relay.</span></span> <span data-ttu-id="909a7-150">hello 閘道節點擁有 hello 轉送傳送 rendezvous 要求 toohello 接聽用戶端，要求 hello 接聽程式 toocreate 暫時通道 toohello 閘道節點已收到 hello 連線要求。</span><span class="sxs-lookup"><span data-stu-id="909a7-150">hello gateway node that owns hello relay sends a rendezvous request toohello listening client, asking hello listener toocreate a temporary channel toohello gateway node that received hello connection request.</span></span>

<span data-ttu-id="909a7-151">建立 hello 轉送連線時，hello 用戶端可以交換訊息，透過用於 hello rendezvous hello 閘道節點。</span><span class="sxs-lookup"><span data-stu-id="909a7-151">When hello relay connection is established, hello clients can exchange messages via hello gateway node that is used for hello rendezvous.</span></span>

![處理內送 WCF 轉送要求](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a><span data-ttu-id="909a7-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="909a7-153">Next steps</span></span>

* [<span data-ttu-id="909a7-154">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="909a7-154">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="909a7-155">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="909a7-155">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="909a7-156">開始使用 .NET</span><span class="sxs-lookup"><span data-stu-id="909a7-156">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="909a7-157">開始使用 Node</span><span class="sxs-lookup"><span data-stu-id="909a7-157">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

