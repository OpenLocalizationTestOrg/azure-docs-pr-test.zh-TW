---
title: "如何設定進階 Azure Redis 快取的 Redis 叢集 | Microsoft Docs"
description: "了解如何建立和管理進階層 Azure Redis 快取執行個體的 Redis 叢集"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 86a4a605dbb3b11924c14ff42238009742f72898
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-redis-clustering-for-a-premium-azure-redis-cache"></a><span data-ttu-id="66d7e-103">如何設定進階 Azure Redis 快取的 Redis 叢集</span><span class="sxs-lookup"><span data-stu-id="66d7e-103">How to configure Redis clustering for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="66d7e-104">Azure Redis 快取有不同的快取供應項目，可讓您彈性選擇快取大小和功能，包括叢集、持續性和虛擬網路支援等進階層功能。</span><span class="sxs-lookup"><span data-stu-id="66d7e-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="66d7e-105">本文說明如何在進階 Azure Redis 快取執行個體中設定叢集。</span><span class="sxs-lookup"><span data-stu-id="66d7e-105">This article describes how to configure clustering in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="66d7e-106">如需其他進階快取功能的相關資訊，請參閱 [Azure Redis 快取進階層簡介](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-106">For information on other premium cache features, see [Introduction to the Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-redis-cluster"></a><span data-ttu-id="66d7e-107">Redis 叢集是什麼？</span><span class="sxs-lookup"><span data-stu-id="66d7e-107">What is Redis Cluster?</span></span>
<span data-ttu-id="66d7e-108">Azure Redis 快取提供 Redis 叢集的方式，就像 [實作於 Redis](http://redis.io/topics/cluster-tutorial)一樣。</span><span class="sxs-lookup"><span data-stu-id="66d7e-108">Azure Redis Cache offers Redis cluster as [implemented in Redis](http://redis.io/topics/cluster-tutorial).</span></span> <span data-ttu-id="66d7e-109">使用 Redis 叢集有下列優點：</span><span class="sxs-lookup"><span data-stu-id="66d7e-109">With Redis Cluster, you get the following benefits:</span></span> 

* <span data-ttu-id="66d7e-110">能夠自動分割您在多個節點之間的資料集。</span><span class="sxs-lookup"><span data-stu-id="66d7e-110">The ability to automatically split your dataset among multiple nodes.</span></span> 
* <span data-ttu-id="66d7e-111">當節點的子集發生故障或無法與叢集的其餘部分通訊時，可以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="66d7e-111">The ability to continue operations when a subset of the nodes is experiencing failures or are unable to communicate with the rest of the cluster.</span></span> 
* <span data-ttu-id="66d7e-112">更多輸送量：當您增加分區數目時，輸送量會呈線性增加。</span><span class="sxs-lookup"><span data-stu-id="66d7e-112">More throughput: Throughput increases linearly as you increase the number of shards.</span></span> 
* <span data-ttu-id="66d7e-113">更多記憶體大小：當您增加分區數目時，會呈線性增加。</span><span class="sxs-lookup"><span data-stu-id="66d7e-113">More memory size: Increases linearly as you increase the number of shards.</span></span>  

<span data-ttu-id="66d7e-114">如需進階快取的大小、輸送量和頻寬的詳細資訊，請參閱[應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="66d7e-114">For more information about size, throughput, and bandwidth with premium caches, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>

<span data-ttu-id="66d7e-115">在 Azure 中，Redis 叢集以主要/複本模型方式提供，其中的每個分區都有一個具複寫功能的主要/複本組，而複寫是由 Azure Redis 快取服務管理。</span><span class="sxs-lookup"><span data-stu-id="66d7e-115">In Azure, Redis cluster is offered as a primary/replica model where each shard has a primary/replica pair with replication where the replication is managed by Azure Redis Cache service.</span></span> 

## <a name="clustering"></a><span data-ttu-id="66d7e-116">叢集</span><span class="sxs-lookup"><span data-stu-id="66d7e-116">Clustering</span></span>
<span data-ttu-id="66d7e-117">叢集是在快取建立期間於 [新的 Redis 快取]  刀鋒視窗中所啟用。</span><span class="sxs-lookup"><span data-stu-id="66d7e-117">Clustering is enabled on the **New Redis Cache** blade during cache creation.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="66d7e-118">叢集是在 [ **Redis 叢集** ] 刀鋒視窗中所設定。</span><span class="sxs-lookup"><span data-stu-id="66d7e-118">Clustering is configured on the **Redis Cluster** blade.</span></span>

![叢集][redis-cache-clustering]

<span data-ttu-id="66d7e-120">叢集中最多可包含 10 個分區。</span><span class="sxs-lookup"><span data-stu-id="66d7e-120">You can have up to 10 shards in the cluster.</span></span> <span data-ttu-id="66d7e-121">按一下 [啟用]，針對 [分區計數]，滑動滑桿或鍵入一個 1 到 10 之間的數字，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="66d7e-121">Click **Enabled** and slide the slider or type a number between 1 and 10 for **Shard count** and click **OK**.</span></span>

<span data-ttu-id="66d7e-122">每個分區都是一個由 Azure 管理的主要/複本快取組，快取總大小的計算方式，是將分區數目乘以在定價層中選取的快取大小。</span><span class="sxs-lookup"><span data-stu-id="66d7e-122">Each shard is a primary/replica cache pair managed by Azure, and the total size of the cache is calculated by multiplying the number of shards by the cache size selected in the pricing tier.</span></span> 

![叢集][redis-cache-clustering-selected]

<span data-ttu-id="66d7e-124">建立快取後，您可以連線並使用它，就像非叢集化快取一樣，而且 Redis 會在整個快取分區散發資料。</span><span class="sxs-lookup"><span data-stu-id="66d7e-124">Once the cache is created you connect to it and use it just like a non-clustered cache, and Redis distributes the data throughout the Cache shards.</span></span> <span data-ttu-id="66d7e-125">如果[已啟用](cache-how-to-monitor.md#enable-cache-diagnostics)診斷，則會針對每個分區個別擷取度量，而且可以在 [Redis 快取] 刀鋒視窗中[檢視](cache-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-125">If diagnostics is [enabled](cache-how-to-monitor.md#enable-cache-diagnostics), metrics are captured separately for each shard and can be [viewed](cache-how-to-monitor.md) in the Redis Cache blade.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="66d7e-126">在設定叢集時，用戶端應用程式中的必要設定有些微差異。</span><span class="sxs-lookup"><span data-stu-id="66d7e-126">There are some minor differences required in your client application when clustering is configured.</span></span> <span data-ttu-id="66d7e-127">如需詳細資訊，請參閱 [我需要對用戶端應用程式進行任何變更才能使用叢集嗎？](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="66d7e-127">For more information, see [Do I need to make any changes to my client application to use clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>
> 
> 

<span data-ttu-id="66d7e-128">如需搭配 StackExchange.Redis 用戶端使用叢集的範例程式碼，請參閱 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 範例的 [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) 部分。</span><span class="sxs-lookup"><span data-stu-id="66d7e-128">For sample code on working with clustering with the StackExchange.Redis client, see the [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of the [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

<a name="cluster-size"></a>

## <a name="change-the-cluster-size-on-a-running-premium-cache"></a><span data-ttu-id="66d7e-129">在執行中的進階快取上變更叢集大小</span><span class="sxs-lookup"><span data-stu-id="66d7e-129">Change the cluster size on a running premium cache</span></span>
<span data-ttu-id="66d7e-130">若要變更已啟用叢集的執行中進階快取上的叢集大小，請從 [資源] 功能表中按一下 [Redis 叢集大小]。</span><span class="sxs-lookup"><span data-stu-id="66d7e-130">To change the cluster size on a running premium cache with clustering enabled, click **Redis Cluster Size** from the **Resource menu**.</span></span>

> [!NOTE]
> <span data-ttu-id="66d7e-131">雖然 Azure Redis 快取進階層已發行正式上市版，但 Redis 叢集大小功能目前仍為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="66d7e-131">While the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 叢集大小][redis-cache-redis-cluster-size]

<span data-ttu-id="66d7e-133">若要變更叢集大小，請使用滑桿，或在 [分區計數] 文字方塊中輸入 1 到 10 之間的數字，然後按一下 [確定] 加以儲存。</span><span class="sxs-lookup"><span data-stu-id="66d7e-133">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!NOTE]
> <span data-ttu-id="66d7e-134">調整叢集大小會執行 [MIGRATE](https://redis.io/commands/migrate) 命令，這個命令會耗用大量資源，因此為了將影響降到最低，請考慮在非尖峰時段執行此作業。</span><span class="sxs-lookup"><span data-stu-id="66d7e-134">Scaling a cluster runs the [MIGRATE](https://redis.io/commands/migrate) command, which is an expensive command, so for minimal impact, consider running this operation during non-peak hours.</span></span> <span data-ttu-id="66d7e-135">在移轉程序期間，您會看到伺服器負載出現峰值。</span><span class="sxs-lookup"><span data-stu-id="66d7e-135">During the migration process, you will see a spike in server load.</span></span> <span data-ttu-id="66d7e-136">調整叢集大小是需要長時間執行的程序，且所需時間決定於索引鍵數目，以及與那些索引鍵相關聯之值的大小。</span><span class="sxs-lookup"><span data-stu-id="66d7e-136">Scaling a cluster is a long running process and the amount of time taken depends on the number of keys and size of the values associated with those keys.</span></span>
> 
> 

## <a name="clustering-faq"></a><span data-ttu-id="66d7e-137">叢集常見問題集</span><span class="sxs-lookup"><span data-stu-id="66d7e-137">Clustering FAQ</span></span>
<span data-ttu-id="66d7e-138">下列清單包含 Azure Redis 快取叢集常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="66d7e-138">The following list contains answers to commonly asked questions about Azure Redis Cache clustering.</span></span>

* [<span data-ttu-id="66d7e-139">我需要對我的用戶端應用程式進行任何變更才能使用叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-139">Do I need to make any changes to my client application to use clustering?</span></span>](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [<span data-ttu-id="66d7e-140">如何在叢集中散發索引鍵？</span><span class="sxs-lookup"><span data-stu-id="66d7e-140">How are keys distributed in a cluster?</span></span>](#how-are-keys-distributed-in-a-cluster)
* [<span data-ttu-id="66d7e-141">我可以建立的最大快取大小為何？</span><span class="sxs-lookup"><span data-stu-id="66d7e-141">What is the largest cache size I can create?</span></span>](#what-is-the-largest-cache-size-i-can-create)
* [<span data-ttu-id="66d7e-142">所有 Redis 用戶端都支援叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-142">Do all Redis clients support clustering?</span></span>](#do-all-redis-clients-support-clustering)
* [<span data-ttu-id="66d7e-143">啟用叢集後，要如何連接到我的快取？</span><span class="sxs-lookup"><span data-stu-id="66d7e-143">How do I connect to my cache when clustering is enabled?</span></span>](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [<span data-ttu-id="66d7e-144">我可以直接連接到我的快取的個別分區嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-144">Can I directly connect to the individual shards of my cache?</span></span>](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [<span data-ttu-id="66d7e-145">我可以為先前建立的快取設定叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-145">Can I configure clustering for a previously created cache?</span></span>](#can-i-configure-clustering-for-a-previously-created-cache)
* [<span data-ttu-id="66d7e-146">我可以設定基本或標準快取的叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-146">Can I configure clustering for a basic or standard cache?</span></span>](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [<span data-ttu-id="66d7e-147">我可以將叢集使用於 Redis ASP.NET 工作階段狀態和輸出快取提供者嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-147">Can I use clustering with the Redis ASP.NET Session State and Output Caching providers?</span></span>](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [<span data-ttu-id="66d7e-148">當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="66d7e-148">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering"></a><span data-ttu-id="66d7e-149">我需要對我的用戶端應用程式進行任何變更才能使用叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-149">Do I need to make any changes to my client application to use clustering?</span></span>
* <span data-ttu-id="66d7e-150">啟用叢集時，只可以使用資料庫 0。</span><span class="sxs-lookup"><span data-stu-id="66d7e-150">When clustering is enabled, only database 0 is available.</span></span> <span data-ttu-id="66d7e-151">如果用戶端應用程式使用多個資料庫，並嘗試讀取或寫入至 0 以外的資料庫，就會擲回下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="66d7e-151">If your client application uses multiple databases and it tries to read or write to a database other than 0, the following exception is thrown.</span></span> <span data-ttu-id="66d7e-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch to database: 6`</span><span class="sxs-lookup"><span data-stu-id="66d7e-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch to database: 6`</span></span>
  
  <span data-ttu-id="66d7e-153">如需詳細資訊，請參閱 [Redis 叢集規格 - 實作的子集](http://redis.io/topics/cluster-spec#implemented-subset)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-153">For more information, see [Redis Cluster Specification - Implemented subset](http://redis.io/topics/cluster-spec#implemented-subset).</span></span>
* <span data-ttu-id="66d7e-154">如果您使用 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/)，則必須使用 1.0.481 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="66d7e-154">If you are using [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), you must use 1.0.481 or later.</span></span> <span data-ttu-id="66d7e-155">您可以使用與連接未啟用叢集的快取時所用的相同 [端點、連接埠和金鑰](cache-configure.md#properties) 來連接快取。</span><span class="sxs-lookup"><span data-stu-id="66d7e-155">You connect to the cache using the same [endpoints, ports, and keys](cache-configure.md#properties) that you use when connecting to a cache that does not have clustering enabled.</span></span> <span data-ttu-id="66d7e-156">唯一的差別在於必須在資料庫 0 上完成所有的讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="66d7e-156">The only difference is that all reads and writes must be done to database 0.</span></span>
  
  * <span data-ttu-id="66d7e-157">其他用戶端可能有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="66d7e-157">Other clients may have different requirements.</span></span> <span data-ttu-id="66d7e-158">請參閱 [所有 Redis 用戶端都支援叢集嗎？](#do-all-redis-clients-support-clustering)</span><span class="sxs-lookup"><span data-stu-id="66d7e-158">See [Do all Redis clients support clustering?](#do-all-redis-clients-support-clustering)</span></span>
* <span data-ttu-id="66d7e-159">如果您的應用程式使用分成單一命令的多個索引鍵作業，則所有索引鍵都必須位於相同的分區。</span><span class="sxs-lookup"><span data-stu-id="66d7e-159">If your application uses multiple key operations batched into a single command, all keys must be located in the same shard.</span></span> <span data-ttu-id="66d7e-160">若要將索引鍵置於相同的分區，請參閱[如何在叢集中散發索引鍵？](#how-are-keys-distributed-in-a-cluster)</span><span class="sxs-lookup"><span data-stu-id="66d7e-160">To locate keys in the same shard, see [How are keys distributed in a cluster?](#how-are-keys-distributed-in-a-cluster)</span></span>
* <span data-ttu-id="66d7e-161">如果您使用 Redis ASP.NET 工作階段狀態提供者，則必須使用 2.0.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="66d7e-161">If you are using Redis ASP.NET Session State provider you must use 2.0.1 or higher.</span></span> <span data-ttu-id="66d7e-162">請參閱 [我可以將叢集使用於 Redis ASP.NET 工作階段狀態和輸出快取提供者嗎？](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span><span class="sxs-lookup"><span data-stu-id="66d7e-162">See [Can I use clustering with the Redis ASP.NET Session State and Output Caching providers?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span></span>

### <a name="how-are-keys-distributed-in-a-cluster"></a><span data-ttu-id="66d7e-163">如何在叢集中散發索引鍵？</span><span class="sxs-lookup"><span data-stu-id="66d7e-163">How are keys distributed in a cluster?</span></span>
<span data-ttu-id="66d7e-164">依據 Redis [金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model) 文件︰金鑰空間會分割成 16384 個位置。</span><span class="sxs-lookup"><span data-stu-id="66d7e-164">Per the Redis [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model) documentation: The key space is split into 16384 slots.</span></span> <span data-ttu-id="66d7e-165">每個索引鍵都會雜湊並指派給上述的其中一個位置，而這些位置散發於叢集的各個節點。</span><span class="sxs-lookup"><span data-stu-id="66d7e-165">Each key is hashed and assigned to one of these slots, which are distributed across the nodes of the cluster.</span></span> <span data-ttu-id="66d7e-166">您可以設定哪個部分的索引鍵會雜湊，以確保多個索引鍵位於使用主題標籤的相同分區中。</span><span class="sxs-lookup"><span data-stu-id="66d7e-166">You can configure which part of the key is hashed to ensure that multiple keys are located in the same shard using hash tags.</span></span>

* <span data-ttu-id="66d7e-167">具有主題標籤的金鑰 - 如果金鑰的任何部分被括在 `{` 和 `}` 中，則只有該部分的金鑰會為了判斷金鑰的主題標籤位置而進行雜湊。</span><span class="sxs-lookup"><span data-stu-id="66d7e-167">Keys with a hash tag - if any part of the key is enclosed in `{` and `}`, only that part of the key is hashed for the purposes of determining the hash slot of a key.</span></span> <span data-ttu-id="66d7e-168">例如，下列 3 個金鑰會位於相同的分區︰`{key}1`、`{key}2` 和 `{key}3`，因為只會雜湊名稱的 `key` 部分。</span><span class="sxs-lookup"><span data-stu-id="66d7e-168">For example, the following 3 keys would be located in the same shard: `{key}1`, `{key}2`, and `{key}3` since only the `key` part of the name is hashed.</span></span> <span data-ttu-id="66d7e-169">如需索引鍵主題標籤規格的完整清單，請參閱[索引鍵主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-169">For a complete list of keys hash tag specifications, see [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>
* <span data-ttu-id="66d7e-170">沒有主題標籤的索引鍵 - 整個索引鍵名稱都用於主題標籤。</span><span class="sxs-lookup"><span data-stu-id="66d7e-170">Keys without a hash tag - the entire key name is used for hashing.</span></span> <span data-ttu-id="66d7e-171">這會導致以統計方式平均散發於快取的各個分區。</span><span class="sxs-lookup"><span data-stu-id="66d7e-171">This results in a statistically even distribution across the shards of the cache.</span></span>

<span data-ttu-id="66d7e-172">如需最佳的效能和輸送量，我們建議平均散發索引鍵。</span><span class="sxs-lookup"><span data-stu-id="66d7e-172">For best performance and throughput, we recommend distributing the keys evenly.</span></span> <span data-ttu-id="66d7e-173">如果您使用具有主題標籤的索引鍵，則應用程式必須負責確保平均散發索引鍵。</span><span class="sxs-lookup"><span data-stu-id="66d7e-173">If you are using keys with a hash tag it is the application's responsibility to ensure the keys are distributed evenly.</span></span>

<span data-ttu-id="66d7e-174">如需詳細資訊，請參閱[金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model)、[Redis 叢集資料分區化](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding)和[金鑰主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-174">For more information, see [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis Cluster data sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), and [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>

<span data-ttu-id="66d7e-175">如需搭配 StackExchange.Redis 用戶端使用叢集，並尋找相同分區中之金鑰的範例程式碼，請參閱 [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 範例的 [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) 部分。</span><span class="sxs-lookup"><span data-stu-id="66d7e-175">For sample code on working with clustering and locating keys in the same shard with the StackExchange.Redis client, see the [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of the [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

### <a name="what-is-the-largest-cache-size-i-can-create"></a><span data-ttu-id="66d7e-176">我可以建立的最大快取大小為何？</span><span class="sxs-lookup"><span data-stu-id="66d7e-176">What is the largest cache size I can create?</span></span>
<span data-ttu-id="66d7e-177">最大的進階快取大小為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="66d7e-177">The largest premium cache size is 53 GB.</span></span> <span data-ttu-id="66d7e-178">您最多可以建立 10 個分區，等於最大大小為 530 GB。</span><span class="sxs-lookup"><span data-stu-id="66d7e-178">You can create up to 10 shards giving you a maximum size of 530 GB.</span></span> <span data-ttu-id="66d7e-179">如果您需要較大的大小，可以 [要求更多](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-179">If you need a larger size you can [request more](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase).</span></span> <span data-ttu-id="66d7e-180">如需詳細資訊，請參閱 [Azure Redis 快取價格](https://azure.microsoft.com/pricing/details/cache/)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-180">For more information, see [Azure Redis Cache Pricing](https://azure.microsoft.com/pricing/details/cache/).</span></span>

### <a name="do-all-redis-clients-support-clustering"></a><span data-ttu-id="66d7e-181">所有 Redis 用戶端都支援叢集嗎？ </span><span class="sxs-lookup"><span data-stu-id="66d7e-181">Do all Redis clients support clustering?</span></span>
<span data-ttu-id="66d7e-182">現階段，並非所有用戶端都支援 Redis 叢集。</span><span class="sxs-lookup"><span data-stu-id="66d7e-182">At the present time not all clients support Redis clustering.</span></span> <span data-ttu-id="66d7e-183">StackExchange.Redis 就是不支援的其中一例。</span><span class="sxs-lookup"><span data-stu-id="66d7e-183">StackExchange.Redis is one that does support for it.</span></span> <span data-ttu-id="66d7e-184">如需其他用戶端的詳細資訊，請參閱 [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)的 [試用叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)一節。</span><span class="sxs-lookup"><span data-stu-id="66d7e-184">For more information on other clients, see the [Playing with the cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) section of the [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

> [!NOTE]
> <span data-ttu-id="66d7e-185">如果您使用 StackExchange.Redis 做為您的用戶端，請確定您使用的是最新版的 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) (1.0.481) 或更新版本，叢集才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="66d7e-185">If you are using StackExchange.Redis as your client, ensure you are using the latest version of [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 or later for clustering to work correctly.</span></span> <span data-ttu-id="66d7e-186">如果您有任何關於 Move 例外狀況的問題，請參閱 [Move 例外狀況](#move-exceptions) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66d7e-186">If you have any issues with move exceptions, see [move exceptions](#move-exceptions) for more information.</span></span>
> 
> 

### <a name="how-do-i-connect-to-my-cache-when-clustering-is-enabled"></a><span data-ttu-id="66d7e-187">啟用叢集後，要如何連接到我的快取？</span><span class="sxs-lookup"><span data-stu-id="66d7e-187">How do I connect to my cache when clustering is enabled?</span></span>
<span data-ttu-id="66d7e-188">您可以使用與連接未啟用叢集的快取時所用的相同 [端點](cache-configure.md#properties)、[連接埠](cache-configure.md#properties)和[金鑰](cache-configure.md#access-keys)來連接快取。</span><span class="sxs-lookup"><span data-stu-id="66d7e-188">You can connect to your cache using the same [endpoints](cache-configure.md#properties), [ports](cache-configure.md#properties), and [keys](cache-configure.md#access-keys) that you use when connecting to a cache that does not have clustering enabled.</span></span> <span data-ttu-id="66d7e-189">Redis 會管理後端上的叢集，因此您不需從用戶端進行管理。</span><span class="sxs-lookup"><span data-stu-id="66d7e-189">Redis manages the clustering on the backend so you don't have to manage it from your client.</span></span>

### <a name="can-i-directly-connect-to-the-individual-shards-of-my-cache"></a><span data-ttu-id="66d7e-190">我可以直接連接到我的快取的個別分區嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-190">Can I directly connect to the individual shards of my cache?</span></span>
<span data-ttu-id="66d7e-191">目前官方尚未提供支援。</span><span class="sxs-lookup"><span data-stu-id="66d7e-191">This is not officially supported.</span></span> <span data-ttu-id="66d7e-192">如前所述，每個分區都包含一個主要/複本快取組，統稱為快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="66d7e-192">With that said, each shard consists of a primary/replica cache pair, collectively known as a cache instance.</span></span> <span data-ttu-id="66d7e-193">您可以使用 GitHub 中 Redis 存放庫[不穩定](http://redis.io/download)分支內的 redis-cli 公用程式，連線到這些快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="66d7e-193">You can connect to these cache instances using the redis-cli utility in the [unstable](http://redis.io/download) branch of the Redis repository at GitHub.</span></span> <span data-ttu-id="66d7e-194">使用 `-c` 參數啟用這個版本時，會實作基本支援。</span><span class="sxs-lookup"><span data-stu-id="66d7e-194">This version implements basic support when started with the `-c` switch.</span></span> <span data-ttu-id="66d7e-195">如需詳細資訊，請參閱 [http://redis.io](http://redis.io) 上 [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)中的[試用叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-195">For more information see [Playing with the cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) on [http://redis.io](http://redis.io) in the [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

<span data-ttu-id="66d7e-196">如為非 SSL，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="66d7e-196">For non-ssl, use the following commands.</span></span>

    Redis-cli.exe –h <<cachename>> -p 13000 (to connect to instance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (to connect to instance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (to connect to instance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (to connect to instance N)

<span data-ttu-id="66d7e-197">如為 SSL，將 `1300N` 取代為 `1500N`。</span><span class="sxs-lookup"><span data-stu-id="66d7e-197">For ssl, replace `1300N` with `1500N`.</span></span>

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a><span data-ttu-id="66d7e-198">我可以為先前建立的快取設定叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-198">Can I configure clustering for a previously created cache?</span></span>
<span data-ttu-id="66d7e-199">目前您只能在建立快取時啟用叢集。</span><span class="sxs-lookup"><span data-stu-id="66d7e-199">Currently you can only enable clustering when you create a cache.</span></span> <span data-ttu-id="66d7e-200">您可以在建立快取之後變更叢集大小，但無法在建立快取之後將叢集新增至進階快取，或從進階快取中移除叢集。</span><span class="sxs-lookup"><span data-stu-id="66d7e-200">You can change the cluster size after the cache is created, but you can't add clustering to a premium cache or remove clustering from a premium cache after the cache is created.</span></span> <span data-ttu-id="66d7e-201">已啟用叢集且只有一個分區的進階快取，與相同大小且沒有叢集的進階快取不同。</span><span class="sxs-lookup"><span data-stu-id="66d7e-201">A premium cache with clustering enabled and only one shard is different than a premium cache of the same size with no clustering.</span></span>

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a><span data-ttu-id="66d7e-202">我可以設定基本或標準快取的叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-202">Can I configure clustering for a basic or standard cache?</span></span>
<span data-ttu-id="66d7e-203">叢集僅適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="66d7e-203">Clustering is only available for premium caches.</span></span>

### <a name="can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers"></a><span data-ttu-id="66d7e-204">我可以將叢集使用於 Redis ASP.NET 工作階段狀態和輸出快取提供者嗎？</span><span class="sxs-lookup"><span data-stu-id="66d7e-204">Can I use clustering with the Redis ASP.NET Session State and Output Caching providers?</span></span>
* <span data-ttu-id="66d7e-205">**Redis 輸出快取提供者** - 不需要變更。</span><span class="sxs-lookup"><span data-stu-id="66d7e-205">**Redis Output Cache provider** - no changes required.</span></span>
* <span data-ttu-id="66d7e-206">**Redis 工作階段狀態供應器** - 若要使用叢集，您必須使用 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，否則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="66d7e-206">**Redis Session State provider** - to use clustering, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="66d7e-207">這是一項重大變更。如需詳細資訊，請參閱 [v2.0.0 重大變更詳細資料](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-207">This is a breaking change; for more information see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span>

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a><span data-ttu-id="66d7e-208">當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="66d7e-208">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>
<span data-ttu-id="66d7e-209">如果您正在使用 StackExchange.Redis，並且在使用叢集時收到 `MOVE` 例外狀況，請確定您使用的是 [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="66d7e-209">If you are using StackExchange.Redis and receive `MOVE` exceptions when using clustering, ensure that you are using [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) or later.</span></span> <span data-ttu-id="66d7e-210">如需設定 .NET 應用程式以使用 StackExchange.Redis 的指示，請參閱 [設定快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="66d7e-210">For instructions on configuring your .NET applications to use StackExchange.Redis, see [Configure the cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d7e-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66d7e-211">Next steps</span></span>
<span data-ttu-id="66d7e-212">了解如何使用更多進階快取功能。</span><span class="sxs-lookup"><span data-stu-id="66d7e-212">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="66d7e-213">Azure Redis Cache 高階層簡介</span><span class="sxs-lookup"><span data-stu-id="66d7e-213">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







