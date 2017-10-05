---
title: "檢視和管理 StorSimple 工作 | Microsoft Docs"
description: "說明 StorSimple Manager 服務工作頁面，以及如何使用該頁面來追蹤最近、當前和排程的備份工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 6df1b27ce76de7a781ecc40af8430114d80b20d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="fe403-103">使用 StorSimple Manager 服務來檢視和管理 StorSimple 工作 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="fe403-103">Use the StorSimple Manager service to view and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="fe403-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fe403-104">Overview</span></span>
<span data-ttu-id="fe403-105">[工作]  頁面提供單一中央入口網站，可針對連接到 StorSimple Manager 服務的裝置，檢視及管理在裝置上啟動的工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="fe403-106">您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="fe403-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="fe403-107">Results are presented in a tabular format.</span></span> 

![[工作] 頁面](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="fe403-109">您可以透過篩選欄位，快速找到您所感興趣的工作，例如：</span><span class="sxs-lookup"><span data-stu-id="fe403-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="fe403-110">**狀態** – 工作可以是執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe403-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="fe403-111">**起迄** – 工作可以根據日期和時間範圍進行篩選。</span><span class="sxs-lookup"><span data-stu-id="fe403-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="fe403-112">**類型** – 工作類型可以是備份、手動備份、還原、複製、裝置容錯移轉、建立固定在本機的磁碟區、修改磁碟區、更新、支援封裝，或佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="fe403-112">**Type** – The job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="fe403-113">**裝置** – 工作會在連接到服務的特定裝置上進行初始化。</span><span class="sxs-lookup"><span data-stu-id="fe403-113">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  <span data-ttu-id="fe403-114">篩選的工作接著會根據下列屬性製成表格：</span><span class="sxs-lookup"><span data-stu-id="fe403-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="fe403-115">**類型** – 備份、手動備份、還原、複製、裝置容錯移轉、建立固定在本機的磁碟區、修改磁碟區、更新、支援封裝，或佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="fe403-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="fe403-116">**狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe403-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="fe403-117">**實體** – 工作可以與磁碟區、備份原則或裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="fe403-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="fe403-118">例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="fe403-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="fe403-119">裝置工作是透過災害復原 (DR) 或還原作業而建立。</span><span class="sxs-lookup"><span data-stu-id="fe403-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="fe403-120">**裝置** – 用來啟動工作之裝置的名稱。</span><span class="sxs-lookup"><span data-stu-id="fe403-120">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="fe403-121">**啟動於** – 啟動工作的時間。</span><span class="sxs-lookup"><span data-stu-id="fe403-121">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="fe403-122">**進度** – 執行中工作的完成度百分比。</span><span class="sxs-lookup"><span data-stu-id="fe403-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="fe403-123">對於完成的工作，百分比應該永遠是 100%。</span><span class="sxs-lookup"><span data-stu-id="fe403-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="fe403-124">工作清單每隔 30 秒會重新整理。</span><span class="sxs-lookup"><span data-stu-id="fe403-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="fe403-125">您可以在此頁面上執行下列工作相關的動作：</span><span class="sxs-lookup"><span data-stu-id="fe403-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="fe403-126">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="fe403-126">View job details</span></span>
* <span data-ttu-id="fe403-127">取消工作</span><span class="sxs-lookup"><span data-stu-id="fe403-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="fe403-128">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="fe403-128">View job details</span></span>
<span data-ttu-id="fe403-129">執行下列步驟來檢視任何工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fe403-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="fe403-130">若要檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="fe403-130">To view job details</span></span>
1. <span data-ttu-id="fe403-131">在 [工作]  頁面上，透過搭配適當的篩選器執行查詢來顯示您所感興趣的工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="fe403-132">您可以搜尋完成、執行中或已取消工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="fe403-133">選取一個工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-133">Select a job.</span></span>
3. <span data-ttu-id="fe403-134">按一下頁面底部的 [詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="fe403-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="fe403-135">在 [備份工作詳細資料]  對話方塊中，您可以檢視狀態、詳細資料、時間統計資料和資料統計資料。</span><span class="sxs-lookup"><span data-stu-id="fe403-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![工作詳細資料頁面](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="fe403-137">取消工作</span><span class="sxs-lookup"><span data-stu-id="fe403-137">Cancel a job</span></span>
<span data-ttu-id="fe403-138">執行下列步驟來取消執行中工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-138">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="fe403-139">有些工作無法取消，例如修改磁碟區以變更磁碟區類型或是展開磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe403-139">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="to-cancel-a-job"></a><span data-ttu-id="fe403-140">取消工作</span><span class="sxs-lookup"><span data-stu-id="fe403-140">To cancel a job</span></span>
1. <span data-ttu-id="fe403-141">在 [工作]  頁面上，透過搭配適當的篩選器執行查詢來顯示您要取消的執行中工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-141">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="fe403-142">選取工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-142">Select the job.</span></span>
3. <span data-ttu-id="fe403-143">按一下頁面底部的 [取消] 。</span><span class="sxs-lookup"><span data-stu-id="fe403-143">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="fe403-144">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="fe403-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="fe403-145">即會取消此工作。</span><span class="sxs-lookup"><span data-stu-id="fe403-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe403-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe403-146">Next steps</span></span>
* <span data-ttu-id="fe403-147">了解如何 [管理您的 StorSimple 備份原則](storsimple-manage-backup-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="fe403-147">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="fe403-148">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="fe403-148">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

