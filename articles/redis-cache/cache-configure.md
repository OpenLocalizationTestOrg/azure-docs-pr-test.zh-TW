---
title: "aaaHow tooconfigure Azure Redis 快取 |Microsoft 文件"
description: "了解 hello Azure Redis 快取的預設 Redis 組態，並了解如何 tooconfigure Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="61ed1-103">如何 tooconfigure Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="61ed1-104">本主題描述如何 tooreview 和 update hello 設定您的 Azure Redis 快取執行個體，並涵蓋 hello 預設 Redis 伺服器設定 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="61ed1-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-105">如需有關設定和使用 premium 快取功能的詳細資訊，請參閱[如何 tooconfigure 持續性](cache-how-to-premium-persistence.md)，[如何叢集 tooconfigure](cache-how-to-premium-clustering.md)，和[如何 tooconfigure 虛擬網路支援](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="61ed1-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="61ed1-106">設定 Redis 快取設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="61ed1-107">Azure Redis 快取設定會檢視和設定上 hello **Redis 快取**刀鋒視窗中使用 hello**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Redis 快取設定](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="61ed1-109">您可以檢視並設定下列設定使用 hello hello**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="61ed1-110">概觀</span><span class="sxs-lookup"><span data-stu-id="61ed1-110">Overview</span></span>](#overview)
* [<span data-ttu-id="61ed1-111">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="61ed1-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="61ed1-112">存取控制 (IAM)</span><span class="sxs-lookup"><span data-stu-id="61ed1-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="61ed1-113">標記</span><span class="sxs-lookup"><span data-stu-id="61ed1-113">Tags</span></span>](#tags)
* [<span data-ttu-id="61ed1-114">診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="61ed1-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="61ed1-115">設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="61ed1-116">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="61ed1-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="61ed1-117">進階設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="61ed1-118">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="61ed1-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="61ed1-119">調整</span><span class="sxs-lookup"><span data-stu-id="61ed1-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="61ed1-120">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="61ed1-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="61ed1-121">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="61ed1-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="61ed1-122">排程更新</span><span class="sxs-lookup"><span data-stu-id="61ed1-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="61ed1-123">異地複寫</span><span class="sxs-lookup"><span data-stu-id="61ed1-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="61ed1-124">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="61ed1-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="61ed1-125">防火牆</span><span class="sxs-lookup"><span data-stu-id="61ed1-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="61ed1-126">屬性</span><span class="sxs-lookup"><span data-stu-id="61ed1-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="61ed1-127">鎖定</span><span class="sxs-lookup"><span data-stu-id="61ed1-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="61ed1-128">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="61ed1-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="61ed1-129">系統管理</span><span class="sxs-lookup"><span data-stu-id="61ed1-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="61ed1-130">匯入資料</span><span class="sxs-lookup"><span data-stu-id="61ed1-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="61ed1-131">匯出資料</span><span class="sxs-lookup"><span data-stu-id="61ed1-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="61ed1-132">重新啟動</span><span class="sxs-lookup"><span data-stu-id="61ed1-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="61ed1-133">監視</span><span class="sxs-lookup"><span data-stu-id="61ed1-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="61ed1-134">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="61ed1-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="61ed1-135">警示規則</span><span class="sxs-lookup"><span data-stu-id="61ed1-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="61ed1-136">診斷</span><span class="sxs-lookup"><span data-stu-id="61ed1-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="61ed1-137">支援和疑難排解設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="61ed1-138">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="61ed1-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="61ed1-139">新的支援要求</span><span class="sxs-lookup"><span data-stu-id="61ed1-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="61ed1-140">概觀</span><span class="sxs-lookup"><span data-stu-id="61ed1-140">Overview</span></span>

<span data-ttu-id="61ed1-141">**概觀**提供您快取的基本資訊，例如名稱、連接埠、定價層，以及選取的快取度量。</span><span class="sxs-lookup"><span data-stu-id="61ed1-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="61ed1-142">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="61ed1-142">Activity log</span></span>

<span data-ttu-id="61ed1-143">按一下**活動記錄檔**tooview 動作對您的快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="61ed1-144">您也可以使用篩選 tooexpand 此檢視 tooinclude 其他資源。</span><span class="sxs-lookup"><span data-stu-id="61ed1-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="61ed1-145">如需使用稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../azure-resource-manager/resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="61ed1-146">如需有關監視 Azure Redis 快取事件的詳細資訊，請參閱 [作業和警示](cache-how-to-monitor.md#operations-and-alerts)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="61ed1-147">存取控制 (IAM)</span><span class="sxs-lookup"><span data-stu-id="61ed1-147">Access control (IAM)</span></span>

<span data-ttu-id="61ed1-148">hello**存取控制 (IAM)** > 一節提供角色型存取控制 (RBAC) 的支援 hello Azure 入口網站 toohelp 組織符合其存取管理需求簡單和精確地。</span><span class="sxs-lookup"><span data-stu-id="61ed1-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="61ed1-149">如需詳細資訊，請參閱[hello Azure 入口網站中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="61ed1-150">標記</span><span class="sxs-lookup"><span data-stu-id="61ed1-150">Tags</span></span>

<span data-ttu-id="61ed1-151">hello**標記**一節可協助您組織資源。</span><span class="sxs-lookup"><span data-stu-id="61ed1-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="61ed1-152">如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="61ed1-153">診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="61ed1-153">Diagnose and solve problems</span></span>

<span data-ttu-id="61ed1-154">按一下**診斷並解決問題**toobe 提供解決一般問題和策略。</span><span class="sxs-lookup"><span data-stu-id="61ed1-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="61ed1-155">設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-155">Settings</span></span>
<span data-ttu-id="61ed1-156">hello**設定**區段可讓您 tooaccess，並設定下列設定您的快取的 hello。</span><span class="sxs-lookup"><span data-stu-id="61ed1-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="61ed1-157">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="61ed1-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="61ed1-158">進階設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="61ed1-159">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="61ed1-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="61ed1-160">調整</span><span class="sxs-lookup"><span data-stu-id="61ed1-160">Scale</span></span>](#scale)
* [<span data-ttu-id="61ed1-161">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="61ed1-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="61ed1-162">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="61ed1-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="61ed1-163">排程更新</span><span class="sxs-lookup"><span data-stu-id="61ed1-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="61ed1-164">異地複寫</span><span class="sxs-lookup"><span data-stu-id="61ed1-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="61ed1-165">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="61ed1-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="61ed1-166">防火牆</span><span class="sxs-lookup"><span data-stu-id="61ed1-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="61ed1-167">屬性</span><span class="sxs-lookup"><span data-stu-id="61ed1-167">Properties</span></span>](#properties)
* [<span data-ttu-id="61ed1-168">鎖定</span><span class="sxs-lookup"><span data-stu-id="61ed1-168">Locks</span></span>](#locks)
* [<span data-ttu-id="61ed1-169">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="61ed1-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="61ed1-170">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="61ed1-170">Access keys</span></span>
<span data-ttu-id="61ed1-171">按一下**存取金鑰**tooview 或重新建立 hello 存取您的快取的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="61ed1-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="61ed1-172">Hello 連接 tooyour 快取的用戶端會使用這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="61ed1-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Redis 快取存取金鑰](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="61ed1-174">進階設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-174">Advanced settings</span></span>
<span data-ttu-id="61ed1-175">hello 下列設定會在 hello**進階設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="61ed1-176">存取連接埠</span><span class="sxs-lookup"><span data-stu-id="61ed1-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="61ed1-177">記憶體原則</span><span class="sxs-lookup"><span data-stu-id="61ed1-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="61ed1-178">Keyspace 通知 (進階設定)</span><span class="sxs-lookup"><span data-stu-id="61ed1-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="61ed1-179">存取連接埠</span><span class="sxs-lookup"><span data-stu-id="61ed1-179">Access Ports</span></span>
<span data-ttu-id="61ed1-180">根據預設，新的快取會停用非 SSL 存取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="61ed1-181">tooenable hello 非 SSL 連接埠，按一下 **否**如**允許存取僅限透過 SSL**上 hello**進階設定**刀鋒視窗，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Redis 快取存取連接埠](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="61ed1-183">記憶體原則</span><span class="sxs-lookup"><span data-stu-id="61ed1-183">Memory policies</span></span>
<span data-ttu-id="61ed1-184">hello **Maxmemory 原則**， **maxmemory 保留**，和**maxfragmentationmemory 保留**hello 上的設定**進階設定**刀鋒視窗中設定 hello 快取的 hello 記憶體原則。</span><span class="sxs-lookup"><span data-stu-id="61ed1-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Redis 快取 Maxmemory 原則](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="61ed1-186">**Maxmemory 原則**設定 hello hello 快取的收回原則，並可讓您從下列收回原則 hello toochoose:</span><span class="sxs-lookup"><span data-stu-id="61ed1-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="61ed1-187">`volatile-lru`-這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="61ed1-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="61ed1-188">如需 `maxmemory` 原則的詳細資訊，請參閱[收回原則](http://redis.io/topics/lru-cache#eviction-policies)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="61ed1-189">hello **maxmemory 保留**設定會設定為非快取作業，例如複寫容錯移轉期間保留 （mb） 的 hello 的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="61ed1-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="61ed1-190">設定此值可讓您更一致的 Redis 伺服器經驗 toohave 時您的負載而改變。</span><span class="sxs-lookup"><span data-stu-id="61ed1-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="61ed1-191">對於頻繁寫入的工作負載，此值應該設定為更高的值。</span><span class="sxs-lookup"><span data-stu-id="61ed1-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="61ed1-192">當記憶體保留給這類作業時，無法用於儲存快取的資料。</span><span class="sxs-lookup"><span data-stu-id="61ed1-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="61ed1-193">hello **maxfragmentationmemory 保留**設定會設定 hello 的記憶體數量 （mb） 是保留的記憶體分散程度 tooaccommodate。</span><span class="sxs-lookup"><span data-stu-id="61ed1-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="61ed1-194">設定此值可讓您更一致的 Redis 伺服器經驗 toohave hello 快取已滿，或關閉 toofull 和 hello 片段比率很高時。</span><span class="sxs-lookup"><span data-stu-id="61ed1-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="61ed1-195">當記憶體保留給這類作業時，無法用於儲存快取的資料。</span><span class="sxs-lookup"><span data-stu-id="61ed1-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="61ed1-196">選擇新的記憶體保留項目值的一件事 tooconsider (**maxmemory 保留**或**maxfragmentationmemory 保留**) 是這項變更可能會如何影響已在執行與快取大量的資料。</span><span class="sxs-lookup"><span data-stu-id="61ed1-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="61ed1-197">比方說，如果您有 53 GB 快取與 49 GB 的資料，則變更 hello 保留項目值 too8 GB，這將會卸除 hello 最大的可用記憶體 hello 系統關閉 too45 GB。</span><span class="sxs-lookup"><span data-stu-id="61ed1-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="61ed1-198">如果您目前`used_memory`或`used_memory_rss`值高於 hello 新限制 45 gb，則 hello 系統將等到有 tooevict 資料`used_memory`和`used_memory_rss`低於 45 GB。</span><span class="sxs-lookup"><span data-stu-id="61ed1-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="61ed1-199">收回會增加伺服器負載並讓記憶體過於分散。</span><span class="sxs-lookup"><span data-stu-id="61ed1-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="61ed1-200">如需快取計量的詳細資訊，例如 `used_memory` 和 `used_memory_rss`，請參閱[可用計量和報告間隔](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-201">hello **maxmemory 保留**和**maxfragmentationmemory 保留**設定只適用於 Standard 和 Premium 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="61ed1-202">Keyspace 通知 (進階設定)</span><span class="sxs-lookup"><span data-stu-id="61ed1-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="61ed1-203">Redis 的 keyspace 通知設定 hello**進階設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="61ed1-204">Keyspace 通知發生特定事件時，允許用戶端 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="61ed1-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Redis 快取進階設定](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="61ed1-206">Keyspace 通知和 hello**通知 keyspace 事件**設定只適用於標準和進階版快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="61ed1-207">如需詳細資訊，請參閱 [Redis Keyspace 通知](http://redis.io/topics/notifications)(英文)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="61ed1-208">範例程式碼，請參閱 hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs)檔案在 hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。</span><span class="sxs-lookup"><span data-stu-id="61ed1-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="61ed1-209">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="61ed1-209">Redis Cache Advisor</span></span>
<span data-ttu-id="61ed1-210">hello **Redis 快取 Advisor**刀鋒視窗會顯示您的快取的建議。</span><span class="sxs-lookup"><span data-stu-id="61ed1-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="61ed1-211">在一般作業期間，不會顯示任何建議。</span><span class="sxs-lookup"><span data-stu-id="61ed1-211">During normal operations, no recommendations are displayed.</span></span> 

![建議](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="61ed1-213">如果您的快取，例如高記憶體使用量、 網路頻寬或伺服器負載 hello 作業過程中發生任何條件，警示會顯示在 hello **Redis 快取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![建議](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="61ed1-215">可以在 hello 上找到的進一步資訊**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-215">Further information can be found on hello **Recommendations** blade.</span></span>

![建議](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="61ed1-217">您可以監視這些度量在 hello[監控圖表](cache-how-to-monitor.md#monitoring-charts)和[使用量圖表](cache-how-to-monitor.md#usage-charts)區段 hello **Redis 快取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="61ed1-218">每個定價層都有不同的用戶端連線、記憶體和頻寬的限制。</span><span class="sxs-lookup"><span data-stu-id="61ed1-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="61ed1-219">如果您的快取持續一段時間接近這些計量的最大容量，即會提供建議。</span><span class="sxs-lookup"><span data-stu-id="61ed1-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="61ed1-220">如需有關 hello 度量和限制的 hello 檢閱**建議**工具，請參閱下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="61ed1-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="61ed1-221">Redis 快取計量</span><span class="sxs-lookup"><span data-stu-id="61ed1-221">Redis Cache metric</span></span> | <span data-ttu-id="61ed1-222">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="61ed1-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="61ed1-223">網路頻寬使用量</span><span class="sxs-lookup"><span data-stu-id="61ed1-223">Network bandwidth usage</span></span> |[<span data-ttu-id="61ed1-224">快取效能 - 可用的頻寬</span><span class="sxs-lookup"><span data-stu-id="61ed1-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="61ed1-225">連線的用戶端</span><span class="sxs-lookup"><span data-stu-id="61ed1-225">Connected clients</span></span> |[<span data-ttu-id="61ed1-226">預設 Redis 伺服器組態 - maxclients</span><span class="sxs-lookup"><span data-stu-id="61ed1-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="61ed1-227">伺服器負載</span><span class="sxs-lookup"><span data-stu-id="61ed1-227">Server load</span></span> |[<span data-ttu-id="61ed1-228">使用量圖表 - Redis 伺服器負載</span><span class="sxs-lookup"><span data-stu-id="61ed1-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="61ed1-229">記憶體使用量</span><span class="sxs-lookup"><span data-stu-id="61ed1-229">Memory usage</span></span> |[<span data-ttu-id="61ed1-230">快取效能 - 大小</span><span class="sxs-lookup"><span data-stu-id="61ed1-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="61ed1-231">tooupgrade 快取中，按一下 **立即升級**toochange hello 定價層和[標尺](#scale)您的快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="61ed1-232">如需選擇定價層的詳細資訊，請參閱 [應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="61ed1-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="61ed1-233">調整</span><span class="sxs-lookup"><span data-stu-id="61ed1-233">Scale</span></span>
<span data-ttu-id="61ed1-234">按一下**標尺**tooview 或變更定價層快取的 hello。</span><span class="sxs-lookup"><span data-stu-id="61ed1-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="61ed1-235">如需有關調整的詳細資訊，請參閱[如何 tooScale Azure Redis 快取](cache-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis 快取定價層](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="61ed1-237">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="61ed1-237">Redis Cluster Size</span></span>
<span data-ttu-id="61ed1-238">按一下**（預覽） Redis 叢集大小**toochange hello 叢集大小執行進階版快取叢集啟用。</span><span class="sxs-lookup"><span data-stu-id="61ed1-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-239">請注意，雖然 hello Azure Redis 快取進階層已被釋放 tooGeneral 可用性 hello Redis 叢集大小功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="61ed1-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 叢集大小](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="61ed1-241">toochange hello 叢集大小，使用 hello 滑桿，或輸入介於 1 到 10 之間的數字 hello**分區計數**文字方塊中，然後按一下**確定**toosave。</span><span class="sxs-lookup"><span data-stu-id="61ed1-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-242">Redis 叢集只適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="61ed1-243">如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="61ed1-244">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="61ed1-244">Redis data persistence</span></span>
<span data-ttu-id="61ed1-245">按一下**Redis 資料持續性**tooenable，停用或設定您的進階版快取的資料持續性。</span><span class="sxs-lookup"><span data-stu-id="61ed1-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="61ed1-246">Azure Redis 快取使用 [RDB 持續性](cache-how-to-premium-persistence.md#configure-rdb-persistence)或 [AOF 持續性](cache-how-to-premium-persistence.md#configure-aof-persistence)來提供 Redis 持續性。</span><span class="sxs-lookup"><span data-stu-id="61ed1-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="61ed1-247">如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="61ed1-248">Redis 資料持續性僅適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="61ed1-249">更新排程</span><span class="sxs-lookup"><span data-stu-id="61ed1-249">Schedule updates</span></span>
<span data-ttu-id="61ed1-250">hello**更新排程**刀鋒視窗可讓您 toodesignate Redis 快取的伺服器更新的維護視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="61ed1-251">hello 維護視窗適用於僅 tooRedis 伺服器更新，並不 tooany Azure 更新或更新 toohello 作業系統 hello vm 的主機 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![更新排程](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="61ed1-253">toospecify 維護視窗中，檢查所需的 hello 天 hello 維護視窗開始時間的每一天，並指定按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="61ed1-254">請注意，hello 維護視窗時間-utc 時區。</span><span class="sxs-lookup"><span data-stu-id="61ed1-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="61ed1-255">hello**更新排程**功能只適用於 Premium 層快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="61ed1-256">如需詳細資訊和指示，請參閱 [Azure Redis 快取管理 - 排程更新](cache-administration.md#schedule-updates)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="61ed1-257">異地複寫</span><span class="sxs-lookup"><span data-stu-id="61ed1-257">Geo-replication</span></span>

<span data-ttu-id="61ed1-258">hello**地理複寫**刀鋒視窗中提供一個機制，連結兩個 Premium 層 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="61ed1-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="61ed1-259">一個快取指定為 hello 主要的連線快取，而 hello hello 次要連結快取為其他。</span><span class="sxs-lookup"><span data-stu-id="61ed1-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="61ed1-260">hello 次要連結快取會變成唯讀的並寫入的 toohello 主要快取的資料複寫 toohello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="61ed1-261">這項功能可以跨 Azure 區域是使用的 tooreplicate 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-262">**異地複寫**僅適用於進階層快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="61ed1-263">如需詳細資訊和指示，請參閱[如何 Azure Redis 快取的地理複寫 tooconfigure](cache-how-to-geo-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="61ed1-264">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="61ed1-264">Virtual Network</span></span>
<span data-ttu-id="61ed1-265">hello**虛擬網路**區段可讓您快取 tooconfigure hello 虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="61ed1-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="61ed1-266">如需有關使用 VNET 中建立進階版快取資訊支援，並更新其設定，請參閱[如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-267">虛擬網路設定只適用於快取建立期間利用 VNET 支援設定的進階快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="61ed1-268">防火牆</span><span class="sxs-lookup"><span data-stu-id="61ed1-268">Firewall</span></span>

<span data-ttu-id="61ed1-269">按一下**防火牆**tooview 和 Premium Azure Redis 快取設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="61ed1-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![防火牆](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="61ed1-271">您可以利用開始和結束 IP 位址範圍來指定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="61ed1-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="61ed1-272">防火牆規則設定時，只有 hello 來自用戶端連線會指定 IP 位址範圍可以連接 toohello 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="61ed1-273">儲存防火牆規則時是短暫的延遲 hello 規則之前有效。</span><span class="sxs-lookup"><span data-stu-id="61ed1-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="61ed1-274">此延遲通常不超過一分鐘。</span><span class="sxs-lookup"><span data-stu-id="61ed1-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-275">一律允許來自 Azure Redis 快取監視系統的連線，即使設定了防火牆規則也一樣。</span><span class="sxs-lookup"><span data-stu-id="61ed1-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="61ed1-276">防火牆規則僅適用於進階層快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="61ed1-277">屬性</span><span class="sxs-lookup"><span data-stu-id="61ed1-277">Properties</span></span>
<span data-ttu-id="61ed1-278">按一下**屬性**tooview 快取，包括 hello 快取端點及連接埠相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="61ed1-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Redis 快取屬性](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="61ed1-280">鎖定</span><span class="sxs-lookup"><span data-stu-id="61ed1-280">Locks</span></span>
<span data-ttu-id="61ed1-281">hello**鎖定**區段可讓您 toolock 訂用帳戶、 資源群組或資源 tooprevent 不小心刪除或修改重要的資源組織中其他使用者。</span><span class="sxs-lookup"><span data-stu-id="61ed1-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="61ed1-282">如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="61ed1-283">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="61ed1-283">Automation script</span></span>

<span data-ttu-id="61ed1-284">按一下**自動化指令碼**toobuild 和匯出範本，未來的部署。 您已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="61ed1-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="61ed1-285">如需使用範本的詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="61ed1-286">管理設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-286">Administration settings</span></span>
<span data-ttu-id="61ed1-287">hello hello 中的設定**管理**區段可讓您 tooperform hello 下列快取的系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="61ed1-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![系統管理](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="61ed1-289">匯入資料</span><span class="sxs-lookup"><span data-stu-id="61ed1-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="61ed1-290">匯出資料</span><span class="sxs-lookup"><span data-stu-id="61ed1-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="61ed1-291">重新啟動</span><span class="sxs-lookup"><span data-stu-id="61ed1-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="61ed1-292">匯入/匯出</span><span class="sxs-lookup"><span data-stu-id="61ed1-292">Import/Export</span></span>
<span data-ttu-id="61ed1-293">匯入/匯出是可讓您所匯入和匯出 Redis 快取資料庫 (RDB) 快照集 premium 快取 tooa 分頁 blob 中的 Azure 儲存體帳戶中的 hello 快取中的 tooimport 和匯出資料的 Azure Redis 快取資料管理作業。</span><span class="sxs-lookup"><span data-stu-id="61ed1-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="61ed1-294">匯入/匯出可讓您 toomigrate 不同的 Azure Redis 快取執行個體之間，或填入 hello 快取，以使用之前的資料。</span><span class="sxs-lookup"><span data-stu-id="61ed1-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="61ed1-295">匯入可為使用的 toobring Redis 相容 RDB 檔案從任何執行中的任何雲端或環境，包括 Linux、 Windows 或任何雲端提供者，例如 Amazon Web Services 等項目上執行的 Redis 的 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="61ed1-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="61ed1-296">匯入資料是簡單的方式 toocreate 預先填入資料的快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="61ed1-297">在 hello 匯入過程中，Azure Redis 快取 Azure 儲存體中的 hello RDB 檔案載入記憶體，並再插入 hello 快取中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="61ed1-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="61ed1-298">匯出可讓您 tooexport hello 資料儲存在 Azure Redis 快取 tooRedis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="61ed1-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="61ed1-299">您可以使用此功能 toomove 資料從一個 Azure Redis 快取執行個體 tooanother 或 tooanother Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="61ed1-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="61ed1-300">在 hello 匯出程序，hello VM 的主機 hello Azure Redis 快取伺服器執行個體，而且 hello 檔案上傳的 toohello 指定儲存體帳戶上建立暫存檔。</span><span class="sxs-lookup"><span data-stu-id="61ed1-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="61ed1-301">Hello 匯出作業完成時為其中一個狀態為成功或失敗，則會刪除 hello 暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="61ed1-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-302">匯入/匯出僅供進階層快取使用。</span><span class="sxs-lookup"><span data-stu-id="61ed1-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="61ed1-303">如需詳細資訊和指示，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="61ed1-304">重新啟動</span><span class="sxs-lookup"><span data-stu-id="61ed1-304">Reboot</span></span>
<span data-ttu-id="61ed1-305">hello**重新開機**刀鋒視窗可讓您的快取 tooreboot hello 節點。</span><span class="sxs-lookup"><span data-stu-id="61ed1-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="61ed1-306">這個重新開機功能可讓您 tootest 提供恢復功能的應用程式的快取節點失敗時。</span><span class="sxs-lookup"><span data-stu-id="61ed1-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![重新啟動](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="61ed1-308">如果您有進階版快取以啟用叢集時，您可以選取 hello 快取 tooreboot 哪一個的分區。</span><span class="sxs-lookup"><span data-stu-id="61ed1-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![重新啟動](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="61ed1-310">tooreboot 一或多個節點的快取中，選取所需的 hello 節點，然後按一下 **重新開機**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="61ed1-311">如果您有進階版快取之啟用叢集時，選取 hello 分區 tooreboot，然後按一下**重新開機**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="61ed1-312">後幾分鐘的時間，hello 選取的節點重新開機，且上線幾分鐘後。</span><span class="sxs-lookup"><span data-stu-id="61ed1-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61ed1-313">重新啟動現在適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="61ed1-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="61ed1-314">如需詳細資訊和指示，請參閱 [Azure Redis Cache administration - Reboot (Azure Redis 快取管理 - 重新啟動)](cache-administration.md#reboot)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="61ed1-315">監視</span><span class="sxs-lookup"><span data-stu-id="61ed1-315">Monitoring</span></span>

<span data-ttu-id="61ed1-316">hello**監視**區段可讓您 tooconfigure 診斷和監視 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="61ed1-317">如需有關 Azure Redis 快取監視和診斷的詳細資訊，請參閱[如何 toomonitor Azure Redis 快取](cache-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![診斷](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="61ed1-319">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="61ed1-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="61ed1-320">警示規則</span><span class="sxs-lookup"><span data-stu-id="61ed1-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="61ed1-321">診斷</span><span class="sxs-lookup"><span data-stu-id="61ed1-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="61ed1-322">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="61ed1-322">Redis metrics</span></span>
<span data-ttu-id="61ed1-323">按一下**Redis 度量**太[檢視度量](cache-how-to-monitor.md#view-cache-metrics)快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="61ed1-324">警示規則</span><span class="sxs-lookup"><span data-stu-id="61ed1-324">Alert rules</span></span>

<span data-ttu-id="61ed1-325">按一下**警示規則**tooconfigure 警示根據 Redis 快取度量。</span><span class="sxs-lookup"><span data-stu-id="61ed1-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="61ed1-326">如需詳細資訊，請參閱[警示](cache-how-to-monitor.md#alerts)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="61ed1-327">診斷</span><span class="sxs-lookup"><span data-stu-id="61ed1-327">Diagnostics</span></span>

<span data-ttu-id="61ed1-328">根據預設，Azure 監視器中的快取計量會[儲存 30 天](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)，而後刪除。</span><span class="sxs-lookup"><span data-stu-id="61ed1-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="61ed1-329">您的快取度量的時間超過 30 天內，按一下 toopersist**診斷**太[設定 hello 儲存體帳戶](cache-how-to-monitor.md#export-cache-metrics)用 toostore 快取診斷。</span><span class="sxs-lookup"><span data-stu-id="61ed1-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="61ed1-330">在加法 tooarchiving 您快取度量 toostorage，您也可以[它們進行串流處理 tooan 事件中心，或將它們傳送 tooLog 分析](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="61ed1-331">支援和疑難排解設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="61ed1-332">hello hello 中的設定**支援 + 疑難排解**> 一節提供您選項來解決您的快取的問題。</span><span class="sxs-lookup"><span data-stu-id="61ed1-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![支援 + 疑難排解](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="61ed1-334">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="61ed1-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="61ed1-335">新的支援要求</span><span class="sxs-lookup"><span data-stu-id="61ed1-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="61ed1-336">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="61ed1-336">Resource health</span></span>
<span data-ttu-id="61ed1-337">**資源健康狀態** 會監看您的資源，並告知您資源是否正如預期般執行。</span><span class="sxs-lookup"><span data-stu-id="61ed1-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="61ed1-338">如需 hello Azure 資源健全狀況服務的詳細資訊，請參閱[Azure 資源健全狀況概觀](../resource-health/resource-health-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-339">資源健全狀況是目前無法 tooreport hello 的虛擬網路中託管的 Azure Redis 快取執行個體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="61ed1-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="61ed1-340">如需詳細資訊，請參閱 [將快取裝載於 VNET 時，所有快取功能都可以正常運作嗎？](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="61ed1-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="61ed1-341">新增支援要求</span><span class="sxs-lookup"><span data-stu-id="61ed1-341">New support request</span></span>
<span data-ttu-id="61ed1-342">按一下**新增支援要求**tooopen 您的快取的支援要求。</span><span class="sxs-lookup"><span data-stu-id="61ed1-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="61ed1-343">預設 Redis 伺服器組態</span><span class="sxs-lookup"><span data-stu-id="61ed1-343">Default Redis server configuration</span></span>
<span data-ttu-id="61ed1-344">Hello 下列預設的 Redis 組態值來設定新的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="61ed1-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-345">本節中的 hello 設定無法使用 hello 變更`StackExchange.Redis.IServer.ConfigSet`方法。</span><span class="sxs-lookup"><span data-stu-id="61ed1-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="61ed1-346">如果一本章節中的 hello 命令呼叫此方法時，會擲回的例外狀況類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="61ed1-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="61ed1-347">任何值，可加以設定，例如**最大記憶體原則**，可透過 hello Azure 入口網站或 Azure CLI 或 PowerShell 之類的命令列管理工具。</span><span class="sxs-lookup"><span data-stu-id="61ed1-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="61ed1-348">設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-348">Setting</span></span> | <span data-ttu-id="61ed1-349">預設值</span><span class="sxs-lookup"><span data-stu-id="61ed1-349">Default value</span></span> | <span data-ttu-id="61ed1-350">說明</span><span class="sxs-lookup"><span data-stu-id="61ed1-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="61ed1-351">16</span><span class="sxs-lookup"><span data-stu-id="61ed1-351">16</span></span> |<span data-ttu-id="61ed1-352">資料庫的 hello 預設數目為 16，但您可以設定定價層不同數字根據的 hello。<sup>1</sup> hello 預設資料庫為 DB 0，則可以選取每個連線使用不同的`connection.GetDatabase(dbid)`其中`dbid`是之間的數字`0`和`databases - 1`。</span><span class="sxs-lookup"><span data-stu-id="61ed1-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="61ed1-353">取決於定價層的 hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="61ed1-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="61ed1-354">這是 hello 允許在 hello 相同連接的用戶端數目最大時間。</span><span class="sxs-lookup"><span data-stu-id="61ed1-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="61ed1-355">一旦達到 hello 限制 Redis 會關閉所有 hello 新的連接，傳回 '的用戶端達到的最大數目' 錯誤。</span><span class="sxs-lookup"><span data-stu-id="61ed1-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="61ed1-356">Maxmemory 原則是 hello 設定 Redis 如何選取哪些 tooremove 時`maxmemory`為止 （hello 供應項目建立 hello 快取時選取的快取中的 hello 大小）。</span><span class="sxs-lookup"><span data-stu-id="61ed1-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="61ed1-357">Azure Redis 快取 hello 預設值是設定`volatile-lru`，以移除具有以 LRU 演算法設定到期日的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="61ed1-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="61ed1-358">可以在 hello Azure 入口網站中設定此設定。</span><span class="sxs-lookup"><span data-stu-id="61ed1-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="61ed1-359">如需詳細資訊，請參閱[記憶體原則](#memory-policies)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="61ed1-360">3</span><span class="sxs-lookup"><span data-stu-id="61ed1-360">3</span></span> |<span data-ttu-id="61ed1-361">toosave 記憶體、 LRU 和 minimal TTL 演算法是近似的演算法，而不是精確的演算法。</span><span class="sxs-lookup"><span data-stu-id="61ed1-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="61ed1-362">根據預設 Redis 檢查三個索引鍵和取用 hello 其中一個較不最近已使用。</span><span class="sxs-lookup"><span data-stu-id="61ed1-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="61ed1-363">5,000</span><span class="sxs-lookup"><span data-stu-id="61ed1-363">5,000</span></span> |<span data-ttu-id="61ed1-364">Lua 指令碼的最大執行時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="61ed1-365">如果已到達最大執行時間 hello，Redis 會記錄的指令碼仍在執行之後 hello 最大允許的時間，以及啟動 tooreply tooqueries 並產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="61ed1-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="61ed1-366">500</span><span class="sxs-lookup"><span data-stu-id="61ed1-366">500</span></span> |<span data-ttu-id="61ed1-367">指令碼事件佇列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="61ed1-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="61ed1-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="61ed1-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="61ed1-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="61ed1-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="61ed1-370">hello 用戶端輸出緩衝區限制可使用 tooforce 中斷連線的用戶端完全不讀取資料從 hello 伺服器速度夠快，基於某些原因 （常見的原因是 Pub/Sub 用戶端無法以最快速度 hello 發行者產生它們取用訊息）。</span><span class="sxs-lookup"><span data-stu-id="61ed1-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="61ed1-371">如需詳細資訊，請參閱 [http://redis.io/topics/clients](http://redis.io/topics/clients)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="61ed1-372"><a name="databases"></a>
<sup>1</sup>hello 限制`databases`每個 Azure Redis 快取定價層不同，且可以在建立快取設定。</span><span class="sxs-lookup"><span data-stu-id="61ed1-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="61ed1-373">如果沒有`databases`設定指定快取建立期間 hello 預設值為 16。</span><span class="sxs-lookup"><span data-stu-id="61ed1-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="61ed1-374">基本和標準的快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="61ed1-375">C0 250 MB 的快取-too16 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="61ed1-376">C1 1 GB 快取-too16 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="61ed1-377">C2 2.5 GB 的快取-too16 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="61ed1-378">C3 6 GB 的快取-too16 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="61ed1-379">C4 13 GB 快取-too32 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="61ed1-380">C5 (26 GB) 的快取-too48 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="61ed1-381">C6 (53 GB) 的快取-too64 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="61ed1-382">進階快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-382">Premium caches</span></span>
  * <span data-ttu-id="61ed1-383">P1 (6 GB-60 GB)-too16 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="61ed1-384">P2 (13 GB-130 GB)-too32 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="61ed1-385">P3 (26 GB-260 GB)-too48 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="61ed1-386">P4 53 GB-530 GB-too64 資料庫</span><span class="sxs-lookup"><span data-stu-id="61ed1-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="61ed1-387">啟用-Redis 叢集的所有進階版快取 Redis 都叢集的支援使用資料庫 0 因此 hello`databases`限制與 Redis 都叢集啟用任何進階版快取有效地為 1，而 hello[選取](http://redis.io/commands/select)不允許的命令。</span><span class="sxs-lookup"><span data-stu-id="61ed1-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="61ed1-388">如需詳細資訊，請參閱[需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse 嗎？](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="61ed1-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="61ed1-389">如需資料庫的詳細資訊，請參閱[什麼是 Redis 資料庫？](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="61ed1-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-390">hello`databases`設定可設定只有在快取建立期間，而且只使用 PowerShell、 CLI 或其他管理用戶端。</span><span class="sxs-lookup"><span data-stu-id="61ed1-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="61ed1-391">如需在快取建立期間使用 PowerShell 設定 `databases` 的範例，請參閱 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="61ed1-392"><a name="maxclients"></a>
<sup>2</sup>適用於每個 Azure Redis 快取定價層的 `maxclients` 皆不相同。</span><span class="sxs-lookup"><span data-stu-id="61ed1-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="61ed1-393">基本和標準的快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="61ed1-394">C0 250 MB 的快取-too256 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="61ed1-395">C1 1 GB 快取-too1 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="61ed1-396">C2 2.5 GB 的快取-too2 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="61ed1-397">C3 6 GB 的快取-too5 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="61ed1-398">C4 13 GB 快取-too10 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="61ed1-399">C5 (26 GB) 的快取-too15 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="61ed1-400">C6 (53 GB) 的快取-too20 向上、 000 連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="61ed1-401">進階快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-401">Premium caches</span></span>
  * <span data-ttu-id="61ed1-402">P1 (6 GB-60 GB)-向上 too7，500 的連線</span><span class="sxs-lookup"><span data-stu-id="61ed1-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="61ed1-403">P2 (13 GB-130 GB)-too15，000 連線設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="61ed1-404">P3 (26 GB-260 GB)-too30，000 連線設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="61ed1-405">P4 53 GB-530 GB-too40，000 連線設定</span><span class="sxs-lookup"><span data-stu-id="61ed1-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="61ed1-406">每個快取的大小可讓*最多*特定數目的連線，每個連線 tooRedis 具有額外負荷與其相關聯。</span><span class="sxs-lookup"><span data-stu-id="61ed1-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="61ed1-407">因 TLS/SSL 加密而產生的 CPU 與記憶體使用量即是這類額外負荷的其中一例。</span><span class="sxs-lookup"><span data-stu-id="61ed1-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="61ed1-408">指定快取大小的 hello 最大連線限制假設輕度載入的快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="61ed1-409">如果從連接的額外負荷載入*加上*從用戶端作業的負載超過容量的 hello 系統、 hello 快取可以體驗容量問題，即使您未超過 hello 目前快取大小的 hello 連線限制。</span><span class="sxs-lookup"><span data-stu-id="61ed1-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="61ed1-410">Azure Redis 快取中不支援的 Redis 命令</span><span class="sxs-lookup"><span data-stu-id="61ed1-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61ed1-411">設定和管理 Azure Redis 快取執行個體由 Microsoft 管理的因為 hello 下列命令會停用。</span><span class="sxs-lookup"><span data-stu-id="61ed1-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="61ed1-412">如果您嘗試 tooinvoke 它們，您會收到類似的錯誤訊息太`"(error) ERR unknown command"`。</span><span class="sxs-lookup"><span data-stu-id="61ed1-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="61ed1-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="61ed1-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="61ed1-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="61ed1-414">BGSAVE</span></span>
> * <span data-ttu-id="61ed1-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="61ed1-415">CONFIG</span></span>
> * <span data-ttu-id="61ed1-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="61ed1-416">DEBUG</span></span>
> * <span data-ttu-id="61ed1-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="61ed1-417">MIGRATE</span></span>
> * <span data-ttu-id="61ed1-418">SAVE</span><span class="sxs-lookup"><span data-stu-id="61ed1-418">SAVE</span></span>
> * <span data-ttu-id="61ed1-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="61ed1-419">SHUTDOWN</span></span>
> * <span data-ttu-id="61ed1-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="61ed1-420">SLAVEOF</span></span>
> * <span data-ttu-id="61ed1-421">CLUSTER - 叢集寫入命令已停用，但允許唯讀的叢集命令。</span><span class="sxs-lookup"><span data-stu-id="61ed1-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="61ed1-422">如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="61ed1-423">Redis 主控台</span><span class="sxs-lookup"><span data-stu-id="61ed1-423">Redis console</span></span>
<span data-ttu-id="61ed1-424">您可以安全地發出命令使用 hello tooyour Azure Redis 快取執行個體**Redis 主控台**，此功能在 hello Azure 入口網站的所有快取層。</span><span class="sxs-lookup"><span data-stu-id="61ed1-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="61ed1-425">hello Redis 主控台不適用於[VNET](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="61ed1-426">當您的快取是 VNET 的一部分時，hello VNET 中的用戶端可以存取 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="61ed1-427">Redis 主控台在超出範圍 hello VNET，您本機瀏覽器中執行，因為它無法連線 tooyour 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="61ed1-428">Azure Redis 快取並未支援所有的 Redis 命令。</span><span class="sxs-lookup"><span data-stu-id="61ed1-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="61ed1-429">Azure Redis 快取已停用 Redis 命令的清單，請參閱先前的 hello [Redis 命令不支援在 Azure Redis 快取](#redis-commands-not-supported-in-azure-redis-cache)> 一節。</span><span class="sxs-lookup"><span data-stu-id="61ed1-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="61ed1-430">如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="61ed1-431">tooaccess hello Redis 主控台中，按一下**主控台**從 hello **Redis 快取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61ed1-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Redis 主控台](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="61ed1-433">tooissue 命令，針對您的快取執行個體，只要類型 hello 所需的命令到 hello 主控台。</span><span class="sxs-lookup"><span data-stu-id="61ed1-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Redis 主控台](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="61ed1-435">使用 hello Redis 主控台使用 premium 叢集快取</span><span class="sxs-lookup"><span data-stu-id="61ed1-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="61ed1-436">當使用高階 hello Redis 主控台叢集快取時，您可以發出命令 tooa 單一分區 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="61ed1-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="61ed1-437">tooissue 命令 tooa 特定分區，第一次連接 toohello 所需的分區按一下 hello 分區選擇器上。</span><span class="sxs-lookup"><span data-stu-id="61ed1-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Redis 主控台](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="61ed1-439">如果您嘗試 tooaccess 比 hello 連接的分區會儲存在不同的分區化索引鍵，您會收到下列訊息錯誤的訊息類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="61ed1-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="61ed1-440">在 hello 前一個範例中，分區 1 是 hello 選的分區，但是`myKey`hello 所示位於分區 0， `(shard 0)` hello 錯誤訊息的一部分。</span><span class="sxs-lookup"><span data-stu-id="61ed1-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="61ed1-441">在此範例中，tooaccess `myKey`，請選取分區 0 使用 hello 分區選擇器，然後按一下 問題所需的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="61ed1-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="61ed1-442">移動您快取 tooa 新訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="61ed1-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="61ed1-443">您可以按一下來移動快取 tooa 新的訂用**移動**。</span><span class="sxs-lookup"><span data-stu-id="61ed1-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![移動 Redis 快取](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="61ed1-445">如需從一個資源群組 tooanother，以及從一個訂用帳戶 tooanother 移動資源資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="61ed1-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61ed1-446">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61ed1-446">Next steps</span></span>
* <span data-ttu-id="61ed1-447">如需使用 Redis 命令的詳細資訊，請參閱[如何執行 Redis 命令？](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="61ed1-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

