---
title: "Azure Redis 快取的 aaaHow tooconfigure 地理複寫 |Microsoft 文件"
description: "了解如何 tooreplicate Azure Redis 快取執行個體跨地理區域。"
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
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a><span data-ttu-id="c30a0-103">如何針對 Azure Redis 快取 tooconfigure 地理複寫</span><span class="sxs-lookup"><span data-stu-id="c30a0-103">How tooconfigure Geo-replication for Azure Redis Cache</span></span>

<span data-ttu-id="c30a0-104">異地複寫提供一個機制，可供連結兩個高階層 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="c30a0-104">Geo-replication provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="c30a0-105">一個快取指定為 hello 主要的連線快取，而 hello hello 次要連結快取為其他。</span><span class="sxs-lookup"><span data-stu-id="c30a0-105">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="c30a0-106">hello 次要連結快取會變成唯讀的並寫入的 toohello 主要快取的資料複寫 toohello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-106">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="c30a0-107">這項功能可以跨 Azure 區域是使用的 tooreplicate 快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-107">This functionality can be used tooreplicate a cache across Azure regions.</span></span> <span data-ttu-id="c30a0-108">本文章提供您高階層 Azure Redis 快取執行個體的指南 tooconfiguring 地理複寫。</span><span class="sxs-lookup"><span data-stu-id="c30a0-108">This article provides a guide tooconfiguring Geo-replication for your Premium tier Azure Redis Cache instances.</span></span>

## <a name="geo-replication-prerequisites"></a><span data-ttu-id="c30a0-109">異地複寫的必要條件</span><span class="sxs-lookup"><span data-stu-id="c30a0-109">Geo-replication prerequisites</span></span>

<span data-ttu-id="c30a0-110">必須符合 tooconfigure 地理複寫之間兩個快取，hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="c30a0-110">tooconfigure Geo-replication between two caches, hello following prerequisites must be met:</span></span>

- <span data-ttu-id="c30a0-111">這兩個快取必須是[高階層](cache-premium-tier-intro.md)快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-111">Both caches must be [Premium tier](cache-premium-tier-intro.md) caches.</span></span>
- <span data-ttu-id="c30a0-112">這兩個快取必須在 hello 相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c30a0-112">Both caches must be in hello same Azure subscription.</span></span>
- <span data-ttu-id="c30a0-113">hello 次要連結快取必須是可以 hello 相同定價層或更大的定價層，比 hello 主要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-113">hello secondary linked cache must be either hello same pricing tier or a larger pricing tier than hello primary linked cache.</span></span>
- <span data-ttu-id="c30a0-114">Hello 次要連結快取 hello 主要連結快取已啟用叢集，如果以 hello 啟用叢集必須有相同數目的分區，做為 hello 主要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-114">If hello primary linked cache has clustering enabled, hello secondary linked cache must have clustering enabled with hello same number of shards as hello primary linked cache.</span></span>
- <span data-ttu-id="c30a0-115">必須建立兩個快取並同時處於執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="c30a0-115">Both caches must be created and in a running state.</span></span>
- <span data-ttu-id="c30a0-116">任何一個快取上皆不能啟用持續性。</span><span class="sxs-lookup"><span data-stu-id="c30a0-116">Persistence must not be enabled on either cache.</span></span>
- <span data-ttu-id="c30a0-117">Hello 支援相同的 VNET 中的快取之間的地理複寫。</span><span class="sxs-lookup"><span data-stu-id="c30a0-117">Geo-replication between caches in hello same VNET is supported.</span></span> <span data-ttu-id="c30a0-118">也支援在不同的 Vnet 中的快取之間的地理複寫，只要 hello 兩個 Vnet 設定的方式 hello Vnet 中的資源都可以 tooreach 彼此透過 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="c30a0-118">Geo-replication between caches in different VNETs is also supported, as long as hello two VNETs are configured in such a way that resources in hello VNETs are able tooreach each other via TCP connections.</span></span>

