---
title: "aaaView 及管理 StorSimple 8000 系列的作業 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員服務作業 刀鋒視窗以及 toouse 它 tootrack 最近、 目前和已排程備份工作。"
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="ae228-103">使用 hello StorSimple 裝置管理員服務 tooview 及管理工作 (Update 3 及更新版本)</span><span class="sxs-lookup"><span data-stu-id="ae228-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="ae228-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ae228-104">Overview</span></span>
<span data-ttu-id="ae228-105">hello**作業**刀鋒視窗會提供單一中央入口網站檢視和管理裝置所啟動的作業已連線 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="ae228-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ae228-106">您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="ae228-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="ae228-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="ae228-107">Results are presented in a tabular format.</span></span>

![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="ae228-109">您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="ae228-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="ae228-110">**狀態** – 作業可能在進行中、成功、已取消、失敗、取消中，或是成功但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ae228-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="ae228-111">**時間範圍**– 工作可以篩選根據的 hello 日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="ae228-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="ae228-112">hello 範圍是過去 1 小時、 過去 24 小時、 過去 7 天、 過去 30 天、 過去一年或自訂的日期。</span><span class="sxs-lookup"><span data-stu-id="ae228-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="ae228-113">**型別**– hello 作業類型可以是已排程的備份、 手動備份、 還原備份複製磁碟區、 容錯移轉磁碟區容器、 建立本機固定磁碟區，修改磁碟區、 安裝更新、 收集支援記錄檔和建立雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="ae228-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="ae228-114">**裝置**– 特定連接裝置 tooyour 服務上起始工作。</span><span class="sxs-lookup"><span data-stu-id="ae228-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="ae228-115">hello 已篩選的工作會再製成資料表的下列屬性的 hello hello 基礎：</span><span class="sxs-lookup"><span data-stu-id="ae228-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="ae228-116">**名稱** – 排程備份、手動備份、還原備份、複製磁碟區、容錯移轉磁碟區容器、建立固定在本機的磁碟區、修改磁碟區、安裝更新、收集支援記錄，以及建立雲端設備。</span><span class="sxs-lookup"><span data-stu-id="ae228-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="ae228-117">**狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ae228-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="ae228-118">**實體**– hello 工作可以與磁碟區、 備份原則或裝置產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ae228-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="ae228-119">例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="ae228-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="ae228-120">裝置工作是透過災害復原 (DR) 或還原作業而建立。</span><span class="sxs-lookup"><span data-stu-id="ae228-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="ae228-121">**裝置**– hello hello 裝置的 hello 已啟動工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae228-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="ae228-122">**在啟動**– hello hello 作業啟動時的時間。</span><span class="sxs-lookup"><span data-stu-id="ae228-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="ae228-123">**持續時間**– hello 時間必要的 toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ae228-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="ae228-124">hello 工作清單會重新整理每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="ae228-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="ae228-125">您可以執行下列作業相關的動作，此頁面上的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae228-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="ae228-126">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae228-126">View job details</span></span>
* <span data-ttu-id="ae228-127">取消工作</span><span class="sxs-lookup"><span data-stu-id="ae228-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="ae228-128">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae228-128">View job details</span></span>
<span data-ttu-id="ae228-129">執行下列步驟 tooview hello 詳細資料的任何作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="ae228-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="ae228-130">tooview 工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae228-130">tooview job details</span></span>
1. <span data-ttu-id="ae228-131">在 tooyour StorSimple 裝置管理員服務的 **作業**。</span><span class="sxs-lookup"><span data-stu-id="ae228-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="ae228-132">在 hello**作業**刀鋒視窗，顯示 hello 工作，您有興趣使用適當的篩選器執行查詢。</span><span class="sxs-lookup"><span data-stu-id="ae228-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="ae228-133">您可以搜尋完成、執行中或已取消工作。</span><span class="sxs-lookup"><span data-stu-id="ae228-133">You can search for completed, running, or canceled jobs.</span></span>

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="ae228-135">選取並按一下 [作業]。</span><span class="sxs-lookup"><span data-stu-id="ae228-135">Select and click a job.</span></span>

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="ae228-137">您可以在 hello 工作詳細資料 刀鋒視窗，檢視 hello 狀態、 詳細資料、 時間統計資料和資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ae228-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="ae228-139">取消工作</span><span class="sxs-lookup"><span data-stu-id="ae228-139">Cancel a job</span></span>
<span data-ttu-id="ae228-140">執行下列步驟 toocancel 執行作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="ae228-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="ae228-141">某些工作，例如修改磁碟區 toochange hello 磁碟區類型，或展開磁碟區，無法取消。</span><span class="sxs-lookup"><span data-stu-id="ae228-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="ae228-142">toocancel 作業</span><span class="sxs-lookup"><span data-stu-id="ae228-142">toocancel a job</span></span>
1. <span data-ttu-id="ae228-143">在 hello**作業**頁面上，顯示 hello 執行工作的 toocancel 使用適當的篩選器執行查詢。</span><span class="sxs-lookup"><span data-stu-id="ae228-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="ae228-144">選取 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ae228-144">Select hello job.</span></span>

2. <span data-ttu-id="ae228-145">以滑鼠右鍵按一下 hello 選取的作業 tooinvoke hello 操作功能表上，按一下 **取消**。</span><span class="sxs-lookup"><span data-stu-id="ae228-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="ae228-147">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="ae228-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="ae228-148">即會取消此工作。</span><span class="sxs-lookup"><span data-stu-id="ae228-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae228-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae228-149">Next steps</span></span>
* <span data-ttu-id="ae228-150">了解如何太[管理您的 StorSimple 備份原則](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="ae228-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="ae228-151">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="ae228-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

