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
# <a name="relay-hybrid-connections-node-api-overview"></a>轉送混合式連接節點 API 概觀

## <a name="overview"></a>概觀

hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure 轉送混合式連接的節點封裝建立，並擴充 hello ['ws'](https://www.npmjs.com/package/ws) NPM 封裝。 此套件重新匯出所有都匯出的基底套件，並加入新的都匯出啟用與 hello Azure 轉送服務的混合式連線功能整合。 

現有的應用程式的`require('ws')`可以使用此封裝`require('hyco-ws')`相反地，它也可讓混合式案例中的應用程式可以接聽的 WebSocket 連線從本機 「 內部 hello 防火牆 」，並透過混合式連線的所有項目hello 相同的時間。
  
## <a name="documentation"></a>文件

hello Api 均為[記載於 hello 主要的 'ws' 封裝](https://github.com/websockets/ws/blob/master/doc/ws.md)。 本文說明此套件與該基準不同之處。 

hello hello 基底套件和此 ' hyco-ws' 之間的主要差異是，它會將新的伺服器類別，透過匯出`require('hyco-ws').RelayedServer`，以及一些 helper 方法。

### <a name="package-helper-methods"></a>套件協助程式方法

上都有數個公用程式方法 hello 匯出封裝，如下所示，您可以參考：

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

hello helper 方法適用於這個封裝，但也會用於節點伺服器啟用 web 或裝置的用戶端 toocreate 接聽程式 」 或 「 寄件者。 hello 伺服器會使用這些方法傳遞這些內嵌存留較短的語彙基元的 Uri。 這些 Uri 也可以搭配常見的 WebSocket 堆疊 hello WebSocket 交握不支援設定 HTTP 標頭。 授權權杖嵌入的 hello 這些程式庫外部使用方式案例的主要目的是為了支援的 URI。 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

建立的有效 Azure 轉送混合式連接接聽程式的 URI hello 命名空間和路徑。 這個 URI 可以搭配 hello 轉送版的 hello WebSocketServer 類別。

- `namespaceName`（必要）-hello hello Azure 轉送命名空間 toouse 網域限定名稱。
- `path`（必要）-hello 該命名空間中現有的 Azure 轉送混合式連接的名稱。
- `token`（選用）-先前發行的轉送存取權杖，內嵌在 hello 接聽程式的 URI （請參閱下列範例中的 hello）。
- `id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。

hello`token`選擇性值，應該只用於在不可能 toosend HTTP 標頭 hello WebSocket 信號交換期間，以及使用 hello W3C WebSocket 堆疊的 hello 案例。                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

建立 hello 命名空間和路徑的有效 Azure 轉送混合式連接傳送的 URI。 這個 URI 可以搭配使用任何 WebSocket 用戶端。

- `namespaceName`（必要）-hello hello Azure 轉送命名空間 toouse 網域限定名稱。
- `path`（必要）-hello 該命名空間中現有的 Azure 轉送混合式連接的名稱。
- `token`（選用）-會內嵌在 hello 先前發行的轉送存取權杖傳送 URI （請參閱下列範例中的 hello）。
- `id` (選用) - 可啟用端對端診斷追蹤要求的追蹤識別碼。

hello`token`選擇性值，應該只用於在不可能 toosend HTTP 標頭 hello WebSocket 信號交換期間，以及使用 hello W3C WebSocket 堆疊的 hello 案例。                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

建立 Azure 轉送共用存取簽章 (SAS) 權杖 hello 指定目標 URI、 SAS 規則和適用於指定數字秒或一小時從目前的 hello 立即省略 hello 到期引數，如果 hello 的 SAS 規則索引鍵。

- `uri`（必要）-hello 的 hello 語彙基元為 toobe 發出的 URI。 hello URI 正規化的 toouse hello HTTP 配置，並不會移除查詢字串資訊。
- `ruleName`（必要）-SAS 規則 hello 給定 URI，表示其中一個 hello 實體的名稱或 hello 命名空間所表示 hello URI 主機部分。
- `key`（必要）-hello SAS 規則的有效索引鍵。 
- `expirationSeconds`（選用）-將應過期 hello 數秒，直到 hello 產生語彙基元。 如果未指定，hello 預設會是 1 小時 (3600)。

hello 發出權杖會授與 hello hello 指定相關聯的權限指定持續時間的 hello 的 SAS 規則。

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

這個方法是相同的功能 toohello`createRelayToken`方法之前，記載，但傳回 hello 語彙基元的正確附加的 toohello 輸入 URI。

### <a name="class-wsrelayedserver"></a>類別 ws.RelayedServer

hello`hycows.RelayedServer`類別是替代的 toohello`ws.Server`類別不會接聽 hello 區域網路，但委派接聽 toohello Azure 轉送服務。

hello 兩個類別都是大部分合約相容的也就是說，現有的應用程式使用 hello`ws.Server`類別可能很輕易就變更的 toouse hello 轉送版本。 hello 主要差異是 hello 建構函式中以及在 hello 可用的選項。

#### <a name="constructor"></a>建構函式  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

hello`RelayedServer`建構函式支援一組不同的引數比 hello `Server`，因為它不是獨立的接聽程式或無法 toobe 內嵌至現有的 HTTP 接聽程式架構。 也有選項較少使用因為 hello WebSocket 管理大部分委派的 toohello 轉送服務。

建構函式引數︰

- `server`（必要）-hello 完整的 URI 上的 toolisten，通常以 hello WebSocket.createRelayListenUri() helper 方法建構的混合式連接名稱。
- `token`這個引數 （必要）-會保留先前發行的權杖字串或回呼函式可以呼叫 tooobtain 語彙基元字串。 hello 回撥選項，最好，因為它可讓更新權杖。

#### <a name="events"></a>事件

`RelayedServer`執行個體發出三個事件，啟用您 toohandle 連入要求、 建立連接，以及偵測錯誤狀況。 您必須訂閱 toohello`connect`事件 toohandle 訊息。 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

hello`headers`之前已接受連入連線，請啟用 hello 標頭 toosend toohello 用戶端的修改，就會引發事件。 

##### <a name="connection"></a>connection

```JavaScript
function(socket)
```

接受新的 WebSocket 連線時就會發出。 hello 物件屬於類型`ws.WebSocket`、 與 hello 基底套件相同。


##### <a name="error"></a>錯誤

```JavaScript
function(error)
```

如果 hello 基礎伺服器發出錯誤，它會在這裡轉送。  

#### <a name="helpers"></a>協助程式

toosimplify 啟動轉送的伺服器後立即訂閱 tooincoming 連線 hello 封裝會公開簡單的 helper 函式，也會使用這個 hello 範例中，如下所示：

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

這個方法會呼叫 hello 建構函式 toocreate hello RelayedServer 的新執行個體，然後訂閱 hello 提供回呼 toohello 'connection' 事件。
 
##### <a name="relayedconnect"></a>relayedConnect

只要鏡像 hello `createRelayedServer` helper 函式，在`relayedConnect`建立用戶端連線，並訂閱 hello 產生通訊端上的 toohello 'open' 事件。

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

## <a name="next-steps"></a>後續步驟
toolearn 深入了解 Azure 轉送，請前往下列連結：
* [什麼是 Azure 轉送？](relay-what-is-it.md)
* [可用的轉送 API](relay-api-overview.md)