<span data-ttu-id="c30a0-119">設定異地複寫後，hello 下列限制適用於 tooyour 連結的快取組：</span><span class="sxs-lookup"><span data-stu-id="c30a0-119">After Geo-replication is configured, hello following restrictions apply tooyour linked cache pair:</span></span>

- <span data-ttu-id="c30a0-120">hello 次要連結快取是唯讀的。您可以讀取它，但您無法寫入任何資料 tooit。</span><span class="sxs-lookup"><span data-stu-id="c30a0-120">hello secondary linked cache is read-only; you can read from it, but you can't write any data tooit.</span></span> 
- <span data-ttu-id="c30a0-121">會移除任何加入 hello 連結之前已在 hello 次要連結快取中的資料。</span><span class="sxs-lookup"><span data-stu-id="c30a0-121">Any data that was in hello secondary linked cache before hello link was added is removed.</span></span> <span data-ttu-id="c30a0-122">Hello 地理複寫之後移除不過，如果 hello 複寫 hello 次要連結快取中的資料仍會保留。</span><span class="sxs-lookup"><span data-stu-id="c30a0-122">If hello Geo-replication is subsequently removed however, hello replicated data remains in hello secondary linked cache.</span></span>
- <span data-ttu-id="c30a0-123">無法起始[調整大小作業](cache-how-to-scale.md)任一個快取或[變更 hello 分區數目](cache-how-to-premium-clustering.md)如果 hello 快取已啟用叢集。</span><span class="sxs-lookup"><span data-stu-id="c30a0-123">You can't initiate a [scaling operation](cache-how-to-scale.md) on either cache or [change hello number of shards](cache-how-to-premium-clustering.md) if hello cache has clustering enabled.</span></span>
- <span data-ttu-id="c30a0-124">您無法啟用任一個快取的持續性。</span><span class="sxs-lookup"><span data-stu-id="c30a0-124">You can't enable persistence on either cache.</span></span>
- <span data-ttu-id="c30a0-125">您可以使用[匯出](cache-how-to-import-export-data.md#export)任一個快取，但是您可以只[匯入](cache-how-to-import-export-data.md#import)到主要 hello 連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-125">You can use [Export](cache-how-to-import-export-data.md#export) with either cache, but you can only [Import](cache-how-to-import-export-data.md#import) into hello primary linked cache.</span></span>
- <span data-ttu-id="c30a0-126">您無法刪除連結的快取或包含它們，直到您移除 hello 異地複寫連結的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="c30a0-126">You can't delete either linked cache, or hello resource group that contains them, until you remove hello Geo-replication link.</span></span> <span data-ttu-id="c30a0-127">如需詳細資訊，請參閱[未 hello 作業失敗的原因當我嘗試 toodelete 我連結的快取？](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span><span class="sxs-lookup"><span data-stu-id="c30a0-127">For more information, see [Why did hello operation fail when I tried toodelete my linked cache?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)</span></span>
- <span data-ttu-id="c30a0-128">如果 hello 兩個快取是在不同的區域中，網路輸出費用將會套用跨區域 toohello 次要連結快取複寫 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="c30a0-128">If hello two caches are in different regions, network egress costs will apply toohello data replicated across regions toohello secondary linked cache.</span></span> <span data-ttu-id="c30a0-129">如需詳細資訊，請參閱[多少作用成本 tooreplicate 我的資料跨 Azure 區域？](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span><span class="sxs-lookup"><span data-stu-id="c30a0-129">For more information, see [How much does it cost tooreplicate my data across Azure regions?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)</span></span>
- <span data-ttu-id="c30a0-130">沒有自動容錯移轉 toohello 次要連結快取如果 hello 主要快取 （和其複本） 當機。</span><span class="sxs-lookup"><span data-stu-id="c30a0-130">There is no automatic failover toohello secondary linked cache if hello primary cache (and its replica) go down.</span></span> <span data-ttu-id="c30a0-131">順序 toofailover 用戶端應用程式，您會需要 toomanually 移除 hello 異地複寫連結，點 hello 用戶端應用程式 toohello 快取，先前作為 hello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-131">In order toofailover client applications, you would need toomanually remove hello Geo-replication link and point hello client applications toohello cache that was formerly hello secondary linked cache.</span></span> <span data-ttu-id="c30a0-132">如需詳細資訊，請參閱[容錯 toohello 次要連結快取移轉如何運作？](#how-does-failing-over-to-the-secondary-linked-cache-work)</span><span class="sxs-lookup"><span data-stu-id="c30a0-132">For more information, see [How does failing over toohello secondary linked cache work?](#how-does-failing-over-to-the-secondary-linked-cache-work)</span></span>

## <a name="add-a-geo-replication-link"></a><span data-ttu-id="c30a0-133">新增異地複寫連結</span><span class="sxs-lookup"><span data-stu-id="c30a0-133">Add a Geo-replication link</span></span>

1. <span data-ttu-id="c30a0-134">toolink 兩個 premium 一起快取的地理複寫中，按一下**地理複寫**hello 主要連結所做的 hello 快取的 hello 資源功能表上，快取，然後再按一下**新增快取複寫連結**從 hello**地理複寫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c30a0-134">toolink two premium caches together for geo-replication, click **Geo-replication** from hello Resource menu of hello cache intended as hello primary linked cache, and then click **Add cache replication link** from hello **Geo-replication** blade.</span></span>

    ![新增連結](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. <span data-ttu-id="c30a0-136">按一下所需的 hello 次要快取從 hello hello 名稱**相容的快取**清單。</span><span class="sxs-lookup"><span data-stu-id="c30a0-136">Click hello name of hello desired secondary cache from hello **Compatible caches** list.</span></span> <span data-ttu-id="c30a0-137">如果您想要的快取未顯示 hello 清單中，確認該 hello[地理複寫必要條件](#geo-replication-prerequisites)的 hello 需要符合次要快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-137">If your desired cache isn't displayed in hello list, verify that hello [Geo-replication prerequisites](#geo-replication-prerequisites) for hello desired secondary cache are met.</span></span> <span data-ttu-id="c30a0-138">toofilter hello 快取，以區域、 按一下 hello 所需的區域中只會快取中 hello hello 對應 toodisplay**相容的快取**清單。</span><span class="sxs-lookup"><span data-stu-id="c30a0-138">toofilter hello caches by region, click hello desired region in hello map toodisplay only those caches in hello **Compatible caches** list.</span></span>

    ![異地複寫相容的快取](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    <span data-ttu-id="c30a0-140">您也可以初始化 hello 使用 hello 操作功能表中連結 hello 次要快取相關的處理程序或檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c30a0-140">You can also initiate hello linking process or view details about hello secondary cache by using hello context menu.</span></span>

    ![異地複寫操作功能表](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. <span data-ttu-id="c30a0-142">按一下**連結**toolink 一起 hello 兩個快取，並開始 hello 複寫程序。</span><span class="sxs-lookup"><span data-stu-id="c30a0-142">Click **Link** toolink hello two caches together and begin hello replication process.</span></span>

    ![連結快取](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. <span data-ttu-id="c30a0-144">您可以檢視 hello 進度 hello 複寫程序上 hello**地理複寫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c30a0-144">You can view hello progress of hello replication process on hello **Geo-replication** blade.</span></span>

    ![連結狀態](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    <span data-ttu-id="c30a0-146">您也可以檢視連結狀態 hello hello**概觀**這兩個 hello 主要和次要快取刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c30a0-146">You can also view hello linking status on hello **Overview** blade for both hello primary and secondary caches.</span></span>

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    <span data-ttu-id="c30a0-148">Hello 複寫程序完成之後，hello**連結狀態**變更太**Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="c30a0-148">Once hello replication process is complete, hello **Link status** changes too**Succeeded**.</span></span>

    ![快取狀態](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    <span data-ttu-id="c30a0-150">期間 hello 連結程序，hello 主要連結快取仍然可供使用，但 hello 連結程序完成之前，沒有可用 hello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-150">During hello linking process, hello primary linked cache remains available for use but hello secondary linked cache is not available until hello linking process completes.</span></span>

## <a name="remove-a-geo-replication-link"></a><span data-ttu-id="c30a0-151">移除異地複寫連結</span><span class="sxs-lookup"><span data-stu-id="c30a0-151">Remove a Geo-replication link</span></span>

1. <span data-ttu-id="c30a0-152">按一下 停止地理複寫中，兩個快取之間 tooremove hello 連結**取消連結的快取**hello 從**地理複寫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c30a0-152">tooremove hello link between two caches and stop Geo-replication, click **Unlink caches** from hello **Geo-replication** blade.</span></span>
    
    ![取消連結快取](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    <span data-ttu-id="c30a0-154">Hello 取消連結的程序完成時，hello 次要快取會使用同時讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="c30a0-154">When hello unlinking process completes, hello secondary cache is available for both reads and writes.</span></span>

>[!NOTE]
><span data-ttu-id="c30a0-155">Hello 異地複寫連結中移除時，hello 會從 hello 連結之主要快取仍會留在 hello 次要快取複寫資料。</span><span class="sxs-lookup"><span data-stu-id="c30a0-155">When hello Geo-replication link is removed, hello replicated data from hello primary linked cache remains in hello secondary cache.</span></span>
>
>

## <a name="geo-replication-faq"></a><span data-ttu-id="c30a0-156">異地複寫常見問題集</span><span class="sxs-lookup"><span data-stu-id="c30a0-156">Geo-replication FAQ</span></span>

- [<span data-ttu-id="c30a0-157">可以使用異地複寫搭配標準或基本層快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-157">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [<span data-ttu-id="c30a0-158">是可供 hello 連結或取消連結的程序期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="c30a0-158">Is my cache available for use during hello linking or unlinking process?</span></span>](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [<span data-ttu-id="c30a0-159">可以同時連結兩個以上的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-159">Can I link more than two caches together?</span></span>](#can-i-link-more-than-two-caches-together)
- [<span data-ttu-id="c30a0-160">可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-160">Can I link two caches from different Azure subscriptions?</span></span>](#can-i-link-two-caches-from-different-azure-subscriptions)
- [<span data-ttu-id="c30a0-161">可以將兩個不同大小的快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-161">Can I link two caches with different sizes?</span></span>](#can-i-link-two-caches-with-different-sizes)
- [<span data-ttu-id="c30a0-162">啟用叢集時可以使用異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-162">Can I use Geo-replication with clustering enabled?</span></span>](#can-i-use-geo-replication-with-clustering-enabled)
- [<span data-ttu-id="c30a0-163">可以使用異地複寫搭配 VNET 中的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-163">Can I use Geo-replication with my caches in a VNET?</span></span>](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [<span data-ttu-id="c30a0-164">可以使用 PowerShell 或 Azure CLI toomanage 地理複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-164">Can I use PowerShell or Azure CLI toomanage Geo-replication?</span></span>](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [<span data-ttu-id="c30a0-165">多少成本 tooreplicate 我的資料跨 Azure 區域？</span><span class="sxs-lookup"><span data-stu-id="c30a0-165">How much does it cost tooreplicate my data across Azure regions?</span></span>](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [<span data-ttu-id="c30a0-166">為什麼沒有 hello 作業失敗時我已嘗試過 toodelete 我連結的快取？</span><span class="sxs-lookup"><span data-stu-id="c30a0-166">Why did hello operation fail when I tried toodelete my linked cache?</span></span>](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [<span data-ttu-id="c30a0-167">要將次要連結快取用於哪個區域？</span><span class="sxs-lookup"><span data-stu-id="c30a0-167">What region should I use for my secondary linked cache?</span></span>](#what-region-should-i-use-for-my-secondary-linked-cache)
- [<span data-ttu-id="c30a0-168">容錯移轉 toohello 次要連結快取的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="c30a0-168">How does failing over toohello secondary linked cache work?</span></span>](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a><span data-ttu-id="c30a0-169">可以使用異地複寫搭配標準或基本層快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-169">Can I use Geo-replication with a Standard or Basic tier cache?</span></span>

<span data-ttu-id="c30a0-170">否，異地複寫僅適用於高階層快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-170">No, Geo-replication is only available for Premium tier caches.</span></span>

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a><span data-ttu-id="c30a0-171">是可供 hello 連結或取消連結的程序期間使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="c30a0-171">Is my cache available for use during hello linking or unlinking process?</span></span>

- <span data-ttu-id="c30a0-172">當連結在一起異地備援的兩個快取，hello 主要連結快取仍然可供使用，但 hello 連結程序完成之前，沒有可用 hello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-172">When linking two caches together for Geo-replication, hello primary linked cache remains available for use but hello secondary linked cache is not available until hello linking process completes.</span></span>
- <span data-ttu-id="c30a0-173">當移除兩個快取之間的 hello 異地複寫連結，這兩個快取保持可供使用。</span><span class="sxs-lookup"><span data-stu-id="c30a0-173">When removing hello Geo-replication link between two caches, both caches remain available for use.</span></span>

### <a name="can-i-link-more-than-two-caches-together"></a><span data-ttu-id="c30a0-174">可以同時連結兩個以上的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-174">Can I link more than two caches together?</span></span>

<span data-ttu-id="c30a0-175">否，使用異地複寫時，您只能將兩個快取連結在一起。</span><span class="sxs-lookup"><span data-stu-id="c30a0-175">No, when using Geo-replication you can only link two caches together.</span></span>

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a><span data-ttu-id="c30a0-176">可以將不同 Azure 訂用帳戶中的兩個快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-176">Can I link two caches from different Azure subscriptions?</span></span>

<span data-ttu-id="c30a0-177">不行，兩個快取必須在 hello 相同的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c30a0-177">No, both caches must be in hello same Azure subscription.</span></span>

### <a name="can-i-link-two-caches-with-different-sizes"></a><span data-ttu-id="c30a0-178">可以將兩個不同大小的快取加以連結嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-178">Can I link two caches with different sizes?</span></span>

<span data-ttu-id="c30a0-179">是，只要 hello 次要連結快取大於 hello 主要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-179">Yes, as long as hello secondary linked cache is larger than hello primary linked cache.</span></span>

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a><span data-ttu-id="c30a0-180">啟用叢集時可以使用異地複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-180">Can I use Geo-replication with clustering enabled?</span></span>

<span data-ttu-id="c30a0-181">是的這兩個快取有 hello 是相同的分區數目。</span><span class="sxs-lookup"><span data-stu-id="c30a0-181">Yes, as long as both caches have hello same number of shards.</span></span>

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a><span data-ttu-id="c30a0-182">可以使用異地複寫搭配 VNET 中的快取嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-182">Can I use Geo-replication with my caches in a VNET?</span></span>

<span data-ttu-id="c30a0-183">是，支援 VNET 中快取的異地複寫。</span><span class="sxs-lookup"><span data-stu-id="c30a0-183">Yes, Geo-replication of caches in VNETs are supported.</span></span> 

- <span data-ttu-id="c30a0-184">Hello 支援相同的 VNET 中的快取之間的地理複寫。</span><span class="sxs-lookup"><span data-stu-id="c30a0-184">Geo-replication between caches in hello same VNET is supported.</span></span>
- <span data-ttu-id="c30a0-185">也支援在不同的 Vnet 中的快取之間的地理複寫，只要 hello 兩個 Vnet 設定的方式 hello Vnet 中的資源都可以 tooreach 彼此透過 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="c30a0-185">Geo-replication between caches in different VNETs is also supported, as long as hello two VNETs are configured in such a way that resources in hello VNETs are able tooreach each other via TCP connections.</span></span>

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a><span data-ttu-id="c30a0-186">可以使用 PowerShell 或 Azure CLI toomanage 地理複寫嗎？</span><span class="sxs-lookup"><span data-stu-id="c30a0-186">Can I use PowerShell or Azure CLI toomanage Geo-replication?</span></span>

<span data-ttu-id="c30a0-187">此時，您只能管理地理複寫使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c30a0-187">At this time you can only manage Geo-replication using hello Azure portal.</span></span>

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a><span data-ttu-id="c30a0-188">多少成本 tooreplicate 我的資料跨 Azure 區域？</span><span class="sxs-lookup"><span data-stu-id="c30a0-188">How much does it cost tooreplicate my data across Azure regions?</span></span>

<span data-ttu-id="c30a0-189">使用地理複寫，從 hello 主要連結快取的資料時，複寫的 toohello 次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-189">When using Geo-replication, data from hello primary linked cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="c30a0-190">快取與 hello 如果 hello 兩個連結位於相同的 Azure 區域 hello 資料傳輸不需付費。</span><span class="sxs-lookup"><span data-stu-id="c30a0-190">If hello two linked caches are in hello same Azure region, there is no charge for hello data transfer.</span></span> <span data-ttu-id="c30a0-191">如果 hello 兩個連結的快取中不同的 Azure 地區，hello 地理複寫資料傳送費用是 hello 複寫該資料 toohello 其他 Azure 區域的 [頻寬] 費用。</span><span class="sxs-lookup"><span data-stu-id="c30a0-191">If hello two linked caches are in different Azure regions, hello Geo-Replication data transfer charge is hello bandwidth cost of replicating that data toohello other Azure region.</span></span> <span data-ttu-id="c30a0-192">如需詳細資訊，請參閱[頻寬定價詳細資料](https://azure.microsoft.com/pricing/details/bandwidth/)。</span><span class="sxs-lookup"><span data-stu-id="c30a0-192">For more information, see [Bandwidth Pricing Details](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a><span data-ttu-id="c30a0-193">為什麼沒有 hello 作業失敗時我已嘗試過 toodelete 我連結的快取？</span><span class="sxs-lookup"><span data-stu-id="c30a0-193">Why did hello operation fail when I tried toodelete my linked cache?</span></span>

<span data-ttu-id="c30a0-194">兩個快取連結在一起，您無法刪除快取或 hello 包含這些，直到您移除 hello 異地複寫連結的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c30a0-194">When two caches are linked together, you can't delete either cache or hello resource group that contains them until you remove hello Geo-replication link.</span></span> <span data-ttu-id="c30a0-195">如果您嘗試 toodelete hello 資源群組，其中包含一或兩個 hello 連結快取、 hello hello 資源群組中的其他資源會被刪除，但 hello 資源群組會停留在 hello`deleting`狀態和任何連結 hello 資源群組中的快取保留在 hello`running`狀態。</span><span class="sxs-lookup"><span data-stu-id="c30a0-195">If you attempt toodelete hello resource group that contains one or both of hello linked caches, hello other resources in hello resource group are deleted, but hello resource group stays in hello `deleting` state and any linked caches in hello resource group remain in hello `running` state.</span></span> <span data-ttu-id="c30a0-196">中所述，toocomplete hello 刪除 hello 資源群組和 hello 連結內中斷 hello 異地複寫連結，它的快取[移除異地複寫連結](#remove-a-geo-replication-link)。</span><span class="sxs-lookup"><span data-stu-id="c30a0-196">toocomplete hello deletion of hello resource group and hello linked caches within it, break hello Geo-replication link as described in [Remove a Geo-replication link](#remove-a-geo-replication-link).</span></span>

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a><span data-ttu-id="c30a0-197">要將次要連結快取用於哪個區域？</span><span class="sxs-lookup"><span data-stu-id="c30a0-197">What region should I use for my secondary linked cache?</span></span>

<span data-ttu-id="c30a0-198">一般情況下，建議您在 hello 的快取 tooexist 相同與 hello 存取它的應用程式的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="c30a0-198">In general, it is recommended for your cache tooexist in hello same Azure region as hello application that accesses it.</span></span> <span data-ttu-id="c30a0-199">如果您的應用程式有主要和後援區域，您的主要和次要快取就應該位於這些相同的區域。</span><span class="sxs-lookup"><span data-stu-id="c30a0-199">If your application has a primary and fallback region, then your primary and secondary caches should exist in those same regions.</span></span> <span data-ttu-id="c30a0-200">如需配對區域的詳細資訊，請參閱[最佳做法 – Azure 配對的區域](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="c30a0-200">For more information about paired regions, see [Best Practices – Azure Paired regions](../best-practices-availability-paired-regions.md).</span></span>

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a><span data-ttu-id="c30a0-201">容錯移轉 toohello 次要連結快取的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="c30a0-201">How does failing over toohello secondary linked cache work?</span></span>

<span data-ttu-id="c30a0-202">在 hello 初始版本中的地理複寫，Azure Redis 快取不支援自動容錯移轉跨 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="c30a0-202">In hello initial release of Geo-replication, Azure Redis Cache does not support automatic failover across Azure regions.</span></span> <span data-ttu-id="c30a0-203">異地複寫主要用於災害復原情節。</span><span class="sxs-lookup"><span data-stu-id="c30a0-203">Geo-replication is used primarily in a disaster recovery scenario.</span></span> <span data-ttu-id="c30a0-204">在 distater 復原案例中，客戶就可使備份區域中的 hello 整個應用程式堆疊中協調的方式，而不是讓個別的應用程式元件決定何時自行 tooswitch tootheir 備份。</span><span class="sxs-lookup"><span data-stu-id="c30a0-204">In a distater recovery scenario, customers should bring up hello entire application stack in a backup region in a coordinated manner rather than letting individual application components decide when tooswitch tootheir backups on their own.</span></span> <span data-ttu-id="c30a0-205">這是 tooRedis 特別有關。</span><span class="sxs-lookup"><span data-stu-id="c30a0-205">This is especially relevant tooRedis.</span></span> <span data-ttu-id="c30a0-206">Hello 的主要優點之一是 redis 的它會非常低度延遲存放區。</span><span class="sxs-lookup"><span data-stu-id="c30a0-206">One of hello key benefits of Redis is that it is a very low-latency store.</span></span> <span data-ttu-id="c30a0-207">如果所使用的 Redis 應用程式容錯移轉 tooa 不同 Azure 區域，但是 hello 計算層則否，hello round trip 時間加上效能會有明顯的影響。</span><span class="sxs-lookup"><span data-stu-id="c30a0-207">If Redis used by an application fails over tooa different Azure region but hello compute tier does not, hello added round trip time would have a noticeable impact on performance.</span></span> <span data-ttu-id="c30a0-208">基於這個理由，我們希望 tooavoid Redis 失敗透過自動到期，tootransient 可用性問題。</span><span class="sxs-lookup"><span data-stu-id="c30a0-208">For this reason, we would like tooavoid Redis failing over automatically due tootransient availability issues.</span></span>

<span data-ttu-id="c30a0-209">Tooinitiate hello 容錯移轉，目前，當您需要 tooremove hello 地理複寫連結 hello Azure 入口網站中，並從 hello 連結之主要快取 （先前稱為連結） 的 toohello 次要將 hello Redis 用戶端中的 hello 連接端點快取。</span><span class="sxs-lookup"><span data-stu-id="c30a0-209">Currently, tooinitiate hello failover, you need tooremove hello Geo-replication link in hello Azure portal, and then change hello connection end-point in hello Redis client from hello primary linked cache toohello (formerly linked) secondary cache.</span></span> <span data-ttu-id="c30a0-210">當兩個快取會分離，hello hello 複本變成一般再次讀取-寫入快取並接受直接來自 Redis 用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="c30a0-210">When hello two caches are disassociated, hello replica becomes a regular read-write cache again and accepts requests directly from Redis clients.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c30a0-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c30a0-211">Next steps</span></span>

<span data-ttu-id="c30a0-212">深入了解 hello [Azure Redis 快取進階層](cache-premium-tier-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="c30a0-212">Learn more about hello [Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

