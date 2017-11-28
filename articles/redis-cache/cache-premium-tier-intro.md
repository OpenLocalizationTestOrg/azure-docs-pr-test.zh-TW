---
title: "Azure Redis 快取進階層簡介 | Microsoft Docs"
description: "了解如何建立和管理高階層 Azure Redis Cache 執行個體的 Redis 永續性、Redis 叢集和 VNET 支援"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: c7a70e74f8b275ed9e10118b0ae9e81309f97ba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-redis-cache-premium-tier"></a><span data-ttu-id="d8f0a-103">Azure Redis Cache 高階層簡介</span><span class="sxs-lookup"><span data-stu-id="d8f0a-103">Introduction to the Azure Redis Cache Premium tier</span></span>
<span data-ttu-id="d8f0a-104">Azure Redis Cache 是一種分散式受管理快取，可提供超快速的資料存取，藉此協助您建置具高度延展性且快速回應的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-104">Azure Redis Cache is a distributed, managed cache that helps you build highly scalable and responsive applications by providing super-fast access to your data.</span></span> 

<span data-ttu-id="d8f0a-105">新的高階層是可供企業立即使用的層，其中包括所有標準層功能及其他優點，例如更佳的效能、更大的工作負載、災害復原、匯入/匯出和增強的安全性。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-105">The new Premium-tier is an Enterprise ready tier, which includes all the Standard-tier features and more, such as better performance, bigger workloads, disaster recovery, import/export, and enhanced security.</span></span> <span data-ttu-id="d8f0a-106">請繼續閱讀，以深入了解高階快取層的其他功能。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-106">Continue reading to learn more about the additional features of the Premium cache tier.</span></span>

## <a name="better-performance-compared-to-standard-or-basic-tier"></a><span data-ttu-id="d8f0a-107">效能優於標準或基本層。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-107">Better performance compared to Standard or Basic tier</span></span>
<span data-ttu-id="d8f0a-108">**效能優於標準或基本層。**</span><span class="sxs-lookup"><span data-stu-id="d8f0a-108">**Better performance over Standard or Basic tier.**</span></span> <span data-ttu-id="d8f0a-109">高階層中的快取是部署在擁有較快處理器的硬體上，因此效能優於基本或標準層。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-109">Caches in the Premium tier are deployed on hardware which has faster processors and gives better performance compared to the Basic or Standard Tier.</span></span> <span data-ttu-id="d8f0a-110">高階層快取的輸送量較高，延遲較低。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-110">Premium tier Caches have higher throughput and lower latencies.</span></span> 

<span data-ttu-id="d8f0a-111">**相較於標準層，高階層中相同大小的快取，其輸送量較高。**</span><span class="sxs-lookup"><span data-stu-id="d8f0a-111">**Throughput for the same sized Cache is higher in Premium as compared to Standard tier.**</span></span> <span data-ttu-id="d8f0a-112">例如：53 GB P4 (高階層) 快取的輸送量是每秒 250K 個要求，相較之下，C6 (標準層) 則只有 150K 個。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-112">For example, the throughput of a 53 GB P4 (Premium) cache is 250K requests per second as compared to 150K for C6 (Standard).</span></span>

