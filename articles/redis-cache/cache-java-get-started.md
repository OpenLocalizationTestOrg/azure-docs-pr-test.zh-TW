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
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="6760f-103">如何 toouse Azure Redis 快取 java</span><span class="sxs-lookup"><span data-stu-id="6760f-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6760f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6760f-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="6760f-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6760f-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="6760f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="6760f-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="6760f-107">Java</span><span class="sxs-lookup"><span data-stu-id="6760f-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="6760f-108">Python</span><span class="sxs-lookup"><span data-stu-id="6760f-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="6760f-109">Azure Redis 快取可讓您存取 tooa 專用 Redis 快取中，由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="6760f-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="6760f-110">從 Microsoft Azure 內的任何應用程式都可以存取您的快取。</span><span class="sxs-lookup"><span data-stu-id="6760f-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="6760f-111">本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Java。</span><span class="sxs-lookup"><span data-stu-id="6760f-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6760f-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="6760f-112">Prerequisites</span></span>
<span data-ttu-id="6760f-113">[Jedis](https://github.com/xetorthio/jedis) - Redis 的 Java 用戶端</span><span class="sxs-lookup"><span data-stu-id="6760f-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="6760f-114">本教學課程使用 Jedis，但是您可以使用列在 [http://redis.io/clients](http://redis.io/clients)的任何 Java 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6760f-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="6760f-115">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="6760f-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="6760f-116">擷取 hello 主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="6760f-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="6760f-117">連接 toohello 快取，安全地使用 SSL</span><span class="sxs-lookup"><span data-stu-id="6760f-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="6760f-118">最新組建 hello [jedis](https://github.com/xetorthio/jedis)連接 tooAzure Redis 快取提供支援使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="6760f-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="6760f-119">hello 下列範例示範如何使用 Redis 快取 tooconnect tooAzure hello 6380 的 SSL 端點。</span><span class="sxs-lookup"><span data-stu-id="6760f-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="6760f-120">取代`<name>`hello 名稱，為您的快取和`<key>`其中一種您的主要或次要金鑰中所述 hello 先前[擷取 hello 主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6760f-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="6760f-121">hello 非 SSL 連接埠已停用新的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="6760f-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="6760f-122">如果您使用不同的用戶端不支援 SSL，請參閱[tooenable hello 非 SSL 連接埠的方式](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="6760f-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="6760f-123">加入一些內容 toohello 快取並擷取它</span><span class="sxs-lookup"><span data-stu-id="6760f-123">Add something toohello cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="6760f-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6760f-124">Next steps</span></span>
* <span data-ttu-id="6760f-125">[啟用快取診斷](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics)這樣您就可以[監視器](https://msdn.microsoft.com/library/azure/dn763945.aspx)hello 快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="6760f-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="6760f-126">讀取 hello 官方[Redis 文件](http://redis.io/documentation)。</span><span class="sxs-lookup"><span data-stu-id="6760f-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
