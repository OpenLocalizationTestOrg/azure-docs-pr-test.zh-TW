---
title: "StorSimple 8000 系列做為 NetBackup 的備份目標 | Microsoft Docs"
description: "描述搭配 Veritas NetBackup 的 StorSimple 備份目標組態。"
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
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: c9b3a259f9bc3e0561c7ba94e91edf7c8e0deabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a><span data-ttu-id="cc8dc-103">使用 StorSimple 做為 NetBackup 的備份目標</span><span class="sxs-lookup"><span data-stu-id="cc8dc-103">StorSimple as a backup target with NetBackup</span></span>

## <a name="overview"></a><span data-ttu-id="cc8dc-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cc8dc-104">Overview</span></span>

<span data-ttu-id="cc8dc-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="cc8dc-106">StorSimple 使用 Azure 儲存體帳戶做為內部部署解決方案的擴充功能，跨內部部署儲存體和雲端儲存體自動將資料分層，解決資料暴增的複雜性問題。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="cc8dc-107">在本文中，我們會討論 StorSimple 與 Veritas NetBackup 的整合，以及整合這兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span></span> <span data-ttu-id="cc8dc-108">我們也會建議如何設定 Veritas NetBackup 來與 StorSimple 進行最佳的整合。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-108">We also make recommendations on how to set up Veritas NetBackup to best integrate with StorSimple.</span></span> <span data-ttu-id="cc8dc-109">我們遵循 Veritas 的最佳作法，並聽從備份架構設計人員和管理員關於如何設定 Veritas NetBackup 以符合個人備份需求和服務等級協定 (SLA) 的意見。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Veritas NetBackup to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="cc8dc-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="cc8dc-111">我們假設基本元件和基礎結構都已正常運作，並準備好支援我們所描述的概念。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="cc8dc-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="cc8dc-112">Who should read this?</span></span>

<span data-ttu-id="cc8dc-113">本文中的資訊最適合於了解儲存體、Windows Server 2012 R2、乙太網路、雲端服務和 Veritas NetBackup 等知識的備份管理員、儲存體管理員及儲存體架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="cc8dc-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="cc8dc-114">Supported versions</span></span>