<span data-ttu-id="d8f0a-113">如需高階快取的大小、輸送量和頻寬的詳細資訊，請參閱 [Azure Redis 快取常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="d8f0a-113">For more information about size, throughput, and bandwidth with premium caches, see [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>

## <a name="redis-data-persistence"></a><span data-ttu-id="d8f0a-114">Redis 資料永續性</span><span class="sxs-lookup"><span data-stu-id="d8f0a-114">Redis data persistence</span></span>
<span data-ttu-id="d8f0a-115">高階層可讓您將快取資料保存在 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-115">The Premium tier allows you to persist the cache data in an Azure Storage account.</span></span> <span data-ttu-id="d8f0a-116">在基本/標準快取中，所有資料都只儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-116">In a Basic/Standard cache all the data is stored only in memory.</span></span> <span data-ttu-id="d8f0a-117">如果基礎結構發生問題，資料可能會遺失。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-117">In case of underlying infrastructure issues there can be potential data loss.</span></span> <span data-ttu-id="d8f0a-118">建議您使用高階層中的 Redis 資料永續性功能，以提高資料遺失時的復原能力。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-118">We recommend using the Redis data persistence feature in the Premium tier to increase resiliency against data loss.</span></span> <span data-ttu-id="d8f0a-119">Azure Redis Cache 在 [Redis 永續性](http://redis.io/topics/persistence)中提供 RDB 和 AOF (即將推出) 選項。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-119">Azure Redis Cache offers RDB and AOF (coming soon) options in [Redis persistence](http://redis.io/topics/persistence).</span></span> 

<span data-ttu-id="d8f0a-120">如需設定永續性的相關指示，請參閱 [如何設定高階 Azure Redis Cache 的永續性](cache-how-to-premium-persistence.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-120">For instructions on configuring persistence, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

## <a name="redis-cluster"></a><span data-ttu-id="d8f0a-121">Redis 叢集</span><span class="sxs-lookup"><span data-stu-id="d8f0a-121">Redis cluster</span></span>
<span data-ttu-id="d8f0a-122">如果您想要建立大於 53 GB 的快取，或想跨多個 Redis 節點共用資料，可以使用高階層中的 Redis 叢集。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-122">If you want to create caches larger than 53 GB or want to shard data across multiple Redis nodes, you can use Redis clustering which is available in the Premium tier.</span></span> <span data-ttu-id="d8f0a-123">每個節點均包含一個 Azure 所管理的主要/複本快取組，可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-123">Each node consists of a primary/replica cache pair managed by Azure for high availability.</span></span> 

<span data-ttu-id="d8f0a-124">**Redis 叢集可提供最大的擴充能力和輸送量。**</span><span class="sxs-lookup"><span data-stu-id="d8f0a-124">**Redis clustering gives you maximum scale and throughput.**</span></span> <span data-ttu-id="d8f0a-125">當您增加叢集中的分區 (節點) 數目時，輸送量會呈線性增加。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-125">Throughput increases linearly as you increase the number of shards (nodes) in the cluster.</span></span> <span data-ttu-id="d8f0a-126">例如</span><span class="sxs-lookup"><span data-stu-id="d8f0a-126">Eg.</span></span> <span data-ttu-id="d8f0a-127">如果建立具有 10 個分區的 P4 叢集，則可用的輸送量為 250K *10 = 每秒 250 萬個要求。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-127">If you create a P4 cluster of 10 shards, then the available throughput is 250K *10 = 2.5 Million requests per second.</span></span> <span data-ttu-id="d8f0a-128">如需高階快取的大小、輸送量和頻寬等方面的詳細資訊，請參閱 [Azure Redis 快取常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-128">Please see the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<span data-ttu-id="d8f0a-129">若要開始使用叢集，請參閱 [如何設定高階 Azure Redis Cache 的叢集](cache-how-to-premium-clustering.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-129">To get started with clustering, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

## <a name="enhanced-security-and-isolation"></a><span data-ttu-id="d8f0a-130">增強的安全性和隔離</span><span class="sxs-lookup"><span data-stu-id="d8f0a-130">Enhanced security and isolation</span></span>
<span data-ttu-id="d8f0a-131">您可透過公用網際網路存取基本或標準層中建立的快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-131">Caches created in the Basic or Standard tier are accessible on the public internet.</span></span> <span data-ttu-id="d8f0a-132">對快取的存取權會受到存取金鑰的限制。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-132">Access to the Cache is restricted based on the access key.</span></span> <span data-ttu-id="d8f0a-133">若使用高階層，您可以進一步確保只有指定網路中的用戶端可以存取快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-133">With the Premium tier you can further ensure that only clients within a specified network can access the Cache.</span></span> <span data-ttu-id="d8f0a-134">您可以在 [Azure 虛擬網路 (VNet)](https://azure.microsoft.com/services/virtual-network/)中部署 Redis Cache。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-134">You can deploy Redis Cache in an [Azure Virtual Network (VNet)](https://azure.microsoft.com/services/virtual-network/).</span></span> <span data-ttu-id="d8f0a-135">您可以使用 VNet 的所有功能，例如子網路、存取控制原則和其他功能，進一步限制對 Redis 的存取權。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-135">You can use all the features of VNet such as subnets, access control policies, and other features to further restrict access to Redis.</span></span>

<span data-ttu-id="d8f0a-136">如需詳細資訊，請參閱 [如何設定高階 Azure Redis Cache 的虛擬網路支援](cache-how-to-premium-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-136">For more information, see [How to configure Virtual Network support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

## <a name="importexport"></a><span data-ttu-id="d8f0a-137">匯入/匯出</span><span class="sxs-lookup"><span data-stu-id="d8f0a-137">Import/Export</span></span>
<span data-ttu-id="d8f0a-138">匯入/匯出是 Azure Redis 快取資料管理作業，可讓您將資料匯入 Azure Redis 快取或將資料從 Azure Redis 快取匯出，方法是從進階快取將 Redis 快取資料庫 (RDB) 快照匯入和匯出至 Azure 儲存體帳戶中的分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-138">Import/Export is an Azure Redis Cache data management operation which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="d8f0a-139">這可讓您在不同的 Azure Redis 快取執行個體之間移轉，或在使用前將資料填入快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-139">This enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="d8f0a-140">匯入可以用來從執行雲端或環境的任何 Redis 伺服器 (包含在 Linux、Windows 上執行的 Redis，或任何雲端提供者，例如 Amazon Web Services 等) 引入 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-140">Import can be used to bring Redis compatible RDB file(s) from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="d8f0a-141">匯入資料是使用預先填入資料建立快取的輕鬆方式。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-141">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="d8f0a-142">在匯入程序期間，Azure Redis 快取會從 Azure 儲存體將 RDB 檔案載入記憶體，然後將金鑰插入快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-142">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

<span data-ttu-id="d8f0a-143">匯出可讓您將儲存在 Azure Redis 快取中的資料匯出至 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-143">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="d8f0a-144">您可以使用這項功能，將資料從一個 Azure Redis 快取執行個體移到另一個或其他 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-144">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="d8f0a-145">在匯出程序期間，會在裝載 Azure Redis 快取伺服器執行個體的 VM 上建立站存檔案，並將檔案上傳至指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-145">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="d8f0a-146">當匯出作業完成時的狀態為成功或失敗時，都會刪除暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-146">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

<span data-ttu-id="d8f0a-147">如需詳細資訊，請參閱 [如何將資料匯入 Azure Redis 快取與從其中匯出資料](cache-how-to-import-export-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-147">For more information, see [How to import data into and export data from Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>

## <a name="reboot"></a><span data-ttu-id="d8f0a-148">重新啟動</span><span class="sxs-lookup"><span data-stu-id="d8f0a-148">Reboot</span></span>
<span data-ttu-id="d8f0a-149">進階層可讓您依需求重新啟動快取的一或多個節點。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-149">The premium tier allows you to reboot one or more nodes of your cache on-demand.</span></span> <span data-ttu-id="d8f0a-150">這可讓您測試應用程式，以便在發生失敗時加以復原。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-150">This allows you to test your application for resiliency in the event of a failure.</span></span> <span data-ttu-id="d8f0a-151">您可以重新啟動下列節點。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-151">You can reboot the following nodes.</span></span>

* <span data-ttu-id="d8f0a-152">快取的主要節點</span><span class="sxs-lookup"><span data-stu-id="d8f0a-152">Master node of your cache</span></span>
* <span data-ttu-id="d8f0a-153">快取的從屬節點</span><span class="sxs-lookup"><span data-stu-id="d8f0a-153">Slave node of your cache</span></span>
* <span data-ttu-id="d8f0a-154">快取的主要和從屬節點</span><span class="sxs-lookup"><span data-stu-id="d8f0a-154">Both master and slave nodes of your cache</span></span>
* <span data-ttu-id="d8f0a-155">使用進階快取搭配叢集時，您可以針對快取中的個別分區重新啟動主要、從屬或這兩個節點</span><span class="sxs-lookup"><span data-stu-id="d8f0a-155">When using a premium cache with clustering, you can reboot the master, slave, or both nodes for individual shards in the cache</span></span>

<span data-ttu-id="d8f0a-156">如需詳細資訊，請參閱[重新啟動](cache-administration.md#reboot)和[重新啟動常見問題集](cache-administration.md#reboot-faq)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-156">For more information, see [Reboot](cache-administration.md#reboot) and [Reboot FAQ](cache-administration.md#reboot-faq).</span></span>

>[!NOTE]
><span data-ttu-id="d8f0a-157">重新啟動功能現在已對所有的 Azure Redis 快取層啟用。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-157">Reboot functionality is now enabled for all Azure Redis Cache tiers.</span></span>
>
>

## <a name="schedule-updates"></a><span data-ttu-id="d8f0a-158">更新排程</span><span class="sxs-lookup"><span data-stu-id="d8f0a-158">Schedule updates</span></span>
<span data-ttu-id="d8f0a-159">排程更新功能可讓您指定適用於快取的維護期間。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-159">The scheduled updates feature allows you to designate a maintenance window for your cache.</span></span> <span data-ttu-id="d8f0a-160">若指定了維護期間，即會在此期間進行任何 Redis 伺服器更新。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-160">When the maintenance window is specified, any Redis server updates are made during this window.</span></span> <span data-ttu-id="d8f0a-161">若要指定維護期間，請選取所需的天數，並指定每一天的維護期間開始小時。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-161">To designate a maintenance window, select the desired days and specify the maintenance window start hour for each day.</span></span> <span data-ttu-id="d8f0a-162">請注意，維護期間時間是 UTC。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-162">Note that the maintenance window time is in UTC.</span></span> 

<span data-ttu-id="d8f0a-163">如需詳細資訊，請參閱[排程更新](cache-administration.md#schedule-updates)和[排程更新常見問題集](cache-administration.md#schedule-updates-faq)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-163">For more information, see [Schedule updates](cache-administration.md#schedule-updates) and [Schedule updates FAQ](cache-administration.md#schedule-updates-faq).</span></span>

> [!NOTE]
> <span data-ttu-id="d8f0a-164">在排程維護期間，只會進行 Redis 伺服器更新。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-164">Only Redis server updates are made during the scheduled maintenance window.</span></span> <span data-ttu-id="d8f0a-165">維護期間不適用於 Azure 更新或 VM 作業系統的更新。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-165">The maintenance window does not apply to Azure updates or updates to the VM operating system.</span></span>
> 
> 

## <a name="geo-replication"></a><span data-ttu-id="d8f0a-166">異地複寫</span><span class="sxs-lookup"><span data-stu-id="d8f0a-166">Geo-replication</span></span>

<span data-ttu-id="d8f0a-167">**異地複寫**提供一個機制，可供連結兩個進階層 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-167">**Geo-replication** provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="d8f0a-168">其中一個快取被指定為主要連結快取，而另一個則為次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-168">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="d8f0a-169">次要連結快取會變成唯讀，而寫入主要快取的資料會複寫至次要連結快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-169">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="d8f0a-170">這項功能可用來跨 Azure 區域複寫快取。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-170">This functionality can be used to replicate a cache across Azure regions.</span></span>

<span data-ttu-id="d8f0a-171">如需詳細資訊，請參閱[如何設定 Azure Redis 快取的異地複寫](cache-how-to-geo-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-171">For more information, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>


## <a name="to-scale-to-the-premium-tier"></a><span data-ttu-id="d8f0a-172">調整為進階層</span><span class="sxs-lookup"><span data-stu-id="d8f0a-172">To scale to the premium tier</span></span>
<span data-ttu-id="d8f0a-173">若要調整為進階層，只需選擇 [變更定價層]  刀鋒視窗中的其中一個進階層。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-173">To scale to the premium tier, simply choose one of the premium tiers in the **Change pricing tier** blade.</span></span> <span data-ttu-id="d8f0a-174">您也可以使用 PowerShell 和 CLI 來將快取調整為進階層。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-174">You can also scale your cache to the premium tier using PowerShell and CLI.</span></span> <span data-ttu-id="d8f0a-175">如需逐步指示，請參閱[如何調整 Azure Redis 快取](cache-how-to-scale.md)和[如何自動化調整作業](cache-how-to-scale.md#how-to-automate-a-scaling-operation)。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-175">For step-by-step instructions, see [How to Scale Azure Redis Cache](cache-how-to-scale.md) and [How to automate a scaling operation](cache-how-to-scale.md#how-to-automate-a-scaling-operation).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8f0a-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8f0a-176">Next steps</span></span>
<span data-ttu-id="d8f0a-177">建立快取並探索高階層的新功能。</span><span class="sxs-lookup"><span data-stu-id="d8f0a-177">Create a cache and explore the new premium tier features.</span></span>

* [<span data-ttu-id="d8f0a-178">如何設定高階 Azure Redis Cache 的永續性</span><span class="sxs-lookup"><span data-stu-id="d8f0a-178">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
* [<span data-ttu-id="d8f0a-179">如何設定高階 Azure Redis Cache 的虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="d8f0a-179">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
* [<span data-ttu-id="d8f0a-180">如何設定高階 Azure Redis Cache 的叢集</span><span class="sxs-lookup"><span data-stu-id="d8f0a-180">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
* [<span data-ttu-id="d8f0a-181">如何將資料匯入 Azure Redis 快取與從其中匯出資料</span><span class="sxs-lookup"><span data-stu-id="d8f0a-181">How to import data into and export data from Azure Redis Cache</span></span>](cache-how-to-import-export-data.md)
* [<span data-ttu-id="d8f0a-182">如何管理 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d8f0a-182">How to administer Azure Redis Cache</span></span>](cache-administration.md)

