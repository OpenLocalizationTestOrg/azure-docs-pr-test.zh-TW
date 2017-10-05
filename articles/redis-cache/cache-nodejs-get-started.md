---
title: "如何搭配使用 Azure Redis 快取與 Node.js | Microsoft Docs"
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
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="e7448-103">如何搭配使用 Azure Redis 快取與 Node.js</span><span class="sxs-lookup"><span data-stu-id="e7448-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7448-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e7448-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="e7448-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e7448-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="e7448-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e7448-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="e7448-107">Java</span><span class="sxs-lookup"><span data-stu-id="e7448-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="e7448-108">Python</span><span class="sxs-lookup"><span data-stu-id="e7448-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="e7448-109">Azure Redis 快取可讓您存取 Microsoft 所管理的專用安全 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="e7448-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="e7448-110">從 Microsoft Azure 內的任何應用程式都可以存取您的快取。</span><span class="sxs-lookup"><span data-stu-id="e7448-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="e7448-111">本主題說明如何開始搭配使用 Azure Redis 快取與 Node.js。</span><span class="sxs-lookup"><span data-stu-id="e7448-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="e7448-112">如需搭配使用 Azure Redis 快取與 Node.js 的另一個範例，請參閱 [在 Azure 網站上使用 Socket.IO 建置 Node.js 聊天應用程式](../app-service-web/web-sites-nodejs-chat-app-socketio.md)。</span><span class="sxs-lookup"><span data-stu-id="e7448-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7448-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7448-113">Prerequisites</span></span>
<span data-ttu-id="e7448-114">安裝 [node_redis](https://github.com/mranney/node_redis)：</span><span class="sxs-lookup"><span data-stu-id="e7448-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="e7448-115">本教學課程使用 [node_redis](https://github.com/mranney/node_redis)。</span><span class="sxs-lookup"><span data-stu-id="e7448-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="e7448-116">如需使用其他 Node.js 用戶端的範例，請參閱列在 [Node.js Redis 用戶端](http://redis.io/clients#nodejs)之 Node.js 用戶端的個別文件。</span><span class="sxs-lookup"><span data-stu-id="e7448-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e7448-117">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="e7448-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="e7448-118">擷取主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="e7448-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="e7448-119">使用 SSL 安全地連接到快取</span><span class="sxs-lookup"><span data-stu-id="e7448-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="e7448-120">[node_redis](https://github.com/mranney/node_redis) 的最新組建提供了使用 SSL 連接到 Azure Redis 快取的支援。</span><span class="sxs-lookup"><span data-stu-id="e7448-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="e7448-121">下列範例示範如何使用 6380 的 SSL 端點連接到 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="e7448-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="e7448-122">以您的快取名稱取代 `<name>`，並以先前[擷取主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)一節中所述的主要或次要金鑰取代 `<key>`。</span><span class="sxs-lookup"><span data-stu-id="e7448-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="e7448-123">新的 Azure Redis 快取執行個體已停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="e7448-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="e7448-124">如果您使用不支援 SSL 的不同用戶端，請參閱[如何啟用非 SSL 連接埠](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="e7448-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="e7448-125">在快取中加入項目並擷取該項目</span><span class="sxs-lookup"><span data-stu-id="e7448-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="e7448-126">下列範例示範如何連接到 Azure Redis 快取執行個體，以及儲存和擷取快取中的項目。</span><span class="sxs-lookup"><span data-stu-id="e7448-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="e7448-127">如需更多搭配使用 Redis 與 [node_redis](https://github.com/mranney/node_redis) 用戶端的範例，請參閱 [http://redis.js.org/](http://redis.js.org/)。</span><span class="sxs-lookup"><span data-stu-id="e7448-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="e7448-128">輸出：</span><span class="sxs-lookup"><span data-stu-id="e7448-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="e7448-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7448-129">Next steps</span></span>
* <span data-ttu-id="e7448-130">[啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)，以[監視](cache-how-to-monitor.md)您快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7448-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="e7448-131">閱讀官方 [Redis 文件](http://redis.io/documentation)。</span><span class="sxs-lookup"><span data-stu-id="e7448-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

