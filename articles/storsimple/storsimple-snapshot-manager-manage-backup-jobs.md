---
title: "StorSimple Snapshot Manager 備份工作 | Microsoft Docs"
description: "描述如何使用 StorSimple Snapshot Manager MMC 嵌入式管理單元來檢視和管理已排程、目前執行中和已完成的備份作業。"
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
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="ef4d4-103">使用 StorSimple Snapshot Manager 來檢視和管理備份作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="ef4d4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ef4d4-104">Overview</span></span>
<span data-ttu-id="ef4d4-105">[範圍] 窗格中的 [作業] 節點會顯示您以互動方式或透過已設定之原則起始的 [已排程]、[過去 24 小時] 和 [執行中] 備份工作。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="ef4d4-106">本教學課程說明如何使用 [ **作業** ] 節點，以顯示已排程、最近和目前執行中之備份作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="ef4d4-107">(作業清單和對應資訊會出現在 [結果] 窗格中)。此外，您也可以以滑鼠右鍵按一下列出的作業，並查看內容功能表，其中列出可用的動作。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="ef4d4-108">檢視已排程的作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-108">View scheduled jobs</span></span>
<span data-ttu-id="ef4d4-109">請使用下列程序來檢視已排程的備份作業。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="ef4d4-110">若要檢視已排程的作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="ef4d4-111">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="ef4d4-112">在 [範圍] 窗格中，展開 [作業] 節點，然後按一下 [已排程]。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="ef4d4-113">下列資訊會出現在 [ **結果** ] 窗格中：</span><span class="sxs-lookup"><span data-stu-id="ef4d4-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="ef4d4-114">**名稱**  – 已排定之快照的名稱</span><span class="sxs-lookup"><span data-stu-id="ef4d4-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="ef4d4-115">**下次執行**  – 下次排定之快照的日期和時間</span><span class="sxs-lookup"><span data-stu-id="ef4d4-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="ef4d4-116">**上次執行**  – 最新排定之快照的日期和時間</span><span class="sxs-lookup"><span data-stu-id="ef4d4-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="ef4d4-117">若為僅一次快照，[下次執行] 和 [上次執行] 將相同。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![排定的備份工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="ef4d4-119">若要在特定工作上執行其他動作，請以滑鼠右鍵按一下 [ **結果** ] 窗格中的作業名稱，然後選取功能表選項。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="ef4d4-120">檢視最近的作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-120">View recent jobs</span></span>
<span data-ttu-id="ef4d4-121">請使用下列程序，來檢視過去 24 小時內完成的備份和還原作業。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="ef4d4-122">若要檢視最近的作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-122">To view recent jobs</span></span>
1. <span data-ttu-id="ef4d4-123">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ef4d4-124">在 [範圍] 窗格中，展開 [作業] 節點，然後按一下 [過去 24 小時]。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="ef4d4-125">[ **結果** ] 窗格會顯示過去 24 小時的備份作業 (最多可顯示 64 個作業)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="ef4d4-126">下列資訊會出現在 [結果] 窗格中，視您指定的 [檢視] 選項而定：</span><span class="sxs-lookup"><span data-stu-id="ef4d4-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="ef4d4-127">**名稱**  – 已排定之快照的名稱。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="ef4d4-128">**已啟動**  – 快照開始的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="ef4d4-129">**已停止**  – 快照完成或已終止的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="ef4d4-130">[經過時間] – [已啟動] 時間與 [已停止] 時間之間的時間量。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="ef4d4-131">**狀態**  – 最近完成之工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="ef4d4-132">**成功**  指出已順利建立備份。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="ef4d4-133">**失敗**  指出作業並未成功執行。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="ef4d4-134">**資訊**  – 失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="ef4d4-135">**已處理的位元組數 (MB)**  – 來自磁碟區群組已處理的資料量 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![過去 24 小時內執行的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="ef4d4-137">若要在特定工作上執行其他動作，請以滑鼠右鍵按一下 [ **結果** ] 窗格中的作業名稱，然後選取功能表選項。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![刪除工作](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="ef4d4-139">檢視目前執行中的作業</span><span class="sxs-lookup"><span data-stu-id="ef4d4-139">View currently running jobs</span></span>
<span data-ttu-id="ef4d4-140">請使用下列程序來檢視目前執行中的作業。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="ef4d4-141">若要檢視目前執行中的工作</span><span class="sxs-lookup"><span data-stu-id="ef4d4-141">To view currently running jobs</span></span>
1. <span data-ttu-id="ef4d4-142">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ef4d4-143">在 [範圍] 窗格中，展開 [作業] 節點，然後按一下 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="ef4d4-144">視您指定的 [檢視] 選項而定，下列資訊會出現在 [結果] 窗格中：</span><span class="sxs-lookup"><span data-stu-id="ef4d4-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="ef4d4-145">**名稱**  – 已排定之快照的名稱。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="ef4d4-146">**已啟動**  – 快照開始的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="ef4d4-147">**檢查點**  – 備份的目前動作。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="ef4d4-148">**狀態**  – 完成百分比。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="ef4d4-149">**經過時間**  – 從備份開始後所經過的時間量。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="ef4d4-150">**平均輸送量 (MB)** – 處理的總資料位元組與處理所花時間的比率 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="ef4d4-151">**處理的位元組 (MB)** – 處理的總資料位元組 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="ef4d4-152">**寫入的位元組 (MB)** – 寫入的總資料位元組 (以 MB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="ef4d4-153">它包含資料以及中繼資料，因此通常大於處理的位元組。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![目前執行中的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="ef4d4-155">若要在特定工作上執行其他動作，請以滑鼠右鍵按一下 [ **結果** ] 窗格中的作業名稱，然後選取功能表選項。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef4d4-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef4d4-156">Next steps</span></span>
* <span data-ttu-id="ef4d4-157">了解如何 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="ef4d4-158">了解如何 [使用 StorSimple Snapshot Manager 管理備份目錄](storsimple-snapshot-manager-manage-backup-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="ef4d4-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

