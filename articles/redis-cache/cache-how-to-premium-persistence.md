---
title: "高階 Azure Redis 快取的 aaaHow tooconfigure 資料持續性"
description: "深入了解如何 tooconfigure 和管理資料持續性 Premium 層 Azure Redis 快取執行個體"
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
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a><span data-ttu-id="65098-103">如何 tooconfigure Premium Azure Redis 快取的資料持續性</span><span class="sxs-lookup"><span data-stu-id="65098-103">How tooconfigure data persistence for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="65098-104">Azure Redis 快取都有提供有彈性地 hello 選擇的快取大小和功能，包括 Premium 層功能，例如叢集、 持續性和虛擬網路支援不同的快取提供項目。</span><span class="sxs-lookup"><span data-stu-id="65098-104">Azure Redis Cache has different cache offerings which provide flexibility in hello choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="65098-105">本文說明如何在 premium tooconfigure 持續性 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="65098-105">This article describes how tooconfigure persistence in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="65098-106">如需其他進階快取功能的資訊，請參閱[簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="65098-106">For information on other premium cache features, see [Introduction toohello Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-data-persistence"></a><span data-ttu-id="65098-107">資料永續性是什麼？</span><span class="sxs-lookup"><span data-stu-id="65098-107">What is data persistence?</span></span>
<span data-ttu-id="65098-108">[Redis 持續性](https://redis.io/topics/persistence)可讓您儲存於 Redis toopersist 資料。</span><span class="sxs-lookup"><span data-stu-id="65098-108">[Redis persistence](https://redis.io/topics/persistence) allows you toopersist data stored in Redis.</span></span> <span data-ttu-id="65098-109">您也可以取得快照集及備份 hello 資料，您可以載入如果發生硬體故障。</span><span class="sxs-lookup"><span data-stu-id="65098-109">You can also take snapshots and back up hello data, which you can load in case of a hardware failure.</span></span> <span data-ttu-id="65098-110">這是龐大的優勢，透過基本或標準層，其中所有 hello 資料儲存在記憶體中，而且可以有其中快取節點為關閉故障的潛在資料遺失。</span><span class="sxs-lookup"><span data-stu-id="65098-110">This is a huge advantage over Basic or Standard tier where all hello data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span></span> 

<span data-ttu-id="65098-111">Azure Redis 快取提供 Redis 持續性，使用下列模型 hello:</span><span class="sxs-lookup"><span data-stu-id="65098-111">Azure Redis Cache offers Redis persistence using hello following models:</span></span>

* <span data-ttu-id="65098-112">**RDB 持續性**-設定當 RDB （Redis 資料庫） 的持續性，Azure Redis 快取保存於二進位格式 toodisk 根據可設定的備份頻率 Redis hello Redis 快取的快照集。</span><span class="sxs-lookup"><span data-stu-id="65098-112">**RDB persistence** - When RDB (Redis database) persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="65098-113">發生重大事件，會停用 hello 主要和複本快取，hello 快取重新建構使用 hello 最新的快照集。</span><span class="sxs-lookup"><span data-stu-id="65098-113">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache is reconstructed using hello most recent snapshot.</span></span> <span data-ttu-id="65098-114">深入了解 hello[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)RDB 持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-114">Learn more about hello [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="65098-115">**很少持續性**-設定時很少 （附加唯一的檔案） 的持續性，Azure Redis 快取會儲存在至少一次秒到 Azure 儲存體帳戶會儲存每個寫入作業 tooa 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65098-115">**AOF persistence** - When AOF (Append only file) persistence is configured, Azure Redis Cache saves every write operation tooa log that is saved at least once per second into an Azure Storage account.</span></span> <span data-ttu-id="65098-116">發生重大事件，會停用 hello 主要和複本快取，hello 快取重新建構使用 hello 儲存寫入作業。</span><span class="sxs-lookup"><span data-stu-id="65098-116">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache is reconstructed using hello stored write operations.</span></span> <span data-ttu-id="65098-117">深入了解 hello[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)很少持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-117">Learn more about hello [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="65098-118">持續性會設定 hello**新增 Redis 快取**刀鋒視窗中的快取建立期間和 hello**資源功能表**現有進階版快取。</span><span class="sxs-lookup"><span data-stu-id="65098-118">Persistence is configured from hello **New Redis Cache** blade during cache creation and on hello **Resource menu** for existing premium caches.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="65098-119">選取進階定價層後，按一下 [Redis 永續性] 。</span><span class="sxs-lookup"><span data-stu-id="65098-119">Once a premium pricing tier is selected, click **Redis persistence**.</span></span>

![Redis 永續性][redis-cache-persistence]

<span data-ttu-id="65098-121">hello hello 下一節中的步驟說明如何 tooconfigure Redis 上新的高階快取的持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-121">hello steps in hello next section describe how tooconfigure Redis persistence on your new premium cache.</span></span> <span data-ttu-id="65098-122">一旦設定 Redis 持續性之後，按一下**建立**toocreate 您新 premium 快取，Redis 持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-122">Once Redis persistence is configured, click **Create** toocreate your new premium cache with Redis persistence.</span></span>

## <a name="enable-redis-persistence"></a><span data-ttu-id="65098-123">啟用 Redis 持續性</span><span class="sxs-lookup"><span data-stu-id="65098-123">Enable Redis persistence</span></span>

<span data-ttu-id="65098-124">Redis 在 hello 上已啟用持續性**Redis 資料持續性**刀鋒視窗中的選擇  **RDB**或**很少**持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-124">Redis persistence is enabled on hello **Redis data persistence** blade by choosing either **RDB** or **AOF** persistence.</span></span> <span data-ttu-id="65098-125">新的快取，此刀鋒視窗存取 hello 快取建立程序期間 hello 上一節中所述。</span><span class="sxs-lookup"><span data-stu-id="65098-125">For new caches, this blade is accessed during hello cache creation process, as described in hello previous section.</span></span> <span data-ttu-id="65098-126">現有的快取，hello **Redis 資料持續性**刀鋒視窗存取從 hello**資源功能表**快取。</span><span class="sxs-lookup"><span data-stu-id="65098-126">For existing caches, hello **Redis data persistence** blade is accessed from hello **Resource menu** for your cache.</span></span>

![Redis 設定][redis-cache-settings]


## <a name="configure-rdb-persistence"></a><span data-ttu-id="65098-128">設定 RDB 持續性</span><span class="sxs-lookup"><span data-stu-id="65098-128">Configure RDB persistence</span></span>

<span data-ttu-id="65098-129">tooenable RDB 持續性，按一下  **RDB**。</span><span class="sxs-lookup"><span data-stu-id="65098-129">tooenable RDB persistence, click **RDB**.</span></span> <span data-ttu-id="65098-130">toodisable RDB 持續性上先前已啟用進階版快取中，按一下**已停用**。</span><span class="sxs-lookup"><span data-stu-id="65098-130">toodisable RDB persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis RDB 持續性][redis-cache-rdb-persistence]

<span data-ttu-id="65098-132">tooconfigure hello 備份間隔，選取**備份頻率**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="65098-132">tooconfigure hello backup interval, select a **Backup Frequency** from hello drop-down list.</span></span> <span data-ttu-id="65098-133">選項包括 [15 分鐘]、[30 分鐘]、[60 分鐘]、[6 小時]、[12 小時] 及 [24 小時]。</span><span class="sxs-lookup"><span data-stu-id="65098-133">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span></span> <span data-ttu-id="65098-134">在此時間間隔開始 hello 先前的備份作業成功完成，並在它耗盡時起始新的備份之後，向下計數。</span><span class="sxs-lookup"><span data-stu-id="65098-134">This interval starts counting down after hello previous backup operation successfully completes and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="65098-135">按一下**儲存體帳戶**tooselect hello 儲存體帳戶 toouse，並選擇其中一個 hello**主索引鍵**或**次要金鑰**從 hello toouse**儲存體索引鍵**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="65098-135">Click **Storage Account** tooselect hello storage account toouse, and choose either hello **Primary key** or **Secondary key** toouse from hello **Storage Key** drop-down.</span></span> <span data-ttu-id="65098-136">您必須選擇儲存體帳戶中 hello 與 hello 快取中，相同的區域和**高階儲存體**因為進階儲存體具有較高的輸送量，建議使用帳戶。</span><span class="sxs-lookup"><span data-stu-id="65098-136">You must choose a storage account in hello same region as hello cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="65098-137">如果重新產生您的持續性帳戶 hello 儲存體金鑰時，您必須重新設定從 hello hello 所需的索引鍵**儲存體金鑰**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="65098-137">If hello storage key for your persistence account is regenerated, you must reconfigure hello desired key from hello **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="65098-138">按一下**確定**toosave hello 持續性組態。</span><span class="sxs-lookup"><span data-stu-id="65098-138">Click **OK** toosave hello persistence configuration.</span></span>

<span data-ttu-id="65098-139">一旦 hello 備份頻率間隔耗盡起始 hello 下一個備份 （或新的快取的第一次備份）。</span><span class="sxs-lookup"><span data-stu-id="65098-139">hello next backup (or first backup for new caches) is initiated once hello backup frequency interval elapses.</span></span>

## <a name="configure-aof-persistence"></a><span data-ttu-id="65098-140">設定 AOF 持續性</span><span class="sxs-lookup"><span data-stu-id="65098-140">Configure AOF persistence</span></span>

<span data-ttu-id="65098-141">tooenable 很少持續性，按一下 **很少**。</span><span class="sxs-lookup"><span data-stu-id="65098-141">tooenable AOF persistence, click **AOF**.</span></span> <span data-ttu-id="65098-142">toodisable 很少持續性上先前已啟用進階版快取中，按一下**已停用**。</span><span class="sxs-lookup"><span data-stu-id="65098-142">toodisable AOF persistence on a previously enabled premium cache, click **Disabled**.</span></span>

![Redis AOF 持續性][redis-cache-aof-persistence]

<span data-ttu-id="65098-144">tooconfigure 很少持續性，指定**第一個儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="65098-144">tooconfigure AOF persistence, specify a **First Storage Account**.</span></span> <span data-ttu-id="65098-145">這個儲存體帳戶必須在 hello 與 hello 快取中，相同的區域和**高階儲存體**因為進階儲存體具有較高的輸送量，建議使用帳戶。</span><span class="sxs-lookup"><span data-stu-id="65098-145">This storage account must be in hello same region as hello cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> <span data-ttu-id="65098-146">您可以選擇性地設定額外的儲存體帳戶，並指定為 [第二個儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="65098-146">You can optionally configure an additional storage account named **Second Storage Account**.</span></span> <span data-ttu-id="65098-147">如果第二個儲存體帳戶設定，hello 寫入 toohello 複本快取寫入 toothis 第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65098-147">If a second storage account is configured, hello writes toohello replica cache are written toothis second storage account.</span></span> <span data-ttu-id="65098-148">針對每個設定的儲存體帳戶中，選擇其中一個 hello**主索引鍵**或**次要金鑰**從 hello toouse**儲存體金鑰**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="65098-148">For each configured storage account, choose either hello **Primary key** or **Secondary key** toouse from hello **Storage Key** drop-down.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="65098-149">如果重新產生您的持續性帳戶 hello 儲存體金鑰時，您必須重新設定從 hello hello 所需的索引鍵**儲存體金鑰**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="65098-149">If hello storage key for your persistence account is regenerated, you must reconfigure hello desired key from hello **Storage Key** drop-down.</span></span>
> 
> 

<span data-ttu-id="65098-150">啟用很少持續性時，寫入作業 toohello 快取會儲存 toohello 指定儲存體帳戶 （或如果您已設定的第二個儲存體帳戶的帳戶）。</span><span class="sxs-lookup"><span data-stu-id="65098-150">When AOF persistence is enabled, write operations toohello cache are saved toohello designated storage account (or accounts if you have configured a second storage account).</span></span> <span data-ttu-id="65098-151">Hello 重大錯誤事件中，會同時向 hello 主要複本快取，hello 預存很少記錄會使用和 toorebuild hello 快取。</span><span class="sxs-lookup"><span data-stu-id="65098-151">In hello event of a catastrophic failure that takes down both hello primary and replica cache, hello stored AOF log is used toorebuild hello cache.</span></span>

## <a name="persistence-faq"></a><span data-ttu-id="65098-152">永續性常見問題集</span><span class="sxs-lookup"><span data-stu-id="65098-152">Persistence FAQ</span></span>
<span data-ttu-id="65098-153">hello 下列清單包含 Azure Redis 快取持續性相關常見問題的解答 toocommonly。</span><span class="sxs-lookup"><span data-stu-id="65098-153">hello following list contains answers toocommonly asked questions about Azure Redis Cache persistence.</span></span>

* [<span data-ttu-id="65098-154">可以對先前建立的快取啟用永續性嗎？</span><span class="sxs-lookup"><span data-stu-id="65098-154">Can I enable persistence on a previously created cache?</span></span>](#can-i-enable-persistence-on-a-previously-created-cache)
* [<span data-ttu-id="65098-155">啟用在 hello 很少和 RDB 持續性相同的時間？</span><span class="sxs-lookup"><span data-stu-id="65098-155">Can I enable AOF and RDB persistence at hello same time?</span></span>](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [<span data-ttu-id="65098-156">我應該選擇哪一種持續性模型？</span><span class="sxs-lookup"><span data-stu-id="65098-156">Which persistence model should I choose?</span></span>](#which-persistence-model-should-i-choose)
* [<span data-ttu-id="65098-157">如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份會怎樣？</span><span class="sxs-lookup"><span data-stu-id="65098-157">What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?</span></span>](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a><span data-ttu-id="65098-158">RDB 持續性</span><span class="sxs-lookup"><span data-stu-id="65098-158">RDB persistence</span></span>
* [<span data-ttu-id="65098-159">在建立 hello 快取之後可以變更 hello RDB 備份頻率嗎？</span><span class="sxs-lookup"><span data-stu-id="65098-159">Can I change hello RDB backup frequency after I create hello cache?</span></span>](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [<span data-ttu-id="65098-160">為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？</span><span class="sxs-lookup"><span data-stu-id="65098-160">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [<span data-ttu-id="65098-161">新的備份進行時，怎樣 toohello 舊 RDB 備份？</span><span class="sxs-lookup"><span data-stu-id="65098-161">What happens toohello old RDB backups when a new backup is made?</span></span>](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a><span data-ttu-id="65098-162">AOF 持續性</span><span class="sxs-lookup"><span data-stu-id="65098-162">AOF persistence</span></span>
* [<span data-ttu-id="65098-163">何時應該使用第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="65098-163">When should I use a second storage account?</span></span>](#when-should-i-use-a-second-storage-account)
* [<span data-ttu-id="65098-164">AOF 持續性是否會影響快取的輸送量、延遲或效能？</span><span class="sxs-lookup"><span data-stu-id="65098-164">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [<span data-ttu-id="65098-165">我要如何移除 hello 第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="65098-165">How can I remove hello second storage account?</span></span>](#how-can-i-remove-the-second-storage-account)
* [<span data-ttu-id="65098-166">什麼是重寫，其對快取有何影響？</span><span class="sxs-lookup"><span data-stu-id="65098-166">What is a rewrite and how does it affect my cache?</span></span>](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [<span data-ttu-id="65098-167">在啟用 AOF 下調整快取預期會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="65098-167">What should I expect when scaling a cache with AOF enabled?</span></span>](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [<span data-ttu-id="65098-168">我的 AOF 資料在儲存體中的組織方式為何？</span><span class="sxs-lookup"><span data-stu-id="65098-168">How is my AOF data organized in storage?</span></span>](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a><span data-ttu-id="65098-169">可以對先前建立的快取啟用永續性嗎？</span><span class="sxs-lookup"><span data-stu-id="65098-169">Can I enable persistence on a previously created cache?</span></span>
<span data-ttu-id="65098-170">可以，可在建立快取時以及現有進階快取中設定 Redis 永續性。</span><span class="sxs-lookup"><span data-stu-id="65098-170">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span></span>

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a><span data-ttu-id="65098-171">啟用在 hello 很少和 RDB 持續性相同的時間？</span><span class="sxs-lookup"><span data-stu-id="65098-171">Can I enable AOF and RDB persistence at hello same time?</span></span>

<span data-ttu-id="65098-172">否，您可以啟用僅 RDB 或很少，但不是能同時執行 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="65098-172">No, you can enable only RDB or AOF, but not both at hello same time.</span></span>

### <a name="which-persistence-model-should-i-choose"></a><span data-ttu-id="65098-173">我應該選擇哪一種持續性模型？</span><span class="sxs-lookup"><span data-stu-id="65098-173">Which persistence model should I choose?</span></span>

<span data-ttu-id="65098-174">很少持續性儲存每個寫入 tooa 記錄檔，會影響部分輸送量，相較於 RDB 持續性 hello 為基礎的備份需要以備份的時間間隔，以設定對效能的影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="65098-174">AOF persistence saves every write tooa log, which has some impact on throughput, compared with RDB persistence which saves backups based on hello configured backup interval, with minimal impact on performance.</span></span> <span data-ttu-id="65098-175">如果您的主要目標 toominimize 資料遺失，而且您可以處理輸送量降低快取，請選擇很少持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-175">Choose AOF persistence if your primary goal is toominimize data loss, and you can handle a decrease in throughput for your cache.</span></span> <span data-ttu-id="65098-176">如果您想在您的快取 toomaintain 最佳輸送量，但仍然想要進行資料復原的機制，請選擇 RDB 持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-176">Choose RDB persistence if you wish toomaintain optimal throughput on your cache, but still want a mechanism for data recovery.</span></span>

* <span data-ttu-id="65098-177">深入了解 hello[優點](https://redis.io/topics/persistence#rdb-advantages)和[缺點](https://redis.io/topics/persistence#rdb-disadvantages)RDB 持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-177">Learn more about hello [advantages](https://redis.io/topics/persistence#rdb-advantages) and [disadvantages](https://redis.io/topics/persistence#rdb-disadvantages) of RDB persistence.</span></span>
* <span data-ttu-id="65098-178">深入了解 hello[優點](https://redis.io/topics/persistence#aof-advantages)和[缺點](https://redis.io/topics/persistence#aof-disadvantages)很少持續性。</span><span class="sxs-lookup"><span data-stu-id="65098-178">Learn more about hello [advantages](https://redis.io/topics/persistence#aof-advantages) and [disadvantages](https://redis.io/topics/persistence#aof-disadvantages) of AOF persistence.</span></span>

<span data-ttu-id="65098-179">如需使用 AOF 持續性時之效能的詳細資訊，請參閱 [AOF 持續性是否會影響快取的輸送量、延遲或效能？](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span><span class="sxs-lookup"><span data-stu-id="65098-179">For more information on performance when using AOF persistence, see [Does AOF persistence affect throughout, latency, or performance of my cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)</span></span>

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a><span data-ttu-id="65098-180">如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份會怎樣？</span><span class="sxs-lookup"><span data-stu-id="65098-180">What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?</span></span>

<span data-ttu-id="65098-181">針對 RDB 和 AOF 持續性：</span><span class="sxs-lookup"><span data-stu-id="65098-181">For both RDB and AOF persistence:</span></span>

* <span data-ttu-id="65098-182">如果您有縮放 tooa 較大的大小，則不會影響。</span><span class="sxs-lookup"><span data-stu-id="65098-182">If you have scaled tooa larger size, there is no impact.</span></span>
* <span data-ttu-id="65098-183">如果您有調整 tooa 較小，而且您有自訂[資料庫](cache-configure.md#databases)設定大於 hello[資料庫限制](cache-configure.md#databases)對於新的大小，不還原那些資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="65098-183">If you have scaled tooa smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than hello [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't restored.</span></span> <span data-ttu-id="65098-184">如需詳細資訊，請參閱[我的自訂資料庫設定在調整期間會受到影響嗎？](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span><span class="sxs-lookup"><span data-stu-id="65098-184">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span></span>
* <span data-ttu-id="65098-185">如果您有向 tooa 較小的大小，hello 所有 hello hello 最後一個備份，索引鍵的資料將會收回 hello 還原程序期間較小的大小 toohold 沒有足夠空間，通常會使用 hello [allkeys lru](http://redis.io/topics/lru-cache)收回原則。</span><span class="sxs-lookup"><span data-stu-id="65098-185">If you have scaled tooa smaller size, and there isn't enough room in hello smaller size toohold all of hello data from hello last backup, keys will be evicted during hello restore process, typically using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span>

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a><span data-ttu-id="65098-186">在建立 hello 快取之後可以變更 hello RDB 備份頻率嗎？</span><span class="sxs-lookup"><span data-stu-id="65098-186">Can I change hello RDB backup frequency after I create hello cache?</span></span>
<span data-ttu-id="65098-187">是，您可以變更在 hello RDB 持續性的 hello 備份頻率**Redis 資料持續性**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="65098-187">Yes, you can change hello backup frequency for RDB persistence on hello **Redis data persistence** blade.</span></span> <span data-ttu-id="65098-188">如需相關指示，請參閱 [設定 Redis 永續性](#configure-redis-persistence)。</span><span class="sxs-lookup"><span data-stu-id="65098-188">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span></span>

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a><span data-ttu-id="65098-189">為什麼我的 RDB 備份頻率是 60 分鐘，備份的間隔卻超過 60 分鐘？</span><span class="sxs-lookup"><span data-stu-id="65098-189">Why if I have an RDB backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>
<span data-ttu-id="65098-190">hello RDB 持續性備份頻率間隔會等到 hello 先前的備份程序已順利完成。</span><span class="sxs-lookup"><span data-stu-id="65098-190">hello RDB persistence backup frequency interval does not start until hello previous backup process has completed successfully.</span></span> <span data-ttu-id="65098-191">如果 hello 備份頻率為 60 分鐘，它會採用完成備份程序 15 分鐘 toosuccessfully hello 下一次備份無法啟動，直到之後 hello 的 75 分鐘開始 hello 先前備份的時間。</span><span class="sxs-lookup"><span data-stu-id="65098-191">If hello backup frequency is 60 minutes and it takes a backup process 15 minutes toosuccessfully complete, hello next backup won't start until 75 minutes after hello start time of hello previous backup.</span></span>

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a><span data-ttu-id="65098-192">新的備份進行時，怎樣 toohello 舊 RDB 備份？</span><span class="sxs-lookup"><span data-stu-id="65098-192">What happens toohello old RDB backups when a new backup is made?</span></span>
<span data-ttu-id="65098-193">所有 RDB 持續性備份，hello 最新的一不會自動都刪除。</span><span class="sxs-lookup"><span data-stu-id="65098-193">All RDB persistence backups except for hello most recent one are automatically deleted.</span></span> <span data-ttu-id="65098-194">這項刪除作業可能不會立即發生，但較舊的備份不會無限期保存。</span><span class="sxs-lookup"><span data-stu-id="65098-194">This deletion may not happen immediately but older backups are not persisted indefinitely.</span></span>


### <a name="when-should-i-use-a-second-storage-account"></a><span data-ttu-id="65098-195">何時應該使用第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="65098-195">When should I use a second storage account?</span></span>

<span data-ttu-id="65098-196">當您認為您有高於 hello 快取的預期的設定作業，您應該很少持續性使用第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65098-196">You should use a second storage account for AOF persistence when you believe you have higher than expected set operations on hello cache.</span></span>  <span data-ttu-id="65098-197">Hello 次要儲存體帳戶的設定可協助確保您的快取不會連線到儲存體頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="65098-197">Setting up hello secondary storage account helps ensure your cache doesn't reach storage bandwidth limits.</span></span>

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a><span data-ttu-id="65098-198">AOF 持續性是否會影響快取的輸送量、延遲或效能？</span><span class="sxs-lookup"><span data-stu-id="65098-198">Does AOF persistence affect throughout, latency, or performance of my cache?</span></span>

<span data-ttu-id="65098-199">很少持續性時，會影響輸送量的大約 15%-20 %hello 快取低於最大負載 (CPU 和伺服器負載兩者在 90%)。</span><span class="sxs-lookup"><span data-stu-id="65098-199">AOF persistence affects throughput by about 15% – 20% when hello cache is below maximum load (CPU and Server Load both under 90%).</span></span> <span data-ttu-id="65098-200">不應該有延遲問題 hello 快取這些限制範圍內時。</span><span class="sxs-lookup"><span data-stu-id="65098-200">There should not be latency issues when hello cache is within these limits.</span></span> <span data-ttu-id="65098-201">不過，hello 快取會達到這些限制較早與啟用很少。</span><span class="sxs-lookup"><span data-stu-id="65098-201">However, hello cache will reach these limits sooner with AOF enabled.</span></span>

### <a name="how-can-i-remove-hello-second-storage-account"></a><span data-ttu-id="65098-202">我要如何移除 hello 第二個儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="65098-202">How can I remove hello second storage account?</span></span>

<span data-ttu-id="65098-203">您可以藉由設定 hello toobe hello 相同 hello 第一個儲存體帳戶為第二個儲存體帳戶中移除 hello 很少持續性次要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65098-203">You can remove hello AOF persistence secondary storage account by setting hello second storage account toobe hello same as hello first storage account.</span></span> <span data-ttu-id="65098-204">如需相關指示，請參閱[設定 AOF 持續性](#configure-aof-persistence)。</span><span class="sxs-lookup"><span data-stu-id="65098-204">For instructions, see [Configure AOF persistence](#configure-aof-persistence).</span></span>

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a><span data-ttu-id="65098-205">什麼是重寫，其對快取有何影響？</span><span class="sxs-lookup"><span data-stu-id="65098-205">What is a rewrite and how does it affect my cache?</span></span>

<span data-ttu-id="65098-206">當 hello 很少檔案變得夠大時，重寫自動排入佇列 hello 快取上。</span><span class="sxs-lookup"><span data-stu-id="65098-206">When hello AOF file becomes large enough, a rewrite is automatically queued on hello cache.</span></span> <span data-ttu-id="65098-207">hello 重寫 hello 很少與最小的 hello 設定檔的作業需要 toocreate hello 目前資料集的調整大小。</span><span class="sxs-lookup"><span data-stu-id="65098-207">hello rewrite resizes hello AOF file with hello minimal set of operations needed toocreate hello current data set.</span></span> <span data-ttu-id="65098-208">在撰寫，預期 tooreach 效能限制更快地尤其是在處理大型資料集。</span><span class="sxs-lookup"><span data-stu-id="65098-208">During rewrites, expect tooreach performance limits sooner especially when dealing with large datasets.</span></span> <span data-ttu-id="65098-209">撰寫發生小於通常 hello 很少檔案變得更大，但需要大量的情況時的時間。</span><span class="sxs-lookup"><span data-stu-id="65098-209">Rewrites occur less often as hello AOF file becomes larger, but will take a significant amount of time when it happens.</span></span>

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a><span data-ttu-id="65098-210">在啟用 AOF 下調整快取預期會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="65098-210">What should I expect when scaling a cache with AOF enabled?</span></span>

<span data-ttu-id="65098-211">如果縮放的 hello 次 hello 很少檔案相當龐大，則預期 hello 延展作業 tootake 時間超出預期行為，因為它將會重新載入 hello 檔案之後調整已完成。</span><span class="sxs-lookup"><span data-stu-id="65098-211">If hello AOF file at hello time of scaling is significantly large, then expect hello scale operation tootake longer than expected since it will be reloading hello file after scaling has finished.</span></span>

<span data-ttu-id="65098-212">如需有關調整的詳細資訊，請參閱[如果我有調整 tooa 不同的大小，而且還原 hello 調整大小作業之前所做的備份，會發生什麼事？](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span><span class="sxs-lookup"><span data-stu-id="65098-212">For more information on scaling, see [What happens if I have scaled tooa different size and a backup is restored that was made before hello scaling operation?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)</span></span>

### <a name="how-is-my-aof-data-organized-in-storage"></a><span data-ttu-id="65098-213">我的 AOF 資料在儲存體中的組織方式為何？</span><span class="sxs-lookup"><span data-stu-id="65098-213">How is my AOF data organized in storage?</span></span>

<span data-ttu-id="65098-214">很少檔案中儲存的資料會分成多個分頁 blob，每個儲存 hello 資料 toostorage 節點 tooincrease 效能。</span><span class="sxs-lookup"><span data-stu-id="65098-214">Data stored in AOF files is divided into multiple page blobs per node tooincrease performance of saving hello data toostorage.</span></span> <span data-ttu-id="65098-215">hello 下表顯示針對每個定價層使用多少的分頁 blob:</span><span class="sxs-lookup"><span data-stu-id="65098-215">hello following table displays how many page blobs are used for each pricing tier:</span></span>

| <span data-ttu-id="65098-216">高階層</span><span class="sxs-lookup"><span data-stu-id="65098-216">Premium tier</span></span> | <span data-ttu-id="65098-217">Blob</span><span class="sxs-lookup"><span data-stu-id="65098-217">Blobs</span></span> |
|--------------|-------|
| <span data-ttu-id="65098-218">P1</span><span class="sxs-lookup"><span data-stu-id="65098-218">P1</span></span>           | <span data-ttu-id="65098-219">每個分區 4 個</span><span class="sxs-lookup"><span data-stu-id="65098-219">4 per shard</span></span>    |
| <span data-ttu-id="65098-220">P2</span><span class="sxs-lookup"><span data-stu-id="65098-220">P2</span></span>           | <span data-ttu-id="65098-221">每個分區 8 個</span><span class="sxs-lookup"><span data-stu-id="65098-221">8 per shard</span></span>    |
| <span data-ttu-id="65098-222">P3</span><span class="sxs-lookup"><span data-stu-id="65098-222">P3</span></span>           | <span data-ttu-id="65098-223">每個分區 16 個</span><span class="sxs-lookup"><span data-stu-id="65098-223">16 per shard</span></span>   |
| <span data-ttu-id="65098-224">P4</span><span class="sxs-lookup"><span data-stu-id="65098-224">P4</span></span>           | <span data-ttu-id="65098-225">每個分區 20 個</span><span class="sxs-lookup"><span data-stu-id="65098-225">20 per shard</span></span>   |

<span data-ttu-id="65098-226">啟用叢集時，hello 快取中的每個分區會有它自己的分頁 blob 集 hello 上表所示。</span><span class="sxs-lookup"><span data-stu-id="65098-226">When clustering is enabled, each shard in hello cache has its own set of page blobs, as indicated in hello previous table.</span></span> <span data-ttu-id="65098-227">例如，具有三個分區的 P2 快取會將其 AOF 檔案散發到 24 個分頁 Blob (3 個分區，所以每個分區 8 個 Blob)。</span><span class="sxs-lookup"><span data-stu-id="65098-227">For example, a P2 cache with three shards distributes its AOF file across 24 page blobs (8 blobs per shard, with 3 shards).</span></span>

<span data-ttu-id="65098-228">重寫後，儲存體中會有兩組 AOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="65098-228">After a rewrite, two sets of AOF files exist in storage.</span></span> <span data-ttu-id="65098-229">撰寫 hello 背景中發生，並附加 toohello 第一組檔案，而傳送嗨重寫期間 toohello 快取的設定作業附加 toohello 第二個集合。</span><span class="sxs-lookup"><span data-stu-id="65098-229">Rewrites occur in hello background and append toohello first set of files, while set operations that are sent toohello cache during hello rewrite append toohello second set.</span></span> <span data-ttu-id="65098-230">重寫期間會暫時儲存備份以備失敗之需，但在重寫完成之後則會立即刪除備份。</span><span class="sxs-lookup"><span data-stu-id="65098-230">A backup is temporarily stored during rewrites in case of failure, but is promptly deleted after a rewrite finishes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65098-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65098-231">Next steps</span></span>
<span data-ttu-id="65098-232">了解如何更進階的 toouse 快取功能。</span><span class="sxs-lookup"><span data-stu-id="65098-232">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="65098-233">簡介 toohello Azure Redis 快取進階層</span><span class="sxs-lookup"><span data-stu-id="65098-233">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
