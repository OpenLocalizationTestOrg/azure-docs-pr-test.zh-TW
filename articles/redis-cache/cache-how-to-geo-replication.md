---
title: "如何設定 Azure Redis 快取的異地複寫 | Microsoft Docs"
description: "了解如何跨地理區域複寫您的 Azure Redis 快取執行個體。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: 71b0d4add7e642487f6d67cda692c500ee78b0e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-geo-replication-for-azure-redis-cache"></a><span data-ttu-id="305bf-103">如何設定 Azure Redis 快取的異地複寫</span><span class="sxs-lookup"><span data-stu-id="305bf-103">How to configure Geo-replication for Azure Redis Cache</span></span>

<span data-ttu-id="305bf-104">異地複寫提供一個機制，可供連結兩個高階層 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="305bf-104">Geo-replication provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="305bf-105">其中一個快取被指定為主要連結快取，而另一個則為次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-105">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="305bf-106">次要連結快取會變成唯讀，而寫入主要快取的資料會複寫至次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-106">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="305bf-107">這項功能可用來跨 Azure 區域複寫快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-107">This functionality can be used to replicate a cache across Azure regions.</span></span> <span data-ttu-id="305bf-108">本文提供的指南說明如何設定高階層 Azure Redis 快取執行個體的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-108">This article provides a guide to configuring Geo-replication for your Premium tier Azure Redis Cache instances.</span></span>

## <a name="geo-replication-prerequisites"></a><span data-ttu-id="305bf-109">異地複寫的必要條件</span><span class="sxs-lookup"><span data-stu-id="305bf-109">Geo-replication prerequisites</span></span>

<span data-ttu-id="305bf-110">若要設定兩個快取之間的異地複寫，必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="305bf-110">To configure Geo-replication between two caches, the following prerequisites must be met:</span></span>

- <span data-ttu-id="305bf-111">這兩個快取必須是[高階層](cache-premium-tier-intro.md)快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-111">Both caches must be [Premium tier](cache-premium-tier-intro.md) caches.</span></span>
- <span data-ttu-id="305bf-112">這兩個快取必須位於相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="305bf-112">Both caches must be in the same Azure subscription.</span></span>
- <span data-ttu-id="305bf-113">次要連結快取必須為相同的定價層，或超過主要連結快取的定價層。</span><span class="sxs-lookup"><span data-stu-id="305bf-113">The secondary linked cache must be either the same pricing tier or a larger pricing tier than the primary linked cache.</span></span>
- <span data-ttu-id="305bf-114">如果主要連結快取已啟用叢集，次要連結快取就必須啟用具有相同分區數目的叢集作為主要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-114">If the primary linked cache has clustering enabled, the secondary linked cache must have clustering enabled with the same number of shards as the primary linked cache.</span></span>
- <span data-ttu-id="305bf-115">必須建立兩個快取並同時處於執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="305bf-115">Both caches must be created and in a running state.</span></span>
- <span data-ttu-id="305bf-116">任何一個快取上皆不能啟用持續性。</span><span class="sxs-lookup"><span data-stu-id="305bf-116">Persistence must not be enabled on either cache.</span></span>
- <span data-ttu-id="305bf-117">支援在相同 VNET 中多個快取之間的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-117">Geo-replication between caches in the same VNET is supported.</span></span> <span data-ttu-id="305bf-118">只要將兩個 VNET 設定為 VNET 中的資源能透過 TCP 連線觸達彼此的方式，就也可支援在不同 VNET 中多個快取之間的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-118">Geo-replication between caches in different VNETs is also supported, as long as the two VNETs are configured in such a way that resources in the VNETs are able to reach each other via TCP connections.</span></span>

<span data-ttu-id="305bf-119">在設定異地複寫之後，下列限制適用於連結的快取組：</span><span class="sxs-lookup"><span data-stu-id="305bf-119">After Geo-replication is configured, the following restrictions apply to your linked cache pair:</span></span>

