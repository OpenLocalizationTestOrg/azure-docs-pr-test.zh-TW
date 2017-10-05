---
title: "如何管理 Azure Redis 快取 | Microsoft Docs"
description: "了解如何執行管理工作，例如重新啟動以及排程 Azure Redis 快取更新"
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
ms.openlocfilehash: 3352fec59d7dfbfab9b0416992a60f11d0ec2402
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-administer-azure-redis-cache"></a><span data-ttu-id="a169a-103">如何管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="a169a-103">How to administer Azure Redis Cache</span></span>
<span data-ttu-id="a169a-104">本主題說明如何執行管理工作，例如為 Azure Redis 快取執行個體進行[重新啟動](#reboot)並[排程更新](#schedule-updates)。</span><span class="sxs-lookup"><span data-stu-id="a169a-104">This topic describes how to perform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span></span>

## <a name="reboot"></a><span data-ttu-id="a169a-105">重新啟動</span><span class="sxs-lookup"><span data-stu-id="a169a-105">Reboot</span></span>
<span data-ttu-id="a169a-106">[重新啟動]  刀鋒視窗可讓您重新啟動快取的一或多個節點。</span><span class="sxs-lookup"><span data-stu-id="a169a-106">The **Reboot** blade allows you to reboot one or more nodes of your cache.</span></span> <span data-ttu-id="a169a-107">這個重新啟動的能力可讓您測試應用程式在快取節點失敗時的恢復功能。</span><span class="sxs-lookup"><span data-stu-id="a169a-107">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![重新啟動](./media/cache-administration/redis-cache-administration-reboot.png)

<span data-ttu-id="a169a-109">選取要重新啟動的節點，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="a169a-109">Select the nodes to reboot and click **Reboot**.</span></span>

![重新啟動](./media/cache-administration/redis-cache-reboot.png)

<span data-ttu-id="a169a-111">如果您的進階快取已啟用叢集，您可以選取要重新啟動的快取分區。</span><span class="sxs-lookup"><span data-stu-id="a169a-111">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![重新啟動](./media/cache-administration/redis-cache-reboot-cluster.png)

<span data-ttu-id="a169a-113">若要重新啟動快取的一或多個節點，選取所需的節點，然後按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="a169a-113">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="a169a-114">如果您的進階快取已啟用叢集，選取要重新啟動的分區，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="a169a-114">If you have a premium cache with clustering enabled, select the desired shards to reboot and then click **Reboot**.</span></span> <span data-ttu-id="a169a-115">稍候幾分鐘之後，選取的節點會重新啟動，並在幾分鐘之後重新上線。</span><span class="sxs-lookup"><span data-stu-id="a169a-115">After a few minutes, the selected nodes reboot, and are back online a few minutes later.</span></span>

<span data-ttu-id="a169a-116">對於用戶端應用程式的影響，會根據您重新啟動的節點而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a169a-116">The impact on client applications varies depending on which nodes that you reboot.</span></span>

* <span data-ttu-id="a169a-117">**主要** - 重新啟動主要節點時，Azure Redis 快取會容錯移轉至複本節點，並將其升級為主要節點。</span><span class="sxs-lookup"><span data-stu-id="a169a-117">**Master** - When the master node is rebooted, Azure Redis Cache fails over to the replica node and promotes it to master.</span></span> <span data-ttu-id="a169a-118">在此容錯移轉期間，可能會有一小段時間無法連接快取。</span><span class="sxs-lookup"><span data-stu-id="a169a-118">During this failover, there may be a short interval in which connections may fail to the cache.</span></span>
* <span data-ttu-id="a169a-119">**從屬** - 重新啟動從屬節點時，通常不會對快取用戶端產生任何影響。</span><span class="sxs-lookup"><span data-stu-id="a169a-119">**Slave** - When the slave node is rebooted, there is typically no impact to cache clients.</span></span>
* <span data-ttu-id="a169a-120">**主要和從屬** - 重新啟動這兩個快取節點時，在主要節點恢復上線之前，將會遺失快取中的所有資料且無法連接快取。</span><span class="sxs-lookup"><span data-stu-id="a169a-120">**Both master and slave** - When both cache nodes are rebooted, all data is lost in the cache and connections to the cache fail until the primary node comes back online.</span></span> <span data-ttu-id="a169a-121">如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，則當快取恢復連線時，將會還原最近一次備份，但在此備份後發生的任何快取寫入將會遺失。</span><span class="sxs-lookup"><span data-stu-id="a169a-121">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup is restored when the cache comes back online, but any cache writes that occurred after the most recent backup are lost.</span></span>
* <span data-ttu-id="a169a-122">**已啟用叢集的進階快取節點** - 當您重新啟動一或多個已啟用叢集的進階快取節點時，所選節點的行為與您重新啟動回應節點或非叢集快取的節點時相同。</span><span class="sxs-lookup"><span data-stu-id="a169a-122">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, the behavior for the selected nodes is the same as when you reboot the corresponding node or nodes of a non-clustered cache.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a169a-123">重新啟動現在適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="a169a-123">Reboot is now available for all pricing tiers.</span></span>
> 
> 

## <a name="reboot-faq"></a><span data-ttu-id="a169a-124">重新啟動常見問題集</span><span class="sxs-lookup"><span data-stu-id="a169a-124">Reboot FAQ</span></span>
* [<span data-ttu-id="a169a-125">若要測試我的應用程式，我應該重新啟動哪一個節點？</span><span class="sxs-lookup"><span data-stu-id="a169a-125">Which node should I reboot to test my application?</span></span>](#which-node-should-i-reboot-to-test-my-application)
* [<span data-ttu-id="a169a-126">我可以重新啟動快取來清除用戶端連線嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-126">Can I reboot the cache to clear client connections?</span></span>](#can-i-reboot-the-cache-to-clear-client-connections)
* [<span data-ttu-id="a169a-127">如果我重新啟動，將會遺失快取中的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-127">Will I lose data from my cache if I do a reboot?</span></span>](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [<span data-ttu-id="a169a-128">我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-128">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="a169a-129">哪些定價層可以使用重新啟動功能？</span><span class="sxs-lookup"><span data-stu-id="a169a-129">What pricing tiers can use the reboot functionality?</span></span>](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-to-test-my-application"></a><span data-ttu-id="a169a-130">若要測試我的應用程式，我應該重新啟動哪一個節點？</span><span class="sxs-lookup"><span data-stu-id="a169a-130">Which node should I reboot to test my application?</span></span>
<span data-ttu-id="a169a-131">若要針對快取的主要節點失敗測試應用程式復原功能，重新啟動 **主要** 節點。</span><span class="sxs-lookup"><span data-stu-id="a169a-131">To test the resiliency of your application against failure of the primary node of your cache, reboot the **Master** node.</span></span> <span data-ttu-id="a169a-132">若要針對次要節點失敗測試應用程式復原功能，重新啟動 **從屬** 節點。</span><span class="sxs-lookup"><span data-stu-id="a169a-132">To test the resiliency of your application against failure of the secondary node, reboot the **Slave** node.</span></span> <span data-ttu-id="a169a-133">若要針對整體快取失敗測試應用程式復原功能，重新啟動 **這兩個** 節點。</span><span class="sxs-lookup"><span data-stu-id="a169a-133">To test the resiliency of your application against total failure of the cache, reboot **Both** nodes.</span></span>

### <a name="can-i-reboot-the-cache-to-clear-client-connections"></a><span data-ttu-id="a169a-134">我可以重新啟動快取來清除用戶端連線嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-134">Can I reboot the cache to clear client connections?</span></span>
<span data-ttu-id="a169a-135">是，如果您重新啟動快取，即會清除所有用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="a169a-135">Yes, if you reboot the cache all client connections are cleared.</span></span> <span data-ttu-id="a169a-136">若發生所有用戶端連線都已用盡的情況 (因為發生邏輯錯誤或用戶端應用程式中發生錯誤)，重新啟動非常實用。</span><span class="sxs-lookup"><span data-stu-id="a169a-136">Rebooting can be useful in the case where all client connections are used up due to a logic error or a bug in the client application.</span></span> <span data-ttu-id="a169a-137">每個定價層對於各種不同大小都有不同的 [用戶端連線限制](cache-configure.md#default-redis-server-configuration) ，一旦觸達這些限制之後，就無法再接受任何用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="a169a-137">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for the various sizes, and once these limits are reached, no more client connections are accepted.</span></span> <span data-ttu-id="a169a-138">重新啟動快取提供一種方式來清除所有用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="a169a-138">Rebooting the cache provides a way to clear all client connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a169a-139">如果您重新啟動您的快取來清除用戶端連線，StackExchange.Redis 會在 Redis 節點回到線上後自動重新連線。</span><span class="sxs-lookup"><span data-stu-id="a169a-139">If you reboot your cache to clear client connections, StackExchange.Redis automatically reconnects once the Redis node is back online.</span></span> <span data-ttu-id="a169a-140">如果沒有解決潛在問題，用戶端連線仍可能被用盡。</span><span class="sxs-lookup"><span data-stu-id="a169a-140">If the underlying issue is not resolved, the client connections may continue to be used up.</span></span>
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a><span data-ttu-id="a169a-141">如果我重新啟動，將會遺失快取中的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-141">Will I lose data from my cache if I do a reboot?</span></span>
<span data-ttu-id="a169a-142">如果您重新啟動**主要**和**從屬**節點，快取中 (或者，如果您使用的是已啟用叢集的進階快取，則是在該分區中) 的所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="a169a-142">If you reboot both the **Master** and **Slave** nodes, all data in the cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span></span> <span data-ttu-id="a169a-143">如果您已設定[資料持續性](cache-how-to-premium-persistence.md)，則當快取恢復連線時，將會還原最近一次備份，但在此備份後發生的任何快取寫入將會遺失。</span><span class="sxs-lookup"><span data-stu-id="a169a-143">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup will be restored when the cache comes back online, but any cache writes that have occurred after the backup was made are lost.</span></span>

<span data-ttu-id="a169a-144">如果您只重新啟動這其中一個節點，通常不會遺失資料，但仍有可能發生。</span><span class="sxs-lookup"><span data-stu-id="a169a-144">If you reboot just one of the nodes, data is not typically lost, but it still may be.</span></span> <span data-ttu-id="a169a-145">例如，如果重新啟動主要節點且快取寫入正在進行中，則來自快取寫入的資料即會遺失。</span><span class="sxs-lookup"><span data-stu-id="a169a-145">For example if the master node is rebooted and a cache write is in progress, the data from the cache write is lost.</span></span> <span data-ttu-id="a169a-146">如果您重新啟動一個節點，而另一個節點剛好同時因為失敗而當機，也有可能造成資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a169a-146">Another scenario for data loss would be if you reboot one node and the other node happens to go down due to a failure at the same time.</span></span> <span data-ttu-id="a169a-147">如需深入了解資料遺失的可能原因，請參閱[我在 Redis 中的資料怎麼了？](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span><span class="sxs-lookup"><span data-stu-id="a169a-147">For more information about possible causes for data loss, see [What happened to my data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span></span>

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="a169a-148">我可以使用 PowerShell、CLI 或其他管理工具重新啟動我的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-148">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="a169a-149">是，如需 PowerShell 指示，請參閱 [重新啟動 Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="a169a-149">Yes, for PowerShell instructions see [To reboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span></span>

### <a name="what-pricing-tiers-can-use-the-reboot-functionality"></a><span data-ttu-id="a169a-150">哪些定價層可以使用重新啟動功能？</span><span class="sxs-lookup"><span data-stu-id="a169a-150">What pricing tiers can use the reboot functionality?</span></span>
<span data-ttu-id="a169a-151">重新啟動適用於所有定價層。</span><span class="sxs-lookup"><span data-stu-id="a169a-151">Reboot is available for all pricing tiers.</span></span>

## <a name="schedule-updates"></a><span data-ttu-id="a169a-152">更新排程</span><span class="sxs-lookup"><span data-stu-id="a169a-152">Schedule updates</span></span>
<span data-ttu-id="a169a-153">[排程更新]  刀鋒視窗可讓您指定適用於進階層快取的維護期間。</span><span class="sxs-lookup"><span data-stu-id="a169a-153">The **Schedule updates** blade allows you to designate a maintenance window for your Premium tier cache.</span></span> <span data-ttu-id="a169a-154">若指定了維護期間，即會在此期間進行任何 Redis 伺服器更新。</span><span class="sxs-lookup"><span data-stu-id="a169a-154">When the maintenance window is specified, any Redis server updates are made during this window.</span></span> 

> [!NOTE] 
> <span data-ttu-id="a169a-155">維護期間僅適用於 Redis 伺服器更新，不適用於任何 Azure 更新，或是在裝載快取的 VM 上更新作業系統。</span><span class="sxs-lookup"><span data-stu-id="a169a-155">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![排程更新](./media/cache-administration/redis-schedule-updates.png)

<span data-ttu-id="a169a-157">若要指定維護期間，請檢查所需的天數，並指定每一天的維護期間開始小時，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a169a-157">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="a169a-158">請注意，維護期間時間是 UTC。</span><span class="sxs-lookup"><span data-stu-id="a169a-158">Note that the maintenance window time is in UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="a169a-159">更新的預設維護期間是 5 小時。</span><span class="sxs-lookup"><span data-stu-id="a169a-159">The default maintenance window for updates is five hours.</span></span> <span data-ttu-id="a169a-160">這個值不可以從 Azure 入口網站設定，不過您可以在 PowerShell 中使用 [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) Cmdlet 的 `MaintenanceWindow` 參數加以設定。</span><span class="sxs-lookup"><span data-stu-id="a169a-160">This value is not configurable from the Azure portal, but you can configure it in PowerShell using the `MaintenanceWindow` parameter of the [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet.</span></span> <span data-ttu-id="a169a-161">如需詳細資訊，請參閱[我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span><span class="sxs-lookup"><span data-stu-id="a169a-161">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span></span>
> 
> 

## <a name="schedule-updates-faq"></a><span data-ttu-id="a169a-162">排程更新常見問題集</span><span class="sxs-lookup"><span data-stu-id="a169a-162">Schedule updates FAQ</span></span>
* [<span data-ttu-id="a169a-163">如果我未使用排程更新功能，更新會在何時發生？</span><span class="sxs-lookup"><span data-stu-id="a169a-163">When do updates occur if I don't use the schedule updates feature?</span></span>](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [<span data-ttu-id="a169a-164">在排程維護期間，會進行何種類型的更新？</span><span class="sxs-lookup"><span data-stu-id="a169a-164">What type of updates are made during the scheduled maintenance window?</span></span>](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [<span data-ttu-id="a169a-165">我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-165">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span></span>](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="a169a-166">哪些定價層可以使用排程更新功能？</span><span class="sxs-lookup"><span data-stu-id="a169a-166">What pricing tiers can use the schedule updates functionality?</span></span>](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature"></a><span data-ttu-id="a169a-167">如果我未使用排程更新功能，更新會在何時發生？</span><span class="sxs-lookup"><span data-stu-id="a169a-167">When do updates occur if I don't use the schedule updates feature?</span></span>
<span data-ttu-id="a169a-168">如果您未指定維護期間，隨時都可進行更新。</span><span class="sxs-lookup"><span data-stu-id="a169a-168">If you don't specify a maintenance window, updates can be made at any time.</span></span>

### <a name="what-type-of-updates-are-made-during-the-scheduled-maintenance-window"></a><span data-ttu-id="a169a-169">在排程維護期間，會進行何種類型的更新？</span><span class="sxs-lookup"><span data-stu-id="a169a-169">What type of updates are made during the scheduled maintenance window?</span></span>
<span data-ttu-id="a169a-170">在排程維護期間，只會進行 Redis 伺服器更新。</span><span class="sxs-lookup"><span data-stu-id="a169a-170">Only Redis server updates are made during the scheduled maintenance window.</span></span> <span data-ttu-id="a169a-171">維護期間不適用於 Azure 更新或 VM 作業系統的更新。</span><span class="sxs-lookup"><span data-stu-id="a169a-171">The maintenance window does not apply to Azure updates or updates to the VM operating system.</span></span>

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="a169a-172">我可以使用 PowerShell、CLI 或其他管理工具管理排程更新嗎？</span><span class="sxs-lookup"><span data-stu-id="a169a-172">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="a169a-173">是，您可以使用下列 PowerShell Cmdlet 管理排程更新：</span><span class="sxs-lookup"><span data-stu-id="a169a-173">Yes, you can manage your scheduled updates using the following PowerShell cmdlets:</span></span>

* [<span data-ttu-id="a169a-174">Get-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="a169a-174">Get-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [<span data-ttu-id="a169a-175">New-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="a169a-175">New-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [<span data-ttu-id="a169a-176">New-AzureRmRedisCacheScheduleEntry</span><span class="sxs-lookup"><span data-stu-id="a169a-176">New-AzureRmRedisCacheScheduleEntry</span></span>](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [<span data-ttu-id="a169a-177">Remove-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="a169a-177">Remove-AzureRmRedisCachePatchSchedule</span></span>](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-the-schedule-updates-functionality"></a><span data-ttu-id="a169a-178">哪些定價層可以使用排程更新功能？</span><span class="sxs-lookup"><span data-stu-id="a169a-178">What pricing tiers can use the schedule updates functionality?</span></span>
<span data-ttu-id="a169a-179">只有進階定價層提供**排程更新**功能。</span><span class="sxs-lookup"><span data-stu-id="a169a-179">The **Schedule updates** feature is only available in the premium pricing tier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a169a-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a169a-180">Next steps</span></span>
* <span data-ttu-id="a169a-181">瀏覽 [Azure Redis 快取進階層](cache-premium-tier-intro.md) 功能。</span><span class="sxs-lookup"><span data-stu-id="a169a-181">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span></span>

