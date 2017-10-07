---
title: "aaaHow toouse 使用 Node.js 的 Azure Redis 快取 |Microsoft 文件"
description: "開始搭配使用 Azure Redis 快取與 Node.js 和 node_redis。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>如何 toouse Azure Redis 快取使用 Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis 快取可讓您存取 tooa 安全且專用 Redis 快取中，由 Microsoft 管理。 從 Microsoft Azure 內的任何應用程式都可以存取您的快取。

本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Node.js。 如需搭配使用 Azure Redis 快取與 Node.js 的另一個範例，請參閱 [在 Azure 網站上使用 Socket.IO 建置 Node.js 聊天應用程式](../app-service-web/web-sites-nodejs-chat-app-socketio.md)。

## <a name="prerequisites"></a>必要條件
安裝 [node_redis](https://github.com/mranney/node_redis)：

    npm install redis

本教學課程使用 [node_redis](https://github.com/mranney/node_redis)。 如需使用其他 Node.js 用戶端的範例，請參閱列在 hello Node.js 用戶端 hello 個別文件[Node.js Redis 用戶端](http://redis.io/clients#nodejs)。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上建立 Redis 快取
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>擷取 hello 主機名稱和存取金鑰
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>連接 toohello 快取，安全地使用 SSL
最新組建 hello [node_redis](https://github.com/mranney/node_redis)連接 tooAzure Redis 快取提供支援使用 SSL。 hello 下列範例示範如何使用 Redis 快取 tooconnect tooAzure hello 6380 的 SSL 端點。 取代`<name>`hello 名稱，為您的快取和`<key>`其中一種您的主要或次要金鑰中所述 hello 先前[擷取 hello 主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)> 一節。

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> hello 非 SSL 連接埠已停用新的 Azure Redis 快取執行個體。 如果您使用不同的用戶端不支援 SSL，請參閱[tooenable hello 非 SSL 連接埠的方式](cache-configure.md#access-ports)。
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>加入一些內容 toohello 快取並擷取它
下列範例會顯示您如何 tooconnect tooan Azure Redis 快取執行個體，並儲存和擷取項目從 hello 快取的 hello。 如需其他範例與 hello 使用 Redis 的[node_redis](https://github.com/mranney/node_redis)用戶端，請參閱[http://redis.js.org/](http://redis.js.org/)。

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

輸出：

    OK
    value


## <a name="next-steps"></a>後續步驟
* [啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)這樣您就可以[監視器](cache-how-to-monitor.md)hello 快取的健全狀況。
* 讀取 hello 官方[Redis 文件](http://redis.io/documentation)。

