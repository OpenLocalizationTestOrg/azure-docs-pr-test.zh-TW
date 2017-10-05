---
title: "Azure Redis 快取範例 | Microsoft Docs"
description: "了解如何使用 Azure Redis 快取"
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
ms.openlocfilehash: 7841fcf0b5f4dcb409abf8bfb804c2e03dad6d3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-redis-cache-samples"></a><span data-ttu-id="34f38-103">Azure Redis 快取範例</span><span class="sxs-lookup"><span data-stu-id="34f38-103">Azure Redis Cache samples</span></span>
<span data-ttu-id="34f38-104">本主題提供 Azure Redis 快取範例清單，其中涵蓋下列這類案例：連線至快取、在快取中讀取和寫入資料，以及使用 ASP.NET Redis 快取提供者。</span><span class="sxs-lookup"><span data-stu-id="34f38-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting to a cache, reading and writing data to and from a cache, and using the ASP.NET Redis Cache providers.</span></span> <span data-ttu-id="34f38-105">有些範例是可下載的專案，有些則提供逐步指導並包括程式碼片段，但沒有可下載專案的連結。</span><span class="sxs-lookup"><span data-stu-id="34f38-105">Some of the samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link to a downloadable project.</span></span>

## <a name="hello-world-samples"></a><span data-ttu-id="34f38-106">Hello World 範例</span><span class="sxs-lookup"><span data-stu-id="34f38-106">Hello world samples</span></span>
<span data-ttu-id="34f38-107">本節中的範例說明連線至 Azure Redis 快取執行個體以及使用各種語言和 Redis 用戶端在快取中讀取和寫入資料的基本概念。</span><span class="sxs-lookup"><span data-stu-id="34f38-107">The samples in this section show the basics of connecting to an Azure Redis Cache instance and reading and writing data to the cache using a variety of languages and Redis clients.</span></span>

