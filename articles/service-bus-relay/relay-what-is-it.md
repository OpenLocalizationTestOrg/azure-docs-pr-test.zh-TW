---
title: "什麼是 Azure 轉送和為什麼使用的概觀 | Microsoft Docs"
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
ms.openlocfilehash: 77ee85db0bcc701514a1a98da9405a79d658d49d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="what-is-azure-relay"></a><span data-ttu-id="0c229-103">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="0c229-103">What is Azure Relay?</span></span>

<span data-ttu-id="0c229-104">Azure 轉送服務可執行混合式應用程式，方法是讓您以安全的方式向公用雲端公開位於企業網路內部的服務，而無需開啟防火牆連線或要求對企業網路基礎結構的進行侵入式變更。</span><span class="sxs-lookup"><span data-stu-id="0c229-104">The Azure Relay service facilitates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="0c229-105">轉送支援各種不同的傳輸通訊協定和 Web 服務標準。</span><span class="sxs-lookup"><span data-stu-id="0c229-105">Relay supports a variety of different transport protocols and web services standards.</span></span>

<span data-ttu-id="0c229-106">轉送服務支援傳統的單向、要求/回應以及對等式流量。</span><span class="sxs-lookup"><span data-stu-id="0c229-106">The relay service supports traditional one-way, request/response, and peer-to-peer traffic.</span></span> <span data-ttu-id="0c229-107">它也支援網際網路範圍內的事件散發，以啟用發佈/訂閱案例和雙向通訊端通訊來提高點對點效率。</span><span class="sxs-lookup"><span data-stu-id="0c229-107">It also supports event distribution at internet-scope to enable publish/subscribe scenarios and bi-directional socket communication for increased point-to-point efficiency.</span></span> 

<span data-ttu-id="0c229-108">在轉送的資料傳輸模式中，內部部署服務會透過輸出連接埠連接到轉送服務，並且針對繫結至特定聚合位址的通訊建立雙向通訊端。</span><span class="sxs-lookup"><span data-stu-id="0c229-108">In the relayed data transfer pattern, an on-premises service connects to the relay service through an outbound port and creates a bi-directional socket for communication tied to a particular rendezvous address.</span></span> <span data-ttu-id="0c229-109">用戶端接著可將流量傳送至以會合位址為目標的轉送服務，藉此與內部部署服務通訊。</span><span class="sxs-lookup"><span data-stu-id="0c229-109">The client can then communicate with the on-premises service by sending traffic to the relay service targeting the rendezvous address.</span></span> <span data-ttu-id="0c229-110">轉送服務接著會透過每個用戶端專用的雙向通訊端，將資料「轉送」至內部部署服務。</span><span class="sxs-lookup"><span data-stu-id="0c229-110">The relay service then "relays" data to the on-premises service through a bi-directional socket dedicated to each client.</span></span> <span data-ttu-id="0c229-111">用戶端不需要直接連線到內部部署服務，不需要知道服務所在的位置，而且內部部署服務不需要在防火牆上開啟任何輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="0c229-111">The client does not need a direct connection to the on-premises service, it is not required to know where the service resides, and the on-premises service does not need any inbound ports open on the firewall.</span></span>

<span data-ttu-id="0c229-112">轉送所提供的重要功能元素是利用類似 TCP 的節流、端點探索、連線狀態和重疊端點安全性，進行跨越網路界限且未經緩衝處理的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="0c229-112">The key capability elements provided by Relay are bi-directional, unbuffered communication across network boundaries with TCP-like throttling, endpoint discovery, connectivity status, and overlaid endpoint security.</span></span> <span data-ttu-id="0c229-113">轉送功能與網路層級整合技術 (例如 VPN) 不同，轉送的範圍可以限定於單一電腦上的單一應用程式端點，而 VPN 技術則比較屬於侵入式，因為其依賴於改變網路環境。</span><span class="sxs-lookup"><span data-stu-id="0c229-113">The relay capabilities differ from network-level integration technologies such as VPN, in that relay can be scoped to a single application endpoint on a single machine, while VPN technology is far more intrusive as it relies on altering the network environment.</span></span>

<span data-ttu-id="0c229-114">Azure 轉送有兩項功能︰</span><span class="sxs-lookup"><span data-stu-id="0c229-114">Azure Relay has two features:</span></span>

