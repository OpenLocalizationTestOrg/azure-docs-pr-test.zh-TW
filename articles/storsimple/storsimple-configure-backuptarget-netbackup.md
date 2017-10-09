---
title: "做為備份目標與 NetBackup aaaStorSimple 8000 系列 |Microsoft 文件"
description: "描述 Veritas NetBackup hello StorSimple 備份目標組態。"
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
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a><span data-ttu-id="46c60-103">使用 StorSimple 做為 NetBackup 的備份目標</span><span class="sxs-lookup"><span data-stu-id="46c60-103">StorSimple as a backup target with NetBackup</span></span>

## <a name="overview"></a><span data-ttu-id="46c60-104">概觀</span><span class="sxs-lookup"><span data-stu-id="46c60-104">Overview</span></span>

<span data-ttu-id="46c60-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="46c60-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="46c60-106">StorSimple 位址為指數的資料成長的 hello 複雜性為 hello 在內部部署方案，以及自動分層資料的延伸的 Azure 儲存體帳戶使用跨內部部署儲存體和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-106">StorSimple addresses hello complexities of exponential data growth by using an Azure storage account as an extension of hello on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="46c60-107">在本文中，我們會討論 StorSimple 與 Veritas NetBackup 的整合，以及整合這兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="46c60-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span></span> <span data-ttu-id="46c60-108">我們也會進行向上 Veritas NetBackup toobest tooset 如何整合與 StorSimple 的建議。</span><span class="sxs-lookup"><span data-stu-id="46c60-108">We also make recommendations on how tooset up Veritas NetBackup toobest integrate with StorSimple.</span></span> <span data-ttu-id="46c60-109">我們延遲 tooVeritas 最佳作法、 備份架構設計人員和系統管理員的 hello 最佳方式 tooset Veritas NetBackup toomeet 個別的備份需求以及服務等級協定 (Sla)。</span><span class="sxs-lookup"><span data-stu-id="46c60-109">We defer tooVeritas best practices, backup architects, and administrators for hello best way tooset up Veritas NetBackup toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="46c60-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="46c60-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="46c60-111">我們假設 hello 基本元件和基礎結構是在工作順序和準備 toosupport hello 概念，我們將描述。</span><span class="sxs-lookup"><span data-stu-id="46c60-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="46c60-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="46c60-112">Who should read this?</span></span>

<span data-ttu-id="46c60-113">最有幫助 toobackup 系統管理員、 存放裝置系統管理員，以及儲存體架構設計人員了解儲存體、 Windows Server 2012 R2、 乙太網路、 雲端服務和 Veritas NetBackup，就會在本文中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="46c60-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="46c60-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="46c60-114">Supported versions</span></span>

