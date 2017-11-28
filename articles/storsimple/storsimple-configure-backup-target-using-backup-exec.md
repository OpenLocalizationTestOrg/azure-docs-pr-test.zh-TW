---
title: "做為備份目標與備份 Exec aaaStorSimple 8000 系列 |Microsoft 文件"
description: "描述搭配 Veritas 備份 Exec hello StorSimple 備份目標組態。"
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
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a><span data-ttu-id="a57a2-103">使用 StorSimple 做為 Backup Exec 的備份目標</span><span class="sxs-lookup"><span data-stu-id="a57a2-103">StorSimple as a backup target with Backup Exec</span></span>

## <a name="overview"></a><span data-ttu-id="a57a2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a57a2-104">Overview</span></span>

<span data-ttu-id="a57a2-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="a57a2-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="a57a2-106">StorSimple 位址為指數的資料成長的 hello 複雜性為 hello 在內部部署方案，以及自動分層資料的延伸的 Azure 儲存體帳戶使用跨內部部署儲存體和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-106">StorSimple addresses hello complexities of exponential data growth by using an Azure storage account as an extension of hello on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="a57a2-107">在本文中，我們會討論 StorSimple 與 Veritas Backup Exec 的整合，以及整合這兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="a57a2-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span></span> <span data-ttu-id="a57a2-108">我們也會進行有關如何設定備份 Exec toobest tooset 整合與 StorSimple 的建議事項。</span><span class="sxs-lookup"><span data-stu-id="a57a2-108">We also make recommendations on how tooset up Backup Exec toobest integrate with StorSimple.</span></span> <span data-ttu-id="a57a2-109">我們延遲 tooVeritas 最佳作法、 備份架構設計人員和系統管理員的 hello 最佳方式 tooset 備份 Exec toomeet 個別的備份需求以及服務等級協定 (Sla)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-109">We defer tooVeritas best practices, backup architects, and administrators for hello best way tooset up Backup Exec toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="a57a2-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="a57a2-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="a57a2-111">我們假設 hello 基本元件和基礎結構是在工作順序和準備 toosupport hello 概念，我們將描述。</span><span class="sxs-lookup"><span data-stu-id="a57a2-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="a57a2-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="a57a2-112">Who should read this?</span></span>

<span data-ttu-id="a57a2-113">本文章中的 hello 資訊將會最有幫助 toobackup 系統管理員、 存放裝置系統管理員，以及儲存體架構設計人員了解儲存體、 Windows Server 2012 R2、 乙太網路、 雲端服務和備份 Exec。</span><span class="sxs-lookup"><span data-stu-id="a57a2-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="a57a2-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="a57a2-114">Supported versions</span></span>