1. <span data-ttu-id="0c229-115">[混合式連線](#hybrid-connections) - 使用開放式標準 Web 通訊端來啟用多平台案例。</span><span class="sxs-lookup"><span data-stu-id="0c229-115">[Hybrid Connections](#hybrid-connections) - Uses the open standard web sockets enabling multi-platform scenarios.</span></span>
2. <span data-ttu-id="0c229-116">[WCF 轉送](#wcf-relays) - 使用 Windows Communication Foundation (WCF) 來啟用遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="0c229-116">[WCF Relays](#wcf-relays) - Uses Windows Communication Foundation (WCF) to enable remote procedure calls.</span></span> <span data-ttu-id="0c229-117">WCF 轉送是舊版的轉送服務，許多客戶已將該服務用於其 WCF 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="0c229-117">WCF Relay is the legacy relay offering that many customers already use with their WCF programming models.</span></span>

<span data-ttu-id="0c229-118">混合式連線和 WCF 轉送都能夠對存在於企業網路內的資產進行安全的連線。</span><span class="sxs-lookup"><span data-stu-id="0c229-118">Hybrid Connections and WCF Relays both enable secure connection to assets that exist within a corporate enterprise network.</span></span> <span data-ttu-id="0c229-119">視您的特定需求使用其中一項功能，詳述於下表︰</span><span class="sxs-lookup"><span data-stu-id="0c229-119">Use of one over the other is dependent on your particular needs, as described in the following table:</span></span>

|  | <span data-ttu-id="0c229-120">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="0c229-120">WCF Relay</span></span> | <span data-ttu-id="0c229-121">混合式連線</span><span class="sxs-lookup"><span data-stu-id="0c229-121">Hybrid Connections</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="0c229-122">**WCF**</span><span class="sxs-lookup"><span data-stu-id="0c229-122">**WCF**</span></span> |<span data-ttu-id="0c229-123">x</span><span class="sxs-lookup"><span data-stu-id="0c229-123">x</span></span> | |
| <span data-ttu-id="0c229-124">**.NET Core**</span><span class="sxs-lookup"><span data-stu-id="0c229-124">**.NET Core**</span></span> | |<span data-ttu-id="0c229-125">x</span><span class="sxs-lookup"><span data-stu-id="0c229-125">x</span></span> |
| <span data-ttu-id="0c229-126">**.NET Framework**</span><span class="sxs-lookup"><span data-stu-id="0c229-126">**.NET Framework**</span></span> |<span data-ttu-id="0c229-127">x</span><span class="sxs-lookup"><span data-stu-id="0c229-127">x</span></span> |<span data-ttu-id="0c229-128">x</span><span class="sxs-lookup"><span data-stu-id="0c229-128">x</span></span> |
| <span data-ttu-id="0c229-129">**JavaScript/NodeJS**</span><span class="sxs-lookup"><span data-stu-id="0c229-129">**JavaScript/NodeJS**</span></span> | |<span data-ttu-id="0c229-130">x</span><span class="sxs-lookup"><span data-stu-id="0c229-130">x</span></span> |
| <span data-ttu-id="0c229-131">**標準型開放式通訊協定**</span><span class="sxs-lookup"><span data-stu-id="0c229-131">**Standards-Based Open Protocol**</span></span> | |<span data-ttu-id="0c229-132">x</span><span class="sxs-lookup"><span data-stu-id="0c229-132">x</span></span> |
| <span data-ttu-id="0c229-133">**多個 RPC 程式設計模型**</span><span class="sxs-lookup"><span data-stu-id="0c229-133">**Multiple RPC Programming Models**</span></span> | |<span data-ttu-id="0c229-134">x</span><span class="sxs-lookup"><span data-stu-id="0c229-134">x</span></span> |

## <a name="hybrid-connections"></a><span data-ttu-id="0c229-135">混合式連線</span><span class="sxs-lookup"><span data-stu-id="0c229-135">Hybrid Connections</span></span>

<span data-ttu-id="0c229-136">[Azure 轉送混合式連線](relay-hybrid-connections-protocol.md)功能是現有轉送功能的安全、開放式通訊協定演化，可以在任何平台上以任何具有基本 WebSocket 功能的語言實作，而基本 WebSocket 功能會明確地將 WebSocket API 納入一般網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0c229-136">The [Azure Relay Hybrid Connections](relay-hybrid-connections-protocol.md) capability is a secure, open-protocol evolution of the existing Relay features that can be implemented on any platform and in any language that has a basic WebSocket capability, which explicitly includes the WebSocket API in common web browsers.</span></span> <span data-ttu-id="0c229-137">混合式連線是以 HTTP 和 Websocket 為基礎。</span><span class="sxs-lookup"><span data-stu-id="0c229-137">Hybrid Connections is based on HTTP and WebSockets.</span></span>

### <a name="service-history"></a><span data-ttu-id="0c229-138">服務歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0c229-138">Service history</span></span>

<span data-ttu-id="0c229-139">「混合式連線」會取代先前的功能，該功能同樣名為「BizTalk 服務」功能且建置於 Azure 服務匯流排 WCF 轉送。</span><span class="sxs-lookup"><span data-stu-id="0c229-139">Hybrid Connections supplants the former, similarly named "BizTalk Services" feature that was built on the Azure Service Bus WCF Relay.</span></span> <span data-ttu-id="0c229-140">新的混合式連線功能可補充現有的 WCF 轉送功能，而這兩個服務功能會並存於 Azure 轉送服務中。</span><span class="sxs-lookup"><span data-stu-id="0c229-140">The new Hybrid Connections capability complements the existing WCF Relay feature and these two service capabilities exist side-by-side in the Azure Relay service.</span></span> <span data-ttu-id="0c229-141">它們共用通用的閘道，但有不同的實作方式。</span><span class="sxs-lookup"><span data-stu-id="0c229-141">They share a common gateway, but are otherwise different implementations.</span></span>

## <a name="wcf-relays"></a><span data-ttu-id="0c229-142">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="0c229-142">WCF Relays</span></span>

<span data-ttu-id="0c229-143">WCF 轉送適用於完整的 .NET Framework (NETFX) 和 WCF。</span><span class="sxs-lookup"><span data-stu-id="0c229-143">The WCF Relay works for the full .NET Framework (NETFX) and for WCF.</span></span> <span data-ttu-id="0c229-144">您在內部部署服務與使用一組 WCF「轉送」繫結的轉送服務之間起始連線。</span><span class="sxs-lookup"><span data-stu-id="0c229-144">You initiate the connection between your on-premises service and the relay service using a suite of WCF "relay" bindings.</span></span> <span data-ttu-id="0c229-145">在幕後，轉送繫結會對應至新的傳輸繫結元素，其設計來建立與雲端中服務匯流排整合的 WCF 通道元件。</span><span class="sxs-lookup"><span data-stu-id="0c229-145">Behind the scenes, the relay bindings map to new transport binding elements designed to create WCF channel components that integrate with Service Bus in the cloud.</span></span>

## <a name="architecture-processing-of-incoming-relay-requests"></a><span data-ttu-id="0c229-146">架構：處理內送轉送要求</span><span class="sxs-lookup"><span data-stu-id="0c229-146">Architecture: Processing of incoming relay requests</span></span>
<span data-ttu-id="0c229-147">當用戶端傳送要求至 [Azure 轉送](/azure/service-bus-relay/)服務時，Azure Load Balancer 會將其路由到任何一個閘道器節點。</span><span class="sxs-lookup"><span data-stu-id="0c229-147">When a client sends a request to the [Azure Relay](/azure/service-bus-relay/) service, the Azure load balancer routes it to any of the gateway nodes.</span></span> <span data-ttu-id="0c229-148">如果要求為接聽要求，閘道器節點會建立新的轉送。</span><span class="sxs-lookup"><span data-stu-id="0c229-148">If the request is a listening request, the gateway node creates a new relay.</span></span> <span data-ttu-id="0c229-149">如果要求為特定轉送的連線要求，閘道器節點會轉送連線要求給擁有轉送的閘道器節點。</span><span class="sxs-lookup"><span data-stu-id="0c229-149">If the request is a connection request to a specific relay, the gateway node forwards the connection request to the gateway node that owns the relay.</span></span> <span data-ttu-id="0c229-150">擁有轉送的閘道器節點會傳送會合要求到接聽用戶端，要求接聽程式建立接收連線要求的閘道器節點的暫時通道。</span><span class="sxs-lookup"><span data-stu-id="0c229-150">The gateway node that owns the relay sends a rendezvous request to the listening client, asking the listener to create a temporary channel to the gateway node that received the connection request.</span></span>

<span data-ttu-id="0c229-151">建立轉送連線時，用戶端可以透過用來會合的閘道節點交換訊息。</span><span class="sxs-lookup"><span data-stu-id="0c229-151">When the relay connection is established, the clients can exchange messages via the gateway node that is used for the rendezvous.</span></span>

![處理內送 WCF 轉送要求](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a><span data-ttu-id="0c229-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c229-153">Next steps</span></span>

* [<span data-ttu-id="0c229-154">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="0c229-154">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="0c229-155">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="0c229-155">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="0c229-156">開始使用 .NET</span><span class="sxs-lookup"><span data-stu-id="0c229-156">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="0c229-157">開始使用 Node</span><span class="sxs-lookup"><span data-stu-id="0c229-157">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

