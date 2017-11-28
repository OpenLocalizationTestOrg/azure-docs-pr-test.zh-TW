---
title: "做為備份目標與 Veeam aaaStorSimple 8000 系列 |Microsoft 文件"
description: "描述 Veeam hello StorSimple 備份目標組態。"
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
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a><span data-ttu-id="1c5f0-103">使用 StorSimple 做為 Veeam 的備份目標</span><span class="sxs-lookup"><span data-stu-id="1c5f0-103">StorSimple as a backup target with Veeam</span></span>

## <a name="overview"></a><span data-ttu-id="1c5f0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1c5f0-104">Overview</span></span>

<span data-ttu-id="1c5f0-105">Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="1c5f0-106">StorSimple 位址為指數的資料成長的 hello 複雜性為 hello 在內部部署方案以及自動分層資料的延伸的 Azure 儲存體帳戶使用跨內部部署儲存體和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-106">StorSimple addresses hello complexities of exponential data growth by using an Azure Storage account as an extension of hello on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="1c5f0-107">在本文，我們會討論 StorSimple 整合 Veeam，以及整合兩種解決方案的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span></span> <span data-ttu-id="1c5f0-108">我們也會進行向上 Veeam toobest tooset 如何整合與 StorSimple 的建議。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-108">We also make recommendations on how tooset up Veeam toobest integrate with StorSimple.</span></span> <span data-ttu-id="1c5f0-109">我們延遲 tooVeeam 最佳作法、 備份架構設計人員和系統管理員的 hello 最佳方式 tooset Veeam toomeet 個別的備份需求以及服務等級協定 (Sla)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-109">We defer tooVeeam best practices, backup architects, and administrators for hello best way tooset up Veeam toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="1c5f0-110">雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="1c5f0-111">我們假設 hello 基本元件和基礎結構是在工作順序和準備 toosupport hello 概念，我們將描述。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="1c5f0-112">哪些人應閱讀本文？</span><span class="sxs-lookup"><span data-stu-id="1c5f0-112">Who should read this?</span></span>

<span data-ttu-id="1c5f0-113">最有幫助 toobackup 系統管理員、 存放裝置系統管理員，以及儲存體架構設計人員了解儲存體、 Windows Server 2012 R2、 乙太網路、 雲端服務和 Veeam，就會在本文中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="1c5f0-114">支援的版本</span><span class="sxs-lookup"><span data-stu-id="1c5f0-114">Supported versions</span></span>

