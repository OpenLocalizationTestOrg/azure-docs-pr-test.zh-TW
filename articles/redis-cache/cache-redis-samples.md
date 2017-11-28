---
title: "aaaAzure Redis 快取範例 |Microsoft 文件"
description: "了解如何 toouse Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a><span data-ttu-id="efa58-103">Azure Redis 快取範例</span><span class="sxs-lookup"><span data-stu-id="efa58-103">Azure Redis Cache samples</span></span>
<span data-ttu-id="efa58-104">本主題提供 Azure Redis 快取的範例，涵蓋的案例，例如連接 tooa 快取、 讀取和寫入資料 tooand 從快取，以及使用 hello ASP.NET Redis 快取提供者的清單。</span><span class="sxs-lookup"><span data-stu-id="efa58-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting tooa cache, reading and writing data tooand from a cache, and using hello ASP.NET Redis Cache providers.</span></span> <span data-ttu-id="efa58-105">某些 hello 範例可下載專案中，且部分提供的逐步指引，包括程式碼片段，但不是連結 tooa 可下載專案。</span><span class="sxs-lookup"><span data-stu-id="efa58-105">Some of hello samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link tooa downloadable project.</span></span>

## <a name="hello-world-samples"></a><span data-ttu-id="efa58-106">Hello World 範例</span><span class="sxs-lookup"><span data-stu-id="efa58-106">Hello world samples</span></span>
<span data-ttu-id="efa58-107">本節中的 hello 範例顯示 hello 的連接 tooan Azure Redis 快取執行個體和讀取及寫入資料 toohello 快取使用多種語言的基本概念和 Redis 用戶端。</span><span class="sxs-lookup"><span data-stu-id="efa58-107">hello samples in this section show hello basics of connecting tooan Azure Redis Cache instance and reading and writing data toohello cache using a variety of languages and Redis clients.</span></span>

<span data-ttu-id="efa58-108">hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例將示範如何 tooperform 各種快取作業使用 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 用戶端。</span><span class="sxs-lookup"><span data-stu-id="efa58-108">hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how tooperform various cache operations using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span></span>

<span data-ttu-id="efa58-109">此範例示範如何：</span><span class="sxs-lookup"><span data-stu-id="efa58-109">This sample shows how to:</span></span>

* <span data-ttu-id="efa58-110">使用各種連線選項</span><span class="sxs-lookup"><span data-stu-id="efa58-110">Use various connection options</span></span>
* <span data-ttu-id="efa58-111">從使用同步和非同步作業的 hello 快取的讀取和寫入物件 tooand</span><span class="sxs-lookup"><span data-stu-id="efa58-111">Read and write objects tooand from hello cache using synchronous and asynchronous operations</span></span>
* <span data-ttu-id="efa58-112">使用指定的索引鍵的 Redis MGET/MSET 命令 tooreturn 值</span><span class="sxs-lookup"><span data-stu-id="efa58-112">Use Redis MGET/MSET commands tooreturn values of specified keys</span></span>
* <span data-ttu-id="efa58-113">執行 Redis 交易作業</span><span class="sxs-lookup"><span data-stu-id="efa58-113">Perform Redis transactional operations</span></span>
* <span data-ttu-id="efa58-114">使用 Redis 清單和已排序的集合</span><span class="sxs-lookup"><span data-stu-id="efa58-114">Work with Redis lists and sorted sets</span></span>
* <span data-ttu-id="efa58-115">使用 JsonConvert 序列化程式儲存 .NET 物件</span><span class="sxs-lookup"><span data-stu-id="efa58-115">Store .NET objects using JsonConvert serializers</span></span>
* <span data-ttu-id="efa58-116">使用 Redis 設定 tooimplement 標記</span><span class="sxs-lookup"><span data-stu-id="efa58-116">Use Redis sets tooimplement tagging</span></span>
* <span data-ttu-id="efa58-117">使用 Redis 叢集</span><span class="sxs-lookup"><span data-stu-id="efa58-117">Work with Redis Cluster</span></span>

<span data-ttu-id="efa58-118">如需詳細資訊，請參閱 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis)文件 github，而且可用於多個使用案例，請參閱 「 hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests)單元測試。</span><span class="sxs-lookup"><span data-stu-id="efa58-118">For more information, see hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span></span>

