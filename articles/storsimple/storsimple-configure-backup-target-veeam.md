---
title: "StorSimple 8000 系列做為 Veeam 的備份目標 | Microsoft Docs"
description: "描述搭配 Veeam 的 StorSimple 備份目標組態。"
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 828cae6c2a0f00e03b6d24a2bd23f87ddad7b7c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a><span data-ttu-id="94087-103">使用 StorSimple 做為 Veeam 的備份目標</span><span class="sxs-lookup"><span data-stu-id="94087-103">StorSimple as a backup target with Veeam</span></span>

## <a name="overview"></a><span data-ttu-id="94087-104">概觀</span><span class="sxs-lookup"><span data-stu-id="94087-104">Overview</span></span>

<span data-ttu-id="94087-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="94087-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="94087-106">StorSimple 使用 Azure 儲存體帳戶做為內部部署解決方案的擴充功能，跨內部部署儲存體和雲端儲存體自動將資料分層，解決資料暴增的複雜性問題。</span><span class="sxs-lookup"><span data-stu-id="94087-106">StorSimple addresses the complexities of exponential data growth by using an Azure Storage account as an extension of the on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="94087-107">在本文，我們會討論 StorSimple 整合 Veeam，以及整合兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="94087-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span></span> <span data-ttu-id="94087-108">我們也會建議如何設定 Veeam 來與 StorSimple 進行最佳的整合。</span><span class="sxs-lookup"><span data-stu-id="94087-108">We also make recommendations on how to set up Veeam to best integrate with StorSimple.</span></span> <span data-ttu-id="94087-109">我們遵循 Veeam 的最佳作法，並聽從備份架構設計人員和管理員關於如何設定 Veeam 以符合個人備份需求和服務等級協定 (SLA) 的意見。</span><span class="sxs-lookup"><span data-stu-id="94087-109">We defer to Veeam best practices, backup architects, and administrators for the best way to set up Veeam to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="94087-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="94087-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="94087-111">我們假設基本元件和基礎結構都已正常運作，並準備好支援我們所描述的概念。</span><span class="sxs-lookup"><span data-stu-id="94087-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="94087-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="94087-112">Who should read this?</span></span>

<span data-ttu-id="94087-113">本文中的資訊最適合於了解儲存體、Windows Server 2012 R2、乙太網路、雲端服務和 Veeam 等知識的備份管理員、儲存體管理員及儲存體架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="94087-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="94087-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="94087-114">Supported versions</span></span>

