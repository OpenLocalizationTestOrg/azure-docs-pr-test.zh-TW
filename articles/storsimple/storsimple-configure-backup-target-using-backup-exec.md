---
title: "StorSimple 8000 系列做為 Backup Exec 的備份目標 | Microsoft Docs"
description: "描述搭配 Veritas Backup Exec 的 StorSimple 備份目標組態。"
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
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 80e29aa9c63d98a32f1bb92750ebd904c918cc92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a><span data-ttu-id="5568e-103">使用 StorSimple 做為 Backup Exec 的備份目標</span><span class="sxs-lookup"><span data-stu-id="5568e-103">StorSimple as a backup target with Backup Exec</span></span>

## <a name="overview"></a><span data-ttu-id="5568e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5568e-104">Overview</span></span>

<span data-ttu-id="5568e-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="5568e-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="5568e-106">StorSimple 使用 Azure 儲存體帳戶做為內部部署解決方案的擴充功能，跨內部部署儲存體和雲端儲存體自動將資料分層，解決資料暴增的複雜性問題。</span><span class="sxs-lookup"><span data-stu-id="5568e-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="5568e-107">在本文中，我們會討論 StorSimple 與 Veritas Backup Exec 的整合，以及整合這兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="5568e-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span></span> <span data-ttu-id="5568e-108">我們也會建議如何設定 Backup Exec 來與 StorSimple 進行最佳的整合。</span><span class="sxs-lookup"><span data-stu-id="5568e-108">We also make recommendations on how to set up Backup Exec to best integrate with StorSimple.</span></span> <span data-ttu-id="5568e-109">我們遵循 Veritas 的最佳作法，並聽從備份架構設計人員和管理員關於如何設定 Backup Exec 以符合個人備份需求和服務等級協定 (SLA) 的意見。</span><span class="sxs-lookup"><span data-stu-id="5568e-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Backup Exec to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="5568e-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="5568e-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="5568e-111">我們假設基本元件和基礎結構都已正常運作，並準備好支援我們所描述的概念。</span><span class="sxs-lookup"><span data-stu-id="5568e-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="5568e-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="5568e-112">Who should read this?</span></span>

<span data-ttu-id="5568e-113">本文中的資訊最適合於了解儲存體、Windows Server 2012 R2、乙太網路、雲端服務和 Backup Exec 等知識的備份管理員、儲存體管理員及儲存體架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="5568e-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="5568e-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="5568e-114">Supported versions</span></span>