- <span data-ttu-id="305bf-120">次要連結快取是唯讀的；您可以從中讀取，但無法寫入任何資料。</span><span class="sxs-lookup"><span data-stu-id="305bf-120">The secondary linked cache is read-only; you can read from it, but you can't write any data to it.</span></span> 
- <span data-ttu-id="305bf-121">任何將連結新增之前就已在次要連結快取中的資料都會加以移除。</span><span class="sxs-lookup"><span data-stu-id="305bf-121">Any data that was in the secondary linked cache before the link was added is removed.</span></span> <span data-ttu-id="305bf-122">不過，如果後續將異地複寫移除，複寫的資料就會保留在次要連結快取中。</span><span class="sxs-lookup"><span data-stu-id="305bf-122">If the Geo-replication is subsequently removed however, the replicated data remains in the secondary linked cache.</span></span>
- <span data-ttu-id="305bf-123">如果快取已啟用叢集，就無法在任一個快取上起始[調整大小作業](cache-how-to-scale.md)，或是[變更分區數目](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="305bf-123">You can't initiate a [scaling operation](cache-how-to-scale.md) on either cache or [change the number of shards](cache-how-to-premium-clustering.md) if the cache has clustering enabled.</span></span>
- <span data-ttu-id="305bf-124">您無法啟用任一個快取的持續性。</span><span class="sxs-lookup"><span data-stu-id="305bf-124">You can't enable persistence on either cache.</span></span>
- <span data-ttu-id="305bf-125">您可以對任一個快取使用[匯出](cache-how-to-import-export-data.md#export)，但是您只可以[匯入](cache-how-to-import-export-data.md#import)主要連結快取中。</span><span class="sxs-lookup"><span data-stu-id="305bf-125">You can use [Export](cache-how-to-import-export-data.md#export) with either cache, but you can only [Import](cache-how-to-import-export-data.md#import) into the primary linked cache.</span></span>
- <span data-ttu-id="305bf-126">您無法刪除任一個連結快取或包含它們的資源群組，直到您移除異地複寫連結為止。</span><span class="sxs-lookup"><span data-stu-id="305bf-126">You can't delete either linked cache, or the resource group that contains them, until you remove the Geo-replication link.</span></span> <span data-ttu-id="305bf-127">如需詳細資訊，請參閱[當我嘗試刪除連結快取時，作業失敗的原因？](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span><span class="sxs-lookup"><span data-stu-id="305bf-127">For more information, see [Why did the operation fail when I tried to delete my linked cache?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span></span>
- <span data-ttu-id="305bf-128">如果兩個快取位於不同的區域，網路輸出費用將會套用至跨區域複寫到次要連結快取的資料。</span><span class="sxs-lookup"><span data-stu-id="305bf-128">If the two caches are in different regions, network egress costs will apply to the data replicated across regions to the secondary linked cache.</span></span> <span data-ttu-id="305bf-129">如需詳細資訊，請參閱[跨 Azure 區域複寫我的資料需要多少費用？](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span><span class="sxs-lookup"><span data-stu-id="305bf-129">For more information, see [How much does it cost to replicate my data across Azure regions?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span></span>
- <span data-ttu-id="305bf-130">如果主要快取 (和其複本) 關閉，沒有任何自動容錯移轉至次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-130">There is no automatic failover to the secondary linked cache if the primary cache (and its replica) go down.</span></span> <span data-ttu-id="305bf-131">為了容錯移轉用戶端應用程式，您必須將異地複寫連結手動移除，並將用戶端應用程式指向先前為次要連結快取的快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-131">In order to failover client applications, you would need to manually remove the Geo-replication link and point the client applications to the cache that was formerly the secondary linked cache.</span></span> <span data-ttu-id="305bf-132">如需詳細資訊，請參閱[容錯移轉至次要連結快取如何運作？](#how-does-failing-over-to-the-secondary-linked-cache-work)</span><span class="sxs-lookup"><span data-stu-id="305bf-132">For more information, see [How does failing over to the secondary linked cache work?](#how-does-failing-over-to-the-secondary-linked-cache-work)</span></span>

## <a name="add-a-geo-replication-link"></a><span data-ttu-id="305bf-133">新增異地複寫連結</span><span class="sxs-lookup"><span data-stu-id="305bf-133">Add a Geo-replication link</span></span>

1. <span data-ttu-id="305bf-134">若要將兩個高階快取連結在一起以進行異地備援，請從要作為主要連結快取之快取的 [資源] 功能表按一下 [異地複寫]，然後從 [異地複寫] 刀鋒視窗按一下 [新增快取複寫連結]。</span><span class="sxs-lookup"><span data-stu-id="305bf-134">To link two premium caches together for geo-replication, click **Geo-replication** from the Resource menu of the cache intended as the primary linked cache, and then click **Add cache replication link** from the **Geo-replication** blade.</span></span>

    ![新增連結](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. <span data-ttu-id="305bf-136">從 [相容的快取] 清單中按一下所需次要快取的名稱。</span><span class="sxs-lookup"><span data-stu-id="305bf-136">Click the name of the desired secondary cache from the **Compatible caches** list.</span></span> <span data-ttu-id="305bf-137">如果您所需的快取未顯示在清單中，請確認符合所需次要快取的[異地複寫必要條件](#geo-replication-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="305bf-137">If your desired cache isn't displayed in the list, verify that the [Geo-replication prerequisites](#geo-replication-prerequisites) for the desired secondary cache are met.</span></span> <span data-ttu-id="305bf-138">若要依區域篩選快取，按一下地圖中的所需區域，可在 [相容的快取] 清單中僅顯示這些快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-138">To filter the caches by region, click the desired region in the map to display only those caches in the **Compatible caches** list.</span></span>

    ![異地複寫相容的快取](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    <span data-ttu-id="305bf-140">您也可以使用操作功能表來起始連結的流程，或檢視有關次要快取的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="305bf-140">You can also initiate the linking process or view details about the secondary cache by using the context menu.</span></span>

    ![異地複寫操作功能表](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. <span data-ttu-id="305bf-142">按一下 [連結] 可將兩個快取連結在一起，並開始複寫流程。</span><span class="sxs-lookup"><span data-stu-id="305bf-142">Click **Link** to link the two caches together and begin the replication process.</span></span>

    ![連結快取](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. <span data-ttu-id="305bf-144">您可以在 [異地複寫] 刀鋒視窗上檢視複寫流程的進度。</span><span class="sxs-lookup"><span data-stu-id="305bf-144">You can view the progress of the replication process on the **Geo-replication** blade.</span></span>

    ![連結狀態](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    <span data-ttu-id="305bf-146">您也可以在 [概觀]刀鋒視窗上檢視主要和次要快取的連結狀態。</span><span class="sxs-lookup"><span data-stu-id="305bf-146">You can also view the linking status on the **Overview** blade for both the primary and secondary caches.</span></span>

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    <span data-ttu-id="305bf-148">一旦複寫程序完成之後，[連結狀態] 會變為 [成功]。</span><span class="sxs-lookup"><span data-stu-id="305bf-148">Once the replication process is complete, the **Link status** changes to **Succeeded**.</span></span>

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    <span data-ttu-id="305bf-150">在連結流程期間，主要連結快取仍然可供使用，但連結流程完成之前，沒有可用的次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-150">During the linking process, the primary linked cache remains available for use but the secondary linked cache is not available until the linking process completes.</span></span>

## <a name="remove-a-geo-replication-link"></a><span data-ttu-id="305bf-151">移除異地複寫連結</span><span class="sxs-lookup"><span data-stu-id="305bf-151">Remove a Geo-replication link</span></span>

1. <span data-ttu-id="305bf-152">若要將兩個快取之間的連結移除並停止異地複寫，請從 [異地複寫] 刀鋒視窗按一下 [取消連結快取]。</span><span class="sxs-lookup"><span data-stu-id="305bf-152">To remove the link between two caches and stop Geo-replication, click **Unlink caches** from the **Geo-replication** blade.</span></span>
    
    ![取消連結快取](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    <span data-ttu-id="305bf-154">取消連結流程完成時，次要快取就可供讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="305bf-154">When the unlinking process completes, the secondary cache is available for both reads and writes.</span></span>

>[!NOTE]
><span data-ttu-id="305bf-155">將異地複寫連結移除時，從主要連結快取複寫的資料就會保留在次要快取中。</span><span class="sxs-lookup"><span data-stu-id="305bf-155">When the Geo-replication link is removed, the replicated data from the primary linked cache remains in the secondary cache.</span></span>
>
>

## <a name="geo-replication-faq"></a><span data-ttu-id="305bf-156">異地複寫常見問題集</span><span class="sxs-lookup"><span data-stu-id="305bf-156">Geo-replication FAQ</span></span>

- [<span data-ttu-id="305bf-157">可以使用異地複寫搭配標準或基本層快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-157">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [<span data-ttu-id="305bf-158">在連結或取消連結流程期間，快取是否可供使用？</span><span class="sxs-lookup"><span data-stu-id="305bf-158">Is my cache available for use during the linking or unlinking process?</span></span>](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [<span data-ttu-id="305bf-159">可以同時連結兩個以上的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-159">Can I link more than two caches together?</span></span>](#can-i-link-more-than-two-caches-together)
- [<span data-ttu-id="305bf-160">可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-160">Can I link two caches from different Azure subscriptions?</span></span>](#can-i-link-two-caches-from-different-azure-subscriptions)
- [<span data-ttu-id="305bf-161">可以將兩個不同大小的快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-161">Can I link two caches with different sizes?</span></span>](#can-i-link-two-caches-with-different-sizes)
- [<span data-ttu-id="305bf-162">啟用叢集時可以使用異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-162">Can I use Geo-replication with clustering enabled?</span></span>](#can-i-use-geo-replication-with-clustering-enabled)
- [<span data-ttu-id="305bf-163">可以使用異地複寫搭配 VNET 中的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-163">Can I use Geo-replication with my caches in a VNET?</span></span>](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [<span data-ttu-id="305bf-164">可以使用 PowerShell 或 Azure CLI 管理異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-164">Can I use PowerShell or Azure CLI to manage Geo-replication?</span></span>](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [<span data-ttu-id="305bf-165">跨 Azure 區域複寫我的資料需要多少費用？</span><span class="sxs-lookup"><span data-stu-id="305bf-165">How much does it cost to replicate my data across Azure regions?</span></span>](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [<span data-ttu-id="305bf-166">當我嘗試刪除連結快取時，作業失敗的原因？</span><span class="sxs-lookup"><span data-stu-id="305bf-166">Why did the operation fail when I tried to delete my linked cache?</span></span>](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [<span data-ttu-id="305bf-167">要將次要連結快取用於哪個區域？</span><span class="sxs-lookup"><span data-stu-id="305bf-167">What region should I use for my secondary linked cache?</span></span>](#what-region-should-i-use-for-my-secondary-linked-cache)
- [<span data-ttu-id="305bf-168">容錯移轉至次要連結快取如何運作？</span><span class="sxs-lookup"><span data-stu-id="305bf-168">How does failing over to the secondary linked cache work?</span></span>](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a><span data-ttu-id="305bf-169">可以使用異地複寫搭配標準或基本層快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-169">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>

<span data-ttu-id="305bf-170">否，異地複寫僅適用於高階層快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-170">No, Geo-replication is only available for Premium tier caches.</span></span>

### <a name="is-my-cache-available-for-use-during-the-linking-or-unlinking-process"></a><span data-ttu-id="305bf-171">在連結或取消連結流程期間，快取是否可供使用？</span><span class="sxs-lookup"><span data-stu-id="305bf-171">Is my cache available for use during the linking or unlinking process?</span></span>

- <span data-ttu-id="305bf-172">同時連結兩個快取進行異地複寫時，主要連結快取仍然可供使用，但連結流程完成之前，沒有可用的次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-172">When linking two caches together for Geo-replication, the primary linked cache remains available for use but the secondary linked cache is not available until the linking process completes.</span></span>
- <span data-ttu-id="305bf-173">將兩個快取之間的異地複寫連結移除時，這兩個快取都保持可供使用。</span><span class="sxs-lookup"><span data-stu-id="305bf-173">When removing the Geo-replication link between two caches, both caches remain available for use.</span></span>

### <a name="can-i-link-more-than-two-caches-together"></a><span data-ttu-id="305bf-174">可以同時連結兩個以上的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-174">Can I link more than two caches together?</span></span>

<span data-ttu-id="305bf-175">否，使用異地複寫時，您只能將兩個快取連結在一起。</span><span class="sxs-lookup"><span data-stu-id="305bf-175">No, when using Geo-replication you can only link two caches together.</span></span>

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a><span data-ttu-id="305bf-176">可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-176">Can I link two caches from different Azure subscriptions?</span></span>

<span data-ttu-id="305bf-177">否，這兩個快取必須位於相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="305bf-177">No, both caches must be in the same Azure subscription.</span></span>

### <a name="can-i-link-two-caches-with-different-sizes"></a><span data-ttu-id="305bf-178">可以將兩個不同大小的快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-178">Can I link two caches with different sizes?</span></span>

<span data-ttu-id="305bf-179">是，前提是次要連結快取超過主要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-179">Yes, as long as the secondary linked cache is larger than the primary linked cache.</span></span>

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a><span data-ttu-id="305bf-180">啟用叢集時可以使用異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-180">Can I use Geo-replication with clustering enabled?</span></span>

<span data-ttu-id="305bf-181">是，前提是這兩個快取具有相同的分區數目。</span><span class="sxs-lookup"><span data-stu-id="305bf-181">Yes, as long as both caches have the same number of shards.</span></span>

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a><span data-ttu-id="305bf-182">可以使用異地複寫搭配 VNET 中的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-182">Can I use Geo-replication with my caches in a VNET?</span></span>

<span data-ttu-id="305bf-183">是，支援 VNET 中快取的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-183">Yes, Geo-replication of caches in VNETs are supported.</span></span> 

- <span data-ttu-id="305bf-184">支援在相同 VNET 中多個快取之間的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-184">Geo-replication between caches in the same VNET is supported.</span></span>
- <span data-ttu-id="305bf-185">只要將兩個 VNET 設定為 VNET 中的資源能透過 TCP 連線觸達彼此的方式，就也可支援在不同 VNET 中多個快取之間的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-185">Geo-replication between caches in different VNETs is also supported, as long as the two VNETs are configured in such a way that resources in the VNETs are able to reach each other via TCP connections.</span></span>

### <a name="can-i-use-powershell-or-azure-cli-to-manage-geo-replication"></a><span data-ttu-id="305bf-186">可以使用 PowerShell 或 Azure CLI 管理異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="305bf-186">Can I use PowerShell or Azure CLI to manage Geo-replication?</span></span>

<span data-ttu-id="305bf-187">目前，您只能使用 Azure 入口網站管理異地複寫。</span><span class="sxs-lookup"><span data-stu-id="305bf-187">At this time you can only manage Geo-replication using the Azure portal.</span></span>

### <a name="how-much-does-it-cost-to-replicate-my-data-across-azure-regions"></a><span data-ttu-id="305bf-188">跨 Azure 區域複寫我的資料需要多少費用？</span><span class="sxs-lookup"><span data-stu-id="305bf-188">How much does it cost to replicate my data across Azure regions?</span></span>

<span data-ttu-id="305bf-189">使用異地複寫時，主要連結快取的資料會複寫到次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-189">When using Geo-replication, data from the primary linked cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="305bf-190">如果兩個連結快取位於相同的 Azure 區域中，資料轉送就不需付費。</span><span class="sxs-lookup"><span data-stu-id="305bf-190">If the two linked caches are in the same Azure region, there is no charge for the data transfer.</span></span> <span data-ttu-id="305bf-191">如果兩個連結快取位於不同的 Azure 區域中，異地複寫資料轉送費用就是將該資料複寫到其他 Azure 區域的頻寬費用。</span><span class="sxs-lookup"><span data-stu-id="305bf-191">If the two linked caches are in different Azure regions, the Geo-Replication data transfer charge is the bandwidth cost of replicating that data to the other Azure region.</span></span> <span data-ttu-id="305bf-192">如需詳細資訊，請參閱[頻寬定價詳細資料](https://azure.microsoft.com/pricing/details/bandwidth/)。</span><span class="sxs-lookup"><span data-stu-id="305bf-192">For more information, see [Bandwidth Pricing Details](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache"></a><span data-ttu-id="305bf-193">當我嘗試刪除連結快取時，作業失敗的原因？</span><span class="sxs-lookup"><span data-stu-id="305bf-193">Why did the operation fail when I tried to delete my linked cache?</span></span>

<span data-ttu-id="305bf-194">當兩個快取連結在一起時，您無法刪除任一個快取或包含它們的資源群組，直到您移除異地複寫連結為止。</span><span class="sxs-lookup"><span data-stu-id="305bf-194">When two caches are linked together, you can't delete either cache or the resource group that contains them until you remove the Geo-replication link.</span></span> <span data-ttu-id="305bf-195">如果您嘗試將包含一個或兩個連結快取的資源群組刪除，就會將資源群組中的其他資源刪除，但資源群組會保留在 `deleting` 狀態，而資源群組中的任何連結快取會維持 `running` 狀態。</span><span class="sxs-lookup"><span data-stu-id="305bf-195">If you attempt to delete the resource group that contains one or both of the linked caches, the other resources in the resource group are deleted, but the resource group stays in the `deleting` state and any linked caches in the resource group remain in the `running` state.</span></span> <span data-ttu-id="305bf-196">若要完成刪除資源群組和其中的連結快取，請如[移除異地複寫連結](#remove-a-geo-replication-link)中所述，將異地複寫連結中斷。</span><span class="sxs-lookup"><span data-stu-id="305bf-196">To complete the deletion of the resource group and the linked caches within it, break the Geo-replication link as described in [Remove a Geo-replication link](#remove-a-geo-replication-link).</span></span>

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a><span data-ttu-id="305bf-197">要將次要連結快取用於哪個區域？</span><span class="sxs-lookup"><span data-stu-id="305bf-197">What region should I use for my secondary linked cache?</span></span>

<span data-ttu-id="305bf-198">一般情況下，建議您的快取與存取它的應用程式位於相同的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="305bf-198">In general, it is recommended for your cache to exist in the same Azure region as the application that accesses it.</span></span> <span data-ttu-id="305bf-199">如果您的應用程式有主要和後援區域，您的主要和次要快取就應該位於這些相同的區域。</span><span class="sxs-lookup"><span data-stu-id="305bf-199">If your application has a primary and fallback region, then your primary and secondary caches should exist in those same regions.</span></span> <span data-ttu-id="305bf-200">如需配對區域的詳細資訊，請參閱[最佳做法 – Azure 配對的區域](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="305bf-200">For more information about paired regions, see [Best Practices – Azure Paired regions](../best-practices-availability-paired-regions.md).</span></span>

### <a name="how-does-failing-over-to-the-secondary-linked-cache-work"></a><span data-ttu-id="305bf-201">容錯移轉至次要連結快取如何運作？</span><span class="sxs-lookup"><span data-stu-id="305bf-201">How does failing over to the secondary linked cache work?</span></span>

<span data-ttu-id="305bf-202">在異地複寫的初始版本中，Azure Redis 快取不支援跨 Azure 區域自動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="305bf-202">In the initial release of Geo-replication, Azure Redis Cache does not support automatic failover across Azure regions.</span></span> <span data-ttu-id="305bf-203">異地複寫主要用於災害復原情節。</span><span class="sxs-lookup"><span data-stu-id="305bf-203">Geo-replication is used primarily in a disaster recovery scenario.</span></span> <span data-ttu-id="305bf-204">在災害復原情節中，客戶需以協調的方式，在備份的區域中提出整個應用程式堆疊，而不是讓個別應用程式元件決定何時要自行切換至其備份。</span><span class="sxs-lookup"><span data-stu-id="305bf-204">In a distater recovery scenario, customers should bring up the entire application stack in a backup region in a coordinated manner rather than letting individual application components decide when to switch to their backups on their own.</span></span> <span data-ttu-id="305bf-205">這與 Redis 特別相關。</span><span class="sxs-lookup"><span data-stu-id="305bf-205">This is especially relevant to Redis.</span></span> <span data-ttu-id="305bf-206">Redis 的主要優點之一是，它是非常低延遲的存放區。</span><span class="sxs-lookup"><span data-stu-id="305bf-206">One of the key benefits of Redis is that it is a very low-latency store.</span></span> <span data-ttu-id="305bf-207">如果應用程式所使用的 Redis 容錯移轉至不同的 Azure 區域，但計算層並未容錯移轉，新增的來回時間就會對效能產生明顯的影響。</span><span class="sxs-lookup"><span data-stu-id="305bf-207">If Redis used by an application fails over to a different Azure region but the compute tier does not, the added round trip time would have a noticeable impact on performance.</span></span> <span data-ttu-id="305bf-208">基於這個理由，我們將需要避免 Redis 因暫時性的可用性問題而自動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="305bf-208">For this reason, we would like to avoid Redis failing over automatically due to transient availability issues.</span></span>

<span data-ttu-id="305bf-209">目前，若要起始容錯移轉，您必須將 Azure 入口網站中的異地複寫連結移除，然後將 Redis 用戶端中的連線端點從主要連結快取變更為 (先前稱為連結) 次要快取。</span><span class="sxs-lookup"><span data-stu-id="305bf-209">Currently, to initiate the failover, you need to remove the Geo-replication link in the Azure portal, and then change the connection end-point in the Redis client from the primary linked cache to the (formerly linked) secondary cache.</span></span> <span data-ttu-id="305bf-210">當兩個快取解除關聯時，複本會再次變成一般的讀寫快取，並接受直接來自 Redis 用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="305bf-210">When the two caches are disassociated, the replica becomes a regular read-write cache again and accepts requests directly from Redis clients.</span></span>


## <a name="next-steps"></a><span data-ttu-id="305bf-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="305bf-211">Next steps</span></span>

<span data-ttu-id="305bf-212">深入了解 [Azure Redis Cache 高階層](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="305bf-212">Learn more about the [Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

