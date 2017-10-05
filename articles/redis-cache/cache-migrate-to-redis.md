---
title: "將受管理的快取服務應用程式移轉至 Redis - Azure | Microsoft Docs"
description: "了解如何將受管理的快取服務和 In-Role Cache 應用程式移轉至 Azure Redis Cache"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: 0fbfb945c66926794721f2ce8cc183dac51ecb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-from-managed-cache-service-to-azure-redis-cache"></a><span data-ttu-id="12563-103">從受管理的快取服務移轉至 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="12563-103">Migrate from Managed Cache Service to Azure Redis Cache</span></span>
<span data-ttu-id="12563-104">若想將使用 Azure 受管理的快取服務的應用程式移轉至 Azure Redis 快取，您幾乎不需要變更應用程式就可達成，詳細情形取決於快取應用程式所使用的受管理的快取服務功能。</span><span class="sxs-lookup"><span data-stu-id="12563-104">Migrating your applications that use Azure Managed Cache Service to Azure Redis Cache can be accomplished with minimal changes to your application, depending on the Managed Cache Service features used by your caching application.</span></span> <span data-ttu-id="12563-105">API 雖非完全相同，但卻極為類似，而且您現有使用受管理的快取服務來存取快取的程式碼，大多只需要略做變更即可重複使用。</span><span class="sxs-lookup"><span data-stu-id="12563-105">While the APIs are not exactly the same they are similar, and much of your existing code that uses Managed Cache Service to access a cache can be reused with minimal changes.</span></span> <span data-ttu-id="12563-106">本主題說明如何對設定和應用程式進行必要的變更，以將受管理的快取服務應用程式移轉為使用 Azure Redis 快取，並說明如何使用 Azure Redis 快取的某些功能，來實作受管理的快取服務快取的功能。</span><span class="sxs-lookup"><span data-stu-id="12563-106">This topic shows how to make the necessary configuration and application changes to migrate your Managed Cache Service applications to use Azure Redis Cache, and shows how some of the features of Azure Redis Cache can be used to implement the functionality of a Managed Cache Service cache.</span></span>