<span data-ttu-id="efa58-119">[如何 toouse Azure Redis 快取使用 Python](cache-python-get-started.md)顯示 tooget 如何開始使用 Azure Redis 快取使用 Python 和 hello [redis py](https://github.com/andymccurdy/redis-py)用戶端。</span><span class="sxs-lookup"><span data-stu-id="efa58-119">[How toouse Azure Redis Cache with Python](cache-python-get-started.md) shows how tooget started with Azure Redis Cache using Python and hello [redis-py](https://github.com/andymccurdy/redis-py) client.</span></span>

<span data-ttu-id="efa58-120">[使用 hello 快取中的.NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)顯示您的其中一種方式 tooserialize.NET 物件，您可以將它們寫入 tooand 讀取它們從 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="efa58-120">[Work with .NET objects in hello cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way tooserialize .NET objects so you can write them tooand read them from an Azure Redis Cache instance.</span></span> 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a><span data-ttu-id="efa58-121">使用 Redis 快取做為 ASP.NET SignalR 的向外延展後擋板</span><span class="sxs-lookup"><span data-stu-id="efa58-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span></span>
<span data-ttu-id="efa58-122">hello[使用 Redis 快取的範圍外後擋板適用於 ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane)範例會示範如何使用 Azure Redis 快取為 SignalR 後擋板。</span><span class="sxs-lookup"><span data-stu-id="efa58-122">hello [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span></span> <span data-ttu-id="efa58-123">如需後擋板的詳細資訊，請參閱 [使用 Redis 的 SignalR 向外延展](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)。</span><span class="sxs-lookup"><span data-stu-id="efa58-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span></span>

## <a name="redis-cache-customer-query-sample"></a><span data-ttu-id="efa58-124">Redis 快取客戶查詢範例</span><span class="sxs-lookup"><span data-stu-id="efa58-124">Redis Cache customer query sample</span></span>
<span data-ttu-id="efa58-125">本範例示範如何比較從快取中存取資料與從持續性儲存體中存取資料之間的效能。</span><span class="sxs-lookup"><span data-stu-id="efa58-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span></span> <span data-ttu-id="efa58-126">此範例有兩個專案。</span><span class="sxs-lookup"><span data-stu-id="efa58-126">This sample has two projects.</span></span>

* [<span data-ttu-id="efa58-127">示範 Redis 快取如何透過快取資料來改善效能</span><span class="sxs-lookup"><span data-stu-id="efa58-127">Demo how Redis Cache can improve performance by Caching data</span></span>](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [<span data-ttu-id="efa58-128">種子 hello 示範 hello 資料庫與快取</span><span class="sxs-lookup"><span data-stu-id="efa58-128">Seed hello Database and Cache for hello demo</span></span>](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a><span data-ttu-id="efa58-129">ASP.NET 工作階段狀態和輸出快取</span><span class="sxs-lookup"><span data-stu-id="efa58-129">ASP.NET Session State and Output Caching</span></span>
<span data-ttu-id="efa58-130">hello[使用 Azure Redis 快取 toostore ASP.NET 工作階段狀態和 OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching)範例會示範如何在您 toouse Azure Redis 快取 toostore ASP.NET 工作階段和輸出快取使用 hello 的工作階段狀態和 OutputCache 提供者Redis。</span><span class="sxs-lookup"><span data-stu-id="efa58-130">hello [Use Azure Redis Cache toostore ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you toouse Azure Redis Cache toostore ASP.NET Session and Output Cache using hello SessionState and OutputCache providers for Redis.</span></span>

## <a name="manage-azure-redis-cache-with-maml"></a><span data-ttu-id="efa58-131">使用 MAML 管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="efa58-131">Manage Azure Redis Cache with MAML</span></span>
<span data-ttu-id="efa58-132">hello[管理 Azure Redis 快取使用 Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML)範例會示範如何使用 Azure Management Libraries toomanage-(建立 / 更新 / 刪除) 您的快取。</span><span class="sxs-lookup"><span data-stu-id="efa58-132">hello [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries toomanage - (Create/ Update/ delete) your Cache.</span></span> 

## <a name="custom-monitoring-sample"></a><span data-ttu-id="efa58-133">自訂監視範例</span><span class="sxs-lookup"><span data-stu-id="efa58-133">Custom monitoring sample</span></span>
<span data-ttu-id="efa58-134">hello[存取 Redis 快取監視資料](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)範例會示範如何存取監視資料，以及在 Azure Redis 快取之外 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="efa58-134">hello [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of hello Azure Portal.</span></span>

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a><span data-ttu-id="efa58-135">使用 PHP 和 Redis 撰寫的 Twitter 風格複製品</span><span class="sxs-lookup"><span data-stu-id="efa58-135">A Twitter-style clone written using PHP and Redis</span></span>
<span data-ttu-id="efa58-136">hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis)範例是 Redis Hello World hello。</span><span class="sxs-lookup"><span data-stu-id="efa58-136">hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is hello Redis Hello World.</span></span> <span data-ttu-id="efa58-137">它是最小的 Twitter 風格的社交網路複製使用 Redis 和使用 hello 的 PHP 撰寫[Predis](https://github.com/nrk/predis)用戶端。</span><span class="sxs-lookup"><span data-stu-id="efa58-137">It is a minimal Twitter-style social network clone written using Redis and PHP using hello [Predis](https://github.com/nrk/predis) client.</span></span> <span data-ttu-id="efa58-138">hello 原始碼，是設計的 toobe 的非常簡單，並在 hello 相同時間 tooshow 不同 Redis 資料結構。</span><span class="sxs-lookup"><span data-stu-id="efa58-138">hello source code is designed toobe very simple and at hello same time tooshow different Redis data structures.</span></span>

## <a name="bandwidth-monitor"></a><span data-ttu-id="efa58-139">頻寬監視器</span><span class="sxs-lookup"><span data-stu-id="efa58-139">Bandwidth monitor</span></span>
<span data-ttu-id="efa58-140">hello[頻寬監視器](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor)範例可讓您用戶端 hello toomonitor hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="efa58-140">hello [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you toomonitor hello bandwidth used on hello client.</span></span> <span data-ttu-id="efa58-141">toomeasure hello 頻寬、 hello 快取的用戶端電腦上執行 hello 範例，請呼叫 toohello 快取，和觀察 hello 頻寬監視器範例所報告的 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="efa58-141">toomeasure hello bandwidth, run hello sample on hello cache client machine, make calls toohello cache, and observe hello bandwidth reported by hello bandwidth monitor sample.</span></span>

