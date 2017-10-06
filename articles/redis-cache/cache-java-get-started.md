---
title: "aaaHow toouse java 的 Azure Redis 快取 |Microsoft 文件"
description: "開始搭配使用 Azure Redis 快取與 Java"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a>如何 toouse Azure Redis 快取 java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Redis 快取可讓您存取 tooa 專用 Redis 快取中，由 Microsoft 管理。 從 Microsoft Azure 內的任何應用程式都可以存取您的快取。

本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Java。

## <a name="prerequisites"></a>必要條件
[Jedis](https://github.com/xetorthio/jedis) - Redis 的 Java 用戶端

本教學課程使用 Jedis，但是您可以使用列在 [http://redis.io/clients](http://redis.io/clients)的任何 Java 用戶端。

## <a name="create-a-redis-cache-on-azure"></a>在 Azure 上建立 Redis 快取
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>擷取 hello 主機名稱和存取金鑰
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>連接 toohello 快取，安全地使用 SSL
最新組建 hello [jedis](https://github.com/xetorthio/jedis)連接 tooAzure Redis 快取提供支援使用 SSL。 hello 下列範例示範如何使用 Redis 快取 tooconnect tooAzure hello 6380 的 SSL 端點。 取代`<name>`hello 名稱，為您的快取和`<key>`其中一種您的主要或次要金鑰中所述 hello 先前[擷取 hello 主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)> 一節。

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> hello 非 SSL 連接埠已停用新的 Azure Redis 快取執行個體。 如果您使用不同的用戶端不支援 SSL，請參閱[tooenable hello 非 SSL 連接埠的方式](cache-configure.md#access-ports)。
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>加入一些內容 toohello 快取並擷取它
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a>後續步驟
* [啟用快取診斷](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics)這樣您就可以[監視器](https://msdn.microsoft.com/library/azure/dn763945.aspx)hello 快取的健全狀況。
* 讀取 hello 官方[Redis 文件](http://redis.io/documentation)。
