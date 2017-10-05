---
title: "如何搭配使用 Azure Redis 快取與 Java | Microsoft Docs"
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
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="356e1-103">如何搭配使用 Azure Redis 快取與 Java</span><span class="sxs-lookup"><span data-stu-id="356e1-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="356e1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="356e1-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="356e1-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="356e1-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="356e1-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="356e1-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="356e1-107">Java</span><span class="sxs-lookup"><span data-stu-id="356e1-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="356e1-108">Python</span><span class="sxs-lookup"><span data-stu-id="356e1-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="356e1-109">Azure Redis 快取可讓您存取 Microsoft 所管理的專用 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="356e1-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="356e1-110">從 Microsoft Azure 內的任何應用程式都可以存取您的快取。</span><span class="sxs-lookup"><span data-stu-id="356e1-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="356e1-111">本主題說明如何搭配使用 Azure Redis 快取與 Java。</span><span class="sxs-lookup"><span data-stu-id="356e1-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="356e1-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="356e1-112">Prerequisites</span></span>
<span data-ttu-id="356e1-113">[Jedis](https://github.com/xetorthio/jedis) - Redis 的 Java 用戶端</span><span class="sxs-lookup"><span data-stu-id="356e1-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="356e1-114">本教學課程使用 Jedis，但是您可以使用列在 [http://redis.io/clients](http://redis.io/clients)的任何 Java 用戶端。</span><span class="sxs-lookup"><span data-stu-id="356e1-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="356e1-115">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="356e1-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="356e1-116">擷取主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="356e1-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="356e1-117">使用 SSL 安全地連接到快取</span><span class="sxs-lookup"><span data-stu-id="356e1-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="356e1-118">[jedis](https://github.com/xetorthio/jedis) 的最新組建提供了使用 SSL 連接到 Azure Redis 快取的支援。</span><span class="sxs-lookup"><span data-stu-id="356e1-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="356e1-119">下列範例示範如何使用 6380 的 SSL 端點連接到 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="356e1-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="356e1-120">以您的快取名稱取代 `<name>`，並以先前[擷取主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)一節中所述的主要或次要金鑰取代 `<key>`。</span><span class="sxs-lookup"><span data-stu-id="356e1-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="356e1-121">新的 Azure Redis 快取執行個體已停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="356e1-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="356e1-122">如果您使用不支援 SSL 的不同用戶端，請參閱[如何啟用非 SSL 連接埠](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="356e1-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="356e1-123">在快取中加入項目並擷取該項目</span><span class="sxs-lookup"><span data-stu-id="356e1-123">Add something to the cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="356e1-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="356e1-124">Next steps</span></span>
* <span data-ttu-id="356e1-125">[啟用快取診斷](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics)，以[監視](https://msdn.microsoft.com/library/azure/dn763945.aspx)您快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="356e1-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="356e1-126">閱讀官方 [Redis 文件](http://redis.io/documentation)。</span><span class="sxs-lookup"><span data-stu-id="356e1-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