-   [<span data-ttu-id="5568e-115">備份 Exec 16 及更新版本</span><span class="sxs-lookup"><span data-stu-id="5568e-115">Backup Exec 16 and later versions</span></span>](http://backupexec.com/compatibility)
-   [<span data-ttu-id="5568e-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="5568e-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="5568e-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="5568e-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="5568e-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="5568e-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="5568e-119">為備份應用程式提供標準的本機儲存體，以做為快速備份目的地，而不需要做任何變更。</span><span class="sxs-lookup"><span data-stu-id="5568e-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="5568e-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="5568e-121">其雲端分層可與 Azure 雲端儲存體帳戶緊密整合，以使用經濟實惠的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="5568e-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="5568e-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="5568e-123">Key concepts</span></span>

<span data-ttu-id="5568e-124">如同任何儲存體解決方案，仔細評估解決方案的儲存體效能、SLA、變更速率及容量成長需求是成功與否的關鍵。</span><span class="sxs-lookup"><span data-stu-id="5568e-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="5568e-125">主要概念是藉由引進雲端層，對雲端的存取時間和輸送量就能對 StorSimple 執行其工作的能力扮演重要角色。</span><span class="sxs-lookup"><span data-stu-id="5568e-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="5568e-126">StorSimple 的設計目的是針對運作定義完善的使用中資料集 (熱資料) 的應用程式提供儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="5568e-127">在此模型中，使用中的資料集儲存在本機層，其餘非使用中/冷/封存的資料集則分層儲存到雲端。</span><span class="sxs-lookup"><span data-stu-id="5568e-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="5568e-128">下圖說明這個模型。</span><span class="sxs-lookup"><span data-stu-id="5568e-128">This model is represented in the following figure.</span></span> <span data-ttu-id="5568e-129">幾乎是平坦的綠線表示儲存在 StorSimple 裝置本機層的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="5568e-130">紅線則表示儲存在 StorSimple 解決方案所有各層的資料總量。</span><span class="sxs-lookup"><span data-stu-id="5568e-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="5568e-131">平坦綠線與呈指數形的紅色曲線之間的空間代表儲存在雲端的資料總量。</span><span class="sxs-lookup"><span data-stu-id="5568e-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="5568e-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="5568e-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span></span>

<span data-ttu-id="5568e-133">記住此架構，您會發現 StorSimple 非常適合做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="5568e-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="5568e-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="5568e-135">從本機使用中的資料集執行最頻繁的還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="5568e-136">對於異地災害復原和較少進行還原的舊資料使用雲端。</span><span class="sxs-lookup"><span data-stu-id="5568e-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="5568e-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="5568e-137">StorSimple benefits</span></span>

<span data-ttu-id="5568e-138">StorSimple 提供的內部部署解決方案，可以不間斷存取內部部署和雲端儲存體，與 Microsoft Azure 緊密整合。</span><span class="sxs-lookup"><span data-stu-id="5568e-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="5568e-139">StorSimple 在具有固態裝置 (SSD) 和序列連接 SCSI (SAS) 儲存體的內部部署裝置與 Azure 儲存體之間使用自動分層。</span><span class="sxs-lookup"><span data-stu-id="5568e-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="5568e-140">自動分層將經常存取的資料保存在本機的 SSD 和 SAS 層。</span><span class="sxs-lookup"><span data-stu-id="5568e-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="5568e-141">而將不常存取的資料移到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="5568e-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="5568e-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="5568e-143">獨家的重複資料刪除和壓縮演算法，使用雲端以達到前所未有的重複資料刪除層級</span><span class="sxs-lookup"><span data-stu-id="5568e-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="5568e-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="5568e-144">High availability</span></span>
-   <span data-ttu-id="5568e-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="5568e-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="5568e-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="5568e-146">Azure integration</span></span>
-   <span data-ttu-id="5568e-147">雲端中的資料會進行加密</span><span class="sxs-lookup"><span data-stu-id="5568e-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="5568e-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="5568e-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="5568e-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="5568e-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="5568e-150">StorSimple 會進行所有的壓縮及重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="5568e-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="5568e-151">它會在雲端、應用程式及檔案系統之間順暢地傳送和擷取資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="5568e-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="5568e-153">此外，您可以檢閱 [StorSimple 8000 系列技術規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5568e-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="5568e-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="5568e-155">Architecture overview</span></span>

<span data-ttu-id="5568e-156">下表顯示裝置機型與架構的初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="5568e-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="5568e-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="5568e-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="5568e-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="5568e-158">Storage capacity</span></span>       | <span data-ttu-id="5568e-159">8100</span><span class="sxs-lookup"><span data-stu-id="5568e-159">8100</span></span>          | <span data-ttu-id="5568e-160">8600</span><span class="sxs-lookup"><span data-stu-id="5568e-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="5568e-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="5568e-161">Local storage capacity</span></span> | <span data-ttu-id="5568e-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5568e-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="5568e-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5568e-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="5568e-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="5568e-164">Cloud storage capacity</span></span> | <span data-ttu-id="5568e-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5568e-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="5568e-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5568e-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="5568e-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="5568e-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="5568e-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="5568e-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="5568e-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="5568e-169">Backup scenario</span></span>  | <span data-ttu-id="5568e-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="5568e-170">Local storage capacity</span></span>  | <span data-ttu-id="5568e-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="5568e-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="5568e-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="5568e-172">Primary backup</span></span>  | <span data-ttu-id="5568e-173">最近的備份會儲存在本機儲存體供快速復原，以符合復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="5568e-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="5568e-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="5568e-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="5568e-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="5568e-175">Secondary backup</span></span> | <span data-ttu-id="5568e-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="5568e-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="5568e-177">N/A</span><span class="sxs-lookup"><span data-stu-id="5568e-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5568e-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="5568e-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="5568e-179">在此案例中，備份應用程式會使用 StorSimple 磁碟區，做為備份的唯一儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5568e-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="5568e-180">下圖說明解決方案架構，其中所有備份都使用 StorSimple 分層磁碟區進行備份和還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="5568e-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="5568e-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="5568e-183">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="5568e-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="5568e-184">備份伺服器將資料寫入 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="5568e-185">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="5568e-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="5568e-186">快照集指令碼可觸發 StorSimple 雲端快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="5568e-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="5568e-187">備份伺服器會根據保留原則刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-187">The backup server deletes expired backups based on a retention policy.</span></span>


### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="5568e-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="5568e-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="5568e-189">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="5568e-190">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="5568e-191">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="5568e-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5568e-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="5568e-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="5568e-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="5568e-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="5568e-194">下圖說明初始備份和還原以高效能磁碟區做為目標的架構。</span><span class="sxs-lookup"><span data-stu-id="5568e-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="5568e-195">這些備份會依照設定好的排程複製並封存至 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="5568e-196">請務必調整您的高效能磁碟區大小，使其能夠處理保留原則、容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="5568e-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="5568e-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="5568e-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="5568e-199">備份伺服器連絡目標備份代理程式，然後備份代理程式將資料傳輸到備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="5568e-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="5568e-200">備份伺服器將資料寫入高效能儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="5568e-201">備份伺服器更新類別目錄資料庫，然後完成備份作業。</span><span class="sxs-lookup"><span data-stu-id="5568e-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="5568e-202">備份伺服器會根據保留原則將備份複製到 StorSimple。</span><span class="sxs-lookup"><span data-stu-id="5568e-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="5568e-203">快照集指令碼可觸發 StorSimple 雲端快照集管理員 (啟動或刪除)。</span><span class="sxs-lookup"><span data-stu-id="5568e-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="5568e-204">備份伺服器會根據保留原則刪除過期的備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="5568e-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="5568e-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="5568e-206">備份伺服器開始從儲存機制還原適當的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="5568e-207">備份代理程式接收來自備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="5568e-208">備份伺服器完成還原作業。</span><span class="sxs-lookup"><span data-stu-id="5568e-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="5568e-209">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="5568e-209">Deploy the solution</span></span>

<span data-ttu-id="5568e-210">部署解決方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="5568e-210">Deploying the solution requires three steps:</span></span>
1. <span data-ttu-id="5568e-211">準備網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5568e-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="5568e-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="5568e-213">部署 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="5568e-213">Deploy Backup Exec.</span></span>

<span data-ttu-id="5568e-214">下列各節會詳細討論每個步驟。</span><span class="sxs-lookup"><span data-stu-id="5568e-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="5568e-215">設定網路</span><span class="sxs-lookup"><span data-stu-id="5568e-215">Set up the network</span></span>

<span data-ttu-id="5568e-216">因為 StorSimple 是與 Azure 雲端整合的解決方案，所以需要作用中並正常運作的 Azure 雲端連線。</span><span class="sxs-lookup"><span data-stu-id="5568e-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="5568e-217">此連線供雲端快照集、管理、中繼資料傳輸等操作使用，以及將較舊、較少存取的資料分層儲存到 Azure 雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="5568e-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="5568e-218">為了能以最佳方式執行解決方案，我們建議您遵循下列網路最佳作法︰</span><span class="sxs-lookup"><span data-stu-id="5568e-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="5568e-219">將 StorSimple 分層連接至 Azure 的連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="5568e-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="5568e-220">若要達到此目的，將必要的服務品質 (QoS) 層級套用至您的基礎結構參數，以符合您的 RPO 和復原時間目標 (RTO) SLA。</span><span class="sxs-lookup"><span data-stu-id="5568e-220">To achieve this, apply the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="5568e-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="5568e-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="5568e-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5568e-222">Deploy StorSimple</span></span>

<span data-ttu-id="5568e-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-backup-exec"></a><span data-ttu-id="5568e-224">部署 Backup Exec</span><span class="sxs-lookup"><span data-stu-id="5568e-224">Deploy Backup Exec</span></span>

<span data-ttu-id="5568e-225">如需 Backup Exec 安裝最佳作法，請參閱 [Backup Exec 安裝的最佳作法](https://www.veritas.com/support/en_US/article.000068207)。</span><span class="sxs-lookup"><span data-stu-id="5568e-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="5568e-226">設定解決方案</span><span class="sxs-lookup"><span data-stu-id="5568e-226">Set up the solution</span></span>

<span data-ttu-id="5568e-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="5568e-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="5568e-228">下列範例和建議說明最基本也最重要的實作。</span><span class="sxs-lookup"><span data-stu-id="5568e-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="5568e-229">此實作可能無法直接套用到您特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="5568e-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="5568e-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5568e-230">Set up StorSimple</span></span>

| <span data-ttu-id="5568e-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="5568e-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="5568e-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="5568e-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="5568e-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="5568e-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="5568e-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="5568e-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="5568e-235">開啟備份目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-235">Turn on the backup target.</span></span> | <span data-ttu-id="5568e-236">使用下列命令來開啟或關閉備份目標模式，以及取得狀態。</span><span class="sxs-lookup"><span data-stu-id="5568e-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="5568e-237">如需詳細資訊，請參閱[從遠端連接至 StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="5568e-238">若要開啟備份模式︰`Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="5568e-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="5568e-239">若要關閉備份模式︰`Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="5568e-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="5568e-240">若要取得備份模式設定的目前狀態：`Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="5568e-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="5568e-241">為儲存備份資料的磁碟區建立一般的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5568e-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="5568e-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="5568e-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="5568e-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="5568e-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="5568e-245">建立大小盡可能接近預期使用量的磁碟區，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="5568e-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="5568e-246">如需有關如何調整磁碟區大小的資訊，請參閱[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="5568e-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="5568e-247">使用 StorSimple 分層磁碟區，並選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5568e-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="5568e-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="5568e-249">為所有備份目標磁碟區建立唯一的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="5568e-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="5568e-250">StorSimple 備份原則定義磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="5568e-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="5568e-251">在快照集到期時停用排程。</span><span class="sxs-lookup"><span data-stu-id="5568e-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="5568e-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="5568e-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="5568e-253">設定主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="5568e-253">Set up the host backup server storage</span></span>

<span data-ttu-id="5568e-254">根據下列指導方針，設定主機備份伺服器儲存體︰</span><span class="sxs-lookup"><span data-stu-id="5568e-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="5568e-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)。</span><span class="sxs-lookup"><span data-stu-id="5568e-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="5568e-256">不支援合併磁碟。</span><span class="sxs-lookup"><span data-stu-id="5568e-256">Spanned disks are not supported.</span></span>
- <span data-ttu-id="5568e-257">使用 64 KB 配置大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-257">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="5568e-258">將 StorSimple 磁碟區直接對應到 Backup Exec 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5568e-258">Map the StorSimple volumes directly to the Backup Exec server.</span></span>
    - <span data-ttu-id="5568e-259">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="5568e-259">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="5568e-260">虛擬伺服器請使用傳遞磁碟。</span><span class="sxs-lookup"><span data-stu-id="5568e-260">Use pass-through disks for virtual servers.</span></span>

## <a name="best-practices-for-storsimple-and-backup-exec"></a><span data-ttu-id="5568e-261">StorSimple 和 Backup Exec 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5568e-261">Best practices for StorSimple and Backup Exec</span></span>

<span data-ttu-id="5568e-262">根據下列各節中的指導方針來設定您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5568e-262">Set up your solution according to the guidelines in the following sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="5568e-263">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="5568e-263">Operating system best practices</span></span>

-   <span data-ttu-id="5568e-264">停用 NTFS 檔案系統的 Windows Server 加密和重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="5568e-264">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="5568e-265">停用 StorSimple 磁碟區的 Windows Server 磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="5568e-265">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="5568e-266">停用 StorSimple 磁碟區的 Windows Server 索引。</span><span class="sxs-lookup"><span data-stu-id="5568e-266">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="5568e-267">在來源主機 (不是針對 StorSimple 磁碟區) 執行防毒軟體掃描。</span><span class="sxs-lookup"><span data-stu-id="5568e-267">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="5568e-268">在工作管理員中關閉預設 [Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5568e-268">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="5568e-269">利用下列其中一種方式來執行此作業：</span><span class="sxs-lookup"><span data-stu-id="5568e-269">Do this in one of the following ways:</span></span>
   - <span data-ttu-id="5568e-270">在 Windows 工作排程器中關閉維護設定程式。</span><span class="sxs-lookup"><span data-stu-id="5568e-270">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
   - <span data-ttu-id="5568e-271">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5568e-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="5568e-272">下載 PsExec 之後，請以系統管理員身分執行 Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="5568e-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="5568e-273">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="5568e-273">StorSimple best practices</span></span>

  -   <span data-ttu-id="5568e-274">確定 StorSimple 裝置已更新為 [Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-274">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
  -   <span data-ttu-id="5568e-275">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="5568e-275">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="5568e-276">針對 StorSimple 和備份伺服器之間的流量使用專用的 iSCSI 連線。</span><span class="sxs-lookup"><span data-stu-id="5568e-276">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
  -   <span data-ttu-id="5568e-277">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-277">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="5568e-278">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="5568e-278">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="backup-exec-best-practices"></a><span data-ttu-id="5568e-279">Backup Exec 最佳作法</span><span class="sxs-lookup"><span data-stu-id="5568e-279">Backup Exec best practices</span></span>

-   <span data-ttu-id="5568e-280">Backup Exec 必須安裝在伺服器的本機磁碟機，而不是在 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-280">Backup Exec must be installed on a local drive of the server, and not on a StorSimple volume.</span></span>
-   <span data-ttu-id="5568e-281">將 Backup Exec 儲存體的**並行寫入作業**設定為允許的最大值。</span><span class="sxs-lookup"><span data-stu-id="5568e-281">Set the Backup Exec storage **concurrent write operations** to the maximum allowed.</span></span>
    -   <span data-ttu-id="5568e-282">將 Backup Exec 儲存體的**區塊和緩衝區大小**設定為 512 KB。</span><span class="sxs-lookup"><span data-stu-id="5568e-282">Set the Backup Exec storage **block and buffer size** to 512 KB.</span></span>
    -   <span data-ttu-id="5568e-283">開啟 Backup Exec 儲存體的**緩衝讀取和寫入**。</span><span class="sxs-lookup"><span data-stu-id="5568e-283">Turn on Backup Exec storage **buffered read and write**.</span></span>
-   <span data-ttu-id="5568e-284">StorSimple 支援 Backup Exec 完整和增量備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-284">StorSimple supports Backup Exec full and incremental backups.</span></span> <span data-ttu-id="5568e-285">建議您不要使用綜合和差異備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-285">We recommend that you not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="5568e-286">備份資料檔案最好只包含特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-286">Backup data files should contain data only for a specific job.</span></span> <span data-ttu-id="5568e-287">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="5568e-287">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="5568e-288">停用作業驗證。</span><span class="sxs-lookup"><span data-stu-id="5568e-288">Disable job verification.</span></span> <span data-ttu-id="5568e-289">如有必要，應該將驗證安排在最新的備份作業之後進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-289">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="5568e-290">請務必了解這項作業會影響您的備份時間範圍。</span><span class="sxs-lookup"><span data-stu-id="5568e-290">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="5568e-291">選取 [儲存體] > 您的磁碟 > [詳細資料] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="5568e-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span></span> <span data-ttu-id="5568e-292">關閉 [預先配置磁碟空間]。</span><span class="sxs-lookup"><span data-stu-id="5568e-292">Turn off **Pre-allocate disk space**.</span></span>

<span data-ttu-id="5568e-293">如需實作這些需求的最新 Backup Exec 設定和最佳作法，請參閱 [Veritas 網站](https://www.veritas.com)。</span><span class="sxs-lookup"><span data-stu-id="5568e-293">For the latest Backup Exec settings and best practices for implementing these requirements, see [the Veritas website](https://www.veritas.com).</span></span>

## <a name="retention-policies"></a><span data-ttu-id="5568e-294">保留原則</span><span class="sxs-lookup"><span data-stu-id="5568e-294">Retention policies</span></span>

<span data-ttu-id="5568e-295">其中一種最常用的備份保留原則類型是三代循環 (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="5568e-295">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="5568e-296">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="5568e-297">此原則會產生六個 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-297">This policy results in six StorSimple tiered volumes.</span></span> <span data-ttu-id="5568e-298">一個磁碟區包含每週、每個月和每年的完整備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-298">One volume contains the weekly, monthly, and yearly full backups.</span></span> <span data-ttu-id="5568e-299">其他五個磁碟區則儲存每日的增量備份。</span><span class="sxs-lookup"><span data-stu-id="5568e-299">The other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="5568e-300">在下列範例中，我們使用 GFS 循環。</span><span class="sxs-lookup"><span data-stu-id="5568e-300">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="5568e-301">範例的假設如下：</span><span class="sxs-lookup"><span data-stu-id="5568e-301">The example assumes the following:</span></span>

-   <span data-ttu-id="5568e-302">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-302">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="5568e-303">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="5568e-303">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="5568e-304">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="5568e-304">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="5568e-305">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="5568e-305">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="5568e-306">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="5568e-306">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="5568e-307">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="5568e-307">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="5568e-308">根據先前的假設，為每個月和每年的完整備份建立 26 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-308">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="5568e-309">為每個每日增量備份建立 5 TiB 的 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-309">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="5568e-310">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="5568e-310">Backup type retention</span></span> | <span data-ttu-id="5568e-311">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="5568e-311">Size (TiB)</span></span> | <span data-ttu-id="5568e-312">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="5568e-312">GFS multiplier\*</span></span> | <span data-ttu-id="5568e-313">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="5568e-313">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="5568e-314">每週完整</span><span class="sxs-lookup"><span data-stu-id="5568e-314">Weekly full</span></span> | <span data-ttu-id="5568e-315">1</span><span class="sxs-lookup"><span data-stu-id="5568e-315">1</span></span> | <span data-ttu-id="5568e-316">4</span><span class="sxs-lookup"><span data-stu-id="5568e-316">4</span></span>  | <span data-ttu-id="5568e-317">4</span><span class="sxs-lookup"><span data-stu-id="5568e-317">4</span></span> |
| <span data-ttu-id="5568e-318">每日增量</span><span class="sxs-lookup"><span data-stu-id="5568e-318">Daily incremental</span></span> | <span data-ttu-id="5568e-319">0.5</span><span class="sxs-lookup"><span data-stu-id="5568e-319">0.5</span></span> | <span data-ttu-id="5568e-320">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="5568e-320">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="5568e-321">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="5568e-321">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="5568e-322">每月完整</span><span class="sxs-lookup"><span data-stu-id="5568e-322">Monthly full</span></span> | <span data-ttu-id="5568e-323">1</span><span class="sxs-lookup"><span data-stu-id="5568e-323">1</span></span> | <span data-ttu-id="5568e-324">12</span><span class="sxs-lookup"><span data-stu-id="5568e-324">12</span></span> | <span data-ttu-id="5568e-325">12</span><span class="sxs-lookup"><span data-stu-id="5568e-325">12</span></span> |
| <span data-ttu-id="5568e-326">每年完整</span><span class="sxs-lookup"><span data-stu-id="5568e-326">Yearly full</span></span> | <span data-ttu-id="5568e-327">1</span><span class="sxs-lookup"><span data-stu-id="5568e-327">1</span></span>  | <span data-ttu-id="5568e-328">10</span><span class="sxs-lookup"><span data-stu-id="5568e-328">10</span></span> | <span data-ttu-id="5568e-329">10</span><span class="sxs-lookup"><span data-stu-id="5568e-329">10</span></span> |
| <span data-ttu-id="5568e-330">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="5568e-330">GFS requirement</span></span> |   | <span data-ttu-id="5568e-331">38</span><span class="sxs-lookup"><span data-stu-id="5568e-331">38</span></span> |   |
| <span data-ttu-id="5568e-332">其他配額</span><span class="sxs-lookup"><span data-stu-id="5568e-332">Additional quota</span></span>  | <span data-ttu-id="5568e-333">4</span><span class="sxs-lookup"><span data-stu-id="5568e-333">4</span></span>  |   | <span data-ttu-id="5568e-334">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="5568e-334">42 total GFS requirement</span></span>  |
<span data-ttu-id="5568e-335">\*GFS 乘數是您為了符合備份原則需求所需保護和保留的複本數目。</span><span class="sxs-lookup"><span data-stu-id="5568e-335">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-backup-exec-storage"></a><span data-ttu-id="5568e-336">設定 Backup Exec 儲存體</span><span class="sxs-lookup"><span data-stu-id="5568e-336">Set up Backup Exec storage</span></span>

### <a name="to-set-up-backup-exec-storage"></a><span data-ttu-id="5568e-337">若要設定 Backup Exec 儲存體</span><span class="sxs-lookup"><span data-stu-id="5568e-337">To set up Backup Exec storage</span></span>

1.  <span data-ttu-id="5568e-338">在 Backup Exec 管理主控台中，選取 [儲存體] > [設定儲存體] > [磁碟型儲存體] > [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5568e-338">In the Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span></span>

    ![Backup Exec 管理主控台，設定儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  <span data-ttu-id="5568e-340">選取 [磁碟儲存體]，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5568e-340">Select **Disk Storage**, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，選取儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  <span data-ttu-id="5568e-342">輸入一個代表性名稱，例如，「星期六完整」和描述。</span><span class="sxs-lookup"><span data-stu-id="5568e-342">Enter a representative name, for example, **Saturday Full**, and a description.</span></span> <span data-ttu-id="5568e-343">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5568e-343">Select **Next**.</span></span>

    ![Backup Exec 管理主控台，名稱和描述頁面](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  <span data-ttu-id="5568e-345">選取您要建立磁碟存放裝置的磁碟，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5568e-345">Select the disk where you want to create the disk storage device, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，儲存體磁碟選取頁面](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  <span data-ttu-id="5568e-347">將寫入作業數目增加為 **16**，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5568e-347">Increment the number of write operations to **16**, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，並行寫入作業設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  <span data-ttu-id="5568e-349">檢閱設定，然後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5568e-349">Review the settings, and then select **Finish**.</span></span>

    ![Backup Exec 管理主控台，儲存體組態摘要頁面](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  <span data-ttu-id="5568e-351">在每項磁碟區指派作業結束時，變更存放裝置設定，以符合 [StorSimple 和 Backup Exec 的最佳作法](#best-practices-for-storsimple-and-backup-exec)所建議的設定。</span><span class="sxs-lookup"><span data-stu-id="5568e-351">At the end of each volume assignment, change the storage device settings to match those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span></span>

    ![Backup Exec 管理主控台，存放裝置設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  <span data-ttu-id="5568e-353">重複步驟 1-7，直到完成將 StorSimple 磁碟區指派給 Backup Exec 為止。</span><span class="sxs-lookup"><span data-stu-id="5568e-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes to Backup Exec.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5568e-354">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="5568e-354">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="5568e-355">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-355">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="5568e-356">下圖說明如何將典型的磁碟區對應到備份作業。</span><span class="sxs-lookup"><span data-stu-id="5568e-356">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="5568e-357">在此情況下，所有的每週備份會對應到星期六完整的磁碟，增量備份則會對應到星期一至星期五的增量磁碟。</span><span class="sxs-lookup"><span data-stu-id="5568e-357">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="5568e-358">所有備份和還原都是從 StorSimple 分層磁碟區進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-358">All the backups and restores are from a StorSimple tiered volume.</span></span>

![主要備份目標組態的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="5568e-360">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="5568e-360">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="5568e-361">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="5568e-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="5568e-362">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="5568e-362">Frequency/backup type</span></span> | <span data-ttu-id="5568e-363">完整</span><span class="sxs-lookup"><span data-stu-id="5568e-363">Full</span></span> | <span data-ttu-id="5568e-364">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-364">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="5568e-365">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="5568e-365">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="5568e-366">星期六</span><span class="sxs-lookup"><span data-stu-id="5568e-366">Saturday</span></span> | <span data-ttu-id="5568e-367">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="5568e-367">Monday-Friday</span></span> |
| <span data-ttu-id="5568e-368">每月</span><span class="sxs-lookup"><span data-stu-id="5568e-368">Monthly</span></span>  | <span data-ttu-id="5568e-369">星期六</span><span class="sxs-lookup"><span data-stu-id="5568e-369">Saturday</span></span>  |   |
| <span data-ttu-id="5568e-370">每年</span><span class="sxs-lookup"><span data-stu-id="5568e-370">Yearly</span></span> | <span data-ttu-id="5568e-371">星期六</span><span class="sxs-lookup"><span data-stu-id="5568e-371">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="5568e-372">將 StorSimple 磁碟區指派給 Backup Exec 備份作業</span><span class="sxs-lookup"><span data-stu-id="5568e-372">Assign StorSimple volumes to a Backup Exec backup job</span></span>

<span data-ttu-id="5568e-373">下列程序假設 Backup Exec 和目標主機已依據 Backup Exec 代理程式指導方針進行設定。</span><span class="sxs-lookup"><span data-stu-id="5568e-373">The following sequence assumes that Backup Exec and the target host are configured in accordance with the Backup Exec agent guidelines.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="5568e-374">若要將 StorSimple 磁碟區指派給 Backup Exec 備份作業</span><span class="sxs-lookup"><span data-stu-id="5568e-374">To assign StorSimple volumes to a Backup Exec backup job</span></span>

1.  <span data-ttu-id="5568e-375">在 Backup Exec 管理主控台中，選取 [主機] > [備份] > [備份到磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5568e-375">In the Backup Exec management console, select **Host** > **Backup** > **Backup to Disk**.</span></span>

    ![Backup Exec 管理主控台，選取主機、備份及備份到磁碟](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  <span data-ttu-id="5568e-377">在 [備份定義屬性] 對話方塊的 [備份] 之下，選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="5568e-377">In the **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  <span data-ttu-id="5568e-379">設定您的完整和增量備份，讓這些備份符合 RPO 和 RTO 需求並遵循 Veritas 的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="5568e-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform to Veritas best practices.</span></span>

4.  <span data-ttu-id="5568e-380">在 [備份選項] 對話方塊中，選取 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="5568e-380">In the **Backup Options** dialog box, select **Storage**.</span></span>

    ![Backup Exec 管理主控台，備份選項、儲存體對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  <span data-ttu-id="5568e-382">將對應的 StorSimple 磁碟區指派到您的備份排程。</span><span class="sxs-lookup"><span data-stu-id="5568e-382">Assign corresponding StorSimple volumes to your backup schedule.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5568e-383">[Compression (壓縮)] 和 [Encryption type (加密類型)] 設定為 [None (無)]。</span><span class="sxs-lookup"><span data-stu-id="5568e-383">**Compression** and **Encryption type** are set to **None**.</span></span>

6.  <span data-ttu-id="5568e-384">在 [確認] 之下，選取 [不要驗證這個作業的資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5568e-384">Under **Verify**, select the **Do not verify data for this job** check box.</span></span> <span data-ttu-id="5568e-385">使用此選項可能會影響 StorSimple 分層。</span><span class="sxs-lookup"><span data-stu-id="5568e-385">Using this option might affect StorSimple tiering.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5568e-386">磁碟重組、索引和背景驗證會對 StorSimple 分層造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="5568e-386">Defragmentation, indexing, and background verification negatively affect the StorSimple tiering.</span></span>

    ![Backup Exec 管理主控台，備份選項、驗證設定](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  <span data-ttu-id="5568e-388">設定完其餘的備份選項以符合需求之後，選取 [確定] 即可完成。</span><span class="sxs-lookup"><span data-stu-id="5568e-388">When you've set up the rest of your backup options to meet your requirements, select **OK** to finish.</span></span>

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5568e-389">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="5568e-389">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="5568e-390">已分層儲存到雲端的備份資料，會以雲端速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-390">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="5568e-391">在此模型中，您必須擁有儲存媒體 (而非 StorSimple) 做為暫時快取。</span><span class="sxs-lookup"><span data-stu-id="5568e-391">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="5568e-392">例如，您可以使用獨立磁碟容錯陣列 (RAID) 磁碟區來容納空間、輸入/輸出 (I/O) 和頻寬。</span><span class="sxs-lookup"><span data-stu-id="5568e-392">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="5568e-393">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="5568e-393">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="5568e-394">下圖說明一般短期保留的 (相對於伺服器) 本機磁碟區，以及長期保留的封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-394">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="5568e-395">在此案例中，所有備份都會在 (相對於伺服器) 本機的 RAID 磁碟區上執行。</span><span class="sxs-lookup"><span data-stu-id="5568e-395">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="5568e-396">這些備份會定期複製並封存到封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-396">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="5568e-397">請務必設定您 (相對於伺服器) 本機的 RAID 磁碟區，以便處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="5568e-397">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="5568e-398">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="5568e-398">StorSimple as a secondary backup target GFS example</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

<span data-ttu-id="5568e-400">下表顯示如何設定備份以在本機和 StorSimple 磁碟上執行。</span><span class="sxs-lookup"><span data-stu-id="5568e-400">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="5568e-401">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="5568e-401">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="5568e-402">備份設定和容量需求</span><span class="sxs-lookup"><span data-stu-id="5568e-402">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="5568e-403">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="5568e-403">Backup type and retention</span></span> | <span data-ttu-id="5568e-404">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="5568e-404">Configured storage</span></span> | <span data-ttu-id="5568e-405">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="5568e-405">Size (TiB)</span></span> | <span data-ttu-id="5568e-406">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="5568e-406">GFS multiplier</span></span> | <span data-ttu-id="5568e-407">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="5568e-407">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="5568e-408">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="5568e-408">Week 1 (full and incremental)</span></span> |<span data-ttu-id="5568e-409">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="5568e-409">Local disk (short-term)</span></span>| <span data-ttu-id="5568e-410">1</span><span class="sxs-lookup"><span data-stu-id="5568e-410">1</span></span> | <span data-ttu-id="5568e-411">1</span><span class="sxs-lookup"><span data-stu-id="5568e-411">1</span></span> | <span data-ttu-id="5568e-412">1</span><span class="sxs-lookup"><span data-stu-id="5568e-412">1</span></span> |
| <span data-ttu-id="5568e-413">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="5568e-413">StorSimple weeks 2-4</span></span> |<span data-ttu-id="5568e-414">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="5568e-414">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5568e-415">1</span><span class="sxs-lookup"><span data-stu-id="5568e-415">1</span></span> | <span data-ttu-id="5568e-416">4</span><span class="sxs-lookup"><span data-stu-id="5568e-416">4</span></span> | <span data-ttu-id="5568e-417">4</span><span class="sxs-lookup"><span data-stu-id="5568e-417">4</span></span> |
| <span data-ttu-id="5568e-418">每月完整</span><span class="sxs-lookup"><span data-stu-id="5568e-418">Monthly full</span></span> |<span data-ttu-id="5568e-419">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="5568e-419">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5568e-420">1</span><span class="sxs-lookup"><span data-stu-id="5568e-420">1</span></span> | <span data-ttu-id="5568e-421">12</span><span class="sxs-lookup"><span data-stu-id="5568e-421">12</span></span> | <span data-ttu-id="5568e-422">12</span><span class="sxs-lookup"><span data-stu-id="5568e-422">12</span></span> |
| <span data-ttu-id="5568e-423">每年完整</span><span class="sxs-lookup"><span data-stu-id="5568e-423">Yearly full</span></span> |<span data-ttu-id="5568e-424">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="5568e-424">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5568e-425">1</span><span class="sxs-lookup"><span data-stu-id="5568e-425">1</span></span> | <span data-ttu-id="5568e-426">1</span><span class="sxs-lookup"><span data-stu-id="5568e-426">1</span></span> | <span data-ttu-id="5568e-427">1</span><span class="sxs-lookup"><span data-stu-id="5568e-427">1</span></span> |
|<span data-ttu-id="5568e-428">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="5568e-428">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="5568e-429">18*</span><span class="sxs-lookup"><span data-stu-id="5568e-429">18*</span></span>|
<span data-ttu-id="5568e-430">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="5568e-431">GFS 範例排程：每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="5568e-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="5568e-432">週</span><span class="sxs-lookup"><span data-stu-id="5568e-432">Week</span></span> | <span data-ttu-id="5568e-433">完整</span><span class="sxs-lookup"><span data-stu-id="5568e-433">Full</span></span> | <span data-ttu-id="5568e-434">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-434">Incremental day 1</span></span> | <span data-ttu-id="5568e-435">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-435">Incremental day 2</span></span> | <span data-ttu-id="5568e-436">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-436">Incremental day 3</span></span> | <span data-ttu-id="5568e-437">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-437">Incremental day 4</span></span> | <span data-ttu-id="5568e-438">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="5568e-438">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="5568e-439">第 1 週</span><span class="sxs-lookup"><span data-stu-id="5568e-439">Week 1</span></span> | <span data-ttu-id="5568e-440">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-440">Local RAID volume</span></span>  | <span data-ttu-id="5568e-441">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-441">Local RAID volume</span></span> | <span data-ttu-id="5568e-442">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-442">Local RAID volume</span></span> | <span data-ttu-id="5568e-443">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-443">Local RAID volume</span></span> | <span data-ttu-id="5568e-444">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-444">Local RAID volume</span></span> | <span data-ttu-id="5568e-445">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5568e-445">Local RAID volume</span></span> |
| <span data-ttu-id="5568e-446">第 2 週</span><span class="sxs-lookup"><span data-stu-id="5568e-446">Week 2</span></span> | <span data-ttu-id="5568e-447">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="5568e-447">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5568e-448">第 3 週</span><span class="sxs-lookup"><span data-stu-id="5568e-448">Week 3</span></span> | <span data-ttu-id="5568e-449">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="5568e-449">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5568e-450">第 4 週</span><span class="sxs-lookup"><span data-stu-id="5568e-450">Week 4</span></span> | <span data-ttu-id="5568e-451">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="5568e-451">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5568e-452">每月</span><span class="sxs-lookup"><span data-stu-id="5568e-452">Monthly</span></span> | <span data-ttu-id="5568e-453">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="5568e-453">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="5568e-454">每年</span><span class="sxs-lookup"><span data-stu-id="5568e-454">Yearly</span></span> | <span data-ttu-id="5568e-455">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="5568e-455">StorSimple yearly</span></span>  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-archive-and-deduplication-job"></a><span data-ttu-id="5568e-456">將 StorSimple 磁碟區指派給 Backup Exec 封存和/重複資料刪除作業</span><span class="sxs-lookup"><span data-stu-id="5568e-456">Assign StorSimple volumes to a Backup Exec archive and deduplication job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-archive-and-duplication-job"></a><span data-ttu-id="5568e-457">若要將 StorSimple 磁碟區指派給 Backup Exec 封存和重複資料刪除作業</span><span class="sxs-lookup"><span data-stu-id="5568e-457">To assign StorSimple volumes to a Backup Exec archive and duplication job</span></span>

1.  <span data-ttu-id="5568e-458">在 Backup Exec 管理主控台中，以滑鼠右鍵按一下您想要封存至 StorSimple 磁碟區的作業，然後選取 [備份定義屬性] > **編輯**。</span><span class="sxs-lookup"><span data-stu-id="5568e-458">In the Backup Exec management console, right-click the job that you want to archive to a StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  <span data-ttu-id="5568e-460">選取 [新增階段] > [複製到磁碟] > [編輯]。</span><span class="sxs-lookup"><span data-stu-id="5568e-460">Select **Add Stage** > **Duplicate to Disk** > **Edit**.</span></span>

    ![Backup Exec 管理主控台，新增階段](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  <span data-ttu-id="5568e-462">在 [複製選項] 對話方塊中，選取您要用於 [來源] 和 [排程] 的值。</span><span class="sxs-lookup"><span data-stu-id="5568e-462">In the **Duplicate Options** dialog box, select the values that you want to use for **Source** and **Schedule**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  <span data-ttu-id="5568e-464">在 [儲存體] 下拉式清單中，選取您想要封存作業以儲存資料的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-464">In the **Storage** drop-down list, select the StorSimple volume where you want the archive job to store the data.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  <span data-ttu-id="5568e-466">選取 [確認]，然後選取 [不要驗證這個作業的資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5568e-466">Select **Verify**, and then select the **Do not verify data for this job** check box.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  <span data-ttu-id="5568e-468">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5568e-468">Select **OK**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  <span data-ttu-id="5568e-470">在 [Backup (備份)] 欄中，新增新的階段。</span><span class="sxs-lookup"><span data-stu-id="5568e-470">In the **Backup** column, add a new stage.</span></span> <span data-ttu-id="5568e-471">針對來源，使用 [增量]。</span><span class="sxs-lookup"><span data-stu-id="5568e-471">For the source, use **incremental**.</span></span> <span data-ttu-id="5568e-472">針對目標，選擇其中封存增量備份作業的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5568e-472">For the target, choose the StorSimple volume where the incremental backup job is archived.</span></span> <span data-ttu-id="5568e-473">重複步驟 1 至 6。</span><span class="sxs-lookup"><span data-stu-id="5568e-473">Repeat steps 1-6.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="5568e-474">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="5568e-474">StorSimple cloud snapshots</span></span>

<span data-ttu-id="5568e-475">StorSimple 雲端快照集可保護位於 StorSimple 裝置中的資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-475">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="5568e-476">建立雲端快照集相當於將本機備份磁碟送到異地場所。</span><span class="sxs-lookup"><span data-stu-id="5568e-476">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="5568e-477">如果您使用 Azure 異地備援儲存體，建立雲端快照集相當於將備份磁帶送到多個站台。</span><span class="sxs-lookup"><span data-stu-id="5568e-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="5568e-478">如果您需要在災害後還原裝置，可以讓另一個 StorSimple 裝置上線並執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5568e-478">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="5568e-479">容錯移轉之後，您就可以從最新的雲端快照集 (以雲端速度) 存取資料。</span><span class="sxs-lookup"><span data-stu-id="5568e-479">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="5568e-480">下一節說明如何建立簡短指令碼，以在備份後處理期間啟動和刪除 StorSimple 雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="5568e-480">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="5568e-481">以手動方式或以程式設計方式建立的快照集不會遵循 StorSimple 快照集到期原則。</span><span class="sxs-lookup"><span data-stu-id="5568e-481">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="5568e-482">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="5568e-482">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="5568e-483">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="5568e-483">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="5568e-484">在刪除 StorSimple 快照集之前，請先仔細評估合規性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="5568e-484">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="5568e-485">如需有關如何執行備份後指令碼的詳細資訊，請參閱 [Backup Exec 文件](https://www.veritas.com/support/en_US/15047.html)。</span><span class="sxs-lookup"><span data-stu-id="5568e-485">For more information about how to run a post-backup script, see the [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="5568e-486">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="5568e-486">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="5568e-488">需求</span><span class="sxs-lookup"><span data-stu-id="5568e-488">Requirements</span></span>

-   <span data-ttu-id="5568e-489">執行指令碼的伺服器必須能夠存取 Azure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="5568e-489">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="5568e-490">使用者帳戶必須擁有必要的權限。</span><span class="sxs-lookup"><span data-stu-id="5568e-490">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="5568e-491">必須設定但不要啟用與 StorSimple 磁碟區相關聯的 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="5568e-491">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="5568e-492">您需要 StorSimple 資源名稱、註冊金鑰、裝置名稱和備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="5568e-492">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="5568e-493">若要啟動或刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="5568e-493">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="5568e-494">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5568e-494">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="5568e-495">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5568e-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="5568e-496">在 Azure 傳統入口網站中，[取得 StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key) 服務的資源名稱和註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="5568e-496">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="5568e-497">在執行指令碼的伺服器上，以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5568e-497">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="5568e-498">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="5568e-498">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="5568e-499">請記下備份原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="5568e-499">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="5568e-500">在記事本中，使用下列程式碼來建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5568e-500">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="5568e-501">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="5568e-501">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="5568e-502">將 PowerShell 指令碼儲存在您儲存 Azure 發佈設定的相同位置。</span><span class="sxs-lookup"><span data-stu-id="5568e-502">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="5568e-503">例如，儲存為 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1。</span><span class="sxs-lookup"><span data-stu-id="5568e-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="5568e-504">編輯 Backup Exec 作業選項的前處理和後處理命令，以在 Backup Exec 的備份作業中新增指令碼。</span><span class="sxs-lookup"><span data-stu-id="5568e-504">Add the script to your backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span></span>

    ![Backup Exec 主控台，備份選項，前處理和後處理命令索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> <span data-ttu-id="5568e-506">我們建議您在每日備份作業結束時執行 StorSimple 雲端快照集集備份原則，做為後處理指令碼。</span><span class="sxs-lookup"><span data-stu-id="5568e-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="5568e-507">如需有關如何備份和還原備份應用程式環境以符合 RPO 和 RTO 的詳細資訊，請洽詢您的備份架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="5568e-507">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="5568e-508">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="5568e-508">StorSimple as a restore source</span></span>

<span data-ttu-id="5568e-509">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-509">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="5568e-510">還原已分層儲存到雲端的資料時，會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-510">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="5568e-511">如果是本機資料，則會以裝置的本機磁碟速度進行還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-511">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="5568e-512">如需有關如何執行還原的詳細資訊，請參閱 Backup Exec 文件。</span><span class="sxs-lookup"><span data-stu-id="5568e-512">For information about how to perform a restore, see the Backup Exec documentation.</span></span> <span data-ttu-id="5568e-513">我們建議您遵守 Backup Exec 還原的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="5568e-513">We recommend that you conform to Backup Exec restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="5568e-514">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="5568e-514">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="5568e-515">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="5568e-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="5568e-516">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="5568e-516">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="5568e-517">下表列出常見的災害復原案例。</span><span class="sxs-lookup"><span data-stu-id="5568e-517">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="5568e-518">案例</span><span class="sxs-lookup"><span data-stu-id="5568e-518">Scenario</span></span> | <span data-ttu-id="5568e-519">影響</span><span class="sxs-lookup"><span data-stu-id="5568e-519">Impact</span></span> | <span data-ttu-id="5568e-520">如何復原</span><span class="sxs-lookup"><span data-stu-id="5568e-520">How to recover</span></span> | <span data-ttu-id="5568e-521">注意事項</span><span class="sxs-lookup"><span data-stu-id="5568e-521">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="5568e-522">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="5568e-522">StorSimple device failure</span></span> | <span data-ttu-id="5568e-523">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="5568e-523">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5568e-524">更換故障的裝置，並執行 [StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-524">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="5568e-525">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="5568e-525">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="5568e-526">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-526">All operations are at cloud speeds.</span></span> <span data-ttu-id="5568e-527">編製索引及編製目錄的重新掃描程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層，而這可能會非常耗時。</span><span class="sxs-lookup"><span data-stu-id="5568e-527">The indexing and cataloging rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="5568e-528">Backup Exec 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="5568e-528">Backup Exec server failure</span></span> | <span data-ttu-id="5568e-529">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="5568e-529">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5568e-530">重建備份伺服器，並依[如何執行手動備份和還原 Backup Exec (BEDB) 資料庫 (英文)](http://www.veritas.com/docs/000041083) 中所述執行資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="5568e-530">Rebuild the backup server and perform database restore as detailed in [How to do a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span></span> | <span data-ttu-id="5568e-531">您必須在災害復原站台重建或還原 Backup Exec 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5568e-531">You must rebuild or restore the Backup Exec server at the disaster recovery site.</span></span> <span data-ttu-id="5568e-532">將資料庫還原到最新的點。</span><span class="sxs-lookup"><span data-stu-id="5568e-532">Restore the database to the most recent point.</span></span> <span data-ttu-id="5568e-533">如果還原的 Backup Exec 資料庫沒有與您最新的備份作業同步，就必須編製索引及編製目錄。</span><span class="sxs-lookup"><span data-stu-id="5568e-533">If the restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="5568e-534">重新掃描索引和目錄的程序可能會造成所有備份集都要進行掃描並從雲端層提取到本機裝置層。</span><span class="sxs-lookup"><span data-stu-id="5568e-534">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="5568e-535">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="5568e-535">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="5568e-536">站台故障造成備份伺服器和 StorSimple 都遺失</span><span class="sxs-lookup"><span data-stu-id="5568e-536">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="5568e-537">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="5568e-537">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5568e-538">先還原 StorSimple，然後再還原 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="5568e-538">Restore StorSimple first, and then restore Backup Exec.</span></span> | <span data-ttu-id="5568e-539">先還原 StorSimple，然後再還原 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="5568e-539">Restore StorSimple first, and then restore Backup Exec.</span></span> <span data-ttu-id="5568e-540">如果您需要在裝置復原後執行還原，則會從雲端擷取完整的使用中資料集到新裝置。</span><span class="sxs-lookup"><span data-stu-id="5568e-540">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="5568e-541">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="5568e-541">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="5568e-542">參考</span><span class="sxs-lookup"><span data-stu-id="5568e-542">References</span></span>

<span data-ttu-id="5568e-543">本文中參考下列文件︰</span><span class="sxs-lookup"><span data-stu-id="5568e-543">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="5568e-544">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="5568e-544">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="5568e-545">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="5568e-545">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="5568e-546">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="5568e-546">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="5568e-547">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="5568e-547">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="5568e-548">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5568e-548">Next steps</span></span>

- <span data-ttu-id="5568e-549">深入了解如何[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-549">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="5568e-550">深入了解如何執行[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="5568e-550">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
