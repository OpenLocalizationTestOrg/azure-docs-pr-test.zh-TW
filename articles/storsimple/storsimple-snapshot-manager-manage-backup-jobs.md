---
title: "aaaStorSimple Snapshot Manager 備份工作 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 及管理排程、 目前執行中和已完成的備份工作。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="982c2-103">使用 StorSimple Snapshot Manager tooview 及管理備份工作</span><span class="sxs-lookup"><span data-stu-id="982c2-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="982c2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="982c2-104">Overview</span></span>
<span data-ttu-id="982c2-105">hello**作業**節點 hello**範圍** 窗格會顯示 hello**排程**，**過去 24 小時**，和**執行**的備份工作，您起始了以互動方式或依據設定的原則。</span><span class="sxs-lookup"><span data-stu-id="982c2-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="982c2-106">本教學課程說明如何使用 hello**作業**節點 toodisplay 資訊已排程、 最近，和目前執行的備份工作。</span><span class="sxs-lookup"><span data-stu-id="982c2-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="982c2-107">(hello 清單作業和對應的資訊會出現在 hello**結果**窗格。)此外，您也可以以滑鼠右鍵按一下列出的作業，並查看內容功能表，其中列出可用的動作。</span><span class="sxs-lookup"><span data-stu-id="982c2-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="982c2-108">檢視已排程的作業</span><span class="sxs-lookup"><span data-stu-id="982c2-108">View scheduled jobs</span></span>
<span data-ttu-id="982c2-109">使用下列程序 tooview 的 hello 排定的備份工作。</span><span class="sxs-lookup"><span data-stu-id="982c2-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="982c2-110">tooview 排程工作</span><span class="sxs-lookup"><span data-stu-id="982c2-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="982c2-111">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="982c2-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="982c2-112">在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**排程**。</span><span class="sxs-lookup"><span data-stu-id="982c2-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="982c2-113">hello 下列資訊會出現在 hello**結果**窗格：</span><span class="sxs-lookup"><span data-stu-id="982c2-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="982c2-114">**名稱**– hello hello 排定之快照的名稱</span><span class="sxs-lookup"><span data-stu-id="982c2-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="982c2-115">**接下來執行**– hello 的日期和時間 hello 下一個排程的快照集</span><span class="sxs-lookup"><span data-stu-id="982c2-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="982c2-116">**上次執行**– hello 的日期和時間 hello 最新的排程快照集</span><span class="sxs-lookup"><span data-stu-id="982c2-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="982c2-117">僅一次快照，如 hello **下次執行**和**上次執行**將 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="982c2-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![排定的備份工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="982c2-119">tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="982c2-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="982c2-120">檢視最近的作業</span><span class="sxs-lookup"><span data-stu-id="982c2-120">View recent jobs</span></span>
<span data-ttu-id="982c2-121">使用下列程序 tooview 備份 hello 和還原作業中完成之 hello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="982c2-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="982c2-122">tooview 最近工作</span><span class="sxs-lookup"><span data-stu-id="982c2-122">tooview recent jobs</span></span>
1. <span data-ttu-id="982c2-123">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="982c2-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="982c2-124">在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**過去 24 小時**。</span><span class="sxs-lookup"><span data-stu-id="982c2-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="982c2-125">hello**結果** 窗格會顯示備份作業的 hello 過去 24 小時 （tooa 最多 64 個工作中）。</span><span class="sxs-lookup"><span data-stu-id="982c2-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="982c2-126">hello 下列資訊會出現在 hello**結果** 窗格中的，根據 hello**檢視**您指定的選項：</span><span class="sxs-lookup"><span data-stu-id="982c2-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="982c2-127">**名稱**– hello hello 排定之快照的名稱。</span><span class="sxs-lookup"><span data-stu-id="982c2-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="982c2-128">**啟動**– hello 開始日期和時間時 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="982c2-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="982c2-129">**停止**– hello 或日期和時間時 hello 快照集完成已終止。</span><span class="sxs-lookup"><span data-stu-id="982c2-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="982c2-130">**經過**– hello 一段時間之間 hello**已啟動**和**已停止**時間。</span><span class="sxs-lookup"><span data-stu-id="982c2-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="982c2-131">**狀態**– hello hello 最近完成的作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="982c2-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="982c2-132">**成功**指出該 hello 備份已成功建立。</span><span class="sxs-lookup"><span data-stu-id="982c2-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="982c2-133">**無法**指出 hello 工作執行成功。</span><span class="sxs-lookup"><span data-stu-id="982c2-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="982c2-134">**資訊**– hello hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="982c2-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="982c2-135">**已處理的位元組 (MB)** – hello 數量 （以 mb 為單位） 已處理的 hello 磁碟區群組中的資料。</span><span class="sxs-lookup"><span data-stu-id="982c2-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![執行在 hello 過去 24 小時內的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="982c2-137">tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="982c2-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![刪除工作](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="982c2-139">檢視目前執行中的作業</span><span class="sxs-lookup"><span data-stu-id="982c2-139">View currently running jobs</span></span>
<span data-ttu-id="982c2-140">使用下列程序 tooview 作業目前正在執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="982c2-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="982c2-141">tooview 目前執行的工作</span><span class="sxs-lookup"><span data-stu-id="982c2-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="982c2-142">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="982c2-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="982c2-143">在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="982c2-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="982c2-144">根據 hello**檢視**選項指定，hello 下列資訊會出現在 hello**結果**窗格：</span><span class="sxs-lookup"><span data-stu-id="982c2-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="982c2-145">**名稱**– hello hello 排定之快照的名稱。</span><span class="sxs-lookup"><span data-stu-id="982c2-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="982c2-146">**啟動**– hello 開始日期和時間時 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="982c2-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="982c2-147">**檢查點**– hello 的 hello 備份目前的動作。</span><span class="sxs-lookup"><span data-stu-id="982c2-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="982c2-148">**狀態**– hello 完成百分比。</span><span class="sxs-lookup"><span data-stu-id="982c2-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="982c2-149">**經過**– hello hello 備份開始後經過的時間量。</span><span class="sxs-lookup"><span data-stu-id="982c2-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="982c2-150">**平均輸送量 (MB)** – 處理 (MBs) 所花費的時間總計的資料處理 toothat 的位元組總數的比率。</span><span class="sxs-lookup"><span data-stu-id="982c2-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="982c2-151">**處理的位元組 (MB)** – 處理的總資料位元組 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="982c2-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="982c2-152">**寫入的位元組 (MB)** – 寫入的總資料位元組 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="982c2-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="982c2-153">它包含 hello 資料以及 hello 中繼資料，並因此大於通常 hello 處理的位元組。</span><span class="sxs-lookup"><span data-stu-id="982c2-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![目前執行中的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="982c2-155">tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="982c2-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="982c2-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="982c2-156">Next steps</span></span>
* <span data-ttu-id="982c2-157">了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="982c2-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="982c2-158">了解如何太[使用 StorSimple Snapshot Manager toomanage hello 備份類別目錄](storsimple-snapshot-manager-manage-backup-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="982c2-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