>[!NOTE]
><span data-ttu-id="12563-107">受管理的快取服務及 In-Role Cache 已於 2016 年 11 月 30 日起[淘汰](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。</span><span class="sxs-lookup"><span data-stu-id="12563-107">Managed Cache Service and In-Role Cache were [retired](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) November 30, 2016.</span></span> <span data-ttu-id="12563-108">如果您有任何 In-Role Cache 部署想要移轉到 Azure Redis Cache，您可以依照這篇文章中的步驟作業。</span><span class="sxs-lookup"><span data-stu-id="12563-108">If you have any In-Role Cache deployments that you want to migrate to Azure Redis Cache, you can follow the steps in this article.</span></span>

## <a name="migration-steps"></a><span data-ttu-id="12563-109">移轉步驟</span><span class="sxs-lookup"><span data-stu-id="12563-109">Migration Steps</span></span>
<span data-ttu-id="12563-110">要將受管理的快取服務應用程式移轉為使用 Azure Redis 快取，需要執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="12563-110">The following steps are required to migrate a Managed Cache Service application to use Azure Redis Cache.</span></span>

* <span data-ttu-id="12563-111">將受管理的快取服務功能對應至 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="12563-111">Map Managed Cache Service features to Azure Redis Cache</span></span>
* <span data-ttu-id="12563-112">選擇快取服務</span><span class="sxs-lookup"><span data-stu-id="12563-112">Choose a Cache Offering</span></span>
* <span data-ttu-id="12563-113">建立快取</span><span class="sxs-lookup"><span data-stu-id="12563-113">Create a Cache</span></span>
* <span data-ttu-id="12563-114">設定快取用戶端</span><span class="sxs-lookup"><span data-stu-id="12563-114">Configure the Cache Clients</span></span>
  * <span data-ttu-id="12563-115">移除受管理的快取服務設定</span><span class="sxs-lookup"><span data-stu-id="12563-115">Remove the Managed Cache Service Configuration</span></span>
  * <span data-ttu-id="12563-116">設定使用 StackExchange.Redis NuGet 封裝的快取用戶端</span><span class="sxs-lookup"><span data-stu-id="12563-116">Configure a cache client using the StackExchange.Redis NuGet Package</span></span>
* <span data-ttu-id="12563-117">移轉受管理的快取服務程式碼</span><span class="sxs-lookup"><span data-stu-id="12563-117">Migrate Managed Cache Service code</span></span>
  * <span data-ttu-id="12563-118">使用 ConnectionMultiplexer 類別連接到快取</span><span class="sxs-lookup"><span data-stu-id="12563-118">Connect to the cache using the ConnectionMultiplexer class</span></span>
  * <span data-ttu-id="12563-119">存取快取中的基本資料型別</span><span class="sxs-lookup"><span data-stu-id="12563-119">Access primitive data types in the cache</span></span>
  * <span data-ttu-id="12563-120">使用快取中的 .NET 物件</span><span class="sxs-lookup"><span data-stu-id="12563-120">Work with .NET objects in the cache</span></span>
* <span data-ttu-id="12563-121">將 ASP.NET 工作階段狀態和輸出快取移轉至 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="12563-121">Migrate ASP.NET Session State and Output caching to Azure Redis Cache</span></span> 

## <a name="map-managed-cache-service-features-to-azure-redis-cache"></a><span data-ttu-id="12563-122">將受管理的快取服務功能對應至 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="12563-122">Map Managed Cache Service features to Azure Redis Cache</span></span>
<span data-ttu-id="12563-123">Azure 受管理的快取服務與 Azure Redis 快取類似，但兩者在實作某些功能時會使用不同的方式。</span><span class="sxs-lookup"><span data-stu-id="12563-123">Azure Managed Cache Service and Azure Redis Cache are similar but implement some of their features in different ways.</span></span> <span data-ttu-id="12563-124">本節將描述其中的一些差異，並提供有關在 Azure Redis 快取中實作受管理的快取服務功能的指引。</span><span class="sxs-lookup"><span data-stu-id="12563-124">This section describes some of the differences and provides guidance on implementing the features of Managed Cache Service in Azure Redis Cache.</span></span>

| <span data-ttu-id="12563-125">受管理的快取服務功能</span><span class="sxs-lookup"><span data-stu-id="12563-125">Managed Cache Service feature</span></span> | <span data-ttu-id="12563-126">受管理的快取服務支援</span><span class="sxs-lookup"><span data-stu-id="12563-126">Managed Cache Service support</span></span> | <span data-ttu-id="12563-127">Azure Redis 快取支援</span><span class="sxs-lookup"><span data-stu-id="12563-127">Azure Redis Cache support</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12563-128">具名快取</span><span class="sxs-lookup"><span data-stu-id="12563-128">Named caches</span></span> |<span data-ttu-id="12563-129">會設定預設快取，而在標準版和進階版快取服務中，還可以視需要額外設定多達 9 個具名快取。</span><span class="sxs-lookup"><span data-stu-id="12563-129">A default cache is configured, and in the Standard and Premium cache offerings, up to nine additional named caches can be configured if desired.</span></span> |<span data-ttu-id="12563-130">Azure Redis 快取具有可供用來對具名快取實作類似功能的可設定數目資料庫 (預設值為 16 個)。</span><span class="sxs-lookup"><span data-stu-id="12563-130">Azure Redis caches have a configurable number of databases (default of 16) that can be used to implement a similar functionality to named caches.</span></span> <span data-ttu-id="12563-131">如需詳細資訊，請參閱[什麼是 Redis 資料庫？](cache-faq.md#what-are-redis-databases)和[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="12563-131">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span> |
| <span data-ttu-id="12563-132">高可用性</span><span class="sxs-lookup"><span data-stu-id="12563-132">High Availability</span></span> |<span data-ttu-id="12563-133">在標準版和進階版快取服務中，會針對快取中的項目提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="12563-133">Provides high availability for items in the cache in the Standard and Premium cache offerings.</span></span> <span data-ttu-id="12563-134">如果因為失敗而導致項目遺失，快取中的項目仍有備份複本可供使用。</span><span class="sxs-lookup"><span data-stu-id="12563-134">If items are lost due to a failure, backup copies of the items in the cache are still available.</span></span> <span data-ttu-id="12563-135">次要快取的寫入作業是以同步方式進行。</span><span class="sxs-lookup"><span data-stu-id="12563-135">Writes to the secondary cache are made synchronously.</span></span> |<span data-ttu-id="12563-136">標準版和進階版快取服務有提供高可用性，其具有雙節點的主要/複本設定 (進階版快取的每個分區都有主要/複本配對)。</span><span class="sxs-lookup"><span data-stu-id="12563-136">High availability is available in the Standard and Premium cache offerings, which have a two node Primary/Replica configuration (each shard in a Premium cache has a primary/replica pair).</span></span> <span data-ttu-id="12563-137">複本的寫入作業是以非同步方式進行。</span><span class="sxs-lookup"><span data-stu-id="12563-137">Writes to the replica are made asynchronously.</span></span> <span data-ttu-id="12563-138">如需詳細資訊，請參閱 [Azure Redis 快取定價](https://azure.microsoft.com/pricing/details/cache/)。</span><span class="sxs-lookup"><span data-stu-id="12563-138">For more information, see [Azure Redis Cache pricing](https://azure.microsoft.com/pricing/details/cache/).</span></span> |
| <span data-ttu-id="12563-139">通知</span><span class="sxs-lookup"><span data-stu-id="12563-139">Notifications</span></span> |<span data-ttu-id="12563-140">當具名快取上發生各種快取作業時，允許用戶端接收非同步通知。</span><span class="sxs-lookup"><span data-stu-id="12563-140">Allows clients to receive asynchronous notifications when a variety of cache operations occur on a named cache.</span></span> |<span data-ttu-id="12563-141">用戶端應用程式可以使用 Redis 發行/訂閱或 [Keyspace 通知](cache-configure.md#keyspace-notifications-advanced-settings) 來達成和通知類似的功能。</span><span class="sxs-lookup"><span data-stu-id="12563-141">Client applications can use Redis pub/sub or [Keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings) to achieve a similar functionality to notifications.</span></span> |
| <span data-ttu-id="12563-142">本機快取</span><span class="sxs-lookup"><span data-stu-id="12563-142">Local cache</span></span> |<span data-ttu-id="12563-143">在用戶端本機上儲存快取物件的複本，以利快速存取。</span><span class="sxs-lookup"><span data-stu-id="12563-143">Stores a copy of cached objects locally on the client for extra-fast access.</span></span> |<span data-ttu-id="12563-144">用戶端應用程式必須使用字典或類似的資料結構來實作這項功能。</span><span class="sxs-lookup"><span data-stu-id="12563-144">Client applications would need to implement this functionality using a dictionary or similar data structure.</span></span> |
| <span data-ttu-id="12563-145">收回原則</span><span class="sxs-lookup"><span data-stu-id="12563-145">Eviction Policy</span></span> |<span data-ttu-id="12563-146">無或 LRU。</span><span class="sxs-lookup"><span data-stu-id="12563-146">None or LRU.</span></span> <span data-ttu-id="12563-147">預設原則是 LRU。</span><span class="sxs-lookup"><span data-stu-id="12563-147">The default policy is LRU.</span></span> |<span data-ttu-id="12563-148">Azure Redis 快取支援下列收回原則：volatile-lru、allkeys-lru、volatile-random、allkeys-random、volatile-ttl、noeviction。</span><span class="sxs-lookup"><span data-stu-id="12563-148">Azure Redis Cache supports the following eviction policies: volatile-lru, allkeys-lru, volatile-random, allkeys-random, volatile-ttl, noeviction.</span></span> <span data-ttu-id="12563-149">預設原則是 volatile-lru。</span><span class="sxs-lookup"><span data-stu-id="12563-149">The default policy is volatile-lru.</span></span> <span data-ttu-id="12563-150">如需詳細資訊，請參閱 [預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。</span><span class="sxs-lookup"><span data-stu-id="12563-150">For more information, see [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span> |
| <span data-ttu-id="12563-151">到期原則</span><span class="sxs-lookup"><span data-stu-id="12563-151">Expiration Policy</span></span> |<span data-ttu-id="12563-152">預設的到期原則為 [絕對]，預設的到期間隔為 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="12563-152">The default expiration policy is Absolute and the default expiration interval is ten minutes.</span></span> <span data-ttu-id="12563-153">另外也提供 [滑動] 和 [永不] 原則。</span><span class="sxs-lookup"><span data-stu-id="12563-153">Sliding and Never policies are also available.</span></span> |<span data-ttu-id="12563-154">依預設，快取中的項目不會到期，但可以使用快取集多載，對每筆寫入作業設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="12563-154">By default items in the cache do not expire, but an expiration can be configured on a per write basis using cache set overloads.</span></span> <span data-ttu-id="12563-155">如需詳細資訊，請參閱 [從快取加入和擷取物件](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache)。</span><span class="sxs-lookup"><span data-stu-id="12563-155">For more information, see [Add and retrieve objects from the cache](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache).</span></span> |
| <span data-ttu-id="12563-156">區域和標記</span><span class="sxs-lookup"><span data-stu-id="12563-156">Regions and Tagging</span></span> |<span data-ttu-id="12563-157">區域是快取項目的子群組。</span><span class="sxs-lookup"><span data-stu-id="12563-157">Regions are subgroups for cached items.</span></span> <span data-ttu-id="12563-158">區域也支援以稱為標記的額外描述性字串，來為快取項目加上註解。</span><span class="sxs-lookup"><span data-stu-id="12563-158">Regions also support the annotation of cached items with additional descriptive strings called tags.</span></span> <span data-ttu-id="12563-159">區域支援對該區域內的任何標記項目執行搜尋作業的能力。</span><span class="sxs-lookup"><span data-stu-id="12563-159">Regions support the ability to perform search operations on any tagged items in that region.</span></span> <span data-ttu-id="12563-160">區域內的所有項目都位於單一快取叢集節點內。</span><span class="sxs-lookup"><span data-stu-id="12563-160">All items within a region are located within a single node of the cache cluster.</span></span> |<span data-ttu-id="12563-161">Redis 快取是由單一節點所組成 (除非已啟用 Redis 叢集)，因此不適用受管理的快取服務區域的概念。</span><span class="sxs-lookup"><span data-stu-id="12563-161">A Redis cache consists of a single node (unless Redis cluster is enabled) so the concept of Managed Cache Service regions does not apply.</span></span> <span data-ttu-id="12563-162">Redis 支援在擷取索引鍵時執行搜尋和萬用字元作業，讓描述性標記可以內嵌在索引鍵名稱內並於稍後用來擷取項目。</span><span class="sxs-lookup"><span data-stu-id="12563-162">Redis supports searching and wildcard operations when retrieving keys so descriptive tags can be embedded within the key names and used to retrieve the items later.</span></span> <span data-ttu-id="12563-163">如需使用 Redis 實作標記解決方案的範例，請參閱 [使用 Redis 實作快取標記](http://stackify.com/implementing-cache-tagging-redis/)。</span><span class="sxs-lookup"><span data-stu-id="12563-163">For an example of implementing a tagging solution using Redis, see [Implementing cache tagging with Redis](http://stackify.com/implementing-cache-tagging-redis/).</span></span> |
| <span data-ttu-id="12563-164">序列化</span><span class="sxs-lookup"><span data-stu-id="12563-164">Serialization</span></span> |<span data-ttu-id="12563-165">受管理的快取支援 NetDataContractSerializer 和 BinaryFormatter，也支援使用自訂序列化程式。</span><span class="sxs-lookup"><span data-stu-id="12563-165">Managed Cache supports NetDataContractSerializer, BinaryFormatter, and the use of custom serializers.</span></span> <span data-ttu-id="12563-166">預設值為 NetDataContractSerializer。</span><span class="sxs-lookup"><span data-stu-id="12563-166">The default is NetDataContractSerializer.</span></span> |<span data-ttu-id="12563-167">由用戶端應用程式負責先將 .NET 物件序列化再將它們放入快取中，至於要選擇使用哪個序列化程式則由用戶端應用程式的開發人員決定。</span><span class="sxs-lookup"><span data-stu-id="12563-167">It is the responsibility of the client application to serialize .NET objects before placing them into the cache, with the choice of the serializer up to the client application developer.</span></span> <span data-ttu-id="12563-168">如需詳細資訊和範例程式碼，請參閱 [在快取中使用 .NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。</span><span class="sxs-lookup"><span data-stu-id="12563-168">For more information and sample code, see [Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span> |
| <span data-ttu-id="12563-169">快取模擬器</span><span class="sxs-lookup"><span data-stu-id="12563-169">Cache emulator</span></span> |<span data-ttu-id="12563-170">受管理的快取提供本機快取模擬器。</span><span class="sxs-lookup"><span data-stu-id="12563-170">Managed Cache provides a local cache emulator.</span></span> |<span data-ttu-id="12563-171">Azure Redis 快取沒有模擬器，但您可以 [在本機執行 redis-server.exe 的 MSOpenTech 組建](cache-faq.md#cache-emulator) 提供模擬器體驗。</span><span class="sxs-lookup"><span data-stu-id="12563-171">Azure Redis Cache does not have an emulator, but you can [run the MSOpenTech build of redis-server.exe locally](cache-faq.md#cache-emulator) to provide an emulator experience.</span></span> |

## <a name="choose-a-cache-offering"></a><span data-ttu-id="12563-172">選擇快取服務</span><span class="sxs-lookup"><span data-stu-id="12563-172">Choose a Cache Offering</span></span>
<span data-ttu-id="12563-173">Microsoft Azure Redis 快取有下列階層：</span><span class="sxs-lookup"><span data-stu-id="12563-173">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="12563-174">**基本** - 單一節點。</span><span class="sxs-lookup"><span data-stu-id="12563-174">**Basic** – Single node.</span></span> <span data-ttu-id="12563-175">多種大小，最高為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="12563-175">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="12563-176">**標準** – 兩個節點 (主要/從屬)。</span><span class="sxs-lookup"><span data-stu-id="12563-176">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="12563-177">多種大小，最高為 53 GB。</span><span class="sxs-lookup"><span data-stu-id="12563-177">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="12563-178">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="12563-178">99.9% SLA.</span></span>
* <span data-ttu-id="12563-179">**進階** – 兩個節點的主要/從屬，最多具有 10 個分區。</span><span class="sxs-lookup"><span data-stu-id="12563-179">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="12563-180">提供多種大小，範圍從 6 GB 到 530 GB。</span><span class="sxs-lookup"><span data-stu-id="12563-180">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="12563-181">所有「標準」層級的功能以及更多功能，可支援 [Redis 叢集](cache-how-to-premium-clustering.md)、[Redis 持續性](cache-how-to-premium-persistence.md)和 [Azure 虛擬網路](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="12563-181">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="12563-182">99.9% SLA。</span><span class="sxs-lookup"><span data-stu-id="12563-182">99.9% SLA.</span></span>

<span data-ttu-id="12563-183">每一個階層都有不同的功能和價格。</span><span class="sxs-lookup"><span data-stu-id="12563-183">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="12563-184">本指南稍後將探討這些功能，如需定價的詳細資訊，請參閱 [快取定價詳細資料](https://azure.microsoft.com/pricing/details/cache/)。</span><span class="sxs-lookup"><span data-stu-id="12563-184">The features are covered later in this guide, and for more information on pricing, see [Cache Pricing Details](https://azure.microsoft.com/pricing/details/cache/).</span></span>

<span data-ttu-id="12563-185">移轉作業的第一步是挑選符合先前受管理的快取服務快取大小的容量，然後再依據應用程式的需求擴大或縮小規模。</span><span class="sxs-lookup"><span data-stu-id="12563-185">A starting point for migration is to pick the size that matches the size of your previous Managed Cache Service cache, and then scale up or down depending on the requirements of your application.</span></span> <span data-ttu-id="12563-186">如須選擇合適的 Azure Redis 快取服務的詳細指引，請參閱 [應該使用哪個 Redis 快取服務和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。</span><span class="sxs-lookup"><span data-stu-id="12563-186">For more guidance on choosing the right Azure Redis Cache offering, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="create-a-cache"></a><span data-ttu-id="12563-187">建立快取</span><span class="sxs-lookup"><span data-stu-id="12563-187">Create a Cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-the-cache-clients"></a><span data-ttu-id="12563-188">設定快取用戶端</span><span class="sxs-lookup"><span data-stu-id="12563-188">Configure the Cache Clients</span></span>
<span data-ttu-id="12563-189">一旦建立並設定快取，下一步是移除受管理的快取服務設定，並加入 Azure Redis 快取設定和參考，讓快取用戶端可以存取快取。</span><span class="sxs-lookup"><span data-stu-id="12563-189">Once the cache is created and configured, the next step is to remove the Managed Cache Service configuration, and add the add the Azure Redis Cache configuration and references so that cache clients can access the cache.</span></span>

* <span data-ttu-id="12563-190">移除受管理的快取服務設定</span><span class="sxs-lookup"><span data-stu-id="12563-190">Remove the Managed Cache Service Configuration</span></span>
* <span data-ttu-id="12563-191">設定使用 StackExchange.Redis NuGet 封裝的快取用戶端</span><span class="sxs-lookup"><span data-stu-id="12563-191">Configure a cache client using the StackExchange.Redis NuGet Package</span></span>

### <a name="remove-the-managed-cache-service-configuration"></a><span data-ttu-id="12563-192">移除受管理的快取服務設定</span><span class="sxs-lookup"><span data-stu-id="12563-192">Remove the Managed Cache Service Configuration</span></span>
<span data-ttu-id="12563-193">要將用戶端應用程式設定為使用 Azure Redis 快取，必須先解除安裝受管理的快取服務 NuGet 封裝，以便移除現有受管理的快取服務的設定和組件參考。</span><span class="sxs-lookup"><span data-stu-id="12563-193">Before the client applications can be configured for Azure Redis Cache, the existing Managed Cache Service configuration and assembly references must be removed by uninstalling the Managed Cache Service NuGet package.</span></span>

<span data-ttu-id="12563-194">若要解除安裝受管理的快取服務 NuGet 封裝，請在 [方案總管] 中的用戶端專案上按一下滑鼠右鍵，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="12563-194">To uninstall the Managed Cache Service NuGet package, right-click the client project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> <span data-ttu-id="12563-195">選取 [已安裝的封裝] 節點，然後在 [搜尋已安裝的封裝] 方塊中輸入 **WindowsAzure.Caching**。</span><span class="sxs-lookup"><span data-stu-id="12563-195">Select the **Installed packages** node, and type W**indowsAzure.Caching** into the Search installed packages box.</span></span> <span data-ttu-id="12563-196">選取 [Windows Azure 快取 (Windows Azure Cache)] \(或 [Windows Azure 快取 (Windows Azure Caching)]，視 NuGet 封裝的版本而定)，按一下 [解除安裝]，然後按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="12563-196">Select **Windows** **Azure Cache** (or **Windows** **Azure Caching** depending on the version of the NuGet package), click **Uninstall**, and then click **Close**.</span></span>

![解除安裝 Azure 受管理的快取服務 NuGet 套件](./media/cache-migrate-to-redis/IC757666.jpg)

<span data-ttu-id="12563-198">解除安裝受管理的快取服務 NuGet 封裝，會移除用戶端應用程式的 app.config 或 web.config 中的受管理的快取服務組件和受管理的快取服務項目。</span><span class="sxs-lookup"><span data-stu-id="12563-198">Uninstalling the Managed Cache Service NuGet package removes the Managed Cache Service assemblies and the Managed Cache Service entries in the app.config or web.config of the client application.</span></span> <span data-ttu-id="12563-199">解除安裝 NuGet 封裝時可能不會移除部分自訂的設定，因此請開啟 web.config 或 app.config，確定已徹底移除下列項目。</span><span class="sxs-lookup"><span data-stu-id="12563-199">Because some customized settings may not be removed when uninstalling the NuGet package, open web.config or app.config and ensure that the following elements are completely removed.</span></span>

<span data-ttu-id="12563-200">確定已從 `configSections` 項目移除 `dataCacheClients` 項目。</span><span class="sxs-lookup"><span data-stu-id="12563-200">Ensure that the `dataCacheClients` entry is removed from the `configSections` element.</span></span> <span data-ttu-id="12563-201">請勿移除整個 `configSections` 項目，只需移除 `dataCacheClients` 項目 (若存在)。</span><span class="sxs-lookup"><span data-stu-id="12563-201">Do not remove the entire `configSections` element; just remove the `dataCacheClients` entry, if it is present.</span></span>

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

<span data-ttu-id="12563-202">確定已移除 `dataCacheClients` 區段。</span><span class="sxs-lookup"><span data-stu-id="12563-202">Ensure that the `dataCacheClients` section is removed.</span></span> <span data-ttu-id="12563-203">`dataCacheClients` 區段會類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="12563-203">The `dataCacheClients` section will be similar to the following example.</span></span>

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--To use the in-role flavor of Azure Cache, set identifier to be the cache cluster role name -->
    <!--To use the Azure Managed Cache Service, set identifier to be the endpoint of the cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section to specify security settings for connecting to your cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

<span data-ttu-id="12563-204">一旦移除受管理的快取服務設定，您就可以如下一節所述設定快取用戶端。</span><span class="sxs-lookup"><span data-stu-id="12563-204">Once the Managed Cache Service configuration is removed, you can configure the cache client as described in the following section.</span></span>

### <a name="configure-a-cache-client-using-the-stackexchangeredis-nuget-package"></a><span data-ttu-id="12563-205">設定使用 StackExchange.Redis NuGet 封裝的快取用戶端</span><span class="sxs-lookup"><span data-stu-id="12563-205">Configure a cache client using the StackExchange.Redis NuGet Package</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a><span data-ttu-id="12563-206">移轉受管理的快取服務程式碼</span><span class="sxs-lookup"><span data-stu-id="12563-206">Migrate Managed Cache Service code</span></span>
<span data-ttu-id="12563-207">StackExchange.Redis 快取用戶端的 API 類似受管理的快取服務。</span><span class="sxs-lookup"><span data-stu-id="12563-207">The API for the StackExchange.Redis cache client is similar to the Managed Cache Service.</span></span> <span data-ttu-id="12563-208">本節將概述兩者的差異。</span><span class="sxs-lookup"><span data-stu-id="12563-208">This section provides an overview of the differences.</span></span>

### <a name="connect-to-the-cache-using-the-connectionmultiplexer-class"></a><span data-ttu-id="12563-209">使用 ConnectionMultiplexer 類別連接到快取</span><span class="sxs-lookup"><span data-stu-id="12563-209">Connect to the cache using the ConnectionMultiplexer class</span></span>
<span data-ttu-id="12563-210">在受管理的快取服務中，快取連線是由 `DataCacheFactory` 和 `DataCache` 類別負責處理。</span><span class="sxs-lookup"><span data-stu-id="12563-210">In Managed Cache Service, connections to the cache were handled by the `DataCacheFactory` and `DataCache` classes.</span></span> <span data-ttu-id="12563-211">在 Azure Redis 快取中，這些連接則是由 `ConnectionMultiplexer` 類別進行管理。</span><span class="sxs-lookup"><span data-stu-id="12563-211">In Azure Redis Cache, these connections are managed by the `ConnectionMultiplexer` class.</span></span>

<span data-ttu-id="12563-212">請在您要用來存取快取的檔案頂端加入下列 using 陳述式。</span><span class="sxs-lookup"><span data-stu-id="12563-212">Add the following using statement to the top of any file from which you want to access the cache.</span></span>

```c#
using StackExchange.Redis
```

<span data-ttu-id="12563-213">如果此命名空間並未解析，請確定您已如 [設定快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)中所述加入 StackExchange.Redis NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="12563-213">If this namespace doesn’t resolve, be sure that you have added the StackExchange.Redis NuGet package as described in [Configure the cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>

> [!NOTE]
> <span data-ttu-id="12563-214">請注意，StackExchange.Redis 用戶端需要 .NET Framework 4 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="12563-214">Note that the StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="12563-215">若要連接至 Azure Redis 快取執行個體，請呼叫靜態 `ConnectionMultiplexer.Connect` 方法並傳入端點和金鑰。</span><span class="sxs-lookup"><span data-stu-id="12563-215">To connect to an Azure Redis Cache instance, call the static `ConnectionMultiplexer.Connect` method and pass in the endpoint and key.</span></span> <span data-ttu-id="12563-216">在您的應用程式中共用 `ConnectionMultiplexer` 執行個體的其中一種方法，就是擁有可傳回已連接執行個體的靜態屬性，類似下列範例。</span><span class="sxs-lookup"><span data-stu-id="12563-216">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="12563-217">這會提供安全執行緒方式，只初始化單一已連接的 `ConnectionMultiplexer` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="12563-217">This provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="12563-218">在此範例中， `abortConnect` 已設為 false，這表示即使無法建立與快取的連接，呼叫也會成功。</span><span class="sxs-lookup"><span data-stu-id="12563-218">In this example `abortConnect` is set to false, which means that the call will succeed even if a connection to the cache is not established.</span></span> <span data-ttu-id="12563-219">`ConnectionMultiplexer` 的主要功能之一，就是一旦網路問題或其他原因獲得解決，它就會自動恢復與快取的連接。</span><span class="sxs-lookup"><span data-stu-id="12563-219">One key feature of `ConnectionMultiplexer` is that it will automatically restore connectivity to the cache once the network issue or other causes are resolved.</span></span>

```c#
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
```

<span data-ttu-id="12563-220">快取端點、金鑰和連接埠可自您快取執行個體的 [Redis 快取]  刀鋒視窗取得。</span><span class="sxs-lookup"><span data-stu-id="12563-220">The cache endpoint, keys, and ports can be obtained from the **Redis Cache** blade for your cache instance.</span></span> <span data-ttu-id="12563-221">如需詳細資訊，請參閱 [Redis 快取屬性](cache-configure.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="12563-221">For more information, see [Redis Cache properties](cache-configure.md#properties).</span></span>

<span data-ttu-id="12563-222">一旦建立連接，即會透過呼叫 `ConnectionMultiplexer.GetDatabase` 方法傳回 Redis 快取資料庫的參考。</span><span class="sxs-lookup"><span data-stu-id="12563-222">Once the connection is established, return a reference to the Redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="12563-223">透過 `GetDatabase` 方法傳回的物件是輕量型傳遞物件，而且不需要儲存。</span><span class="sxs-lookup"><span data-stu-id="12563-223">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

<span data-ttu-id="12563-224">StackExchange.Redis 用戶端會使用 `RedisKey` 和 `RedisValue` 型別來對快取存取和儲存項目。</span><span class="sxs-lookup"><span data-stu-id="12563-224">The StackExchange.Redis client uses the `RedisKey` and `RedisValue` types for accessing and storing items in the cache.</span></span> <span data-ttu-id="12563-225">這些型別會對應到最基本的語言型別 (包括字串)，但通常不會直接使用。</span><span class="sxs-lookup"><span data-stu-id="12563-225">These types map onto most primitive language types, including string, and often are not used directly.</span></span> <span data-ttu-id="12563-226">Redis 字串是最基本的一種 Redis 值，可包含許多型別的資料 (包括序列化的二進位資料流)，您可能不會直接使用此型別，但您會使用到名稱中包含 `String` 的方法。</span><span class="sxs-lookup"><span data-stu-id="12563-226">Redis Strings are the most basic kind of Redis value, and can contain many types of data, including serialized binary streams, and while you may not use the type directly, you will use methods that contain `String` in the name.</span></span> <span data-ttu-id="12563-227">對於最基本的資料型別，您會使用 `StringSet` 和 `StringGet` 方法對快取儲存和擷取項目，除非您是要在快取中儲存集合或其他 Redis 資料型別。</span><span class="sxs-lookup"><span data-stu-id="12563-227">For most primitive data types you store and retrieve items from the cache using the `StringSet` and `StringGet` methods, unless you are storing collections or other Redis data types in the cache.</span></span> 

<span data-ttu-id="12563-228">`StringSet` 和 `StringGet` 非常類似受管理的快取服務的 `Put` 和 `Get` 方法，其中最主要的不同點在於，若要設定 .NET 物件並將其放到快取中，您必須先將其序列化。</span><span class="sxs-lookup"><span data-stu-id="12563-228">`StringSet` and `StringGet` are very similar to the Managed Cache Service `Put` and `Get` methods, with one major difference being that before you set and get a .NET object into the cache you must serialize it first.</span></span> 

<span data-ttu-id="12563-229">呼叫 `StringGet` 時，如果物件已存在，即會傳回，如果物件不存在，則會傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="12563-229">When calling `StringGet`, if the object exists, it is returned, and if it does not, null is returned.</span></span> <span data-ttu-id="12563-230">在此情況下，您可以從需要的資料來源中擷取值，並將它儲存在快取中供後續使用。</span><span class="sxs-lookup"><span data-stu-id="12563-230">In this case you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="12563-231">這稱為另行快取模式。</span><span class="sxs-lookup"><span data-stu-id="12563-231">This is known as the cache-aside pattern.</span></span>

<span data-ttu-id="12563-232">若要指定快取中項目的到期時間，請使用 `StringSet` 的 `TimeSpan` 參數。</span><span class="sxs-lookup"><span data-stu-id="12563-232">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

<span data-ttu-id="12563-233">Azure Redis 快取可以使用 .NET 物件及基本資料型別，但必須先將 .NET 物件序列化，才能加以快取。</span><span class="sxs-lookup"><span data-stu-id="12563-233">Azure Redis Cache can work with .NET objects as well as primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="12563-234">這是應用程式開發人員的責任。</span><span class="sxs-lookup"><span data-stu-id="12563-234">This is the responsibility of the application developer.</span></span> <span data-ttu-id="12563-235">這可讓開發人員彈性選擇序列化程式。</span><span class="sxs-lookup"><span data-stu-id="12563-235">This gives the developer flexibility in the choice of the serializer.</span></span> <span data-ttu-id="12563-236">如需詳細資訊和範例程式碼，請參閱 [在快取中使用 .NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。</span><span class="sxs-lookup"><span data-stu-id="12563-236">For more information and sample code, see [Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

## <a name="migrate-aspnet-session-state-and-output-caching-to-azure-redis-cache"></a><span data-ttu-id="12563-237">將 ASP.NET 工作階段狀態和輸出快取移轉至 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="12563-237">Migrate ASP.NET Session State and Output caching to Azure Redis Cache</span></span>
<span data-ttu-id="12563-238">Azure Redis 快取有適用於 ASP.NET 工作階段狀態和頁面輸出快取的提供者。</span><span class="sxs-lookup"><span data-stu-id="12563-238">Azure Redis Cache has providers for both ASP.NET Session State and Page Output caching.</span></span> <span data-ttu-id="12563-239">若要移轉使用這些提供者之受管理的快取服務版本的應用程式，請先從您的 web.config 移除現有的區段，然後設定這些提供者的 Azure Redis 快取版本。</span><span class="sxs-lookup"><span data-stu-id="12563-239">To migrate your application that uses the Managed Cache Service versions of these providers, first remove the existing sections from your web.config, and then configure the Azure Redis Cache versions of the providers.</span></span> <span data-ttu-id="12563-240">如需使用 Azure Redis 快取 ASP.NET 提供者的指示，請參閱 [Azure Redis 快取的 ASP.NET 工作階段狀態供應器](cache-aspnet-session-state-provider.md)和 [Azure Redis 快取的 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="12563-240">For instructions on using the Azure Redis Cache ASP.NET providers, see [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md) and [ASP.NET Output Cache Provider for Azure Redis Cache](cache-aspnet-output-cache-provider.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12563-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12563-241">Next steps</span></span>
<span data-ttu-id="12563-242">瀏覽 [Azure Redis 快取文件](https://azure.microsoft.com/documentation/services/cache/) 中的教學課程、範例、影片及其他資訊。</span><span class="sxs-lookup"><span data-stu-id="12563-242">Explore the [Azure Redis Cache documentation](https://azure.microsoft.com/documentation/services/cache/) for tutorials, samples, videos, and more.</span></span>

