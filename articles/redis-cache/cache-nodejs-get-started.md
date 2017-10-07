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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="382ff-103">如何 toouse Azure Redis 快取使用 Node.js</span><span class="sxs-lookup"><span data-stu-id="382ff-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="382ff-104">.NET</span><span class="sxs-lookup"><span data-stu-id="382ff-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="382ff-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="382ff-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="382ff-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="382ff-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="382ff-107">Java</span><span class="sxs-lookup"><span data-stu-id="382ff-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="382ff-108">Python</span><span class="sxs-lookup"><span data-stu-id="382ff-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="382ff-109">Azure Redis 快取可讓您存取 tooa 安全且專用 Redis 快取中，由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="382ff-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="382ff-110">從 Microsoft Azure 內的任何應用程式都可以存取您的快取。</span><span class="sxs-lookup"><span data-stu-id="382ff-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="382ff-111">本主題說明您如何 tooget 開始使用 Azure Redis 快取使用 Node.js。</span><span class="sxs-lookup"><span data-stu-id="382ff-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="382ff-112">如需搭配使用 Azure Redis 快取與 Node.js 的另一個範例，請參閱 [在 Azure 網站上使用 Socket.IO 建置 Node.js 聊天應用程式](../app-service-web/web-sites-nodejs-chat-app-socketio.md)。</span><span class="sxs-lookup"><span data-stu-id="382ff-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="382ff-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="382ff-113">Prerequisites</span></span>
<span data-ttu-id="382ff-114">安裝 [node_redis](https://github.com/mranney/node_redis)：</span><span class="sxs-lookup"><span data-stu-id="382ff-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="382ff-115">本教學課程使用 [node_redis](https://github.com/mranney/node_redis)。</span><span class="sxs-lookup"><span data-stu-id="382ff-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="382ff-116">如需使用其他 Node.js 用戶端的範例，請參閱列在 hello Node.js 用戶端 hello 個別文件[Node.js Redis 用戶端](http://redis.io/clients#nodejs)。</span><span class="sxs-lookup"><span data-stu-id="382ff-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="382ff-117">在 Azure 上建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="382ff-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="382ff-118">擷取 hello 主機名稱和存取金鑰</span><span class="sxs-lookup"><span data-stu-id="382ff-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="382ff-119">連接 toohello 快取，安全地使用 SSL</span><span class="sxs-lookup"><span data-stu-id="382ff-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="382ff-120">最新組建 hello [node_redis](https://github.com/mranney/node_redis)連接 tooAzure Redis 快取提供支援使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="382ff-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="382ff-121">hello 下列範例示範如何使用 Redis 快取 tooconnect tooAzure hello 6380 的 SSL 端點。</span><span class="sxs-lookup"><span data-stu-id="382ff-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="382ff-122">取代`<name>`hello 名稱，為您的快取和`<key>`其中一種您的主要或次要金鑰中所述 hello 先前[擷取 hello 主機名稱和存取金鑰](#retrieve-the-host-name-and-access-keys)> 一節。</span><span class="sxs-lookup"><span data-stu-id="382ff-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="382ff-123">hello 非 SSL 連接埠已停用新的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="382ff-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="382ff-124">如果您使用不同的用戶端不支援 SSL，請參閱[tooenable hello 非 SSL 連接埠的方式](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="382ff-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="382ff-125">加入一些內容 toohello 快取並擷取它</span><span class="sxs-lookup"><span data-stu-id="382ff-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="382ff-126">下列範例會顯示您如何 tooconnect tooan Azure Redis 快取執行個體，並儲存和擷取項目從 hello 快取的 hello。</span><span class="sxs-lookup"><span data-stu-id="382ff-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="382ff-127">如需其他範例與 hello 使用 Redis 的[node_redis](https://github.com/mranney/node_redis)用戶端，請參閱[http://redis.js.org/](http://redis.js.org/)。</span><span class="sxs-lookup"><span data-stu-id="382ff-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="382ff-128">輸出：</span><span class="sxs-lookup"><span data-stu-id="382ff-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="382ff-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="382ff-129">Next steps</span></span>
* <span data-ttu-id="382ff-130">[啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)這樣您就可以[監視器](cache-how-to-monitor.md)hello 快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="382ff-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="382ff-131">讀取 hello 官方[Redis 文件](http://redis.io/documentation)。</span><span class="sxs-lookup"><span data-stu-id="382ff-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

