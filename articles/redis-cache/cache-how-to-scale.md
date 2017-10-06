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
# <a name="how-tooscale-azure-redis-cache"></a>如何 tooScale Azure Redis 快取
Azure Redis 快取都有不同的快取提供項目，提供有彈性地 hello 選擇的快取大小和功能。 建立快取之後，您可以調整 hello 大小和 hello 定價層的 hello 快取，應用程式的 hello 需求變更時。 本文章將示範如何 tooscale hello Azure 入口網站以及使用您的快取工具，例如 Azure PowerShell 和 Azure CLI。

## <a name="when-tooscale"></a>當 tooscale
您可以使用 hello[監視](cache-how-to-monitor.md)功能 Azure Redis 快取 toomonitor hello 健全狀況和效能的快取，以及協助您判斷何時 tooscale hello 快取。 

您可以監視 hello 下列度量 toohelp 判斷您是否需要 tooscale。

* Redis 伺服器負載
* 記憶體使用量
* 網路頻寬
* CPU 使用率

如果您判斷您的快取不再符合您的應用程式需求，您可以調整 tooa 放大或縮小快取定價層，最適合您的應用程式。 如需判斷這些快取定價層 toouse 的詳細資訊，請參閱[何種 Redis 快取提供項目和大小應該使用](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。

## <a name="scale-a-cache"></a>調整快取
tooscale 快取、[瀏覽 toohello 快取](cache-configure.md#configure-redis-cache-settings)在 hello [Azure 入口網站](https://portal.azure.com)按一下**標尺**從 hello**資源功能表**。

![調整](./media/cache-how-to-scale/redis-cache-scale-menu.png)

選取 hello 預期定價層從 hello**選取定價層**刀鋒視窗，然後按一下**選取**。

![定價層 ][redis-cache-pricing-tier-blade]


您可以調整 tooa 不同定價層與 hello 下列限制：

* 您無法調整從較高定價層 tooa 較低的定價層。
  * 您無法從延展**Premium**快取下 tooa**標準**或**基本**快取。
  * 您無法從延展**標準**快取下 tooa**基本**快取。
* 您可以調整從**基本**快取 tooa**標準**快取，但是您無法變更在 hello hello 大小相同的時間。 如果您需要不同的大小，您可以執行後續的縮放作業 toohello 預期大小。
* 您無法從延展**基本**快取直接 tooa **Premium**快取。 您必須從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續的縮放比例作業。
* 您無法從較大的向下 toohello 延展**C0 250 MB**大小。
 
雖然 hello 快取調整新定價層，toohello**調整**狀態會顯示在 hello **Redis 快取**刀鋒視窗。

![調整大小][redis-cache-scaling]

調整完畢後，請從 hello 狀態變更**調整**太**執行**。

## <a name="how-tooautomate-a-scaling-operation"></a>如何 tooautomate 縮放作業
在加法 tooscaling 中的快取執行個體 hello Azure 入口網站，您可以調整使用 PowerShell cmdlet，Azure CLI，並使用 hello Microsoft Azure 管理程式庫 (MAML)。 

* [使用 PowerShell 進行調整](#scale-using-powershell)
* [使用 Azure CLI 進行調整](#scale-using-azure-cli)
* [使用 MAML 進行調整](#scale-using-maml)

### <a name="scale-using-powershell"></a>使用 PowerShell 進行調整
您可以藉由使用 hello 調整您的 Azure Redis 快取執行個體，使用 PowerShell[組 AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet 時 hello `Size`， `Sku`，或`ShardCount`修改屬性。 hello 下列範例示範如何 tooscale 快取命名`myCache`tooa 2.5 GB 的快取。 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

如需有關使用 PowerShell 縮放比例的詳細資訊，請參閱[tooscale Redis 快取使用 Powershell](cache-howto-manage-redis-cache-powershell.md#scale)。

### <a name="scale-using-azure-cli"></a>使用 Azure CLI 進行調整
tooscale 您的 Azure Redis 快取執行個體，使用 Azure CLI 呼叫 hello`azure rediscache set`命令，並傳入 hello 預期組態變更，包括新的大小、 sku 或根據 hello 的叢集大小所需之縮放作業。

如需有關如何使用 Azure CLI 進行調整的詳細資訊，請參閱 [變更現有 Redis 快取的設定](cache-manage-cli.md#scale)。

### <a name="scale-using-maml"></a>使用 MAML 進行調整
tooscale 您的 Azure Redis 快取執行個體使用 hello [Microsoft Azure 管理程式庫 (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/)，呼叫 hello`IRedisOperations.CreateOrUpdate`方法並傳入 hello hello 新大小`RedisProperties.SKU.Capacity`。

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

如需詳細資訊，請參閱 hello[管理 Redis 快取使用 MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML)範例。

## <a name="scaling-faq"></a>調整常見問題集
hello 下列清單包含 Azure Redis 快取縮放的相關常見問題的解答 toocommonly。

* [可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？](#can-i-scale-to-from-or-within-a-premium-cache)
* [縮放之後，我必須 toochange 快取名稱或存取金鑰嗎？](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [調整運作方式如何？](#how-does-scaling-work)
* [我是否會在調整期間遺失快取中的資料？](#will-i-lose-data-from-my-cache-during-scaling)
* [我的自訂資料庫設定在調整期間會受到影響嗎？](#is-my-custom-databases-setting-affected-during-scaling)
* [是否可以在調整期間使用我的快取？](#will-my-cache-be-available-during-scaling)
* [不支援的作業](#operations-that-are-not-supported)
* [調整需要多長的時間？](#how-long-does-scaling-take)
* [如何分辨調整何時完成？](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>可以向上調整為 Premium 快取，或在其中調整、向下調整嗎？
* 您無法從延展**Premium**快取下 tooa**基本**或**標準**定價層。
* 您可以從其中一個調整**Premium**定價層 tooanother 快取。
* 您無法從延展**基本**快取直接 tooa **Premium**快取。 您必須先從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續調整大小作業。
* 如果您啟用叢集建立時您**Premium**快取中，您可以[變更 hello 叢集大小](cache-how-to-premium-clustering.md#cluster-size)。 如果在建立快取時未啟用叢集，之後便無法設定叢集。
  
  如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)。

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>縮放之後，我必須 toochange 快取名稱或存取金鑰嗎？
否，在調整作業期間，您的快取名稱和金鑰不會變更。

### <a name="how-does-scaling-work"></a>調整運作方式如何？
* 當**基本**快取調整 tooa 不同的大小，它會關閉，而且新的快取已佈建使用 hello 新大小。 在此期間，hello 快取無法使用且 hello 快取中的所有資料都都會遺失。
* 當**基本**快取是縮放的 tooa**標準**快取中，複本快取已佈建，且從 hello 主要快取 toohello 複本快取 hello 資料複製。 hello 快取 hello 調整處理程序期間會保持可用。
* 當**標準**快取是縮放的 tooa 不同大小或 tooa **Premium**快取，其中一個 hello 複本會關閉並重新佈建 toohello 新大小和 hello 透過傳送資料，然後按一下 其他 hello複本執行容錯移轉之前重新佈建、 在其中一個 hello 快取節點失敗時，就會發生類似 toohello 程序。

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>我是否會在調整期間遺失快取中的資料？
* 當**基本**快取是縮放的 tooa 新大小，所有資料都會遺失而且 hello 快取期間無法使用 hello 調整大小作業。
* 當**基本**快取是縮放的 tooa**標準**快取，hello hello 快取中的資料時通常會保留。
* 當**標準**快取是縮放的 tooa 較大的大小或階層，或**Premium**快取調整通常會保留 tooa 較大的大小，所有資料。 當調整**標準**或**Premium**向 tooa 較小，資料的快取可能會取決於多少資料可在 hello 快取中遺失時它就更能調整的相關 toohello 新大小。 如果向下擴充時，會遺失資料，索引鍵中收回使用 hello [allkeys lru](http://redis.io/topics/lru-cache)收回原則。 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>我的自訂資料庫設定在調整期間會受到影響嗎？
某些定價層會具有不同[資料庫限制](cache-configure.md#databases)，因此有一些考量當向下調整如果您設定自訂值的 hello`databases`快取建立期間設定。

* 當調整 tooa 定價層低於`databases`與 hello 目前層的限制：
  * 如果您使用 hello 預設數目`databases`此為 16 個所有定價層，會遺失任何資料。
  * 如果您使用自訂的數字的`databases`落在 hello 限制範圍內則會擴充，hello 層 toowhich 這`databases`設定會保留下來，並不會遺失資料。
  * 如果您使用自訂的數字的`databases`超過 hello hello 新階層，限制 hello`databases`設定值為 hello 新階層的降低的 toohello 限制，並且在 hello 移除資料庫中的所有資料都都會遺失。
* 當調整 tooa 相同或更高定價層與 hello`databases`限制 hello 目前層高於您`databases`設定會保留下來，並不會遺失資料。

請注意，標準和進階快取有 99.9% SLA 的可用性時，則資料遺失沒有 SLA。

### <a name="will-my-cache-be-available-during-scaling"></a>是否可以在調整期間使用我的快取？
* **標準**和**Premium** hello 調整大小作業期間仍可快取。
* **基本**快取離線期間是調整作業 tooa 不同大小、 但仍可從擴充時**基本**太**標準**。

### <a name="operations-that-are-not-supported"></a>不支援的作業
* 您無法調整從較高定價層 tooa 較低的定價層。
  * 您無法從延展**Premium**快取下 tooa**標準**或**基本**快取。
  * 您無法從延展**標準**快取下 tooa**基本**快取。
* 您可以調整從**基本**快取 tooa**標準**快取，但是您無法變更在 hello hello 大小相同的時間。 如果您需要不同的大小，您可以執行後續的縮放作業 toohello 預期大小。
* 您無法從延展**基本**快取直接 tooa **Premium**快取。 您必須先從延展**基本**太**標準**一個縮放作業，然後從**標準**太**Premium**中後續調整大小作業。
* 您無法從較大的向下 toohello 延展**C0 250 MB**大小。

如果縮放作業失敗，hello 服務將會嘗試 toorevert hello 作業和 hello 快取將會還原 toohello 原始大小。

### <a name="how-long-does-scaling-take"></a>調整需要多長的時間？
縮放比例會採用約 20 分鐘，視資料量是 hello 快取中。

### <a name="how-can-i-tell-when-scaling-is-complete"></a>如何分辨調整何時完成？
在 hello Azure 入口網站中，您可以看到 hello 調整大小作業正在進行中。 調整完畢後，請 hello hello 快取變更狀態太**執行**。

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