-   <span data-ttu-id="1c5f0-115">Veeam 9 及更新版本</span><span class="sxs-lookup"><span data-stu-id="1c5f0-115">Veeam 9 and later versions</span></span>
-   [<span data-ttu-id="1c5f0-116">StorSimple Update 3 及更新版本</span><span class="sxs-lookup"><span data-stu-id="1c5f0-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="1c5f0-117">為什麼使用 StorSimple 做為備份目標？</span><span class="sxs-lookup"><span data-stu-id="1c5f0-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="1c5f0-118">StorSimple 是不錯的備份目標選擇，因為︰</span><span class="sxs-lookup"><span data-stu-id="1c5f0-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="1c5f0-119">它提供標準的本機儲存體備份應用程式 toouse 做為快速備份的目的地，不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="1c5f0-120">您也可以將 StorSimple 用來快速還原最新的備份。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="1c5f0-121">其雲端層與 Azure 雲端儲存體帳戶 toouse 順暢地整合符合成本效益的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="1c5f0-122">自動提供可供災害復原的異地儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-122">It automatically provides offsite storage for disaster recovery.</span></span>


## <a name="key-concepts"></a><span data-ttu-id="1c5f0-123">重要概念</span><span class="sxs-lookup"><span data-stu-id="1c5f0-123">Key concepts</span></span>

<span data-ttu-id="1c5f0-124">如同任何儲存體解決方案，hello 方案的儲存體效能 Sla，仔細評估變更與容量成長需求的速率是重大 toosuccess。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="1c5f0-125">hello 主要概念是，藉由引進雲端層，您的存取時間和輸送量 toohello 雲端扮演了基本角色 StorSimple toodo hello 能力其工作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="1c5f0-126">StorSimple 是設計的 tooprovide 儲存體 tooapplications 妥善定義的工作集的資料 （熱資料） 上運作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="1c5f0-127">在此模型中，hello 工作集的資料儲存在 hello 本機層，而且 hello 剩餘非/冷/封存的資料集是階層式的 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="1c5f0-128">此模型會以 hello 遵循圖表示。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="1c5f0-129">hello 幾乎單層綠色線條代表 hello hello 的 hello StorSimple 裝置的本機層上儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="1c5f0-130">hello 紅線表示 hello 總儲存在 hello StorSimple 解決方案，跨所有階層的資料量。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="1c5f0-131">hello 間距 hello 單層綠色線條和 hello 指數的紅色曲線表示 hello 的 hello 雲端中儲存的資料量總計。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="1c5f0-132">**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span></span>

<span data-ttu-id="1c5f0-133">請注意這種架構，與您會發現 StorSimple 是適合的 toooperate 做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="1c5f0-134">您可以使用 StorSimple 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-134">You can use StorSimple to:</span></span>

-   <span data-ttu-id="1c5f0-135">執行您最常出現的還原從 hello 本機工作集的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="1c5f0-136">使用 hello 雲端異地災害復原和較舊的資料，其中還原就都是較不頻繁。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="1c5f0-137">StorSimple 的優點</span><span class="sxs-lookup"><span data-stu-id="1c5f0-137">StorSimple benefits</span></span>

<span data-ttu-id="1c5f0-138">StorSimple 提供順暢地整合 Microsoft Azure 與內部部署解決方案，藉由運用無縫存取 tooon 內部部署和雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="1c5f0-139">StorSimple 會使用自動 hello 在內部部署裝置，具有固態裝置 (SSD) 和序列連結 SCSI (SAS) 存放裝置，與 Azure 儲存體階層處理。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="1c5f0-140">自動分層維持經常存取的本機 hello SSD 和 SAS 層上的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="1c5f0-141">它會移動不常存取的資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="1c5f0-142">StorSimple 提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="1c5f0-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="1c5f0-143">使用 hello 雲端 tooachieve 前所未有的重複資料刪除層級的唯一重複資料刪除和壓縮演算法</span><span class="sxs-lookup"><span data-stu-id="1c5f0-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="1c5f0-144">高可用性</span><span class="sxs-lookup"><span data-stu-id="1c5f0-144">High availability</span></span>
-   <span data-ttu-id="1c5f0-145">使用 Azure 異地複寫進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="1c5f0-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="1c5f0-146">與 Azure 整合</span><span class="sxs-lookup"><span data-stu-id="1c5f0-146">Azure integration</span></span>
-   <span data-ttu-id="1c5f0-147">Hello 雲端中的資料加密</span><span class="sxs-lookup"><span data-stu-id="1c5f0-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="1c5f0-148">改進災害復原和提高合規性</span><span class="sxs-lookup"><span data-stu-id="1c5f0-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="1c5f0-149">雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="1c5f0-150">壓縮和重複資料刪除，所有有 hello StorSimple 沒有。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="1c5f0-151">順暢地傳送，並擷取 hello 雲端與 hello 應用程式和檔案系統之間的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="1c5f0-152">如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="1c5f0-153">此外，您可以檢閱 hello[技術 StorSimple 8000 系列規格](storsimple-technical-specifications-and-compliance.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c5f0-154">只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="1c5f0-155">架構概觀</span><span class="sxs-lookup"><span data-stu-id="1c5f0-155">Architecture overview</span></span>

<span data-ttu-id="1c5f0-156">hello 下列表格顯示 hello 裝置模型-架構初始指導方針。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="1c5f0-157">**StorSimple 的本機和雲端儲存體容量**</span><span class="sxs-lookup"><span data-stu-id="1c5f0-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="1c5f0-158">儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-158">Storage capacity</span></span> | <span data-ttu-id="1c5f0-159">8100</span><span class="sxs-lookup"><span data-stu-id="1c5f0-159">8100</span></span> | <span data-ttu-id="1c5f0-160">8600</span><span class="sxs-lookup"><span data-stu-id="1c5f0-160">8600</span></span> |
|---|---|---|
| <span data-ttu-id="1c5f0-161">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-161">Local storage capacity</span></span> | <span data-ttu-id="1c5f0-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="1c5f0-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="1c5f0-164">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-164">Cloud storage capacity</span></span> | <span data-ttu-id="1c5f0-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="1c5f0-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-166">&gt; 500 TiB\*</span></span> |

<span data-ttu-id="1c5f0-167">\* 儲存體大小假設沒有重複資料刪除或壓縮。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="1c5f0-168">**StorSimple 的主要和次要備份容量**</span><span class="sxs-lookup"><span data-stu-id="1c5f0-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="1c5f0-169">備份案例</span><span class="sxs-lookup"><span data-stu-id="1c5f0-169">Backup scenario</span></span>  | <span data-ttu-id="1c5f0-170">本機儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-170">Local storage capacity</span></span>  | <span data-ttu-id="1c5f0-171">雲端儲存體容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="1c5f0-172">主要備份</span><span class="sxs-lookup"><span data-stu-id="1c5f0-172">Primary backup</span></span>  | <span data-ttu-id="1c5f0-173">最新的備份儲存在本機儲存體的快速復原 toomeet 復原點目標 (RPO)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="1c5f0-174">備份歷程記錄 (RPO) 可放入雲端容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="1c5f0-175">次要備份</span><span class="sxs-lookup"><span data-stu-id="1c5f0-175">Secondary backup</span></span> | <span data-ttu-id="1c5f0-176">備份資料的次要複本可儲存在雲端容量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="1c5f0-177">N/A</span><span class="sxs-lookup"><span data-stu-id="1c5f0-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="1c5f0-178">使用 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="1c5f0-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="1c5f0-179">在此案例中，StorSimple 磁碟區會呈現為 hello 備份的唯一儲存機制的 toohello 備份應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="1c5f0-180">下列圖 hello 顯示中的所有備份使用 StorSimple 都分層磁碟區的備份和還原的方案架構。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="1c5f0-182">主要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="1c5f0-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="1c5f0-183">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="1c5f0-184">hello 備份伺服器將資料寫入 toohello StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="1c5f0-185">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="1c5f0-186">快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-186">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="1c5f0-187">hello 備份伺服器會刪除過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-187">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="1c5f0-188">主要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="1c5f0-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="1c5f0-189">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="1c5f0-190">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="1c5f0-191">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="1c5f0-192">使用 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="1c5f0-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="1c5f0-193">在此案例中，StorSimple 磁碟區主要用於長期保留或封存。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="1c5f0-194">hello 下圖顯示的架構中的初始備份及還原高效能的目標磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="1c5f0-195">這些備份複製並封存的 tooa StorSimple 分層磁碟區上設定的排程。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="1c5f0-196">它是重要的 toosize 高效能磁碟區，好讓它可以處理保留原則容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-196">It is important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="1c5f0-198">次要目標備份的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="1c5f0-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="1c5f0-199">hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="1c5f0-200">hello 備份伺服器寫入資料 toohigh 能儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="1c5f0-201">hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="1c5f0-202">hello 備份伺服器複製備份 tooStorSimple 根據保留原則。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="1c5f0-203">快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-203">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="1c5f0-204">hello 備份伺服器會刪除過期的備份保留原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-204">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="1c5f0-205">次要目標還原的邏輯步驟</span><span class="sxs-lookup"><span data-stu-id="1c5f0-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="1c5f0-206">hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="1c5f0-207">hello 備份代理程式接收 hello 備份伺服器 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="1c5f0-208">hello 備份伺服器會完成 hello 還原作業。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="1c5f0-209">部署 hello 方案</span><span class="sxs-lookup"><span data-stu-id="1c5f0-209">Deploy hello solution</span></span>

<span data-ttu-id="1c5f0-210">部署 hello 方案需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-210">Deploying hello solution requires three steps:</span></span>

1. <span data-ttu-id="1c5f0-211">準備 hello 網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="1c5f0-212">部署您的 StorSimple 裝置做為備份目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="1c5f0-213">部署 Veeam。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-213">Deploy Veeam.</span></span>

<span data-ttu-id="1c5f0-214">每個步驟是在 hello 下列各節中詳細討論。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="1c5f0-215">設定 hello 網路</span><span class="sxs-lookup"><span data-stu-id="1c5f0-215">Set up hello network</span></span>

<span data-ttu-id="1c5f0-216">StorSimple 是與 hello Azure 雲端整合解決方案，因為 StorSimple 會需要使用中且正在運作的連線 toohello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-216">Because StorSimple is a solution that is integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="1c5f0-217">作業，像是雲端快照集、 資料管理和中繼資料傳輸和 tootier 較舊且較少存取的資料 tooAzure 雲端存放裝置，則使用此連接。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="1c5f0-218">Hello 方案 tooperform 最佳情況是，我們建議您遵循這些網路的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="1c5f0-219">連接您的 StorSimple 分層 tooAzure hello 連結必須符合您的頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-219">hello link that connects your StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="1c5f0-220">達到此目的藉由套用 hello 必要服務品質 (QoS) 層級 tooyour 基礎結構交換器 toomatch 您 RPO 和復原時間目標 (RTO) Sla。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-220">Achieve this by applying hello necessary Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="1c5f0-221">最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="1c5f0-222">部署 StorSimple</span><span class="sxs-lookup"><span data-stu-id="1c5f0-222">Deploy StorSimple</span></span>

<span data-ttu-id="1c5f0-223">如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-veeam"></a><span data-ttu-id="1c5f0-224">部署 Veeam</span><span class="sxs-lookup"><span data-stu-id="1c5f0-224">Deploy Veeam</span></span>

<span data-ttu-id="1c5f0-225">Veeam 安裝最佳作法，請參閱[Veeam 備份 （& s) 複寫的最佳作法](https://bp.veeam.expert/)，並讀取 hello 使用者指南 》，網址[Veeam 說明中心 （技術文件）](https://www.veeam.com/documentation-guides-datasheets.html)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read hello user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="1c5f0-226">設定 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="1c5f0-226">Set up hello solution</span></span>

<span data-ttu-id="1c5f0-227">在本節中，我們會示範一些組態範例。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="1c5f0-228">hello 下列的範例和建議事項說明 hello 最基本也最基本的實作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="1c5f0-229">此實作中可能不適用，直接 tooyour 特定的備份需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="1c5f0-230">設定 StorSimple</span><span class="sxs-lookup"><span data-stu-id="1c5f0-230">Set up StorSimple</span></span>

| <span data-ttu-id="1c5f0-231">StorSimple 部署工作</span><span class="sxs-lookup"><span data-stu-id="1c5f0-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="1c5f0-232">其他註解</span><span class="sxs-lookup"><span data-stu-id="1c5f0-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="1c5f0-233">部署您的內部部署 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="1c5f0-234">支援的版本：Update 3 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="1c5f0-235">開啟 hello 備份目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-235">Turn on hello backup target.</span></span> | <span data-ttu-id="1c5f0-236">使用這些命令 tooturn 上或備份的目標模式和 tooget 狀態為關閉。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="1c5f0-237">如需詳細資訊，請參閱[遠端連線 tooa StorSimple 裝置](storsimple-remote-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="1c5f0-238">備份模式 tooturn: `Set-HCSBackupApplianceMode -enable`。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="1c5f0-239">備份模式關閉 tooturn: `Set-HCSBackupApplianceMode -disable`。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="1c5f0-240">tooget hello 目前狀態的備份模式設定： `Get-HCSBackupApplianceMode`。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="1c5f0-241">建立您將 hello 備份資料儲存的磁碟區的一般磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="1c5f0-242">磁碟區容器中的所有資料都已刪除重複資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="1c5f0-243">StorSimple 磁碟區容器定義重複資料刪除網域。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="1c5f0-244">建立 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="1c5f0-245">建立磁碟區大小為預期的關閉 toohello 使用量越好，因為磁碟區大小會影響雲端快照集的持續時間。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="1c5f0-246">如需有關資訊 toosize 磁碟區，閱讀有關[保留原則](#retention-policies)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="1c5f0-247">使用 StorSimple 分層磁碟區，並選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="1c5f0-248">不支援只使用固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="1c5f0-249">建立所有 hello 備份目標磁碟區的唯一 StorSimple 備份原則。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="1c5f0-250">StorSimple 的備份原則定義 hello 磁碟區一致性群組。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="1c5f0-251">停用 hello 排程，因為到期 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="1c5f0-252">後處理作業會觸發快照集。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="1c5f0-253">設定 hello 主機備份伺服器儲存體</span><span class="sxs-lookup"><span data-stu-id="1c5f0-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="1c5f0-254">設定 hello 主機備份伺服器儲存體，根據 toothese 指導方針：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="1c5f0-255">不要使用合併磁碟區 (由 Windows 磁碟管理所建立)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="1c5f0-256">不支援合併磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-256">Spanned volumes are not supported.</span></span>
- <span data-ttu-id="1c5f0-257">使用 64 KB 配置單位大小的 NTFS 格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-257">Format your volumes using NTFS with 64-KB allocation unit size.</span></span>
- <span data-ttu-id="1c5f0-258">對應 hello StorSimple 磁碟區直接 toohello Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-258">Map hello StorSimple volumes directly toohello Veeam server.</span></span>
    - <span data-ttu-id="1c5f0-259">為實體伺服器使用 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-259">Use iSCSI for physical servers.</span></span>


## <a name="best-practices-for-storsimple-and-veeam"></a><span data-ttu-id="1c5f0-260">StorSimple 和 Veeam 的最佳作法</span><span class="sxs-lookup"><span data-stu-id="1c5f0-260">Best practices for StorSimple and Veeam</span></span>

<span data-ttu-id="1c5f0-261">設定您的解決方案，根據 toohello hello 下列幾節中的指導方針。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-261">Set up your solution according toohello guidelines in hello following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="1c5f0-262">作業系統最佳作法</span><span class="sxs-lookup"><span data-stu-id="1c5f0-262">Operating system best practices</span></span>

-   <span data-ttu-id="1c5f0-263">停用 Windows Server 的加密和 hello NTFS 檔案系統的重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-263">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="1c5f0-264">停用 hello StorSimple 磁碟區上的 Windows 伺服器磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-264">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="1c5f0-265">停用 Windows hello 索引 StorSimple 磁碟區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-265">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="1c5f0-266">在 hello （不是針對 hello StorSimple 磁碟區） 的來源主機上執行的防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-266">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="1c5f0-267">關閉 hello 預設[Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)工作管理員 中。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-267">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="1c5f0-268">執行下列其中一 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-268">Do this in one of hello following ways:</span></span>
    - <span data-ttu-id="1c5f0-269">關閉 Windows 工作排程器中的 hello 維護 configurator。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-269">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="1c5f0-270">從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="1c5f0-271">下載 PsExec 之後，請以系統管理員身分執行 Windows PowerShell 並輸入：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="1c5f0-272">StorSimple 最佳作法</span><span class="sxs-lookup"><span data-stu-id="1c5f0-272">StorSimple best practices</span></span>

-   <span data-ttu-id="1c5f0-273">請務必更新該 hello StorSimple 裝置時太[Update 3 或更新版本](storsimple-install-update-3.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-273">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="1c5f0-274">隔離 iSCSI 和雲端流量。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="1c5f0-275">您可以使用專用的 iSCSI 連線的 StorSimple 與 hello 備份的伺服器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-275">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
-   <span data-ttu-id="1c5f0-276">確定 StorSimple 裝置是專用的備份目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="1c5f0-277">不支援混合的工作負載，因為它們會影響 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="veeam-best-practices"></a><span data-ttu-id="1c5f0-278">Veeam 最佳作法</span><span class="sxs-lookup"><span data-stu-id="1c5f0-278">Veeam best practices</span></span>

-   <span data-ttu-id="1c5f0-279">hello Veeam 資料庫應該是本機 toohello 伺服器，而且在 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-279">hello Veeam database should be local toohello server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="1c5f0-280">災害復原，備份 hello Veeam 資料庫上的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-280">For disaster recovery, back up hello Veeam database on a StorSimple volume.</span></span>
-   <span data-ttu-id="1c5f0-281">我們支援此解決方案的 Veeam 完整和增量備份。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-281">We support Veeam full and incremental backups for this solution.</span></span> <span data-ttu-id="1c5f0-282">我們建議您不要使用綜合和差異備份。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="1c5f0-283">備份資料檔案應包含只有 hello 特定作業的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-283">Backup data files should contain only hello data for a specific job.</span></span> <span data-ttu-id="1c5f0-284">例如，不允許在不同作業之間附加媒體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-284">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="1c5f0-285">關閉作業驗證。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-285">Turn off job verification.</span></span> <span data-ttu-id="1c5f0-286">如有必要，都應該排程驗證 hello 最新的備份作業之後。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-286">If necessary, verification should be scheduled after hello latest backup job.</span></span> <span data-ttu-id="1c5f0-287">這項作業會影響您的備份時間範圍的重要 toounderstand 它。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-287">It is important toounderstand that this job affects your backup window.</span></span>
-   <span data-ttu-id="1c5f0-288">開啟媒體預先配置。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-288">Turn on media pre-allocation.</span></span>
-   <span data-ttu-id="1c5f0-289">確定已開啟平行處理。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-289">Be sure parallel processing is turned on.</span></span>
-   <span data-ttu-id="1c5f0-290">關閉壓縮。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-290">Turn off compression.</span></span>
-   <span data-ttu-id="1c5f0-291">關閉 hello 備份作業的重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-291">Turn off deduplication on hello backup job.</span></span>
-   <span data-ttu-id="1c5f0-292">設定最佳化太**LAN 目標**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-292">Set optimization too**LAN Target**.</span></span>
-   <span data-ttu-id="1c5f0-293">開啟 [建立作用中的完整備份] \(每 2 週)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-293">Turn on **Create active full backup** (every 2 weeks).</span></span>
-   <span data-ttu-id="1c5f0-294">在 hello 備份存放庫上設定**使用每個 VM 備份檔案**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-294">On hello backup repository, set up **Use per-VM backup files**.</span></span>
-   <span data-ttu-id="1c5f0-295">設定**使用每個工作的多個上傳資料流**太**8** （允許最多 16 個）。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-295">Set **Use multiple upload streams per job** too**8** (a maximum of 16 is allowed).</span></span> <span data-ttu-id="1c5f0-296">調整這個數字向上或向下根據 hello StorSimple 裝置上的 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-296">Adjust this number up or down based on CPU utilization on hello StorSimple device.</span></span>

## <a name="retention-policies"></a><span data-ttu-id="1c5f0-297">保留原則</span><span class="sxs-lookup"><span data-stu-id="1c5f0-297">Retention policies</span></span>

<span data-ttu-id="1c5f0-298">Hello 最常見的備份保留原則類型的其中一個是祖父、 父親和 Son (GFS) 原則。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-298">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="1c5f0-299">在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="1c5f0-300">此原則會產生六個 StorSimple 分層磁碟區： 一個磁碟區包含 hello 每週、 每月和每年完整備份。hello 其他五個磁碟區儲存每日增量備份。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-300">This policy results in six StorSimple tiered volumes: one volume contains hello weekly, monthly, and yearly full backups; hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="1c5f0-301">在下列範例的 hello，我們會使用 GFS 旋轉。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-301">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="1c5f0-302">hello 範例假設 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-302">hello example assumes hello following:</span></span>

-   <span data-ttu-id="1c5f0-303">使用非重複資料刪除或壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-303">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="1c5f0-304">每個完整備份為 1 TiB。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-304">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="1c5f0-305">每個每日增量備份為 500 GiB。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-305">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="1c5f0-306">四個每週備份會保留一個月。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-306">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="1c5f0-307">十二個每月備份會保留一年。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-307">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="1c5f0-308">一個每年備份會保留 10 年。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-308">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="1c5f0-309">根據上述假設 hello，建立 26 TiB StorSimple 分層 hello 每月和每年完整備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-309">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="1c5f0-310">建立 5 TiB StorSimple hello 的每日增量備份的每個分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-310">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="1c5f0-311">備份類型保留期</span><span class="sxs-lookup"><span data-stu-id="1c5f0-311">Backup type retention</span></span> | <span data-ttu-id="1c5f0-312">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-312">Size (TiB)</span></span> | <span data-ttu-id="1c5f0-313">GFS 乘數\*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-313">GFS multiplier\*</span></span> | <span data-ttu-id="1c5f0-314">總容量 (TiB)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-314">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="1c5f0-315">每週完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-315">Weekly full</span></span> | <span data-ttu-id="1c5f0-316">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-316">1</span></span> | <span data-ttu-id="1c5f0-317">4</span><span class="sxs-lookup"><span data-stu-id="1c5f0-317">4</span></span>  | <span data-ttu-id="1c5f0-318">4</span><span class="sxs-lookup"><span data-stu-id="1c5f0-318">4</span></span> |
| <span data-ttu-id="1c5f0-319">每日增量</span><span class="sxs-lookup"><span data-stu-id="1c5f0-319">Daily incremental</span></span> | <span data-ttu-id="1c5f0-320">0.5</span><span class="sxs-lookup"><span data-stu-id="1c5f0-320">0.5</span></span> | <span data-ttu-id="1c5f0-321">20 (循環數等於每個月的週數)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-321">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="1c5f0-322">12 (2 為其他配額)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-322">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="1c5f0-323">每月完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-323">Monthly full</span></span> | <span data-ttu-id="1c5f0-324">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-324">1</span></span> | <span data-ttu-id="1c5f0-325">12</span><span class="sxs-lookup"><span data-stu-id="1c5f0-325">12</span></span> | <span data-ttu-id="1c5f0-326">12</span><span class="sxs-lookup"><span data-stu-id="1c5f0-326">12</span></span> |
| <span data-ttu-id="1c5f0-327">每年完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-327">Yearly full</span></span> | <span data-ttu-id="1c5f0-328">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-328">1</span></span>  | <span data-ttu-id="1c5f0-329">10</span><span class="sxs-lookup"><span data-stu-id="1c5f0-329">10</span></span> | <span data-ttu-id="1c5f0-330">10</span><span class="sxs-lookup"><span data-stu-id="1c5f0-330">10</span></span> |
| <span data-ttu-id="1c5f0-331">GFS 需求</span><span class="sxs-lookup"><span data-stu-id="1c5f0-331">GFS requirement</span></span> |   | <span data-ttu-id="1c5f0-332">38</span><span class="sxs-lookup"><span data-stu-id="1c5f0-332">38</span></span> |   |
| <span data-ttu-id="1c5f0-333">其他配額</span><span class="sxs-lookup"><span data-stu-id="1c5f0-333">Additional quota</span></span>  | <span data-ttu-id="1c5f0-334">4</span><span class="sxs-lookup"><span data-stu-id="1c5f0-334">4</span></span>  |   | <span data-ttu-id="1c5f0-335">42 (總計 GFS 需求)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-335">42 total GFS requirement</span></span>  |
<span data-ttu-id="1c5f0-336">\*hello GFS 乘數是 hello 的數字的複本需要 tooprotect 和保留 toomeet 您備份原則的需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-336">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-veeam-storage"></a><span data-ttu-id="1c5f0-337">設定 Veeam 儲存體</span><span class="sxs-lookup"><span data-stu-id="1c5f0-337">Set up Veeam storage</span></span>

### <a name="tooset-up-veeam-storage"></a><span data-ttu-id="1c5f0-338">tooset Veeam 存放裝置</span><span class="sxs-lookup"><span data-stu-id="1c5f0-338">tooset up Veeam storage</span></span>

1.  <span data-ttu-id="1c5f0-339">Hello Veeam 備份和複寫主控台中，在**儲存機制工具**，跳過**備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-339">In hello Veeam Backup and Replication console, in **Repository Tools**, go too**Backup Infrastructure**.</span></span> <span data-ttu-id="1c5f0-340">以滑鼠右鍵按一下 [備份儲存裝置]，然後選取 [新增備份儲存裝置]。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  <span data-ttu-id="1c5f0-342">在 hello**新的備份儲存機制**對話方塊方塊中，輸入的名稱和描述 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-342">In hello **New Backup Repository** dialog box, enter a name and description for hello repository.</span></span> <span data-ttu-id="1c5f0-343">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-343">Select **Next**.</span></span>

    ![Veeam 管理主控台，名稱和描述頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  <span data-ttu-id="1c5f0-345">Hello 類型 選取**Microsoft Windows server**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-345">For hello type, select **Microsoft Windows server**.</span></span> <span data-ttu-id="1c5f0-346">選取 hello Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-346">Select hello Veeam server.</span></span> <span data-ttu-id="1c5f0-347">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-347">Select **Next**.</span></span>

    ![Veeam 管理主控台，選取備份存放庫的類型](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  <span data-ttu-id="1c5f0-349">toospecify**位置**，瀏覽並選取 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-349">toospecify **Location**, browse and select hello volume.</span></span> <span data-ttu-id="1c5f0-350">選取 hello**限制最大並行工作：**核取方塊並組 hello 值太**4**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-350">Select hello **Limit maximum concurrent tasks to:** check box and set hello value too**4**.</span></span> <span data-ttu-id="1c5f0-351">這可確保處理每個虛擬機器時，只會同時處理四個虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span></span> <span data-ttu-id="1c5f0-352">選取 hello**進階** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-352">Select hello **Advanced** button.</span></span>

    ![Veeam 管理主控台，選取磁碟區](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  <span data-ttu-id="1c5f0-354">在 hello**存放裝置的相容性設定**對話方塊中，選取 hello**使用每個 VM 備份檔案**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-354">In hello **Storage Compatibility Settings** dialog box, select hello **Use per-VM backup files** check box.</span></span>

    ![Veeam 管理主控台，存放裝置相容性設定](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  <span data-ttu-id="1c5f0-356">在 hello**新的備份儲存機制**對話方塊中，選取 hello**啟用 vPower hello 掛接伺服器 （建議選項） 上的 NFS 服務**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-356">In hello **New Backup Repository** dialog box, select hello **Enable vPower NFS service on hello mount server (recommended)** check box.</span></span> <span data-ttu-id="1c5f0-357">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-357">Select **Next**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  <span data-ttu-id="1c5f0-359">檢閱 hello 設定，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-359">Review hello settings, and then select **Next**.</span></span>

    ![Veeam 管理主控台，備份儲存機制頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    <span data-ttu-id="1c5f0-361">儲存機制會加入 toohello Veeam 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-361">A repository is added toohello Veeam server.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="1c5f0-362">設定 StorSimple 做為主要備份目標</span><span class="sxs-lookup"><span data-stu-id="1c5f0-362">Set up StorSimple as a primary backup target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c5f0-363">從已分層式的 toohello 雲端備份資料還原就會發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-363">Data restore from a backup that has been tiered toohello cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="1c5f0-364">hello 下圖顯示典型的磁碟區 tooa 備份工作的 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-364">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="1c5f0-365">在此情況下，所有的 hello 每週備份對應 toohello 星期六磁碟已滿，而 hello 增量備份對應 tooMonday 星期五累加磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-365">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="1c5f0-366">所有 hello 備份與還原就都是從 StorSimple 分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-366">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![主要備份目標組態的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="1c5f0-368">使用 StorSimple 做為主要備份目標的 GFS 排程範例</span><span class="sxs-lookup"><span data-stu-id="1c5f0-368">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="1c5f0-369">以下是四週、每月和每年的 GFS 循環排程範例：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="1c5f0-370">頻率/備份類型</span><span class="sxs-lookup"><span data-stu-id="1c5f0-370">Frequency/backup type</span></span> | <span data-ttu-id="1c5f0-371">完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-371">Full</span></span> | <span data-ttu-id="1c5f0-372">增量 (第 1-5 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-372">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="1c5f0-373">每週 (第 1 - 4 週)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-373">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="1c5f0-374">星期六</span><span class="sxs-lookup"><span data-stu-id="1c5f0-374">Saturday</span></span> | <span data-ttu-id="1c5f0-375">星期一至星期五</span><span class="sxs-lookup"><span data-stu-id="1c5f0-375">Monday-Friday</span></span> |
| <span data-ttu-id="1c5f0-376">每月</span><span class="sxs-lookup"><span data-stu-id="1c5f0-376">Monthly</span></span>  | <span data-ttu-id="1c5f0-377">星期六</span><span class="sxs-lookup"><span data-stu-id="1c5f0-377">Saturday</span></span>  |   |
| <span data-ttu-id="1c5f0-378">每年</span><span class="sxs-lookup"><span data-stu-id="1c5f0-378">Yearly</span></span> | <span data-ttu-id="1c5f0-379">星期六</span><span class="sxs-lookup"><span data-stu-id="1c5f0-379">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a><span data-ttu-id="1c5f0-380">指派 StorSimple 磁碟區 tooa Veeam 備份工作</span><span class="sxs-lookup"><span data-stu-id="1c5f0-380">Assign StorSimple volumes tooa Veeam backup job</span></span>

<span data-ttu-id="1c5f0-381">在主要備份目標案例中，建立主要 Veeam StorSimple 磁碟區的每日作業。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span></span> <span data-ttu-id="1c5f0-382">在第二個備份目標案例中，使用直接連接儲存體 (DAS)、網路連接儲存體 (NAS) 或簡單磁碟綁定 (JBOD) 儲存體，建立每日作業。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a><span data-ttu-id="1c5f0-383">tooassign StorSimple 磁碟區 tooa Veeam 備份工作</span><span class="sxs-lookup"><span data-stu-id="1c5f0-383">tooassign StorSimple volumes tooa Veeam backup job</span></span>

1.  <span data-ttu-id="1c5f0-384">在 hello Veeam 備份及複寫主控台，選取**備份 （& s) 複寫**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-384">In hello Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="1c5f0-385">以滑鼠右鍵按一下 [備份]，然後根據您的環境選取 [VMware] 或 [Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 管理主控台，新增備份作業](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  <span data-ttu-id="1c5f0-387">在 hello**新的備份工作**對話方塊方塊中，輸入的名稱和描述 hello 每日備份工作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-387">In hello **New Backup Job** dialog box, enter a name and description for hello daily backup job.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  <span data-ttu-id="1c5f0-389">虛擬機器 tooback 選取最多。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-389">Select a virtual machine tooback up to.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  <span data-ttu-id="1c5f0-391">選取您想要的 hello 值**備份 proxy**和**備份存放庫**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-391">Select hello values you want for **Backup proxy** and **Backup repository**.</span></span> <span data-ttu-id="1c5f0-392">選取的值**磁碟上的還原點 tookeep**根據 toohello RPO 和 RTO 定義您的環境上本機附加儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-392">Select a value for **Restore points tookeep on disk** according toohello RPO and RTO definitions for your environment on locally attached storage.</span></span> <span data-ttu-id="1c5f0-393">選取 [進階]。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-393">Select **Advanced**.</span></span>

    ![Veeam 管理主控台，新增備份作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. <span data-ttu-id="1c5f0-395">在 [hello**進階設定**] 對話方塊上 hello**備份**索引標籤上，選取**Incremental**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-395">In hello **Advanced Settings** dialog box, on hello **Backup** tab, select **Incremental**.</span></span> <span data-ttu-id="1c5f0-396">務必要是屬於該 hello**定期建立綜合的完整備份**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-396">Be sure that hello **Create synthetic full backups periodically** check box is cleared.</span></span> <span data-ttu-id="1c5f0-397">選取 hello**定期建立作用中的完整備份**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-397">Select hello **Create active full backups periodically** check box.</span></span> <span data-ttu-id="1c5f0-398">在下**作用中的完整備份**，選取 hello**每週的某幾天**星期六的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-398">Under **Active full backup**, select hello **Weekly on selected days** check box for Saturday.</span></span>

    ![Veeam 管理主控台，新增備份作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. <span data-ttu-id="1c5f0-400">在 hello**儲存體**索引標籤上，請確定該 hello**啟用內嵌重複資料刪除**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-400">On hello **Storage** tab, make sure that hello **Enable inline data deduplication** check box is cleared.</span></span> <span data-ttu-id="1c5f0-401">選取 hello**排除的檔案區塊，交換**核取方塊，並選取 hello**排除刪除的檔案區塊**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-401">Select hello **Exclude swap file blocks** check box, and select hello **Exclude deleted file blocks** check box.</span></span> <span data-ttu-id="1c5f0-402">設定**壓縮層級**太**無**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-402">Set **Compression level** too**None**.</span></span> <span data-ttu-id="1c5f0-403">平衡的效能和重複資料刪除，設定**儲存最佳化**太**LAN 目標**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-403">For balanced performance and deduplication, set **Storage optimization** too**LAN target**.</span></span> <span data-ttu-id="1c5f0-404">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-404">Select **OK**.</span></span>

    ![Veeam 管理主控台，新增備份作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    <span data-ttu-id="1c5f0-406">如需 Veeam 重複資料刪除和壓縮設定的相關資訊，請參閱[資料壓縮和重複資料刪除](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span></span>

7.  <span data-ttu-id="1c5f0-407">在 hello**編輯備份工作**對話方塊中，您可以選取 hello**啟用應用程式感知的處理**（選擇性） 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-407">In hello **Edit Backup Job** dialog box, you can select hello **Enable application-aware processing** check box (optional).</span></span>

    ![Veeam 管理主控台，新增備份作業客體處理頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  <span data-ttu-id="1c5f0-409">設定 hello 排程 toorun 一旦每日，您可以指定一次。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-409">Set hello schedule toorun once daily, at a time you can specify.</span></span>

    ![Veeam 管理主控台，新增備份作業排程器頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="1c5f0-411">設定 StorSimple 做為次要備份目標</span><span class="sxs-lookup"><span data-stu-id="1c5f0-411">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="1c5f0-412">從已分層式的 toohello 雲端備份資料還原發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-412">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="1c5f0-413">在此模型中，您必須擁有儲存媒體 （非 StorSimple) tooserve 暫時快取。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-413">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="1c5f0-414">例如，您可以使用獨立磁碟 (RAID) 磁碟區 tooaccommodate 空間、 輸入/輸出 (I/O) 和頻寬的備援陣列。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-414">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="1c5f0-415">我們建議使用 RAID 5、50 和 10。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-415">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="1c5f0-416">hello 遵循圖顯示典型的短期保留本機 （toohello 伺服器） 磁碟區和長期的保留封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-416">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archive volumes.</span></span> <span data-ttu-id="1c5f0-417">在此案例中，所有備份上都執行本機 hello （toohello 伺服器） RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-417">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="1c5f0-418">這些備份定期重複，並封存 tooan 封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-418">These backups are periodically duplicated and archived tooan archive volume.</span></span> <span data-ttu-id="1c5f0-419">它是本機 （toohello 伺服器） 的重要 toosize RAID 磁碟區，好讓它可以處理短期保留容量和效能需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-419">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="1c5f0-421">使用 StorSimple 做為次要備份目標 GFS 範例</span><span class="sxs-lookup"><span data-stu-id="1c5f0-421">StorSimple as a secondary backup target GFS example</span></span>

<span data-ttu-id="1c5f0-422">hello 下表顯示如何 tooset 向上備份 toorun hello 本機和 StorSimple 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-422">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="1c5f0-423">其中包含個別和總容量需求。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-423">It includes individual and total capacity requirements.</span></span>

| <span data-ttu-id="1c5f0-424">備份類型和保留期</span><span class="sxs-lookup"><span data-stu-id="1c5f0-424">Backup type and retention</span></span> | <span data-ttu-id="1c5f0-425">設定的儲存體</span><span class="sxs-lookup"><span data-stu-id="1c5f0-425">Configured storage</span></span> | <span data-ttu-id="1c5f0-426">大小 (TiB)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-426">Size (TiB)</span></span> | <span data-ttu-id="1c5f0-427">GFS 乘數</span><span class="sxs-lookup"><span data-stu-id="1c5f0-427">GFS multiplier</span></span> | <span data-ttu-id="1c5f0-428">總容量\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-428">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="1c5f0-429">第 1 週 (完整和增量)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-429">Week 1 (full and incremental)</span></span> |<span data-ttu-id="1c5f0-430">本機磁碟 (短期)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-430">Local disk (short-term)</span></span>| <span data-ttu-id="1c5f0-431">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-431">1</span></span> | <span data-ttu-id="1c5f0-432">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-432">1</span></span> | <span data-ttu-id="1c5f0-433">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-433">1</span></span> |
| <span data-ttu-id="1c5f0-434">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-434">StorSimple weeks 2-4</span></span> |<span data-ttu-id="1c5f0-435">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-435">StorSimple disk (long-term)</span></span> | <span data-ttu-id="1c5f0-436">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-436">1</span></span> | <span data-ttu-id="1c5f0-437">4</span><span class="sxs-lookup"><span data-stu-id="1c5f0-437">4</span></span> | <span data-ttu-id="1c5f0-438">4</span><span class="sxs-lookup"><span data-stu-id="1c5f0-438">4</span></span> |
| <span data-ttu-id="1c5f0-439">每月完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-439">Monthly full</span></span> |<span data-ttu-id="1c5f0-440">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-440">StorSimple disk (long-term)</span></span> | <span data-ttu-id="1c5f0-441">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-441">1</span></span> | <span data-ttu-id="1c5f0-442">12</span><span class="sxs-lookup"><span data-stu-id="1c5f0-442">12</span></span> | <span data-ttu-id="1c5f0-443">12</span><span class="sxs-lookup"><span data-stu-id="1c5f0-443">12</span></span> |
| <span data-ttu-id="1c5f0-444">每年完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-444">Yearly full</span></span> |<span data-ttu-id="1c5f0-445">StorSimple 磁碟 (長期)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-445">StorSimple disk (long-term)</span></span> | <span data-ttu-id="1c5f0-446">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-446">1</span></span> | <span data-ttu-id="1c5f0-447">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-447">1</span></span> | <span data-ttu-id="1c5f0-448">1</span><span class="sxs-lookup"><span data-stu-id="1c5f0-448">1</span></span> |
|<span data-ttu-id="1c5f0-449">GFS 磁碟區大小需求</span><span class="sxs-lookup"><span data-stu-id="1c5f0-449">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="1c5f0-450">18*</span><span class="sxs-lookup"><span data-stu-id="1c5f0-450">18*</span></span>|
<span data-ttu-id="1c5f0-451">\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule"></a><span data-ttu-id="1c5f0-452">GFS 範例排程</span><span class="sxs-lookup"><span data-stu-id="1c5f0-452">GFS example schedule</span></span>

<span data-ttu-id="1c5f0-453">每週、每月和每年排程的 GFS 循環</span><span class="sxs-lookup"><span data-stu-id="1c5f0-453">GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="1c5f0-454">週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-454">Week</span></span> | <span data-ttu-id="1c5f0-455">完整</span><span class="sxs-lookup"><span data-stu-id="1c5f0-455">Full</span></span> | <span data-ttu-id="1c5f0-456">增量 (第 1 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-456">Incremental day 1</span></span> | <span data-ttu-id="1c5f0-457">增量 (第 2 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-457">Incremental day 2</span></span> | <span data-ttu-id="1c5f0-458">增量 (第 3 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-458">Incremental day 3</span></span> | <span data-ttu-id="1c5f0-459">增量 (第 4 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-459">Incremental day 4</span></span> | <span data-ttu-id="1c5f0-460">增量 (第 5 天)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-460">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="1c5f0-461">第 1 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-461">Week 1</span></span> | <span data-ttu-id="1c5f0-462">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-462">Local RAID volume</span></span>  | <span data-ttu-id="1c5f0-463">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-463">Local RAID volume</span></span> | <span data-ttu-id="1c5f0-464">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-464">Local RAID volume</span></span> | <span data-ttu-id="1c5f0-465">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-465">Local RAID volume</span></span> | <span data-ttu-id="1c5f0-466">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-466">Local RAID volume</span></span> | <span data-ttu-id="1c5f0-467">本機 RAID 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1c5f0-467">Local RAID volume</span></span> |
| <span data-ttu-id="1c5f0-468">第 2 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-468">Week 2</span></span> | <span data-ttu-id="1c5f0-469">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-469">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="1c5f0-470">第 3 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-470">Week 3</span></span> | <span data-ttu-id="1c5f0-471">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-471">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="1c5f0-472">第 4 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-472">Week 4</span></span> | <span data-ttu-id="1c5f0-473">StorSimple 第 2-4 週</span><span class="sxs-lookup"><span data-stu-id="1c5f0-473">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="1c5f0-474">每月</span><span class="sxs-lookup"><span data-stu-id="1c5f0-474">Monthly</span></span> | <span data-ttu-id="1c5f0-475">StorSimple 每月</span><span class="sxs-lookup"><span data-stu-id="1c5f0-475">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="1c5f0-476">每年</span><span class="sxs-lookup"><span data-stu-id="1c5f0-476">Yearly</span></span> | <span data-ttu-id="1c5f0-477">StorSimple 每年</span><span class="sxs-lookup"><span data-stu-id="1c5f0-477">StorSimple yearly</span></span>  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a><span data-ttu-id="1c5f0-478">指派 StorSimple 磁碟區 tooa Veeam 複製作業</span><span class="sxs-lookup"><span data-stu-id="1c5f0-478">Assign StorSimple volumes tooa Veeam copy job</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a><span data-ttu-id="1c5f0-479">tooassign StorSimple 磁碟區 tooa Veeam 複製作業</span><span class="sxs-lookup"><span data-stu-id="1c5f0-479">tooassign StorSimple volumes tooa Veeam copy job</span></span>

1.  <span data-ttu-id="1c5f0-480">在 hello Veeam 備份及複寫主控台，選取**備份 （& s) 複寫**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-480">In hello Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="1c5f0-481">以滑鼠右鍵按一下 [備份]，然後根據您的環境選取 [VMware] 或 [Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  <span data-ttu-id="1c5f0-483">在 hello**新的備份複本工作**對話方塊方塊中，輸入的名稱和描述 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-483">In hello **New Backup Copy Job** dialog box, enter a name and description for hello job.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  <span data-ttu-id="1c5f0-485">選取您想要 tooprocess hello Vm。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-485">Select hello VMs you want tooprocess.</span></span> <span data-ttu-id="1c5f0-486">從備份中，選取，然後選取 hello 您稍早建立的每日備份。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-486">Select from backups, and then select hello daily backup that you created earlier.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  <span data-ttu-id="1c5f0-488">如有需要請從 hello 備份作業排除物件。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-488">Exclude objects from hello backup copy job, if needed.</span></span>

5.  <span data-ttu-id="1c5f0-489">選取備份的儲存機制，並將設定的值**還原點 tookeep**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-489">Select your backup repository, and set a value for **Restore points tookeep**.</span></span> <span data-ttu-id="1c5f0-490">要確定 tooselect hello**保持 hello 下列封存之用的還原點**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-490">Be sure tooselect hello **Keep hello following restore points for archival purposes** check box.</span></span> <span data-ttu-id="1c5f0-491">定義 hello 備份頻率，然後選取**進階**。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-491">Define hello backup frequency, and then select **Advanced**.</span></span>

    ![Veeam 管理主控台，新增備份複製作業頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  <span data-ttu-id="1c5f0-493">指定 hello 下列進階設定：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-493">Specify hello following advanced settings:</span></span>

    * <span data-ttu-id="1c5f0-494">在 hello**維護**索引標籤上，關閉儲存體層級的損毀保護。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-494">On hello **Maintenance** tab, turn off storage level corruption guard.</span></span>

    ![Veeam 管理主控台，新增備份複製作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * <span data-ttu-id="1c5f0-496">在 hello**儲存體**索引標籤上，確定重複資料刪除和壓縮已關閉。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-496">On hello **Storage** tab, be sure that deduplication and compression are turned off.</span></span>

    ![Veeam 管理主控台，新增備份複製作業進階設定頁面](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  <span data-ttu-id="1c5f0-498">指定直接 hello 資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-498">Specify that hello data transfer is direct.</span></span>

8.  <span data-ttu-id="1c5f0-499">定義根據 tooyour 需求 hello 備份視窗排程，然後完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-499">Define hello backup copy window schedule according tooyour needs, and then finish hello wizard.</span></span>

<span data-ttu-id="1c5f0-500">如需詳細資訊，請參閱[建立備份複製作業](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="1c5f0-501">StorSimple 雲端快照集</span><span class="sxs-lookup"><span data-stu-id="1c5f0-501">StorSimple cloud snapshots</span></span>

<span data-ttu-id="1c5f0-502">StorSimple 雲端快照集保護位於您的 StorSimple 裝置中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-502">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="1c5f0-503">建立雲端快照集是對等 tooshipping 本機備份磁帶 tooan 異地設施。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-503">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="1c5f0-504">如果您使用 Azure 地理備援儲存體，建立雲端快照是相等的 tooshipping 備份磁帶 toomultiple 站台。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="1c5f0-505">如果您需要 toorestore 裝置在損毀之後，您可能會讓其他 StorSimple 裝置上線，並且進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-505">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="1c5f0-506">Hello 容錯移轉之後，您將無法 tooaccess hello 資料 （速度雲端） 從 hello 最新的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-506">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="1c5f0-507">hello 下列章節描述如何 toocreate 簡短的指令碼 toostart 和 delete StorSimple 雲端快照在備份後的處理期間。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-507">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="1c5f0-508">手動或以程式設計方式建立的快照集未遵循 hello StorSimple 快照集的到期原則。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-508">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="1c5f0-509">這些快照集必須以手動方式或以程式設計方式刪除。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-509">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="1c5f0-510">使用指令碼啟動和刪除雲端快照集</span><span class="sxs-lookup"><span data-stu-id="1c5f0-510">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="1c5f0-511">請仔細在刪除 StorSimple 快照集之前，先評估 hello 相容性和資料保留的影響。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-511">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="1c5f0-512">如需有關如何 toorun 備份後指令碼，請參閱 hello Veeam 文件。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-512">For more information about how toorun a post-backup script, see hello Veeam documentation.</span></span>


### <a name="backup-lifecycle"></a><span data-ttu-id="1c5f0-513">備份生命週期</span><span class="sxs-lookup"><span data-stu-id="1c5f0-513">Backup lifecycle</span></span>

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="1c5f0-515">需求</span><span class="sxs-lookup"><span data-stu-id="1c5f0-515">Requirements</span></span>

-   <span data-ttu-id="1c5f0-516">執行 hello 指令碼的 hello 伺服器必須具備存取 tooAzure 雲端資源。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-516">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="1c5f0-517">hello 使用者帳戶必須擁有 hello 必要的權限。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-517">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="1c5f0-518">StorSimple hello 與備份原則相關聯的 StorSimple 磁碟區必須設定，但未開啟。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-518">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="1c5f0-519">您將需要 hello StorSimple 資源名稱、 登錄機碼、 裝置名稱和備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-519">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="1c5f0-520">toostart 或刪除的雲端快照</span><span class="sxs-lookup"><span data-stu-id="1c5f0-520">toostart or delete a cloud snapshot</span></span>

1. <span data-ttu-id="1c5f0-521">[安裝 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-521">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="1c5f0-522">[下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3. <span data-ttu-id="1c5f0-523">在 hello Azure 傳統入口網站中取得 hello 資源名稱和[StorSimple Manager 服務登錄機碼](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-523">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4. <span data-ttu-id="1c5f0-524">Hello 在伺服器上執行 hello 指令碼，請以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-524">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="1c5f0-525">輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-525">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="1c5f0-526">請注意 hello 備份原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-526">Note hello backup policy ID.</span></span>
5. <span data-ttu-id="1c5f0-527">在記事本中，請使用下列程式碼的 hello 以建立新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-527">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="1c5f0-528">複製並貼上此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-528">Copy and paste this code snippet:</span></span>
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
6. <span data-ttu-id="1c5f0-529">tooadd hello 指令碼 tooyour 備份作業，請編輯您的進階選項的 Veeam 工作。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-529">tooadd hello script tooyour backup job, edit your Veeam job advanced options.</span></span>

    ![Veeam 備份進階設定指令碼索引標籤](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

<span data-ttu-id="1c5f0-531">我們建議做為後置處理指令碼執行 StorSimple 雲端快照集備份原則，在您每日備份工作的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="1c5f0-532">如需有關如何向上 tooback 和還原您備份應用程式環境 toohelp 您符合您的 RPO 和 RTO，請參閱與您備份的架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-532">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="1c5f0-533">使用 StorSimple 做為還原來源</span><span class="sxs-lookup"><span data-stu-id="1c5f0-533">StorSimple as a restore source</span></span>

<span data-ttu-id="1c5f0-534">從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-534">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="1c5f0-535">還原的是階層式的 toohello 雲端的資料就會發生在雲端的速度。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-535">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="1c5f0-536">對於本機資料，還原發生 hello 裝置 hello 本機磁碟速度。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-536">For local data, restores occur at hello local disk speed of hello device.</span></span>

<span data-ttu-id="1c5f0-537">透過 Veeam，您可以取得快速、 更細微的檔案層級復原透過 StorSimple 透過 hello hello Veeam 主控台中的內建的總管檢視。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via hello built-in explorer views in hello Veeam console.</span></span> <span data-ttu-id="1c5f0-538">使用 Veeam 總管 toorecover 個別項目，例如電子郵件訊息、 Active Directory 物件和備份中的 SharePoint 項目。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-538">Use the Veeam Explorers toorecover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span></span> <span data-ttu-id="1c5f0-539">不會在內部部署 VM 中斷，就可以執行 hello 復原。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-539">hello recovery can be done without on-premises VM disruption.</span></span> <span data-ttu-id="1c5f0-540">您也可以進行 Azure SQL Database 和 Oracle Database 的時間點復原。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span></span> <span data-ttu-id="1c5f0-541">Veeam 和 StorSimple 可讓項目層級復原，從 Azure 快速、 輕鬆地 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-541">Veeam and StorSimple make hello process of item-level recovery from Azure fast and easy.</span></span> <span data-ttu-id="1c5f0-542">如需有關資訊 tooperform 還原，請參閱 hello Veeam 文件：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-542">For information about how tooperform a restore, see hello Veeam documentation:</span></span>

- <span data-ttu-id="1c5f0-543">若為 [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span></span>
- <span data-ttu-id="1c5f0-544">若為 [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span></span>
- <span data-ttu-id="1c5f0-545">若為 [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span></span>
- <span data-ttu-id="1c5f0-546">若為 [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span></span>
- <span data-ttu-id="1c5f0-547">若為 [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span></span>


## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="1c5f0-548">StorSimple 容錯移轉和災害復原</span><span class="sxs-lookup"><span data-stu-id="1c5f0-548">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="1c5f0-549">對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="1c5f0-550">各種因素都可能造成災害。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-550">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="1c5f0-551">hello 下表列出常見的嚴重損壞修復案例。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-551">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="1c5f0-552">案例</span><span class="sxs-lookup"><span data-stu-id="1c5f0-552">Scenario</span></span> | <span data-ttu-id="1c5f0-553">影響</span><span class="sxs-lookup"><span data-stu-id="1c5f0-553">Impact</span></span> | <span data-ttu-id="1c5f0-554">如何 toorecover</span><span class="sxs-lookup"><span data-stu-id="1c5f0-554">How toorecover</span></span> | <span data-ttu-id="1c5f0-555">注意事項</span><span class="sxs-lookup"><span data-stu-id="1c5f0-555">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="1c5f0-556">StorSimple 裝置故障</span><span class="sxs-lookup"><span data-stu-id="1c5f0-556">StorSimple device failure</span></span> | <span data-ttu-id="1c5f0-557">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-557">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="1c5f0-558">取代 hello 失敗的裝置，並執行[StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-558">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="1c5f0-559">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-559">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="1c5f0-560">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-560">All operations are at cloud speeds.</span></span> <span data-ttu-id="1c5f0-561">hello 索引和目錄重新掃描程序可能會導致所有備份組 toobe 掃描並取自 hello 雲端層 toohello 本機裝置層，這可能會很費時的程序。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-561">hello index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="1c5f0-562">Veeam 伺服器故障</span><span class="sxs-lookup"><span data-stu-id="1c5f0-562">Veeam server failure</span></span> | <span data-ttu-id="1c5f0-563">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-563">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="1c5f0-564">重建 hello 備份伺服器和執行中所述的資料庫還原[Veeam 說明中心 （技術文件）](https://www.veeam.com/documentation-guides-datasheets.html)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-564">Rebuild hello backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>  | <span data-ttu-id="1c5f0-565">您必須重建或還原 hello Veeam hello 災害復原站台伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-565">You must rebuild or restore hello Veeam server at hello disaster recovery site.</span></span> <span data-ttu-id="1c5f0-566">還原 hello 資料庫 toohello 最新的點。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-566">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="1c5f0-567">Hello Veeam 還原的資料庫不是最新的備份工作同步，索引和分類需要。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-567">If hello restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="1c5f0-568">此索引和重新掃描程序的目錄，可能會導致所有備份組 toobe 掃描，並從 hello 雲端層 toohello 本機裝置層提取。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-568">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="1c5f0-569">這會更耗費時間。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-569">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="1c5f0-570">站台失敗所產生的 hello 備份伺服器和 StorSimple hello 遺失。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-570">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="1c5f0-571">備份和還原作業會中斷。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="1c5f0-572">先還原 StorSimple，然後再還原 Veeam。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-572">Restore StorSimple first, and then restore Veeam.</span></span> | <span data-ttu-id="1c5f0-573">先還原 StorSimple，然後再還原 Veeam。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-573">Restore StorSimple first, and then restore Veeam.</span></span> <span data-ttu-id="1c5f0-574">如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取 hello 完整的資料工作集。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-574">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="1c5f0-575">所有作業都會以雲端速度進行。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-575">All operations are at cloud speeds.</span></span> |


## <a name="references"></a><span data-ttu-id="1c5f0-576">參考</span><span class="sxs-lookup"><span data-stu-id="1c5f0-576">References</span></span>

<span data-ttu-id="1c5f0-577">下列文件的 hello 時參考這個發行項：</span><span class="sxs-lookup"><span data-stu-id="1c5f0-577">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="1c5f0-578">StorSimple 多重路徑 I/O 設定</span><span class="sxs-lookup"><span data-stu-id="1c5f0-578">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="1c5f0-579">儲存體案例︰精簡佈建 (英文)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-579">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="1c5f0-580">使用 GPT 磁碟機 (英文)</span><span class="sxs-lookup"><span data-stu-id="1c5f0-580">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="1c5f0-581">設定共用資料夾的陰影複製</span><span class="sxs-lookup"><span data-stu-id="1c5f0-581">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="1c5f0-582">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c5f0-582">Next steps</span></span>

- <span data-ttu-id="1c5f0-583">深入了解如何太[從備份集還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-583">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="1c5f0-584">深入了解如何 tooperform[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5f0-584">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
