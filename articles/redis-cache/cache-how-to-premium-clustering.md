---
title: "aaaHow tooconfigure Redis Premium Azure Redis 快取叢集 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理 Redis 叢集高檔的 Azure Redis 快取執行個體"
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
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a><span data-ttu-id="90d03-103">Tooconfigure Redis Premium Azure Redis 快取叢集</span><span class="sxs-lookup"><span data-stu-id="90d03-103">How tooconfigure Redis clustering for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="90d03-104">Azure Redis 快取都有不同的快取提供項目，提供有彈性地 hello 選擇的快取大小和功能，包括 Premium 層功能，例如叢集、 持續性和虛擬網路支援。</span><span class="sxs-lookup"><span data-stu-id="90d03-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="90d03-105">本文說明如何 tooconfigure 叢集的高階 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="90d03-105">This article describes how tooconfigure clustering in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="90d03-106">如需其他進階快取功能的資訊，請參閱[簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="90d03-106">For information on other premium cache features, see [Introduction toohello Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-redis-cluster"></a><span data-ttu-id="90d03-107">Redis 叢集是什麼？</span><span class="sxs-lookup"><span data-stu-id="90d03-107">What is Redis Cluster?</span></span>
<span data-ttu-id="90d03-108">Azure Redis 快取提供 Redis 叢集的方式，就像 [實作於 Redis](http://redis.io/topics/cluster-tutorial)一樣。</span><span class="sxs-lookup"><span data-stu-id="90d03-108">Azure Redis Cache offers Redis cluster as [implemented in Redis](http://redis.io/topics/cluster-tutorial).</span></span> <span data-ttu-id="90d03-109">Redis 叢集後，您會收到 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="90d03-109">With Redis Cluster, you get hello following benefits:</span></span> 

* <span data-ttu-id="90d03-110">hello 能力 tooautomatically 分割您在多個節點之間的資料集。</span><span class="sxs-lookup"><span data-stu-id="90d03-110">hello ability tooautomatically split your dataset among multiple nodes.</span></span> 
* <span data-ttu-id="90d03-111">hello 能力 toocontinue 作業時子集的 hello 節點發生失敗或無法 toocommunicate 與 hello hello 叢集其餘部分。</span><span class="sxs-lookup"><span data-stu-id="90d03-111">hello ability toocontinue operations when a subset of hello nodes is experiencing failures or are unable toocommunicate with hello rest of hello cluster.</span></span> 
* <span data-ttu-id="90d03-112">增加輸送量： 輸送量增加以線性方式隨著您增加 hello 分區的數目。</span><span class="sxs-lookup"><span data-stu-id="90d03-112">More throughput: Throughput increases linearly as you increase hello number of shards.</span></span> 
* <span data-ttu-id="90d03-113">更多的記憶體大小： 以線性方式隨著您增加 hello 分區的數目。</span><span class="sxs-lookup"><span data-stu-id="90d03-113">More memory size: Increases linearly as you increase hello number of shards.</span></span>  

<span data-ttu-id="90d03-114">如需進階快取的大小、輸送量和頻寬的詳細資訊，請參閱[應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="90d03-114">For more information about size, throughput, and bandwidth with premium caches, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>

<span data-ttu-id="90d03-115">在 Azure 中，Redis 叢集被提供做為主要/複本模型，其中每個分區都有複寫的主要/複本組 hello 複寫受 Azure Redis 快取服務的位置。</span><span class="sxs-lookup"><span data-stu-id="90d03-115">In Azure, Redis cluster is offered as a primary/replica model where each shard has a primary/replica pair with replication where hello replication is managed by Azure Redis Cache service.</span></span> 

## <a name="clustering"></a><span data-ttu-id="90d03-116">叢集</span><span class="sxs-lookup"><span data-stu-id="90d03-116">Clustering</span></span>
<span data-ttu-id="90d03-117">叢集上 hello 啟用**新增 Redis 快取**快取建立期間的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90d03-117">Clustering is enabled on hello **New Redis Cache** blade during cache creation.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="90d03-118">叢集上 hello 設定**Redis 叢集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="90d03-118">Clustering is configured on hello **Redis Cluster** blade.</span></span>

![叢集][redis-cache-clustering]

<span data-ttu-id="90d03-120">您可以向上 too10 分區 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="90d03-120">You can have up too10 shards in hello cluster.</span></span> <span data-ttu-id="90d03-121">按一下**啟用**和滑桿 hello 或輸入介於 1 到 10 之間的數字**分區計數**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="90d03-121">Click **Enabled** and slide hello slider or type a number between 1 and 10 for **Shard count** and click **OK**.</span></span>

<span data-ttu-id="90d03-122">每個分區都是一個主要/複本快取配對受 Azure，而 hello hello 快取的大小總計的計算方式是 hello 分區數目乘以 hello 定價層中選取的 hello 快取大小。</span><span class="sxs-lookup"><span data-stu-id="90d03-122">Each shard is a primary/replica cache pair managed by Azure, and hello total size of hello cache is calculated by multiplying hello number of shards by hello cache size selected in hello pricing tier.</span></span> 

![叢集][redis-cache-clustering-selected]

<span data-ttu-id="90d03-124">一旦建立 hello 快取連接 tooit 和使用，只要有非叢集的快取，並 Redis 散發整個 hello 快取分區的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="90d03-124">Once hello cache is created you connect tooit and use it just like a non-clustered cache, and Redis distributes hello data throughout hello Cache shards.</span></span> <span data-ttu-id="90d03-125">如果是診斷[啟用](cache-how-to-monitor.md#enable-cache-diagnostics)，度量資訊會為每個分區分別擷取，而且可以是[檢視](cache-how-to-monitor.md)hello Redis 快取刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="90d03-125">If diagnostics is [enabled](cache-how-to-monitor.md#enable-cache-diagnostics), metrics are captured separately for each shard and can be [viewed](cache-how-to-monitor.md) in hello Redis Cache blade.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="90d03-126">在設定叢集時，用戶端應用程式中的必要設定有些微差異。</span><span class="sxs-lookup"><span data-stu-id="90d03-126">There are some minor differences required in your client application when clustering is configured.</span></span> <span data-ttu-id="90d03-127">如需詳細資訊，請參閱[需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse 嗎？](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="90d03-127">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>
> 
> 

<span data-ttu-id="90d03-128">如需使用的群集與 hello StackExchange.Redis 用戶端的範例程式碼，請參閱 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs)部分 hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。</span><span class="sxs-lookup"><span data-stu-id="90d03-128">For sample code on working with clustering with hello StackExchange.Redis client, see hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a><span data-ttu-id="90d03-129">變更 hello 叢集大小上執行的進階版快取</span><span class="sxs-lookup"><span data-stu-id="90d03-129">Change hello cluster size on a running premium cache</span></span>
<span data-ttu-id="90d03-130">toochange hello 叢集大小上執行的高階快取叢集的已啟用，按一下**Redis 叢集大小**從 hello**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="90d03-130">toochange hello cluster size on a running premium cache with clustering enabled, click **Redis Cluster Size** from hello **Resource menu**.</span></span>

> [!NOTE]
> <span data-ttu-id="90d03-131">雖然 hello Azure Redis 快取進階層已被釋放 tooGeneral 可用性，hello Redis 叢集大小功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="90d03-131">While hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 叢集大小][redis-cache-redis-cluster-size]

<span data-ttu-id="90d03-133">toochange hello 叢集大小，使用 hello 滑桿，或輸入介於 1 到 10 之間的數字 hello**分區計數**文字方塊中，然後按一下**確定**toosave。</span><span class="sxs-lookup"><span data-stu-id="90d03-133">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!NOTE]
> <span data-ttu-id="90d03-134">調整叢集中執行 hello[移轉](https://redis.io/commands/migrate)命令，它是高度耗費資源的命令，因此影響降到最低，請考慮執行這項作業在非尖峰時間。</span><span class="sxs-lookup"><span data-stu-id="90d03-134">Scaling a cluster runs hello [MIGRATE](https://redis.io/commands/migrate) command, which is an expensive command, so for minimal impact, consider running this operation during non-peak hours.</span></span> <span data-ttu-id="90d03-135">在 hello 移轉過程中，您會看到伺服器負載中的突然增加。</span><span class="sxs-lookup"><span data-stu-id="90d03-135">During hello migration process, you will see a spike in server load.</span></span> <span data-ttu-id="90d03-136">調整叢集長時間執行程序，並且 hello 所需的時間取決於 hello 索引鍵的數目和大小 hello 這些索引鍵相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="90d03-136">Scaling a cluster is a long running process and hello amount of time taken depends on hello number of keys and size of hello values associated with those keys.</span></span>
> 
> 

## <a name="clustering-faq"></a><span data-ttu-id="90d03-137">叢集常見問題集</span><span class="sxs-lookup"><span data-stu-id="90d03-137">Clustering FAQ</span></span>
<span data-ttu-id="90d03-138">hello 下列清單包含 Azure Redis 快取叢集的相關常見問題的解答 toocommonly。</span><span class="sxs-lookup"><span data-stu-id="90d03-138">hello following list contains answers toocommonly asked questions about Azure Redis Cache clustering.</span></span>

* [<span data-ttu-id="90d03-139">我需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse？</span><span class="sxs-lookup"><span data-stu-id="90d03-139">Do I need toomake any changes toomy client application toouse clustering?</span></span>](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [<span data-ttu-id="90d03-140">如何在叢集中散發索引鍵？</span><span class="sxs-lookup"><span data-stu-id="90d03-140">How are keys distributed in a cluster?</span></span>](#how-are-keys-distributed-in-a-cluster)
* [<span data-ttu-id="90d03-141">Hello 我可以建立最大快取大小為何？</span><span class="sxs-lookup"><span data-stu-id="90d03-141">What is hello largest cache size I can create?</span></span>](#what-is-the-largest-cache-size-i-can-create)
* [<span data-ttu-id="90d03-142">所有 Redis 用戶端都支援叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-142">Do all Redis clients support clustering?</span></span>](#do-all-redis-clients-support-clustering)
* [<span data-ttu-id="90d03-143">當叢集已啟用時如何連接 toomy 快取？</span><span class="sxs-lookup"><span data-stu-id="90d03-143">How do I connect toomy cache when clustering is enabled?</span></span>](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [<span data-ttu-id="90d03-144">我可以直接連接 我的快取 toohello 個別的分區嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-144">Can I directly connect toohello individual shards of my cache?</span></span>](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [<span data-ttu-id="90d03-145">我可以為先前建立的快取設定叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-145">Can I configure clustering for a previously created cache?</span></span>](#can-i-configure-clustering-for-a-previously-created-cache)
* [<span data-ttu-id="90d03-146">我可以設定基本或標準快取的叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-146">Can I configure clustering for a basic or standard cache?</span></span>](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [<span data-ttu-id="90d03-147">我可以使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-147">Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?</span></span>](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [<span data-ttu-id="90d03-148">當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="90d03-148">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a><span data-ttu-id="90d03-149">我需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse？</span><span class="sxs-lookup"><span data-stu-id="90d03-149">Do I need toomake any changes toomy client application toouse clustering?</span></span>
* <span data-ttu-id="90d03-150">啟用叢集時，只可以使用資料庫 0。</span><span class="sxs-lookup"><span data-stu-id="90d03-150">When clustering is enabled, only database 0 is available.</span></span> <span data-ttu-id="90d03-151">如果用戶端應用程式會使用多個資料庫，而且它會嘗試 tooread 或寫入 tooa 資料庫不是 0，hello 下列擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="90d03-151">If your client application uses multiple databases and it tries tooread or write tooa database other than 0, hello following exception is thrown.</span></span> <span data-ttu-id="90d03-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`</span><span class="sxs-lookup"><span data-stu-id="90d03-152">`Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`</span></span>
  
  <span data-ttu-id="90d03-153">如需詳細資訊，請參閱 [Redis 叢集規格 - 實作的子集](http://redis.io/topics/cluster-spec#implemented-subset)。</span><span class="sxs-lookup"><span data-stu-id="90d03-153">For more information, see [Redis Cluster Specification - Implemented subset](http://redis.io/topics/cluster-spec#implemented-subset).</span></span>
* <span data-ttu-id="90d03-154">如果您使用 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/)，則必須使用 1.0.481 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="90d03-154">If you are using [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), you must use 1.0.481 or later.</span></span> <span data-ttu-id="90d03-155">連接 toohello 快取使用 hello 相同[端點、 連接埠和索引鍵](cache-configure.md#properties)連接 tooa 快取，但是沒有啟用叢集時，所使用。</span><span class="sxs-lookup"><span data-stu-id="90d03-155">You connect toohello cache using hello same [endpoints, ports, and keys](cache-configure.md#properties) that you use when connecting tooa cache that does not have clustering enabled.</span></span> <span data-ttu-id="90d03-156">hello 唯一的差異在於，所有讀取和寫入必須都以 toodatabase 0。</span><span class="sxs-lookup"><span data-stu-id="90d03-156">hello only difference is that all reads and writes must be done toodatabase 0.</span></span>
  
  * <span data-ttu-id="90d03-157">其他用戶端可能有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="90d03-157">Other clients may have different requirements.</span></span> <span data-ttu-id="90d03-158">請參閱 [所有 Redis 用戶端都支援叢集嗎？](#do-all-redis-clients-support-clustering)</span><span class="sxs-lookup"><span data-stu-id="90d03-158">See [Do all Redis clients support clustering?](#do-all-redis-clients-support-clustering)</span></span>
* <span data-ttu-id="90d03-159">如果您的應用程式使用多個索引鍵作業批次處理到單一命令，必須位於所有索引鍵中 hello 相同分區。</span><span class="sxs-lookup"><span data-stu-id="90d03-159">If your application uses multiple key operations batched into a single command, all keys must be located in hello same shard.</span></span> <span data-ttu-id="90d03-160">toolocate 金鑰在 hello 相同分區，請參閱[金鑰散發在叢集中的方式？](#how-are-keys-distributed-in-a-cluster)</span><span class="sxs-lookup"><span data-stu-id="90d03-160">toolocate keys in hello same shard, see [How are keys distributed in a cluster?](#how-are-keys-distributed-in-a-cluster)</span></span>
* <span data-ttu-id="90d03-161">如果您使用 Redis ASP.NET 工作階段狀態提供者，則必須使用 2.0.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="90d03-161">If you are using Redis ASP.NET Session State provider you must use 2.0.1 or higher.</span></span> <span data-ttu-id="90d03-162">請參閱[使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span><span class="sxs-lookup"><span data-stu-id="90d03-162">See [Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)</span></span>

### <a name="how-are-keys-distributed-in-a-cluster"></a><span data-ttu-id="90d03-163">如何在叢集中散發索引鍵？</span><span class="sxs-lookup"><span data-stu-id="90d03-163">How are keys distributed in a cluster?</span></span>
<span data-ttu-id="90d03-164">每個 hello Redis[金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model)文件： hello 金鑰空間分割成 16384 的位置。</span><span class="sxs-lookup"><span data-stu-id="90d03-164">Per hello Redis [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model) documentation: hello key space is split into 16384 slots.</span></span> <span data-ttu-id="90d03-165">每個索引鍵是雜湊，並指派 tooone 的這些介面槽分散於 hello hello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="90d03-165">Each key is hashed and assigned tooone of these slots, which are distributed across hello nodes of hello cluster.</span></span> <span data-ttu-id="90d03-166">您可以設定 hello 索引鍵的一部分是位於多個索引鍵的雜湊的 tooensure hello 相同分區使用雜湊標記。</span><span class="sxs-lookup"><span data-stu-id="90d03-166">You can configure which part of hello key is hashed tooensure that multiple keys are located in hello same shard using hash tags.</span></span>

* <span data-ttu-id="90d03-167">索引鍵，並雜湊標記-如果 hello 索引鍵的任何一部分住`{`和`}`，只有該 hello 索引鍵的一部分會基於 hello 判斷 hello 雜湊位置索引鍵的雜湊。</span><span class="sxs-lookup"><span data-stu-id="90d03-167">Keys with a hash tag - if any part of hello key is enclosed in `{` and `}`, only that part of hello key is hashed for hello purposes of determining hello hash slot of a key.</span></span> <span data-ttu-id="90d03-168">例如，下列 3 個索引鍵的 hello 可能位在 hello 相同分區： `{key}1`， `{key}2`，和`{key}3`自只 hello `key` hello 名稱的一部分進行雜湊處理。</span><span class="sxs-lookup"><span data-stu-id="90d03-168">For example, hello following 3 keys would be located in hello same shard: `{key}1`, `{key}2`, and `{key}3` since only hello `key` part of hello name is hashed.</span></span> <span data-ttu-id="90d03-169">如需索引鍵主題標籤規格的完整清單，請參閱[索引鍵主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。</span><span class="sxs-lookup"><span data-stu-id="90d03-169">For a complete list of keys hash tag specifications, see [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>
* <span data-ttu-id="90d03-170">沒有雜湊標記-hello 整個索引鍵名稱的索引鍵使用雜湊。</span><span class="sxs-lookup"><span data-stu-id="90d03-170">Keys without a hash tag - hello entire key name is used for hashing.</span></span> <span data-ttu-id="90d03-171">這會導致統計上平均分佈在 hello 分區 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="90d03-171">This results in a statistically even distribution across hello shards of hello cache.</span></span>

<span data-ttu-id="90d03-172">為了最佳效能和輸送量，建議您平均散發 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="90d03-172">For best performance and throughput, we recommend distributing hello keys evenly.</span></span> <span data-ttu-id="90d03-173">如果您正在使用的雜湊標記中的索引鍵是平均分佈 hello 應用程式的責任 tooensure hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="90d03-173">If you are using keys with a hash tag it is hello application's responsibility tooensure hello keys are distributed evenly.</span></span>

<span data-ttu-id="90d03-174">如需詳細資訊，請參閱[金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model)、[Redis 叢集資料分區化](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding)和[金鑰主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。</span><span class="sxs-lookup"><span data-stu-id="90d03-174">For more information, see [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis Cluster data sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), and [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags).</span></span>

<span data-ttu-id="90d03-175">使用叢集和在 hello 中尋找機碼的範例程式碼相同的分區，與 hello StackExchange.Redis 用戶端，請參閱 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs)部分 hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。</span><span class="sxs-lookup"><span data-stu-id="90d03-175">For sample code on working with clustering and locating keys in hello same shard with hello StackExchange.Redis client, see hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) portion of hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>

### <a name="what-is-hello-largest-cache-size-i-can-create"></a><span data-ttu-id="90d03-176">Hello 我可以建立最大快取大小為何？</span><span class="sxs-lookup"><span data-stu-id="90d03-176">What is hello largest cache size I can create?</span></span>
<span data-ttu-id="90d03-177">hello 最大 premium 快取大小為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="90d03-177">hello largest premium cache size is 53 GB.</span></span> <span data-ttu-id="90d03-178">您可以建立註冊 too10 分區，提供 530 GB 的最大大小。</span><span class="sxs-lookup"><span data-stu-id="90d03-178">You can create up too10 shards giving you a maximum size of 530 GB.</span></span> <span data-ttu-id="90d03-179">如果您需要較大的大小，可以 [要求更多](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase)。</span><span class="sxs-lookup"><span data-stu-id="90d03-179">If you need a larger size you can [request more](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase).</span></span> <span data-ttu-id="90d03-180">如需詳細資訊，請參閱 [Azure Redis 快取價格](https://azure.microsoft.com/pricing/details/cache/)。</span><span class="sxs-lookup"><span data-stu-id="90d03-180">For more information, see [Azure Redis Cache Pricing](https://azure.microsoft.com/pricing/details/cache/).</span></span>

### <a name="do-all-redis-clients-support-clustering"></a><span data-ttu-id="90d03-181">所有 Redis 用戶端都支援叢集嗎？ </span><span class="sxs-lookup"><span data-stu-id="90d03-181">Do all Redis clients support clustering?</span></span>
<span data-ttu-id="90d03-182">在 hello 目前時間並非所有支援的用戶端都 Redis 叢集。</span><span class="sxs-lookup"><span data-stu-id="90d03-182">At hello present time not all clients support Redis clustering.</span></span> <span data-ttu-id="90d03-183">StackExchange.Redis 就是不支援的其中一例。</span><span class="sxs-lookup"><span data-stu-id="90d03-183">StackExchange.Redis is one that does support for it.</span></span> <span data-ttu-id="90d03-184">如需其他用戶端的詳細資訊，請參閱 hello[播放與 hello 叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)區段 hello [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)。</span><span class="sxs-lookup"><span data-stu-id="90d03-184">For more information on other clients, see hello [Playing with hello cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) section of hello [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

> [!NOTE]
> <span data-ttu-id="90d03-185">如果您使用 StackExchange.Redis 作為您的用戶端，請確定您使用 hello 最新版本的[StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 或更新版本的正確叢集 toowork。</span><span class="sxs-lookup"><span data-stu-id="90d03-185">If you are using StackExchange.Redis as your client, ensure you are using hello latest version of [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 or later for clustering toowork correctly.</span></span> <span data-ttu-id="90d03-186">如果您有任何關於 Move 例外狀況的問題，請參閱 [Move 例外狀況](#move-exceptions) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="90d03-186">If you have any issues with move exceptions, see [move exceptions](#move-exceptions) for more information.</span></span>
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a><span data-ttu-id="90d03-187">當叢集已啟用時如何連接 toomy 快取？</span><span class="sxs-lookup"><span data-stu-id="90d03-187">How do I connect toomy cache when clustering is enabled?</span></span>
<span data-ttu-id="90d03-188">您可以連接 tooyour 快取使用 hello 相同[端點](cache-configure.md#properties)，[連接埠](cache-configure.md#properties)，和[金鑰](cache-configure.md#access-keys)連接 tooa 快取，但是沒有啟用叢集時，所使用。</span><span class="sxs-lookup"><span data-stu-id="90d03-188">You can connect tooyour cache using hello same [endpoints](cache-configure.md#properties), [ports](cache-configure.md#properties), and [keys](cache-configure.md#access-keys) that you use when connecting tooa cache that does not have clustering enabled.</span></span> <span data-ttu-id="90d03-189">Redis 管理叢集 hello 後端上，所以您不需 toomanage hello 從您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="90d03-189">Redis manages hello clustering on hello backend so you don't have toomanage it from your client.</span></span>

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a><span data-ttu-id="90d03-190">我可以直接連接 我的快取 toohello 個別的分區嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-190">Can I directly connect toohello individual shards of my cache?</span></span>
<span data-ttu-id="90d03-191">目前官方尚未提供支援。</span><span class="sxs-lookup"><span data-stu-id="90d03-191">This is not officially supported.</span></span> <span data-ttu-id="90d03-192">如前所述，每個分區都包含一個主要/複本快取組，統稱為快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="90d03-192">With that said, each shard consists of a primary/replica cache pair, collectively known as a cache instance.</span></span> <span data-ttu-id="90d03-193">您可以連接 toothese 快取執行個體使用 hello redis cli 公用程式在 hello[不穩定](http://redis.io/download)hello Redis GitHub 儲存機制分支。</span><span class="sxs-lookup"><span data-stu-id="90d03-193">You can connect toothese cache instances using hello redis-cli utility in hello [unstable](http://redis.io/download) branch of hello Redis repository at GitHub.</span></span> <span data-ttu-id="90d03-194">這個版本會實作基本支援啟動與 hello`-c`切換。</span><span class="sxs-lookup"><span data-stu-id="90d03-194">This version implements basic support when started with hello `-c` switch.</span></span> <span data-ttu-id="90d03-195">如需詳細資訊，請參閱[播放與 hello 叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)上[http://redis.io](http://redis.io)在 hello [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)。</span><span class="sxs-lookup"><span data-stu-id="90d03-195">For more information see [Playing with hello cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) on [http://redis.io](http://redis.io) in hello [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>

<span data-ttu-id="90d03-196">非 ssl，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="90d03-196">For non-ssl, use hello following commands.</span></span>

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

<span data-ttu-id="90d03-197">如為 SSL，將 `1300N` 取代為 `1500N`。</span><span class="sxs-lookup"><span data-stu-id="90d03-197">For ssl, replace `1300N` with `1500N`.</span></span>

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a><span data-ttu-id="90d03-198">我可以為先前建立的快取設定叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-198">Can I configure clustering for a previously created cache?</span></span>
<span data-ttu-id="90d03-199">目前您只能在建立快取時啟用叢集。</span><span class="sxs-lookup"><span data-stu-id="90d03-199">Currently you can only enable clustering when you create a cache.</span></span> <span data-ttu-id="90d03-200">之後，建立 hello 快取，但您無法加入叢集 tooa 進階版快取，或移除建立 hello 快取之後，從進階版快取叢集，您可以變更 hello 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="90d03-200">You can change hello cluster size after hello cache is created, but you can't add clustering tooa premium cache or remove clustering from a premium cache after hello cache is created.</span></span> <span data-ttu-id="90d03-201">進階版快取與啟用叢集只有一個分區是 hello 的不同的大小與任何叢集相同進階版快取。</span><span class="sxs-lookup"><span data-stu-id="90d03-201">A premium cache with clustering enabled and only one shard is different than a premium cache of hello same size with no clustering.</span></span>

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a><span data-ttu-id="90d03-202">我可以設定基本或標準快取的叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-202">Can I configure clustering for a basic or standard cache?</span></span>
<span data-ttu-id="90d03-203">叢集僅適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="90d03-203">Clustering is only available for premium caches.</span></span>

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a><span data-ttu-id="90d03-204">我可以使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？</span><span class="sxs-lookup"><span data-stu-id="90d03-204">Can I use clustering with hello Redis ASP.NET Session State and Output Caching providers?</span></span>
* <span data-ttu-id="90d03-205">**Redis 輸出快取提供者** - 不需要變更。</span><span class="sxs-lookup"><span data-stu-id="90d03-205">**Redis Output Cache provider** - no changes required.</span></span>
* <span data-ttu-id="90d03-206">**Redis 工作階段狀態提供者**-toouse 叢集，您必須使用[RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，或例外狀況就會擲回。</span><span class="sxs-lookup"><span data-stu-id="90d03-206">**Redis Session State provider** - toouse clustering, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="90d03-207">這是一項重大變更。如需詳細資訊，請參閱 [v2.0.0 重大變更詳細資料](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。</span><span class="sxs-lookup"><span data-stu-id="90d03-207">This is a breaking change; for more information see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span>

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a><span data-ttu-id="90d03-208">當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="90d03-208">I am getting MOVE exceptions when using StackExchange.Redis and clustering, what should I do?</span></span>
<span data-ttu-id="90d03-209">如果您正在使用 StackExchange.Redis，並且在使用叢集時收到 `MOVE` 例外狀況，請確定您使用的是 [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="90d03-209">If you are using StackExchange.Redis and receive `MOVE` exceptions when using clustering, ensure that you are using [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) or later.</span></span> <span data-ttu-id="90d03-210">如需設定您的.NET 應用程式 toouse StackExchange.Redis 指示，請參閱[設定 hello 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="90d03-210">For instructions on configuring your .NET applications toouse StackExchange.Redis, see [Configure hello cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90d03-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90d03-211">Next steps</span></span>
<span data-ttu-id="90d03-212">了解如何更進階的 toouse 快取功能。</span><span class="sxs-lookup"><span data-stu-id="90d03-212">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="90d03-213">簡介 toohello Azure Redis 快取進階層</span><span class="sxs-lookup"><span data-stu-id="90d03-213">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







