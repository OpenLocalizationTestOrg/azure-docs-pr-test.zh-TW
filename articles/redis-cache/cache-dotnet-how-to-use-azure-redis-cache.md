---
title: "aaaHow tooUse Azure Redis 快取 |Microsoft 文件"
description: "了解如何 tooimprove hello Azure Redis 快取與 Azure 應用程式的效能"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="6f07b-103">如何 tooUse Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="6f07b-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f07b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6f07b-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="6f07b-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6f07b-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="6f07b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="6f07b-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="6f07b-107">Java</span><span class="sxs-lookup"><span data-stu-id="6f07b-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="6f07b-108">Python</span><span class="sxs-lookup"><span data-stu-id="6f07b-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="6f07b-109">本指南也說明如何 tooget 啟動使用**Azure Redis 快取**。</span><span class="sxs-lookup"><span data-stu-id="6f07b-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="6f07b-110">Microsoft Azure Redis 快取根據 hello 熱門開放原始碼 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="6f07b-111">它可讓您存取 tooa 安全且專用 Redis 快取中，由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="6f07b-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="6f07b-112">使用 Azure Redis 快取建立的快取，可透過 Microsoft Azure 內的任何應用程式加以存取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="6f07b-113">Microsoft Azure Redis 快取位於下列層 hello:</span><span class="sxs-lookup"><span data-stu-id="6f07b-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="6f07b-114">**基本** - 單一節點。</span><span class="sxs-lookup"><span data-stu-id="6f07b-114">**Basic** – Single node.</span></span> <span data-ttu-id="6f07b-115">多個向上 too53 GB 的大小。</span><span class="sxs-lookup"><span data-stu-id="6f07b-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="6f07b-116">**標準** – 兩個節點 (主要/從屬)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="6f07b-117">多個向上 too53 GB 的大小。</span><span class="sxs-lookup"><span data-stu-id="6f07b-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="6f07b-118">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="6f07b-118">99.9% SLA.</span></span>
* <span data-ttu-id="6f07b-119">**Premium** – 雙節點主要/複本向上 too10 分區。</span><span class="sxs-lookup"><span data-stu-id="6f07b-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="6f07b-120">多個大小為 6 GB too530 GB。</span><span class="sxs-lookup"><span data-stu-id="6f07b-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="6f07b-121">所有「標準」層級的功能以及更多功能，可支援 [Redis 叢集](cache-how-to-premium-clustering.md)、[Redis 持續性](cache-how-to-premium-persistence.md)和 [Azure 虛擬網路](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="6f07b-122">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="6f07b-122">99.9% SLA.</span></span>

<span data-ttu-id="6f07b-123">每一個階層都有不同的功能和價格。</span><span class="sxs-lookup"><span data-stu-id="6f07b-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="6f07b-124">如需價格的相關資訊，請參閱 [快取價格詳細資料][Cache Pricing Details]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="6f07b-125">本指南也說明如何 toouse hello [StackExchange.Redis] [ StackExchange.Redis]用戶端會使用 C\#程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f07b-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="6f07b-126">hello 涵蓋案例包括**建立和設定快取**，**設定快取用戶端**，和**中新增和移除物件 hello 快取**。</span><span class="sxs-lookup"><span data-stu-id="6f07b-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="6f07b-127">如需使用 Azure Redis 快取的詳細資訊，請參閱 [後續步驟][Next Steps]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="6f07b-128">建立 ASP.NET MVC web 應用程式使用 Redis 快取的逐步教學課程中，請參閱[如何 toocreate Web 應用程式使用 Redis 快取](cache-web-app-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="6f07b-129">開始使用 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="6f07b-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="6f07b-130">開始使用 Azure Redis 快取相當簡單。</span><span class="sxs-lookup"><span data-stu-id="6f07b-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="6f07b-131">tooget 啟動，您的佈建和設定快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="6f07b-132">接下來，讓他們可以存取 hello 快取設定 hello 快取用戶端。</span><span class="sxs-lookup"><span data-stu-id="6f07b-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="6f07b-133">一旦設定 hello 快取用戶端，您可以開始使用它們。</span><span class="sxs-lookup"><span data-stu-id="6f07b-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="6f07b-134">[建立 hello 快取][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="6f07b-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="6f07b-135">[設定 hello 快取用戶端][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="6f07b-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="6f07b-136">建立快取</span><span class="sxs-lookup"><span data-stu-id="6f07b-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="6f07b-137">您的快取之後，它會建立 tooaccess</span><span class="sxs-lookup"><span data-stu-id="6f07b-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="6f07b-138">如需有關設定快取的詳細資訊，請參閱[如何 tooconfigure Azure Redis 快取](cache-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="6f07b-139">設定 hello 快取用戶端</span><span class="sxs-lookup"><span data-stu-id="6f07b-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="6f07b-140">一旦用戶端專案設定為快取，您可以使用 hello 下列各節以使用您的快取中所述的 hello 技巧。</span><span class="sxs-lookup"><span data-stu-id="6f07b-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="6f07b-141">使用快取</span><span class="sxs-lookup"><span data-stu-id="6f07b-141">Working with Caches</span></span>
<span data-ttu-id="6f07b-142">本節中的 hello 步驟說明 tooperform 一般快取的工作。</span><span class="sxs-lookup"><span data-stu-id="6f07b-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="6f07b-143">[連接 toohello 快取][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="6f07b-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="6f07b-144">[新增和從 hello 快取擷取物件][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="6f07b-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="6f07b-145">使用 hello 快取中的.NET 物件</span><span class="sxs-lookup"><span data-stu-id="6f07b-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="6f07b-146">連接 toohello 快取</span><span class="sxs-lookup"><span data-stu-id="6f07b-146">Connect toohello cache</span></span>
<span data-ttu-id="6f07b-147">tooprogrammatically 工作與快取，您需要參考 toohello 快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="6f07b-148">新增 hello 遵循 toohello 前要 toouse hello StackExchange.Redis 用戶端 tooaccess Azure Redis 快取的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="6f07b-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="6f07b-149">hello StackExchange.Redis 用戶端需要.NET Framework 4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6f07b-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="6f07b-150">hello Azure Redis 快取受 hello 連接 toohello`ConnectionMultiplexer`類別。</span><span class="sxs-lookup"><span data-stu-id="6f07b-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="6f07b-151">這個類別應該共用和在用戶端應用程式中重複使用，而且不需要 toobe 依作業基礎上建立。</span><span class="sxs-lookup"><span data-stu-id="6f07b-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="6f07b-152">tooconnect tooan Azure Redis 快取，且已連接的執行個體傳回`ConnectionMultiplexer`，呼叫 hello 靜態`Connect`方法並傳入 hello 快取端點和金鑰。</span><span class="sxs-lookup"><span data-stu-id="6f07b-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="6f07b-153">使用 hello hello hello password 參數為 Azure 入口網站所產生的金鑰。</span><span class="sxs-lookup"><span data-stu-id="6f07b-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="6f07b-154">警告：請勿將認證儲存在原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="6f07b-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="6f07b-155">tookeep 此範例簡單，我有顯示它們 hello 原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="6f07b-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="6f07b-156">請參閱[如何應用程式字串與連接字串工作][ How Application Strings and Connection Strings Work]如需詳細資訊 toostore 認證。</span><span class="sxs-lookup"><span data-stu-id="6f07b-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="6f07b-157">如果您不想 toouse SSL，請將`ssl=false`或省略 hello`ssl`參數。</span><span class="sxs-lookup"><span data-stu-id="6f07b-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="6f07b-158">新的快取預設為停用 hello 非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6f07b-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="6f07b-159">如需啟用 hello 非 SSL 連接埠的指示，請參閱[存取連接埠](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="6f07b-160">其中一個方法 toosharing`ConnectionMultiplexer`應用程式中的執行個體是 toohave 傳回連接的執行個體，下列範例類似 toohello 的靜態屬性。</span><span class="sxs-lookup"><span data-stu-id="6f07b-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="6f07b-161">此方法提供的執行緒安全的方式 tooinitialize 僅連接單一`ConnectionMultiplexer`執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f07b-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="6f07b-162">這些範例中`abortConnect`是集 toofalse，這表示即使不會建立連接 toohello Azure Redis 快取，hello 呼叫會成功。</span><span class="sxs-lookup"><span data-stu-id="6f07b-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="6f07b-163">一項重要功能`ConnectionMultiplexer`是它會自動還原連線 toohello 快取，一旦 hello 網路問題或其他原因，在解決。</span><span class="sxs-lookup"><span data-stu-id="6f07b-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="6f07b-164">如需進階連線組態選項的詳細資訊，請參閱 [StackExchange.Redis 組態模型][StackExchange.Redis configuration model]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="6f07b-165">一旦建立 hello 連線之後，傳回參考 toohello redis 快取資料庫呼叫 hello`ConnectionMultiplexer.GetDatabase`方法。</span><span class="sxs-lookup"><span data-stu-id="6f07b-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="6f07b-166">傳回的 hello hello 物件`GetDatabase`方法是輕量的傳遞物件，而且不需要 toobe 儲存。</span><span class="sxs-lookup"><span data-stu-id="6f07b-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="6f07b-167">Azure Redis 快取有可以是使用的 toologically Redis 快取內的個別 hello 資料的資料庫 （預設值為 16） 可設定的數目。</span><span class="sxs-lookup"><span data-stu-id="6f07b-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="6f07b-168">如需詳細資訊，請參閱 [Redis 資料庫是什麼？](cache-faq.md#what-are-redis-databases)和[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="6f07b-169">您現在知道如何 tooconnect tooan Azure Redis 快取執行個體並傳回參考 toohello 快取資料庫，讓我們看看使用 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="6f07b-170">新增和從 hello 快取擷取物件</span><span class="sxs-lookup"><span data-stu-id="6f07b-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="6f07b-171">可以儲存在與使用 hello 從快取擷取項目`StringSet`和`StringGet`方法。</span><span class="sxs-lookup"><span data-stu-id="6f07b-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="6f07b-172">Redis 大部分的資料，做為 Redis 字串，但這些字串可以包含許多類型的資料，包括序列化的二進位資料，可用於儲存.NET 物件時 hello 快取存放區。</span><span class="sxs-lookup"><span data-stu-id="6f07b-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="6f07b-173">呼叫時`StringGet`，如果 hello 物件存在，則會傳回，而且如果沒有，`null`傳回。</span><span class="sxs-lookup"><span data-stu-id="6f07b-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="6f07b-174">如果`null`傳回時，您可以從 hello 所需的資料來源擷取 hello 值，並將它儲存在 hello 快取供後續使用。</span><span class="sxs-lookup"><span data-stu-id="6f07b-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="6f07b-175">此使用方式的模式稱為 hello 另行快取模式。</span><span class="sxs-lookup"><span data-stu-id="6f07b-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="6f07b-176">您也可以使用`RedisValue`hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6f07b-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="6f07b-177">`RedisValue` 有隱含的運算子適用於整數資料類型，而如果 `null` 是預期的快取項目值則很實用。</span><span class="sxs-lookup"><span data-stu-id="6f07b-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="6f07b-178">hello 快取中，使用 hello 項目的 toospecify hello 到期`TimeSpan`參數`StringSet`。</span><span class="sxs-lookup"><span data-stu-id="6f07b-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="6f07b-179">使用 hello 快取中的.NET 物件</span><span class="sxs-lookup"><span data-stu-id="6f07b-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="6f07b-180">Azure Redis 快取可以快取 .NET 物件及基本資料類型，但必須先將 .NET 物件序列化，才能加以快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="6f07b-181">這個.NET 物件序列化 hello 責任 hello 應用程式開發人員，並且讓 hello 開發人員彈性 hello 選擇 hello 序列化程式。</span><span class="sxs-lookup"><span data-stu-id="6f07b-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="6f07b-182">一個簡單的方式 tooserialize 物件為 toouse hello`JsonConvert`中的序列化方法[Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1)和序列化 tooand 從 JSON。</span><span class="sxs-lookup"><span data-stu-id="6f07b-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="6f07b-183">hello 下列範例示範 get 和 set 使用`Employee`物件執行個體。</span><span class="sxs-lookup"><span data-stu-id="6f07b-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="6f07b-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f07b-184">Next Steps</span></span>
<span data-ttu-id="6f07b-185">既然您已經學會 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="6f07b-186">簽出 hello Azure Redis 快取的 ASP.NET 提供者。</span><span class="sxs-lookup"><span data-stu-id="6f07b-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="6f07b-187">Azure Redis 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="6f07b-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="6f07b-188">Azure Redis 快取 ASP.NET 輸出快取提供者</span><span class="sxs-lookup"><span data-stu-id="6f07b-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="6f07b-189">[啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)這樣您就可以[監視器](cache-how-to-monitor.md)hello 快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="6f07b-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="6f07b-190">您可以檢視度量 hello Azure 入口網站，而且也可以的 hello[下載並檢閱](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)它們使用您選擇的 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="6f07b-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="6f07b-191">簽出 hello [StackExchange.Redis 快取的用戶端文件][StackExchange.Redis cache client documentation]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="6f07b-192">Azure Redis 快取可以透過許多 Redis 用戶端和開發語言進行存取。</span><span class="sxs-lookup"><span data-stu-id="6f07b-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="6f07b-193">如需詳細資訊，請參閱 [http://redis.io/clients][http://redis.io/clients]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="6f07b-194">Azure Redis 快取也可以與協力廠商服務和工具搭配使用 (例如 Redsmin 和 Redis Desktop Manager)。</span><span class="sxs-lookup"><span data-stu-id="6f07b-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="6f07b-195">如需 Redsmin 的詳細資訊，請參閱[如何 tooretrieve Azure Redis 的連接字串，並使用它搭配 Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="6f07b-196">使用 [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)，透過 GUI 存取和檢查 Azure Redis 快取中的資料。</span><span class="sxs-lookup"><span data-stu-id="6f07b-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="6f07b-197">請參閱 hello [redis] [ redis]文件，並了解[redis 資料型別][ redis data types]和[十五分鐘簡介tooRedis 資料型別][a fifteen minute introduction tooRedis data types]。</span><span class="sxs-lookup"><span data-stu-id="6f07b-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


