---
title: "aaaHow tooScale Azure Redis 快取 |Microsoft 文件"
description: "了解如何 tooscale Azure Redis 快取執行個體"
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
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="dd2f4-103">如何 tooScale Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="dd2f4-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="dd2f4-104">Azure Redis 快取都有不同的快取提供項目，提供有彈性地 hello 選擇的快取大小和功能。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="dd2f4-105">建立快取之後，您可以調整 hello 大小和 hello 定價層的 hello 快取，應用程式的 hello 需求變更時。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="dd2f4-106">本文章將示範如何 tooscale hello Azure 入口網站以及使用您的快取工具，例如 Azure PowerShell 和 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="dd2f4-107">當 tooscale</span><span class="sxs-lookup"><span data-stu-id="dd2f4-107">When tooscale</span></span>
<span data-ttu-id="dd2f4-108">您可以使用 hello[監視](cache-how-to-monitor.md)功能 Azure Redis 快取 toomonitor hello 健全狀況和效能的快取，以及協助您判斷何時 tooscale hello 快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="dd2f4-109">您可以監視 hello 下列度量 toohelp 判斷您是否需要 tooscale。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="dd2f4-110">Redis 伺服器負載</span><span class="sxs-lookup"><span data-stu-id="dd2f4-110">Redis Server Load</span></span>
* <span data-ttu-id="dd2f4-111">記憶體使用量</span><span class="sxs-lookup"><span data-stu-id="dd2f4-111">Memory Usage</span></span>
* <span data-ttu-id="dd2f4-112">網路頻寬</span><span class="sxs-lookup"><span data-stu-id="dd2f4-112">Network Bandwidth</span></span>
* <span data-ttu-id="dd2f4-113">CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="dd2f4-113">CPU Usage</span></span>

