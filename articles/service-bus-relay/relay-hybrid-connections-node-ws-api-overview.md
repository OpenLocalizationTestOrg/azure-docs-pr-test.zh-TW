---
title: "Azure 轉送節點 API 概觀 | Microsoft Docs"
description: "轉送節點 API 概觀"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="55746-103">轉送混合式連接節點 API 概觀</span><span class="sxs-lookup"><span data-stu-id="55746-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="55746-104">概觀</span><span class="sxs-lookup"><span data-stu-id="55746-104">Overview</span></span>

<span data-ttu-id="55746-105">[`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Azure 轉送混合式連線的節點封裝建置於並擴充 ['ws'](https://www.npmjs.com/package/ws) NPM 封裝。</span><span class="sxs-lookup"><span data-stu-id="55746-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="55746-106">此封裝重新匯出該基本封裝的所有匯出，並新增新的匯出，可啟用與 Azure 轉送服務混合式連線功能整合。</span><span class="sxs-lookup"><span data-stu-id="55746-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="55746-107">現有的應用程式 `require('ws')` 可以改為搭配使用這個套件與 `require('hyco-ws')`，這也會啟用混合式案例，其中應用程式可以從「防火牆內部」及透過混合式連線，在本機接聽 WebSocket 連線，全部都在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="55746-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="55746-108">文件</span><span class="sxs-lookup"><span data-stu-id="55746-108">Documentation</span></span>

<span data-ttu-id="55746-109">API [記載於主要的 'ws' 封裝中](https://github.com/websockets/ws/blob/master/doc/ws.md)。</span><span class="sxs-lookup"><span data-stu-id="55746-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="55746-110">本文說明此套件與該基準不同之處。</span><span class="sxs-lookup"><span data-stu-id="55746-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="55746-111">基本封裝和此 ' hyco-ws' 之間的主要差異在於此 'hyco-ws' 新增了新的伺服器類別，透過 `require('hyco-ws').RelayedServer` 匯出，和一些協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="55746-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="55746-112">套件協助程式方法</span><span class="sxs-lookup"><span data-stu-id="55746-112">Package helper methods</span></span>

<span data-ttu-id="55746-113">封裝匯出上有數個公用程式方法可供您參考，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="55746-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="55746-114">協助程式方法適用於與此封裝搭配使用，但也可供節點伺服器用來啟用 web 或裝置用戶端以建立接聽程式或傳送程式。</span><span class="sxs-lookup"><span data-stu-id="55746-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="55746-115">伺服器會將內嵌短期權杖的 URI 傳遞給它們來使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="55746-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="55746-116">這些 URI 也可以搭配使用一般不支援設定 WebSocket 信號交換之 HTTP 標頭的 WebSocket 堆疊。</span><span class="sxs-lookup"><span data-stu-id="55746-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="55746-117">將授權權杖內嵌至 URI 主要目的是為了支援這些程式庫外部使用方式案例。</span><span class="sxs-lookup"><span data-stu-id="55746-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="55746-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="55746-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="55746-119">建立指定命名空間和路徑的有效 Azure 轉送混合式連線接聽程式 URI。</span><span class="sxs-lookup"><span data-stu-id="55746-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="55746-120">此 URI 便可搭配使用轉送版本的 WebSocketServer 類別。</span><span class="sxs-lookup"><span data-stu-id="55746-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="55746-121">`namespaceName` (必要) - 要使用的 Azure 轉送命名空間之網域限定名稱。</span><span class="sxs-lookup"><span data-stu-id="55746-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="55746-122">`path` (必要) - 該命名空間中現有的 Azure 轉送混合式連線名稱。</span><span class="sxs-lookup"><span data-stu-id="55746-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="55746-123">`token` (選用) - 內嵌在接聽程式 URI 的先前發行轉送存取權杖 (請參閱下列範例)。</span><span class="sxs-lookup"><span data-stu-id="55746-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="55746-124">`id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="55746-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="55746-125">`token` 值是選擇性的，且應該僅用於無法傳送 HTTP 標題與 WebSocket 交握作業時，在此情況下為 W3C WebSocket 堆疊。</span><span class="sxs-lookup"><span data-stu-id="55746-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="55746-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="55746-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="55746-127">建立指定命名空間和路徑的有效 Azure 轉送混合式連線傳送 URI。</span><span class="sxs-lookup"><span data-stu-id="55746-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="55746-128">這個 URI 可以搭配使用任何 WebSocket 用戶端。</span><span class="sxs-lookup"><span data-stu-id="55746-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="55746-129">`namespaceName` (必要) - 要使用的 Azure 轉送命名空間之網域限定名稱。</span><span class="sxs-lookup"><span data-stu-id="55746-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="55746-130">`path` (必要) - 該命名空間中現有的 Azure 轉送混合式連線名稱。</span><span class="sxs-lookup"><span data-stu-id="55746-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="55746-131">`token` (選用) - 內嵌在傳送 URI 的先前發行轉送存取權杖 (請參閱下列範例)。</span><span class="sxs-lookup"><span data-stu-id="55746-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="55746-132">`id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="55746-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="55746-133">`token` 值是選擇性的，且應該僅用於無法傳送 HTTP 標題與 WebSocket 交握作業時，在此情況下為 W3C WebSocket 堆疊。</span><span class="sxs-lookup"><span data-stu-id="55746-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="55746-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="55746-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="55746-135">建立指定目標 URI、SAS 規則和 SAS 規則金鑰的 Azure 轉送共用存取簽章 (SAS) 權杖，如果省略到期引數，則其從目前即刻起指定的秒數或一小時為有效。</span><span class="sxs-lookup"><span data-stu-id="55746-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="55746-136">`uri` (必要) - 要發行權杖的 URI。</span><span class="sxs-lookup"><span data-stu-id="55746-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="55746-137">URI 會正規化為使用 HTTP 配置，且會移除查詢字串資訊。</span><span class="sxs-lookup"><span data-stu-id="55746-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="55746-138">`ruleName` (必要) - 指定 URI 所代表之實體或 URI 主機部分所代表之命名空間的 SAS 規則名稱。</span><span class="sxs-lookup"><span data-stu-id="55746-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="55746-139">`key` (必要) - SAS 規則的有效金鑰。</span><span class="sxs-lookup"><span data-stu-id="55746-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="55746-140">`expirationSeconds` (選用) - 所產生權杖應過期前的秒數。</span><span class="sxs-lookup"><span data-stu-id="55746-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="55746-141">如果未指定，則預設值是 1 小時 (3600)。</span><span class="sxs-lookup"><span data-stu-id="55746-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="55746-142">發行的權杖會授與指定持續時間與所指定之 SAS 規則相關聯的權限。</span><span class="sxs-lookup"><span data-stu-id="55746-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="55746-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="55746-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="55746-144">此方法在功能上相當於先前所記載的 `createRelayToken` 方法，但傳回的權杖正確地附加至輸入 URI。</span><span class="sxs-lookup"><span data-stu-id="55746-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="55746-145">類別 ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="55746-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="55746-146">`hycows.RelayedServer` 類別是替代 `ws.Server` 類別，其不會接聽本機網路，但會委派接聽 Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="55746-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="55746-147">這兩個類別大部分是合約相容，也就是說使用 `ws.Server` 類別的現有應用程式可以輕鬆地變更為使用轉送的版本。</span><span class="sxs-lookup"><span data-stu-id="55746-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="55746-148">主要差異是在建構函式以及可用的選項中。</span><span class="sxs-lookup"><span data-stu-id="55746-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="55746-149">建構函式</span><span class="sxs-lookup"><span data-stu-id="55746-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="55746-150">`RelayedServer` 建構函式支援與 `Server` 不同的一組引數，因為它並非獨立接聽程式，也不能內嵌到現有的 HTTP 接聽程式架構。</span><span class="sxs-lookup"><span data-stu-id="55746-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="55746-151">可用選項也較少，因為 WebSocket 管理多半會委派至轉送服務。</span><span class="sxs-lookup"><span data-stu-id="55746-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="55746-152">建構函式引數︰</span><span class="sxs-lookup"><span data-stu-id="55746-152">Constructor arguments:</span></span>

- <span data-ttu-id="55746-153">`server` (必要) - 要接聽之混合式連線名稱的完整 URI，通常是使用 WebSocket.createRelayListenUri() 協助程式方法所建構。</span><span class="sxs-lookup"><span data-stu-id="55746-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="55746-154">`token` (必要) - 這個引數包含先前發行的權杖字串或可以呼叫以取得權杖字串的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="55746-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="55746-155">回呼是慣用選項，因為它可讓權杖更新。</span><span class="sxs-lookup"><span data-stu-id="55746-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="55746-156">事件</span><span class="sxs-lookup"><span data-stu-id="55746-156">Events</span></span>

<span data-ttu-id="55746-157">`RelayedServer` 執行個體會發出三個事件，可讓您處理傳入要求、建立連線，以及偵測錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="55746-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="55746-158">您必須訂閱 `connect` 事件以處理訊息。</span><span class="sxs-lookup"><span data-stu-id="55746-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="55746-159">headers</span><span class="sxs-lookup"><span data-stu-id="55746-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="55746-160">接受連入連線前才會引發 `headers` 事件，讓修改標題傳送給用戶端。</span><span class="sxs-lookup"><span data-stu-id="55746-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="55746-161">connection</span><span class="sxs-lookup"><span data-stu-id="55746-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="55746-162">接受新的 WebSocket 連線時就會發出。</span><span class="sxs-lookup"><span data-stu-id="55746-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="55746-163">物件類型是 `ws.WebSocket`，與基本封裝相同。</span><span class="sxs-lookup"><span data-stu-id="55746-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="55746-164">錯誤</span><span class="sxs-lookup"><span data-stu-id="55746-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="55746-165">如果基礎伺服器發出錯誤，它會在這裡轉送。</span><span class="sxs-lookup"><span data-stu-id="55746-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="55746-166">協助程式</span><span class="sxs-lookup"><span data-stu-id="55746-166">Helpers</span></span>

<span data-ttu-id="55746-167">若要簡化啟動轉送的伺服器，並立即訂閱連入連線，封裝會公開簡單的協助程式函式，也會在範例中使用，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="55746-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="55746-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="55746-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="55746-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="55746-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="55746-170">這個方法會呼叫建構函式來建立 RelayedServer 的新執行個體，然後訂閱 'connection' 事件所提供的回呼。</span><span class="sxs-lookup"><span data-stu-id="55746-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="55746-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="55746-171">relayedConnect</span></span>

<span data-ttu-id="55746-172">只要鏡像函式中的 `createRelayedServer`協助程式，`relayedConnect` 會建立用戶端連線，並在產生的通訊端上訂閱 'open' 事件。</span><span class="sxs-lookup"><span data-stu-id="55746-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="55746-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55746-173">Next steps</span></span>
<span data-ttu-id="55746-174">若要深入了解 Azure 轉送，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="55746-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="55746-175">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="55746-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="55746-176">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="55746-176">Available Relay APIs</span></span>](relay-api-overview.md)
