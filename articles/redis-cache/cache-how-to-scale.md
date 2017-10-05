---
title: "如何調整 Azure Redis 快取 | Microsoft Docs"
description: "了解如何調整 Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="de080-103">如何調整 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="de080-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="de080-104">Azure Redis 快取都有不同的快取提供項目，以提供選擇快取大小和功能的彈性。</span><span class="sxs-lookup"><span data-stu-id="de080-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="de080-105">建立快取之後，如果您應用程式的需求改變，您可以調整快取的大小和定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="de080-106">本文說明如何在 Azure 入口網站中使用 Azure PowerShell 和 Azure CLI 之類的工具來調整快取。</span><span class="sxs-lookup"><span data-stu-id="de080-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="de080-107">調整時機</span><span class="sxs-lookup"><span data-stu-id="de080-107">When to scale</span></span>
<span data-ttu-id="de080-108">您可以使用 Azure Redis 快取的[監視](cache-how-to-monitor.md)功能來監視快取的健康狀態和效能，以及協助判斷何時要調整快取。</span><span class="sxs-lookup"><span data-stu-id="de080-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="de080-109">您可以監視下列度量，以協助判斷是否需要調整。</span><span class="sxs-lookup"><span data-stu-id="de080-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="de080-110">Redis 伺服器負載</span><span class="sxs-lookup"><span data-stu-id="de080-110">Redis Server Load</span></span>
* <span data-ttu-id="de080-111">記憶體使用量</span><span class="sxs-lookup"><span data-stu-id="de080-111">Memory Usage</span></span>
* <span data-ttu-id="de080-112">網路頻寬</span><span class="sxs-lookup"><span data-stu-id="de080-112">Network Bandwidth</span></span>
* <span data-ttu-id="de080-113">CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="de080-113">CPU Usage</span></span>