<span data-ttu-id="dd2f4-114">如果您判斷您的快取不再符合您的應用程式需求，您可以調整 tooa 放大或縮小快取定價層，最適合您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="dd2f4-115">如需判斷這些快取定價層 toouse 的詳細資訊，請參閱[何種 Redis 快取提供項目和大小應該使用](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="dd2f4-116">調整快取</span><span class="sxs-lookup"><span data-stu-id="dd2f4-116">Scale a cache</span></span>
<span data-ttu-id="dd2f4-117">tooscale 快取、[瀏覽 toohello 快取](cache-configure.md#configure-redis-cache-settings)在 hello [Azure 入口網站](https://portal.azure.com)按一下**標尺**從 hello**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![調整](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="dd2f4-119">選取 hello 預期定價層從 hello**選取定價層**刀鋒視窗，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![定價層 ][redis-cache-pricing-tier-blade]


<span data-ttu-id="dd2f4-121">您可以調整 tooa 不同定價層與 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="dd2f4-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="dd2f4-122">您無法調整從較高定價層 tooa 較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="dd2f4-123">您無法從延展**Premium**快取下 tooa**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="dd2f4-124">您無法從延展**標準**快取下 tooa**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="dd2f4-125">您可以調整從**基本**快取 tooa**標準**快取，但是您無法變更在 hello hello 大小相同的時間。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="dd2f4-126">如果您需要不同的大小，您可以執行後續的縮放作業 toohello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="dd2f4-127">您無法從延展**基本**快取直接 tooa **Premium**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="dd2f4-128">您必須從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續的縮放比例作業。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="dd2f4-129">您無法從較大的向下 toohello 延展**C0 250 MB**大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="dd2f4-130">雖然 hello 快取調整新定價層，toohello**調整**狀態會顯示在 hello **Redis 快取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![調整大小][redis-cache-scaling]

<span data-ttu-id="dd2f4-132">調整完畢後，請從 hello 狀態變更**調整**太**執行**。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="dd2f4-133">如何 tooautomate 縮放作業</span><span class="sxs-lookup"><span data-stu-id="dd2f4-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="dd2f4-134">在加法 tooscaling 中的快取執行個體 hello Azure 入口網站，您可以調整使用 PowerShell cmdlet，Azure CLI，並使用 hello Microsoft Azure 管理程式庫 (MAML)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="dd2f4-135">使用 PowerShell 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="dd2f4-136">使用 Azure CLI 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="dd2f4-137">使用 MAML 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="dd2f4-138">使用 PowerShell 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-138">Scale using PowerShell</span></span>
<span data-ttu-id="dd2f4-139">您可以藉由使用 hello 調整您的 Azure Redis 快取執行個體，使用 PowerShell[組 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet 時 hello `Size`， `Sku`，或`ShardCount`修改屬性。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="dd2f4-140">hello 下列範例示範如何 tooscale 快取命名`myCache`tooa 2.5 GB 的快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="dd2f4-141">如需有關使用 PowerShell 縮放比例的詳細資訊，請參閱[tooscale Redis 快取使用 Powershell](cache-howto-manage-redis-cache-powershell.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="dd2f4-142">使用 Azure CLI 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-142">Scale using Azure CLI</span></span>
<span data-ttu-id="dd2f4-143">tooscale 您的 Azure Redis 快取執行個體，使用 Azure CLI 呼叫 hello`azure rediscache set`命令，並傳入 hello 預期組態變更，包括新的大小、 sku 或根據 hello 的叢集大小所需之縮放作業。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="dd2f4-144">如需有關如何使用 Azure CLI 進行調整的詳細資訊，請參閱 [變更現有 Redis 快取的設定](cache-manage-cli.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="dd2f4-145">使用 MAML 進行調整</span><span class="sxs-lookup"><span data-stu-id="dd2f4-145">Scale using MAML</span></span>
<span data-ttu-id="dd2f4-146">tooscale 您的 Azure Redis 快取執行個體使用 hello [Microsoft Azure 管理程式庫 (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/)，呼叫 hello`IRedisOperations.CreateOrUpdate`方法並傳入 hello hello 新大小`RedisProperties.SKU.Capacity`。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="dd2f4-147">如需詳細資訊，請參閱 hello[管理 Redis 快取使用 MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML)範例。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="dd2f4-148">調整常見問題集</span><span class="sxs-lookup"><span data-stu-id="dd2f4-148">Scaling FAQ</span></span>
<span data-ttu-id="dd2f4-149">hello 下列清單包含 Azure Redis 快取縮放的相關常見問題的解答 toocommonly。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="dd2f4-150">可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="dd2f4-151">縮放之後，我必須 toochange 快取名稱或存取金鑰嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="dd2f4-152">調整運作方式如何？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="dd2f4-153">我是否會在調整期間遺失快取中的資料？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="dd2f4-154">我的自訂資料庫設定在調整期間會受到影響嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="dd2f4-155">是否可以在調整期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="dd2f4-156">不支援的作業</span><span class="sxs-lookup"><span data-stu-id="dd2f4-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="dd2f4-157">調整需要多長的時間？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="dd2f4-158">如何分辨調整何時完成？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="dd2f4-159">可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="dd2f4-160">您無法從延展**Premium**快取下 tooa**基本**或**標準**定價層。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="dd2f4-161">您可以從其中一個調整**Premium**定價層 tooanother 快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="dd2f4-162">您無法從延展**基本**快取直接 tooa **Premium**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="dd2f4-163">您必須先從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="dd2f4-164">如果您啟用叢集建立時您**Premium**快取中，您可以[變更 hello 叢集大小](cache-how-to-premium-clustering.md#cluster-size)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="dd2f4-165">如果在建立快取時未啟用叢集，之後便無法設定叢集。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="dd2f4-166">如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="dd2f4-167">縮放之後，我必須 toochange 快取名稱或存取金鑰嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="dd2f4-168">否，在調整作業期間，您的快取名稱和金鑰不會變更。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="dd2f4-169">調整運作方式如何？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-169">How does scaling work?</span></span>
* <span data-ttu-id="dd2f4-170">當**基本**快取調整 tooa 不同的大小，它會關閉，而且新的快取已佈建使用 hello 新大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="dd2f4-171">在此期間，hello 快取無法使用且 hello 快取中的所有資料都都會遺失。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="dd2f4-172">當**基本**快取是縮放的 tooa**標準**快取中，複本快取已佈建，且從 hello 主要快取 toohello 複本快取 hello 資料複製。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="dd2f4-173">hello 快取 hello 調整處理程序期間會保持可用。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="dd2f4-174">當**標準**快取是縮放的 tooa 不同大小或 tooa **Premium**快取，其中一個 hello 複本會關閉並重新佈建 toohello 新大小和 hello 透過傳送資料，然後按一下 其他 hello複本執行容錯移轉之前重新佈建、 在其中一個 hello 快取節點失敗時，就會發生類似 toohello 程序。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="dd2f4-175">我是否會在調整期間遺失快取中的資料？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="dd2f4-176">當**基本**快取是縮放的 tooa 新大小，所有資料都會遺失而且 hello 快取期間無法使用 hello 調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="dd2f4-177">當**基本**快取是縮放的 tooa**標準**快取，hello hello 快取中的資料時通常會保留。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="dd2f4-178">當**標準**快取是縮放的 tooa 較大的大小或階層，或**Premium**快取調整通常會保留 tooa 較大的大小，所有資料。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="dd2f4-179">當調整**標準**或**Premium**向 tooa 較小，資料的快取可能會取決於多少資料可在 hello 快取中遺失時它就更能調整的相關 toohello 新大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="dd2f4-180">如果向下擴充時，會遺失資料，索引鍵中收回使用 hello [allkeys lru](http://redis.io/topics/lru-cache)收回原則。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="dd2f4-181">我的自訂資料庫設定在調整期間會受到影響嗎？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="dd2f4-182">某些定價層會具有不同[資料庫限制](cache-configure.md#databases)，因此有一些考量當向下調整如果您設定自訂值的 hello`databases`快取建立期間設定。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="dd2f4-183">當調整 tooa 定價層低於`databases`與 hello 目前層的限制：</span><span class="sxs-lookup"><span data-stu-id="dd2f4-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="dd2f4-184">如果您使用 hello 預設數目`databases`此為 16 個所有定價層，會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="dd2f4-185">如果您使用自訂的數字的`databases`落在 hello 限制範圍內則會擴充，hello 層 toowhich 這`databases`設定會保留下來，並不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="dd2f4-186">如果您使用自訂的數字的`databases`超過 hello hello 新階層，限制 hello`databases`設定值為 hello 新階層的降低的 toohello 限制，並且在 hello 移除資料庫中的所有資料都都會遺失。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="dd2f4-187">當調整 tooa 相同或更高定價層與 hello`databases`限制 hello 目前層高於您`databases`設定會保留下來，並不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="dd2f4-188">請注意，標準和進階快取有 99.9% SLA 的可用性時，則資料遺失沒有 SLA。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="dd2f4-189">是否可以在調整期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="dd2f4-190">**標準**和**Premium** hello 調整大小作業期間仍可快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="dd2f4-191">**基本**快取離線期間是調整作業 tooa 不同大小、 但仍可從擴充時**基本**太**標準**。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="dd2f4-192">不支援的作業</span><span class="sxs-lookup"><span data-stu-id="dd2f4-192">Operations that are not supported</span></span>
* <span data-ttu-id="dd2f4-193">您無法調整從較高定價層 tooa 較低的定價層。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="dd2f4-194">您無法從延展**Premium**快取下 tooa**標準**或**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="dd2f4-195">您無法從延展**標準**快取下 tooa**基本**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="dd2f4-196">您可以調整從**基本**快取 tooa**標準**快取，但是您無法變更在 hello hello 大小相同的時間。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="dd2f4-197">如果您需要不同的大小，您可以執行後續的縮放作業 toohello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="dd2f4-198">您無法從延展**基本**快取直接 tooa **Premium**快取。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="dd2f4-199">您必須先從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="dd2f4-200">您無法從較大的向下 toohello 延展**C0 250 MB**大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="dd2f4-201">如果縮放作業失敗，hello 服務將會嘗試 toorevert hello 作業和 hello 快取將會還原 toohello 原始大小。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="dd2f4-202">調整需要多長的時間？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-202">How long does scaling take?</span></span>
<span data-ttu-id="dd2f4-203">縮放比例會採用約 20 分鐘，視資料量是 hello 快取中。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="dd2f4-204">如何分辨調整何時完成？</span><span class="sxs-lookup"><span data-stu-id="dd2f4-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="dd2f4-205">在 hello Azure 入口網站中，您可以看到 hello 調整大小作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="dd2f4-206">調整完畢後，請 hello hello 快取變更狀態太**執行**。</span><span class="sxs-lookup"><span data-stu-id="dd2f4-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