-   <span data-ttu-id="94087-115">Veeam 9 及更新版本</span><span class="sxs-lookup"><span data-stu-id="94087-115">Veeam 9 and later versions</span></span>
-   [<span data-ttu-id="94087-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="94087-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="94087-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="94087-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="94087-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="94087-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="94087-119">為備份應用程式提供標準的本機儲存體，以做為快速備份目的地，而不需要做任何變更。</span><span class="sxs-lookup"><span data-stu-id="94087-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="94087-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="94087-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="94087-121">其雲端分層可與 Azure 雲端儲存體帳戶緊密整合，以使用經濟實惠的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="94087-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-122">It automatically provides offsite storage for disaster recovery.</span></span>


## <a name="key-concepts"></a><span data-ttu-id="94087-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="94087-123">Key concepts</span></span>

<span data-ttu-id="94087-124">如同任何儲存體解決方案，仔細評估解決方案的儲存體效能、SLA、變更速率及容量成長需求是成功與否的關鍵。</span><span class="sxs-lookup"><span data-stu-id="94087-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="94087-125">主要概念是藉由引進雲端層，對雲端的存取時間和輸送量就能對 StorSimple 執行其工作的能力扮演重要角色。</span><span class="sxs-lookup"><span data-stu-id="94087-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="94087-126">StorSimple 的設計目的是針對運作定義完善的使用中資料集 (熱資料) 的應用程式提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="94087-127">在此模型中，使用中的資料集儲存在本機層，其餘非使用中/冷/封存的資料集則分層儲存到雲端。</span><span class="sxs-lookup"><span data-stu-id="94087-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="94087-128">下圖說明這個模型。</span><span class="sxs-lookup"><span data-stu-id="94087-128">This model is represented in the following figure.</span></span> <span data-ttu-id="94087-129">幾乎是平坦的綠線表示儲存在 StorSimple 裝置本機層的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="94087-130">紅線則表示儲存在 StorSimple 解決方案所有各層的資料總量。</span><span class="sxs-lookup"><span data-stu-id="94087-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="94087-131">平坦綠線與呈指數形的紅色曲線之間的空間代表儲存在雲端的資料總量。</span><span class="sxs-lookup"><span data-stu-id="94087-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="94087-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="94087-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span></span>

<span data-ttu-id="94087-133">記住此架構，您會發現 StorSimple 非常適合做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="94087-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="94087-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="94087-134">You can use StorSimple to:</span></span>

-   <span data-ttu-id="94087-135">從本機使用中的資料集執行最頻繁的還原。</span><span class="sxs-lookup"><span data-stu-id="94087-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="94087-136">對於異地災害復原和較少進行還原的舊資料使用雲端。</span><span class="sxs-lookup"><span data-stu-id="94087-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="94087-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="94087-137">StorSimple benefits</span></span>

<span data-ttu-id="94087-138">StorSimple 提供的內部部署解決方案，可以不間斷存取內部部署和雲端儲存體，與 Microsoft Azure 緊密整合。</span><span class="sxs-lookup"><span data-stu-id="94087-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="94087-139">StorSimple 在具有固態裝置 (SSD) 和序列連接 SCSI (SAS) 儲存體的內部部署裝置與 Azure 儲存體之間使用自動分層。</span><span class="sxs-lookup"><span data-stu-id="94087-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="94087-140">自動分層將經常存取的資料保存在本機的 SSD 和 SAS 層。</span><span class="sxs-lookup"><span data-stu-id="94087-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="94087-141">而將不常存取的資料移到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="94087-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="94087-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="94087-143">獨家的重複資料刪除和壓縮演算法，使用雲端以達到前所未有的重複資料刪除層級</span><span class="sxs-lookup"><span data-stu-id="94087-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="94087-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="94087-144">High availability</span></span>
-   <span data-ttu-id="94087-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="94087-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="94087-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="94087-146">Azure integration</span></span>
-   <span data-ttu-id="94087-147">雲端中的資料會進行加密</span><span class="sxs-lookup"><span data-stu-id="94087-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="94087-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="94087-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="94087-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="94087-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="94087-150">StorSimple 會進行所有的壓縮及重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="94087-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="94087-151">它會在雲端、應用程式及檔案系統之間順暢地傳送和擷取資料。</span><span class="sxs-lookup"><span data-stu-id="94087-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="94087-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="94087-153">此外，您可以檢閱 [StorSimple 8000 系列技術規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94087-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="94087-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="94087-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="94087-155">Architecture overview</span></span>

<span data-ttu-id="94087-156">下表顯示裝置機型與架構的初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="94087-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="94087-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="94087-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="94087-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="94087-158">Storage capacity</span></span> | <span data-ttu-id="94087-159">8100</span><span class="sxs-lookup"><span data-stu-id="94087-159">8100</span></span> | <span data-ttu-id="94087-160">8600</span><span class="sxs-lookup"><span data-stu-id="94087-160">8600</span></span> |
|---|---|---|
| <span data-ttu-id="94087-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="94087-161">Local storage capacity</span></span> | <span data-ttu-id="94087-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="94087-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="94087-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="94087-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="94087-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="94087-164">Cloud storage capacity</span></span> | <span data-ttu-id="94087-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="94087-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="94087-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="94087-166">&gt; 500 TiB\*</span></span> |

<span data-ttu-id="94087-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="94087-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="94087-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="94087-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="94087-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="94087-169">Backup scenario</span></span>  | <span data-ttu-id="94087-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="94087-170">Local storage capacity</span></span>  | <span data-ttu-id="94087-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="94087-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="94087-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="94087-172">Primary backup</span></span>  | <span data-ttu-id="94087-173">最近的備份會儲存在本機儲存體供快速復原，以符合復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="94087-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="94087-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="94087-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="94087-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="94087-175">Secondary backup</span></span> | <span data-ttu-id="94087-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="94087-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="94087-177">N/A</span><span class="sxs-lookup"><span data-stu-id="94087-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="94087-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="94087-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="94087-179">在此案例中，備份應用程式會使用 StorSimple 磁碟區，做為備份的唯一儲存機制。</span><span class="sxs-lookup"><span data-stu-id="94087-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="94087-180">下圖說明解決方案架構，其中所有備份都使用 StorSimple 分層磁碟區進行備份和還原。</span><span class="sxs-lookup"><span data-stu-id="94087-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="94087-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="94087-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="94087-183">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="94087-184">備份伺服器將資料寫入 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="94087-185">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="94087-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="94087-186">快照集指令碼可觸發 StorSimple 雲端快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="94087-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="94087-187">備份伺服器會根據保留原則刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="94087-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="94087-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="94087-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="94087-189">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="94087-190">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="94087-191">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="94087-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="94087-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="94087-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="94087-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="94087-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="94087-194">下圖說明初始備份和還原以高效能磁碟區做為目標的架構。</span><span class="sxs-lookup"><span data-stu-id="94087-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="94087-195">這些備份會依照設定好的排程複製並封存至 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="94087-196">請務必調整您的高效能磁碟區大小，使其能夠處理保留原則、容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="94087-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="94087-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="94087-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="94087-199">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="94087-200">備份伺服器將資料寫入高效能儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="94087-201">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="94087-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="94087-202">備份伺服器會根據保留原則將備份複製到 StorSimple。</span><span class="sxs-lookup"><span data-stu-id="94087-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="94087-203">快照集指令碼可觸發 StorSimple 雲端快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="94087-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="94087-204">備份伺服器會根據保留原則刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="94087-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="94087-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="94087-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="94087-206">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="94087-207">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="94087-208">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="94087-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="94087-209">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="94087-209">Deploy the solution</span></span>

<span data-ttu-id="94087-210">部署解決方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="94087-210">Deploying the solution requires three steps:</span></span>

1. <span data-ttu-id="94087-211">準備網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="94087-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="94087-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="94087-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="94087-213">部署 Veeam。</span><span class="sxs-lookup"><span data-stu-id="94087-213">Deploy Veeam.</span></span>

<span data-ttu-id="94087-214">下列各節會詳細討論每個步驟。</span><span class="sxs-lookup"><span data-stu-id="94087-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="94087-215">設定網路</span><span class="sxs-lookup"><span data-stu-id="94087-215">Set up the network</span></span>

<span data-ttu-id="94087-216">因為 StorSimple 是與 Azure 雲端整合的解決方案，所以需要作用中並正常運作的 Azure 雲端連線。</span><span class="sxs-lookup"><span data-stu-id="94087-216">Because StorSimple is a solution that is integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="94087-217">此連線供雲端快照集、資料管理、中繼資料傳輸等操作使用，以及將較舊、較少存取的資料分層儲存到 Azure 雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="94087-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="94087-218">為了能以最佳方式執行解決方案，我們建議您遵循下列網路最佳作法︰</span><span class="sxs-lookup"><span data-stu-id="94087-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="94087-219">將 StorSimple 分層連接至 Azure 的連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="94087-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="94087-220">若要達到此目的，將必要的服務品質 (QoS) 層級套用至您的基礎結構參數，以符合您的 RPO 和復原時間目標 (RTO) SLA。</span><span class="sxs-lookup"><span data-stu-id="94087-220">Achieve this by applying the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="94087-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="94087-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="94087-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="94087-222">Deploy StorSimple</span></span>

<span data-ttu-id="94087-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-veeam"></a><span data-ttu-id="94087-224">部署 Veeam</span><span class="sxs-lookup"><span data-stu-id="94087-224">Deploy Veeam</span></span>

<span data-ttu-id="94087-225">如需 Veeam 的安裝最佳作法，請參閱 [Veeam 備份和複寫的最佳作法](https://bp.veeam.expert/)，以及 [Veeam 說明中心 (技術文件)](https://www.veeam.com/documentation-guides-datasheets.html) 的使用者指南。</span><span class="sxs-lookup"><span data-stu-id="94087-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read the user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="94087-226">設定解決方案</span><span class="sxs-lookup"><span data-stu-id="94087-226">Set up the solution</span></span>

<span data-ttu-id="94087-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="94087-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="94087-228">下列範例和建議說明最基本也最重要的實作。</span><span class="sxs-lookup"><span data-stu-id="94087-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="94087-229">此實作可能無法直接套用到您特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="94087-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="94087-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="94087-230">Set up StorSimple</span></span>

| <span data-ttu-id="94087-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="94087-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="94087-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="94087-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="94087-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="94087-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="94087-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="94087-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="94087-235">開啟備份目標。</span><span class="sxs-lookup"><span data-stu-id="94087-235">Turn on the backup target.</span></span> | <span data-ttu-id="94087-236">使用下列命令來開啟或關閉備份目標模式，以及取得狀態。</span><span class="sxs-lookup"><span data-stu-id="94087-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="94087-237">如需詳細資訊，請參閱[從遠端連接至 StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="94087-238">若要開啟備份模式︰`Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="94087-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="94087-239">若要關閉備份模式︰`Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="94087-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="94087-240">若要取得備份模式設定的目前狀態：`Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="94087-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="94087-241">為儲存備份資料的磁碟區建立一般的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="94087-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="94087-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="94087-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="94087-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="94087-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="94087-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="94087-245">建立大小盡可能接近預期使用量的磁碟區，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="94087-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="94087-246">如需有關如何調整磁碟區大小的資訊，請參閱[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="94087-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="94087-247">使用 StorSimple 分層磁碟區，並選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="94087-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="94087-249">為所有備份目標磁碟區建立唯一的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="94087-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="94087-250">StorSimple 備份原則定義磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="94087-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="94087-251">在快照集到期時停用排程。</span><span class="sxs-lookup"><span data-stu-id="94087-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="94087-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="94087-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="94087-253">設定主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="94087-253">Set up the host backup server storage</span></span>

<span data-ttu-id="94087-254">根據下列指導方針，設定主機備份伺服器儲存體︰</span><span class="sxs-lookup"><span data-stu-id="94087-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="94087-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)。</span><span class="sxs-lookup"><span data-stu-id="94087-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="94087-256">不支援合併磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-256">Spanned volumes are not supported.</span></span>
- <span data-ttu-id="94087-257">使用 64 KB 配置單位大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-257">Format your volumes using NTFS with 64-KB allocation unit size.</span></span>
- <span data-ttu-id="94087-258">將 StorSimple 磁碟區直接對應到 Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-258">Map the StorSimple volumes directly to the Veeam server.</span></span>
    - <span data-ttu-id="94087-259">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="94087-259">Use iSCSI for physical servers.</span></span>


## <a name="best-practices-for-storsimple-and-veeam"></a><span data-ttu-id="94087-260">StorSimple 和 Veeam 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="94087-260">Best practices for StorSimple and Veeam</span></span>

<span data-ttu-id="94087-261">根據下列幾節中的指導方針來設定您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="94087-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="94087-262">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="94087-262">Operating system best practices</span></span>

-   <span data-ttu-id="94087-263">停用 NTFS 檔案系統的 Windows Server 加密和重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="94087-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="94087-264">停用 StorSimple 磁碟區的 Windows Server 磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="94087-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="94087-265">停用 StorSimple 磁碟區的 Windows Server 索引。</span><span class="sxs-lookup"><span data-stu-id="94087-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="94087-266">在來源主機 (不是針對 StorSimple 磁碟區) 執行防毒軟體掃描。</span><span class="sxs-lookup"><span data-stu-id="94087-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="94087-267">在工作管理員中關閉預設 [Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94087-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="94087-268">利用下列其中一種方式來執行此作業：</span><span class="sxs-lookup"><span data-stu-id="94087-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="94087-269">在 Windows 工作排程器中關閉維護設定程式。</span><span class="sxs-lookup"><span data-stu-id="94087-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="94087-270">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94087-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="94087-271">下載 PsExec 之後，請以系統管理員身分執行 Windows PowerShell 並輸入：</span><span class="sxs-lookup"><span data-stu-id="94087-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="94087-272">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="94087-272">StorSimple best practices</span></span>

-   <span data-ttu-id="94087-273">確定 StorSimple 裝置已更新為 [Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="94087-274">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="94087-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="94087-275">針對 StorSimple 和備份伺服器之間的流量使用專用的 iSCSI 連線。</span><span class="sxs-lookup"><span data-stu-id="94087-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="94087-276">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="94087-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="94087-277">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="94087-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="veeam-best-practices"></a><span data-ttu-id="94087-278">Veeam 最佳作法</span><span class="sxs-lookup"><span data-stu-id="94087-278">Veeam best practices</span></span>

-   <span data-ttu-id="94087-279">Veeam 資料庫應在伺服器本機，而且不在 StorSimple 磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="94087-279">The Veeam database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="94087-280">在災害復原時，請將 Veeam 資料庫備份在 StorSimple 磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="94087-280">For disaster recovery, back up the Veeam database on a StorSimple volume.</span></span>
-   <span data-ttu-id="94087-281">我們支援此解決方案的 Veeam 完整和增量備份。</span><span class="sxs-lookup"><span data-stu-id="94087-281">We support Veeam full and incremental backups for this solution.</span></span> <span data-ttu-id="94087-282">我們建議您不要使用綜合和差異備份。</span><span class="sxs-lookup"><span data-stu-id="94087-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="94087-283">備份資料檔案最好只包含特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="94087-284">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="94087-284">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="94087-285">關閉作業驗證。</span><span class="sxs-lookup"><span data-stu-id="94087-285">Turn off job verification.</span></span> <span data-ttu-id="94087-286">如有必要，應該將驗證安排在最新的備份作業之後進行。</span><span class="sxs-lookup"><span data-stu-id="94087-286">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="94087-287">請務必了解這項作業會影響您的備份時間範圍。</span><span class="sxs-lookup"><span data-stu-id="94087-287">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="94087-288">開啟媒體預先配置。</span><span class="sxs-lookup"><span data-stu-id="94087-288">Turn on media pre-allocation.</span></span>
-   <span data-ttu-id="94087-289">確定已開啟平行處理。</span><span class="sxs-lookup"><span data-stu-id="94087-289">Be sure parallel processing is turned on.</span></span>
-   <span data-ttu-id="94087-290">關閉壓縮。</span><span class="sxs-lookup"><span data-stu-id="94087-290">Turn off compression.</span></span>
-   <span data-ttu-id="94087-291">關閉備份作業的重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="94087-291">Turn off deduplication on the backup job.</span></span>
-   <span data-ttu-id="94087-292">設定最佳化為 [LAN Target (LAN 目標)]。</span><span class="sxs-lookup"><span data-stu-id="94087-292">Set optimization to **LAN Target**.</span></span>
-   <span data-ttu-id="94087-293">開啟 [建立作用中的完整備份] \(每 2 週)。</span><span class="sxs-lookup"><span data-stu-id="94087-293">Turn on **Create active full backup** (every 2 weeks).</span></span>
-   <span data-ttu-id="94087-294">在備份儲存機制中，設定 [使用每個 VM 的備份檔案]。</span><span class="sxs-lookup"><span data-stu-id="94087-294">On the backup repository, set up **Use per-VM backup files**.</span></span>
-   <span data-ttu-id="94087-295">將 [每個作業使用多個上傳資料流] 設定為 **8** (最多允許 16 個)。</span><span class="sxs-lookup"><span data-stu-id="94087-295">Set **Use multiple upload streams per job** to **8** (a maximum of 16 is allowed).</span></span> <span data-ttu-id="94087-296">根據 StorSimple 裝置的 CPU 使用量向上或向下調整此數字。</span><span class="sxs-lookup"><span data-stu-id="94087-296">Adjust this number up or down based on CPU utilization on the StorSimple device.</span></span>

## <a name="retention-policies"></a><span data-ttu-id="94087-297">保留原則</span><span class="sxs-lookup"><span data-stu-id="94087-297">Retention policies</span></span>

<span data-ttu-id="94087-298">其中一種最常用的備份保留原則類型是三代循環 (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="94087-298">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="94087-299">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="94087-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="94087-300">此原則會造成六個 StorSimple 分層磁碟區︰一個磁碟區包含每週、每月和每年完整備份；其他五個磁碟區則儲存每日增量備份。</span><span class="sxs-lookup"><span data-stu-id="94087-300">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="94087-301">在下列範例中，我們使用 GFS 循環。</span><span class="sxs-lookup"><span data-stu-id="94087-301">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="94087-302">範例的假設如下：</span><span class="sxs-lookup"><span data-stu-id="94087-302">The example assumes the following:</span></span>

-   <span data-ttu-id="94087-303">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-303">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="94087-304">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="94087-304">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="94087-305">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="94087-305">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="94087-306">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="94087-306">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="94087-307">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="94087-307">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="94087-308">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="94087-308">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="94087-309">根據先前的假設，為每個月和每年的完整備份建立 26 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-309">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="94087-310">為每個每日增量備份建立 5 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-310">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="94087-311">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="94087-311">Backup type retention</span></span> | <span data-ttu-id="94087-312">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="94087-312">Size (TiB)</span></span> | <span data-ttu-id="94087-313">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="94087-313">GFS multiplier\*</span></span> | <span data-ttu-id="94087-314">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="94087-314">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="94087-315">每週完整</span><span class="sxs-lookup"><span data-stu-id="94087-315">Weekly full</span></span> | <span data-ttu-id="94087-316">1</span><span class="sxs-lookup"><span data-stu-id="94087-316">1</span></span> | <span data-ttu-id="94087-317">4</span><span class="sxs-lookup"><span data-stu-id="94087-317">4</span></span>  | <span data-ttu-id="94087-318">4</span><span class="sxs-lookup"><span data-stu-id="94087-318">4</span></span> |
| <span data-ttu-id="94087-319">每日增量</span><span class="sxs-lookup"><span data-stu-id="94087-319">Daily incremental</span></span> | <span data-ttu-id="94087-320">0.5</span><span class="sxs-lookup"><span data-stu-id="94087-320">0.5</span></span> | <span data-ttu-id="94087-321">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="94087-321">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="94087-322">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="94087-322">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="94087-323">每月完整</span><span class="sxs-lookup"><span data-stu-id="94087-323">Monthly full</span></span> | <span data-ttu-id="94087-324">1</span><span class="sxs-lookup"><span data-stu-id="94087-324">1</span></span> | <span data-ttu-id="94087-325">12</span><span class="sxs-lookup"><span data-stu-id="94087-325">12</span></span> | <span data-ttu-id="94087-326">12</span><span class="sxs-lookup"><span data-stu-id="94087-326">12</span></span> |
| <span data-ttu-id="94087-327">每年完整</span><span class="sxs-lookup"><span data-stu-id="94087-327">Yearly full</span></span> | <span data-ttu-id="94087-328">1</span><span class="sxs-lookup"><span data-stu-id="94087-328">1</span></span>  | <span data-ttu-id="94087-329">10</span><span class="sxs-lookup"><span data-stu-id="94087-329">10</span></span> | <span data-ttu-id="94087-330">10</span><span class="sxs-lookup"><span data-stu-id="94087-330">10</span></span> |
| <span data-ttu-id="94087-331">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="94087-331">GFS requirement</span></span> |   | <span data-ttu-id="94087-332">38</span><span class="sxs-lookup"><span data-stu-id="94087-332">38</span></span> |   |
| <span data-ttu-id="94087-333">其他配額</span><span class="sxs-lookup"><span data-stu-id="94087-333">Additional quota</span></span>  | <span data-ttu-id="94087-334">4</span><span class="sxs-lookup"><span data-stu-id="94087-334">4</span></span>  |   | <span data-ttu-id="94087-335">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="94087-335">42 total GFS requirement</span></span>  |
<span data-ttu-id="94087-336">\*GFS 乘數是您為了符合備份原則需求所需保護和保留的複本數目。</span><span class="sxs-lookup"><span data-stu-id="94087-336">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-veeam-storage"></a><span data-ttu-id="94087-337">設定 Veeam 儲存體</span><span class="sxs-lookup"><span data-stu-id="94087-337">Set up Veeam storage</span></span>

### <a name="to-set-up-veeam-storage"></a><span data-ttu-id="94087-338">若要設定 Veeam 儲存體</span><span class="sxs-lookup"><span data-stu-id="94087-338">To set up Veeam storage</span></span>

1.  <span data-ttu-id="94087-339">在 [Veeam 備份和複寫] 主控台的 [儲存機制工具] 中，移至 [備份基礎結構]。</span><span class="sxs-lookup"><span data-stu-id="94087-339">In the Veeam Backup and Replication console, in **Repository Tools**, go to **Backup Infrastructure**.</span></span> <span data-ttu-id="94087-340">以滑鼠右鍵按一下 [備份儲存裝置]，然後選取 [新增備份儲存裝置]。</span><span class="sxs-lookup"><span data-stu-id="94087-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  <span data-ttu-id="94087-342">在 [新增備份儲存機制] 對話方塊中，輸入儲存機制的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="94087-342">In the **New Backup Repository** dialog box, enter a name and description for the repository.</span></span> <span data-ttu-id="94087-343">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="94087-343">Select **Next**.</span></span>

    ![Veeam 管理主控台，名稱和描述頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  <span data-ttu-id="94087-345">選取 [Microsoft Windows Server] 做為類型。</span><span class="sxs-lookup"><span data-stu-id="94087-345">For the type, select **Microsoft Windows server**.</span></span> <span data-ttu-id="94087-346">選取 Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-346">Select the Veeam server.</span></span> <span data-ttu-id="94087-347">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="94087-347">Select **Next**.</span></span>

    ![Veeam 管理主控台，選取備份存放庫的類型](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  <span data-ttu-id="94087-349">若要指定 [位置]，請瀏覽並選取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-349">To specify **Location**, browse and select the volume.</span></span> <span data-ttu-id="94087-350">選取 [限制最大並行工作數:] 核取方塊並將此值設定為 **4**。</span><span class="sxs-lookup"><span data-stu-id="94087-350">Select the **Limit maximum concurrent tasks to:** check box and set the value to **4**.</span></span> <span data-ttu-id="94087-351">這可確保處理每個虛擬機器時，只會同時處理四個虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="94087-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span></span> <span data-ttu-id="94087-352">選取 [進階] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="94087-352">Select the **Advanced** button.</span></span>

    ![Veeam 管理主控台，選取磁碟區](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  <span data-ttu-id="94087-354">在 [儲存體相容性設定] 對話方塊中，選取 [使用每個 VM 的備份檔案] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-354">In the **Storage Compatibility Settings** dialog box, select the **Use per-VM backup files** check box.</span></span>

    ![Veeam 管理主控台，存放裝置相容性設定](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  <span data-ttu-id="94087-356">在 [新增備份儲存機制] 對話方塊中，選取 [在裝載伺服器上啟用 vPower NFS 服務 (建議)] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-356">In the **New Backup Repository** dialog box, select the **Enable vPower NFS service on the mount server (recommended)** check box.</span></span> <span data-ttu-id="94087-357">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="94087-357">Select **Next**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  <span data-ttu-id="94087-359">檢閱設定，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="94087-359">Review the settings, and then select **Next**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    <span data-ttu-id="94087-361">存放庫會加入 Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-361">A repository is added to the Veeam server.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="94087-362">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="94087-362">Set up StorSimple as a primary backup target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94087-363">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="94087-363">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="94087-364">下圖說明如何將典型的磁碟區對應到備份作業。</span><span class="sxs-lookup"><span data-stu-id="94087-364">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="94087-365">在此情況下，所有的每週備份會對應到星期六完整的磁碟，增量備份則會對應到星期一至星期五的增量磁碟。</span><span class="sxs-lookup"><span data-stu-id="94087-365">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="94087-366">所有備份和還原都是從 StorSimple 分層磁碟區進行。</span><span class="sxs-lookup"><span data-stu-id="94087-366">All the backups and restores are from a StorSimple tiered volume.</span></span>

![主要備份目標組態的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="94087-368">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="94087-368">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="94087-369">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="94087-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="94087-370">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="94087-370">Frequency/backup type</span></span> | <span data-ttu-id="94087-371">完整</span><span class="sxs-lookup"><span data-stu-id="94087-371">Full</span></span> | <span data-ttu-id="94087-372">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="94087-372">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="94087-373">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="94087-373">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="94087-374">星期六</span><span class="sxs-lookup"><span data-stu-id="94087-374">Saturday</span></span> | <span data-ttu-id="94087-375">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="94087-375">Monday-Friday</span></span> |
| <span data-ttu-id="94087-376">每月</span><span class="sxs-lookup"><span data-stu-id="94087-376">Monthly</span></span>  | <span data-ttu-id="94087-377">星期六</span><span class="sxs-lookup"><span data-stu-id="94087-377">Saturday</span></span>  |   |
| <span data-ttu-id="94087-378">每年</span><span class="sxs-lookup"><span data-stu-id="94087-378">Yearly</span></span> | <span data-ttu-id="94087-379">星期六</span><span class="sxs-lookup"><span data-stu-id="94087-379">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="94087-380">將 StorSimple 磁碟區指派給 Veeam 備份作業</span><span class="sxs-lookup"><span data-stu-id="94087-380">Assign StorSimple volumes to a Veeam backup job</span></span>

<span data-ttu-id="94087-381">在主要備份目標案例中，建立主要 Veeam StorSimple 磁碟區的每日作業。</span><span class="sxs-lookup"><span data-stu-id="94087-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span></span> <span data-ttu-id="94087-382">在第二個備份目標案例中，使用直接連接儲存體 (DAS)、網路連接儲存體 (NAS) 或簡單磁碟綁定 (JBOD) 儲存體，建立每日作業。</span><span class="sxs-lookup"><span data-stu-id="94087-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="94087-383">若要將 StorSimple 磁碟區指派給 Veeam 備份作業</span><span class="sxs-lookup"><span data-stu-id="94087-383">To assign StorSimple volumes to a Veeam backup job</span></span>

1.  <span data-ttu-id="94087-384">在 [Veeam 備份和複寫] 主控台中，選取 [備份和複寫]。</span><span class="sxs-lookup"><span data-stu-id="94087-384">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="94087-385">以滑鼠右鍵按一下 [備份]，然後根據您的環境選取 [VMware] 或 [Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="94087-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 管理主控台，新增備份作業](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  <span data-ttu-id="94087-387">在 [新增備份作業] 對話方塊中，輸入每日備份作業的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="94087-387">In the **New Backup Job** dialog box, enter a name and description for the daily backup job.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  <span data-ttu-id="94087-389">選取要備份到哪個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="94087-389">Select a virtual machine to back up to.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  <span data-ttu-id="94087-391">選取您想的 [備份 Proxy] 和 [備份儲存機制] 值。</span><span class="sxs-lookup"><span data-stu-id="94087-391">Select the values you want for **Backup proxy** and **Backup repository**.</span></span> <span data-ttu-id="94087-392">根據本機連接儲存體上環境的 RPO 和 RTO 定義，選取 [要保留在磁碟上的還原點] 的值。</span><span class="sxs-lookup"><span data-stu-id="94087-392">Select a value for **Restore points to keep on disk** according to the RPO and RTO definitions for your environment on locally attached storage.</span></span> <span data-ttu-id="94087-393">選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="94087-393">Select **Advanced**.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. <span data-ttu-id="94087-395">在 [進階設定]  對話方塊的 [備份] 索引標籤上，選取 [增量]。</span><span class="sxs-lookup"><span data-stu-id="94087-395">In the **Advanced Settings** dialog box, on the **Backup** tab, select **Incremental**.</span></span> <span data-ttu-id="94087-396">確定已清除 [定期建立綜合的完整備份] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-396">Be sure that the **Create synthetic full backups periodically** check box is cleared.</span></span> <span data-ttu-id="94087-397">選取 [定期建立作用中的完整備份] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-397">Select the **Create active full backups periodically** check box.</span></span> <span data-ttu-id="94087-398">在 [作用中的完整備份] 之下，針對星期六選取 [每週選取的日期] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-398">Under **Active full backup**, select the **Weekly on selected days** check box for Saturday.</span></span>

    ![Veeam 管理主控台，新增備份作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. <span data-ttu-id="94087-400">在 [儲存體] 索引標籤上，確定 [啟用內嵌重複資料刪除] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-400">On the **Storage** tab, make sure that the **Enable inline data deduplication** check box is cleared.</span></span> <span data-ttu-id="94087-401">選取 [排除分頁檔案區塊] 核取方塊，然後選取 [排除已刪除的檔案區塊] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-401">Select the **Exclude swap file blocks** check box, and select the **Exclude deleted file blocks** check box.</span></span> <span data-ttu-id="94087-402">將 [壓縮層級] 設定為 [無]。</span><span class="sxs-lookup"><span data-stu-id="94087-402">Set **Compression level** to **None**.</span></span> <span data-ttu-id="94087-403">若要獲得平衡的效能和重複資料刪除，請將 [儲存體最佳化] 設定為 [LAN 目標]。</span><span class="sxs-lookup"><span data-stu-id="94087-403">For balanced performance and deduplication, set **Storage optimization** to **LAN target**.</span></span> <span data-ttu-id="94087-404">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="94087-404">Select **OK**.</span></span>

    ![Veeam 管理主控台，新增備份作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    <span data-ttu-id="94087-406">如需 Veeam 重複資料刪除和壓縮設定的相關資訊，請參閱[資料壓縮和重複資料刪除](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html)。</span><span class="sxs-lookup"><span data-stu-id="94087-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span></span>

7.  <span data-ttu-id="94087-407">在 [編輯備份作業] 對話方塊中，您可以選取 [啟用應用程式感知處理] 核取方塊 (選用)。</span><span class="sxs-lookup"><span data-stu-id="94087-407">In the **Edit Backup Job** dialog box, you can select the **Enable application-aware processing** check box (optional).</span></span>

    ![Veeam 管理主控台，新增備份作業客體處理頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  <span data-ttu-id="94087-409">將排程設定為每天在您指定的時間執行一次。</span><span class="sxs-lookup"><span data-stu-id="94087-409">Set the schedule to run once daily, at a time you can specify.</span></span>

    ![Veeam 管理主控台，新增備份作業排程器頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="94087-411">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="94087-411">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="94087-412">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="94087-412">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="94087-413">在此模型中，您必須擁有儲存媒體 (而非 StorSimple) 做為暫時快取。</span><span class="sxs-lookup"><span data-stu-id="94087-413">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="94087-414">例如，您可以使用獨立磁碟容錯陣列 (RAID) 磁碟區來容納空間、輸入/輸出 (I/O) 和頻寬。</span><span class="sxs-lookup"><span data-stu-id="94087-414">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="94087-415">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="94087-415">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="94087-416">下圖說明一般短期保留的 (相對於伺服器) 本機磁碟區，以及長期保留的封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-416">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archive volumes.</span></span> <span data-ttu-id="94087-417">在此案例中，所有備份都會在 (相對於伺服器) 本機的 RAID 磁碟區上執行。</span><span class="sxs-lookup"><span data-stu-id="94087-417">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="94087-418">這些備份會定期複製並封存到封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-418">These backups are periodically duplicated and archived to an archive volume.</span></span> <span data-ttu-id="94087-419">請務必設定您 (相對於伺服器) 本機的 RAID 磁碟區，以便處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="94087-419">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="94087-421">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="94087-421">StorSimple as a secondary backup target GFS example</span></span>

<span data-ttu-id="94087-422">下表顯示如何設定備份以在本機和 StorSimple 磁碟上執行。</span><span class="sxs-lookup"><span data-stu-id="94087-422">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="94087-423">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="94087-423">It includes individual and total capacity requirements.</span></span>

| <span data-ttu-id="94087-424">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="94087-424">Backup type and retention</span></span> | <span data-ttu-id="94087-425">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="94087-425">Configured storage</span></span> | <span data-ttu-id="94087-426">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="94087-426">Size (TiB)</span></span> | <span data-ttu-id="94087-427">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="94087-427">GFS multiplier</span></span> | <span data-ttu-id="94087-428">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="94087-428">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="94087-429">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="94087-429">Week 1 (full and incremental)</span></span> |<span data-ttu-id="94087-430">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="94087-430">Local disk (short-term)</span></span>| <span data-ttu-id="94087-431">1</span><span class="sxs-lookup"><span data-stu-id="94087-431">1</span></span> | <span data-ttu-id="94087-432">1</span><span class="sxs-lookup"><span data-stu-id="94087-432">1</span></span> | <span data-ttu-id="94087-433">1</span><span class="sxs-lookup"><span data-stu-id="94087-433">1</span></span> |
| <span data-ttu-id="94087-434">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="94087-434">StorSimple weeks 2-4</span></span> |<span data-ttu-id="94087-435">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="94087-435">StorSimple disk (long-term)</span></span> | <span data-ttu-id="94087-436">1</span><span class="sxs-lookup"><span data-stu-id="94087-436">1</span></span> | <span data-ttu-id="94087-437">4</span><span class="sxs-lookup"><span data-stu-id="94087-437">4</span></span> | <span data-ttu-id="94087-438">4</span><span class="sxs-lookup"><span data-stu-id="94087-438">4</span></span> |
| <span data-ttu-id="94087-439">每月完整</span><span class="sxs-lookup"><span data-stu-id="94087-439">Monthly full</span></span> |<span data-ttu-id="94087-440">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="94087-440">StorSimple disk (long-term)</span></span> | <span data-ttu-id="94087-441">1</span><span class="sxs-lookup"><span data-stu-id="94087-441">1</span></span> | <span data-ttu-id="94087-442">12</span><span class="sxs-lookup"><span data-stu-id="94087-442">12</span></span> | <span data-ttu-id="94087-443">12</span><span class="sxs-lookup"><span data-stu-id="94087-443">12</span></span> |
| <span data-ttu-id="94087-444">每年完整</span><span class="sxs-lookup"><span data-stu-id="94087-444">Yearly full</span></span> |<span data-ttu-id="94087-445">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="94087-445">StorSimple disk (long-term)</span></span> | <span data-ttu-id="94087-446">1</span><span class="sxs-lookup"><span data-stu-id="94087-446">1</span></span> | <span data-ttu-id="94087-447">1</span><span class="sxs-lookup"><span data-stu-id="94087-447">1</span></span> | <span data-ttu-id="94087-448">1</span><span class="sxs-lookup"><span data-stu-id="94087-448">1</span></span> |
|<span data-ttu-id="94087-449">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="94087-449">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="94087-450">18*</span><span class="sxs-lookup"><span data-stu-id="94087-450">18*</span></span>|
<span data-ttu-id="94087-451">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="94087-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule"></a><span data-ttu-id="94087-452">GFS 範例排程</span><span class="sxs-lookup"><span data-stu-id="94087-452">GFS example schedule</span></span>

<span data-ttu-id="94087-453">每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="94087-453">GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="94087-454">週</span><span class="sxs-lookup"><span data-stu-id="94087-454">Week</span></span> | <span data-ttu-id="94087-455">完整</span><span class="sxs-lookup"><span data-stu-id="94087-455">Full</span></span> | <span data-ttu-id="94087-456">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="94087-456">Incremental day 1</span></span> | <span data-ttu-id="94087-457">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="94087-457">Incremental day 2</span></span> | <span data-ttu-id="94087-458">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="94087-458">Incremental day 3</span></span> | <span data-ttu-id="94087-459">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="94087-459">Incremental day 4</span></span> | <span data-ttu-id="94087-460">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="94087-460">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="94087-461">第 1 週</span><span class="sxs-lookup"><span data-stu-id="94087-461">Week 1</span></span> | <span data-ttu-id="94087-462">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-462">Local RAID volume</span></span>  | <span data-ttu-id="94087-463">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-463">Local RAID volume</span></span> | <span data-ttu-id="94087-464">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-464">Local RAID volume</span></span> | <span data-ttu-id="94087-465">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-465">Local RAID volume</span></span> | <span data-ttu-id="94087-466">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-466">Local RAID volume</span></span> | <span data-ttu-id="94087-467">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="94087-467">Local RAID volume</span></span> |
| <span data-ttu-id="94087-468">第 2 週</span><span class="sxs-lookup"><span data-stu-id="94087-468">Week 2</span></span> | <span data-ttu-id="94087-469">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="94087-469">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="94087-470">第 3 週</span><span class="sxs-lookup"><span data-stu-id="94087-470">Week 3</span></span> | <span data-ttu-id="94087-471">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="94087-471">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="94087-472">第 4 週</span><span class="sxs-lookup"><span data-stu-id="94087-472">Week 4</span></span> | <span data-ttu-id="94087-473">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="94087-473">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="94087-474">每月</span><span class="sxs-lookup"><span data-stu-id="94087-474">Monthly</span></span> | <span data-ttu-id="94087-475">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="94087-475">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="94087-476">每年</span><span class="sxs-lookup"><span data-stu-id="94087-476">Yearly</span></span> | <span data-ttu-id="94087-477">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="94087-477">StorSimple yearly</span></span>  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="94087-478">將 StorSimple 磁碟區指派給 Veeam 複製作業</span><span class="sxs-lookup"><span data-stu-id="94087-478">Assign StorSimple volumes to a Veeam copy job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="94087-479">若要將 StorSimple 磁碟區指派給 Veeam 複製作業</span><span class="sxs-lookup"><span data-stu-id="94087-479">To assign StorSimple volumes to a Veeam copy job</span></span>

1.  <span data-ttu-id="94087-480">在 [Veeam 備份和複寫] 主控台中，選取 [備份和複寫]。</span><span class="sxs-lookup"><span data-stu-id="94087-480">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="94087-481">以滑鼠右鍵按一下 [備份]，然後根據您的環境選取 [VMware] 或 [Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="94087-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  <span data-ttu-id="94087-483">在 [新增備份複製作業] 對話方塊中，輸入作業的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="94087-483">In the **New Backup Copy Job** dialog box, enter a name and description for the job.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  <span data-ttu-id="94087-485">選取您要處理的 VM。</span><span class="sxs-lookup"><span data-stu-id="94087-485">Select the VMs you want to process.</span></span> <span data-ttu-id="94087-486">選取 [從備份]，然後選取您稍早建立的每日備份。</span><span class="sxs-lookup"><span data-stu-id="94087-486">Select from backups, and then select the daily backup that you created earlier.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  <span data-ttu-id="94087-488">如有需要，從備份複製作業排除物件。</span><span class="sxs-lookup"><span data-stu-id="94087-488">Exclude objects from the backup copy job, if needed.</span></span>

5.  <span data-ttu-id="94087-489">選取您的備份儲存機制，並設定 [要保留的還原點] 的值。</span><span class="sxs-lookup"><span data-stu-id="94087-489">Select your backup repository, and set a value for **Restore points to keep**.</span></span> <span data-ttu-id="94087-490">務必選取 [保留下列還原點以供封存之用] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="94087-490">Be sure to select the **Keep the following restore points for archival purposes** check box.</span></span> <span data-ttu-id="94087-491">定義備份頻率，然後選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="94087-491">Define the backup frequency, and then select **Advanced**.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  <span data-ttu-id="94087-493">指定下列進階設定：</span><span class="sxs-lookup"><span data-stu-id="94087-493">Specify the following advanced settings:</span></span>

    * <span data-ttu-id="94087-494">在 [維護] 索引標籤上，關閉儲存體層級損毀保護。</span><span class="sxs-lookup"><span data-stu-id="94087-494">On the **Maintenance** tab, turn off storage level corruption guard.</span></span>

    ![Veeam 管理主控台，新增備份複製作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * <span data-ttu-id="94087-496">在 [儲存體] 索引標籤上，確定已關閉重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="94087-496">On the **Storage** tab, be sure that deduplication and compression are turned off.</span></span>

    ![Veeam 管理主控台，新增備份複製作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  <span data-ttu-id="94087-498">指定直接資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="94087-498">Specify that the data transfer is direct.</span></span>

8.  <span data-ttu-id="94087-499">根據您的需求定義備份複製時間範圍排程，然後完成精靈。</span><span class="sxs-lookup"><span data-stu-id="94087-499">Define the backup copy window schedule according to your needs, and then finish the wizard.</span></span>

<span data-ttu-id="94087-500">如需詳細資訊，請參閱[建立備份複製作業](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html)。</span><span class="sxs-lookup"><span data-stu-id="94087-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="94087-501">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="94087-501">StorSimple cloud snapshots</span></span>

<span data-ttu-id="94087-502">StorSimple 雲端快照集可保護位於 StorSimple 裝置中的資料。</span><span class="sxs-lookup"><span data-stu-id="94087-502">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="94087-503">建立雲端快照集相當於將本機備份磁碟送到異地場所。</span><span class="sxs-lookup"><span data-stu-id="94087-503">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="94087-504">如果您使用 Azure 異地備援儲存體，建立雲端快照集相當於將備份磁帶送到多個站台。</span><span class="sxs-lookup"><span data-stu-id="94087-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="94087-505">如果您需要在災害後還原裝置，可以讓另一個 StorSimple 裝置上線並執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="94087-505">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="94087-506">容錯移轉之後，您就可以從最新的雲端快照集 (以雲端速度) 存取資料。</span><span class="sxs-lookup"><span data-stu-id="94087-506">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="94087-507">下一節說明如何建立簡短指令碼，以在備份後處理期間啟動和刪除 StorSimple 雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="94087-507">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="94087-508">以手動方式或以程式設計方式建立的快照集不會遵循 StorSimple 快照集到期原則。</span><span class="sxs-lookup"><span data-stu-id="94087-508">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="94087-509">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="94087-509">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="94087-510">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="94087-510">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="94087-511">在刪除 StorSimple 快照集之前，請先仔細評估合規性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="94087-511">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="94087-512">如需有關如何執行備份後指令碼的詳細資訊，請參閱 Veeam 文件。</span><span class="sxs-lookup"><span data-stu-id="94087-512">For more information about how to run a post-backup script, see the Veeam documentation.</span></span>


### <a name="backup-lifecycle"></a><span data-ttu-id="94087-513">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="94087-513">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="94087-515">需求</span><span class="sxs-lookup"><span data-stu-id="94087-515">Requirements</span></span>

-   <span data-ttu-id="94087-516">執行指令碼的伺服器必須能夠存取 Azure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="94087-516">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="94087-517">使用者帳戶必須擁有必要的權限。</span><span class="sxs-lookup"><span data-stu-id="94087-517">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="94087-518">必須設定但不要啟用與 StorSimple 磁碟區相關聯的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="94087-518">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="94087-519">您需要 StorSimple 資源名稱、註冊金鑰、裝置名稱和備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="94087-519">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="94087-520">若要啟動或刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="94087-520">To start or delete a cloud snapshot</span></span>

1. <span data-ttu-id="94087-521">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="94087-521">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="94087-522">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94087-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3. <span data-ttu-id="94087-523">在 Azure 傳統入口網站中，[取得 StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key) 服務的資源名稱和註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="94087-523">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4. <span data-ttu-id="94087-524">在執行指令碼的伺服器上，以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="94087-524">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="94087-525">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="94087-525">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="94087-526">請記下備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="94087-526">Note the backup policy ID.</span></span>
5. <span data-ttu-id="94087-527">在記事本中，使用下列程式碼來建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="94087-527">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="94087-528">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="94087-528">Copy and paste this code snippet:</span></span>
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "The Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs to be deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
6. <span data-ttu-id="94087-529">若要將指令碼新增至您的備份作業，請編輯 Veeam 作業進階選項。</span><span class="sxs-lookup"><span data-stu-id="94087-529">To add the script to your backup job, edit your Veeam job advanced options.</span></span>

    ![Veeam 備份進階設定指令碼索引標籤](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

<span data-ttu-id="94087-531">我們建議您在每日備份作業結束時執行 StorSimple 雲端快照集集備份原則，做為後處理指令碼。</span><span class="sxs-lookup"><span data-stu-id="94087-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="94087-532">如需有關如何備份和還原備份應用程式環境以符合 RPO 和 RTO 的詳細資訊，請洽詢您的備份架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="94087-532">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="94087-533">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="94087-533">StorSimple as a restore source</span></span>

<span data-ttu-id="94087-534">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="94087-534">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="94087-535">還原已分層儲存到雲端的資料時，會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="94087-535">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="94087-536">如果是本機資料，則會以裝置的本機磁碟速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="94087-536">For local data, restores occur at the local disk speed of the device.</span></span>

<span data-ttu-id="94087-537">使用 Veeam，您可經由 Veeam 主控台中內建的瀏覽器檢視，透過 StorSimple 進行快速細微的檔案層級復原。</span><span class="sxs-lookup"><span data-stu-id="94087-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via the built-in explorer views in the Veeam console.</span></span> <span data-ttu-id="94087-538">您可以使用 Veeam 瀏覽器，從備份復原個別的項目，例如電子郵件訊息、Active Directory 物件和 SharePoint 項目。</span><span class="sxs-lookup"><span data-stu-id="94087-538">Use the Veeam Explorers to recover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span></span> <span data-ttu-id="94087-539">內部部署 VM 不需要中斷，就可以完成復原。</span><span class="sxs-lookup"><span data-stu-id="94087-539">The recovery can be done without on-premises VM disruption.</span></span> <span data-ttu-id="94087-540">您也可以進行 Azure SQL Database 和 Oracle Database 的時間點復原。</span><span class="sxs-lookup"><span data-stu-id="94087-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span></span> <span data-ttu-id="94087-541">Veeam 與 StorSimple 可以既快速又簡單地從 Azure 復原項目層級。</span><span class="sxs-lookup"><span data-stu-id="94087-541">Veeam and StorSimple make the process of item-level recovery from Azure fast and easy.</span></span> <span data-ttu-id="94087-542">如需有關如何執行還原的詳細資訊，請參閱 Veeam 文件：</span><span class="sxs-lookup"><span data-stu-id="94087-542">For information about how to perform a restore, see the Veeam documentation:</span></span>

- <span data-ttu-id="94087-543">若為 [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span><span class="sxs-lookup"><span data-stu-id="94087-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span></span>
- <span data-ttu-id="94087-544">若為 [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="94087-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span></span>
- <span data-ttu-id="94087-545">若為 [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="94087-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span></span>
- <span data-ttu-id="94087-546">若為 [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="94087-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span></span>
- <span data-ttu-id="94087-547">若為 [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="94087-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span></span>


## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="94087-548">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="94087-548">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="94087-549">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="94087-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="94087-550">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="94087-550">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="94087-551">下表列出常見的災害復原案例。</span><span class="sxs-lookup"><span data-stu-id="94087-551">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="94087-552">案例</span><span class="sxs-lookup"><span data-stu-id="94087-552">Scenario</span></span> | <span data-ttu-id="94087-553">影響</span><span class="sxs-lookup"><span data-stu-id="94087-553">Impact</span></span> | <span data-ttu-id="94087-554">如何復原</span><span class="sxs-lookup"><span data-stu-id="94087-554">How to recover</span></span> | <span data-ttu-id="94087-555">注意事項</span><span class="sxs-lookup"><span data-stu-id="94087-555">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="94087-556">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="94087-556">StorSimple device failure</span></span> | <span data-ttu-id="94087-557">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="94087-557">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="94087-558">更換故障的裝置，並執行 [StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-558">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="94087-559">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="94087-559">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="94087-560">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="94087-560">All operations are at cloud speeds.</span></span> <span data-ttu-id="94087-561">索引和目錄重新掃描程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層，而這可能會非常耗時。</span><span class="sxs-lookup"><span data-stu-id="94087-561">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="94087-562">Veeam 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="94087-562">Veeam server failure</span></span> | <span data-ttu-id="94087-563">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="94087-563">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="94087-564">重建備份伺服器，並執行 [Veeam 說明中心 (技術文件)](https://www.veeam.com/documentation-guides-datasheets.html) 中所述的資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="94087-564">Rebuild the backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>  | <span data-ttu-id="94087-565">您必須在災害復原站台重建或還原 Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="94087-565">You must rebuild or restore the Veeam server at the disaster recovery site.</span></span> <span data-ttu-id="94087-566">將資料庫還原到最新的點。</span><span class="sxs-lookup"><span data-stu-id="94087-566">Restore the database to the most recent point.</span></span> <span data-ttu-id="94087-567">如果還原的 Veeam 資料庫沒有與您最新的備份作業同步，就必須編製索引及編製目錄。</span><span class="sxs-lookup"><span data-stu-id="94087-567">If the restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="94087-568">重新掃描索引和目錄的程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層。</span><span class="sxs-lookup"><span data-stu-id="94087-568">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="94087-569">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="94087-569">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="94087-570">站台故障造成備份伺服器和 StorSimple 都遺失</span><span class="sxs-lookup"><span data-stu-id="94087-570">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="94087-571">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="94087-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="94087-572">先還原 StorSimple，然後再還原 Veeam。</span><span class="sxs-lookup"><span data-stu-id="94087-572">Restore StorSimple first, and then restore Veeam.</span></span> | <span data-ttu-id="94087-573">先還原 StorSimple，然後再還原 Veeam。</span><span class="sxs-lookup"><span data-stu-id="94087-573">Restore StorSimple first, and then restore Veeam.</span></span> <span data-ttu-id="94087-574">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="94087-574">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="94087-575">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="94087-575">All operations are at cloud speeds.</span></span> |


## <a name="references"></a><span data-ttu-id="94087-576">參考</span><span class="sxs-lookup"><span data-stu-id="94087-576">References</span></span>

<span data-ttu-id="94087-577">本文中參考下列文件︰</span><span class="sxs-lookup"><span data-stu-id="94087-577">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="94087-578">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="94087-578">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="94087-579">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="94087-579">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="94087-580">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="94087-580">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="94087-581">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="94087-581">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="94087-582">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94087-582">Next steps</span></span>

- <span data-ttu-id="94087-583">深入了解如何[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-583">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="94087-584">深入了解如何執行[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="94087-584">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
