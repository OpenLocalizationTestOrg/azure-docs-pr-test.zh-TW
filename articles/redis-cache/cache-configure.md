---
title: "如何設定 Azure Redis 快取 | Microsoft Docs"
description: "了解 Azure Redis 快取的預設 Redis 組態，以及了解如何設定您的 Azure Redis 快取執行個體"
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
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="bb720-103">如何設定 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="bb720-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="bb720-104">本主題描述如何檢視並更新您的 Azure Redis 快取執行個體的組態，並涵蓋 Azure Redis 快取執行個體的預設 Redis 伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="bb720-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-105">如需設定及使用進階快取功能的詳細資訊，請參閱[如何設定持續性](cache-how-to-premium-persistence.md)、[如何設定叢集](cache-how-to-premium-clustering.md)，以及[如何設定虛擬網路支援](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="bb720-106">設定 Redis 快取設定</span><span class="sxs-lookup"><span data-stu-id="bb720-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="bb720-107">您可以在 [Redis 快取] 刀鋒視窗中使用 [資源功能表] 檢視及設定 Azure Redis 快取設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Redis 快取設定](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="bb720-109">您可以使用 [資源功能表] 檢視及設定下列設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="bb720-110">概觀</span><span class="sxs-lookup"><span data-stu-id="bb720-110">Overview</span></span>](#overview)
* [<span data-ttu-id="bb720-111">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="bb720-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="bb720-112">存取控制 (IAM)</span><span class="sxs-lookup"><span data-stu-id="bb720-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="bb720-113">標記</span><span class="sxs-lookup"><span data-stu-id="bb720-113">Tags</span></span>](#tags)
* [<span data-ttu-id="bb720-114">診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="bb720-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="bb720-115">設定</span><span class="sxs-lookup"><span data-stu-id="bb720-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="bb720-116">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="bb720-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="bb720-117">進階設定</span><span class="sxs-lookup"><span data-stu-id="bb720-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="bb720-118">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="bb720-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="bb720-119">調整</span><span class="sxs-lookup"><span data-stu-id="bb720-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="bb720-120">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="bb720-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="bb720-121">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="bb720-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="bb720-122">排程更新</span><span class="sxs-lookup"><span data-stu-id="bb720-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="bb720-123">異地複寫</span><span class="sxs-lookup"><span data-stu-id="bb720-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="bb720-124">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="bb720-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="bb720-125">防火牆</span><span class="sxs-lookup"><span data-stu-id="bb720-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="bb720-126">屬性</span><span class="sxs-lookup"><span data-stu-id="bb720-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="bb720-127">鎖定</span><span class="sxs-lookup"><span data-stu-id="bb720-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="bb720-128">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="bb720-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="bb720-129">系統管理</span><span class="sxs-lookup"><span data-stu-id="bb720-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="bb720-130">匯入資料</span><span class="sxs-lookup"><span data-stu-id="bb720-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="bb720-131">匯出資料</span><span class="sxs-lookup"><span data-stu-id="bb720-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="bb720-132">重新啟動</span><span class="sxs-lookup"><span data-stu-id="bb720-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="bb720-133">監視</span><span class="sxs-lookup"><span data-stu-id="bb720-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="bb720-134">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="bb720-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="bb720-135">警示規則</span><span class="sxs-lookup"><span data-stu-id="bb720-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="bb720-136">診斷</span><span class="sxs-lookup"><span data-stu-id="bb720-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="bb720-137">支援和疑難排解設定</span><span class="sxs-lookup"><span data-stu-id="bb720-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="bb720-138">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="bb720-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="bb720-139">新的支援要求</span><span class="sxs-lookup"><span data-stu-id="bb720-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="bb720-140">概觀</span><span class="sxs-lookup"><span data-stu-id="bb720-140">Overview</span></span>

<span data-ttu-id="bb720-141">**概觀**提供您快取的基本資訊，例如名稱、連接埠、定價層，以及選取的快取度量。</span><span class="sxs-lookup"><span data-stu-id="bb720-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="bb720-142">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="bb720-142">Activity log</span></span>

<span data-ttu-id="bb720-143">按一下 [活動記錄]  ，以檢視在快取上執行的動作。</span><span class="sxs-lookup"><span data-stu-id="bb720-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="bb720-144">您也可以使用篩選，來展開此檢視以包含其他資源。</span><span class="sxs-lookup"><span data-stu-id="bb720-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="bb720-145">如需使用稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../azure-resource-manager/resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="bb720-146">如需有關監視 Azure Redis 快取事件的詳細資訊，請參閱 [作業和警示](cache-how-to-monitor.md#operations-and-alerts)。</span><span class="sxs-lookup"><span data-stu-id="bb720-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="bb720-147">存取控制 (IAM)</span><span class="sxs-lookup"><span data-stu-id="bb720-147">Access control (IAM)</span></span>

<span data-ttu-id="bb720-148">[存取控制 (IAM)]  區段會在 Azure 入口網站中提供角色型存取控制 (RBAC) 支援，協助組織輕鬆且準確地滿足其存取管理需求。</span><span class="sxs-lookup"><span data-stu-id="bb720-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="bb720-149">如需詳細資訊，請參閱 [Azure 入口網站中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="bb720-150">標記</span><span class="sxs-lookup"><span data-stu-id="bb720-150">Tags</span></span>

<span data-ttu-id="bb720-151">[標記]  區段有助於您組織資源。</span><span class="sxs-lookup"><span data-stu-id="bb720-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="bb720-152">如需詳細資訊，請參閱 [使用標記組織您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="bb720-153">診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="bb720-153">Diagnose and solve problems</span></span>

<span data-ttu-id="bb720-154">按一下 [診斷並解決問題]  將提供您這些常見問題和解決問題的策略。</span><span class="sxs-lookup"><span data-stu-id="bb720-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="bb720-155">設定</span><span class="sxs-lookup"><span data-stu-id="bb720-155">Settings</span></span>
<span data-ttu-id="bb720-156">[設定] 區段中的設定可讓您存取和設定下列快取設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="bb720-157">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="bb720-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="bb720-158">進階設定</span><span class="sxs-lookup"><span data-stu-id="bb720-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="bb720-159">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="bb720-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="bb720-160">調整</span><span class="sxs-lookup"><span data-stu-id="bb720-160">Scale</span></span>](#scale)
* [<span data-ttu-id="bb720-161">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="bb720-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="bb720-162">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="bb720-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="bb720-163">排程更新</span><span class="sxs-lookup"><span data-stu-id="bb720-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="bb720-164">異地複寫</span><span class="sxs-lookup"><span data-stu-id="bb720-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="bb720-165">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="bb720-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="bb720-166">防火牆</span><span class="sxs-lookup"><span data-stu-id="bb720-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="bb720-167">屬性</span><span class="sxs-lookup"><span data-stu-id="bb720-167">Properties</span></span>](#properties)
* [<span data-ttu-id="bb720-168">鎖定</span><span class="sxs-lookup"><span data-stu-id="bb720-168">Locks</span></span>](#locks)
* [<span data-ttu-id="bb720-169">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="bb720-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="bb720-170">存取金鑰</span><span class="sxs-lookup"><span data-stu-id="bb720-170">Access keys</span></span>
<span data-ttu-id="bb720-171">按一下 [存取金鑰]  以檢視或重新產生快取的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="bb720-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="bb720-172">這些金鑰是由連線到您的快取的用戶端所使用。</span><span class="sxs-lookup"><span data-stu-id="bb720-172">These keys are used by the clients connecting to your cache.</span></span>

![Redis 快取存取金鑰](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="bb720-174">進階設定</span><span class="sxs-lookup"><span data-stu-id="bb720-174">Advanced settings</span></span>
<span data-ttu-id="bb720-175">下列設定是在 [進階設定] 刀鋒視窗上進行設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="bb720-176">存取連接埠</span><span class="sxs-lookup"><span data-stu-id="bb720-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="bb720-177">記憶體原則</span><span class="sxs-lookup"><span data-stu-id="bb720-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="bb720-178">Keyspace 通知 (進階設定)</span><span class="sxs-lookup"><span data-stu-id="bb720-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="bb720-179">存取連接埠</span><span class="sxs-lookup"><span data-stu-id="bb720-179">Access Ports</span></span>
<span data-ttu-id="bb720-180">根據預設，新的快取會停用非 SSL 存取。</span><span class="sxs-lookup"><span data-stu-id="bb720-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="bb720-181">若要啟用非 SSL 連接埠，請針對 [進階設定] 刀鋒視窗上的 [只允許透過 SSL 存取]，按一下 [否]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bb720-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Redis 快取存取連接埠](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="bb720-183">記憶體原則</span><span class="sxs-lookup"><span data-stu-id="bb720-183">Memory policies</span></span>
<span data-ttu-id="bb720-184">[進階設定] 刀鋒視窗中的 [Maxmemory 原則]、[maxmemory-reserved] 和 [maxfragmentationmemory-reserved] 設定，會設定快取的記憶體原則。</span><span class="sxs-lookup"><span data-stu-id="bb720-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Redis 快取 Maxmemory 原則](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="bb720-186">[Maxmemory 原則] 設定快取的收回原則，並讓您從下列收回原則中選擇：</span><span class="sxs-lookup"><span data-stu-id="bb720-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="bb720-187">`volatile-lru` - 這是預設值。</span><span class="sxs-lookup"><span data-stu-id="bb720-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="bb720-188">如需 `maxmemory` 原則的詳細資訊，請參閱[收回原則](http://redis.io/topics/lru-cache#eviction-policies)。</span><span class="sxs-lookup"><span data-stu-id="bb720-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="bb720-189">**maxmemory-reserved** 設定會設定保留給非快取作業 (例如容錯移轉期間的複寫) 的記憶體量 (MB)。</span><span class="sxs-lookup"><span data-stu-id="bb720-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="bb720-190">設定此值可讓您在負載變動時具有更一致的 Redis 伺服器體驗。</span><span class="sxs-lookup"><span data-stu-id="bb720-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="bb720-191">對於頻繁寫入的工作負載，此值應該設定為更高的值。</span><span class="sxs-lookup"><span data-stu-id="bb720-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="bb720-192">當記憶體保留給這類作業時，無法用於儲存快取的資料。</span><span class="sxs-lookup"><span data-stu-id="bb720-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="bb720-193">[maxfragmentationmemory-reserved] 設定會以 MB 為單位設定保留的記憶體數量，以容納過於分散的記憶體。</span><span class="sxs-lookup"><span data-stu-id="bb720-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="bb720-194">設定此值可讓您在快取已滿或接近全滿，且片段比率也很高時，有更為一致的 Redis 伺服器體驗。</span><span class="sxs-lookup"><span data-stu-id="bb720-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="bb720-195">當記憶體保留給這類作業時，無法用於儲存快取的資料。</span><span class="sxs-lookup"><span data-stu-id="bb720-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="bb720-196">選擇新的記憶體保留值 (**maxmemory-reserved** 或 **maxfragmentationmemory-reserved**) 時，需要考慮的一件事是，這項變更對已有大量資料在執行的快取會有怎麼樣的影響。</span><span class="sxs-lookup"><span data-stu-id="bb720-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="bb720-197">例如，如果您的快取是 53 GB 而資料為 49 GB，則將保留值變更為 8 GB，會將系統的最大可用記憶體降至 45 GB。</span><span class="sxs-lookup"><span data-stu-id="bb720-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="bb720-198">如果目前的 `used_memory` 或 `used_memory_rss` 值高於 45 GB 的新限制，則等 `used_memory` 和 `used_memory_rss` 都低於 45 GB 後，系統必須收回資料。</span><span class="sxs-lookup"><span data-stu-id="bb720-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="bb720-199">收回會增加伺服器負載並讓記憶體過於分散。</span><span class="sxs-lookup"><span data-stu-id="bb720-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="bb720-200">如需快取計量的詳細資訊，例如 `used_memory` 和 `used_memory_rss`，請參閱[可用計量和報告間隔](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)。</span><span class="sxs-lookup"><span data-stu-id="bb720-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-201">只有標準和高階快取提供 **maxmemory-reserved** 和 **maxfragmentationmemory-reserved** 設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="bb720-202">Keyspace 通知 (進階設定)</span><span class="sxs-lookup"><span data-stu-id="bb720-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="bb720-203">Redis Keyspace 通知是在 [進階設定]  刀鋒視窗上進行設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="bb720-204">Keyspace 通知可讓用戶端在特定事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="bb720-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Redis 快取進階設定](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="bb720-206">Keyspace 通知和 **notify-keyspace-events** 設定只適用於標準和高階快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="bb720-207">如需詳細資訊，請參閱 [Redis Keyspace 通知](http://redis.io/topics/notifications)(英文)。</span><span class="sxs-lookup"><span data-stu-id="bb720-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="bb720-208">如需範例程式碼，請參閱 [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) 範例中的 [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) 檔案。</span><span class="sxs-lookup"><span data-stu-id="bb720-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="bb720-209">Redis 快取顧問</span><span class="sxs-lookup"><span data-stu-id="bb720-209">Redis Cache Advisor</span></span>
<span data-ttu-id="bb720-210">[Redis 快取建議程式] 刀鋒視窗會顯示適用於快取的建議。</span><span class="sxs-lookup"><span data-stu-id="bb720-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="bb720-211">在一般作業期間，不會顯示任何建議。</span><span class="sxs-lookup"><span data-stu-id="bb720-211">During normal operations, no recommendations are displayed.</span></span> 

![建議](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="bb720-213">如果在快取作業期間發生任何狀況 (例如，高記憶體使用量、網路頻寬或伺服器負載)，即會在 [Redis 快取]  刀鋒視窗中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="bb720-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![建議](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="bb720-215">您可以在 [建議]  刀鋒視窗中找到進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="bb720-215">Further information can be found on the **Recommendations** blade.</span></span>

![建議](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="bb720-217">您可以在 [Redis 快取] 刀鋒視窗的[監視圖表](cache-how-to-monitor.md#monitoring-charts)和[使用量圖表](cache-how-to-monitor.md#usage-charts)區段上監視這些計量。</span><span class="sxs-lookup"><span data-stu-id="bb720-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="bb720-218">每個定價層都有不同的用戶端連線、記憶體和頻寬的限制。</span><span class="sxs-lookup"><span data-stu-id="bb720-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="bb720-219">如果您的快取持續一段時間接近這些計量的最大容量，即會提供建議。</span><span class="sxs-lookup"><span data-stu-id="bb720-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="bb720-220">如需透過**建議**工具檢閱的計量和限制詳細資訊，請參閱下表：</span><span class="sxs-lookup"><span data-stu-id="bb720-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="bb720-221">Redis 快取計量</span><span class="sxs-lookup"><span data-stu-id="bb720-221">Redis Cache metric</span></span> | <span data-ttu-id="bb720-222">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="bb720-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="bb720-223">網路頻寬使用量</span><span class="sxs-lookup"><span data-stu-id="bb720-223">Network bandwidth usage</span></span> |[<span data-ttu-id="bb720-224">快取效能 - 可用的頻寬</span><span class="sxs-lookup"><span data-stu-id="bb720-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="bb720-225">連線的用戶端</span><span class="sxs-lookup"><span data-stu-id="bb720-225">Connected clients</span></span> |[<span data-ttu-id="bb720-226">預設 Redis 伺服器組態 - maxclients</span><span class="sxs-lookup"><span data-stu-id="bb720-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="bb720-227">伺服器負載</span><span class="sxs-lookup"><span data-stu-id="bb720-227">Server load</span></span> |[<span data-ttu-id="bb720-228">使用量圖表 - Redis 伺服器負載</span><span class="sxs-lookup"><span data-stu-id="bb720-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="bb720-229">記憶體使用量</span><span class="sxs-lookup"><span data-stu-id="bb720-229">Memory usage</span></span> |[<span data-ttu-id="bb720-230">快取效能 - 大小</span><span class="sxs-lookup"><span data-stu-id="bb720-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="bb720-231">若要升級快取，按一下 [立即升級]  以變更定價層及[調整](#scale)您的快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="bb720-232">如需選擇定價層的詳細資訊，請參閱 [應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="bb720-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="bb720-233">調整</span><span class="sxs-lookup"><span data-stu-id="bb720-233">Scale</span></span>
<span data-ttu-id="bb720-234">按一下 [調整] 以檢視或變更快取的定價層。</span><span class="sxs-lookup"><span data-stu-id="bb720-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="bb720-235">如需調整的詳細資訊，請參閱 [如何調整 Azure Redis Cache](cache-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis 快取定價層](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="bb720-237">Redis 叢集大小</span><span class="sxs-lookup"><span data-stu-id="bb720-237">Redis Cluster Size</span></span>
<span data-ttu-id="bb720-238">按一下 [Redis 叢集大小 (預覽)]  ，針對已啟用叢集且目前執行中的進階快取，變更叢集大小。</span><span class="sxs-lookup"><span data-stu-id="bb720-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-239">請注意，雖然 Azure Redis 快取進階層已發行正式上市版，但 Redis 叢集大小功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="bb720-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis 叢集大小](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="bb720-241">若要變更叢集大小，請使用滑桿，或在 [分區計數] 文字方塊中輸入 1 到 10 之間的數字，然後按一下 [確定] 加以儲存。</span><span class="sxs-lookup"><span data-stu-id="bb720-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-242">Redis 叢集只適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="bb720-243">如需詳細資訊，請參閱 [如何設定進階 Azure Redis 快取的叢集](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="bb720-244">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="bb720-244">Redis data persistence</span></span>
<span data-ttu-id="bb720-245">按一下 [Redis 資料持續性]  可加以啟用、停用，或設定高階快取的資料持續性。</span><span class="sxs-lookup"><span data-stu-id="bb720-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="bb720-246">Azure Redis 快取使用 [RDB 持續性](cache-how-to-premium-persistence.md#configure-rdb-persistence)或 [AOF 持續性](cache-how-to-premium-persistence.md#configure-aof-persistence)來提供 Redis 持續性。</span><span class="sxs-lookup"><span data-stu-id="bb720-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="bb720-247">如需詳細資訊，請參閱 [如何設定進階 Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="bb720-248">Redis 資料持續性僅適用於進階快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="bb720-249">更新排程</span><span class="sxs-lookup"><span data-stu-id="bb720-249">Schedule updates</span></span>
<span data-ttu-id="bb720-250">[排程更新]  刀鋒視窗可讓您指定適用於快取的 Redis 伺服器更新維護期間。</span><span class="sxs-lookup"><span data-stu-id="bb720-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bb720-251">維護期間僅適用於 Redis 伺服器更新，不適用於任何 Azure 更新，或是在裝載快取的 VM 上更新作業系統。</span><span class="sxs-lookup"><span data-stu-id="bb720-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![排程更新](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="bb720-253">若要指定維護期間，請檢查所需的天數，並指定每一天的維護期間開始小時，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bb720-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="bb720-254">請注意，維護期間時間是 UTC。</span><span class="sxs-lookup"><span data-stu-id="bb720-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bb720-255">只有進階層快取提供**排程更新**功能。</span><span class="sxs-lookup"><span data-stu-id="bb720-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="bb720-256">如需詳細資訊和指示，請參閱 [Azure Redis 快取管理 - 排程更新](cache-administration.md#schedule-updates)。</span><span class="sxs-lookup"><span data-stu-id="bb720-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="bb720-257">異地複寫</span><span class="sxs-lookup"><span data-stu-id="bb720-257">Geo-replication</span></span>

<span data-ttu-id="bb720-258">[異地複寫] 刀鋒視窗提供一個機制，可供連結兩個進階層 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="bb720-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="bb720-259">其中一個快取被指定為主要連結快取，而另一個則為次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="bb720-260">次要連結快取會變成唯讀，而寫入主要快取的資料會複寫至次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="bb720-261">這項功能可用來跨 Azure 區域複寫快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-262">**異地複寫**僅適用於進階層快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="bb720-263">如需詳細資訊和指示，請參閱[如何設定 Azure Redis 快取的異地複寫](cache-how-to-geo-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="bb720-264">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="bb720-264">Virtual Network</span></span>
<span data-ttu-id="bb720-265">[虛擬網路] 區段可讓您為快取設定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb720-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="bb720-266">如需使用 VNET 支援建立進階快取並更新其設定的相關資訊，請參閱 [如何設定進階 Azure Redis 快取的虛擬網路支援](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-267">虛擬網路設定只適用於快取建立期間利用 VNET 支援設定的進階快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="bb720-268">防火牆</span><span class="sxs-lookup"><span data-stu-id="bb720-268">Firewall</span></span>

<span data-ttu-id="bb720-269">按一下 [防火牆]，檢視並設定進階 Azure Redis 快取的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="bb720-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![防火牆](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="bb720-271">您可以利用開始和結束 IP 位址範圍來指定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="bb720-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="bb720-272">設定防火牆規則時，只有來自指定 IP 位址範圍的用戶端連線可以連接至快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="bb720-273">儲存防火牆規則時，在規則生效之前，會有短暫的延遲。</span><span class="sxs-lookup"><span data-stu-id="bb720-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="bb720-274">此延遲通常不超過一分鐘。</span><span class="sxs-lookup"><span data-stu-id="bb720-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-275">一律允許來自 Azure Redis 快取監視系統的連線，即使設定了防火牆規則也一樣。</span><span class="sxs-lookup"><span data-stu-id="bb720-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="bb720-276">防火牆規則僅適用於進階層快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="bb720-277">屬性</span><span class="sxs-lookup"><span data-stu-id="bb720-277">Properties</span></span>
<span data-ttu-id="bb720-278">按一下 [屬性]  以檢視快取的相關資訊，包括快取端點和連接埠。</span><span class="sxs-lookup"><span data-stu-id="bb720-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Redis 快取屬性](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="bb720-280">鎖定</span><span class="sxs-lookup"><span data-stu-id="bb720-280">Locks</span></span>
<span data-ttu-id="bb720-281">[鎖定] 區段可讓您鎖定訂用帳戶、資源群組或資源，以防止組織中的其他使用者不小心刪除或修改重要資源。</span><span class="sxs-lookup"><span data-stu-id="bb720-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="bb720-282">如需詳細資訊，請參閱 [使用 Azure 資源管理員來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="bb720-283">自動化指令碼</span><span class="sxs-lookup"><span data-stu-id="bb720-283">Automation script</span></span>

<span data-ttu-id="bb720-284">按一下 [自動化指令碼] 可建置並匯出您所部署資源的範本，供未來部署使用。</span><span class="sxs-lookup"><span data-stu-id="bb720-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="bb720-285">如需使用範本的詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署資源](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="bb720-286">管理設定</span><span class="sxs-lookup"><span data-stu-id="bb720-286">Administration settings</span></span>
<span data-ttu-id="bb720-287">[管理] 區段中的設定可讓您針對快取執行下列管理工作。</span><span class="sxs-lookup"><span data-stu-id="bb720-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![系統管理](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="bb720-289">匯入資料</span><span class="sxs-lookup"><span data-stu-id="bb720-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="bb720-290">匯出資料</span><span class="sxs-lookup"><span data-stu-id="bb720-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="bb720-291">重新啟動</span><span class="sxs-lookup"><span data-stu-id="bb720-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="bb720-292">匯入/匯出</span><span class="sxs-lookup"><span data-stu-id="bb720-292">Import/Export</span></span>
<span data-ttu-id="bb720-293">匯入/匯出是 Azure Redis 快取的資料管理作業，可讓您匯入或匯出快取中的資料，方法是從進階快取將 Redis 快取資料庫 (RDB) 快照集匯入和匯出至 Azure 儲存體帳戶中的分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="bb720-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="bb720-294">匯入/匯出可讓您在不同的 Azure Redis 快取執行個體之間移轉，或在使用前將資料填入快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="bb720-295">匯入可以用來從任何雲端或環境中執行的 Redis 伺服器 (包含在 Linux、Windows 上執行的 Redis，或任何雲端提供者，例如 Amazon Web Services 等) 引入 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="bb720-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="bb720-296">匯入資料是使用預先填入資料建立快取的輕鬆方式。</span><span class="sxs-lookup"><span data-stu-id="bb720-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="bb720-297">在匯入程序期間，Azure Redis 快取會從 Azure 儲存體將 RDB 檔案載入記憶體，然後將金鑰插入快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="bb720-298">匯出可讓您將儲存在 Azure Redis 快取中的資料匯出至 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="bb720-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="bb720-299">您可以使用這項功能，將資料從一個 Azure Redis 快取執行個體移到另一個或其他 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb720-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="bb720-300">在匯出程序期間，會在裝載 Azure Redis 快取伺服器執行個體的 VM 上建立站存檔案，並將檔案上傳至指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb720-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="bb720-301">當匯出作業完成時的狀態為成功或失敗時，都會刪除暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="bb720-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-302">匯入/匯出僅供進階層快取使用。</span><span class="sxs-lookup"><span data-stu-id="bb720-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="bb720-303">如需詳細資訊和指示，請參閱 [在 Azure Redis 快取中匯入與匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="bb720-304">重新啟動</span><span class="sxs-lookup"><span data-stu-id="bb720-304">Reboot</span></span>
<span data-ttu-id="bb720-305">[重新啟動] 刀鋒視窗可讓您重新啟動快取的節點。</span><span class="sxs-lookup"><span data-stu-id="bb720-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="bb720-306">這個重新啟動的能力可讓您測試應用程式在快取節點失敗時的恢復功能。</span><span class="sxs-lookup"><span data-stu-id="bb720-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![重新啟動](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="bb720-308">如果您的進階快取已啟用叢集，您可以選取要重新啟動的快取分區。</span><span class="sxs-lookup"><span data-stu-id="bb720-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![重新啟動](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="bb720-310">若要重新啟動快取的一或多個節點，選取所需的節點，然後按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="bb720-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="bb720-311">如果您的進階快取已啟用叢集，選取要重新啟動的分區，然後按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="bb720-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="bb720-312">稍候幾分鐘之後，選取的節點會重新啟動，並在幾分鐘之後重新上線。</span><span class="sxs-lookup"><span data-stu-id="bb720-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb720-313">重新啟動現在適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="bb720-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="bb720-314">如需詳細資訊和指示，請參閱 [Azure Redis Cache administration - Reboot (Azure Redis 快取管理 - 重新啟動)](cache-administration.md#reboot)。</span><span class="sxs-lookup"><span data-stu-id="bb720-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="bb720-315">監視</span><span class="sxs-lookup"><span data-stu-id="bb720-315">Monitoring</span></span>

<span data-ttu-id="bb720-316">[監視] 區段可讓您設定診斷並監視您的 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="bb720-317">如需有關 Azure Redis 快取監視和診斷的詳細資訊，請參閱[如何監視 Azure Redis 快取](cache-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![診斷](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="bb720-319">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="bb720-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="bb720-320">警示規則</span><span class="sxs-lookup"><span data-stu-id="bb720-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="bb720-321">診斷</span><span class="sxs-lookup"><span data-stu-id="bb720-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="bb720-322">Redis 度量</span><span class="sxs-lookup"><span data-stu-id="bb720-322">Redis metrics</span></span>
<span data-ttu-id="bb720-323">按一下 [Redis 度量] 以針對您的快取[檢視度量](cache-how-to-monitor.md#view-cache-metrics)。</span><span class="sxs-lookup"><span data-stu-id="bb720-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="bb720-324">警示規則</span><span class="sxs-lookup"><span data-stu-id="bb720-324">Alert rules</span></span>

<span data-ttu-id="bb720-325">按一下 [警示規則] 以根據 Redis 快取度量設定警示。</span><span class="sxs-lookup"><span data-stu-id="bb720-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="bb720-326">如需詳細資訊，請參閱[警示](cache-how-to-monitor.md#alerts)。</span><span class="sxs-lookup"><span data-stu-id="bb720-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="bb720-327">診斷</span><span class="sxs-lookup"><span data-stu-id="bb720-327">Diagnostics</span></span>

<span data-ttu-id="bb720-328">根據預設，Azure 監視器中的快取計量會[儲存 30 天](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)，而後刪除。</span><span class="sxs-lookup"><span data-stu-id="bb720-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="bb720-329">若要保存您的快取計量超過 30 天，按一下 [診斷] 以[設定用來儲存快取診斷的儲存體帳戶](cache-how-to-monitor.md#export-cache-metrics)。</span><span class="sxs-lookup"><span data-stu-id="bb720-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="bb720-330">除了將快取計量封存至儲存體，您也可以[將它們串流處理至事件中樞或將它們傳送至 Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)。</span><span class="sxs-lookup"><span data-stu-id="bb720-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="bb720-331">支援和疑難排解設定</span><span class="sxs-lookup"><span data-stu-id="bb720-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="bb720-332">**支援 + 疑難排解** 區段中的設定提供選項，讓您解決快取的問題。</span><span class="sxs-lookup"><span data-stu-id="bb720-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![支援 + 疑難排解](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="bb720-334">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="bb720-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="bb720-335">新的支援要求</span><span class="sxs-lookup"><span data-stu-id="bb720-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="bb720-336">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="bb720-336">Resource health</span></span>
<span data-ttu-id="bb720-337">**資源健康狀態** 會監看您的資源，並告知您資源是否正如預期般執行。</span><span class="sxs-lookup"><span data-stu-id="bb720-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="bb720-338">如需 Azure 資源健康狀態服務的詳細資訊，請參閱 [Azure 資源健康狀態概觀](../resource-health/resource-health-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-339">資源健全狀況目前無法回報裝載於虛擬網路上的 Azure Redis 快取執行個體健全狀況。</span><span class="sxs-lookup"><span data-stu-id="bb720-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="bb720-340">如需詳細資訊，請參閱 [將快取裝載於 VNET 時，所有快取功能都可以正常運作嗎？](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="bb720-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="bb720-341">新增支援要求</span><span class="sxs-lookup"><span data-stu-id="bb720-341">New support request</span></span>
<span data-ttu-id="bb720-342">按一下 [新增支援要求]  以開啟快取的支援要求。</span><span class="sxs-lookup"><span data-stu-id="bb720-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="bb720-343">預設 Redis 伺服器組態</span><span class="sxs-lookup"><span data-stu-id="bb720-343">Default Redis server configuration</span></span>
<span data-ttu-id="bb720-344">新的 Azure Redis 快取執行個體是以下列的預設 Redis 組態值設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-345">您無法使用 `StackExchange.Redis.IServer.ConfigSet` 方法變更本區段中的設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="bb720-346">如果在本區段中利用其中一個命令呼叫此方法，則會擲回如下的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="bb720-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="bb720-347">任何可設定的值 (例如 **max-memory-policy**) 都可以透過 Azure 入口網站或命令列管理工具 (例如 Azure CLI 或 PowerShell) 加以設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="bb720-348">設定</span><span class="sxs-lookup"><span data-stu-id="bb720-348">Setting</span></span> | <span data-ttu-id="bb720-349">預設值</span><span class="sxs-lookup"><span data-stu-id="bb720-349">Default value</span></span> | <span data-ttu-id="bb720-350">說明</span><span class="sxs-lookup"><span data-stu-id="bb720-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="bb720-351">16</span><span class="sxs-lookup"><span data-stu-id="bb720-351">16</span></span> |<span data-ttu-id="bb720-352">資料庫的預設數目為 16，但是您可以根據定價層設定不同的數字。<sup>1</sup> 預設資料庫為 DB 0，您可以根據每個連線使用 `connection.GetDatabase(dbid)` 選取一個不同的資料庫，其中 `dbid` 是介於 `0` 與 `databases - 1` 之間的數字。</span><span class="sxs-lookup"><span data-stu-id="bb720-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="bb720-353">取決於定價層<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="bb720-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="bb720-354">這是允許同時連線的用戶端數目上限。</span><span class="sxs-lookup"><span data-stu-id="bb720-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="bb720-355">一旦達到限制，Redis 會關閉所有新的連線，並傳送「達到用戶端的數目上限」錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb720-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="bb720-356">maxmemory 原則可設定當達到 `maxmemory` (建立快取時所選取之快取提供項目的大小) 時 Redis 將如何選取要移除的具目。</span><span class="sxs-lookup"><span data-stu-id="bb720-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="bb720-357">Azure Redis 快取的預設設定為 `volatile-lru`，其會移除使用 LRU 演算法設定到期日的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bb720-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="bb720-358">此設定可以在 Azure 入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="bb720-359">如需詳細資訊，請參閱[記憶體原則](#memory-policies)。</span><span class="sxs-lookup"><span data-stu-id="bb720-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="bb720-360">3</span><span class="sxs-lookup"><span data-stu-id="bb720-360">3</span></span> |<span data-ttu-id="bb720-361">為了節省記憶體，LRU 和最小 TTL 演算法是近似的演算法而不是精確的演算法。</span><span class="sxs-lookup"><span data-stu-id="bb720-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="bb720-362">依預設 Redis 將檢查三個金鑰，並挑選最近較少使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bb720-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="bb720-363">5,000</span><span class="sxs-lookup"><span data-stu-id="bb720-363">5,000</span></span> |<span data-ttu-id="bb720-364">Lua 指令碼的最大執行時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="bb720-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="bb720-365">如果已到達最大執行時間，Redis 會記錄指令碼在最大允許的時間之後仍在執行中，並開始回覆查詢發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bb720-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="bb720-366">500</span><span class="sxs-lookup"><span data-stu-id="bb720-366">500</span></span> |<span data-ttu-id="bb720-367">指令碼事件佇列的大小上限。</span><span class="sxs-lookup"><span data-stu-id="bb720-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="bb720-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="bb720-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="bb720-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="bb720-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="bb720-370">用戶端輸出緩衝區限制可用來強制中斷基於某些原因而無法足夠快地從伺服器讀取資料之用戶端的連線 (常見的原因是 Pub/Sub 用戶端使用訊息的速度無法與發佈者產生這些訊息的速度一樣快)。</span><span class="sxs-lookup"><span data-stu-id="bb720-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="bb720-371">如需詳細資訊，請參閱 [http://redis.io/topics/clients](http://redis.io/topics/clients)。</span><span class="sxs-lookup"><span data-stu-id="bb720-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="bb720-372"><a name="databases"></a>
<sup>1</sup>適用於每個 Azure Redis 快取定價層的 `databases` 限制皆不相同，可在快取建立時加以設定。</span><span class="sxs-lookup"><span data-stu-id="bb720-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="bb720-373">如果快取建立期間未指定 `databases` 設定，則預設值為 16。</span><span class="sxs-lookup"><span data-stu-id="bb720-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="bb720-374">基本和標準的快取</span><span class="sxs-lookup"><span data-stu-id="bb720-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="bb720-375">C0 (250 MB) 快取 - 最多 16 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="bb720-376">C1 (1 GB) 快取 - 最多 16 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="bb720-377">C2 (2.5 GB) 快取 - 最多 16 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="bb720-378">C3 (6 GB) 快取 - 最多 16 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="bb720-379">C4 (13 GB) 快取 - 最多 32 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="bb720-380">C5 (26 GB) 快取 - 最多 48 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="bb720-381">C6 (53 GB) 快取 - 最多 64 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="bb720-382">進階快取</span><span class="sxs-lookup"><span data-stu-id="bb720-382">Premium caches</span></span>
  * <span data-ttu-id="bb720-383">P1 (6 GB - 60 GB) - 最多 16 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="bb720-384">P2 (13 GB - 130 GB) - 最多 32 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="bb720-385">P3 (26 GB - 260 GB) - 最多 48 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="bb720-386">P4 (53 GB - 530 GB) - 最多 64 個資料庫</span><span class="sxs-lookup"><span data-stu-id="bb720-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="bb720-387">所有進階快取均已啟用 Redis 叢集 - Redis 叢集僅支援使用資料庫 0，因此對於已啟用 Redis 叢集的任何進階快取， `databases` 限制實際上是 1，並且不允許 [Select](http://redis.io/commands/select) 命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="bb720-388">如需詳細資訊，請參閱 [我需要對用戶端應用程式進行任何變更才能使用叢集嗎？](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="bb720-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="bb720-389">如需資料庫的詳細資訊，請參閱[什麼是 Redis 資料庫？](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="bb720-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-390">`databases` 設定，而且只能使用 PowerShell、CLI 或其他管理用戶端。</span><span class="sxs-lookup"><span data-stu-id="bb720-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="bb720-391">如需在快取建立期間使用 PowerShell 設定 `databases` 的範例，請參閱 [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="bb720-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="bb720-392"><a name="maxclients"></a>
<sup>2</sup>適用於每個 Azure Redis 快取定價層的 `maxclients` 皆不相同。</span><span class="sxs-lookup"><span data-stu-id="bb720-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="bb720-393">基本和標準的快取</span><span class="sxs-lookup"><span data-stu-id="bb720-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="bb720-394">C0 (250 MB) 快取 - 最多 256 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="bb720-395">C1 (1 GB) 快取 - 最多 1,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="bb720-396">C2 (2.5GB) 快取 - 最多 2,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="bb720-397">C3 (6 GB) 快取 - 最多 5,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="bb720-398">C4 (13 GB) 快取 - 最多 10,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="bb720-399">C5 (26 GB) 快取 - 最多 15,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="bb720-400">C6 (53 GB) 快取 - 最多 20,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="bb720-401">進階快取</span><span class="sxs-lookup"><span data-stu-id="bb720-401">Premium caches</span></span>
  * <span data-ttu-id="bb720-402">P1 (6 GB - 60 GB) - 最多 7,500 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="bb720-403">P2 (13 GB - 130 GB) - 最多 15,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="bb720-404">P3 (26 GB - 260 GB) - 最多 30,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="bb720-405">P4 (53 GB - 530 GB) - 最多 40,000 個連接</span><span class="sxs-lookup"><span data-stu-id="bb720-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="bb720-406">雖然每種大小的快取皆允許連接數可*多達*某個數目，但對 Redis 的每個連接都有相關聯的負荷。</span><span class="sxs-lookup"><span data-stu-id="bb720-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="bb720-407">因 TLS/SSL 加密而產生的 CPU 與記憶體使用量即是這類額外負荷的其中一例。</span><span class="sxs-lookup"><span data-stu-id="bb720-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="bb720-408">所指定快取大小的連線數上限是假設快取負載情況為輕度。</span><span class="sxs-lookup"><span data-stu-id="bb720-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="bb720-409">如果連接負荷的負擔*加上*用戶端作業的負擔，超過系統的容量，則快取會碰到容量問題，即使您尚未超過目前快取大小的連接限制。</span><span class="sxs-lookup"><span data-stu-id="bb720-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="bb720-410">Azure Redis 快取中不支援的 Redis 命令</span><span class="sxs-lookup"><span data-stu-id="bb720-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bb720-411">因為 Azure Redis 快取執行個體的設定與管理是由 Microsoft 管理，所以會停用下列命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="bb720-412">如果您嘗試叫用它們，會收到類似 `"(error) ERR unknown command"` 的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="bb720-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="bb720-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="bb720-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="bb720-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="bb720-414">BGSAVE</span></span>
> * <span data-ttu-id="bb720-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="bb720-415">CONFIG</span></span>
> * <span data-ttu-id="bb720-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="bb720-416">DEBUG</span></span>
> * <span data-ttu-id="bb720-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="bb720-417">MIGRATE</span></span>
> * <span data-ttu-id="bb720-418">SAVE</span><span class="sxs-lookup"><span data-stu-id="bb720-418">SAVE</span></span>
> * <span data-ttu-id="bb720-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="bb720-419">SHUTDOWN</span></span>
> * <span data-ttu-id="bb720-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="bb720-420">SLAVEOF</span></span>
> * <span data-ttu-id="bb720-421">CLUSTER - 叢集寫入命令已停用，但允許唯讀的叢集命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="bb720-422">如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。</span><span class="sxs-lookup"><span data-stu-id="bb720-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="bb720-423">Redis 主控台</span><span class="sxs-lookup"><span data-stu-id="bb720-423">Redis console</span></span>
<span data-ttu-id="bb720-424">您可以使用 [Redis 主控台] (適用於 Azure 入口網站中的所有快取層) 安全地發出命令給 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="bb720-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="bb720-425">Redis 主控台不使用 [VNET](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="bb720-426">如果您的快取是 VNET 的一部分，只有在 VNET 中的用戶端可以存取快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="bb720-427">由於 Redis 主控台在您的本機瀏覽器 (位於 VNET 之外) 中執行，因此無法連接到您的快取。</span><span class="sxs-lookup"><span data-stu-id="bb720-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="bb720-428">Azure Redis 快取並未支援所有的 Redis 命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="bb720-429">如需對 Azure Redis 快取所停用之 Redis 命令的清單，請參閱先前的 [Azure Redis 快取中不支援的 Redis 命令](#redis-commands-not-supported-in-azure-redis-cache)一節。</span><span class="sxs-lookup"><span data-stu-id="bb720-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="bb720-430">如需 Redis 命令的詳細資訊，請參閱 [http://redis.io/commands](http://redis.io/commands)。</span><span class="sxs-lookup"><span data-stu-id="bb720-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="bb720-431">若要存取 Redis 主控台，請從 [Redis 快取] 刀鋒視窗按一下 [主控台]。</span><span class="sxs-lookup"><span data-stu-id="bb720-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Redis 主控台](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="bb720-433">只需在主控台中輸入想要的命令，即可對您的快取執行個體發出命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Redis 主控台](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="bb720-435">使用 Redis 主控台搭配進階叢集快取</span><span class="sxs-lookup"><span data-stu-id="bb720-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="bb720-436">使用 Redis 主控台搭配進階叢集快取時，您可以向單一快取分區發出命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="bb720-437">若要向特定的分區發出命令，請先按一下分區選擇器上所需的分區進行連線。</span><span class="sxs-lookup"><span data-stu-id="bb720-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Redis 主控台](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="bb720-439">如果您嘗試存取儲存在與連線分區不同分區中的金鑰，您會收到類似下列的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="bb720-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="bb720-440">在上一個範例中，分區 1 是所選的分區，但 `myKey` 位於分區 0，如錯誤訊息的 `(shard 0)` 部分所指出。</span><span class="sxs-lookup"><span data-stu-id="bb720-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="bb720-441">在此範例中，若要存取 `myKey`，使用分區選擇器選取分區 0，然後發出所需的命令。</span><span class="sxs-lookup"><span data-stu-id="bb720-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="bb720-442">將您的快取移動到新的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bb720-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="bb720-443">您也可以按一下 [移動] ，將快取移到新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bb720-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![移動 Redis 快取](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="bb720-445">如需將資源從某個資源群組移到另一個資源群組，以及從某個訂用帳戶移到另一個訂用帳戶的相關資訊，請參閱 [將資源移動到新的資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="bb720-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb720-446">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb720-446">Next steps</span></span>
* <span data-ttu-id="bb720-447">如需使用 Redis 命令的詳細資訊，請參閱[如何執行 Redis 命令？](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="bb720-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