-   <span data-ttu-id="46c60-115">NetBackup 7.7x 及更新版本</span><span class="sxs-lookup"><span data-stu-id="46c60-115">NetBackup 7.7.x and later versions</span></span>
-   [<span data-ttu-id="46c60-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="46c60-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="46c60-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="46c60-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="46c60-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="46c60-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="46c60-119">它提供標準的本機儲存體備份應用程式 toouse 做為快速備份的目的地，不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="46c60-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="46c60-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="46c60-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="46c60-121">其雲端層與 Azure 雲端儲存體帳戶 toouse 順暢地整合符合成本效益的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="46c60-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="46c60-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="46c60-123">Key concepts</span></span>

<span data-ttu-id="46c60-124">如同任何儲存體解決方案，hello 方案的儲存體效能 Sla，仔細評估變更與容量成長需求的速率是重大 toosuccess。</span><span class="sxs-lookup"><span data-stu-id="46c60-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="46c60-125">hello 主要概念是，藉由引進雲端層，您的存取時間和輸送量 toohello 雲端扮演了基本角色 StorSimple toodo hello 能力其工作。</span><span class="sxs-lookup"><span data-stu-id="46c60-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="46c60-126">StorSimple 是設計的 tooprovide 儲存體 tooapplications 妥善定義的工作集的資料 （熱資料） 上運作。</span><span class="sxs-lookup"><span data-stu-id="46c60-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="46c60-127">在此模型中，hello 工作集的資料儲存在 hello 本機層，而且 hello 剩餘非/冷/封存的資料集是階層式的 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="46c60-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="46c60-128">此模型會以 hello 遵循圖表示。</span><span class="sxs-lookup"><span data-stu-id="46c60-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="46c60-129">hello 幾乎單層綠色線條代表 hello hello 的 hello StorSimple 裝置的本機層上儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="46c60-130">hello 紅線表示 hello 總儲存在 hello StorSimple 解決方案，跨所有階層的資料量。</span><span class="sxs-lookup"><span data-stu-id="46c60-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="46c60-131">hello 間距 hello 單層綠色線條和 hello 指數的紅色曲線表示 hello 的 hello 雲端中儲存的資料量總計。</span><span class="sxs-lookup"><span data-stu-id="46c60-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="46c60-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="46c60-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span></span>

<span data-ttu-id="46c60-133">請注意這種架構，與您會發現 StorSimple 是適合的 toooperate 做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="46c60-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="46c60-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="46c60-135">執行您最常出現的還原從 hello 本機工作集的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="46c60-136">使用 hello 雲端異地災害復原和較舊的資料，其中還原就都是較不頻繁。</span><span class="sxs-lookup"><span data-stu-id="46c60-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="46c60-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="46c60-137">StorSimple benefits</span></span>

<span data-ttu-id="46c60-138">StorSimple 提供順暢地整合 Microsoft Azure 與內部部署解決方案，藉由運用無縫存取 tooon 內部部署和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="46c60-139">StorSimple 會使用自動 hello 在內部部署裝置，具有固態裝置 (SSD) 和序列連結 SCSI (SAS) 存放裝置，與 Azure 儲存體階層處理。</span><span class="sxs-lookup"><span data-stu-id="46c60-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="46c60-140">自動分層維持經常存取的本機 hello SSD 和 SAS 層上的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="46c60-141">它會移動不常存取的資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="46c60-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="46c60-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="46c60-143">使用 hello 雲端 tooachieve 前所未有的重複資料刪除層級的唯一重複資料刪除和壓縮演算法</span><span class="sxs-lookup"><span data-stu-id="46c60-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="46c60-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="46c60-144">High availability</span></span>
-   <span data-ttu-id="46c60-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="46c60-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="46c60-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="46c60-146">Azure integration</span></span>
-   <span data-ttu-id="46c60-147">Hello 雲端中的資料加密</span><span class="sxs-lookup"><span data-stu-id="46c60-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="46c60-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="46c60-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="46c60-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="46c60-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="46c60-150">壓縮和重複資料刪除，所有有 hello StorSimple 沒有。</span><span class="sxs-lookup"><span data-stu-id="46c60-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="46c60-151">順暢地傳送，並擷取 hello 雲端與 hello 應用程式和檔案系統之間的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="46c60-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="46c60-153">此外，您可以檢閱 hello[技術 StorSimple 8000 系列規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46c60-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="46c60-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="46c60-155">Architecture overview</span></span>

<span data-ttu-id="46c60-156">hello 下列表格顯示 hello 裝置模型-架構初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="46c60-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="46c60-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="46c60-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="46c60-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="46c60-158">Storage capacity</span></span>       | <span data-ttu-id="46c60-159">8100</span><span class="sxs-lookup"><span data-stu-id="46c60-159">8100</span></span>          | <span data-ttu-id="46c60-160">8600</span><span class="sxs-lookup"><span data-stu-id="46c60-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="46c60-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="46c60-161">Local storage capacity</span></span> | <span data-ttu-id="46c60-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="46c60-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="46c60-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="46c60-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="46c60-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="46c60-164">Cloud storage capacity</span></span> | <span data-ttu-id="46c60-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="46c60-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="46c60-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="46c60-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="46c60-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="46c60-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="46c60-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="46c60-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="46c60-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="46c60-169">Backup scenario</span></span>  | <span data-ttu-id="46c60-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="46c60-170">Local storage capacity</span></span>  | <span data-ttu-id="46c60-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="46c60-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="46c60-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="46c60-172">Primary backup</span></span>  | <span data-ttu-id="46c60-173">最新的備份儲存在本機儲存體的快速復原 toomeet 復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="46c60-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="46c60-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="46c60-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="46c60-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="46c60-175">Secondary backup</span></span> | <span data-ttu-id="46c60-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="46c60-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="46c60-177">N/A</span><span class="sxs-lookup"><span data-stu-id="46c60-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="46c60-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="46c60-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="46c60-179">在此案例中，StorSimple 磁碟區會呈現為 hello 備份的唯一儲存機制的 toohello 備份應用程式。</span><span class="sxs-lookup"><span data-stu-id="46c60-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="46c60-180">下列圖 hello 顯示中的所有備份使用 StorSimple 都分層磁碟區的備份和還原的方案架構。</span><span class="sxs-lookup"><span data-stu-id="46c60-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="46c60-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="46c60-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="46c60-183">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="46c60-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="46c60-184">hello 備份伺服器將資料寫入 toohello StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="46c60-185">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="46c60-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="46c60-186">快照集指令碼觸發 hello StorSimple snapshot manager （開始或刪除）。</span><span class="sxs-lookup"><span data-stu-id="46c60-186">A snapshot script triggers hello StorSimple snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="46c60-187">hello 備份伺服器會刪除過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="46c60-187">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="46c60-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="46c60-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="46c60-189">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="46c60-190">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="46c60-191">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="46c60-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="46c60-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="46c60-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="46c60-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="46c60-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="46c60-194">hello 下圖顯示的架構中的初始備份及還原高效能的目標磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="46c60-195">這些備份複製並封存的 tooa StorSimple 分層磁碟區上設定的排程。</span><span class="sxs-lookup"><span data-stu-id="46c60-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="46c60-196">它是重要的 toosize 高效能磁碟區，它可以處理保留原則容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-196">It's important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="46c60-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="46c60-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="46c60-199">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="46c60-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="46c60-200">hello 備份伺服器寫入資料 toohigh 能儲存體。</span><span class="sxs-lookup"><span data-stu-id="46c60-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="46c60-201">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="46c60-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="46c60-202">hello 備份伺服器複製備份 tooStorSimple 根據保留原則。</span><span class="sxs-lookup"><span data-stu-id="46c60-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="46c60-203">快照集指令碼觸發 hello StorSimple snapshot manager （開始或刪除）。</span><span class="sxs-lookup"><span data-stu-id="46c60-203">A snapshot script triggers hello StorSimple snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="46c60-204">hello 備份伺服器刪除 hello 過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="46c60-204">hello backup server deletes hello expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="46c60-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="46c60-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="46c60-206">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="46c60-207">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="46c60-208">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="46c60-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="46c60-209">部署 hello 方案</span><span class="sxs-lookup"><span data-stu-id="46c60-209">Deploy hello solution</span></span>

<span data-ttu-id="46c60-210">部署此解決方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="46c60-210">Deploying this solution requires three steps:</span></span>
1. <span data-ttu-id="46c60-211">準備 hello 網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="46c60-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="46c60-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="46c60-213">部署 Veritas NetBackup。</span><span class="sxs-lookup"><span data-stu-id="46c60-213">Deploy Veritas NetBackup.</span></span>

<span data-ttu-id="46c60-214">每個步驟是在 hello 下列各節中詳細討論。</span><span class="sxs-lookup"><span data-stu-id="46c60-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="46c60-215">設定 hello 網路</span><span class="sxs-lookup"><span data-stu-id="46c60-215">Set up hello network</span></span>

<span data-ttu-id="46c60-216">StorSimple 是與 hello Azure 雲端整合解決方案，因為 StorSimple 會需要使用中且正在運作的連線 toohello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="46c60-216">Because StorSimple is a solution that's integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="46c60-217">作業，像是雲端快照集、 資料管理和中繼資料傳輸和 tootier 較舊且較少存取的資料 tooAzure 雲端存放裝置，則使用此連接。</span><span class="sxs-lookup"><span data-stu-id="46c60-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="46c60-218">Hello 方案 tooperform 最佳情況是，我們建議您遵循這些網路的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="46c60-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="46c60-219">連接 hello StorSimple 分層 tooAzure hello 連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-219">hello link that connects hello StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="46c60-220">tooachieve，套用 hello 適當服務品質 (QoS) 層級 tooyour 基礎結構交換器 toomatch 您 RPO 和復原時間目標 (RTO) Sla。</span><span class="sxs-lookup"><span data-stu-id="46c60-220">tooachieve this, apply hello proper Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>

-   <span data-ttu-id="46c60-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="46c60-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="46c60-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="46c60-222">Deploy StorSimple</span></span>

<span data-ttu-id="46c60-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-netbackup"></a><span data-ttu-id="46c60-224">部署 NetBackup</span><span class="sxs-lookup"><span data-stu-id="46c60-224">Deploy NetBackup</span></span>

<span data-ttu-id="46c60-225">如需逐步 NetBackup 7.7.x 部署指導，請參閱 hello [NetBackup 7.7.x 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="46c60-225">For step-by-step NetBackup 7.7.x deployment guidance, see hello [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="46c60-226">設定 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="46c60-226">Set up hello solution</span></span>

<span data-ttu-id="46c60-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="46c60-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="46c60-228">hello 下列的範例和建議事項說明 hello 最基本也最基本的實作。</span><span class="sxs-lookup"><span data-stu-id="46c60-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="46c60-229">此實作中可能不適用，直接 tooyour 特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="46c60-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="46c60-230">Set up StorSimple</span></span>

| <span data-ttu-id="46c60-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="46c60-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="46c60-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="46c60-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="46c60-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="46c60-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="46c60-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="46c60-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="46c60-235">開啟 hello 備份目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-235">Turn on hello backup target.</span></span> | <span data-ttu-id="46c60-236">使用這些命令 tooturn 上或備份的目標模式和 tooget 狀態為關閉。</span><span class="sxs-lookup"><span data-stu-id="46c60-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="46c60-237">如需詳細資訊，請參閱[遠端連線 tooa StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="46c60-238">備份模式 tooturn: `Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="46c60-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="46c60-239">備份模式關閉 tooturn: `Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="46c60-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="46c60-240">tooget hello 目前狀態的備份模式設定： `Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="46c60-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="46c60-241">建立您將 hello 備份資料儲存的磁碟區的一般磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="46c60-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="46c60-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="46c60-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="46c60-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="46c60-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="46c60-245">建立磁碟區大小為預期的關閉 toohello 使用量越好，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="46c60-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="46c60-246">如需有關資訊 toosize 磁碟區，閱讀有關[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="46c60-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="46c60-247">使用 StorSimple 分層磁碟區，並選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="46c60-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="46c60-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="46c60-249">建立所有 hello 備份目標磁碟區的唯一 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="46c60-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="46c60-250">StorSimple 的備份原則定義 hello 磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="46c60-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="46c60-251">停用 hello 排程，因為到期 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="46c60-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="46c60-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="46c60-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="46c60-253">設定 hello 主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="46c60-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="46c60-254">設定 hello 主機備份伺服器儲存體，根據 toothese 指導方針：</span><span class="sxs-lookup"><span data-stu-id="46c60-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="46c60-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)；不支援合併磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span></span>
- <span data-ttu-id="46c60-256">使用 64 KB 配置大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-256">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="46c60-257">對應 hello StorSimple 磁碟區直接 toohello NetBackup 伺服器。</span><span class="sxs-lookup"><span data-stu-id="46c60-257">Map hello StorSimple volumes directly toohello NetBackup server.</span></span>
    - <span data-ttu-id="46c60-258">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="46c60-258">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="46c60-259">虛擬伺服器請使用傳遞磁碟。</span><span class="sxs-lookup"><span data-stu-id="46c60-259">Use pass-through disks for virtual servers.</span></span>


## <a name="best-practices-for-storsimple-and-netbackup"></a><span data-ttu-id="46c60-260">StorSimple 和 NetBackup 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="46c60-260">Best practices for StorSimple and NetBackup</span></span>

<span data-ttu-id="46c60-261">設定您的解決方案，根據 toohello hello 下列幾節中的指導方針。</span><span class="sxs-lookup"><span data-stu-id="46c60-261">Set up your solution according toohello guidelines in hello following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="46c60-262">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="46c60-262">Operating system best practices</span></span>

-   <span data-ttu-id="46c60-263">停用 Windows Server 的加密和 hello NTFS 檔案系統的重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="46c60-263">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="46c60-264">停用 hello StorSimple 磁碟區上的 Windows 伺服器磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="46c60-264">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="46c60-265">停用 Windows hello 索引 StorSimple 磁碟區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="46c60-265">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="46c60-266">在 hello （不是針對 hello StorSimple 磁碟區） 的來源主機上執行的防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="46c60-266">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="46c60-267">關閉 hello 預設[Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)工作管理員 中。</span><span class="sxs-lookup"><span data-stu-id="46c60-267">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="46c60-268">執行下列其中一 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="46c60-268">Do this in one of hello following ways:</span></span>
    - <span data-ttu-id="46c60-269">關閉 Windows 工作排程器中的 hello 維護 configurator。</span><span class="sxs-lookup"><span data-stu-id="46c60-269">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="46c60-270">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="46c60-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="46c60-271">下載 PsExec 之後，請以系統管理員身分執行 Windows PowerShell 並輸入：</span><span class="sxs-lookup"><span data-stu-id="46c60-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="46c60-272">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="46c60-272">StorSimple best practices</span></span>

-   <span data-ttu-id="46c60-273">請務必更新該 hello StorSimple 裝置時太[Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-273">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="46c60-274">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="46c60-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="46c60-275">您可以使用專用的 iSCSI 連線的 StorSimple 與 hello 備份的伺服器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="46c60-275">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
-   <span data-ttu-id="46c60-276">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="46c60-277">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="46c60-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="netbackup-best-practices"></a><span data-ttu-id="46c60-278">NetBackup 最佳作法</span><span class="sxs-lookup"><span data-stu-id="46c60-278">NetBackup best practices</span></span>

-   <span data-ttu-id="46c60-279">hello NetBackup 資料庫應該是本機 toohello 伺服器，而且在 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-279">hello NetBackup database should be local toohello server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="46c60-280">災害復原，備份 hello NetBackup 資料庫上的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-280">For disaster recovery, back up hello NetBackup database on a StorSimple volume.</span></span>
-   <span data-ttu-id="46c60-281">我們支援 NetBackup 完整和增量備份 （也參考的 tooas 差異增量備份中 NetBackup） 針對此解決方案。</span><span class="sxs-lookup"><span data-stu-id="46c60-281">We support NetBackup full and incremental backups (also referred tooas differential incremental backups in NetBackup) for this solution.</span></span> <span data-ttu-id="46c60-282">建議您不要使用綜合和累積增量備份。</span><span class="sxs-lookup"><span data-stu-id="46c60-282">We recommend that you do not use synthetic and cumulative incremental backups.</span></span>
-   <span data-ttu-id="46c60-283">備份資料檔案應包含只有 hello 特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-283">Backup data files should contain only hello data for a specific job.</span></span> <span data-ttu-id="46c60-284">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="46c60-284">For example, no media appends across different jobs are allowed.</span></span>

<span data-ttu-id="46c60-285">Hello NetBackup 最新的設定和最佳做法的實作這些需求，請參閱 hello NetBackup 文件，網址[www.veritas.com](https://www.veritas.com)。</span><span class="sxs-lookup"><span data-stu-id="46c60-285">For hello latest NetBackup settings and best practices for implementing these requirements, see hello NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span></span>


## <a name="retention-policies"></a><span data-ttu-id="46c60-286">保留原則</span><span class="sxs-lookup"><span data-stu-id="46c60-286">Retention policies</span></span>

<span data-ttu-id="46c60-287">Hello 最常見的備份保留原則類型的其中一個是祖父、 父親和 Son (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="46c60-287">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="46c60-288">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="46c60-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="46c60-289">此原則會產生六個 StorSimple 分層磁碟區： 一個磁碟區包含 hello 每週、 每月和每年完整備份。hello 其他五個磁碟區儲存每日增量備份。</span><span class="sxs-lookup"><span data-stu-id="46c60-289">This policy results in six StorSimple tiered volumes: one volume contains hello weekly, monthly, and yearly full backups; hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="46c60-290">在下列範例的 hello，我們會使用 GFS 旋轉。</span><span class="sxs-lookup"><span data-stu-id="46c60-290">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="46c60-291">hello 範例假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="46c60-291">hello example assumes hello following:</span></span>

-   <span data-ttu-id="46c60-292">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-292">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="46c60-293">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="46c60-293">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="46c60-294">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="46c60-294">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="46c60-295">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="46c60-295">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="46c60-296">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="46c60-296">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="46c60-297">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="46c60-297">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="46c60-298">根據上述假設 hello，建立 26 TiB StorSimple 分層 hello 每月和每年完整備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-298">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="46c60-299">建立 5 TiB StorSimple hello 的每日增量備份的每個分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-299">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="46c60-300">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="46c60-300">Backup type retention</span></span> | <span data-ttu-id="46c60-301">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-301">Size (TiB)</span></span> | <span data-ttu-id="46c60-302">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="46c60-302">GFS multiplier\*</span></span> | <span data-ttu-id="46c60-303">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-303">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="46c60-304">每週完整</span><span class="sxs-lookup"><span data-stu-id="46c60-304">Weekly full</span></span> | <span data-ttu-id="46c60-305">1</span><span class="sxs-lookup"><span data-stu-id="46c60-305">1</span></span> | <span data-ttu-id="46c60-306">4</span><span class="sxs-lookup"><span data-stu-id="46c60-306">4</span></span>  | <span data-ttu-id="46c60-307">4</span><span class="sxs-lookup"><span data-stu-id="46c60-307">4</span></span> |
| <span data-ttu-id="46c60-308">每日增量</span><span class="sxs-lookup"><span data-stu-id="46c60-308">Daily incremental</span></span> | <span data-ttu-id="46c60-309">0.5</span><span class="sxs-lookup"><span data-stu-id="46c60-309">0.5</span></span> | <span data-ttu-id="46c60-310">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="46c60-310">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="46c60-311">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="46c60-311">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="46c60-312">每月完整</span><span class="sxs-lookup"><span data-stu-id="46c60-312">Monthly full</span></span> | <span data-ttu-id="46c60-313">1</span><span class="sxs-lookup"><span data-stu-id="46c60-313">1</span></span> | <span data-ttu-id="46c60-314">12</span><span class="sxs-lookup"><span data-stu-id="46c60-314">12</span></span> | <span data-ttu-id="46c60-315">12</span><span class="sxs-lookup"><span data-stu-id="46c60-315">12</span></span> |
| <span data-ttu-id="46c60-316">每年完整</span><span class="sxs-lookup"><span data-stu-id="46c60-316">Yearly full</span></span> | <span data-ttu-id="46c60-317">1</span><span class="sxs-lookup"><span data-stu-id="46c60-317">1</span></span>  | <span data-ttu-id="46c60-318">10</span><span class="sxs-lookup"><span data-stu-id="46c60-318">10</span></span> | <span data-ttu-id="46c60-319">10</span><span class="sxs-lookup"><span data-stu-id="46c60-319">10</span></span> |
| <span data-ttu-id="46c60-320">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="46c60-320">GFS requirement</span></span> |   | <span data-ttu-id="46c60-321">38</span><span class="sxs-lookup"><span data-stu-id="46c60-321">38</span></span> |   |
| <span data-ttu-id="46c60-322">其他配額</span><span class="sxs-lookup"><span data-stu-id="46c60-322">Additional quota</span></span>  | <span data-ttu-id="46c60-323">4</span><span class="sxs-lookup"><span data-stu-id="46c60-323">4</span></span>  |   | <span data-ttu-id="46c60-324">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="46c60-324">42 total GFS requirement</span></span>  |
<span data-ttu-id="46c60-325">\*hello GFS 乘數是 hello 的數字的複本需要 tooprotect 和保留 toomeet 您備份原則的需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-325">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-netbackup-storage"></a><span data-ttu-id="46c60-326">設定 NetBackup 儲存體</span><span class="sxs-lookup"><span data-stu-id="46c60-326">Set up NetBackup storage</span></span>

### <a name="tooset-up-netbackup-storage"></a><span data-ttu-id="46c60-327">tooset NetBackup 存放裝置</span><span class="sxs-lookup"><span data-stu-id="46c60-327">tooset up NetBackup storage</span></span>

1.  <span data-ttu-id="46c60-328">在 hello NetBackup 管理主控台中，選取 **媒體和裝置管理** > **裝置** > **磁碟集區**。</span><span class="sxs-lookup"><span data-stu-id="46c60-328">In hello NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span></span> <span data-ttu-id="46c60-329">在 hello 磁碟集區設定精靈，選取 hello 儲存伺服器類型**AdvancedDisk**，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="46c60-329">In hello Disk Pool Configuration Wizard, select hello storage server type **AdvancedDisk**, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，磁碟集區設定精靈](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  <span data-ttu-id="46c60-331">選取您的伺服器，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="46c60-331">Select your server, and then select **Next**.</span></span>

    ![NetBackup 管理主控台中，選取 hello 伺服器](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  <span data-ttu-id="46c60-333">選取您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-333">Select your StorSimple volume.</span></span>

    ![NetBackup 管理主控台中，選取 hello StorSimple 磁碟區磁碟](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  <span data-ttu-id="46c60-335">輸入 hello 備份目標的名稱，然後選取**下一步** > **下一步**toofinish hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="46c60-335">Enter a name for hello backup target, and then select **Next** > **Next** toofinish hello wizard.</span></span>

5.  <span data-ttu-id="46c60-336">檢閱 hello 設定，然後選取**完成**。</span><span class="sxs-lookup"><span data-stu-id="46c60-336">Review hello settings, and then select **Finish**.</span></span>

6.  <span data-ttu-id="46c60-337">在每個磁碟區指派 hello 最後，變更這些建議中的 hello 存放裝置設定 toomatch [StorSimple 和 NetBackup 最佳作法](#best-practices-for-storsimple-and-netbackup)。</span><span class="sxs-lookup"><span data-stu-id="46c60-337">At hello end of each volume assignment, change hello storage device settings toomatch those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span></span>

7. <span data-ttu-id="46c60-338">重複步驟 1-6，直到完成指派 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span></span>

    ![NetBackup 管理主控台，磁碟設定](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="46c60-340">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="46c60-340">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="46c60-341">從已分層式的 toohello 雲端備份資料還原發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="46c60-341">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="46c60-342">hello 下圖顯示典型的磁碟區 tooa 備份工作的 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="46c60-342">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="46c60-343">在此情況下，所有的 hello 每週備份對應 toohello 星期六磁碟已滿，而 hello 增量備份對應 tooMonday 星期五累加磁碟。</span><span class="sxs-lookup"><span data-stu-id="46c60-343">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="46c60-344">所有 hello 備份與還原就都是從 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-344">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![<span data-ttu-id="46c60-345">主要備份目標組態的邏輯圖</span><span class="sxs-lookup"><span data-stu-id="46c60-345">Primary backup target configuration logical diagram</span></span> ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="46c60-346">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="46c60-346">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="46c60-347">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="46c60-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="46c60-348">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="46c60-348">Frequency/backup type</span></span> | <span data-ttu-id="46c60-349">完整</span><span class="sxs-lookup"><span data-stu-id="46c60-349">Full</span></span> | <span data-ttu-id="46c60-350">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-350">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="46c60-351">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="46c60-351">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="46c60-352">星期六</span><span class="sxs-lookup"><span data-stu-id="46c60-352">Saturday</span></span> | <span data-ttu-id="46c60-353">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="46c60-353">Monday-Friday</span></span> |
| <span data-ttu-id="46c60-354">每月</span><span class="sxs-lookup"><span data-stu-id="46c60-354">Monthly</span></span>  | <span data-ttu-id="46c60-355">星期六</span><span class="sxs-lookup"><span data-stu-id="46c60-355">Saturday</span></span>  |   |
| <span data-ttu-id="46c60-356">每年</span><span class="sxs-lookup"><span data-stu-id="46c60-356">Yearly</span></span> | <span data-ttu-id="46c60-357">星期六</span><span class="sxs-lookup"><span data-stu-id="46c60-357">Saturday</span></span>  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a><span data-ttu-id="46c60-358">指派 StorSimple 磁碟區 tooa NetBackup 備份作業</span><span class="sxs-lookup"><span data-stu-id="46c60-358">Assigning StorSimple volumes tooa NetBackup backup job</span></span>

<span data-ttu-id="46c60-359">下列順序的 hello 假設 NetBackup 和 hello 目標主機設定依據 hello NetBackup 代理程式的指導方針。</span><span class="sxs-lookup"><span data-stu-id="46c60-359">hello following sequence assumes that NetBackup and hello target host are configured in accordance with hello NetBackup agent guidelines.</span></span>

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a><span data-ttu-id="46c60-360">tooassign StorSimple 磁碟區 tooa NetBackup 備份工作</span><span class="sxs-lookup"><span data-stu-id="46c60-360">tooassign StorSimple volumes tooa NetBackup backup job</span></span>

1.  <span data-ttu-id="46c60-361">在 hello NetBackup 管理主控台中，選取  **NetBackup 管理**，以滑鼠右鍵按一下**原則**，然後選取**新原則**。</span><span class="sxs-lookup"><span data-stu-id="46c60-361">In hello NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span></span>

    ![NetBackup 管理主控台，建立新的原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  <span data-ttu-id="46c60-363">在 hello**新增原則**對話方塊中，輸入 hello 原則的名稱，然後選取 hello**使用原則設定精靈**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="46c60-363">In hello **Add a New Policy** dialog box, enter a name for hello policy, and then select hello **Use Policy Configuration Wizard** check box.</span></span> <span data-ttu-id="46c60-364">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="46c60-364">Select **OK**.</span></span>

    ![NetBackup 管理主控台，新增原則對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  <span data-ttu-id="46c60-366">在 hello 備份原則設定精靈，選擇 hello 備份類型，然後再選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="46c60-366">In hello Backup Policy Configuration Wizard, elect hello backup type you want, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，選取備份類型](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  <span data-ttu-id="46c60-368">tooset hello 原則類型，選取**標準**，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="46c60-368">tooset hello policy type, select **Standard**, and then select **Next**.</span></span>

    ![NetBackup 管理主控台，選取原則類型](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  <span data-ttu-id="46c60-370">選取您的主機選取 hello**偵測用戶端作業系統**核取方塊，然後再選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="46c60-370">Select your host, select hello **Detect client operating system** check box, and then select **Add**.</span></span> <span data-ttu-id="46c60-371">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="46c60-371">Select **Next**.</span></span>

    ![NetBackup 管理主控台，列出新原則中的用戶端](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  <span data-ttu-id="46c60-373">選取您想 tooback hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="46c60-373">Select hello drives you want tooback up.</span></span>

    ![NetBackup 管理主控台，新原則的備份選取項目](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  <span data-ttu-id="46c60-375">選取 hello 頻率和保留值符合您備份旋轉的需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-375">Select hello frequency and retention values that meet your backup rotation requirements.</span></span>

    ![NetBackup 管理主控台，新原則的備份頻率和循環](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  <span data-ttu-id="46c60-377">選取 [下一步] > [下一步] > [完成]。</span><span class="sxs-lookup"><span data-stu-id="46c60-377">Select **Next** > **Next** > **Finish**.</span></span>  <span data-ttu-id="46c60-378">建立 hello 原則之後，您可以修改 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="46c60-378">You can modify hello schedule after hello policy is created.</span></span>

9.  <span data-ttu-id="46c60-379">選取您剛才 tooexpand hello 原則建立、，然後選取**排程**。</span><span class="sxs-lookup"><span data-stu-id="46c60-379">Select tooexpand hello policy you just created, and then select **Schedules**.</span></span>

    ![NetBackup 管理主控台，新原則的排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  <span data-ttu-id="46c60-381">以滑鼠右鍵按一下**差異 Inc**，選取**複製 toonew**，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="46c60-381">Right-click **Differential-Inc**, select **Copy toonew**, and then select **OK**.</span></span>

    ![NetBackup 管理主控台中，複製排程 tooa 新原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  <span data-ttu-id="46c60-383">以滑鼠右鍵按一下新建立的 hello 排程，然後選取**變更**。</span><span class="sxs-lookup"><span data-stu-id="46c60-383">Right-click hello newly created schedule, and then select **Change**.</span></span>

12.  <span data-ttu-id="46c60-384">在 hello**屬性**索引標籤，選取 hello**覆寫原則存放區選取**核取方塊，，然後選取 hello 星期一增量備份位置的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-384">On hello **Attributes** tab, select hello **Override policy storage selection** check box, and then select hello volume where Monday incremental backups go.</span></span>

    ![NetBackup 管理主控台，變更排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  <span data-ttu-id="46c60-386">在 hello**開始視窗**索引標籤，選取 hello 備份的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="46c60-386">On hello **Start Window** tab, select hello time window for your backups.</span></span>

    ![NetBackup 管理主控台，變更開始時間範圍](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  <span data-ttu-id="46c60-388">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="46c60-388">Select **OK**.</span></span>

15.  <span data-ttu-id="46c60-389">針對每個增量備份重複步驟 10-14。</span><span class="sxs-lookup"><span data-stu-id="46c60-389">Repeat steps 10-14 for each incremental backup.</span></span> <span data-ttu-id="46c60-390">選取 hello 適當的磁碟區和每個您所建立的備份排程。</span><span class="sxs-lookup"><span data-stu-id="46c60-390">Select hello appropriate volume and schedule for each backup you create.</span></span>

16.  <span data-ttu-id="46c60-391">以滑鼠右鍵按一下 hello**差異 Inc**排程，然後再刪除它。</span><span class="sxs-lookup"><span data-stu-id="46c60-391">Right-click hello **Differential-Inc** schedule, and then delete it.</span></span>

17.  <span data-ttu-id="46c60-392">修改您的備份需要您完整排程 toomeet。</span><span class="sxs-lookup"><span data-stu-id="46c60-392">Modify your Full schedule toomeet your backup needs.</span></span>

    ![NetBackup 管理主控台，變更完整排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  <span data-ttu-id="46c60-394">變更 hello 開始視窗。</span><span class="sxs-lookup"><span data-stu-id="46c60-394">Change hello start window.</span></span>

    ![NetBackup 管理主控台中，變更 hello 開始視窗](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  <span data-ttu-id="46c60-396">hello 最終排程看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="46c60-396">hello final schedule looks like this:</span></span>

    ![NetBackup 管理主控台，變更排程](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="46c60-398">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="46c60-398">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="46c60-399">從已分層式的 toohello 雲端備份資料還原發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="46c60-399">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="46c60-400">在此模型中，您必須擁有儲存媒體 （非 StorSimple) tooserve 暫時快取。</span><span class="sxs-lookup"><span data-stu-id="46c60-400">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="46c60-401">例如，您可以使用獨立磁碟 (RAID) 磁碟區 tooaccommodate 空間、 輸入/輸出 (I/O) 和頻寬的備援陣列。</span><span class="sxs-lookup"><span data-stu-id="46c60-401">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="46c60-402">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="46c60-402">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="46c60-403">hello 下圖顯示典型短期保留本機 （toohello 伺服器） 的磁碟區和長期的保留封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-403">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="46c60-404">在此案例中，所有備份上都執行本機 hello （toohello 伺服器） RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-404">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="46c60-405">定期重複這些備份和封存的 tooan 封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-405">These backups are periodically duplicated and archived tooan archives volume.</span></span> <span data-ttu-id="46c60-406">它是本機 （toohello 伺服器） 的重要 toosize RAID 磁碟區，好讓它可以處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-406">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="46c60-407">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="46c60-407">StorSimple as a secondary backup target GFS example</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

<span data-ttu-id="46c60-409">hello 下表顯示如何 tooset 向上備份 toorun hello 本機和 StorSimple 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="46c60-409">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="46c60-410">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-410">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="46c60-411">備份設定和容量需求</span><span class="sxs-lookup"><span data-stu-id="46c60-411">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="46c60-412">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="46c60-412">Backup type and retention</span></span> | <span data-ttu-id="46c60-413">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="46c60-413">Configured storage</span></span> | <span data-ttu-id="46c60-414">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-414">Size (TiB)</span></span> | <span data-ttu-id="46c60-415">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="46c60-415">GFS multiplier</span></span> | <span data-ttu-id="46c60-416">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-416">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="46c60-417">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="46c60-417">Week 1 (full and incremental)</span></span> |<span data-ttu-id="46c60-418">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="46c60-418">Local disk (short-term)</span></span>| <span data-ttu-id="46c60-419">1</span><span class="sxs-lookup"><span data-stu-id="46c60-419">1</span></span> | <span data-ttu-id="46c60-420">1</span><span class="sxs-lookup"><span data-stu-id="46c60-420">1</span></span> | <span data-ttu-id="46c60-421">1</span><span class="sxs-lookup"><span data-stu-id="46c60-421">1</span></span> |
| <span data-ttu-id="46c60-422">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="46c60-422">StorSimple weeks 2-4</span></span> |<span data-ttu-id="46c60-423">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="46c60-423">StorSimple disk (long-term)</span></span> | <span data-ttu-id="46c60-424">1</span><span class="sxs-lookup"><span data-stu-id="46c60-424">1</span></span> | <span data-ttu-id="46c60-425">4</span><span class="sxs-lookup"><span data-stu-id="46c60-425">4</span></span> | <span data-ttu-id="46c60-426">4</span><span class="sxs-lookup"><span data-stu-id="46c60-426">4</span></span> |
| <span data-ttu-id="46c60-427">每月完整</span><span class="sxs-lookup"><span data-stu-id="46c60-427">Monthly full</span></span> |<span data-ttu-id="46c60-428">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="46c60-428">StorSimple disk (long-term)</span></span> | <span data-ttu-id="46c60-429">1</span><span class="sxs-lookup"><span data-stu-id="46c60-429">1</span></span> | <span data-ttu-id="46c60-430">12</span><span class="sxs-lookup"><span data-stu-id="46c60-430">12</span></span> | <span data-ttu-id="46c60-431">12</span><span class="sxs-lookup"><span data-stu-id="46c60-431">12</span></span> |
| <span data-ttu-id="46c60-432">每年完整</span><span class="sxs-lookup"><span data-stu-id="46c60-432">Yearly full</span></span> |<span data-ttu-id="46c60-433">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="46c60-433">StorSimple disk (long-term)</span></span> | <span data-ttu-id="46c60-434">1</span><span class="sxs-lookup"><span data-stu-id="46c60-434">1</span></span> | <span data-ttu-id="46c60-435">1</span><span class="sxs-lookup"><span data-stu-id="46c60-435">1</span></span> | <span data-ttu-id="46c60-436">1</span><span class="sxs-lookup"><span data-stu-id="46c60-436">1</span></span> |
|<span data-ttu-id="46c60-437">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="46c60-437">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="46c60-438">18*</span><span class="sxs-lookup"><span data-stu-id="46c60-438">18*</span></span>|
<span data-ttu-id="46c60-439">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="46c60-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="46c60-440">GFS 範例排程：每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="46c60-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="46c60-441">週</span><span class="sxs-lookup"><span data-stu-id="46c60-441">Week</span></span> | <span data-ttu-id="46c60-442">完整</span><span class="sxs-lookup"><span data-stu-id="46c60-442">Full</span></span> | <span data-ttu-id="46c60-443">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-443">Incremental day 1</span></span> | <span data-ttu-id="46c60-444">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-444">Incremental day 2</span></span> | <span data-ttu-id="46c60-445">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-445">Incremental day 3</span></span> | <span data-ttu-id="46c60-446">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-446">Incremental day 4</span></span> | <span data-ttu-id="46c60-447">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="46c60-447">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="46c60-448">第 1 週</span><span class="sxs-lookup"><span data-stu-id="46c60-448">Week 1</span></span> | <span data-ttu-id="46c60-449">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-449">Local RAID volume</span></span>  | <span data-ttu-id="46c60-450">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-450">Local RAID volume</span></span> | <span data-ttu-id="46c60-451">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-451">Local RAID volume</span></span> | <span data-ttu-id="46c60-452">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-452">Local RAID volume</span></span> | <span data-ttu-id="46c60-453">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-453">Local RAID volume</span></span> | <span data-ttu-id="46c60-454">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="46c60-454">Local RAID volume</span></span> |
| <span data-ttu-id="46c60-455">第 2 週</span><span class="sxs-lookup"><span data-stu-id="46c60-455">Week 2</span></span> | <span data-ttu-id="46c60-456">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="46c60-456">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="46c60-457">第 3 週</span><span class="sxs-lookup"><span data-stu-id="46c60-457">Week 3</span></span> | <span data-ttu-id="46c60-458">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="46c60-458">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="46c60-459">第 4 週</span><span class="sxs-lookup"><span data-stu-id="46c60-459">Week 4</span></span> | <span data-ttu-id="46c60-460">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="46c60-460">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="46c60-461">每月</span><span class="sxs-lookup"><span data-stu-id="46c60-461">Monthly</span></span> | <span data-ttu-id="46c60-462">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="46c60-462">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="46c60-463">每年</span><span class="sxs-lookup"><span data-stu-id="46c60-463">Yearly</span></span> | <span data-ttu-id="46c60-464">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="46c60-464">StorSimple yearly</span></span>  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a><span data-ttu-id="46c60-465">指派 StorSimple 磁碟區 tooa NetBackup 封存及重複工作</span><span class="sxs-lookup"><span data-stu-id="46c60-465">Assign StorSimple volumes tooa NetBackup archive and duplication job</span></span>

<span data-ttu-id="46c60-466">因為 NetBackup 提供各種不同的存放裝置和媒體管理選項，所以我們建議您諮詢 Veritas，或您 NetBackup 架構設計人員 tooproperly 評估儲存空間的生命週期原則 (SLP) 需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect tooproperly assess your storage lifecycle policy (SLP) requirements.</span></span>

<span data-ttu-id="46c60-467">定義 hello 初始磁碟集區之後，您需要三個額外的存放裝置生命週期原則 toodefine，總共有四個原則：</span><span class="sxs-lookup"><span data-stu-id="46c60-467">After you've defined hello initial disk pools, you need toodefine three additional storage lifecycle policies, for a total of four policies:</span></span>
* <span data-ttu-id="46c60-468">LocalRAIDVolume</span><span class="sxs-lookup"><span data-stu-id="46c60-468">LocalRAIDVolume</span></span>
* <span data-ttu-id="46c60-469">StorSimpleWeek2-4</span><span class="sxs-lookup"><span data-stu-id="46c60-469">StorSimpleWeek2-4</span></span>
* <span data-ttu-id="46c60-470">StorSimpleMonthlyFulls</span><span class="sxs-lookup"><span data-stu-id="46c60-470">StorSimpleMonthlyFulls</span></span>
* <span data-ttu-id="46c60-471">StorSimpleYearlyFulls</span><span class="sxs-lookup"><span data-stu-id="46c60-471">StorSimpleYearlyFulls</span></span>

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a><span data-ttu-id="46c60-472">tooassign StorSimple 磁碟區 tooa NetBackup 封存和複製作業</span><span class="sxs-lookup"><span data-stu-id="46c60-472">tooassign StorSimple volumes tooa NetBackup archive and duplication job</span></span>

1.  <span data-ttu-id="46c60-473">在 hello NetBackup 管理主控台中，選取 **儲存體** > **儲存生命週期原則** > **新存放裝置生命週期原則**。</span><span class="sxs-lookup"><span data-stu-id="46c60-473">In hello NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span></span>

    ![NetBackup 管理主控台，新增儲存體生命週期原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  <span data-ttu-id="46c60-475">輸入 hello 快照的名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="46c60-475">Enter a name for hello snapshot, and then select **Add**.</span></span>

3.  <span data-ttu-id="46c60-476">在 hello**新作業** 對話方塊上 hello**屬性**索引標籤上，針對**作業**，選取**備份**。</span><span class="sxs-lookup"><span data-stu-id="46c60-476">In hello **New Operation** dialog box, on hello **Properties** tab, for **Operation**, select **Backup**.</span></span> <span data-ttu-id="46c60-477">選取您想要的 hello 值**目的地儲存體**，**保留型別**，和**保留期限**。</span><span class="sxs-lookup"><span data-stu-id="46c60-477">Select hello values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span> <span data-ttu-id="46c60-478">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="46c60-478">Select **OK**.</span></span>

    ![NetBackup 管理主控台，新增作業對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    <span data-ttu-id="46c60-480">這會定義 hello 的第一個備份作業和儲存機制。</span><span class="sxs-lookup"><span data-stu-id="46c60-480">This defines hello first backup operation and repository.</span></span>

4.  <span data-ttu-id="46c60-481">選取 toohighlight hello 前一個作業，然後再選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="46c60-481">Select toohighlight hello previous operation, and then select **Add**.</span></span> <span data-ttu-id="46c60-482">在 hello**變更儲存體作業**對話方塊中，您想要選取 hello 值**目的地儲存體**，**保留型別**，和**保留期限**.</span><span class="sxs-lookup"><span data-stu-id="46c60-482">In hello **Change Storage Operation** dialog box, select hello values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span>

    ![NetBackup 管理主控台，變更儲存體作業對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  <span data-ttu-id="46c60-484">選取 toohighlight hello 前一個作業，然後再選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="46c60-484">Select toohighlight hello previous operation, and then select **Add**.</span></span> <span data-ttu-id="46c60-485">在 hello**新存放裝置生命週期原則**對話方塊方塊中，加入一年的每月備份。</span><span class="sxs-lookup"><span data-stu-id="46c60-485">In hello **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span></span>

    ![NetBackup 管理主控台，新增儲存體生命週期原則對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  <span data-ttu-id="46c60-487">重複步驟 4-5，直到您已建立您需要的 hello 完整 SLP 保留原則。</span><span class="sxs-lookup"><span data-stu-id="46c60-487">Repeat steps 4-5 until you've created hello comprehensive SLP retention policy that you need.</span></span>

    ![NetBackup 管理主控台中，在新的存放裝置生命週期原則對話方塊 hello 新增原則](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  <span data-ttu-id="46c60-489">當您完成定義您 SLP 保留原則，在**原則**，定義備份原則中詳述的 hello 步驟[指派 StorSimple 磁碟區 tooa NetBackup 備份工作](#assigning-storsimple-volumes-to-a-netbackup-backup-job)。</span><span class="sxs-lookup"><span data-stu-id="46c60-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following hello steps detailed in [Assigning StorSimple volumes tooa NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span></span>

8.  <span data-ttu-id="46c60-490">下**排程**，在 hello**變更排程**對話方塊中，以滑鼠右鍵按一下**完整**，然後選取**變更**。</span><span class="sxs-lookup"><span data-stu-id="46c60-490">Under **Schedules**, in hello **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span></span>

    ![NetBackup 管理主控台，變更排程對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  <span data-ttu-id="46c60-492">選取 hello**覆寫原則存放區選取**核取方塊，然後選取 hello SLP 保留原則，您在步驟 1-6 中建立。</span><span class="sxs-lookup"><span data-stu-id="46c60-492">Select hello **Override policy storage selection** check box, and then select hello SLP retention policy that you created in steps 1-6.</span></span>

    ![NetBackup 管理主控台，複寫原則儲存體選取項目](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  <span data-ttu-id="46c60-494">選取**確定**，然後重複 hello 增量備份排程。</span><span class="sxs-lookup"><span data-stu-id="46c60-494">Select **OK**, and then repeat for hello incremental backup schedule.</span></span>

    ![NetBackup 管理主控台，增量備份的 [變更排程] 對話方塊](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| <span data-ttu-id="46c60-496">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="46c60-496">Backup type retention</span></span> | <span data-ttu-id="46c60-497">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-497">Size (TiB)</span></span> | <span data-ttu-id="46c60-498">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="46c60-498">GFS multiplier\*</span></span> | <span data-ttu-id="46c60-499">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="46c60-499">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="46c60-500">每週完整</span><span class="sxs-lookup"><span data-stu-id="46c60-500">Weekly full</span></span> |  <span data-ttu-id="46c60-501">1</span><span class="sxs-lookup"><span data-stu-id="46c60-501">1</span></span>  |  <span data-ttu-id="46c60-502">4</span><span class="sxs-lookup"><span data-stu-id="46c60-502">4</span></span> | <span data-ttu-id="46c60-503">4</span><span class="sxs-lookup"><span data-stu-id="46c60-503">4</span></span>  |
| <span data-ttu-id="46c60-504">每日增量</span><span class="sxs-lookup"><span data-stu-id="46c60-504">Daily incremental</span></span>  | <span data-ttu-id="46c60-505">0.5</span><span class="sxs-lookup"><span data-stu-id="46c60-505">0.5</span></span>  | <span data-ttu-id="46c60-506">20 （循環是等於 toohello 每月的週數）</span><span class="sxs-lookup"><span data-stu-id="46c60-506">20 (cycles are equal toohello number of weeks per month)</span></span> | <span data-ttu-id="46c60-507">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="46c60-507">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="46c60-508">每月完整</span><span class="sxs-lookup"><span data-stu-id="46c60-508">Monthly full</span></span>  | <span data-ttu-id="46c60-509">1</span><span class="sxs-lookup"><span data-stu-id="46c60-509">1</span></span> | <span data-ttu-id="46c60-510">12</span><span class="sxs-lookup"><span data-stu-id="46c60-510">12</span></span> | <span data-ttu-id="46c60-511">12</span><span class="sxs-lookup"><span data-stu-id="46c60-511">12</span></span> |
| <span data-ttu-id="46c60-512">每年完整</span><span class="sxs-lookup"><span data-stu-id="46c60-512">Yearly full</span></span> | <span data-ttu-id="46c60-513">1</span><span class="sxs-lookup"><span data-stu-id="46c60-513">1</span></span>  | <span data-ttu-id="46c60-514">10</span><span class="sxs-lookup"><span data-stu-id="46c60-514">10</span></span> | <span data-ttu-id="46c60-515">10</span><span class="sxs-lookup"><span data-stu-id="46c60-515">10</span></span> |
| <span data-ttu-id="46c60-516">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="46c60-516">GFS requirement</span></span>  |     |     | <span data-ttu-id="46c60-517">38</span><span class="sxs-lookup"><span data-stu-id="46c60-517">38</span></span> |
| <span data-ttu-id="46c60-518">其他配額</span><span class="sxs-lookup"><span data-stu-id="46c60-518">Additional quota</span></span>  | <span data-ttu-id="46c60-519">4</span><span class="sxs-lookup"><span data-stu-id="46c60-519">4</span></span>  |    | <span data-ttu-id="46c60-520">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="46c60-520">42 total GFS requirement</span></span> |
<span data-ttu-id="46c60-521">\*hello GFS 乘數是 hello 的數字的複本需要 tooprotect 和保留 toomeet 您備份原則的需求。</span><span class="sxs-lookup"><span data-stu-id="46c60-521">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="46c60-522">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="46c60-522">StorSimple cloud snapshots</span></span>

<span data-ttu-id="46c60-523">StorSimple 雲端快照集保護位於您的 StorSimple 裝置中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="46c60-523">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="46c60-524">建立雲端快照集是對等 tooshipping 本機備份磁帶 tooan 異地設施。</span><span class="sxs-lookup"><span data-stu-id="46c60-524">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="46c60-525">如果您使用 Azure 地理備援儲存體，建立雲端快照是相等的 tooshipping 備份磁帶 toomultiple 站台。</span><span class="sxs-lookup"><span data-stu-id="46c60-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="46c60-526">如果您需要 toorestore 裝置在損毀之後，您可能會讓其他 StorSimple 裝置上線，並且進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="46c60-526">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="46c60-527">Hello 容錯移轉之後，您將無法 tooaccess hello 資料 （速度雲端） 從 hello 最新的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="46c60-527">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="46c60-528">hello 下列章節描述如何 toocreate 簡短的指令碼 toostart 和 delete StorSimple 雲端快照在備份後的處理期間。</span><span class="sxs-lookup"><span data-stu-id="46c60-528">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="46c60-529">手動或以程式設計方式建立的快照集未遵循 hello StorSimple 快照集的到期原則。</span><span class="sxs-lookup"><span data-stu-id="46c60-529">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="46c60-530">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="46c60-530">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="46c60-531">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="46c60-531">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="46c60-532">請仔細在刪除 StorSimple 快照集之前，先評估 hello 相容性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="46c60-532">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="46c60-533">如需有關如何 toorun 備份後指令碼，請參閱 hello [NetBackup 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="46c60-533">For more information about how toorun a post-backup script, see hello [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="46c60-534">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="46c60-534">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="46c60-536">需求</span><span class="sxs-lookup"><span data-stu-id="46c60-536">Requirements</span></span>

-   <span data-ttu-id="46c60-537">執行 hello 指令碼的 hello 伺服器必須具備存取 tooAzure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="46c60-537">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="46c60-538">hello 使用者帳戶必須擁有 hello 必要的權限。</span><span class="sxs-lookup"><span data-stu-id="46c60-538">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="46c60-539">StorSimple hello 與備份原則相關聯的 StorSimple 磁碟區必須設定，但未開啟。</span><span class="sxs-lookup"><span data-stu-id="46c60-539">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="46c60-540">您將需要 hello StorSimple 資源名稱、 登錄機碼、 裝置名稱和備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="46c60-540">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="46c60-541">toostart 或刪除的雲端快照</span><span class="sxs-lookup"><span data-stu-id="46c60-541">toostart or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="46c60-542">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="46c60-542">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="46c60-543">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="46c60-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="46c60-544">在 hello Azure 傳統入口網站中取得 hello 資源名稱和[StorSimple Manager 服務登錄機碼](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="46c60-544">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="46c60-545">Hello 在伺服器上執行 hello 指令碼，請以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="46c60-545">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="46c60-546">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="46c60-546">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="46c60-547">請注意 hello 備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="46c60-547">Note hello backup policy ID.</span></span>
5.  <span data-ttu-id="46c60-548">在記事本中，請使用下列程式碼的 hello 以建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="46c60-548">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="46c60-549">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="46c60-549">Copy and paste this code snippet:</span></span>
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
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      <span data-ttu-id="46c60-550">Hello PowerShell 指令碼 toohello 儲存相同的位置儲存您的 Azure 發行設定。</span><span class="sxs-lookup"><span data-stu-id="46c60-550">Save hello PowerShell script toohello same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="46c60-551">例如，儲存為 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1。</span><span class="sxs-lookup"><span data-stu-id="46c60-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="46c60-552">增益 NetBackup hello 指令碼 tooyour 備份工作。</span><span class="sxs-lookup"><span data-stu-id="46c60-552">Add hello script tooyour backup job in NetBackup.</span></span> <span data-ttu-id="46c60-553">toodo，編輯您 NetBackup 作業選項預先處理和後置處理指令。</span><span class="sxs-lookup"><span data-stu-id="46c60-553">toodo this, edit your NetBackup job options' pre-processing and post-processing commands.</span></span>

> [!NOTE]
> <span data-ttu-id="46c60-554">我們建議做為後置處理指令碼執行 StorSimple 雲端快照集備份原則，在您每日備份工作的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="46c60-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="46c60-555">如需有關如何向上 tooback 和還原您備份應用程式環境 toohelp 您符合您的 RPO 和 RTO，請參閱與您備份的架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="46c60-555">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="46c60-556">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="46c60-556">StorSimple as a restore source</span></span>

<span data-ttu-id="46c60-557">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="46c60-557">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="46c60-558">還原的是階層式的 toohello 雲端的資料就會發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="46c60-558">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="46c60-559">對於本機資料，還原發生 hello 裝置 hello 本機磁碟速度。</span><span class="sxs-lookup"><span data-stu-id="46c60-559">For local data, restores occur at hello local disk speed of hello device.</span></span> <span data-ttu-id="46c60-560">如需有關資訊 tooperform 還原，請參閱 hello [NetBackup 文件](http://www.veritas.com/docs/000094423)。</span><span class="sxs-lookup"><span data-stu-id="46c60-560">For information about how tooperform a restore, see hello [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span> <span data-ttu-id="46c60-561">我們建議您符合 tooNetBackup 還原最佳作法。</span><span class="sxs-lookup"><span data-stu-id="46c60-561">We recommend that you conform tooNetBackup restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="46c60-562">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="46c60-562">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="46c60-563">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="46c60-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="46c60-564">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="46c60-564">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="46c60-565">hello 下表列出常見的嚴重損壞修復案例。</span><span class="sxs-lookup"><span data-stu-id="46c60-565">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="46c60-566">案例</span><span class="sxs-lookup"><span data-stu-id="46c60-566">Scenario</span></span> | <span data-ttu-id="46c60-567">影響</span><span class="sxs-lookup"><span data-stu-id="46c60-567">Impact</span></span> | <span data-ttu-id="46c60-568">如何 toorecover</span><span class="sxs-lookup"><span data-stu-id="46c60-568">How toorecover</span></span> | <span data-ttu-id="46c60-569">注意事項</span><span class="sxs-lookup"><span data-stu-id="46c60-569">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="46c60-570">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="46c60-570">StorSimple device failure</span></span> | <span data-ttu-id="46c60-571">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="46c60-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="46c60-572">取代 hello 失敗的裝置，並執行[StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-572">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="46c60-573">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="46c60-573">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="46c60-574">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="46c60-574">All operations are at cloud speeds.</span></span> <span data-ttu-id="46c60-575">hello 索引和目錄重新掃描程序可能會導致所有備份組 toobe 掃描並取自 hello 雲端層 toohello 本機裝置層，這可能會很費時的程序。</span><span class="sxs-lookup"><span data-stu-id="46c60-575">hello index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="46c60-576">NetBackup 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="46c60-576">NetBackup server failure</span></span> | <span data-ttu-id="46c60-577">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="46c60-577">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="46c60-578">重建 hello 備份伺服器，並執行資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="46c60-578">Rebuild hello backup server and perform database restore.</span></span> | <span data-ttu-id="46c60-579">您必須重建或還原 hello NetBackup hello 災害復原站台伺服器。</span><span class="sxs-lookup"><span data-stu-id="46c60-579">You must rebuild or restore hello NetBackup server at hello disaster recovery site.</span></span> <span data-ttu-id="46c60-580">還原 hello 資料庫 toohello 最新的點。</span><span class="sxs-lookup"><span data-stu-id="46c60-580">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="46c60-581">Hello NetBackup 還原的資料庫不是最新的備份工作同步，索引和分類需要。</span><span class="sxs-lookup"><span data-stu-id="46c60-581">If hello restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="46c60-582">此索引和重新掃描程序的目錄，可能會導致所有備份組 toobe 掃描，並從 hello 雲端層 toohello 本機裝置層提取。</span><span class="sxs-lookup"><span data-stu-id="46c60-582">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="46c60-583">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="46c60-583">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="46c60-584">站台失敗所產生的 hello 備份伺服器和 StorSimple hello 遺失。</span><span class="sxs-lookup"><span data-stu-id="46c60-584">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="46c60-585">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="46c60-585">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="46c60-586">先還原 StorSimple，然後再還原 NetBackup。</span><span class="sxs-lookup"><span data-stu-id="46c60-586">Restore StorSimple first, and then restore NetBackup.</span></span> | <span data-ttu-id="46c60-587">先還原 StorSimple，然後再還原 NetBackup。</span><span class="sxs-lookup"><span data-stu-id="46c60-587">Restore StorSimple first, and then restore NetBackup.</span></span> <span data-ttu-id="46c60-588">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取 hello 完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="46c60-588">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="46c60-589">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="46c60-589">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="46c60-590">參考</span><span class="sxs-lookup"><span data-stu-id="46c60-590">References</span></span>

<span data-ttu-id="46c60-591">下列文件的 hello 時參考這個發行項：</span><span class="sxs-lookup"><span data-stu-id="46c60-591">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="46c60-592">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="46c60-592">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="46c60-593">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="46c60-593">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="46c60-594">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="46c60-594">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="46c60-595">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="46c60-595">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="46c60-596">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46c60-596">Next steps</span></span>

- <span data-ttu-id="46c60-597">深入了解如何太[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-597">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="46c60-598">深入了解如何 tooperform[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="46c60-598">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
