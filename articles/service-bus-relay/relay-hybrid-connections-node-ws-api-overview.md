---
title: "hello Azure 轉送節點 Api 的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="0bc71-103">轉送混合式連接節點 API 概觀</span><span class="sxs-lookup"><span data-stu-id="0bc71-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="0bc71-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0bc71-104">Overview</span></span>

<span data-ttu-id="0bc71-105">hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure 轉送混合式連接的節點封裝建立，並擴充 hello ['ws'](https://www.npmjs.com/package/ws) NPM 封裝。</span><span class="sxs-lookup"><span data-stu-id="0bc71-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="0bc71-106">此套件重新匯出所有都匯出的基底套件，並加入新的都匯出啟用與 hello Azure 轉送服務的混合式連線功能整合。</span><span class="sxs-lookup"><span data-stu-id="0bc71-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="0bc71-107">現有的應用程式的`require('ws')`可以使用此封裝`require('hyco-ws')`相反地，它也可讓混合式案例中的應用程式可以接聽的 WebSocket 連線從本機 「 內部 hello 防火牆 」，並透過混合式連線的所有項目hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="0bc71-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="0bc71-108">文件</span><span class="sxs-lookup"><span data-stu-id="0bc71-108">Documentation</span></span>

<span data-ttu-id="0bc71-109">hello Api 均為[記載於 hello 主要的 'ws' 封裝](https://github.com/websockets/ws/blob/master/doc/ws.md)。</span><span class="sxs-lookup"><span data-stu-id="0bc71-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="0bc71-110">本文說明此套件與該基準不同之處。</span><span class="sxs-lookup"><span data-stu-id="0bc71-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="0bc71-111">hello hello 基底套件和此 ' hyco-ws' 之間的主要差異是，它會將新的伺服器類別，透過匯出`require('hyco-ws').RelayedServer`，以及一些 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="0bc71-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="0bc71-112">套件協助程式方法</span><span class="sxs-lookup"><span data-stu-id="0bc71-112">Package helper methods</span></span>

<span data-ttu-id="0bc71-113">上都有數個公用程式方法 hello 匯出封裝，如下所示，您可以參考：</span><span class="sxs-lookup"><span data-stu-id="0bc71-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="0bc71-114">hello helper 方法適用於這個封裝，但也會用於節點伺服器啟用 web 或裝置的用戶端 toocreate 接聽程式 」 或 「 寄件者。</span><span class="sxs-lookup"><span data-stu-id="0bc71-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="0bc71-115">hello 伺服器會使用這些方法傳遞這些內嵌存留較短的語彙基元的 Uri。</span><span class="sxs-lookup"><span data-stu-id="0bc71-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="0bc71-116">這些 Uri 也可以搭配常見的 WebSocket 堆疊 hello WebSocket 交握不支援設定 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="0bc71-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="0bc71-117">授權權杖嵌入的 hello 這些程式庫外部使用方式案例的主要目的是為了支援的 URI。</span><span class="sxs-lookup"><span data-stu-id="0bc71-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="0bc71-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="0bc71-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="0bc71-119">建立的有效 Azure 轉送混合式連接接聽程式的 URI hello 命名空間和路徑。</span><span class="sxs-lookup"><span data-stu-id="0bc71-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="0bc71-120">這個 URI 可以搭配 hello 轉送版的 hello WebSocketServer 類別。</span><span class="sxs-lookup"><span data-stu-id="0bc71-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="0bc71-121">`namespaceName`（必要）-hello hello Azure 轉送命名空間 toouse 網域限定名稱。</span><span class="sxs-lookup"><span data-stu-id="0bc71-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="0bc71-122">`path`（必要）-hello 該命名空間中現有的 Azure 轉送混合式連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="0bc71-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="0bc71-123">`token`（選用）-先前發行的轉送存取權杖，內嵌在 hello 接聽程式的 URI （請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="0bc71-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="0bc71-124">`id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="0bc71-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="0bc71-125">hello`token`選擇性值，應該只用於在不可能 toosend HTTP 標頭 hello WebSocket 信號交換期間，以及使用 hello W3C WebSocket 堆疊的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="0bc71-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="0bc71-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="0bc71-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="0bc71-127">建立 hello 命名空間和路徑的有效 Azure 轉送混合式連接傳送的 URI。</span><span class="sxs-lookup"><span data-stu-id="0bc71-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="0bc71-128">這個 URI 可以搭配使用任何 WebSocket 用戶端。</span><span class="sxs-lookup"><span data-stu-id="0bc71-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="0bc71-129">`namespaceName`（必要）-hello hello Azure 轉送命名空間 toouse 網域限定名稱。</span><span class="sxs-lookup"><span data-stu-id="0bc71-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="0bc71-130">`path`（必要）-hello 該命名空間中現有的 Azure 轉送混合式連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="0bc71-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="0bc71-131">`token`（選用）-會內嵌在 hello 先前發行的轉送存取權杖傳送 URI （請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="0bc71-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="0bc71-132">`id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="0bc71-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="0bc71-133">hello`token`選擇性值，應該只用於在不可能 toosend HTTP 標頭 hello WebSocket 信號交換期間，以及使用 hello W3C WebSocket 堆疊的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="0bc71-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="0bc71-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="0bc71-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="0bc71-135">建立 Azure 轉送共用存取簽章 (SAS) 權杖 hello 指定目標 URI、 SAS 規則和適用於指定數字秒或一小時從目前的 hello 立即省略 hello 到期引數，如果 hello 的 SAS 規則索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0bc71-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="0bc71-136">`uri`（必要）-hello 的 hello 語彙基元為 toobe 發出的 URI。</span><span class="sxs-lookup"><span data-stu-id="0bc71-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="0bc71-137">hello URI 正規化的 toouse hello HTTP 配置，並不會移除查詢字串資訊。</span><span class="sxs-lookup"><span data-stu-id="0bc71-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="0bc71-138">`ruleName`（必要）-SAS 規則 hello 給定 URI，表示其中一個 hello 實體的名稱或 hello 命名空間所表示 hello URI 主機部分。</span><span class="sxs-lookup"><span data-stu-id="0bc71-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="0bc71-139">`key`（必要）-hello SAS 規則的有效索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0bc71-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="0bc71-140">`expirationSeconds`（選用）-將應過期 hello 數秒，直到 hello 產生語彙基元。</span><span class="sxs-lookup"><span data-stu-id="0bc71-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="0bc71-141">如果未指定，hello 預設會是 1 小時 (3600)。</span><span class="sxs-lookup"><span data-stu-id="0bc71-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="0bc71-142">hello 發出權杖會授與 hello hello 指定相關聯的權限指定持續時間的 hello 的 SAS 規則。</span><span class="sxs-lookup"><span data-stu-id="0bc71-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="0bc71-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="0bc71-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="0bc71-144">這個方法是相同的功能 toohello`createRelayToken`方法之前，記載，但傳回 hello 語彙基元的正確附加的 toohello 輸入 URI。</span><span class="sxs-lookup"><span data-stu-id="0bc71-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="0bc71-145">類別 ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="0bc71-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="0bc71-146">hello`hycows.RelayedServer`類別是替代的 toohello`ws.Server`類別不會接聽 hello 區域網路，但委派接聽 toohello Azure 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="0bc71-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="0bc71-147">hello 兩個類別都是大部分合約相容的也就是說，現有的應用程式使用 hello`ws.Server`類別可能很輕易就變更的 toouse hello 轉送版本。</span><span class="sxs-lookup"><span data-stu-id="0bc71-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="0bc71-148">hello 主要差異是 hello 建構函式中以及在 hello 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="0bc71-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="0bc71-149">建構函式</span><span class="sxs-lookup"><span data-stu-id="0bc71-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="0bc71-150">hello`RelayedServer`建構函式支援一組不同的引數比 hello `Server`，因為它不是獨立的接聽程式或無法 toobe 內嵌至現有的 HTTP 接聽程式架構。</span><span class="sxs-lookup"><span data-stu-id="0bc71-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="0bc71-151">也有選項較少使用因為 hello WebSocket 管理大部分委派的 toohello 轉送服務。</span><span class="sxs-lookup"><span data-stu-id="0bc71-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="0bc71-152">建構函式引數︰</span><span class="sxs-lookup"><span data-stu-id="0bc71-152">Constructor arguments:</span></span>

- <span data-ttu-id="0bc71-153">`server`（必要）-hello 完整的 URI 上的 toolisten，通常以 hello WebSocket.createRelayListenUri() helper 方法建構的混合式連接名稱。</span><span class="sxs-lookup"><span data-stu-id="0bc71-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="0bc71-154">`token`這個引數 （必要）-會保留先前發行的權杖字串或回呼函式可以呼叫 tooobtain 語彙基元字串。</span><span class="sxs-lookup"><span data-stu-id="0bc71-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="0bc71-155">hello 回撥選項，最好，因為它可讓更新權杖。</span><span class="sxs-lookup"><span data-stu-id="0bc71-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="0bc71-156">事件</span><span class="sxs-lookup"><span data-stu-id="0bc71-156">Events</span></span>

<span data-ttu-id="0bc71-157">`RelayedServer`執行個體發出三個事件，啟用您 toohandle 連入要求、 建立連接，以及偵測錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="0bc71-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="0bc71-158">您必須訂閱 toohello`connect`事件 toohandle 訊息。</span><span class="sxs-lookup"><span data-stu-id="0bc71-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="0bc71-159">headers</span><span class="sxs-lookup"><span data-stu-id="0bc71-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="0bc71-160">hello`headers`之前已接受連入連線，請啟用 hello 標頭 toosend toohello 用戶端的修改，就會引發事件。</span><span class="sxs-lookup"><span data-stu-id="0bc71-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="0bc71-161">connection</span><span class="sxs-lookup"><span data-stu-id="0bc71-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="0bc71-162">接受新的 WebSocket 連線時就會發出。</span><span class="sxs-lookup"><span data-stu-id="0bc71-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="0bc71-163">hello 物件屬於類型`ws.WebSocket`、 與 hello 基底套件相同。</span><span class="sxs-lookup"><span data-stu-id="0bc71-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="0bc71-164">錯誤</span><span class="sxs-lookup"><span data-stu-id="0bc71-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="0bc71-165">如果 hello 基礎伺服器發出錯誤，它會在這裡轉送。</span><span class="sxs-lookup"><span data-stu-id="0bc71-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="0bc71-166">協助程式</span><span class="sxs-lookup"><span data-stu-id="0bc71-166">Helpers</span></span>

<span data-ttu-id="0bc71-167">toosimplify 啟動轉送的伺服器後立即訂閱 tooincoming 連線 hello 封裝會公開簡單的 helper 函式，也會使用這個 hello 範例中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0bc71-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="0bc71-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="0bc71-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="0bc71-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="0bc71-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="0bc71-170">這個方法會呼叫 hello 建構函式 toocreate hello RelayedServer 的新執行個體，然後訂閱 hello 提供回呼 toohello 'connection' 事件。</span><span class="sxs-lookup"><span data-stu-id="0bc71-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="0bc71-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="0bc71-171">relayedConnect</span></span>

<span data-ttu-id="0bc71-172">只要鏡像 hello `createRelayedServer` helper 函式，在`relayedConnect`建立用戶端連線，並訂閱 hello 產生通訊端上的 toohello 'open' 事件。</span><span class="sxs-lookup"><span data-stu-id="0bc71-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0bc71-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bc71-173">Next steps</span></span>
<span data-ttu-id="0bc71-174">toolearn 深入了解 Azure 轉送，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="0bc71-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="0bc71-175">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="0bc71-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="0bc71-176">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="0bc71-176">Available Relay APIs</span></span>](relay-api-overview.md)
