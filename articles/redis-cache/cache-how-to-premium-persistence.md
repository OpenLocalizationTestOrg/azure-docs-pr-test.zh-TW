---
title: "如何設定進階 Azure Redis 快取的資料永續性"
description: "了解如何設定和管理進階層 Azure Redis 快取執行個體的資料永續性"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 638f0154d3a4fd091197a2da86374a053b31c4c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-persistence-for-a-premium-azure-redis-cache"></a><span data-ttu-id="c1306-103">如何設定進階 Azure Redis 快取的資料永續性</span><span class="sxs-lookup"><span data-stu-id="c1306-103">How to configure data persistence for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="c1306-104">Azure Redis 快取有不同的快取供應項目，可讓您彈性選擇快取大小和功能，包括叢集、持續性和虛擬網路支援等進階層功能。</span><span class="sxs-lookup"><span data-stu-id="c1306-104">Azure Redis Cache has different cache offerings which provide flexibility in the choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="c1306-105">本文說明如何在進階 Azure Redis 快取執行個體中設定永續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-105">This article describes how to configure persistence in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="c1306-106">如需其他進階快取功能的相關資訊，請參閱 [Azure Redis 快取進階層簡介](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="c1306-106">For information on other premium cache features, see [Introduction to the Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-data-persistence"></a><span data-ttu-id="c1306-107">資料永續性是什麼？</span><span class="sxs-lookup"><span data-stu-id="c1306-107">What is data persistence?</span></span>
<span data-ttu-id="c1306-108">[Redis 持續性](https://redis.io/topics/persistence)可讓您保存儲存在 Redis 中的資料。</span><span class="sxs-lookup"><span data-stu-id="c1306-108">[Redis persistence](https://redis.io/topics/persistence) allows you to persist data stored in Redis.</span></span> <span data-ttu-id="c1306-109">您也可以擷取快照和備份資料，以在硬體失敗時載入。</span><span class="sxs-lookup"><span data-stu-id="c1306-109">You can also take snapshots and back up the data, which you can load in case of a hardware failure.</span></span> <span data-ttu-id="c1306-110">這是優於基本或標準層的重大優勢，基本或標準層的所有資料是儲存在記憶體中，若發生快取節點故障的失敗，資料可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="c1306-110">This is a huge advantage over Basic or Standard tier where all the data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span></span> 

<span data-ttu-id="c1306-111">Azure Redis 快取使用下列模型提供 Redis 持續性：</span><span class="sxs-lookup"><span data-stu-id="c1306-111">Azure Redis Cache offers Redis persistence using the following models:</span></span>

* <span data-ttu-id="c1306-112">**RDB 持續性** - 設定 RDB (Redis 資料庫) 持續性後，Azure Redis 快取會依據可設定的備份頻率，在磁碟中保存一份 Redis 二進位格式的 Redis 快取快照。</span><span class="sxs-lookup"><span data-stu-id="c1306-112">**RDB persistence** - When RDB (Redis database) persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="c1306-113">如果發生同時停用主要和複本快取的災難性事件，即可使用最新的快照重新建構快取。</span><span class="sxs-lookup"><span data-stu-id="c1306-113">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the most recent snapshot.</span></span> <span data-ttu-id="c1306-114">深入了解 RDB 持續性的[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)。</span><span class="sxs-lookup"><span data-stu-id="c1306-114">Learn more about the [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="c1306-115">**AOF 持續性** - 設定 AOF (僅附加檔案) 持續性後，Azure Redis 快取會將每個寫入作業儲存至記錄，而此記錄則會每秒至少一次儲存至 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1306-115">**AOF persistence** - When AOF (Append only file) persistence is configured, Azure Redis Cache saves every write operation to a log that is saved at least once per second into an Azure Storage account.</span></span> <span data-ttu-id="c1306-116">如果發生同時停用主要和複本快取的災難性事件，即可使用儲存的寫入作業重新建構快取。</span><span class="sxs-lookup"><span data-stu-id="c1306-116">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the stored write operations.</span></span> <span data-ttu-id="c1306-117">深入了解 AOF 持續性的[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)。</span><span class="sxs-lookup"><span data-stu-id="c1306-117">Learn more about the [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="c1306-118">您可以在建立快取期間從 [新的 Redis 快取] 刀鋒視窗設定持續性，也可以在現有進階快取的 [資源] 功能表中設定。</span><span class="sxs-lookup"><span data-stu-id="c1306-118">Persistence is configured from the **New Redis Cache** blade during cache creation and on the **Resource menu** for existing premium caches.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="c1306-119">選取進階定價層後，按一下 [Redis 永續性] 。</span><span class="sxs-lookup"><span data-stu-id="c1306-119">Once a premium pricing tier is selected, click **Redis persistence**.</span></span>

![Redis 永續性][redis-cache-persistence]

<span data-ttu-id="c1306-121">下節的步驟說明如何在您的新進階快取上設定 Redis 持續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-121">The steps in the next section describe how to configure Redis persistence on your new premium cache.</span></span> <span data-ttu-id="c1306-122">Redis 永續性設定後，按一下 [ **建立** ] 以建立具有 Redis 永續性的新進階快取。</span><span class="sxs-lookup"><span data-stu-id="c1306-122">Once Redis persistence is configured, click **Create** to create your new premium cache with Redis persistence.</span></span>

## <a name="enable-redis-persistence"></a><span data-ttu-id="c1306-123">啟用 Redis 持續性</span><span class="sxs-lookup"><span data-stu-id="c1306-123">Enable Redis persistence</span></span>

<span data-ttu-id="c1306-124">您可以在 [Redis 資料持續性] 刀鋒視窗中選擇 [RDB] 或 [AOF] 持續性，來啟用 Redis 持續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-124">Redis persistence is enabled on the **Redis data persistence** blade by choosing either **RDB** or **AOF** persistence.</span></span> <span data-ttu-id="c1306-125">若為新的快取，則在快取建立程序期間存取此刀鋒視窗，如上節所述。</span><span class="sxs-lookup"><span data-stu-id="c1306-125">For new caches, this blade is accessed during the cache creation process, as described in the previous section.</span></span> <span data-ttu-id="c1306-126">若為現有快取，則從快取的 [資源] 功能表存取 [Redis 資料永續性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c1306-126">For existing caches, the **Redis data persistence** blade is accessed from the **Resource menu** for your cache.</span></span>

![Redis 設定][redis-cache-settings]


## <a name="configure-rdb-persistence"></a><span data-ttu-id="c1306-128">設定 RDB 持續性</span><span class="sxs-lookup"><span data-stu-id="c1306-128">Configure RDB persistence</span></span>

<span data-ttu-id="c1306-129">若要啟用 RDB 持續性，請按一下 [RDB]。</span><span class="sxs-lookup"><span data-stu-id="c1306-129">To enable RDB persistence, click **RDB**.</span></span> <span data-ttu-id="c1306-130">若要停用先前所啟用進階快取的 RDB 持續性，請按一下 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="c1306-130">To disable RDB persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis RDB 持續性][redis-cache-rdb-persistence]

<span data-ttu-id="c1306-132">若要設定備份間隔，請選取下拉式清單中的 [ **備份頻率** ]。</span><span class="sxs-lookup"><span data-stu-id="c1306-132">To configure the backup interval, select a **Backup Frequency** from the drop-down list.</span></span> <span data-ttu-id="c1306-133">選項包括 [15 分鐘]、[30 分鐘]、[60 分鐘]、[6 小時]、[12 小時] 及 [24 小時]。</span><span class="sxs-lookup"><span data-stu-id="c1306-133">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span></span> <span data-ttu-id="c1306-134">在先前的備份作業成功完成後，此間隔便會開始倒數計時，時間過後就會起始新的備份。</span><span class="sxs-lookup"><span data-stu-id="c1306-134">This interval starts counting down after the previous backup operation successfully completes and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="c1306-135">按一下 [儲存體帳戶] 選取要使用的儲存體帳戶，然後從 [儲存體金鑰] 下拉式清單中選擇 [主要金鑰] 或 [次要金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c1306-135">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> <span data-ttu-id="c1306-136">您必須選擇與快取相同區域的儲存體帳戶，建議選取 [進階儲存體]  帳戶，因為進儲存體的輸送量較高。</span><span class="sxs-lookup"><span data-stu-id="c1306-136">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c1306-137">如果重新產生了永續性帳戶的儲存體金鑰，您必須從 [儲存體金鑰] 下拉式清單中重新設定所需的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c1306-137">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="c1306-138">按一下 [確定]  以儲存持續性組態。</span><span class="sxs-lookup"><span data-stu-id="c1306-138">Click **OK** to save the persistence configuration.</span></span>

<span data-ttu-id="c1306-139">備份頻率間隔過後，會啟動下一個備份 (或新快取的第一個備份)。</span><span class="sxs-lookup"><span data-stu-id="c1306-139">The next backup (or first backup for new caches) is initiated once the backup frequency interval elapses.</span></span>

## <a name="configure-aof-persistence"></a><span data-ttu-id="c1306-140">設定 AOF 持續性</span><span class="sxs-lookup"><span data-stu-id="c1306-140">Configure AOF persistence</span></span>

<span data-ttu-id="c1306-141">若要啟用 AOF 持續性，請按一下 [AOF]。</span><span class="sxs-lookup"><span data-stu-id="c1306-141">To enable AOF persistence, click **AOF**.</span></span> <span data-ttu-id="c1306-142">若要停用先前所啟用進階快取的 AOF 持續性，請按一下 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="c1306-142">To disable AOF persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis AOF 持續性][redis-cache-aof-persistence]

<span data-ttu-id="c1306-144">若要設定 AOF 持續性，請指定 [第一個儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c1306-144">To configure AOF persistence, specify a **First Storage Account**.</span></span> <span data-ttu-id="c1306-145">此儲存體帳戶必須與快取位於相同區域，建議選取 [進階儲存體] 帳戶，因為進階儲存體的輸送量較高。</span><span class="sxs-lookup"><span data-stu-id="c1306-145">This storage account must be in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> <span data-ttu-id="c1306-146">您可以選擇性地設定額外的儲存體帳戶，並指定為 [第二個儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="c1306-146">You can optionally configure an additional storage account named **Second Storage Account**.</span></span> <span data-ttu-id="c1306-147">如果設定第二個儲存體帳戶，複本快取的寫入內容會寫入至此第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1306-147">If a second storage account is configured, the writes to the replica cache are written to this second storage account.</span></span> <span data-ttu-id="c1306-148">針對所設定的每個儲存體帳戶，請選擇要從 [儲存體金鑰] 下拉式清單中使用 [主要金鑰] 或 [次要金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c1306-148">For each configured storage account, choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c1306-149">如果重新產生了永續性帳戶的儲存體金鑰，您必須從 [儲存體金鑰] 下拉式清單中重新設定所需的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c1306-149">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="c1306-150">啟用 AOF 持續性時，快取的寫入作業會儲存至指定的儲存體帳戶 (或設定為第二個儲存體帳戶的帳戶)。</span><span class="sxs-lookup"><span data-stu-id="c1306-150">When AOF persistence is enabled, write operations to the cache are saved to the designated storage account (or accounts if you have configured a second storage account).</span></span> <span data-ttu-id="c1306-151">如果發生使主要和複本快取離線的災難性失敗，則會使用儲存的 AOF 記錄來重建快取。</span><span class="sxs-lookup"><span data-stu-id="c1306-151">In the event of a catastrophic failure that takes down both the primary and replica cache, the stored AOF log is used to rebuild the cache.</span></span>

## <a name="persistence-faq"></a><span data-ttu-id="c1306-152">永續性常見問題集</span><span class="sxs-lookup"><span data-stu-id="c1306-152">Persistence FAQ</span></span>
<span data-ttu-id="c1306-153">下列清單包含 Azure Redis 快取永續性常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="c1306-153">The following list contains answers to commonly asked questions about Azure Redis Cache persistence.</span></span>

* [<span data-ttu-id="c1306-154">可以對先前建立的快取啟用永續性嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-154">Can I enable persistence on a previously created cache?</span></span>](#can-i-enable-persistence-on-a-previously-created-cache)
* [<span data-ttu-id="c1306-155">我可以同時啟用 AOF 和 RDB 持續性嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-155">Can I enable AOF and RDB persistence at the same time?</span></span>](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [<span data-ttu-id="c1306-156">我應該選擇哪一種持續性模型？</span><span class="sxs-lookup"><span data-stu-id="c1306-156">Which persistence model should I choose?</span></span>](#which-persistence-model-should-i-choose)
* [<span data-ttu-id="c1306-157">如果我調整為不同大小，並還原為調整作業之前製作的備份時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-157">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a><span data-ttu-id="c1306-158">RDB 持續性</span><span class="sxs-lookup"><span data-stu-id="c1306-158">RDB persistence</span></span>
* [<span data-ttu-id="c1306-159">在建立快取之後，可以變更 RDB 備份頻率嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-159">Can I change the RDB backup frequency after I create the cache?</span></span>](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [<span data-ttu-id="c1306-160">為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？</span><span class="sxs-lookup"><span data-stu-id="c1306-160">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [<span data-ttu-id="c1306-161">建立新的備份時，舊的 RDB 備份會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-161">What happens to the old RDB backups when a new backup is made?</span></span>](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a><span data-ttu-id="c1306-162">AOF 持續性</span><span class="sxs-lookup"><span data-stu-id="c1306-162">AOF persistence</span></span>
* [<span data-ttu-id="c1306-163">何時應該使用第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="c1306-163">When should I use a second storage account?</span></span>](#when-should-i-use-a-second-storage-account)
* [<span data-ttu-id="c1306-164">AOF 持續性是否會影響快取的輸送量、延遲或效能？</span><span class="sxs-lookup"><span data-stu-id="c1306-164">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [<span data-ttu-id="c1306-165">我要如何移除第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="c1306-165">How can I remove the second storage account?</span></span>](#how-can-i-remove-the-second-storage-account)
* [<span data-ttu-id="c1306-166">什麼是重寫，其對快取有何影響？</span><span class="sxs-lookup"><span data-stu-id="c1306-166">What is a rewrite and how does it affect my cache?</span></span>](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [<span data-ttu-id="c1306-167">在啟用 AOF 下調整快取預期會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-167">What should I expect when scaling a cache with AOF enabled?</span></span>](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [<span data-ttu-id="c1306-168">我的 AOF 資料在儲存體中的組織方式為何？</span><span class="sxs-lookup"><span data-stu-id="c1306-168">How is my AOF data organized in storage?</span></span>](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a><span data-ttu-id="c1306-169">可以對先前建立的快取啟用永續性嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-169">Can I enable persistence on a previously created cache?</span></span>
<span data-ttu-id="c1306-170">可以，可在建立快取時以及現有進階快取中設定 Redis 永續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-170">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span></span>

### <a name="can-i-enable-aof-and-rdb-persistence-at-the-same-time"></a><span data-ttu-id="c1306-171">我可以同時啟用 AOF 和 RDB 持續性嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-171">Can I enable AOF and RDB persistence at the same time?</span></span>

<span data-ttu-id="c1306-172">不可以，您只能啟用 RDB 或 AOF，但不能同時啟用。</span><span class="sxs-lookup"><span data-stu-id="c1306-172">No, you can enable only RDB or AOF, but not both at the same time.</span></span>

### <a name="which-persistence-model-should-i-choose"></a><span data-ttu-id="c1306-173">我應該選擇哪一種持續性模型？</span><span class="sxs-lookup"><span data-stu-id="c1306-173">Which persistence model should I choose?</span></span>

<span data-ttu-id="c1306-174">AOF 持續性將每筆寫入內容儲存至記錄，因此會對輸送量造成一些影響；相較之下，RDB 持續性根據所設定的備份間隔儲存備份，因此對效能的影響很低。</span><span class="sxs-lookup"><span data-stu-id="c1306-174">AOF persistence saves every write to a log, which has some impact on throughput, compared with RDB persistence which saves backups based on the configured backup interval, with minimal impact on performance.</span></span> <span data-ttu-id="c1306-175">如果您的主要目標在於減少資料遺失，而且您可以處理快取輸送量降低的情況，請選擇 AOF 持續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-175">Choose AOF persistence if your primary goal is to minimize data loss, and you can handle a decrease in throughput for your cache.</span></span> <span data-ttu-id="c1306-176">如果您想要維持快取的最佳輸送量，但仍需要資料復原的機制，請選擇 RDB 持續性。</span><span class="sxs-lookup"><span data-stu-id="c1306-176">Choose RDB persistence if you wish to maintain optimal throughput on your cache, but still want a mechanism for data recovery.</span></span>

* <span data-ttu-id="c1306-177">深入了解 RDB 持續性的[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)。</span><span class="sxs-lookup"><span data-stu-id="c1306-177">Learn more about the [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="c1306-178">深入了解 AOF 持續性的[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)。</span><span class="sxs-lookup"><span data-stu-id="c1306-178">Learn more about the [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="c1306-179">如需使用 AOF 持續性時之效能的詳細資訊，請參閱 [AOF 持續性是否會影響快取的輸送量、延遲或效能？](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span><span class="sxs-lookup"><span data-stu-id="c1306-179">For more information on performance when using AOF persistence, see [Does AOF persistence affect throughout, latency, or performance of my cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span></span>

### <a name="what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation"></a><span data-ttu-id="c1306-180">如果我調整為不同大小，並還原為調整作業之前製作的備份時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-180">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>

<span data-ttu-id="c1306-181">針對 RDB 和 AOF 持續性：</span><span class="sxs-lookup"><span data-stu-id="c1306-181">For both RDB and AOF persistence:</span></span>

* <span data-ttu-id="c1306-182">如果您已調整為較大的大小則沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="c1306-182">If you have scaled to a larger size, there is no impact.</span></span>
* <span data-ttu-id="c1306-183">如果已調整為較小的大小，而且您的自訂[資料庫](cache-configure.md#databases)設定大於新大小的[資料庫限制](cache-configure.md#databases)，則不會還原這些資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="c1306-183">If you have scaled to a smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than the [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't restored.</span></span> <span data-ttu-id="c1306-184">如需詳細資訊，請參閱[我的自訂資料庫設定在調整期間會受到影響嗎？](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span><span class="sxs-lookup"><span data-stu-id="c1306-184">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span></span>
* <span data-ttu-id="c1306-185">如果已調整為較小的大小，而且較小的大小中沒有足夠的空間可保存來自最近備份的所有資料，將會在還原程序中收回金鑰，通常是使用 [allkeys-lru](http://redis.io/topics/lru-cache) 收回原則。</span><span class="sxs-lookup"><span data-stu-id="c1306-185">If you have scaled to a smaller size, and there isn't enough room in the smaller size to hold all of the data from the last backup, keys will be evicted during the restore process, typically using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span>

### <a name="can-i-change-the-rdb-backup-frequency-after-i-create-the-cache"></a><span data-ttu-id="c1306-186">在建立快取之後，可以變更 RDB 備份頻率嗎？</span><span class="sxs-lookup"><span data-stu-id="c1306-186">Can I change the RDB backup frequency after I create the cache?</span></span>
<span data-ttu-id="c1306-187">可以，您可以在 [Redis 資料持續性] 刀鋒視窗上變更 RDB 持續性的備份頻率。</span><span class="sxs-lookup"><span data-stu-id="c1306-187">Yes, you can change the backup frequency for RDB persistence on the **Redis data persistence** blade.</span></span> <span data-ttu-id="c1306-188">如需相關指示，請參閱 [設定 Redis 永續性](#configure-redis-persistence)。</span><span class="sxs-lookup"><span data-stu-id="c1306-188">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span></span>

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a><span data-ttu-id="c1306-189">為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？</span><span class="sxs-lookup"><span data-stu-id="c1306-189">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>
<span data-ttu-id="c1306-190">在前一個備份程序順利完成後，RDB 持續性備份頻率間隔才會開始計算。</span><span class="sxs-lookup"><span data-stu-id="c1306-190">The RDB persistence backup frequency interval does not start until the previous backup process has completed successfully.</span></span> <span data-ttu-id="c1306-191">如果備份頻率是 60 分鐘，而備份程序要 15 分鐘才能順利完成，則下一次備份要在先前的備份開始的 75 分鐘後才會開始。</span><span class="sxs-lookup"><span data-stu-id="c1306-191">If the backup frequency is 60 minutes and it takes a backup process 15 minutes to successfully complete, the next backup won't start until 75 minutes after the start time of the previous backup.</span></span>

### <a name="what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made"></a><span data-ttu-id="c1306-192">建立新的備份時，舊的 RDB 備份會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-192">What happens to the old RDB backups when a new backup is made?</span></span>
<span data-ttu-id="c1306-193">除了最新的備份外，所有 RDB 持續性備份都會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="c1306-193">All RDB persistence backups except for the most recent one are automatically deleted.</span></span> <span data-ttu-id="c1306-194">這項刪除作業可能不會立即發生，但較舊的備份不會無限期保存。</span><span class="sxs-lookup"><span data-stu-id="c1306-194">This deletion may not happen immediately but older backups are not persisted indefinitely.</span></span>


### <a name="when-should-i-use-a-second-storage-account"></a><span data-ttu-id="c1306-195">何時應該使用第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="c1306-195">When should I use a second storage account?</span></span>

<span data-ttu-id="c1306-196">當您認為快取上有比預期更高的設定作業時，您應該針對 AOF 持續性使用第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1306-196">You should use a second storage account for AOF persistence when you believe you have higher than expected set operations on the cache.</span></span>  <span data-ttu-id="c1306-197">設定第二個儲存體帳戶有助於確保您的快取不會達到儲存體頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="c1306-197">Setting up the secondary storage account helps ensure your cache doesn't reach storage bandwidth limits.</span></span>

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a><span data-ttu-id="c1306-198">AOF 持續性是否會影響快取的輸送量、延遲或效能？</span><span class="sxs-lookup"><span data-stu-id="c1306-198">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>

<span data-ttu-id="c1306-199">當快取低於最大負載 (CPU 和伺服器負載皆低於 90%) 時，AOF 持續性會影響輸送量約 15%-20%。</span><span class="sxs-lookup"><span data-stu-id="c1306-199">AOF persistence affects throughput by about 15% – 20% when the cache is below maximum load (CPU and Server Load both under 90%).</span></span> <span data-ttu-id="c1306-200">當快取在這些限制範圍內時，不應該有延遲問題。</span><span class="sxs-lookup"><span data-stu-id="c1306-200">There should not be latency issues when the cache is within these limits.</span></span> <span data-ttu-id="c1306-201">不過，啟用 AOF 時，快取會更快達到這些限制。</span><span class="sxs-lookup"><span data-stu-id="c1306-201">However, the cache will reach these limits sooner with AOF enabled.</span></span>

### <a name="how-can-i-remove-the-second-storage-account"></a><span data-ttu-id="c1306-202">我要如何移除第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="c1306-202">How can I remove the second storage account?</span></span>

<span data-ttu-id="c1306-203">您可以透過將 AOF 持續性的第二個儲存體帳戶設定為與第一個儲存體帳戶相同，來移除第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1306-203">You can remove the AOF persistence secondary storage account by setting the second storage account to be the same as the first storage account.</span></span> <span data-ttu-id="c1306-204">如需相關指示，請參閱[設定 AOF 持續性](#configure-aof-persistence)。</span><span class="sxs-lookup"><span data-stu-id="c1306-204">For instructions, see [Configure AOF persistence](#configure-aof-persistence).</span></span>

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a><span data-ttu-id="c1306-205">什麼是重寫，其對快取有何影響？</span><span class="sxs-lookup"><span data-stu-id="c1306-205">What is a rewrite and how does it affect my cache?</span></span>

<span data-ttu-id="c1306-206">當 AOF 檔案變得夠大時，系統會自動將重寫作業排入快取佇列。</span><span class="sxs-lookup"><span data-stu-id="c1306-206">When the AOF file becomes large enough, a rewrite is automatically queued on the cache.</span></span> <span data-ttu-id="c1306-207">重寫作業會調整 AOF 檔案大小，只包含建立目前資料集所需的一組基本作業。</span><span class="sxs-lookup"><span data-stu-id="c1306-207">The rewrite resizes the AOF file with the minimal set of operations needed to create the current data set.</span></span> <span data-ttu-id="c1306-208">在重寫期間，預期會更快達到效能限制，特別是在處理大型資料集時。</span><span class="sxs-lookup"><span data-stu-id="c1306-208">During rewrites, expect to reach performance limits sooner especially when dealing with large datasets.</span></span> <span data-ttu-id="c1306-209">隨著 AOF 檔案愈來愈大，重寫的發生頻率會減少，但發生時將需要大量時間。</span><span class="sxs-lookup"><span data-stu-id="c1306-209">Rewrites occur less often as the AOF file becomes larger, but will take a significant amount of time when it happens.</span></span>

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a><span data-ttu-id="c1306-210">在啟用 AOF 下調整快取預期會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c1306-210">What should I expect when scaling a cache with AOF enabled?</span></span>

<span data-ttu-id="c1306-211">如果 AOF 檔案在調整時相當大，調整作業所花的時間會超出預期，因為在調整完成之後會重新載入檔案。</span><span class="sxs-lookup"><span data-stu-id="c1306-211">If the AOF file at the time of scaling is significantly large, then expect the scale operation to take longer than expected since it will be reloading the file after scaling has finished.</span></span>

<span data-ttu-id="c1306-212">如需調整的詳細資訊，請參閱[如果我調整為不同大小，並還原為調整作業之前製作的備份時，會發生什麼事？](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span><span class="sxs-lookup"><span data-stu-id="c1306-212">For more information on scaling, see [What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span></span>

### <a name="how-is-my-aof-data-organized-in-storage"></a><span data-ttu-id="c1306-213">我的 AOF 資料在儲存體中的組織方式為何？</span><span class="sxs-lookup"><span data-stu-id="c1306-213">How is my AOF data organized in storage?</span></span>

<span data-ttu-id="c1306-214">儲存在 AOF 檔案中的資料會根據節點分成多個分頁 Blob，以提升將資料儲存至儲存體的效能。</span><span class="sxs-lookup"><span data-stu-id="c1306-214">Data stored in AOF files is divided into multiple page blobs per node to increase performance of saving the data to storage.</span></span> <span data-ttu-id="c1306-215">下表顯示針對每個定價層所使用的分頁 Blob 數量：</span><span class="sxs-lookup"><span data-stu-id="c1306-215">The following table displays how many page blobs are used for each pricing tier:</span></span>

| <span data-ttu-id="c1306-216">高階層</span><span class="sxs-lookup"><span data-stu-id="c1306-216">Premium tier</span></span> | <span data-ttu-id="c1306-217">Blob</span><span class="sxs-lookup"><span data-stu-id="c1306-217">Blobs</span></span> |
|--------------|-------|
| <span data-ttu-id="c1306-218">P1</span><span class="sxs-lookup"><span data-stu-id="c1306-218">P1</span></span>           | <span data-ttu-id="c1306-219">每個分區 4 個</span><span class="sxs-lookup"><span data-stu-id="c1306-219">4 per shard</span></span>    |
| <span data-ttu-id="c1306-220">P2</span><span class="sxs-lookup"><span data-stu-id="c1306-220">P2</span></span>           | <span data-ttu-id="c1306-221">每個分區 8 個</span><span class="sxs-lookup"><span data-stu-id="c1306-221">8 per shard</span></span>    |
| <span data-ttu-id="c1306-222">P3</span><span class="sxs-lookup"><span data-stu-id="c1306-222">P3</span></span>           | <span data-ttu-id="c1306-223">每個分區 16 個</span><span class="sxs-lookup"><span data-stu-id="c1306-223">16 per shard</span></span>   |
| <span data-ttu-id="c1306-224">P4</span><span class="sxs-lookup"><span data-stu-id="c1306-224">P4</span></span>           | <span data-ttu-id="c1306-225">每個分區 20 個</span><span class="sxs-lookup"><span data-stu-id="c1306-225">20 per shard</span></span>   |

<span data-ttu-id="c1306-226">啟用叢集時，快取中的每個分區會有一組專屬的分頁 Blob，如上表所示。</span><span class="sxs-lookup"><span data-stu-id="c1306-226">When clustering is enabled, each shard in the cache has its own set of page blobs, as indicated in the previous table.</span></span> <span data-ttu-id="c1306-227">例如，具有三個分區的 P2 快取會將其 AOF 檔案散發到 24 個分頁 Blob (3 個分區，所以每個分區 8 個 Blob)。</span><span class="sxs-lookup"><span data-stu-id="c1306-227">For example, a P2 cache with three shards distributes its AOF file across 24 page blobs (8 blobs per shard, with 3 shards).</span></span>

<span data-ttu-id="c1306-228">重寫後，儲存體中會有兩組 AOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="c1306-228">After a rewrite, two sets of AOF files exist in storage.</span></span> <span data-ttu-id="c1306-229">重寫會在背景進行並將內容附加至第一組檔案，而當重寫內容附加至第二組檔案期間，會將設定作業傳送至快取。</span><span class="sxs-lookup"><span data-stu-id="c1306-229">Rewrites occur in the background and append to the first set of files, while set operations that are sent to the cache during the rewrite append to the second set.</span></span> <span data-ttu-id="c1306-230">重寫期間會暫時儲存備份以備失敗之需，但在重寫完成之後則會立即刪除備份。</span><span class="sxs-lookup"><span data-stu-id="c1306-230">A backup is temporarily stored during rewrites in case of failure, but is promptly deleted after a rewrite finishes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1306-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1306-231">Next steps</span></span>
<span data-ttu-id="c1306-232">了解如何使用更多進階快取功能。</span><span class="sxs-lookup"><span data-stu-id="c1306-232">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="c1306-233">Azure Redis Cache 高階層簡介</span><span class="sxs-lookup"><span data-stu-id="c1306-233">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
