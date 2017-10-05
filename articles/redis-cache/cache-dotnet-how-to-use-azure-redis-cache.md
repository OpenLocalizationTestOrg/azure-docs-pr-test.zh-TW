---
title: "如何使用 Azure Redis 快取 | Microsoft Docs"
description: "了解如何改善與 Azure Redis 快取的 Azure 應用程式的效能"
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="76e35-103">如何使用 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="76e35-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76e35-104">.NET</span><span class="sxs-lookup"><span data-stu-id="76e35-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="76e35-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="76e35-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="76e35-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="76e35-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="76e35-107">Java</span><span class="sxs-lookup"><span data-stu-id="76e35-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="76e35-108">Python</span><span class="sxs-lookup"><span data-stu-id="76e35-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="76e35-109">本指南示範如何開始使用 **Azure Redis 快取**。</span><span class="sxs-lookup"><span data-stu-id="76e35-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="76e35-110">Microsoft Azure Redis 快取是基於受歡迎的開放原始碼 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="76e35-111">它可讓您存取由 Microsoft 管理的安全、專用 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="76e35-112">使用 Azure Redis 快取建立的快取，可透過 Microsoft Azure 內的任何應用程式加以存取。</span><span class="sxs-lookup"><span data-stu-id="76e35-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="76e35-113">Microsoft Azure Redis 快取有下列階層：</span><span class="sxs-lookup"><span data-stu-id="76e35-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="76e35-114">**基本** - 單一節點。</span><span class="sxs-lookup"><span data-stu-id="76e35-114">**Basic** – Single node.</span></span> <span data-ttu-id="76e35-115">多種大小，最高為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="76e35-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="76e35-116">**標準** – 兩個節點 (主要/從屬)。</span><span class="sxs-lookup"><span data-stu-id="76e35-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="76e35-117">多種大小，最高為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="76e35-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="76e35-118">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="76e35-118">99.9% SLA.</span></span>
* <span data-ttu-id="76e35-119">**進階** – 兩個節點的主要/從屬，最多具有 10 個分區。</span><span class="sxs-lookup"><span data-stu-id="76e35-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="76e35-120">提供多種大小，範圍從 6 GB 到 530 GB。</span><span class="sxs-lookup"><span data-stu-id="76e35-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="76e35-121">所有「標準」層級的功能以及更多功能，可支援 [Redis 叢集](cache-how-to-premium-clustering.md)、[Redis 持續性](cache-how-to-premium-persistence.md)和 [Azure 虛擬網路](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="76e35-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="76e35-122">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="76e35-122">99.9% SLA.</span></span>

<span data-ttu-id="76e35-123">每一個階層都有不同的功能和價格。</span><span class="sxs-lookup"><span data-stu-id="76e35-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="76e35-124">如需價格的相關資訊，請參閱 [快取價格詳細資料][Cache Pricing Details]。</span><span class="sxs-lookup"><span data-stu-id="76e35-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="76e35-125">本指南說明如何使用採用 C\# 程式碼的 [StackExchange.Redis][StackExchange.Redis] 用戶端。</span><span class="sxs-lookup"><span data-stu-id="76e35-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="76e35-126">涵蓋的案例包括**建立和設定快取**、**設定快取用戶端**，以及**新增和移除快取中的物件**。</span><span class="sxs-lookup"><span data-stu-id="76e35-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="76e35-127">如需使用 Azure Redis 快取的詳細資訊，請參閱 [後續步驟][Next Steps]。</span><span class="sxs-lookup"><span data-stu-id="76e35-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="76e35-128">如需使用 Redis 快取建置 ASP.NET MVC Web 應用程式的逐步教學課程，請參閱 [如何使用 Redis 快取建立 Web 應用程式](cache-web-app-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="76e35-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="76e35-129">開始使用 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="76e35-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="76e35-130">開始使用 Azure Redis 快取相當簡單。</span><span class="sxs-lookup"><span data-stu-id="76e35-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="76e35-131">若要開始，請佈建並設定快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="76e35-132">接著，設定快取用戶端，以便它們可以存取快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="76e35-133">一旦設定了快取用戶端，就可以開始使用它們。</span><span class="sxs-lookup"><span data-stu-id="76e35-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="76e35-134">[建立快取][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="76e35-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="76e35-135">[設定快取用戶端][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="76e35-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="76e35-136">建立快取</span><span class="sxs-lookup"><span data-stu-id="76e35-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="76e35-137">在建立好之後存取快取</span><span class="sxs-lookup"><span data-stu-id="76e35-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="76e35-138">如需設定快取的詳細資訊，請參閱 [如何設定 Azure Redis 快取](cache-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="76e35-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="76e35-139">設定快取用戶端</span><span class="sxs-lookup"><span data-stu-id="76e35-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="76e35-140">一旦設定用戶端專案的快取功能，您就可以使用下列幾節中描述的技術來使用快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="76e35-141">使用快取</span><span class="sxs-lookup"><span data-stu-id="76e35-141">Working with Caches</span></span>
<span data-ttu-id="76e35-142">本節中的步驟描述如何利用快取執行常見工作。</span><span class="sxs-lookup"><span data-stu-id="76e35-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="76e35-143">[連接到快取][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="76e35-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="76e35-144">[從快取新增和擷取物件][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="76e35-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="76e35-145">使用快取中的 .NET 物件</span><span class="sxs-lookup"><span data-stu-id="76e35-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="76e35-146">連接到快取</span><span class="sxs-lookup"><span data-stu-id="76e35-146">Connect to the cache</span></span>
<span data-ttu-id="76e35-147">若要以程式設計方式使用快取，您需要快取的參考。</span><span class="sxs-lookup"><span data-stu-id="76e35-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="76e35-148">將下面這一行加入至您想要從中使用 StackExchange.Redis 用戶端來存取 Azure Redis 快取之檔案的頂端。</span><span class="sxs-lookup"><span data-stu-id="76e35-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="76e35-149">StackExchange.Redis 用戶端需要 .NET Framework 4 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="76e35-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="76e35-150">與 Azure Redis 快取的連線是由 `ConnectionMultiplexer` 類別所管理。</span><span class="sxs-lookup"><span data-stu-id="76e35-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="76e35-151">此類別應要在用戶端應用程式中共用和重複使用，而不需要依據每個作業加以建立。</span><span class="sxs-lookup"><span data-stu-id="76e35-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="76e35-152">若要連線至 Azure Redis 快取，並傳回已連線 `ConnectionMultiplexer` 的執行個體，請呼叫靜態 `Connect` 方法，並傳入快取端點和金鑰。</span><span class="sxs-lookup"><span data-stu-id="76e35-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="76e35-153">使用從 Azure 入口網站產生的金鑰做為密碼參數。</span><span class="sxs-lookup"><span data-stu-id="76e35-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="76e35-154">警告：請勿將認證儲存在原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="76e35-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="76e35-155">為了讓這個範例簡單明瞭，我會以原始程式碼來呈現認證內容。</span><span class="sxs-lookup"><span data-stu-id="76e35-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="76e35-156">如需如何儲存認證的相關資訊，請參閱[應用程式字串與連接字串的運作方式][How Application Strings and Connection Strings Work]。</span><span class="sxs-lookup"><span data-stu-id="76e35-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="76e35-157">如果您不想使用 SSL，請設定 `ssl=false` 或省略 `ssl` 參數。</span><span class="sxs-lookup"><span data-stu-id="76e35-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="76e35-158">預設會為新快取停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="76e35-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="76e35-159">如需啟用非 SSL 連接埠的指示，請參閱[存取連接埠](cache-configure.md#access-ports)。</span><span class="sxs-lookup"><span data-stu-id="76e35-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="76e35-160">在您的應用程式中共用 `ConnectionMultiplexer` 執行個體的其中一種方法，就是擁有可傳回已連接執行個體的靜態屬性，類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="76e35-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="76e35-161">此方法提供安全執行緒方式，只初始化單一已連接的 `ConnectionMultiplexer` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="76e35-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="76e35-162">在這些範例中， `abortConnect` 已設為 false，這表示即使無法建立與 Azure Redis 快取的連線，呼叫也會成功。</span><span class="sxs-lookup"><span data-stu-id="76e35-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="76e35-163">`ConnectionMultiplexer` 的主要功能之一，就是一旦網路問題或其他原因獲得解決，它就會自動恢復與快取的連接。</span><span class="sxs-lookup"><span data-stu-id="76e35-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="76e35-164">如需進階連線組態選項的詳細資訊，請參閱 [StackExchange.Redis 組態模型][StackExchange.Redis configuration model]。</span><span class="sxs-lookup"><span data-stu-id="76e35-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="76e35-165">一旦建立連線，即會透過呼叫 `ConnectionMultiplexer.GetDatabase` 方法傳回 Redis 快取資料庫的參考。</span><span class="sxs-lookup"><span data-stu-id="76e35-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="76e35-166">透過 `GetDatabase` 方法傳回的物件是輕量型傳遞物件，而且不需要儲存。</span><span class="sxs-lookup"><span data-stu-id="76e35-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="76e35-167">Azure Redis 快取具有可供用來以邏輯方式區隔 Redis 快取內資料的可設定數目資料庫 (預設值為 16 個)。</span><span class="sxs-lookup"><span data-stu-id="76e35-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="76e35-168">如需詳細資訊，請參閱 [Redis 資料庫是什麼？](cache-faq.md#what-are-redis-databases)和[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="76e35-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="76e35-169">現在您知道如何連線至 Azure Redis 快取執行個體，並傳回快取資料庫的參考，讓我們來看看如何使用快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="76e35-170">從快取新增和擷取物件</span><span class="sxs-lookup"><span data-stu-id="76e35-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="76e35-171">您可以使用 `StringSet` 和 `StringGet` 方法，在快取中儲存或擷取項目。</span><span class="sxs-lookup"><span data-stu-id="76e35-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="76e35-172">Redis 會將多數資料儲存為 Redis 字串，但這些字串可能包含許多類型的資料，包括序列化的二進位資料 (在快取中儲存 .NET 物件時可能會用到)。</span><span class="sxs-lookup"><span data-stu-id="76e35-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="76e35-173">呼叫 `StringGet` 時，如果物件已存在，即會傳回，如果物件不存在，則會傳回 `null`。</span><span class="sxs-lookup"><span data-stu-id="76e35-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="76e35-174">如果傳回 `null`，您可以從需要的資料來源中擷取值，並將它儲存在快取中供後續使用。</span><span class="sxs-lookup"><span data-stu-id="76e35-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="76e35-175">這種使用模式稱為另行快取模式。</span><span class="sxs-lookup"><span data-stu-id="76e35-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="76e35-176">您也可以使用 `RedisValue`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="76e35-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="76e35-177">`RedisValue` 有隱含的運算子適用於整數資料類型，而如果 `null` 是預期的快取項目值則很實用。</span><span class="sxs-lookup"><span data-stu-id="76e35-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="76e35-178">若要指定快取中項目的到期時間，請使用 `StringSet` 的 `TimeSpan` 參數。</span><span class="sxs-lookup"><span data-stu-id="76e35-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="76e35-179">使用快取中的 .NET 物件</span><span class="sxs-lookup"><span data-stu-id="76e35-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="76e35-180">Azure Redis 快取可以快取 .NET 物件及基本資料類型，但必須先將 .NET 物件序列化，才能加以快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="76e35-181">.NET 物件序列化是應用程式開發人員的責任，同時賦與開發人員選擇序列化程式的彈性。</span><span class="sxs-lookup"><span data-stu-id="76e35-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="76e35-182">將物件序列化的其中一個簡單方法就是使用 [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) 中的 `JsonConvert` 序列化方法並進行 JSON 的雙向序列化。</span><span class="sxs-lookup"><span data-stu-id="76e35-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="76e35-183">下列範例使用 `Employee` 物件執行個體顯示 get 和 set。</span><span class="sxs-lookup"><span data-stu-id="76e35-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="76e35-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76e35-184">Next Steps</span></span>
<span data-ttu-id="76e35-185">了解基礎概念之後，請依照下列連結深入了解 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="76e35-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="76e35-186">查看 Azure Redis 快取的 ASP.NET 提供者。</span><span class="sxs-lookup"><span data-stu-id="76e35-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="76e35-187">Azure Redis 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="76e35-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="76e35-188">Azure Redis 快取 ASP.NET 輸出快取提供者</span><span class="sxs-lookup"><span data-stu-id="76e35-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="76e35-189">[啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)，以[監視](cache-how-to-monitor.md)您快取的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="76e35-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="76e35-190">您可以在 Azure 入口網站中檢視度量，也可以使用您選擇的工具 [下載並檢閱](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 它們。</span><span class="sxs-lookup"><span data-stu-id="76e35-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="76e35-191">請參閱 [StackExchange.Redis 快取用戶端文件][StackExchange.Redis cache client documentation]。</span><span class="sxs-lookup"><span data-stu-id="76e35-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="76e35-192">Azure Redis 快取可以透過許多 Redis 用戶端和開發語言進行存取。</span><span class="sxs-lookup"><span data-stu-id="76e35-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="76e35-193">如需詳細資訊，請參閱 [http://redis.io/clients][http://redis.io/clients]。</span><span class="sxs-lookup"><span data-stu-id="76e35-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="76e35-194">Azure Redis 快取也可以與協力廠商服務和工具搭配使用 (例如 Redsmin 和 Redis Desktop Manager)。</span><span class="sxs-lookup"><span data-stu-id="76e35-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="76e35-195">如需 Redsmin 的詳細資訊，請參閱 [如何擷取 Azure Redis 連接字串並將它與 Redsmin 搭配使用][How to retrieve an Azure Redis connection string and use it with Redsmin]。</span><span class="sxs-lookup"><span data-stu-id="76e35-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="76e35-196">使用 [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)，透過 GUI 存取和檢查 Azure Redis 快取中的資料。</span><span class="sxs-lookup"><span data-stu-id="76e35-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="76e35-197">請參閱 [redis][redis] 文件，並閱讀有關 [Redis 資料類型][redis data types]和 [Redis 資料類型的 15 分鐘簡介][a fifteen minute introduction to Redis data types]。</span><span class="sxs-lookup"><span data-stu-id="76e35-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