-   [<span data-ttu-id="a57a2-115">備份 Exec 16 及更新版本</span><span class="sxs-lookup"><span data-stu-id="a57a2-115">Backup Exec 16 and later versions</span></span>](http://backupexec.com/compatibility)
-   [<span data-ttu-id="a57a2-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="a57a2-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="a57a2-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="a57a2-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="a57a2-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="a57a2-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="a57a2-119">它提供標準的本機儲存體備份應用程式 toouse 做為快速備份的目的地，不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="a57a2-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="a57a2-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="a57a2-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="a57a2-121">其雲端層與 Azure 雲端儲存體帳戶 toouse 順暢地整合符合成本效益的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="a57a2-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="a57a2-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="a57a2-123">Key concepts</span></span>

<span data-ttu-id="a57a2-124">如同任何儲存體解決方案，hello 方案的儲存體效能 Sla，仔細評估變更與容量成長需求的速率是重大 toosuccess。</span><span class="sxs-lookup"><span data-stu-id="a57a2-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="a57a2-125">hello 主要概念是，藉由引進雲端層，您的存取時間和輸送量 toohello 雲端扮演了基本角色 StorSimple toodo hello 能力其工作。</span><span class="sxs-lookup"><span data-stu-id="a57a2-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="a57a2-126">StorSimple 是設計的 tooprovide 儲存體 tooapplications 妥善定義的工作集的資料 （熱資料） 上運作。</span><span class="sxs-lookup"><span data-stu-id="a57a2-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="a57a2-127">在此模型中，hello 工作集的資料儲存在 hello 本機層，而且 hello 剩餘非/冷/封存的資料集是階層式的 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="a57a2-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="a57a2-128">此模型會以 hello 遵循圖表示。</span><span class="sxs-lookup"><span data-stu-id="a57a2-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="a57a2-129">hello 幾乎單層綠色線條代表 hello hello 的 hello StorSimple 裝置的本機層上儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="a57a2-130">hello 紅線表示 hello 總儲存在 hello StorSimple 解決方案，跨所有階層的資料量。</span><span class="sxs-lookup"><span data-stu-id="a57a2-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="a57a2-131">hello 間距 hello 單層綠色線條和 hello 指數的紅色曲線表示 hello 的 hello 雲端中儲存的資料量總計。</span><span class="sxs-lookup"><span data-stu-id="a57a2-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="a57a2-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="a57a2-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span></span>

<span data-ttu-id="a57a2-133">請注意這種架構，與您會發現 StorSimple 是適合的 toooperate 做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="a57a2-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="a57a2-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="a57a2-135">執行您最常出現的還原從 hello 本機工作集的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="a57a2-136">使用 hello 雲端異地災害復原和較舊的資料，其中還原就都是較不頻繁。</span><span class="sxs-lookup"><span data-stu-id="a57a2-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="a57a2-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="a57a2-137">StorSimple benefits</span></span>

<span data-ttu-id="a57a2-138">StorSimple 提供順暢地整合 Microsoft Azure 與內部部署解決方案，藉由運用無縫存取 tooon 內部部署和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="a57a2-139">StorSimple 會使用自動 hello 在內部部署裝置，具有固態裝置 (SSD) 和序列連結 SCSI (SAS) 存放裝置，與 Azure 儲存體階層處理。</span><span class="sxs-lookup"><span data-stu-id="a57a2-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="a57a2-140">自動分層維持經常存取的本機 hello SSD 和 SAS 層上的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="a57a2-141">它會移動不常存取的資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="a57a2-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="a57a2-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="a57a2-143">使用 hello 雲端 tooachieve 前所未有的重複資料刪除層級的唯一重複資料刪除和壓縮演算法</span><span class="sxs-lookup"><span data-stu-id="a57a2-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="a57a2-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="a57a2-144">High availability</span></span>
-   <span data-ttu-id="a57a2-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="a57a2-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="a57a2-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="a57a2-146">Azure integration</span></span>
-   <span data-ttu-id="a57a2-147">Hello 雲端中的資料加密</span><span class="sxs-lookup"><span data-stu-id="a57a2-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="a57a2-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="a57a2-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="a57a2-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a57a2-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="a57a2-150">壓縮和重複資料刪除，所有有 hello StorSimple 沒有。</span><span class="sxs-lookup"><span data-stu-id="a57a2-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="a57a2-151">順暢地傳送，並擷取 hello 雲端與 hello 應用程式和檔案系統之間的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="a57a2-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="a57a2-153">此外，您可以檢閱 hello[技術 StorSimple 8000 系列規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a57a2-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="a57a2-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="a57a2-155">Architecture overview</span></span>

<span data-ttu-id="a57a2-156">hello 下列表格顯示 hello 裝置模型-架構初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="a57a2-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="a57a2-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="a57a2-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="a57a2-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-158">Storage capacity</span></span>       | <span data-ttu-id="a57a2-159">8100</span><span class="sxs-lookup"><span data-stu-id="a57a2-159">8100</span></span>          | <span data-ttu-id="a57a2-160">8600</span><span class="sxs-lookup"><span data-stu-id="a57a2-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="a57a2-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-161">Local storage capacity</span></span> | <span data-ttu-id="a57a2-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="a57a2-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="a57a2-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="a57a2-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="a57a2-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-164">Cloud storage capacity</span></span> | <span data-ttu-id="a57a2-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="a57a2-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="a57a2-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="a57a2-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="a57a2-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="a57a2-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="a57a2-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="a57a2-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="a57a2-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="a57a2-169">Backup scenario</span></span>  | <span data-ttu-id="a57a2-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-170">Local storage capacity</span></span>  | <span data-ttu-id="a57a2-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="a57a2-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="a57a2-172">Primary backup</span></span>  | <span data-ttu-id="a57a2-173">最新的備份儲存在本機儲存體的快速復原 toomeet 復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="a57a2-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="a57a2-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="a57a2-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="a57a2-175">Secondary backup</span></span> | <span data-ttu-id="a57a2-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="a57a2-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="a57a2-177">N/A</span><span class="sxs-lookup"><span data-stu-id="a57a2-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="a57a2-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="a57a2-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="a57a2-179">在此案例中，StorSimple 磁碟區會呈現為 hello 備份的唯一儲存機制的 toohello 備份應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57a2-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="a57a2-180">下列圖 hello 顯示中的所有備份使用 StorSimple 都分層磁碟區的備份和還原的方案架構。</span><span class="sxs-lookup"><span data-stu-id="a57a2-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="a57a2-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="a57a2-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="a57a2-183">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="a57a2-184">hello 備份伺服器將資料寫入 toohello StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="a57a2-185">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="a57a2-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="a57a2-186">快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。</span><span class="sxs-lookup"><span data-stu-id="a57a2-186">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="a57a2-187">hello 備份伺服器會刪除過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="a57a2-187">hello backup server deletes expired backups based on a retention policy.</span></span>


### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="a57a2-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="a57a2-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="a57a2-189">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="a57a2-190">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="a57a2-191">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="a57a2-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="a57a2-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="a57a2-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="a57a2-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="a57a2-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="a57a2-194">hello 下圖顯示的架構中的初始備份及還原高效能的目標磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="a57a2-195">這些備份複製並封存的 tooa StorSimple 分層磁碟區上設定的排程。</span><span class="sxs-lookup"><span data-stu-id="a57a2-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="a57a2-196">它是重要的 toosize 高效能磁碟區，好讓它可以處理保留原則容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-196">It is important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="a57a2-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="a57a2-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="a57a2-199">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="a57a2-200">hello 備份伺服器寫入資料 toohigh 能儲存體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="a57a2-201">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="a57a2-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="a57a2-202">hello 備份伺服器複製備份 tooStorSimple 根據保留原則。</span><span class="sxs-lookup"><span data-stu-id="a57a2-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="a57a2-203">快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。</span><span class="sxs-lookup"><span data-stu-id="a57a2-203">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="a57a2-204">hello 備份伺服器會刪除過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="a57a2-204">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="a57a2-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="a57a2-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="a57a2-206">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="a57a2-207">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="a57a2-208">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="a57a2-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="a57a2-209">部署 hello 方案</span><span class="sxs-lookup"><span data-stu-id="a57a2-209">Deploy hello solution</span></span>

<span data-ttu-id="a57a2-210">部署 hello 方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="a57a2-210">Deploying hello solution requires three steps:</span></span>
1. <span data-ttu-id="a57a2-211">準備 hello 網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a57a2-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="a57a2-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="a57a2-213">部署 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="a57a2-213">Deploy Backup Exec.</span></span>

<span data-ttu-id="a57a2-214">每個步驟是在 hello 下列各節中詳細討論。</span><span class="sxs-lookup"><span data-stu-id="a57a2-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="a57a2-215">設定 hello 網路</span><span class="sxs-lookup"><span data-stu-id="a57a2-215">Set up hello network</span></span>

<span data-ttu-id="a57a2-216">StorSimple 是與 hello Azure 雲端整合解決方案，因為 StorSimple 會需要使用中且正在運作的連線 toohello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="a57a2-216">Because StorSimple is a solution that's integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="a57a2-217">作業，像是雲端快照、 管理和中繼資料傳輸和 tootier 較舊且較少存取的資料 tooAzure 雲端存放裝置，則使用此連接。</span><span class="sxs-lookup"><span data-stu-id="a57a2-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="a57a2-218">Hello 方案 tooperform 最佳情況是，我們建議您遵循這些網路的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="a57a2-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="a57a2-219">連接您的 StorSimple 分層 tooAzure hello 連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-219">hello link that connects your StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="a57a2-220">tooachieve，套用 hello 必要服務品質 (QoS) 層級 tooyour 基礎結構交換器 toomatch 您 RPO 和復原時間目標 (RTO) Sla。</span><span class="sxs-lookup"><span data-stu-id="a57a2-220">tooachieve this, apply hello necessary Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="a57a2-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="a57a2-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="a57a2-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="a57a2-222">Deploy StorSimple</span></span>

<span data-ttu-id="a57a2-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-backup-exec"></a><span data-ttu-id="a57a2-224">部署 Backup Exec</span><span class="sxs-lookup"><span data-stu-id="a57a2-224">Deploy Backup Exec</span></span>

<span data-ttu-id="a57a2-225">如需 Backup Exec 安裝最佳作法，請參閱 [Backup Exec 安裝的最佳作法](https://www.veritas.com/support/en_US/article.000068207)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="a57a2-226">設定 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="a57a2-226">Set up hello solution</span></span>

<span data-ttu-id="a57a2-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="a57a2-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="a57a2-228">hello 下列的範例和建議事項說明 hello 最基本也最基本的實作。</span><span class="sxs-lookup"><span data-stu-id="a57a2-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="a57a2-229">此實作中可能不適用，直接 tooyour 特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="a57a2-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="a57a2-230">Set up StorSimple</span></span>

| <span data-ttu-id="a57a2-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="a57a2-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="a57a2-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="a57a2-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="a57a2-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="a57a2-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="a57a2-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="a57a2-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="a57a2-235">開啟 hello 備份目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-235">Turn on hello backup target.</span></span> | <span data-ttu-id="a57a2-236">使用這些命令 tooturn 上或備份的目標模式和 tooget 狀態為關閉。</span><span class="sxs-lookup"><span data-stu-id="a57a2-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="a57a2-237">如需詳細資訊，請參閱[遠端連線 tooa StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="a57a2-238">備份模式 tooturn: `Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="a57a2-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="a57a2-239">備份模式關閉 tooturn: `Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="a57a2-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="a57a2-240">tooget hello 目前狀態的備份模式設定： `Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="a57a2-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="a57a2-241">建立您將 hello 備份資料儲存的磁碟區的一般磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="a57a2-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="a57a2-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="a57a2-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="a57a2-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="a57a2-245">建立磁碟區大小為預期的關閉 toohello 使用量越好，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="a57a2-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="a57a2-246">如需有關資訊 toosize 磁碟區，閱讀有關[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="a57a2-247">使用 StorSimple 分層磁碟區，並選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a57a2-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="a57a2-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="a57a2-249">建立所有 hello 備份目標磁碟區的唯一 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="a57a2-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="a57a2-250">StorSimple 的備份原則定義 hello 磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="a57a2-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="a57a2-251">停用 hello 排程，因為到期 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="a57a2-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="a57a2-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="a57a2-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="a57a2-253">設定 hello 主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="a57a2-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="a57a2-254">設定 hello 主機備份伺服器儲存體，根據 toothese 指導方針：</span><span class="sxs-lookup"><span data-stu-id="a57a2-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="a57a2-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="a57a2-256">不支援合併磁碟。</span><span class="sxs-lookup"><span data-stu-id="a57a2-256">Spanned disks are not supported.</span></span>
- <span data-ttu-id="a57a2-257">使用 64 KB 配置大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-257">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="a57a2-258">對應 hello StorSimple 磁碟區直接 toohello Exec 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-258">Map hello StorSimple volumes directly toohello Backup Exec server.</span></span>
    - <span data-ttu-id="a57a2-259">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="a57a2-259">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="a57a2-260">虛擬伺服器請使用傳遞磁碟。</span><span class="sxs-lookup"><span data-stu-id="a57a2-260">Use pass-through disks for virtual servers.</span></span>

## <a name="best-practices-for-storsimple-and-backup-exec"></a><span data-ttu-id="a57a2-261">StorSimple 和 Backup Exec 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="a57a2-261">Best practices for StorSimple and Backup Exec</span></span>

<span data-ttu-id="a57a2-262">設定您的解決方案，根據下列各節的 hello toohello 指導方針。</span><span class="sxs-lookup"><span data-stu-id="a57a2-262">Set up your solution according toohello guidelines in hello following sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="a57a2-263">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="a57a2-263">Operating system best practices</span></span>

-   <span data-ttu-id="a57a2-264">停用 Windows Server 的加密和 hello NTFS 檔案系統的重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="a57a2-264">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="a57a2-265">停用 hello StorSimple 磁碟區上的 Windows 伺服器磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="a57a2-265">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="a57a2-266">停用 Windows hello 索引 StorSimple 磁碟區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-266">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="a57a2-267">在 hello （不是針對 hello StorSimple 磁碟區） 的來源主機上執行的防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="a57a2-267">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="a57a2-268">關閉 hello 預設[Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)工作管理員 中。</span><span class="sxs-lookup"><span data-stu-id="a57a2-268">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="a57a2-269">執行下列其中一 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="a57a2-269">Do this in one of hello following ways:</span></span>
   - <span data-ttu-id="a57a2-270">關閉 Windows 工作排程器中的 hello 維護 configurator。</span><span class="sxs-lookup"><span data-stu-id="a57a2-270">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
   - <span data-ttu-id="a57a2-271">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="a57a2-272">下載 PsExec 之後，請以系統管理員身分執行 Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="a57a2-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="a57a2-273">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="a57a2-273">StorSimple best practices</span></span>

  -   <span data-ttu-id="a57a2-274">請務必更新該 hello StorSimple 裝置時太[Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-274">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
  -   <span data-ttu-id="a57a2-275">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="a57a2-275">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="a57a2-276">您可以使用專用的 iSCSI 連線的 StorSimple 與 hello 備份的伺服器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="a57a2-276">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
  -   <span data-ttu-id="a57a2-277">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-277">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="a57a2-278">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="a57a2-278">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="backup-exec-best-practices"></a><span data-ttu-id="a57a2-279">Backup Exec 最佳作法</span><span class="sxs-lookup"><span data-stu-id="a57a2-279">Backup Exec best practices</span></span>

-   <span data-ttu-id="a57a2-280">Hello 伺服器的本機磁碟機上，而不是在 StorSimple 磁碟區，則必須安裝備份執行。</span><span class="sxs-lookup"><span data-stu-id="a57a2-280">Backup Exec must be installed on a local drive of hello server, and not on a StorSimple volume.</span></span>
-   <span data-ttu-id="a57a2-281">設定 hello 備份 Exec 儲存**並行寫入作業**toohello 最大允許。</span><span class="sxs-lookup"><span data-stu-id="a57a2-281">Set hello Backup Exec storage **concurrent write operations** toohello maximum allowed.</span></span>
    -   <span data-ttu-id="a57a2-282">設定 hello 備份 Exec 儲存**區塊和緩衝區大小**too512 KB。</span><span class="sxs-lookup"><span data-stu-id="a57a2-282">Set hello Backup Exec storage **block and buffer size** too512 KB.</span></span>
    -   <span data-ttu-id="a57a2-283">開啟 Backup Exec 儲存體的**緩衝讀取和寫入**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-283">Turn on Backup Exec storage **buffered read and write**.</span></span>
-   <span data-ttu-id="a57a2-284">StorSimple 支援 Backup Exec 完整和增量備份。</span><span class="sxs-lookup"><span data-stu-id="a57a2-284">StorSimple supports Backup Exec full and incremental backups.</span></span> <span data-ttu-id="a57a2-285">建議您不要使用綜合和差異備份。</span><span class="sxs-lookup"><span data-stu-id="a57a2-285">We recommend that you not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="a57a2-286">備份資料檔案最好只包含特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-286">Backup data files should contain data only for a specific job.</span></span> <span data-ttu-id="a57a2-287">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="a57a2-287">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="a57a2-288">停用作業驗證。</span><span class="sxs-lookup"><span data-stu-id="a57a2-288">Disable job verification.</span></span> <span data-ttu-id="a57a2-289">如有必要，都應該排程驗證 hello 最新的備份作業之後。</span><span class="sxs-lookup"><span data-stu-id="a57a2-289">If necessary, verification should be scheduled after hello latest backup job.</span></span> <span data-ttu-id="a57a2-290">這項作業會影響您的備份時間範圍的重要 toounderstand 它。</span><span class="sxs-lookup"><span data-stu-id="a57a2-290">It is important toounderstand that this job affects your backup window.</span></span>
-   <span data-ttu-id="a57a2-291">選取 [儲存體] > 您的磁碟 > [詳細資料] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="a57a2-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span></span> <span data-ttu-id="a57a2-292">關閉 [預先配置磁碟空間]。</span><span class="sxs-lookup"><span data-stu-id="a57a2-292">Turn off **Pre-allocate disk space**.</span></span>

<span data-ttu-id="a57a2-293">Hello 最新的備份 Exec 設定及實作這些需求的最佳作法，請參閱[hello Veritas 網站](https://www.veritas.com)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-293">For hello latest Backup Exec settings and best practices for implementing these requirements, see [hello Veritas website](https://www.veritas.com).</span></span>

## <a name="retention-policies"></a><span data-ttu-id="a57a2-294">保留原則</span><span class="sxs-lookup"><span data-stu-id="a57a2-294">Retention policies</span></span>

<span data-ttu-id="a57a2-295">Hello 最常見的備份保留原則類型的其中一個是祖父、 父親和 Son (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="a57a2-295">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="a57a2-296">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="a57a2-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="a57a2-297">此原則會產生六個 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-297">This policy results in six StorSimple tiered volumes.</span></span> <span data-ttu-id="a57a2-298">一個磁碟區包含 hello 每週、 每月和每年完整備份。</span><span class="sxs-lookup"><span data-stu-id="a57a2-298">One volume contains hello weekly, monthly, and yearly full backups.</span></span> <span data-ttu-id="a57a2-299">hello 其他五個磁碟區儲存每日增量備份。</span><span class="sxs-lookup"><span data-stu-id="a57a2-299">hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="a57a2-300">在下列範例的 hello，我們會使用 GFS 旋轉。</span><span class="sxs-lookup"><span data-stu-id="a57a2-300">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="a57a2-301">hello 範例假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a57a2-301">hello example assumes hello following:</span></span>

-   <span data-ttu-id="a57a2-302">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-302">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="a57a2-303">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="a57a2-303">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="a57a2-304">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="a57a2-304">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="a57a2-305">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="a57a2-305">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="a57a2-306">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="a57a2-306">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="a57a2-307">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="a57a2-307">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="a57a2-308">根據上述假設 hello，建立 26 TiB StorSimple 分層 hello 每月和每年完整備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-308">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="a57a2-309">建立 5 TiB StorSimple hello 的每日增量備份的每個分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-309">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="a57a2-310">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="a57a2-310">Backup type retention</span></span> | <span data-ttu-id="a57a2-311">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="a57a2-311">Size (TiB)</span></span> | <span data-ttu-id="a57a2-312">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="a57a2-312">GFS multiplier\*</span></span> | <span data-ttu-id="a57a2-313">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="a57a2-313">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="a57a2-314">每週完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-314">Weekly full</span></span> | <span data-ttu-id="a57a2-315">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-315">1</span></span> | <span data-ttu-id="a57a2-316">4</span><span class="sxs-lookup"><span data-stu-id="a57a2-316">4</span></span>  | <span data-ttu-id="a57a2-317">4</span><span class="sxs-lookup"><span data-stu-id="a57a2-317">4</span></span> |
| <span data-ttu-id="a57a2-318">每日增量</span><span class="sxs-lookup"><span data-stu-id="a57a2-318">Daily incremental</span></span> | <span data-ttu-id="a57a2-319">0.5</span><span class="sxs-lookup"><span data-stu-id="a57a2-319">0.5</span></span> | <span data-ttu-id="a57a2-320">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="a57a2-320">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="a57a2-321">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="a57a2-321">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="a57a2-322">每月完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-322">Monthly full</span></span> | <span data-ttu-id="a57a2-323">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-323">1</span></span> | <span data-ttu-id="a57a2-324">12</span><span class="sxs-lookup"><span data-stu-id="a57a2-324">12</span></span> | <span data-ttu-id="a57a2-325">12</span><span class="sxs-lookup"><span data-stu-id="a57a2-325">12</span></span> |
| <span data-ttu-id="a57a2-326">每年完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-326">Yearly full</span></span> | <span data-ttu-id="a57a2-327">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-327">1</span></span>  | <span data-ttu-id="a57a2-328">10</span><span class="sxs-lookup"><span data-stu-id="a57a2-328">10</span></span> | <span data-ttu-id="a57a2-329">10</span><span class="sxs-lookup"><span data-stu-id="a57a2-329">10</span></span> |
| <span data-ttu-id="a57a2-330">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="a57a2-330">GFS requirement</span></span> |   | <span data-ttu-id="a57a2-331">38</span><span class="sxs-lookup"><span data-stu-id="a57a2-331">38</span></span> |   |
| <span data-ttu-id="a57a2-332">其他配額</span><span class="sxs-lookup"><span data-stu-id="a57a2-332">Additional quota</span></span>  | <span data-ttu-id="a57a2-333">4</span><span class="sxs-lookup"><span data-stu-id="a57a2-333">4</span></span>  |   | <span data-ttu-id="a57a2-334">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="a57a2-334">42 total GFS requirement</span></span>  |
<span data-ttu-id="a57a2-335">\*hello GFS 乘數是 hello 的數字的複本需要 tooprotect 和保留 toomeet 您備份原則的需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-335">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-backup-exec-storage"></a><span data-ttu-id="a57a2-336">設定 Backup Exec 儲存體</span><span class="sxs-lookup"><span data-stu-id="a57a2-336">Set up Backup Exec storage</span></span>

### <a name="tooset-up-backup-exec-storage"></a><span data-ttu-id="a57a2-337">tooset 備份 Exec 存放裝置</span><span class="sxs-lookup"><span data-stu-id="a57a2-337">tooset up Backup Exec storage</span></span>

1.  <span data-ttu-id="a57a2-338">在 hello 備份 Exec 管理主控台中，選取 **儲存體** > **設定儲存體** > **磁碟型儲存裝置** >  **下一步**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-338">In hello Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span></span>

    ![Backup Exec 管理主控台，設定儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  <span data-ttu-id="a57a2-340">選取 [磁碟儲存體]，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a57a2-340">Select **Disk Storage**, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，選取儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  <span data-ttu-id="a57a2-342">輸入一個代表性名稱，例如，「星期六完整」和描述。</span><span class="sxs-lookup"><span data-stu-id="a57a2-342">Enter a representative name, for example, **Saturday Full**, and a description.</span></span> <span data-ttu-id="a57a2-343">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a57a2-343">Select **Next**.</span></span>

    ![Backup Exec 管理主控台，名稱和描述頁面](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  <span data-ttu-id="a57a2-345">您想 toocreate hello 磁碟存放裝置，然後選取選取 hello 磁碟**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-345">Select hello disk where you want toocreate hello disk storage device, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，儲存體磁碟選取頁面](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  <span data-ttu-id="a57a2-347">遞增 hello 寫入作業數目太**16**，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-347">Increment hello number of write operations too**16**, and then select **Next**.</span></span>

    ![Backup Exec 管理主控台，並行寫入作業設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  <span data-ttu-id="a57a2-349">檢閱 hello 設定，然後選取**完成**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-349">Review hello settings, and then select **Finish**.</span></span>

    ![Backup Exec 管理主控台，儲存體組態摘要頁面](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  <span data-ttu-id="a57a2-351">在每個磁碟區指派 hello 最後，變更這些建議您在 hello 存放裝置設定 toomatch [StorSimple 和備份 Exec 最佳作法](#best-practices-for-storsimple-and-backup-exec)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-351">At hello end of each volume assignment, change hello storage device settings toomatch those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span></span>

    ![Backup Exec 管理主控台，存放裝置設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  <span data-ttu-id="a57a2-353">重複步驟 1 到 7，直到完成指派您的 StorSimple 磁碟區 tooBackup Exec。</span><span class="sxs-lookup"><span data-stu-id="a57a2-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes tooBackup Exec.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="a57a2-354">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="a57a2-354">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="a57a2-355">從已分層式的 toohello 雲端備份資料還原就會發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="a57a2-355">Data restore from a backup that has been tiered toohello cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="a57a2-356">hello 下圖顯示典型的磁碟區 tooa 備份工作的 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="a57a2-356">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="a57a2-357">在此情況下，所有的 hello 每週備份對應 toohello 星期六磁碟已滿，而 hello 增量備份對應 tooMonday 星期五累加磁碟。</span><span class="sxs-lookup"><span data-stu-id="a57a2-357">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="a57a2-358">所有 hello 備份與還原就都是從 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-358">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![主要備份目標組態的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="a57a2-360">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="a57a2-360">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="a57a2-361">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="a57a2-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="a57a2-362">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="a57a2-362">Frequency/backup type</span></span> | <span data-ttu-id="a57a2-363">完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-363">Full</span></span> | <span data-ttu-id="a57a2-364">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-364">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="a57a2-365">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="a57a2-365">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="a57a2-366">星期六</span><span class="sxs-lookup"><span data-stu-id="a57a2-366">Saturday</span></span> | <span data-ttu-id="a57a2-367">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="a57a2-367">Monday-Friday</span></span> |
| <span data-ttu-id="a57a2-368">每月</span><span class="sxs-lookup"><span data-stu-id="a57a2-368">Monthly</span></span>  | <span data-ttu-id="a57a2-369">星期六</span><span class="sxs-lookup"><span data-stu-id="a57a2-369">Saturday</span></span>  |   |
| <span data-ttu-id="a57a2-370">每年</span><span class="sxs-lookup"><span data-stu-id="a57a2-370">Yearly</span></span> | <span data-ttu-id="a57a2-371">星期六</span><span class="sxs-lookup"><span data-stu-id="a57a2-371">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a><span data-ttu-id="a57a2-372">指派 StorSimple 磁碟區 tooa 備份執行備份工作</span><span class="sxs-lookup"><span data-stu-id="a57a2-372">Assign StorSimple volumes tooa Backup Exec backup job</span></span>

<span data-ttu-id="a57a2-373">hello 下列程序會假設該備份 Exec 和 hello 的目標主機設定依據 hello 備份 Exec 代理程式的指導方針。</span><span class="sxs-lookup"><span data-stu-id="a57a2-373">hello following sequence assumes that Backup Exec and hello target host are configured in accordance with hello Backup Exec agent guidelines.</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a><span data-ttu-id="a57a2-374">tooassign StorSimple 磁碟區 tooa 備份執行備份作業</span><span class="sxs-lookup"><span data-stu-id="a57a2-374">tooassign StorSimple volumes tooa Backup Exec backup job</span></span>

1.  <span data-ttu-id="a57a2-375">在 hello 備份 Exec 管理主控台中，選取 **主機** > **備份** > **備份 tooDisk**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-375">In hello Backup Exec management console, select **Host** > **Backup** > **Backup tooDisk**.</span></span>

    ![備份 Exec 管理主控台中，選取主機上，備份，和備份 toodisk](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  <span data-ttu-id="a57a2-377">在 hello**備份定義屬性**對話方塊的 **備份**，選取**編輯**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-377">In hello **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  <span data-ttu-id="a57a2-379">設定完整和增量備份，以便符合您的 RPO 和 RTO 需求並符合 tooVeritas 最佳作法。</span><span class="sxs-lookup"><span data-stu-id="a57a2-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform tooVeritas best practices.</span></span>

4.  <span data-ttu-id="a57a2-380">在 hello**備份選項**對話方塊中，選取**儲存體**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-380">In hello **Backup Options** dialog box, select **Storage**.</span></span>

    ![Backup Exec 管理主控台，備份選項、儲存體對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  <span data-ttu-id="a57a2-382">指派對應 StorSimple 磁碟區 tooyour 備份排程。</span><span class="sxs-lookup"><span data-stu-id="a57a2-382">Assign corresponding StorSimple volumes tooyour backup schedule.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a57a2-383">**壓縮**和**加密類型**設定得**無**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-383">**Compression** and **Encryption type** are set too**None**.</span></span>

6.  <span data-ttu-id="a57a2-384">在下**確認**，選取 hello**不會驗證此作業的資料**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a57a2-384">Under **Verify**, select hello **Do not verify data for this job** check box.</span></span> <span data-ttu-id="a57a2-385">使用此選項可能會影響 StorSimple 分層。</span><span class="sxs-lookup"><span data-stu-id="a57a2-385">Using this option might affect StorSimple tiering.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a57a2-386">磁碟重組、 索引和背景驗證造成負面影響 hello StorSimple 階層處理。</span><span class="sxs-lookup"><span data-stu-id="a57a2-386">Defragmentation, indexing, and background verification negatively affect hello StorSimple tiering.</span></span>

    ![Backup Exec 管理主控台，備份選項、驗證設定](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  <span data-ttu-id="a57a2-388">當您設定的備份選項 toomeet hello rest 您的需求時，選取**確定**toofinish。</span><span class="sxs-lookup"><span data-stu-id="a57a2-388">When you've set up hello rest of your backup options toomeet your requirements, select **OK** toofinish.</span></span>

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="a57a2-389">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="a57a2-389">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="a57a2-390">從已分層式的 toohello 雲端備份資料還原發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="a57a2-390">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="a57a2-391">在此模型中，您必須擁有儲存媒體 （非 StorSimple) tooserve 暫時快取。</span><span class="sxs-lookup"><span data-stu-id="a57a2-391">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="a57a2-392">例如，您可以使用獨立磁碟 (RAID) 磁碟區 tooaccommodate 空間、 輸入/輸出 (I/O) 和頻寬的備援陣列。</span><span class="sxs-lookup"><span data-stu-id="a57a2-392">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="a57a2-393">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="a57a2-393">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="a57a2-394">hello 下圖顯示典型短期保留本機 （toohello 伺服器） 的磁碟區和長期的保留封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-394">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="a57a2-395">在此案例中，所有備份上都執行本機 hello （toohello 伺服器） RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-395">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="a57a2-396">定期重複這些備份和封存的 tooan 封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-396">These backups are periodically duplicated and archived tooan archives volume.</span></span> <span data-ttu-id="a57a2-397">它是本機 （toohello 伺服器） 的重要 toosize RAID 磁碟區，好讓它可以處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-397">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="a57a2-398">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="a57a2-398">StorSimple as a secondary backup target GFS example</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

<span data-ttu-id="a57a2-400">hello 下表顯示如何 tooset 向上備份 toorun hello 本機和 StorSimple 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="a57a2-400">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="a57a2-401">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="a57a2-401">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="a57a2-402">備份設定和容量需求</span><span class="sxs-lookup"><span data-stu-id="a57a2-402">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="a57a2-403">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="a57a2-403">Backup type and retention</span></span> | <span data-ttu-id="a57a2-404">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="a57a2-404">Configured storage</span></span> | <span data-ttu-id="a57a2-405">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="a57a2-405">Size (TiB)</span></span> | <span data-ttu-id="a57a2-406">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="a57a2-406">GFS multiplier</span></span> | <span data-ttu-id="a57a2-407">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="a57a2-407">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="a57a2-408">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="a57a2-408">Week 1 (full and incremental)</span></span> |<span data-ttu-id="a57a2-409">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="a57a2-409">Local disk (short-term)</span></span>| <span data-ttu-id="a57a2-410">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-410">1</span></span> | <span data-ttu-id="a57a2-411">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-411">1</span></span> | <span data-ttu-id="a57a2-412">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-412">1</span></span> |
| <span data-ttu-id="a57a2-413">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-413">StorSimple weeks 2-4</span></span> |<span data-ttu-id="a57a2-414">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="a57a2-414">StorSimple disk (long-term)</span></span> | <span data-ttu-id="a57a2-415">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-415">1</span></span> | <span data-ttu-id="a57a2-416">4</span><span class="sxs-lookup"><span data-stu-id="a57a2-416">4</span></span> | <span data-ttu-id="a57a2-417">4</span><span class="sxs-lookup"><span data-stu-id="a57a2-417">4</span></span> |
| <span data-ttu-id="a57a2-418">每月完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-418">Monthly full</span></span> |<span data-ttu-id="a57a2-419">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="a57a2-419">StorSimple disk (long-term)</span></span> | <span data-ttu-id="a57a2-420">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-420">1</span></span> | <span data-ttu-id="a57a2-421">12</span><span class="sxs-lookup"><span data-stu-id="a57a2-421">12</span></span> | <span data-ttu-id="a57a2-422">12</span><span class="sxs-lookup"><span data-stu-id="a57a2-422">12</span></span> |
| <span data-ttu-id="a57a2-423">每年完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-423">Yearly full</span></span> |<span data-ttu-id="a57a2-424">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="a57a2-424">StorSimple disk (long-term)</span></span> | <span data-ttu-id="a57a2-425">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-425">1</span></span> | <span data-ttu-id="a57a2-426">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-426">1</span></span> | <span data-ttu-id="a57a2-427">1</span><span class="sxs-lookup"><span data-stu-id="a57a2-427">1</span></span> |
|<span data-ttu-id="a57a2-428">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="a57a2-428">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="a57a2-429">18*</span><span class="sxs-lookup"><span data-stu-id="a57a2-429">18*</span></span>|
<span data-ttu-id="a57a2-430">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="a57a2-431">GFS 範例排程：每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="a57a2-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="a57a2-432">週</span><span class="sxs-lookup"><span data-stu-id="a57a2-432">Week</span></span> | <span data-ttu-id="a57a2-433">完整</span><span class="sxs-lookup"><span data-stu-id="a57a2-433">Full</span></span> | <span data-ttu-id="a57a2-434">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-434">Incremental day 1</span></span> | <span data-ttu-id="a57a2-435">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-435">Incremental day 2</span></span> | <span data-ttu-id="a57a2-436">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-436">Incremental day 3</span></span> | <span data-ttu-id="a57a2-437">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-437">Incremental day 4</span></span> | <span data-ttu-id="a57a2-438">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="a57a2-438">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="a57a2-439">第 1 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-439">Week 1</span></span> | <span data-ttu-id="a57a2-440">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-440">Local RAID volume</span></span>  | <span data-ttu-id="a57a2-441">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-441">Local RAID volume</span></span> | <span data-ttu-id="a57a2-442">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-442">Local RAID volume</span></span> | <span data-ttu-id="a57a2-443">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-443">Local RAID volume</span></span> | <span data-ttu-id="a57a2-444">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-444">Local RAID volume</span></span> | <span data-ttu-id="a57a2-445">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="a57a2-445">Local RAID volume</span></span> |
| <span data-ttu-id="a57a2-446">第 2 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-446">Week 2</span></span> | <span data-ttu-id="a57a2-447">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-447">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="a57a2-448">第 3 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-448">Week 3</span></span> | <span data-ttu-id="a57a2-449">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-449">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="a57a2-450">第 4 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-450">Week 4</span></span> | <span data-ttu-id="a57a2-451">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="a57a2-451">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="a57a2-452">每月</span><span class="sxs-lookup"><span data-stu-id="a57a2-452">Monthly</span></span> | <span data-ttu-id="a57a2-453">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="a57a2-453">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="a57a2-454">每年</span><span class="sxs-lookup"><span data-stu-id="a57a2-454">Yearly</span></span> | <span data-ttu-id="a57a2-455">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="a57a2-455">StorSimple yearly</span></span>  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a><span data-ttu-id="a57a2-456">指派 StorSimple 磁碟區 tooa 備份 Exec 封存及重複資料刪除工作</span><span class="sxs-lookup"><span data-stu-id="a57a2-456">Assign StorSimple volumes tooa Backup Exec archive and deduplication job</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a><span data-ttu-id="a57a2-457">tooassign StorSimple 磁碟區 tooa 備份 Exec 封存和複製作業</span><span class="sxs-lookup"><span data-stu-id="a57a2-457">tooassign StorSimple volumes tooa Backup Exec archive and duplication job</span></span>

1.  <span data-ttu-id="a57a2-458">在 hello 備份 Exec 管理主控台中，以滑鼠右鍵按一下您想 tooarchive tooa StorSimple 磁碟區，然後選取 hello 作業**備份定義屬性** > **編輯**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-458">In hello Backup Exec management console, right-click hello job that you want tooarchive tooa StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  <span data-ttu-id="a57a2-460">選取**新增階段** > **重複 tooDisk** > **編輯**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-460">Select **Add Stage** > **Duplicate tooDisk** > **Edit**.</span></span>

    ![Backup Exec 管理主控台，新增階段](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  <span data-ttu-id="a57a2-462">在 hello**重複選項**對話方塊中，您想要針對 toouse 選取 hello 值**來源**和**排程**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-462">In hello **Duplicate Options** dialog box, select hello values that you want toouse for **Source** and **Schedule**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  <span data-ttu-id="a57a2-464">在 hello**儲存體**下拉式清單中，選取 hello hello 封存作業 toostore hello 資料所在的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-464">In hello **Storage** drop-down list, select hello StorSimple volume where you want hello archive job toostore hello data.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  <span data-ttu-id="a57a2-466">選取**確認**，然後選取 hello**不會驗證此作業的資料**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a57a2-466">Select **Verify**, and then select hello **Do not verify data for this job** check box.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  <span data-ttu-id="a57a2-468">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a57a2-468">Select **OK**.</span></span>

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  <span data-ttu-id="a57a2-470">在 hello**備份**資料行，將新的階段。</span><span class="sxs-lookup"><span data-stu-id="a57a2-470">In hello **Backup** column, add a new stage.</span></span> <span data-ttu-id="a57a2-471">Hello 來源使用**累加**。</span><span class="sxs-lookup"><span data-stu-id="a57a2-471">For hello source, use **incremental**.</span></span> <span data-ttu-id="a57a2-472">Hello 目標，選擇 hello hello 增量備份工作會封存位置的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a57a2-472">For hello target, choose hello StorSimple volume where hello incremental backup job is archived.</span></span> <span data-ttu-id="a57a2-473">重複步驟 1 至 6。</span><span class="sxs-lookup"><span data-stu-id="a57a2-473">Repeat steps 1-6.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="a57a2-474">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="a57a2-474">StorSimple cloud snapshots</span></span>

<span data-ttu-id="a57a2-475">StorSimple 雲端快照集保護位於您的 StorSimple 裝置中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a57a2-475">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="a57a2-476">建立雲端快照集是對等 tooshipping 本機備份磁帶 tooan 異地設施。</span><span class="sxs-lookup"><span data-stu-id="a57a2-476">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="a57a2-477">如果您使用 Azure 地理備援儲存體，建立雲端快照是相等的 tooshipping 備份磁帶 toomultiple 站台。</span><span class="sxs-lookup"><span data-stu-id="a57a2-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="a57a2-478">如果您需要 toorestore 裝置在損毀之後，您可能會讓其他 StorSimple 裝置上線，並且進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a57a2-478">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="a57a2-479">Hello 容錯移轉之後，您將無法 tooaccess hello 資料 （速度雲端） 從 hello 最新的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="a57a2-479">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="a57a2-480">hello 下列章節描述如何 toocreate 簡短的指令碼 toostart 和 delete StorSimple 雲端快照在備份後的處理期間。</span><span class="sxs-lookup"><span data-stu-id="a57a2-480">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="a57a2-481">手動或以程式設計方式建立的快照集未遵循 hello StorSimple 快照集的到期原則。</span><span class="sxs-lookup"><span data-stu-id="a57a2-481">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="a57a2-482">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="a57a2-482">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="a57a2-483">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="a57a2-483">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="a57a2-484">請仔細在刪除 StorSimple 快照集之前，先評估 hello 相容性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="a57a2-484">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="a57a2-485">如需有關如何 toorun 備份後指令碼，請參閱 hello[備份 Exec 文件](https://www.veritas.com/support/en_US/15047.html)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-485">For more information about how toorun a post-backup script, see hello [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="a57a2-486">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="a57a2-486">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="a57a2-488">需求</span><span class="sxs-lookup"><span data-stu-id="a57a2-488">Requirements</span></span>

-   <span data-ttu-id="a57a2-489">執行 hello 指令碼的 hello 伺服器必須具備存取 tooAzure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="a57a2-489">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="a57a2-490">hello 使用者帳戶必須擁有 hello 必要的權限。</span><span class="sxs-lookup"><span data-stu-id="a57a2-490">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="a57a2-491">StorSimple hello 與備份原則相關聯的 StorSimple 磁碟區必須設定，但未開啟。</span><span class="sxs-lookup"><span data-stu-id="a57a2-491">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="a57a2-492">您將需要 hello StorSimple 資源名稱、 登錄機碼、 裝置名稱和備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a57a2-492">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="a57a2-493">toostart 或刪除的雲端快照</span><span class="sxs-lookup"><span data-stu-id="a57a2-493">toostart or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="a57a2-494">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-494">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="a57a2-495">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="a57a2-496">在 hello Azure 傳統入口網站中取得 hello 資源名稱和[StorSimple Manager 服務登錄機碼](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-496">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="a57a2-497">Hello 在伺服器上執行 hello 指令碼，請以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a57a2-497">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="a57a2-498">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="a57a2-498">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="a57a2-499">請注意 hello 備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a57a2-499">Note hello backup policy ID.</span></span>
5.  <span data-ttu-id="a57a2-500">在記事本中，請使用下列程式碼的 hello 以建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a57a2-500">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="a57a2-501">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="a57a2-501">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="a57a2-502">Hello PowerShell 指令碼 toohello 儲存相同的位置儲存您的 Azure 發行設定。</span><span class="sxs-lookup"><span data-stu-id="a57a2-502">Save hello PowerShell script toohello same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="a57a2-503">例如，儲存為 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1。</span><span class="sxs-lookup"><span data-stu-id="a57a2-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="a57a2-504">在備份 Exec 增加 hello 指令碼 tooyour 備份工作，請編輯您備份執行的工作選項的前置處理和後置處理指令。</span><span class="sxs-lookup"><span data-stu-id="a57a2-504">Add hello script tooyour backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span></span>

    ![Backup Exec 主控台，備份選項，前處理和後處理命令索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> <span data-ttu-id="a57a2-506">我們建議做為後置處理指令碼執行 StorSimple 雲端快照集備份原則，在您每日備份工作的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="a57a2-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="a57a2-507">如需有關如何向上 tooback 和還原您備份應用程式環境 toohelp 您符合您的 RPO 和 RTO，請參閱與您備份的架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="a57a2-507">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="a57a2-508">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="a57a2-508">StorSimple as a restore source</span></span>

<span data-ttu-id="a57a2-509">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="a57a2-509">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="a57a2-510">還原的是階層式的 toohello 雲端的資料就會發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="a57a2-510">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="a57a2-511">對於本機資料，還原發生 hello 裝置 hello 本機磁碟速度。</span><span class="sxs-lookup"><span data-stu-id="a57a2-511">For local data, restores occur at hello local disk speed of hello device.</span></span> <span data-ttu-id="a57a2-512">如需有關資訊 tooperform 還原，請參閱 hello 備份 Exec 文件。</span><span class="sxs-lookup"><span data-stu-id="a57a2-512">For information about how tooperform a restore, see hello Backup Exec documentation.</span></span> <span data-ttu-id="a57a2-513">我們建議您符合 tooBackup Exec 還原最佳作法。</span><span class="sxs-lookup"><span data-stu-id="a57a2-513">We recommend that you conform tooBackup Exec restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="a57a2-514">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="a57a2-514">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="a57a2-515">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="a57a2-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="a57a2-516">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="a57a2-516">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="a57a2-517">hello 下表列出常見的嚴重損壞修復案例。</span><span class="sxs-lookup"><span data-stu-id="a57a2-517">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="a57a2-518">案例</span><span class="sxs-lookup"><span data-stu-id="a57a2-518">Scenario</span></span> | <span data-ttu-id="a57a2-519">影響</span><span class="sxs-lookup"><span data-stu-id="a57a2-519">Impact</span></span> | <span data-ttu-id="a57a2-520">如何 toorecover</span><span class="sxs-lookup"><span data-stu-id="a57a2-520">How toorecover</span></span> | <span data-ttu-id="a57a2-521">注意事項</span><span class="sxs-lookup"><span data-stu-id="a57a2-521">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="a57a2-522">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="a57a2-522">StorSimple device failure</span></span> | <span data-ttu-id="a57a2-523">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="a57a2-523">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="a57a2-524">取代 hello 失敗的裝置，並執行[StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-524">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="a57a2-525">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="a57a2-525">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="a57a2-526">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="a57a2-526">All operations are at cloud speeds.</span></span> <span data-ttu-id="a57a2-527">hello 編製索引及編目重新掃描程序可能會導致所有備份組 toobe 掃描並取自 hello 雲端層 toohello 本機裝置層，這可能會很費時的程序。</span><span class="sxs-lookup"><span data-stu-id="a57a2-527">hello indexing and cataloging rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="a57a2-528">Backup Exec 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="a57a2-528">Backup Exec server failure</span></span> | <span data-ttu-id="a57a2-529">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="a57a2-529">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="a57a2-530">重建 hello 備份伺服器和執行中所述的資料庫還原[如何 toodo 手動備份和還原的備份 Exec (BEDB) 資料庫](http://www.veritas.com/docs/000041083)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-530">Rebuild hello backup server and perform database restore as detailed in [How toodo a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span></span> | <span data-ttu-id="a57a2-531">您必須重建或還原 hello 備份 Exec hello 災害復原站台伺服器。</span><span class="sxs-lookup"><span data-stu-id="a57a2-531">You must rebuild or restore hello Backup Exec server at hello disaster recovery site.</span></span> <span data-ttu-id="a57a2-532">還原 hello 資料庫 toohello 最新的點。</span><span class="sxs-lookup"><span data-stu-id="a57a2-532">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="a57a2-533">如果 hello 還原備份執行的資料庫不是最新的備份工作，同步索引和編目不需要。</span><span class="sxs-lookup"><span data-stu-id="a57a2-533">If hello restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="a57a2-534">此索引和重新掃描程序的目錄，可能會導致所有備份組 toobe 掃描，並從 hello 雲端層 toohello 本機裝置層提取。</span><span class="sxs-lookup"><span data-stu-id="a57a2-534">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="a57a2-535">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="a57a2-535">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="a57a2-536">站台失敗所產生的 hello 備份伺服器和 StorSimple hello 遺失。</span><span class="sxs-lookup"><span data-stu-id="a57a2-536">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="a57a2-537">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="a57a2-537">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="a57a2-538">先還原 StorSimple，然後再還原 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="a57a2-538">Restore StorSimple first, and then restore Backup Exec.</span></span> | <span data-ttu-id="a57a2-539">先還原 StorSimple，然後再還原 Backup Exec。</span><span class="sxs-lookup"><span data-stu-id="a57a2-539">Restore StorSimple first, and then restore Backup Exec.</span></span> <span data-ttu-id="a57a2-540">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取 hello 完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="a57a2-540">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="a57a2-541">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="a57a2-541">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="a57a2-542">參考</span><span class="sxs-lookup"><span data-stu-id="a57a2-542">References</span></span>

<span data-ttu-id="a57a2-543">下列文件的 hello 時參考這個發行項：</span><span class="sxs-lookup"><span data-stu-id="a57a2-543">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="a57a2-544">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="a57a2-544">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="a57a2-545">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="a57a2-545">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="a57a2-546">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="a57a2-546">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="a57a2-547">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="a57a2-547">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="a57a2-548">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a57a2-548">Next steps</span></span>

- <span data-ttu-id="a57a2-549">深入了解如何太[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-549">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="a57a2-550">深入了解如何 tooperform[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="a57a2-550">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