-   <span data-ttu-id="cc8dc-115">NetBackup 7.7x 及更新版本</span><span class="sxs-lookup"><span data-stu-id="cc8dc-115">NetBackup 7.7.x and later versions</span></span>
-   [<span data-ttu-id="cc8dc-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="cc8dc-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="cc8dc-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="cc8dc-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="cc8dc-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="cc8dc-119">為備份應用程式提供標準的本機儲存體，以做為快速備份目的地，而不需要做任何變更。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="cc8dc-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="cc8dc-121">其雲端分層可與 Azure 雲端儲存體帳戶緊密整合，以使用經濟實惠的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="cc8dc-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="cc8dc-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="cc8dc-123">Key concepts</span></span>

<span data-ttu-id="cc8dc-124">如同任何儲存體解決方案，仔細評估解決方案的儲存體效能、SLA、變更速率及容量成長需求是成功與否的關鍵。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="cc8dc-125">主要概念是藉由引進雲端層，對雲端的存取時間和輸送量就能對 StorSimple 執行其工作的能力扮演重要角色。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="cc8dc-126">StorSimple 的設計目的是針對運作定義完善的使用中資料集 (熱資料) 的應用程式提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="cc8dc-127">在此模型中，使用中的資料集儲存在本機層，其餘非使用中/冷/封存的資料集則分層儲存到雲端。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="cc8dc-128">下圖說明這個模型。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-128">This model is represented in the following figure.</span></span> <span data-ttu-id="cc8dc-129">幾乎是平坦的綠線表示儲存在 StorSimple 裝置本機層的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="cc8dc-130">紅線則表示儲存在 StorSimple 解決方案所有各層的資料總量。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="cc8dc-131">平坦綠線與呈指數形的紅色曲線之間的空間代表儲存在雲端的資料總量。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="cc8dc-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span></span>

<span data-ttu-id="cc8dc-133">記住此架構，您會發現 StorSimple 非常適合做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="cc8dc-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="cc8dc-135">從本機使用中的資料集執行最頻繁的還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="cc8dc-136">對於異地災害復原和較少進行還原的舊資料使用雲端。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="cc8dc-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="cc8dc-137">StorSimple benefits</span></span>

<span data-ttu-id="cc8dc-138">StorSimple 提供的內部部署解決方案，可以不間斷存取內部部署和雲端儲存體，與 Microsoft Azure 緊密整合。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="cc8dc-139">StorSimple 在具有固態裝置 (SSD) 和序列連接 SCSI (SAS) 儲存體的內部部署裝置與 Azure 儲存體之間使用自動分層。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="cc8dc-140">自動分層將經常存取的資料保存在本機的 SSD 和 SAS 層。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="cc8dc-141">而將不常存取的資料移到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="cc8dc-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="cc8dc-143">獨家的重複資料刪除和壓縮演算法，使用雲端以達到前所未有的重複資料刪除層級</span><span class="sxs-lookup"><span data-stu-id="cc8dc-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="cc8dc-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="cc8dc-144">High availability</span></span>
-   <span data-ttu-id="cc8dc-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="cc8dc-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="cc8dc-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="cc8dc-146">Azure integration</span></span>
-   <span data-ttu-id="cc8dc-147">雲端中的資料會進行加密</span><span class="sxs-lookup"><span data-stu-id="cc8dc-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="cc8dc-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="cc8dc-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="cc8dc-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="cc8dc-150">StorSimple 會進行所有的壓縮及重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="cc8dc-151">它會在雲端、應用程式及檔案系統之間順暢地傳送和擷取資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="cc8dc-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="cc8dc-153">此外，您可以檢閱 [StorSimple 8000 系列技術規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc8dc-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="cc8dc-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="cc8dc-155">Architecture overview</span></span>

<span data-ttu-id="cc8dc-156">下表顯示裝置機型與架構的初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="cc8dc-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="cc8dc-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="cc8dc-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-158">Storage capacity</span></span>       | <span data-ttu-id="cc8dc-159">8100</span><span class="sxs-lookup"><span data-stu-id="cc8dc-159">8100</span></span>          | <span data-ttu-id="cc8dc-160">8600</span><span class="sxs-lookup"><span data-stu-id="cc8dc-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="cc8dc-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-161">Local storage capacity</span></span> | <span data-ttu-id="cc8dc-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="cc8dc-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="cc8dc-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-164">Cloud storage capacity</span></span> | <span data-ttu-id="cc8dc-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="cc8dc-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="cc8dc-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="cc8dc-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="cc8dc-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="cc8dc-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="cc8dc-169">Backup scenario</span></span>  | <span data-ttu-id="cc8dc-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-170">Local storage capacity</span></span>  | <span data-ttu-id="cc8dc-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="cc8dc-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="cc8dc-172">Primary backup</span></span>  | <span data-ttu-id="cc8dc-173">最近的備份會儲存在本機儲存體供快速復原，以符合復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="cc8dc-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="cc8dc-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="cc8dc-175">Secondary backup</span></span> | <span data-ttu-id="cc8dc-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="cc8dc-177">N/A</span><span class="sxs-lookup"><span data-stu-id="cc8dc-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="cc8dc-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="cc8dc-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="cc8dc-179">在此案例中，備份應用程式會使用 StorSimple 磁碟區，做為備份的唯一儲存機制。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="cc8dc-180">下圖說明解決方案架構，其中所有備份都使用 StorSimple 分層磁碟區進行備份和還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="cc8dc-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="cc8dc-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="cc8dc-183">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="cc8dc-184">備份伺服器將資料寫入 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="cc8dc-185">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="cc8dc-186">快照集指令碼可觸發 StorSimple 快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-186">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="cc8dc-187">備份伺服器會根據保留原則刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="cc8dc-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="cc8dc-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="cc8dc-189">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="cc8dc-190">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="cc8dc-191">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="cc8dc-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="cc8dc-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="cc8dc-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="cc8dc-194">下圖說明初始備份和還原以高效能磁碟區做為目標的架構。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="cc8dc-195">這些備份會依照設定好的排程複製並封存至 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="cc8dc-196">請務必調整您的高效能磁碟區大小，使其能夠處理保留原則、容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-196">It's important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="cc8dc-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="cc8dc-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="cc8dc-199">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="cc8dc-200">備份伺服器將資料寫入高效能儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="cc8dc-201">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="cc8dc-202">備份伺服器會根據保留原則將備份複製到 StorSimple。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="cc8dc-203">快照集指令碼可觸發 StorSimple 快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-203">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="cc8dc-204">備份伺服器會根據保留原則來刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-204">The backup server deletes the expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="cc8dc-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="cc8dc-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="cc8dc-206">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="cc8dc-207">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="cc8dc-208">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="cc8dc-209">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="cc8dc-209">Deploy the solution</span></span>

<span data-ttu-id="cc8dc-210">部署此解決方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-210">Deploying this solution requires three steps:</span></span>
1. <span data-ttu-id="cc8dc-211">準備網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="cc8dc-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="cc8dc-213">部署 Veritas NetBackup。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-213">Deploy Veritas NetBackup.</span></span>

<span data-ttu-id="cc8dc-214">下列各節會詳細討論每個步驟。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="cc8dc-215">設定網路</span><span class="sxs-lookup"><span data-stu-id="cc8dc-215">Set up the network</span></span>

<span data-ttu-id="cc8dc-216">因為 StorSimple 是與 Azure 雲端整合的解決方案，所以需要作用中並正常運作的 Azure 雲端連線。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="cc8dc-217">此連線供雲端快照集、資料管理、中繼資料傳輸等操作使用，以及將較舊、較少存取的資料分層儲存到 Azure 雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="cc8dc-218">為了能以最佳方式執行解決方案，我們建議您遵循下列網路最佳作法︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="cc8dc-219">將 StorSimple 分層連接至 Azure 的連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-219">The link that connects the StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="cc8dc-220">若要達到此目的，將適當的服務品質 (QoS) 層級套用至您的基礎結構參數，以符合您的 RPO 和復原時間目標 (RTO) SLA。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-220">To achieve this, apply the proper Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>

-   <span data-ttu-id="cc8dc-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="cc8dc-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="cc8dc-222">Deploy StorSimple</span></span>

<span data-ttu-id="cc8dc-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-netbackup"></a><span data-ttu-id="cc8dc-224">部署 NetBackup</span><span class="sxs-lookup"><span data-stu-id="cc8dc-224">Deploy NetBackup</span></span>

<span data-ttu-id="cc8dc-225">如需逐步解說的 NetBackup 7.7.x 部署指南，請參閱 [NetBackup 7.7.x 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-225">For step-by-step NetBackup 7.7.x deployment guidance, see the [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="cc8dc-226">設定解決方案</span><span class="sxs-lookup"><span data-stu-id="cc8dc-226">Set up the solution</span></span>

<span data-ttu-id="cc8dc-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="cc8dc-228">下列範例和建議說明最基本也最重要的實作。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="cc8dc-229">此實作可能無法直接套用到您特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="cc8dc-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="cc8dc-230">Set up StorSimple</span></span>

| <span data-ttu-id="cc8dc-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="cc8dc-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="cc8dc-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="cc8dc-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="cc8dc-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="cc8dc-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="cc8dc-235">開啟備份目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-235">Turn on the backup target.</span></span> | <span data-ttu-id="cc8dc-236">使用下列命令來開啟或關閉備份目標模式，以及取得狀態。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="cc8dc-237">如需詳細資訊，請參閱[從遠端連接至 StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="cc8dc-238">若要開啟備份模式︰`Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="cc8dc-239">若要關閉備份模式︰`Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="cc8dc-240">若要取得備份模式設定的目前狀態：`Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="cc8dc-241">為儲存備份資料的磁碟區建立一般的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="cc8dc-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="cc8dc-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="cc8dc-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="cc8dc-245">建立大小盡可能接近預期使用量的磁碟區，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="cc8dc-246">如需有關如何調整磁碟區大小的資訊，請參閱[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="cc8dc-247">使用 StorSimple 分層磁碟區，並選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="cc8dc-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="cc8dc-249">為所有備份目標磁碟區建立唯一的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="cc8dc-250">StorSimple 備份原則定義磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="cc8dc-251">在快照集到期時停用排程。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="cc8dc-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="cc8dc-253">設定主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="cc8dc-253">Set up the host backup server storage</span></span>

<span data-ttu-id="cc8dc-254">根據下列指導方針，設定主機備份伺服器儲存體︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="cc8dc-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)；不支援合併磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span></span>
- <span data-ttu-id="cc8dc-256">使用 64 KB 配置大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-256">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="cc8dc-257">將 StorSimple 磁碟區直接對應到 NetBackup 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-257">Map the StorSimple volumes directly to the NetBackup server.</span></span>
    - <span data-ttu-id="cc8dc-258">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-258">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="cc8dc-259">虛擬伺服器請使用傳遞磁碟。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-259">Use pass-through disks for virtual servers.</span></span>


## <a name="best-practices-for-storsimple-and-netbackup"></a><span data-ttu-id="cc8dc-260">StorSimple 和 NetBackup 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="cc8dc-260">Best practices for StorSimple and NetBackup</span></span>

<span data-ttu-id="cc8dc-261">根據下列幾節中的指導方針來設定您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="cc8dc-262">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="cc8dc-262">Operating system best practices</span></span>

-   <span data-ttu-id="cc8dc-263">停用 NTFS 檔案系統的 Windows Server 加密和重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="cc8dc-264">停用 StorSimple 磁碟區的 Windows Server 磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="cc8dc-265">停用 StorSimple 磁碟區的 Windows Server 索引。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="cc8dc-266">在來源主機 (不是針對 StorSimple 磁碟區) 執行防毒軟體掃描。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="cc8dc-267">在工作管理員中關閉預設 [Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="cc8dc-268">利用下列其中一種方式來執行此作業：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="cc8dc-269">在 Windows 工作排程器中關閉維護設定程式。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="cc8dc-270">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="cc8dc-271">下載 PsExec 之後，請以系統管理員身分執行 Windows PowerShell 並輸入：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="cc8dc-272">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="cc8dc-272">StorSimple best practices</span></span>

-   <span data-ttu-id="cc8dc-273">確定 StorSimple 裝置已更新為 [Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="cc8dc-274">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="cc8dc-275">針對 StorSimple 和備份伺服器之間的流量使用專用的 iSCSI 連線。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="cc8dc-276">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="cc8dc-277">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="netbackup-best-practices"></a><span data-ttu-id="cc8dc-278">NetBackup 最佳作法</span><span class="sxs-lookup"><span data-stu-id="cc8dc-278">NetBackup best practices</span></span>

-   <span data-ttu-id="cc8dc-279">NetBackup 資料庫應在伺服器本機，而且不在 StorSimple 磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-279">The NetBackup database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="cc8dc-280">在災害復原時，請將 NetBackup 資料庫備份在 StorSimple 磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-280">For disaster recovery, back up the NetBackup database on a StorSimple volume.</span></span>
-   <span data-ttu-id="cc8dc-281">我們為此解決方案支援 NetBackup 完整和增量備份 (在 NetBackup 中也稱為差異化增量備份)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-281">We support NetBackup full and incremental backups (also referred to as differential incremental backups in NetBackup) for this solution.</span></span> <span data-ttu-id="cc8dc-282">建議您不要使用綜合和累積增量備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-282">We recommend that you do not use synthetic and cumulative incremental backups.</span></span>
-   <span data-ttu-id="cc8dc-283">備份資料檔案最好只包含特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="cc8dc-284">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-284">For example, no media appends across different jobs are allowed.</span></span>

<span data-ttu-id="cc8dc-285">如需實作這些需求的最新 NetBackup 設定和最佳作法，請參閱 NetBackup 文件 (網址為 [www.veritas.com](https://www.veritas.com))。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-285">For the latest NetBackup settings and best practices for implementing these requirements, see the NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span></span>


## <a name="retention-policies"></a><span data-ttu-id="cc8dc-286">保留原則</span><span class="sxs-lookup"><span data-stu-id="cc8dc-286">Retention policies</span></span>

<span data-ttu-id="cc8dc-287">其中一種最常用的備份保留原則類型是三代循環 (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-287">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="cc8dc-288">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="cc8dc-289">此原則會造成六個 StorSimple 分層磁碟區︰一個磁碟區包含每週、每月和每年完整備份；其他五個磁碟區則儲存每日增量備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-289">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="cc8dc-290">在下列範例中，我們使用 GFS 循環。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-290">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="cc8dc-291">範例的假設如下：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-291">The example assumes the following:</span></span>

-   <span data-ttu-id="cc8dc-292">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-292">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="cc8dc-293">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-293">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="cc8dc-294">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-294">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="cc8dc-295">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-295">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="cc8dc-296">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-296">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="cc8dc-297">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-297">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="cc8dc-298">根據先前的假設，為每個月和每年的完整備份建立 26 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-298">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="cc8dc-299">為每個每日增量備份建立 5 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-299">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="cc8dc-300">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="cc8dc-300">Backup type retention</span></span> | <span data-ttu-id="cc8dc-301">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-301">Size (TiB)</span></span> | <span data-ttu-id="cc8dc-302">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-302">GFS multiplier\*</span></span> | <span data-ttu-id="cc8dc-303">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-303">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="cc8dc-304">每週完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-304">Weekly full</span></span> | <span data-ttu-id="cc8dc-305">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-305">1</span></span> | <span data-ttu-id="cc8dc-306">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-306">4</span></span>  | <span data-ttu-id="cc8dc-307">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-307">4</span></span> |
| <span data-ttu-id="cc8dc-308">每日增量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-308">Daily incremental</span></span> | <span data-ttu-id="cc8dc-309">0.5</span><span class="sxs-lookup"><span data-stu-id="cc8dc-309">0.5</span></span> | <span data-ttu-id="cc8dc-310">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-310">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="cc8dc-311">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-311">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="cc8dc-312">每月完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-312">Monthly full</span></span> | <span data-ttu-id="cc8dc-313">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-313">1</span></span> | <span data-ttu-id="cc8dc-314">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-314">12</span></span> | <span data-ttu-id="cc8dc-315">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-315">12</span></span> |
| <span data-ttu-id="cc8dc-316">每年完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-316">Yearly full</span></span> | <span data-ttu-id="cc8dc-317">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-317">1</span></span>  | <span data-ttu-id="cc8dc-318">10</span><span class="sxs-lookup"><span data-stu-id="cc8dc-318">10</span></span> | <span data-ttu-id="cc8dc-319">10</span><span class="sxs-lookup"><span data-stu-id="cc8dc-319">10</span></span> |
| <span data-ttu-id="cc8dc-320">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="cc8dc-320">GFS requirement</span></span> |   | <span data-ttu-id="cc8dc-321">38</span><span class="sxs-lookup"><span data-stu-id="cc8dc-321">38</span></span> |   |
| <span data-ttu-id="cc8dc-322">其他配額</span><span class="sxs-lookup"><span data-stu-id="cc8dc-322">Additional quota</span></span>  | <span data-ttu-id="cc8dc-323">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-323">4</span></span>  |   | <span data-ttu-id="cc8dc-324">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-324">42 total GFS requirement</span></span>  |
<span data-ttu-id="cc8dc-325">\*GFS 乘數是您為了符合備份原則需求所需保護和保留的複本數目。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-325">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-netbackup-storage"></a><span data-ttu-id="cc8dc-326">設定 NetBackup 儲存體</span><span class="sxs-lookup"><span data-stu-id="cc8dc-326">Set up NetBackup storage</span></span>

### <a name="to-set-up-netbackup-storage"></a><span data-ttu-id="cc8dc-327">若要設定 NetBackup 儲存體</span><span class="sxs-lookup"><span data-stu-id="cc8dc-327">To set up NetBackup storage</span></span>

1.  <span data-ttu-id="cc8dc-328">在 NetBackup 管理主控台中，選取 [媒體和裝置管理] > [裝置] > [磁碟集區]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-328">In the NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span></span> <span data-ttu-id="cc8dc-329">在 [磁碟集區設定精靈] 中，選取 [AdvancedDisk] 儲存體伺服器類型，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-329">In the Disk Pool Configuration Wizard, select the storage server type **AdvancedDisk**, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，磁碟集區設定精靈](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  <span data-ttu-id="cc8dc-331">選取您的伺服器，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-331">Select your server, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，選取伺服器](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  <span data-ttu-id="cc8dc-333">選取您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-333">Select your StorSimple volume.</span></span>

    ![NetBackup 管理主控台，選取 StorSimple 磁碟區磁碟](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  <span data-ttu-id="cc8dc-335">輸入備份目標的名稱，然後選取 [下一步] >  [下一步] 完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-335">Enter a name for the backup target, and then select **Next** > **Next** to finish the wizard.</span></span>

5.  <span data-ttu-id="cc8dc-336">檢閱設定，然後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-336">Review the settings, and then select **Finish**.</span></span>

6.  <span data-ttu-id="cc8dc-337">在每項磁碟區指派作業結束時，變更存放裝置設定，以符合 [StorSimple 和 NetBackup 的最佳作法](#best-practices-for-storsimple-and-netbackup)中建議的設定。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-337">At the end of each volume assignment, change the storage device settings to match those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span></span>

7. <span data-ttu-id="cc8dc-338">重複步驟 1-6，直到完成指派 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span></span>

    ![NetBackup 管理主控台，磁碟設定](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="cc8dc-340">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="cc8dc-340">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="cc8dc-341">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-341">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="cc8dc-342">下圖說明如何將典型的磁碟區對應到備份作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-342">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="cc8dc-343">在此情況下，所有的每週備份會對應到星期六完整的磁碟，增量備份則會對應到星期一至星期五的增量磁碟。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-343">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="cc8dc-344">所有備份和還原都是從 StorSimple 分層磁碟區進行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-344">All the backups and restores are from a StorSimple tiered volume.</span></span>

![<span data-ttu-id="cc8dc-345">主要備份目標組態的邏輯圖</span><span class="sxs-lookup"><span data-stu-id="cc8dc-345">Primary backup target configuration logical diagram</span></span> ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="cc8dc-346">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="cc8dc-346">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="cc8dc-347">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="cc8dc-348">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="cc8dc-348">Frequency/backup type</span></span> | <span data-ttu-id="cc8dc-349">完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-349">Full</span></span> | <span data-ttu-id="cc8dc-350">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-350">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="cc8dc-351">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-351">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="cc8dc-352">星期六</span><span class="sxs-lookup"><span data-stu-id="cc8dc-352">Saturday</span></span> | <span data-ttu-id="cc8dc-353">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="cc8dc-353">Monday-Friday</span></span> |
| <span data-ttu-id="cc8dc-354">每月</span><span class="sxs-lookup"><span data-stu-id="cc8dc-354">Monthly</span></span>  | <span data-ttu-id="cc8dc-355">星期六</span><span class="sxs-lookup"><span data-stu-id="cc8dc-355">Saturday</span></span>  |   |
| <span data-ttu-id="cc8dc-356">每年</span><span class="sxs-lookup"><span data-stu-id="cc8dc-356">Yearly</span></span> | <span data-ttu-id="cc8dc-357">星期六</span><span class="sxs-lookup"><span data-stu-id="cc8dc-357">Saturday</span></span>  |   |   |

## <a name="assigning-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="cc8dc-358">將 StorSimple 磁碟區指派給 NetBackup 備份作業</span><span class="sxs-lookup"><span data-stu-id="cc8dc-358">Assigning StorSimple volumes to a NetBackup backup job</span></span>

<span data-ttu-id="cc8dc-359">下列程序假設 NetBackup 和目標主機已依據 NetBackup 代理程式指導方針進行設定。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-359">The following sequence assumes that NetBackup and the target host are configured in accordance with the NetBackup agent guidelines.</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="cc8dc-360">若要將 StorSimple 磁碟區指派給 NetBackup 備份作業</span><span class="sxs-lookup"><span data-stu-id="cc8dc-360">To assign StorSimple volumes to a NetBackup backup job</span></span>

1.  <span data-ttu-id="cc8dc-361">在 NetBackup 管理主控台中，選取 [NetBackup 管理]，以滑鼠右鍵按一下 [原則]，然後選取 [新增原則]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-361">In the NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span></span>

    ![NetBackup 管理主控台，建立新的原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  <span data-ttu-id="cc8dc-363">在 [新增原則] 對話方塊中，輸入原則的名稱，然後選取 [使用原則設定精靈] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-363">In the **Add a New Policy** dialog box, enter a name for the policy, and then select the **Use Policy Configuration Wizard** check box.</span></span> <span data-ttu-id="cc8dc-364">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-364">Select **OK**.</span></span>

    ![NetBackup 管理主控台，新增原則對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  <span data-ttu-id="cc8dc-366">在 [備份原則設定精靈] 中，選擇您想要的備份類型，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-366">In the Backup Policy Configuration Wizard, elect the backup type you want, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，選取備份類型](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  <span data-ttu-id="cc8dc-368">若要設定原則類型，請選取 [標準]，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-368">To set the policy type, select **Standard**, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，選取原則類型](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  <span data-ttu-id="cc8dc-370">選取您的主機，選取 [偵測用戶端作業系統] 核准方塊，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-370">Select your host, select the **Detect client operating system** check box, and then select **Add**.</span></span> <span data-ttu-id="cc8dc-371">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-371">Select **Next**.</span></span>

    ![NetBackup 管理主控台，列出新原則中的用戶端](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  <span data-ttu-id="cc8dc-373">選取您要備份的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-373">Select the drives you want to back up.</span></span>

    ![NetBackup 管理主控台，新原則的備份選取項目](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  <span data-ttu-id="cc8dc-375">選取符合您的備份循環需求的頻率和保留值。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-375">Select the frequency and retention values that meet your backup rotation requirements.</span></span>

    ![NetBackup 管理主控台，新原則的備份頻率和循環](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  <span data-ttu-id="cc8dc-377">選取 [下一步] > [下一步] > [完成]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-377">Select **Next** > **Next** > **Finish**.</span></span>  <span data-ttu-id="cc8dc-378">您可以在建立原則後修改排程。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-378">You can modify the schedule after the policy is created.</span></span>

9.  <span data-ttu-id="cc8dc-379">選擇展開您剛建立的原則，然後選取 [排程]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-379">Select to expand the policy you just created, and then select **Schedules**.</span></span>

    ![NetBackup 管理主控台，新原則的排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  <span data-ttu-id="cc8dc-381">以滑鼠右鍵按一下 [Differential-Inc]，選取 [複製到新的]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-381">Right-click **Differential-Inc**, select **Copy to new**, and then select **OK**.</span></span>

    ![NetBackup 管理主控台，將排程複製到新原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  <span data-ttu-id="cc8dc-383">以滑鼠右鍵按一下新建立的排程，然後選取 [變更]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-383">Right-click the newly created schedule, and then select **Change**.</span></span>

12.  <span data-ttu-id="cc8dc-384">在 [屬性] 索引標籤上，選取 [覆寫原則儲存體選取項目] 核取方塊，然後選取要儲存星期一增量備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-384">On the **Attributes** tab, select the **Override policy storage selection** check box, and then select the volume where Monday incremental backups go.</span></span>

    ![NetBackup 管理主控台，變更排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  <span data-ttu-id="cc8dc-386">在 [開始時間範圍] 索引標籤中選取備份的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-386">On the **Start Window** tab, select the time window for your backups.</span></span>

    ![NetBackup 管理主控台，變更開始時間範圍](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  <span data-ttu-id="cc8dc-388">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-388">Select **OK**.</span></span>

15.  <span data-ttu-id="cc8dc-389">針對每個增量備份重複步驟 10-14。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-389">Repeat steps 10-14 for each incremental backup.</span></span> <span data-ttu-id="cc8dc-390">針對您建立的每個備份，選取適當的磁碟區和排程。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-390">Select the appropriate volume and schedule for each backup you create.</span></span>

16.  <span data-ttu-id="cc8dc-391">在 [Differential-inc] 排程上按一下滑鼠右鍵，然後將它刪除。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-391">Right-click the **Differential-Inc** schedule, and then delete it.</span></span>

17.  <span data-ttu-id="cc8dc-392">修改您的完整排程，以符合您的備份需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-392">Modify your Full schedule to meet your backup needs.</span></span>

    ![NetBackup 管理主控台，變更完整排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  <span data-ttu-id="cc8dc-394">變更開始時間範圍。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-394">Change the start window.</span></span>

    ![NetBackup 管理主控台，變更開始時間範圍](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  <span data-ttu-id="cc8dc-396">最終的排程如下所示：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-396">The final schedule looks like this:</span></span>

    ![NetBackup 管理主控台，變更排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="cc8dc-398">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="cc8dc-398">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="cc8dc-399">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-399">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="cc8dc-400">在此模型中，您必須擁有儲存媒體 (而非 StorSimple) 做為暫時快取。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-400">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="cc8dc-401">例如，您可以使用獨立磁碟容錯陣列 (RAID) 磁碟區來容納空間、輸入/輸出 (I/O) 和頻寬。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-401">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="cc8dc-402">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-402">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="cc8dc-403">下圖說明一般短期保留的 (相對於伺服器) 本機磁碟區，以及長期保留的封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-403">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="cc8dc-404">在此案例中，所有備份都會在 (相對於伺服器) 本機的 RAID 磁碟區上執行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-404">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="cc8dc-405">這些備份會定期複製並封存到封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-405">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="cc8dc-406">請務必設定您 (相對於伺服器) 本機的 RAID 磁碟區，以便處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-406">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="cc8dc-407">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="cc8dc-407">StorSimple as a secondary backup target GFS example</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

<span data-ttu-id="cc8dc-409">下表顯示如何設定備份以在本機和 StorSimple 磁碟上執行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-409">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="cc8dc-410">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-410">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="cc8dc-411">備份設定和容量需求</span><span class="sxs-lookup"><span data-stu-id="cc8dc-411">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="cc8dc-412">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="cc8dc-412">Backup type and retention</span></span> | <span data-ttu-id="cc8dc-413">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="cc8dc-413">Configured storage</span></span> | <span data-ttu-id="cc8dc-414">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-414">Size (TiB)</span></span> | <span data-ttu-id="cc8dc-415">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="cc8dc-415">GFS multiplier</span></span> | <span data-ttu-id="cc8dc-416">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-416">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="cc8dc-417">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-417">Week 1 (full and incremental)</span></span> |<span data-ttu-id="cc8dc-418">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-418">Local disk (short-term)</span></span>| <span data-ttu-id="cc8dc-419">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-419">1</span></span> | <span data-ttu-id="cc8dc-420">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-420">1</span></span> | <span data-ttu-id="cc8dc-421">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-421">1</span></span> |
| <span data-ttu-id="cc8dc-422">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-422">StorSimple weeks 2-4</span></span> |<span data-ttu-id="cc8dc-423">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-423">StorSimple disk (long-term)</span></span> | <span data-ttu-id="cc8dc-424">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-424">1</span></span> | <span data-ttu-id="cc8dc-425">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-425">4</span></span> | <span data-ttu-id="cc8dc-426">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-426">4</span></span> |
| <span data-ttu-id="cc8dc-427">每月完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-427">Monthly full</span></span> |<span data-ttu-id="cc8dc-428">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-428">StorSimple disk (long-term)</span></span> | <span data-ttu-id="cc8dc-429">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-429">1</span></span> | <span data-ttu-id="cc8dc-430">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-430">12</span></span> | <span data-ttu-id="cc8dc-431">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-431">12</span></span> |
| <span data-ttu-id="cc8dc-432">每年完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-432">Yearly full</span></span> |<span data-ttu-id="cc8dc-433">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-433">StorSimple disk (long-term)</span></span> | <span data-ttu-id="cc8dc-434">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-434">1</span></span> | <span data-ttu-id="cc8dc-435">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-435">1</span></span> | <span data-ttu-id="cc8dc-436">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-436">1</span></span> |
|<span data-ttu-id="cc8dc-437">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="cc8dc-437">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="cc8dc-438">18*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-438">18*</span></span>|
<span data-ttu-id="cc8dc-439">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="cc8dc-440">GFS 範例排程：每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="cc8dc-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="cc8dc-441">週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-441">Week</span></span> | <span data-ttu-id="cc8dc-442">完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-442">Full</span></span> | <span data-ttu-id="cc8dc-443">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-443">Incremental day 1</span></span> | <span data-ttu-id="cc8dc-444">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-444">Incremental day 2</span></span> | <span data-ttu-id="cc8dc-445">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-445">Incremental day 3</span></span> | <span data-ttu-id="cc8dc-446">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-446">Incremental day 4</span></span> | <span data-ttu-id="cc8dc-447">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-447">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="cc8dc-448">第 1 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-448">Week 1</span></span> | <span data-ttu-id="cc8dc-449">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-449">Local RAID volume</span></span>  | <span data-ttu-id="cc8dc-450">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-450">Local RAID volume</span></span> | <span data-ttu-id="cc8dc-451">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-451">Local RAID volume</span></span> | <span data-ttu-id="cc8dc-452">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-452">Local RAID volume</span></span> | <span data-ttu-id="cc8dc-453">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-453">Local RAID volume</span></span> | <span data-ttu-id="cc8dc-454">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="cc8dc-454">Local RAID volume</span></span> |
| <span data-ttu-id="cc8dc-455">第 2 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-455">Week 2</span></span> | <span data-ttu-id="cc8dc-456">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-456">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="cc8dc-457">第 3 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-457">Week 3</span></span> | <span data-ttu-id="cc8dc-458">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-458">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="cc8dc-459">第 4 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-459">Week 4</span></span> | <span data-ttu-id="cc8dc-460">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="cc8dc-460">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="cc8dc-461">每月</span><span class="sxs-lookup"><span data-stu-id="cc8dc-461">Monthly</span></span> | <span data-ttu-id="cc8dc-462">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="cc8dc-462">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="cc8dc-463">每年</span><span class="sxs-lookup"><span data-stu-id="cc8dc-463">Yearly</span></span> | <span data-ttu-id="cc8dc-464">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="cc8dc-464">StorSimple yearly</span></span>  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="cc8dc-465">將 StorSimple 磁碟區指派給 NetBackup 封存和重複資料刪除作業</span><span class="sxs-lookup"><span data-stu-id="cc8dc-465">Assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

<span data-ttu-id="cc8dc-466">NetBackup 提供各式各樣的儲存體和媒體管理選項，所以我們建議您洽詢 Veritas 或 NetBackup 架構設計人員，以正確評估您的儲存體生命週期原則 (SLP) 需求。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect to properly assess your storage lifecycle policy (SLP) requirements.</span></span>

<span data-ttu-id="cc8dc-467">在您定義初始磁碟集區之後，您需要定義額外三個儲存體生命週期原則 (總共四個原則)︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-467">After you've defined the initial disk pools, you need to define three additional storage lifecycle policies, for a total of four policies:</span></span>
* <span data-ttu-id="cc8dc-468">LocalRAIDVolume</span><span class="sxs-lookup"><span data-stu-id="cc8dc-468">LocalRAIDVolume</span></span>
* <span data-ttu-id="cc8dc-469">StorSimpleWeek2-4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-469">StorSimpleWeek2-4</span></span>
* <span data-ttu-id="cc8dc-470">StorSimpleMonthlyFulls</span><span class="sxs-lookup"><span data-stu-id="cc8dc-470">StorSimpleMonthlyFulls</span></span>
* <span data-ttu-id="cc8dc-471">StorSimpleYearlyFulls</span><span class="sxs-lookup"><span data-stu-id="cc8dc-471">StorSimpleYearlyFulls</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="cc8dc-472">若要將 StorSimple 磁碟區指派給 NetBackup 封存和重複資料刪除作業</span><span class="sxs-lookup"><span data-stu-id="cc8dc-472">To assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

1.  <span data-ttu-id="cc8dc-473">在 NetBackup 管理主控台中，選取 [儲存體] > [儲存體生命週期原則] > [新增儲存體生命週期原則]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-473">In the NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span></span>

    ![NetBackup 管理主控台，新增儲存體生命週期原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  <span data-ttu-id="cc8dc-475">輸入快照集的名稱，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-475">Enter a name for the snapshot, and then select **Add**.</span></span>

3.  <span data-ttu-id="cc8dc-476">在 [新增作業] 對話方塊的 [屬性] 索引標籤上，針對 [作業] 選取[備份]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-476">In the **New Operation** dialog box, on the **Properties** tab, for **Operation**, select **Backup**.</span></span> <span data-ttu-id="cc8dc-477">選取您想要的 [目的地儲存體]、[保留類型] 和 [保留期限] 值。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-477">Select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span> <span data-ttu-id="cc8dc-478">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-478">Select **OK**.</span></span>

    ![NetBackup 管理主控台，新增作業對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    <span data-ttu-id="cc8dc-480">這會定義第一個備份作業和儲存機制。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-480">This defines the first backup operation and repository.</span></span>

4.  <span data-ttu-id="cc8dc-481">選擇反白顯示先前的作業，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-481">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="cc8dc-482">在 [變更儲存體作業] 對話方塊方塊中，選取您想要的 [目的地儲存體]、[保留類型] 和 [保留期限] 值。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-482">In the **Change Storage Operation** dialog box, select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span>

    ![NetBackup 管理主控台，變更儲存體作業對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  <span data-ttu-id="cc8dc-484">選擇反白顯示先前的作業，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-484">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="cc8dc-485">在 [新增儲存體生命週期原則] 對話方塊中，新增一整年的每月備份。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-485">In the **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span></span>

    ![NetBackup 管理主控台，新增儲存體生命週期原則對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  <span data-ttu-id="cc8dc-487">重複步驟 4-5，直到您已建立您需要的全方位 SLP 保留原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-487">Repeat steps 4-5 until you've created the comprehensive SLP retention policy that you need.</span></span>

    ![NetBackup 管理主控台，在 [新增儲存體生命週期原則] 對話方塊中新增原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  <span data-ttu-id="cc8dc-489">當您完成定義 SLP 保留原則時，請遵循[將 StorSimple 磁碟區指派給 NetBackup 備份作業](#assigning-storsimple-volumes-to-a-netbackup-backup-job)中詳述的步驟，以在 [原則] 之下定義備份原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following the steps detailed in [Assigning StorSimple volumes to a NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span></span>

8.  <span data-ttu-id="cc8dc-490">在 [排程] 之下的 [變更排程] 對話方塊中，以滑鼠右鍵按一下 [完整]，然後選取 [變更]。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-490">Under **Schedules**, in the **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span></span>

    ![NetBackup 管理主控台，變更排程對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  <span data-ttu-id="cc8dc-492">選取 [覆寫原則儲存體選取項目] 核取方塊，然後選取您在步驟 1-6 中建立的 SLP 保留原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-492">Select the **Override policy storage selection** check box, and then select the SLP retention policy that you created in steps 1-6.</span></span>

    ![NetBackup 管理主控台，複寫原則儲存體選取項目](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  <span data-ttu-id="cc8dc-494">許取 [確定]，然後重複執行增量備份排程。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-494">Select **OK**, and then repeat for the incremental backup schedule.</span></span>

    ![NetBackup 管理主控台，增量備份的 [變更排程] 對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| <span data-ttu-id="cc8dc-496">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="cc8dc-496">Backup type retention</span></span> | <span data-ttu-id="cc8dc-497">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-497">Size (TiB)</span></span> | <span data-ttu-id="cc8dc-498">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="cc8dc-498">GFS multiplier\*</span></span> | <span data-ttu-id="cc8dc-499">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-499">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="cc8dc-500">每週完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-500">Weekly full</span></span> |  <span data-ttu-id="cc8dc-501">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-501">1</span></span>  |  <span data-ttu-id="cc8dc-502">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-502">4</span></span> | <span data-ttu-id="cc8dc-503">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-503">4</span></span>  |
| <span data-ttu-id="cc8dc-504">每日增量</span><span class="sxs-lookup"><span data-stu-id="cc8dc-504">Daily incremental</span></span>  | <span data-ttu-id="cc8dc-505">0.5</span><span class="sxs-lookup"><span data-stu-id="cc8dc-505">0.5</span></span>  | <span data-ttu-id="cc8dc-506">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-506">20 (cycles are equal to the number of weeks per month)</span></span> | <span data-ttu-id="cc8dc-507">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-507">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="cc8dc-508">每月完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-508">Monthly full</span></span>  | <span data-ttu-id="cc8dc-509">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-509">1</span></span> | <span data-ttu-id="cc8dc-510">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-510">12</span></span> | <span data-ttu-id="cc8dc-511">12</span><span class="sxs-lookup"><span data-stu-id="cc8dc-511">12</span></span> |
| <span data-ttu-id="cc8dc-512">每年完整</span><span class="sxs-lookup"><span data-stu-id="cc8dc-512">Yearly full</span></span> | <span data-ttu-id="cc8dc-513">1</span><span class="sxs-lookup"><span data-stu-id="cc8dc-513">1</span></span>  | <span data-ttu-id="cc8dc-514">10</span><span class="sxs-lookup"><span data-stu-id="cc8dc-514">10</span></span> | <span data-ttu-id="cc8dc-515">10</span><span class="sxs-lookup"><span data-stu-id="cc8dc-515">10</span></span> |
| <span data-ttu-id="cc8dc-516">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="cc8dc-516">GFS requirement</span></span>  |     |     | <span data-ttu-id="cc8dc-517">38</span><span class="sxs-lookup"><span data-stu-id="cc8dc-517">38</span></span> |
| <span data-ttu-id="cc8dc-518">其他配額</span><span class="sxs-lookup"><span data-stu-id="cc8dc-518">Additional quota</span></span>  | <span data-ttu-id="cc8dc-519">4</span><span class="sxs-lookup"><span data-stu-id="cc8dc-519">4</span></span>  |    | <span data-ttu-id="cc8dc-520">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-520">42 total GFS requirement</span></span> |
<span data-ttu-id="cc8dc-521">\*GFS 乘數是您為了符合備份原則需求所需保護和保留的複本數目。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-521">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="cc8dc-522">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="cc8dc-522">StorSimple cloud snapshots</span></span>

<span data-ttu-id="cc8dc-523">StorSimple 雲端快照集可保護位於 StorSimple 裝置中的資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-523">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="cc8dc-524">建立雲端快照集相當於將本機備份磁碟送到異地場所。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-524">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="cc8dc-525">如果您使用 Azure 異地備援儲存體，建立雲端快照集相當於將備份磁帶送到多個站台。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="cc8dc-526">如果您需要在災害後還原裝置，可以讓另一個 StorSimple 裝置上線並執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-526">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="cc8dc-527">容錯移轉之後，您就可以從最新的雲端快照集 (以雲端速度) 存取資料。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-527">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="cc8dc-528">下一節說明如何建立簡短指令碼，以在備份後處理期間啟動和刪除 StorSimple 雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-528">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8dc-529">以手動方式或以程式設計方式建立的快照集不會遵循 StorSimple 快照集到期原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-529">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="cc8dc-530">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-530">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="cc8dc-531">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="cc8dc-531">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="cc8dc-532">在刪除 StorSimple 快照集之前，請先仔細評估合規性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-532">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="cc8dc-533">如需有關如何執行備份後指令碼的詳細資訊，請參閱 [NetBackup 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-533">For more information about how to run a post-backup script, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="cc8dc-534">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="cc8dc-534">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="cc8dc-536">需求</span><span class="sxs-lookup"><span data-stu-id="cc8dc-536">Requirements</span></span>

-   <span data-ttu-id="cc8dc-537">執行指令碼的伺服器必須能夠存取 Azure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-537">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="cc8dc-538">使用者帳戶必須擁有必要的權限。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-538">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="cc8dc-539">必須設定但不要啟用與 StorSimple 磁碟區相關聯的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-539">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="cc8dc-540">您需要 StorSimple 資源名稱、註冊金鑰、裝置名稱和備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-540">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="cc8dc-541">若要啟動或刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="cc8dc-541">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="cc8dc-542">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-542">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="cc8dc-543">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="cc8dc-544">在 Azure 傳統入口網站中，[取得 StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key) 服務的資源名稱和註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-544">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="cc8dc-545">在執行指令碼的伺服器上，以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-545">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="cc8dc-546">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-546">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="cc8dc-547">請記下備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-547">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="cc8dc-548">在記事本中，使用下列程式碼來建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-548">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="cc8dc-549">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="cc8dc-549">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="cc8dc-550">將 PowerShell 指令碼儲存在您儲存 Azure 發佈設定的相同位置。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-550">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="cc8dc-551">例如，儲存為 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="cc8dc-552">將指令碼新增至 NetBackup 中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-552">Add the script to your backup job in NetBackup.</span></span> <span data-ttu-id="cc8dc-553">若要這麼做，請編輯 NetBackup 作業選項的前處理和後處理命令。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-553">To do this, edit your NetBackup job options' pre-processing and post-processing commands.</span></span>

> [!NOTE]
> <span data-ttu-id="cc8dc-554">我們建議您在每日備份作業結束時執行 StorSimple 雲端快照集集備份原則，做為後處理指令碼。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="cc8dc-555">如需有關如何備份和還原備份應用程式環境以符合 RPO 和 RTO 的詳細資訊，請洽詢您的備份架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-555">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="cc8dc-556">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="cc8dc-556">StorSimple as a restore source</span></span>

<span data-ttu-id="cc8dc-557">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-557">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="cc8dc-558">還原已分層儲存到雲端的資料時，會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-558">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="cc8dc-559">如果是本機資料，則會以裝置的本機磁碟速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-559">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="cc8dc-560">如需有關如何執行還原的詳細資訊，請參閱 [NetBackup 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-560">For information about how to perform a restore, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span> <span data-ttu-id="cc8dc-561">我們建議您遵守 NetBackup 還原的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-561">We recommend that you conform to NetBackup restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="cc8dc-562">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="cc8dc-562">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="cc8dc-563">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="cc8dc-564">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-564">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="cc8dc-565">下表列出常見的災害復原案例。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-565">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="cc8dc-566">案例</span><span class="sxs-lookup"><span data-stu-id="cc8dc-566">Scenario</span></span> | <span data-ttu-id="cc8dc-567">影響</span><span class="sxs-lookup"><span data-stu-id="cc8dc-567">Impact</span></span> | <span data-ttu-id="cc8dc-568">如何復原</span><span class="sxs-lookup"><span data-stu-id="cc8dc-568">How to recover</span></span> | <span data-ttu-id="cc8dc-569">注意事項</span><span class="sxs-lookup"><span data-stu-id="cc8dc-569">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="cc8dc-570">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="cc8dc-570">StorSimple device failure</span></span> | <span data-ttu-id="cc8dc-571">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="cc8dc-572">更換故障的裝置，並執行 [StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-572">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="cc8dc-573">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-573">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="cc8dc-574">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-574">All operations are at cloud speeds.</span></span> <span data-ttu-id="cc8dc-575">索引和目錄重新掃描程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層，而這可能會非常耗時。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-575">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="cc8dc-576">NetBackup 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="cc8dc-576">NetBackup server failure</span></span> | <span data-ttu-id="cc8dc-577">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-577">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="cc8dc-578">重建備份伺服器，並執行資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-578">Rebuild the backup server and perform database restore.</span></span> | <span data-ttu-id="cc8dc-579">您必須在災害復原站台重建或還原 NetBackup 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-579">You must rebuild or restore the NetBackup server at the disaster recovery site.</span></span> <span data-ttu-id="cc8dc-580">將資料庫還原到最新的點。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-580">Restore the database to the most recent point.</span></span> <span data-ttu-id="cc8dc-581">如果還原的 NetBackup 資料庫沒有與您最新的備份作業同步，就必須編製索引及編製目錄。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-581">If the restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="cc8dc-582">重新掃描索引和目錄的程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-582">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="cc8dc-583">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-583">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="cc8dc-584">站台故障造成備份伺服器和 StorSimple 都遺失</span><span class="sxs-lookup"><span data-stu-id="cc8dc-584">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="cc8dc-585">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-585">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="cc8dc-586">先還原 StorSimple，然後再還原 NetBackup。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-586">Restore StorSimple first, and then restore NetBackup.</span></span> | <span data-ttu-id="cc8dc-587">先還原 StorSimple，然後再還原 NetBackup。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-587">Restore StorSimple first, and then restore NetBackup.</span></span> <span data-ttu-id="cc8dc-588">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-588">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="cc8dc-589">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-589">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="cc8dc-590">參考</span><span class="sxs-lookup"><span data-stu-id="cc8dc-590">References</span></span>

<span data-ttu-id="cc8dc-591">本文中參考下列文件︰</span><span class="sxs-lookup"><span data-stu-id="cc8dc-591">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="cc8dc-592">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="cc8dc-592">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="cc8dc-593">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-593">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="cc8dc-594">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="cc8dc-594">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="cc8dc-595">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="cc8dc-595">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="cc8dc-596">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc8dc-596">Next steps</span></span>

- <span data-ttu-id="cc8dc-597">深入了解如何[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-597">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="cc8dc-598">深入了解如何執行[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="cc8dc-598">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