<span data-ttu-id="de080-114">如果您判斷快取不再符合您應用程式的需求，則可以調整為適合您應用程式的較大或較小快取定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="de080-115">如需判斷要使用之快取定價層的詳細資訊，請參閱 [我應該使用哪些 Redis 快取提供項目和大小](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。</span><span class="sxs-lookup"><span data-stu-id="de080-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="de080-116">調整快取</span><span class="sxs-lookup"><span data-stu-id="de080-116">Scale a cache</span></span>
<span data-ttu-id="de080-117">若要調整快取，在 [Azure 入口網站](https://portal.azure.com)中[瀏覽至快取](cache-configure.md#configure-redis-cache-settings)，然後按一下 **[資源]** 功能表中的 **[調整]**。</span><span class="sxs-lookup"><span data-stu-id="de080-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![調整](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="de080-119">從 [選取定價層] 刀鋒視窗中選取想要的定價層，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="de080-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![定價層 ][redis-cache-pricing-tier-blade]


<span data-ttu-id="de080-121">您可以調整具有下列限制的不同定價層：</span><span class="sxs-lookup"><span data-stu-id="de080-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="de080-122">您無法從較高的定價層調整至較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="de080-123">您無法從**進階**快取向下調整至**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="de080-124">您無法從**標準**快取向下調整到**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="de080-125">您可以從**基本**快取調整到**標準**快取，但您無法同時變更大小。</span><span class="sxs-lookup"><span data-stu-id="de080-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="de080-126">如果您需要不同的大小，您可以進行後續調整作業，調整到您需要的大小。</span><span class="sxs-lookup"><span data-stu-id="de080-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="de080-127">您無法直接從**基本**快取調整至**進階**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="de080-128">您必須在單一調整作業中從**基本**調整至**標準**，然後在後續的調整作業中從**標準**調整至**進階**。</span><span class="sxs-lookup"><span data-stu-id="de080-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="de080-129">您無法從較大的大小向下調整至 **C0 (250 MB)** 的大小。</span><span class="sxs-lookup"><span data-stu-id="de080-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="de080-130">快取調整為新的定價層時，[正在調整] 狀態會顯示在 [Redis 快取] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="de080-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![調整大小][redis-cache-scaling]

<span data-ttu-id="de080-132">調整完成時，狀態會從 [正在調整] 變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="de080-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="de080-133">如何自動化調整作業</span><span class="sxs-lookup"><span data-stu-id="de080-133">How to automate a scaling operation</span></span>
<span data-ttu-id="de080-134">除了在 Azure 入口網站中調整快取執行個體之外，您還可以使用 PowerShell Cmdlet、Azure CLI 以及使用 Microsoft Azure 管理庫 (MAML) 進行調整。</span><span class="sxs-lookup"><span data-stu-id="de080-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="de080-135">使用 PowerShell 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="de080-136">使用 Azure CLI 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="de080-137">使用 MAML 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="de080-138">使用 PowerShell 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-138">Scale using PowerShell</span></span>
<span data-ttu-id="de080-139">修改 `Size`、`Sku`，或 `ShardCount` 屬性時，您可以使用 [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) Cmdlet 搭配 PowerShell 來調整您的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="de080-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="de080-140">下列範例示範如何將名為 `myCache` 的快取調整為 2.5 GB 快取。</span><span class="sxs-lookup"><span data-stu-id="de080-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="de080-141">如需有關如何使用 PowerShell 進行調整的詳細資訊，請參閱 [使用 Powershell 調整 Redis 快取](cache-howto-manage-redis-cache-powershell.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="de080-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="de080-142">使用 Azure CLI 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-142">Scale using Azure CLI</span></span>
<span data-ttu-id="de080-143">若要使用 Azure CLI 調整您的 Azure Redis 快取執行個體，請呼叫 `azure rediscache set` 命令並傳入所需的設定變更，其中包括新的大小、SKU 或叢集大小，視所需的調整作業而定。</span><span class="sxs-lookup"><span data-stu-id="de080-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="de080-144">如需有關如何使用 Azure CLI 進行調整的詳細資訊，請參閱 [變更現有 Redis 快取的設定](cache-manage-cli.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="de080-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="de080-145">使用 MAML 進行調整</span><span class="sxs-lookup"><span data-stu-id="de080-145">Scale using MAML</span></span>
<span data-ttu-id="de080-146">若要使用 [Microsoft Azure 管理庫 (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/) 來調整您的 Azure Redis 快取執行個體，請呼叫 `IRedisOperations.CreateOrUpdate` 方法並傳入 `RedisProperties.SKU.Capacity` 的新大小。</span><span class="sxs-lookup"><span data-stu-id="de080-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="de080-147">如需詳細資訊，請參閱 [使用 MAML 管理 Redis 快取](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) 範例。</span><span class="sxs-lookup"><span data-stu-id="de080-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="de080-148">調整常見問題集</span><span class="sxs-lookup"><span data-stu-id="de080-148">Scaling FAQ</span></span>
<span data-ttu-id="de080-149">下列清單包含 Azure Redis 快取調整常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="de080-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="de080-150">可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？</span><span class="sxs-lookup"><span data-stu-id="de080-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="de080-151">調整之後，是否必須變更我的快取名稱或存取金鑰？</span><span class="sxs-lookup"><span data-stu-id="de080-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="de080-152">調整運作方式如何？</span><span class="sxs-lookup"><span data-stu-id="de080-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="de080-153">我是否會在調整期間遺失快取中的資料？</span><span class="sxs-lookup"><span data-stu-id="de080-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="de080-154">我的自訂資料庫設定在調整期間會受到影響嗎？</span><span class="sxs-lookup"><span data-stu-id="de080-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="de080-155">是否可以在調整期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="de080-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="de080-156">不支援的作業</span><span class="sxs-lookup"><span data-stu-id="de080-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="de080-157">調整需要多長的時間？</span><span class="sxs-lookup"><span data-stu-id="de080-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="de080-158">如何分辨調整何時完成？</span><span class="sxs-lookup"><span data-stu-id="de080-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="de080-159">可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？</span><span class="sxs-lookup"><span data-stu-id="de080-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="de080-160">您無法從**進階**快取向下調整至**基本**或**標準**定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="de080-161">您可以將一個 **進階** 快取定價層調整為另一個定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="de080-162">您無法直接從**基本**快取調整至**進階**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="de080-163">您必須先在單一調整作業中從**基本**調整至**標準**，然後在後續的調整作業中從**標準**調整至**進階**。</span><span class="sxs-lookup"><span data-stu-id="de080-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="de080-164">如果在建立 **進階** 快取時已啟用叢集，您可以 [變更叢集大小](cache-how-to-premium-clustering.md#cluster-size)。</span><span class="sxs-lookup"><span data-stu-id="de080-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="de080-165">如果在建立快取時未啟用叢集，之後便無法設定叢集。</span><span class="sxs-lookup"><span data-stu-id="de080-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="de080-166">如需詳細資訊，請參閱 [如何設定進階 Azure Redis 快取的叢集](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="de080-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="de080-167">調整之後，是否必須變更我的快取名稱或存取金鑰？</span><span class="sxs-lookup"><span data-stu-id="de080-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="de080-168">否，在調整作業期間，您的快取名稱和金鑰不會變更。</span><span class="sxs-lookup"><span data-stu-id="de080-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="de080-169">調整運作方式如何？</span><span class="sxs-lookup"><span data-stu-id="de080-169">How does scaling work?</span></span>
* <span data-ttu-id="de080-170">**基本** 快取在調整為不同的大小時會關閉，並會使用新的大小佈建新的快取。</span><span class="sxs-lookup"><span data-stu-id="de080-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="de080-171">在此期間，快取無法使用，而且快取中的所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="de080-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="de080-172">**基本**快取在調整為**標準**快取時，會佈建複本快取，且會從主要快取將資料複製到複本快取。</span><span class="sxs-lookup"><span data-stu-id="de080-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="de080-173">調整程序期間仍可使用快取。</span><span class="sxs-lookup"><span data-stu-id="de080-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="de080-174">當**標準**快取調整為不同的大小或**進階**快取時，會關閉其中一個複本，並會將其重新佈建為新的大小並傳輸資料，然後另一個複本會先執行容錯移轉，再進行重新佈建，這與其中一個快取節點失敗期間發生的程序類似。</span><span class="sxs-lookup"><span data-stu-id="de080-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="de080-175">我是否會在調整期間遺失快取中的資料？</span><span class="sxs-lookup"><span data-stu-id="de080-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="de080-176">**基本** 快取調整為新的大小時，會遺失所有資料，且無法在調整作業期間使用快取。</span><span class="sxs-lookup"><span data-stu-id="de080-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="de080-177">**基本**快取調整為**標準**快取時，通常會保留快取中的資料。</span><span class="sxs-lookup"><span data-stu-id="de080-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="de080-178">當**標準**快取調整為較大的大小或層，或者**進階**快取調整為較大的大小時，通常會保留所有資料。</span><span class="sxs-lookup"><span data-stu-id="de080-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="de080-179">當**標準**或**進階**快取向下調整為較小大小時，根據調整時快取中與新大小相關的資料量，資料可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="de080-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="de080-180">如果縮小時遺失資料，則會使用 [allkeys-lru](http://redis.io/topics/lru-cache) 收回原則來收回金鑰。</span><span class="sxs-lookup"><span data-stu-id="de080-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="de080-181">我的自訂資料庫設定在調整期間會受到影響嗎？</span><span class="sxs-lookup"><span data-stu-id="de080-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="de080-182">某些定價層具有不同的[資料庫限制](cache-configure.md#databases)，因此，在向下調整時，如果您在快取建立期間為 `databases` 設定設定了自訂值，則有一些考量。</span><span class="sxs-lookup"><span data-stu-id="de080-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="de080-183">調整為較現有階層具有較低 `databases` 限制的定價層時：</span><span class="sxs-lookup"><span data-stu-id="de080-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="de080-184">如果您使用預設數字 `databases`，即所有定價層為 16，則不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="de080-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="de080-185">如果您要使用的自訂數字 `databases`，落在您要調整之階層限制範圍內，則會保留此 `databases` 設定，並且不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="de080-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="de080-186">如果您要使用的自訂數字 `databases`，超出新階層的限制，則會將 `databases` 設定降低至新階層的限制，而且在已移除的資料庫中的所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="de080-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="de080-187">調整為較現有階層具有具有相同或更高 `databases` 限制的定價層時，會保留您的 `databases` 設定，而且不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="de080-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="de080-188">請注意，標準和進階快取有 99.9% SLA 的可用性時，則資料遺失沒有 SLA。</span><span class="sxs-lookup"><span data-stu-id="de080-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="de080-189">是否可以在調整期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="de080-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="de080-190">**標準**與**進階**快取在調整作業期間會保持可用。</span><span class="sxs-lookup"><span data-stu-id="de080-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="de080-191">**基本**快取在調整為不同大小的作業期間為離線，但是從**基本**調整為**標準**時仍可使用快取。</span><span class="sxs-lookup"><span data-stu-id="de080-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="de080-192">不支援的作業</span><span class="sxs-lookup"><span data-stu-id="de080-192">Operations that are not supported</span></span>
* <span data-ttu-id="de080-193">您無法從較高的定價層調整至較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="de080-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="de080-194">您無法從**進階**快取向下調整至**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="de080-195">您無法從**標準**快取向下調整到**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="de080-196">您可以從**基本**快取調整到**標準**快取，但您無法同時變更大小。</span><span class="sxs-lookup"><span data-stu-id="de080-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="de080-197">如果您需要不同的大小，您可以進行後續調整作業，調整到您需要的大小。</span><span class="sxs-lookup"><span data-stu-id="de080-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="de080-198">您無法直接從**基本**快取調整至**進階**快取。</span><span class="sxs-lookup"><span data-stu-id="de080-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="de080-199">您必須先在單一調整作業中從**基本**調整至**標準**，然後在後續的調整作業中從**標準**調整至**進階**。</span><span class="sxs-lookup"><span data-stu-id="de080-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="de080-200">您無法從較大的大小向下調整至 **C0 (250 MB)** 的大小。</span><span class="sxs-lookup"><span data-stu-id="de080-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="de080-201">如果調整作業失敗，服務會嘗試還原作業，而且快取會還原成原始大小。</span><span class="sxs-lookup"><span data-stu-id="de080-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="de080-202">調整需要多長的時間？</span><span class="sxs-lookup"><span data-stu-id="de080-202">How long does scaling take?</span></span>
<span data-ttu-id="de080-203">根據快取中的資料量，調整大約需要 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="de080-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="de080-204">如何分辨調整何時完成？</span><span class="sxs-lookup"><span data-stu-id="de080-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="de080-205">在 Azure 入口網站中，您可以看到調整作業進行中。</span><span class="sxs-lookup"><span data-stu-id="de080-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="de080-206">調整完成時，快取的狀態會變更為 [執行中] 。</span><span class="sxs-lookup"><span data-stu-id="de080-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



