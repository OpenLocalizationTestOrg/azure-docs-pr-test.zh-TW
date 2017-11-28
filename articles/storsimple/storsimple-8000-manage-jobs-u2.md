---
title: "管理和檢視 StorSimple 8000 系列的作業 | Microsoft Docs"
description: "說明 StorSimple 裝置管理員服務作業刀鋒視窗，以及如何使用該視窗來追蹤最近、當前和排程的備份作業。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="1922e-103">使用 StorSimple 裝置管理員服務來檢視和管理作業 (Update 3 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="1922e-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="1922e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1922e-104">Overview</span></span>
<span data-ttu-id="1922e-105">[作業] 刀鋒視窗提供單一中央入口網站，可針對連接到 StorSimple 裝置管理員服務的裝置，檢視及管理在裝置上啟動的作業。</span><span class="sxs-lookup"><span data-stu-id="1922e-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="1922e-106">您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="1922e-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="1922e-107">Results are presented in a tabular format.</span></span>

![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="1922e-109">您可以透過篩選欄位，快速找到您所感興趣的工作，例如：</span><span class="sxs-lookup"><span data-stu-id="1922e-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="1922e-110">**狀態** – 作業可能在進行中、成功、已取消、失敗、取消中，或是成功但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1922e-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="1922e-111">**時間範圍** – 您可以根據日期和時間範圍來篩選作業。</span><span class="sxs-lookup"><span data-stu-id="1922e-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="1922e-112">範圍可以是過去 1 小時、過去 24 小時、過去 7 天、過去 30 天、過去一年，或自訂日期。</span><span class="sxs-lookup"><span data-stu-id="1922e-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="1922e-113">**類型** – 作業類型可以是排程備份、手動備份、還原備份、複製磁碟區、容錯移轉磁碟區容器、建立固定在本機的磁碟區、修改磁碟區、安裝更新、收集支援記錄檔，以及建立雲端設備。</span><span class="sxs-lookup"><span data-stu-id="1922e-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="1922e-114">**裝置** – 工作會在連接到服務的特定裝置上進行初始化。</span><span class="sxs-lookup"><span data-stu-id="1922e-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="1922e-115">篩選的工作接著會根據下列屬性製成表格：</span><span class="sxs-lookup"><span data-stu-id="1922e-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="1922e-116">**名稱** – 排程備份、手動備份、還原備份、複製磁碟區、容錯移轉磁碟區容器、建立固定在本機的磁碟區、修改磁碟區、安裝更新、收集支援記錄，以及建立雲端設備。</span><span class="sxs-lookup"><span data-stu-id="1922e-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="1922e-117">**狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1922e-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="1922e-118">**實體** – 工作可以與磁碟區、備份原則或裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="1922e-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="1922e-119">例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="1922e-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="1922e-120">裝置工作是透過災害復原 (DR) 或還原作業而建立。</span><span class="sxs-lookup"><span data-stu-id="1922e-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="1922e-121">**裝置** – 用來啟動工作之裝置的名稱。</span><span class="sxs-lookup"><span data-stu-id="1922e-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="1922e-122">**啟動於** – 啟動工作的時間。</span><span class="sxs-lookup"><span data-stu-id="1922e-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="1922e-123">**期間** – 完成作業所需要的時間。</span><span class="sxs-lookup"><span data-stu-id="1922e-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="1922e-124">工作清單每隔 30 秒會重新整理。</span><span class="sxs-lookup"><span data-stu-id="1922e-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="1922e-125">您可以在此頁面上執行下列工作相關的動作：</span><span class="sxs-lookup"><span data-stu-id="1922e-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="1922e-126">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="1922e-126">View job details</span></span>
* <span data-ttu-id="1922e-127">取消工作</span><span class="sxs-lookup"><span data-stu-id="1922e-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="1922e-128">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="1922e-128">View job details</span></span>
<span data-ttu-id="1922e-129">執行下列步驟來檢視任何工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1922e-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="1922e-130">若要檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="1922e-130">To view job details</span></span>
1. <span data-ttu-id="1922e-131">移至 StorSimple 裝置管理員服務，然後按一下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="1922e-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="1922e-132">在 [作業] 刀鋒視窗中，利用適當的篩選條件執行查詢，以顯示您感興趣的作業。</span><span class="sxs-lookup"><span data-stu-id="1922e-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="1922e-133">您可以搜尋完成、執行中或已取消工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-133">You can search for completed, running, or canceled jobs.</span></span>

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="1922e-135">選取並按一下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="1922e-135">Select and click a job.</span></span>

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="1922e-137">在 [作業詳細資料] 刀鋒視窗中，您可以檢視狀態、詳細資料、時間統計資料和資料統計資料。</span><span class="sxs-lookup"><span data-stu-id="1922e-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="1922e-139">取消工作</span><span class="sxs-lookup"><span data-stu-id="1922e-139">Cancel a job</span></span>
<span data-ttu-id="1922e-140">執行下列步驟來取消執行中工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="1922e-141">有些工作無法取消，例如修改磁碟區以變更磁碟區類型或是展開磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1922e-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="1922e-142">取消工作</span><span class="sxs-lookup"><span data-stu-id="1922e-142">To cancel a job</span></span>
1. <span data-ttu-id="1922e-143">在 [工作]  頁面上，透過搭配適當的篩選器執行查詢來顯示您要取消的執行中工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="1922e-144">選取工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-144">Select the job.</span></span>

2. <span data-ttu-id="1922e-145">用滑鼠右鍵按一下選取的作業以叫用操作功能表，然後按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="1922e-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="1922e-147">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="1922e-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="1922e-148">即會取消此工作。</span><span class="sxs-lookup"><span data-stu-id="1922e-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1922e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1922e-149">Next steps</span></span>
* <span data-ttu-id="1922e-150">了解如何 [管理您的 StorSimple 備份原則](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="1922e-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="1922e-151">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="1922e-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

