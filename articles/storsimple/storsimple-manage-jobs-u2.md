---
title: "aaaView 及管理 StorSimple 作業 |Microsoft 文件"
description: "描述 hello StorSimple Manager 服務作業 頁面以及 toouse 它 tootrack 最近、 目前和已排程備份工作。"
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
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="2455b-103">使用 hello StorSimple Manager 服務 tooview 及管理 StorSimple 工作 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="2455b-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="2455b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2455b-104">Overview</span></span>
<span data-ttu-id="2455b-105">hello**作業**頁面會提供單一中央入口網站檢視和管理裝置所啟動的工作連接 tooyour StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="2455b-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="2455b-106">您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="2455b-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="2455b-107">Results are presented in a tabular format.</span></span> 

![[工作] 頁面](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="2455b-109">您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="2455b-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="2455b-110">**狀態** – 工作可以是執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2455b-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="2455b-111">**From 和 To** – 工作可以篩選根據的 hello 日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="2455b-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="2455b-112">**型別**– hello 工作類型可以是備份、 手動備份、 還原、 複製、 裝置容錯移轉，建立本機固定磁碟區、 修改磁碟區、 更新、 支援套件，或虛擬裝置佈建。</span><span class="sxs-lookup"><span data-stu-id="2455b-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="2455b-113">**裝置**– 特定連接裝置 tooyour 服務上起始工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="2455b-114">hello 已篩選的工作會再製成資料表的下列屬性的 hello hello 基礎：</span><span class="sxs-lookup"><span data-stu-id="2455b-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="2455b-115">**類型** – 備份、手動備份、還原、複製、裝置容錯移轉、建立固定在本機的磁碟區、修改磁碟區、更新、支援封裝，或佈建虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="2455b-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="2455b-116">**狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2455b-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="2455b-117">**實體**– hello 工作可以與磁碟區、 備份原則或裝置產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2455b-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="2455b-118">例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="2455b-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="2455b-119">裝置工作是透過災害復原 (DR) 或還原作業而建立。</span><span class="sxs-lookup"><span data-stu-id="2455b-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="2455b-120">**裝置**– hello hello 裝置的 hello 已啟動工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="2455b-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="2455b-121">**在啟動**– hello hello 作業啟動時的時間。</span><span class="sxs-lookup"><span data-stu-id="2455b-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="2455b-122">**進度**– hello 執行工作的完成百分比。</span><span class="sxs-lookup"><span data-stu-id="2455b-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="2455b-123">對於完成的工作，百分比應該永遠是 100%。</span><span class="sxs-lookup"><span data-stu-id="2455b-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="2455b-124">hello 工作清單會重新整理每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="2455b-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="2455b-125">您可以執行下列作業相關的動作，此頁面上的 hello:</span><span class="sxs-lookup"><span data-stu-id="2455b-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="2455b-126">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="2455b-126">View job details</span></span>
* <span data-ttu-id="2455b-127">取消工作</span><span class="sxs-lookup"><span data-stu-id="2455b-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="2455b-128">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="2455b-128">View job details</span></span>
<span data-ttu-id="2455b-129">執行下列步驟 tooview hello 詳細資料的任何作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="2455b-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="2455b-130">tooview 工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="2455b-130">tooview job details</span></span>
1. <span data-ttu-id="2455b-131">在 hello**作業**頁面上，顯示您有興趣使用適當的篩選器執行查詢的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="2455b-132">您可以搜尋完成、執行中或已取消工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="2455b-133">選取一個工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-133">Select a job.</span></span>
3. <span data-ttu-id="2455b-134">在 hello hello 頁面底部，按一下**詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="2455b-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="2455b-135">在 hello**備份工作詳細資料**對話方塊中，您可以檢視 hello 狀態、 詳細資料、 時間統計資料，以及資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="2455b-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![工作詳細資料頁面](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="2455b-137">取消工作</span><span class="sxs-lookup"><span data-stu-id="2455b-137">Cancel a job</span></span>
<span data-ttu-id="2455b-138">執行下列步驟 toocancel 執行作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="2455b-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="2455b-139">某些工作，例如修改磁碟區 toochange hello 磁碟區類型，或展開磁碟區，無法取消。</span><span class="sxs-lookup"><span data-stu-id="2455b-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="2455b-140">toocancel 作業</span><span class="sxs-lookup"><span data-stu-id="2455b-140">toocancel a job</span></span>
1. <span data-ttu-id="2455b-141">在 hello**作業**頁面上，顯示 hello 執行工作的 toocancel 使用適當的篩選器執行查詢。</span><span class="sxs-lookup"><span data-stu-id="2455b-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="2455b-142">選取 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="2455b-142">Select hello job.</span></span>
3. <span data-ttu-id="2455b-143">在 hello hello 頁面底部，按一下**取消**。</span><span class="sxs-lookup"><span data-stu-id="2455b-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="2455b-144">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="2455b-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="2455b-145">即會取消此工作。</span><span class="sxs-lookup"><span data-stu-id="2455b-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2455b-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2455b-146">Next steps</span></span>
* <span data-ttu-id="2455b-147">了解如何太[管理您的 StorSimple 備份原則](storsimple-manage-backup-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="2455b-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="2455b-148">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="2455b-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

