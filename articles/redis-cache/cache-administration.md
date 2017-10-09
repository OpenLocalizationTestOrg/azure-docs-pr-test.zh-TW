---
title: "aaaHow tooadminister Azure Redis 快取 |Microsoft 文件"
description: "了解 tooperform 系統管理工作這類的重新和排程 Azure Redis 快取更新"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a><span data-ttu-id="bea04-103">如何 tooadminister Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="bea04-103">How tooadminister Azure Redis Cache</span></span>
<span data-ttu-id="bea04-104">本主題描述如何 tooperform 系統管理工作如[重新開機](#reboot)和[排程更新](#schedule-updates)對您的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="bea04-104">This topic describes how tooperform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span></span>

## <a name="reboot"></a><span data-ttu-id="bea04-105">重新啟動</span><span class="sxs-lookup"><span data-stu-id="bea04-105">Reboot</span></span>
<span data-ttu-id="bea04-106">hello**重新開機**刀鋒視窗可讓您 tooreboot 快取的一個或多個節點。</span><span class="sxs-lookup"><span data-stu-id="bea04-106">hello **Reboot** blade allows you tooreboot one or more nodes of your cache.</span></span> <span data-ttu-id="bea04-107">這個重新開機功能可讓您 tootest 提供恢復功能的應用程式的快取節點失敗時。</span><span class="sxs-lookup"><span data-stu-id="bea04-107">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![重新啟動](./media/cache-administration/redis-cache-administration-reboot.png)

<span data-ttu-id="bea04-109">選取 hello 節點 tooreboot，然後按一下**重新開機**。</span><span class="sxs-lookup"><span data-stu-id="bea04-109">Select hello nodes tooreboot and click **Reboot**.</span></span>

![重新啟動](./media/cache-administration/redis-cache-reboot.png)

<span data-ttu-id="bea04-111">如果您有進階版快取以啟用叢集時，您可以選取 hello 快取 tooreboot 哪一個的分區。</span><span class="sxs-lookup"><span data-stu-id="bea04-111">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![重新啟動](./media/cache-administration/redis-cache-reboot-cluster.png)

<span data-ttu-id="bea04-113">tooreboot 一或多個節點的快取中，選取所需的 hello 節點，然後按一下 **重新開機**。</span><span class="sxs-lookup"><span data-stu-id="bea04-113">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="bea04-114">如果您有進階版快取之啟用叢集時，選取所需的 hello 分區 tooreboot，然後按一下**重新開機**。</span><span class="sxs-lookup"><span data-stu-id="bea04-114">If you have a premium cache with clustering enabled, select hello desired shards tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="bea04-115">後幾分鐘的時間，hello 選取的節點重新開機，且上線幾分鐘後。</span><span class="sxs-lookup"><span data-stu-id="bea04-115">After a few minutes, hello selected nodes reboot, and are back online a few minutes later.</span></span>

<span data-ttu-id="bea04-116">hello 影響用戶端應用程式而異的哪些節點您重新開機。</span><span class="sxs-lookup"><span data-stu-id="bea04-116">hello impact on client applications varies depending on which nodes that you reboot.</span></span>

* <span data-ttu-id="bea04-117">**主要**-hello 主要節點重新啟動，Azure Redis 快取失敗 toohello 複本節點上，並將它升級 toomaster 時。</span><span class="sxs-lookup"><span data-stu-id="bea04-117">**Master** - When hello master node is rebooted, Azure Redis Cache fails over toohello replica node and promotes it toomaster.</span></span> <span data-ttu-id="bea04-118">在此容錯移轉，可能會較短的間隔中的連線可能會失敗 toohello 快取。</span><span class="sxs-lookup"><span data-stu-id="bea04-118">During this failover, there may be a short interval in which connections may fail toohello cache.</span></span>
* <span data-ttu-id="bea04-119">**從屬**-時 hello 從屬節點重新開機時，通常是沒有影響 toocache 用戶端。</span><span class="sxs-lookup"><span data-stu-id="bea04-119">**Slave** - When hello slave node is rebooted, there is typically no impact toocache clients.</span></span>
* <span data-ttu-id="bea04-120">**主要和備用**-當這兩個快取節點重新開機時，hello 主要節點恢復上線之前，將會遺失在 hello 快取和連線 toohello 快取失敗的所有資料。</span><span class="sxs-lookup"><span data-stu-id="bea04-120">**Both master and slave** - When both cache nodes are rebooted, all data is lost in hello cache and connections toohello cache fail until hello primary node comes back online.</span></span> <span data-ttu-id="bea04-121">如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，hello 最新的備份還原時 hello 快取的重新上線，但 hello 最近備份之後發生的任何快取寫入都會遺失。</span><span class="sxs-lookup"><span data-stu-id="bea04-121">If you have configured [data persistence](cache-how-to-premium-persistence.md), hello most recent backup is restored when hello cache comes back online, but any cache writes that occurred after hello most recent backup are lost.</span></span>
* <span data-ttu-id="bea04-122">**快取啟用叢集節點的高階**-當您重新啟動其中一個或更多進階版快取叢集的節點已啟用，hello 行為 hello 選取節點是 hello 相同做為當您重新啟動 hello 對應的節點或節點的非叢集快取。</span><span class="sxs-lookup"><span data-stu-id="bea04-122">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, hello behavior for hello selected nodes is hello same as when you reboot hello corresponding node or nodes of a non-clustered cache.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bea04-123">重新啟動現在適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="bea04-123">Reboot is now available for all pricing tiers.</span></span>
> 
> 

## <a name="reboot-faq"></a><span data-ttu-id="bea04-124">重新啟動常見問題集</span><span class="sxs-lookup"><span data-stu-id="bea04-124">Reboot FAQ</span></span>
* [<span data-ttu-id="bea04-125">哪些節點應該我重新啟動 tootest 我的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-125">Which node should I reboot tootest my application?</span></span>](#which-node-should-i-reboot-to-test-my-application)
* [<span data-ttu-id="bea04-126">可以重新啟動 hello 快取 tooclear 用戶端連線嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-126">Can I reboot hello cache tooclear client connections?</span></span>](#can-i-reboot-the-cache-to-clear-client-connections)
* [<span data-ttu-id="bea04-127">如果我重新啟動，將會遺失快取中的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-127">Will I lose data from my cache if I do a reboot?</span></span>](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [<span data-ttu-id="bea04-128">我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-128">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="bea04-129">哪些定價層可以使用 hello 重新開機功能嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-129">What pricing tiers can use hello reboot functionality?</span></span>](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a><span data-ttu-id="bea04-130">哪些節點應該我重新啟動 tootest 我的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-130">Which node should I reboot tootest my application?</span></span>
<span data-ttu-id="bea04-131">tootest hello 恢復功能的應用程式發生故障的 hello 主要節點的快取、 重新開機 hello **Master**節點。</span><span class="sxs-lookup"><span data-stu-id="bea04-131">tootest hello resiliency of your application against failure of hello primary node of your cache, reboot hello **Master** node.</span></span> <span data-ttu-id="bea04-132">tootest hello 恢復功能的應用程式發生故障的 hello 次要節點，重新開機 hello**從屬**節點。</span><span class="sxs-lookup"><span data-stu-id="bea04-132">tootest hello resiliency of your application against failure of hello secondary node, reboot hello **Slave** node.</span></span> <span data-ttu-id="bea04-133">tootest hello 復原應用程式的總發生故障的 hello 快取，重新啟動**兩者**節點。</span><span class="sxs-lookup"><span data-stu-id="bea04-133">tootest hello resiliency of your application against total failure of hello cache, reboot **Both** nodes.</span></span>

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a><span data-ttu-id="bea04-134">可以重新啟動 hello 快取 tooclear 用戶端連線嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-134">Can I reboot hello cache tooclear client connections?</span></span>
<span data-ttu-id="bea04-135">是，如果您重新啟動 hello 快取會清除所有用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="bea04-135">Yes, if you reboot hello cache all client connections are cleared.</span></span> <span data-ttu-id="bea04-136">重新開機可以是其中所有用戶端連接都用完到期 tooa 邏輯錯誤或 hello 用戶端應用程式中的 bug hello 案例中很有用。</span><span class="sxs-lookup"><span data-stu-id="bea04-136">Rebooting can be useful in hello case where all client connections are used up due tooa logic error or a bug in hello client application.</span></span> <span data-ttu-id="bea04-137">每個定價層而有不同[用戶端連線限制](cache-configure.md#default-redis-server-configuration)的 hello 各種大小，而且一旦達到這些限制，會接受用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="bea04-137">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for hello various sizes, and once these limits are reached, no more client connections are accepted.</span></span> <span data-ttu-id="bea04-138">重新開機 hello 快取提供方式 tooclear 所有用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="bea04-138">Rebooting hello cache provides a way tooclear all client connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bea04-139">如果您重新啟動您的快取 tooclear 用戶端連線，StackExchange.Redis 會自動重新連線之後 hello Redis 節點上線。</span><span class="sxs-lookup"><span data-stu-id="bea04-139">If you reboot your cache tooclear client connections, StackExchange.Redis automatically reconnects once hello Redis node is back online.</span></span> <span data-ttu-id="bea04-140">如果未解決根本問題的 hello，hello 用戶端連線可能會繼續 toobe 用完。</span><span class="sxs-lookup"><span data-stu-id="bea04-140">If hello underlying issue is not resolved, hello client connections may continue toobe used up.</span></span>
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a><span data-ttu-id="bea04-141">如果我重新啟動，將會遺失快取中的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-141">Will I lose data from my cache if I do a reboot?</span></span>
<span data-ttu-id="bea04-142">如果您重新啟動這兩個 hello **Master**和**從屬**節點 hello 快取 （或如果您使用進階版快取叢集啟用該分區） 中的所有資料都都會遺失。</span><span class="sxs-lookup"><span data-stu-id="bea04-142">If you reboot both hello **Master** and **Slave** nodes, all data in hello cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span></span> <span data-ttu-id="bea04-143">如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，hello 快取的重新上線，但 hello 備份之後所發生的任何快取寫入都會遺失時，將會還原 hello 最新備份。</span><span class="sxs-lookup"><span data-stu-id="bea04-143">If you have configured [data persistence](cache-how-to-premium-persistence.md), hello most recent backup will be restored when hello cache comes back online, but any cache writes that have occurred after hello backup was made are lost.</span></span>

<span data-ttu-id="bea04-144">如果您重新啟動其中一個 hello 節點，資料不是通常遺失，但仍可能。</span><span class="sxs-lookup"><span data-stu-id="bea04-144">If you reboot just one of hello nodes, data is not typically lost, but it still may be.</span></span> <span data-ttu-id="bea04-145">例如，如果 hello 主要節點重新開機，而且快取寫入正在進行中，從 hello 快取寫入 hello 資料就會遺失。</span><span class="sxs-lookup"><span data-stu-id="bea04-145">For example if hello master node is rebooted and a cache write is in progress, hello data from hello cache write is lost.</span></span> <span data-ttu-id="bea04-146">另一個資料遺失的狀況是如果您重新啟動一個節點，然後 hello 其他節點會 toogo 向下 hello tooa 失敗因為相同的時間。</span><span class="sxs-lookup"><span data-stu-id="bea04-146">Another scenario for data loss would be if you reboot one node and hello other node happens toogo down due tooa failure at hello same time.</span></span> <span data-ttu-id="bea04-147">如需資料遺失的可能原因的詳細資訊，請參閱[Redis 在何種情形的 toomy 資料嗎？](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span><span class="sxs-lookup"><span data-stu-id="bea04-147">For more information about possible causes for data loss, see [What happened toomy data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span></span>

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="bea04-148">我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-148">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="bea04-149">是，適用於 PowerShell 指示看到[tooreboot Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="bea04-149">Yes, for PowerShell instructions see [tooreboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span></span>

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a><span data-ttu-id="bea04-150">哪些定價層可以使用 hello 重新開機功能嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-150">What pricing tiers can use hello reboot functionality?</span></span>
<span data-ttu-id="bea04-151">重新啟動適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="bea04-151">Reboot is available for all pricing tiers.</span></span>

## <a name="schedule-updates"></a><span data-ttu-id="bea04-152">更新排程</span><span class="sxs-lookup"><span data-stu-id="bea04-152">Schedule updates</span></span>
<span data-ttu-id="bea04-153">hello**更新排程**刀鋒視窗可讓您 toodesignate Premium 層快取的維護視窗。</span><span class="sxs-lookup"><span data-stu-id="bea04-153">hello **Schedule updates** blade allows you toodesignate a maintenance window for your Premium tier cache.</span></span> <span data-ttu-id="bea04-154">當指定 hello 維護視窗時，Redis 伺服器的任何更新都會在此期間。</span><span class="sxs-lookup"><span data-stu-id="bea04-154">When hello maintenance window is specified, any Redis server updates are made during this window.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bea04-155">hello 維護視窗適用於僅 tooRedis 伺服器更新，並不 tooany Azure 更新或更新 toohello 作業系統 hello vm 的主機 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="bea04-155">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![更新排程](./media/cache-administration/redis-schedule-updates.png)

<span data-ttu-id="bea04-157">toospecify 維護視窗中，檢查所需的 hello 天 hello 維護視窗開始時間的每一天，並指定按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="bea04-157">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="bea04-158">請注意，hello 維護視窗時間-utc 時區。</span><span class="sxs-lookup"><span data-stu-id="bea04-158">Note that hello maintenance window time is in UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="bea04-159">更新 hello 預設維護視窗是 5 小時。</span><span class="sxs-lookup"><span data-stu-id="bea04-159">hello default maintenance window for updates is five hours.</span></span> <span data-ttu-id="bea04-160">這個值不是可從 hello Azure 入口網站設定，但您可以設定它在 PowerShell 中使用 hello `MaintenanceWindow` hello 參數[新增 AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bea04-160">This value is not configurable from hello Azure portal, but you can configure it in PowerShell using hello `MaintenanceWindow` parameter of hello [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet.</span></span> <span data-ttu-id="bea04-161">如需詳細資訊，請參閱[我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span><span class="sxs-lookup"><span data-stu-id="bea04-161">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span></span>
> 
> 

## <a name="schedule-updates-faq"></a><span data-ttu-id="bea04-162">排程更新常見問題集</span><span class="sxs-lookup"><span data-stu-id="bea04-162">Schedule updates FAQ</span></span>
* [<span data-ttu-id="bea04-163">更新時如果我沒有將 hello 排程更新功能？</span><span class="sxs-lookup"><span data-stu-id="bea04-163">When do updates occur if I don't use hello schedule updates feature?</span></span>](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [<span data-ttu-id="bea04-164">Hello 期間所做的更新類型排程維護視窗嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-164">What type of updates are made during hello scheduled maintenance window?</span></span>](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [<span data-ttu-id="bea04-165">我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-165">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span></span>](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="bea04-166">哪些定價層可以使用 hello 排程更新的功能嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-166">What pricing tiers can use hello schedule updates functionality?</span></span>](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a><span data-ttu-id="bea04-167">更新時如果我沒有將 hello 排程更新功能？</span><span class="sxs-lookup"><span data-stu-id="bea04-167">When do updates occur if I don't use hello schedule updates feature?</span></span>
<span data-ttu-id="bea04-168">如果您未指定維護期間，隨時都可進行更新。</span><span class="sxs-lookup"><span data-stu-id="bea04-168">If you don't specify a maintenance window, updates can be made at any time.</span></span>

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a><span data-ttu-id="bea04-169">Hello 期間所做的更新類型排程維護視窗嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-169">What type of updates are made during hello scheduled maintenance window?</span></span>
<span data-ttu-id="bea04-170">只有 Redis 的伺服器 hello 排程的維護期間進行更新。</span><span class="sxs-lookup"><span data-stu-id="bea04-170">Only Redis server updates are made during hello scheduled maintenance window.</span></span> <span data-ttu-id="bea04-171">hello 維護視窗不會套用 tooAzure 更新，或更新 toohello VM 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="bea04-171">hello maintenance window does not apply tooAzure updates or updates toohello VM operating system.</span></span>

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="bea04-172">我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-172">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="bea04-173">是，您可以管理您使用下列 PowerShell 指令程式的 hello 的排程的更新：</span><span class="sxs-lookup"><span data-stu-id="bea04-173">Yes, you can manage your scheduled updates using hello following PowerShell cmdlets:</span></span>

* [<span data-ttu-id="bea04-174">Get-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="bea04-174">Get-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [<span data-ttu-id="bea04-175">New-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="bea04-175">New-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [<span data-ttu-id="bea04-176">New-AzureRmRedisCacheScheduleEntry</span><span class="sxs-lookup"><span data-stu-id="bea04-176">New-AzureRmRedisCacheScheduleEntry</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [<span data-ttu-id="bea04-177">Remove-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="bea04-177">Remove-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a><span data-ttu-id="bea04-178">哪些定價層可以使用 hello 排程更新的功能嗎？</span><span class="sxs-lookup"><span data-stu-id="bea04-178">What pricing tiers can use hello schedule updates functionality?</span></span>
<span data-ttu-id="bea04-179">hello**更新排程**功能僅供以 hello premium 定價層。</span><span class="sxs-lookup"><span data-stu-id="bea04-179">hello **Schedule updates** feature is only available in hello premium pricing tier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bea04-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bea04-180">Next steps</span></span>
* <span data-ttu-id="bea04-181">瀏覽 [Azure Redis 快取進階層](cache-premium-tier-intro.md) 功能。</span><span class="sxs-lookup"><span data-stu-id="bea04-181">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span></span>