<span data-ttu-id="34f38-108">[Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 範例示範如何使用 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 用戶端來執行各種快取作業。</span><span class="sxs-lookup"><span data-stu-id="34f38-108">The [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how to perform various cache operations using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span></span>

<span data-ttu-id="34f38-109">此範例示範如何：</span><span class="sxs-lookup"><span data-stu-id="34f38-109">This sample shows how to:</span></span>

* <span data-ttu-id="34f38-110">使用各種連線選項</span><span class="sxs-lookup"><span data-stu-id="34f38-110">Use various connection options</span></span>
* <span data-ttu-id="34f38-111">使用同步和非同步作業在快取中讀取和寫入物件</span><span class="sxs-lookup"><span data-stu-id="34f38-111">Read and write objects to and from the cache using synchronous and asynchronous operations</span></span>
* <span data-ttu-id="34f38-112">使用 Redis MGET/MSET 命令來傳回所指定金鑰的值</span><span class="sxs-lookup"><span data-stu-id="34f38-112">Use Redis MGET/MSET commands to return values of specified keys</span></span>
* <span data-ttu-id="34f38-113">執行 Redis 交易作業</span><span class="sxs-lookup"><span data-stu-id="34f38-113">Perform Redis transactional operations</span></span>
* <span data-ttu-id="34f38-114">使用 Redis 清單和已排序的集合</span><span class="sxs-lookup"><span data-stu-id="34f38-114">Work with Redis lists and sorted sets</span></span>
* <span data-ttu-id="34f38-115">使用 JsonConvert 序列化程式儲存 .NET 物件</span><span class="sxs-lookup"><span data-stu-id="34f38-115">Store .NET objects using JsonConvert serializers</span></span>
* <span data-ttu-id="34f38-116">使用 Redis 集合來實作標記</span><span class="sxs-lookup"><span data-stu-id="34f38-116">Use Redis sets to implement tagging</span></span>
* <span data-ttu-id="34f38-117">使用 Redis 叢集</span><span class="sxs-lookup"><span data-stu-id="34f38-117">Work with Redis Cluster</span></span>

<span data-ttu-id="34f38-118">如需詳細資訊，請參閱 github 上的 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) 文件，如需使用案例，則請參閱 [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) 單元測試。</span><span class="sxs-lookup"><span data-stu-id="34f38-118">For more information, see the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see the [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span></span>

<span data-ttu-id="34f38-119">[如何搭配使用 Azure Redis 快取與 Python](cache-python-get-started.md) 說明如何使用 Python 和 [redis-py](https://github.com/andymccurdy/redis-py) 用戶端開始搭配 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="34f38-119">[How to use Azure Redis Cache with Python](cache-python-get-started.md) shows how to get started with Azure Redis Cache using Python and the [redis-py](https://github.com/andymccurdy/redis-py) client.</span></span>

<span data-ttu-id="34f38-120">[使用快取中的 .NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) 說明序列化 .NET 物件的一種方式，以在 Azure Redis 快取執行個體中寫入和讀取它們。</span><span class="sxs-lookup"><span data-stu-id="34f38-120">[Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way to serialize .NET objects so you can write them to and read them from an Azure Redis Cache instance.</span></span> 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a><span data-ttu-id="34f38-121">使用 Redis 快取做為 ASP.NET SignalR 的向外延展後擋板</span><span class="sxs-lookup"><span data-stu-id="34f38-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span></span>
<span data-ttu-id="34f38-122">[使用 Redis 快取做為 ASP.NET SignalR 的向外延展後擋板](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) 範例示範如何使用 Azure Redis 快取做為 SignalR 後擋板。</span><span class="sxs-lookup"><span data-stu-id="34f38-122">The [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span></span> <span data-ttu-id="34f38-123">如需後擋板的詳細資訊，請參閱 [使用 Redis 的 SignalR 向外延展](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)。</span><span class="sxs-lookup"><span data-stu-id="34f38-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span></span>

## <a name="redis-cache-customer-query-sample"></a><span data-ttu-id="34f38-124">Redis 快取客戶查詢範例</span><span class="sxs-lookup"><span data-stu-id="34f38-124">Redis Cache customer query sample</span></span>
<span data-ttu-id="34f38-125">本範例示範如何比較從快取中存取資料與從持續性儲存體中存取資料之間的效能。</span><span class="sxs-lookup"><span data-stu-id="34f38-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span></span> <span data-ttu-id="34f38-126">此範例有兩個專案。</span><span class="sxs-lookup"><span data-stu-id="34f38-126">This sample has two projects.</span></span>

* [<span data-ttu-id="34f38-127">示範 Redis 快取如何透過快取資料來改善效能</span><span class="sxs-lookup"><span data-stu-id="34f38-127">Demo how Redis Cache can improve performance by Caching data</span></span>](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [<span data-ttu-id="34f38-128">植入示範的資料庫和快取</span><span class="sxs-lookup"><span data-stu-id="34f38-128">Seed the Database and Cache for the demo</span></span>](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a><span data-ttu-id="34f38-129">ASP.NET 工作階段狀態和輸出快取</span><span class="sxs-lookup"><span data-stu-id="34f38-129">ASP.NET Session State and Output Caching</span></span>
<span data-ttu-id="34f38-130">[使用 Azure Redis 快取儲存 ASP.NET SessionState 和 OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) 範例示範如何使用 Azure Redis 快取，以使用 Redis 的 SessionState 和 OutputCache 提供者來儲存 ASP.NET 工作階段和輸出快取。</span><span class="sxs-lookup"><span data-stu-id="34f38-130">The [Use Azure Redis Cache to store ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you to use Azure Redis Cache to store ASP.NET Session and Output Cache using the SessionState and OutputCache providers for Redis.</span></span>

## <a name="manage-azure-redis-cache-with-maml"></a><span data-ttu-id="34f38-131">使用 MAML 管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="34f38-131">Manage Azure Redis Cache with MAML</span></span>
<span data-ttu-id="34f38-132">[使用 Azure 管理庫管理 Azure Redis 快取](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 範例示範如何使用 Azure 管理庫來管理 - (建立/更新/刪除) 快取。</span><span class="sxs-lookup"><span data-stu-id="34f38-132">The [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries to manage - (Create/ Update/ delete) your Cache.</span></span> 

## <a name="custom-monitoring-sample"></a><span data-ttu-id="34f38-133">自訂監視範例</span><span class="sxs-lookup"><span data-stu-id="34f38-133">Custom monitoring sample</span></span>
<span data-ttu-id="34f38-134">[存取 Redis 快取監視資料](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) 範例示範如何在 Azure 入口網站外部存取 Azure Redis 快取的監視資料。</span><span class="sxs-lookup"><span data-stu-id="34f38-134">The [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of the Azure Portal.</span></span>

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a><span data-ttu-id="34f38-135">使用 PHP 和 Redis 撰寫的 Twitter 風格複製品</span><span class="sxs-lookup"><span data-stu-id="34f38-135">A Twitter-style clone written using PHP and Redis</span></span>
<span data-ttu-id="34f38-136">[Retwis](https://github.com/SyntaxC4-MSFT/retwis) 範例是 Redis Hello World。</span><span class="sxs-lookup"><span data-stu-id="34f38-136">The [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is the Redis Hello World.</span></span> <span data-ttu-id="34f38-137">它是透過 [Predis](https://github.com/nrk/predis) 用戶端使用 Redis 和 PHP 撰寫的最小 Twitter 風格社交網路複製品。</span><span class="sxs-lookup"><span data-stu-id="34f38-137">It is a minimal Twitter-style social network clone written using Redis and PHP using the [Predis](https://github.com/nrk/predis) client.</span></span> <span data-ttu-id="34f38-138">原始碼的設計十分簡單，並且同時顯示不同的 Redis 資料結構。</span><span class="sxs-lookup"><span data-stu-id="34f38-138">The source code is designed to be very simple and at the same time to show different Redis data structures.</span></span>

## <a name="bandwidth-monitor"></a><span data-ttu-id="34f38-139">頻寬監視器</span><span class="sxs-lookup"><span data-stu-id="34f38-139">Bandwidth monitor</span></span>
<span data-ttu-id="34f38-140">[頻寬監視器](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) 範例可讓您監視用戶端上使用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="34f38-140">The [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you to monitor the bandwidth used on the client.</span></span> <span data-ttu-id="34f38-141">若要測量頻寬，請在快取用戶端電腦上執行這個範例、呼叫快取，並觀察頻寬監視器範例所報告的頻寬。</span><span class="sxs-lookup"><span data-stu-id="34f38-141">To measure the bandwidth, run the sample on the cache client machine, make calls to the cache, and observe the bandwidth reported by the bandwidth monitor sample.</span></span>

